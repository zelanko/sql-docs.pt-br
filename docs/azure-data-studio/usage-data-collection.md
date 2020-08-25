---
title: Habilitar ou desabilitar a coleta de dados de uso e o relatório de falha
description: Este artigo explica como controlar se dados de relatórios de falha e de uso são coletados e enviados à Microsoft.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, maghan, sstein
ms.custom: seodec18; seo-lt-2019
ms.date: 09/24/2018
ms.openlocfilehash: 5d65a1333f3fc0f41bdcb5b7ac1f5284f32a03cc
ms.sourcegitcommit: dc8a30a4a27e15fc6671ca2674da9b7c637ec255
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/21/2020
ms.locfileid: "88745536"
---
# <a name="enable-or-disable-usage-data-collection-for-azure-data-studio"></a>Habilitar ou desabilitar a coleta de dados de uso para o Azure Data Studio

## <a name="how-to-disable-telemetry-reporting"></a>Como desabilitar relatórios de telemetria

O Azure Data Studio coleta dados de uso e os envia à Microsoft para ajudar a aprimorar nossos produtos e serviços. Para saber mais, leia a [política de privacidade](https://go.microsoft.com/fwlink/?LinkID=528096&clcid=0x409).

Se não quiser enviar dados de uso para a Microsoft, você poderá definir a configuração *telemetry.enableTelemetry* como *falso*.

Para silenciar todos os eventos de telemetria do Azure Data Studio, em **Arquivo** > **Preferências** > **Configurações**, adicione a seguinte opção:

```json
    "telemetry.enableTelemetry": false
```

**Aviso Importante**: Esta opção requer a reinicialização do Azure Data Studio para entrar em vigor. 

## <a name="how-to-disable-crash-reporting"></a>Como desabilitar o relatório de falhas

Para desabilitar o relatório de falhas, em **Arquivo** > **Preferências** > **Configurações**, adicione a seguinte opção:

```json
    "telemetry.enableCrashReporter": false
```

**Aviso Importante**: Esta opção requer a reinicialização do Azure Data Studio para entrar em vigor.

## <a name="additional-resources"></a>Recursos adicionais
- [Configurações do Workspace e do Usuário](settings.md)
