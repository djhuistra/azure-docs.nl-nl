---
title: In deze snelstart wordt uitgelegd hoe u een X.509-apparaat kunt registreren bij Azure Device Provisioning Service met behulp van Python | Microsoft Docs
description: In deze snelstart registreert u X.509-apparaten bij Azure IoT Hub Device Provisioning Service met behulp van Python
author: wesmc7777
ms.author: wesmc
ms.date: 01/25/2018
ms.topic: quickstart
ms.service: iot-dps
services: iot-dps
manager: timlt
ms.devlang: python
ms.custom: mvc
ms.openlocfilehash: 84ec165a78f873f6378e840d7f339cb7590dc098
ms.sourcegitcommit: ad08b2db50d63c8f550575d2e7bb9a0852efb12f
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/26/2018
ms.locfileid: "47227381"
---
# <a name="quickstart-enroll-x509-devices-to-the-device-provisioning-service-using-python"></a>Snelstart: X.509-apparaten registreren bij Device Provisioning Service met behulp van Python

[!INCLUDE [iot-dps-selector-quick-enroll-device-x509](../../includes/iot-dps-selector-quick-enroll-device-x509.md)]

Apparaten worden geregistreerd op een exemplaar van de inrichtingsservice door een [registratiegroep](concepts-service.md#enrollment-group) of een [afzonderlijke inschrijving](concepts-service.md#individual-enrollment) te maken. In deze snelstart wordt uitgelegd hoe u met Python programmatisch een [registratiegroep](concepts-service.md#enrollment-group) kunt maken die gebruikmaakt van tussenliggende of hoofd-CA X.509-certificaten. Een registratiegroep beheert de toegang tot de inrichtingsservice voor apparaten die een gemeenschappelijk handtekeningcertificaat in hun certificaatketen delen. De registratiegroep wordt gemaakt met behulp van de [Python Provisioning Service-SDK](https://github.com/Azure/azure-iot-sdk-python/tree/master/provisioning_service_client) en een Python-voorbeeldtoepassing. Er wordt nog gewerkt aan het maken van afzonderlijke inschrijvingen via de *Python Provisioning Service-SDK*. Zie [Apparaattoegang tot de inrichtingsservice beheren met X.509-certificaten](./concepts-security.md#controlling-device-access-to-the-provisioning-service-with-x509-certificates) voor meer informatie. Zie [Overzicht van beveiliging op basis van X.509-CA-certificaten](https://docs.microsoft.com/azure/iot-hub/iot-hub-x509ca-overview) voor meer informatie over het gebruik vanop X.509-certificaten gebaseerde Public Key Infrastructure (PKI) met Azure IoT Hub en Device Provisioning Service. 

Voor deze snelstart wordt aangenomen dat u al een IoT-hub en Device Provisioning Service-exemplaar hebt gemaakt. Als u deze resources niet al hebt gemaakt, voert u de snelstart [IoT Hub Device Provisioning Service instellen met Azure Portal](./quick-setup-auto-provision.md) uit voordat u verdergaat met dit artikel.

Hoewel de stappen in dit artikel zowel op Windows- als op Linux-computers werken, is dit artikel ontwikkeld voor een Windows-ontwikkelcomputer.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]


## <a name="prerequisites"></a>Vereisten

