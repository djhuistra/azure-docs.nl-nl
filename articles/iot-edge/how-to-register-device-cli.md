---
title: Registreer een nieuwe Azure IoT Edge-apparaat (CLI) | Microsoft Docs
description: De IoT-extensie voor Azure CLI gebruiken om een nieuwe IoT Edge-apparaat te registreren
author: kgremban
manager: timlt
ms.author: kgremban
ms.date: 07/27/2018
ms.topic: conceptual
ms.reviewer: menchi
ms.service: iot-edge
services: iot-edge
ms.openlocfilehash: ee5e68d45c7d966619238312dabedc1628a4bf61
ms.sourcegitcommit: 32d218f5bd74f1cd106f4248115985df631d0a8c
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/24/2018
ms.locfileid: "46998029"
---
# <a name="register-a-new-azure-iot-edge-device-with-azure-cli"></a>Een nieuw Azure IoT Edge-apparaat registreren bij Azure CLI

Voordat u uw IoT-apparaten met Azure IoT Edge gebruiken kunt, moet u hen registreert bij uw IoT-hub. Wanneer u een apparaat hebt geregistreerd, ontvangt u een verbindingsreeks die kan worden gebruikt voor het instellen van uw apparaat voor Edge-werkbelastingen. 

[Azure CLI](https://docs.microsoft.com/cli/azure?view=azure-cli-latest) is een open-source, cross-platform opdrachtregelprogramma voor het beheren van Azure-resources, zoals IoT Edge. Hiermee kunt u voor het beheren van Azure IoT Hub-resources, device provisioning service-exemplaren en gekoppelde hubs buiten het vak. Azure CLI verrijkt de nieuwe IoT-extensie met functies zoals Apparaatbeheer en de volledige functionaliteit van IoT Edge.

In dit artikel bevat informatie over het registreren van een nieuwe IoT Edge-apparaat met behulp van Azure CLI.

## <a name="prerequisites"></a>Vereisten

* Een [IoT-hub](../iot-hub/iot-hub-create-using-cli.md) in uw Azure-abonnement. 
* [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli) in uw omgeving. Uw Azure CLI-versie moet ten minste 2.0.24 of hoger. Gebruik `az –-version` om de versie te valideren. In deze versie worden az-extensie-opdrachten ondersteund en is voor het eerst het Knack-opdrachtframework opgenomen. 
* De [IoT-extensie voor Azure CLI](https://github.com/Azure/azure-iot-cli-extension).

## <a name="create-a-device"></a>Maken van een apparaat

Gebruik de volgende opdracht om te maken van een nieuwe apparaat-id in uw IoT-hub: 

   ```cli
   az iot hub device-identity create --device-id [device id] --hub-name [hub name] --edge-enabled
   ```

Met deze opdracht worden drie parameters:
* **apparaat-id**: Geef een beschrijvende naam die uniek is voor uw IoT-hub.
* **naam van de hub**: Geef de naam van uw IoT-hub.
* **Edge-functionaliteit**: deze parameter geeft aan dat het apparaat voor gebruik met IoT Edge.

   ![Een IoT Edge-apparaat maken](./media/how-to-register-device-cli/Create-edge-device.png)

## <a name="view-all-devices"></a>Alle apparaten weergeven

Gebruik de volgende opdracht om alle apparaten in uw IoT-hub weer te geven:

   ```cli
   az iot hub device-identity list --hub-name [hub name]
   ```

Een apparaat dat is geregistreerd als een IoT Edge-apparaat de eigenschap heeft **capabilities.iotEdge** ingesteld op **waar**. 

## <a name="retrieve-the-connection-string"></a>De verbindingsreeks ophalen

Wanneer u klaar bent om uw apparaat instellen, moet u de verbindingsreeks die is gekoppeld aan uw fysieke apparaat met de identiteit van de IoT-hub. Gebruik de volgende opdracht uit om te retourneren van de verbindingsreeks voor een enkel apparaat:

   ```cli
   az iot hub device-identity show-connection-string --device-id [device id] --hub-name [hub name] 
   ```

De apparaat-id-parameter is hoofdlettergevoelig. Kopieer niet de aanhalingstekens rond de verbindingsreeks. 

## <a name="next-steps"></a>Volgende stappen

Meer informatie over het [modules implementeert op een apparaat met Azure CLI](how-to-deploy-modules-cli.md)
