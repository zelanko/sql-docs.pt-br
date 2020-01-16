---
title: Habilitar ou desabilitar a coleta de dados de uso e o relatório de falha
titleSuffix: Azure Data Studio
description: Este artigo explica como controlar se dados de relatórios de falha e de uso são coletados e enviados à Microsoft.
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18; seo-lt-2019
ms.date: 09/24/2018
ms.openlocfilehash: 416c22aa04e289e7959e41924344666e4329ecf1
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957000"
---
# <a name="enable-or-disable-usage-data-collection-for-includename-sosincludesname-sos-shortmd"></a>Habilitar ou desabilitar a coleta de dados de uso para [!INCLUDE[name-sos](../includes/name-sos-short.md)]

## <a name="how-to-disable-telemetry-reporting"></a>Como desabilitar relatórios de telemetria

O [!INCLUDE[name-sos](../includes/name-sos-short.md)] coleta dados de uso e os envia à Microsoft para ajudar a melhorar nossos produtos e serviços. Para saber mais, leia a [política de privacidade](https://go.microsoft.com/fwlink/?LinkID=528096&clcid=0x409).

Se não quiser enviar dados de uso para a Microsoft, você poderá definir a configuração *telemetry.enableTelemetry* como *falso*.

Para silenciar todos os eventos de telemetria de [!INCLUDE[name-sos](../includes/name-sos-short.md)], em **Arquivo** > **Preferências** > **Configurações**, adicione a seguinte opção:

```json
    "telemetry.enableTelemetry": false
```

**Aviso Importante**: Esta opção requer a reinicialização do [!INCLUDE[name-sos](../includes/name-sos-short.md)] para entrar em vigor. 

## <a name="how-to-disable-crash-reporting"></a>Como desabilitar o relatório de falhas

Para desabilitar o relatório de falhas, em **Arquivo** > **Preferências** > **Configurações**, adicione a seguinte opção:

```json
    "telemetry.enableCrashReporter": false
```

**Aviso Importante**: Esta opção requer a reinicialização do [!INCLUDE[name-sos](../includes/name-sos-short.md)] para entrar em vigor.

## <a name="additional-resources"></a>Recursos adicionais
- [Configurações do Workspace e do Usuário](settings.md)
