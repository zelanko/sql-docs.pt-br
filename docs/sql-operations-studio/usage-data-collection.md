---
title: Habilitar ou desabilitar a coleta de dados de uso e falhas de emissão de relatórios para o Studio de operações do SQL (visualização) | Microsoft Docs
description: Este artigo explica como controlar se os dados de relatório de falhas e de uso são coletados e enviados à Microsoft.
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3fbf952360599642497c1d7109229cba89728d61
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="enable-or-disable-usage-data-collection-for-includename-sosincludesname-sos-shortmd"></a>Habilitar ou desabilitar a coleta de dados de uso para [!INCLUDE[name-sos](../includes/name-sos-short.md)]

## <a name="how-to-disable-telemetry-reporting"></a>Como desabilitar o relatório de telemetria

[!INCLUDE[name-sos](../includes/name-sos-short.md)] coleta dados de uso e a envia para a Microsoft para ajudar a melhorar nossos produtos e serviços. Para saber mais, leia o [privacidade](https://go.microsoft.com/fwlink/?LinkID=528096&clcid=0x409).

Se você não deseja enviar dados de uso à Microsoft, você pode definir o *telemetry.enableTelemetry* definindo como *false*.

Para todos os eventos de telemetria de silêncio [!INCLUDE[name-sos](../includes/name-sos-short.md)], de **arquivo** > **preferências** > **configurações**, adicione a seguinte opção:

```json
    "telemetry.enableTelemetry": false
```

**Aviso importante**: essa opção requer a reinicialização do [!INCLUDE[name-sos](../includes/name-sos-short.md)] entrem em vigor. 

## <a name="how-to-disable-crash-reporting"></a>Como desabilitar o relatório de falhas

Para desabilitar o relatório de falhas de **arquivo** > **preferências** > **configurações**, adicione a seguinte opção:

```json
    "telemetry.enableCrashReporter": false
```

**Aviso importante**: essa opção requer a reinicialização do [!INCLUDE[name-sos](../includes/name-sos-short.md)] entrem em vigor.

## <a name="additional-resources"></a>Recursos adicionais
- [Configurações de usuário e o espaço de trabalho](settings.md)