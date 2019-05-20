---
title: Tarefa do Hive do Hadoop | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hadoophivetask.f1
ms.assetid: 10ff37c0-9f3f-442a-889b-c351afbdc74c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1d9ae752dabee68d6fae786675e640773009f4b7
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65727617"
---
# <a name="hadoop-hive-task"></a>Tarefa do Hive do Hadoop

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Use a Tarefa do Hive do Hadoop para executar o script de Hive em um cluster Hadoop.  
  
 Para adicionar uma Tarefa do Hive do Hadoop, arraste-a e solte-a para o designer. Em seguida, clique duas vezes na tarefa, ou clique com o botão direito do mouse e clique em **Editar**para abrir a caixa de diálogo **Editor de Tarefa do Hive do Hadoop** .  
  
 ![Editor de Tarefa do Hive do Hadoop](../../integration-services/control-flow/media/hadoop-hive-task.png "Editor de Tarefa do Hive do Hadoop")  
  
## <a name="options"></a>Opções  
 Configure as opções a seguir na caixa de diálogo **Editor de Tarefa do Hive do Hadoop** .  
  
|Campo|Descrição|  
|-----------|-----------------|  
|**Conexão do Hadoop**|Especifique um gerenciador de conexões do Hadoop existente ou crie um novo. Esse gerenciador de conexões indica onde o serviço WebHCat está hospedado.|  
|**SourceType**|Especifique o tipo de fonte da consulta. Os valores disponíveis são **ScriptFile** e **DirectInput**.|  
|**InlineScript**|Quando o valor de **SourceType** for **DirectInput**, especifique o script do Hive.|  
|**HadoopScriptFilePath**|Quando o valor de **SourceType** for **ScriptFile**, especifique o caminho do arquivo de script no Hadoop.|  
|**TimeoutInMinutes**|Especifique um valor de tempo limite em minutos. O trabalho do Hadoop para se não tiver sido concluído antes do tempo limite ser decorrido. Especifique 0 para agendar o trabalho do Hadoop para executar de forma assíncrona.|  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciador de conexões do Hadoop](../../integration-services/connection-manager/hadoop-connection-manager.md)  
  
  