- Installeer [Python 2.x of 3.x](https://www.python.org/downloads/). Zorg ervoor dat u de 32-bits of 64-bits installatie gebruikt, zoals vereist door uw configuratie. Zorg ervoor dat u Python toevoegt aan uw platformspecifieke omgevingsvariabelen als u hierom wordt gevraagd tijdens de installatie.
- [Installeer of upgrade *pip*, het Python-pakketbeheersysteem](https://pip.pypa.io/en/stable/installing/).
- Installeer [Git](https://git-scm.com/download/).



## <a name="prepare-test-certificates"></a>Testcertificaten voorbereiden

Voor deze snelstart hebt u een .pem- of een .cer-bestand met het openbare gedeelte van een tussenliggend of hoofd-CA x.509-certificaat nodig. Dit certificaat moet worden geüpload naar uw inrichtingsservice en door de service worden geverifieerd. 

De [Azure IoT C-SDK](https://github.com/Azure/azure-iot-sdk-c) bevat testhulpmiddelen waarmee u een X.509-certificaatketen kunt maken, een basis- of tussencertificaat kunt uploaden vanuit die keten en een bewijs van eigendom kunt uitvoeren met de service om het certificaat te verifiëren. Certificaten die zijn gemaakt met de SDK-hulpmiddelen zijn alleen ontworpen voor **ontwikkeltesten**. Deze certificaten **mogen niet in productie worden gebruikt**. Ze bevatten in code vastgelegde wachtwoorden ('1234') die na 30 dagen verlopen. Zie [Een x.509-CA-certificaat ophalen](https://docs.microsoft.com/azure/iot-hub/iot-hub-x509ca-overview#how-to-get-an-x509-ca-certificate) in de documentatie van Azure IoT Hub voor meer informatie over het verkrijgen van certificaten die geschikt zijn voor productiegebruik.

Voer de volgende stappen uit om deze testhulpmiddelen te gebruiken om certificaten te genereren: 
 
1. Open een opdrachtprompt of Git Bash-shell en wijzig deze in een werkmap op uw computer. Voer de volgende opdracht uit voor het klonen van de [Azure IoT C SDK](https://github.com/Azure/azure-iot-sdk-c) GitHub-opslagplaats:
    
  ```cmd/sh
  git clone https://github.com/Azure/azure-iot-sdk-c.git --recursive
  ```

  De grootte van deze opslagplaats is momenteel ongeveer 220 MB. Deze bewerking kan enkele minuten in beslag nemen.

  De testhulpmiddelen bevinden zich in de *azure-iot-sdk-c/tools/CACertificates* van de opslagplaats die u hebt gekloond.    

2. Volg de stappen in [Managing test CA certificates for samples and tutorials](https://github.com/Azure/azure-iot-sdk-c/blob/master/tools/CACertificates/CACertificateOverview.md) (CA-testcertificaten voor voorbeelden en zelfstudies beheren). 


## <a name="modify-the-python-sample-code"></a>De Python-voorbeeldcode wijzigen

In deze sectie ziet u hoe u de inrichtingsgegevens van het X.509-apparaat toevoegt aan de voorbeeldcode. 

1. Start een teksteditor en maak een nieuw bestand **EnrollmentGroup.py**.

1. Voeg de volgende `import`-instructies en -variabelen aan het begin van het bestand **EnrollmentGroup.py** toe. Vervang vervolgens `dpsConnectionString` door uw verbindingsreeks die is te vinden onder **Gedeeld toegangsbeleid** in **Device Provisioning Service** op **Azure Portal**. Vervang de tijdelijke aanduiding voor het certificaat door het certificaat dat u eerder hebt gemaakt in [Testcertificaten voorbereiden](quick-enroll-device-x509-python.md#prepare-test-certificates). Maak ten slotte een unieke `registrationid` en zorg dat deze alleen bestaat uit kleine letters en afbreekstreepjes.  
   
    ```python
    from provisioningserviceclient import ProvisioningServiceClient
    from provisioningserviceclient.models import EnrollmentGroup, AttestationMechanism

    CONNECTION_STRING = "{dpsConnectionString}"

    SIGNING_CERT = """-----BEGIN CERTIFICATE-----
    XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    -----END CERTIFICATE-----"""

    GROUP_ID = "{registrationid}"
    ```

1. Voeg de volgende functie en functieaanroep toe om het aanmaken van de groepsinschrijving te implementeren:
   
    ```python
    def main():
        print ( "Initiating enrollment group creation..." )

        psc = ProvisioningServiceClient.create_from_connection_string(CONNECTION_STRING)
        att = AttestationMechanism.create_with_x509_signing_certs(SIGNING_CERT)
        eg = EnrollmentGroup.create(GROUP_ID, att)

        eg = psc.create_or_update(eg)
    
        print ( "Enrollment group created." )

    if __name__ == '__main__':
        main()
    ```

1. Sla het bestand **EnrollmentGroup.py** op en sluit het.
 

## <a name="run-the-sample-group-enrollment"></a>De voorbeeldgroepsinschrijving uitvoeren

1. Open een opdrachtprompt en voer de volgende opdracht uit om de [azure-iot-provisioning-device-client](https://pypi.org/project/azure-iot-provisioning-device-client) te installeren.

    ```cmd/sh
    pip install azure-iothub-provisioningserviceclient    
    ```

2. Voer in de opdrachtprompt het script uit.

    ```cmd/sh
    python EnrollmentGroup.py
    ```

3. Houd de uitvoer in de gaten voor een geslaagde inschrijving.

4. Navigeer naar de inrichtingsservice in Azure Portal. Klik op **Inschrijvingen beheren**. U ziet dat de groep X.509-apparaten wordt weergegeven op het tabblad **Inschrijvingsgroepen** met de naam `registrationid` die u eerder hebt gemaakt. 

    ![De X.509-inschrijving controleren in de portal](./media/quick-enroll-device-x509-python/1.png)  


## <a name="clean-up-resources"></a>Resources opschonen
Als u van plan bent om het voorbeeld van de Java.js-service te verkennen, verwijdert u de resources die u in deze quickstart hebt gemaakt, niet. Als u niet wilt doorgaan, gebruikt u de volgende stappen om alle resources die via deze Snelstartgids zijn gemaakt, te verwijderen.

1. Sluit het uitvoervenster van het Java-voorbeeld op de computer.
1. Sluit het venster voor de _X.509-certificaatgenerator_ op de computer.
1. Navigeer naar Device Provisioning Service in Azure Portal, klik op **Registraties beheren** en selecteer vervolgens het tabblad **Registratiegroepen**. Selecteer de *GROEPSNAAM* van de X.509-apparaten die u hebt ingeschreven met behulp van deze quickstart. Klik vervolgens op de knop **Verwijderen** boven aan de blade.  


## <a name="next-steps"></a>Volgende stappen
In deze quickstart hebt u een gesimuleerde groep met X.509-apparaten ingeschreven met Device Provisioning Service. Voor meer informatie over device provisioning, gaat u verder met de zelfstudie voor het instellen van Device Provisioning Service in Azure Portal. 

> [!div class="nextstepaction"]
> [Zelfstudies over Azure IoT Hub Device Provisioning Service](./tutorial-set-up-cloud.md)
