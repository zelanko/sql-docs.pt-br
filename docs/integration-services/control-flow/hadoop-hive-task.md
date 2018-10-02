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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ba25c8b70ad39c073c713a79381b058ece4599ec
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47749764"
---
# <a name="hadoop-hive-task"></a>Tarefa do Hive do Hadoop
  Use a Tarefa do Hive do Hadoop para executar o script de Hive em um cluster Hadoop.  
  
 Para adicionar uma Tarefa do Hive do Hadoop, arraste-a e solte-a para o designer. Em seguida, clique duas vezes na tarefa, ou clique com o botão direito do mouse e clique em **Editar**para abrir a caixa de diálogo **Editor de Tarefa do Hive do Hadoop** .  
  
 ![Editor de Tarefa do Hive do Hadoop](../../integration-services/control-flow/media/hadoop-hive-task.png "Editor de Tarefa do Hive do Hadoop")  
  
## <a name="options"></a>Opções  
 Configure as opções a seguir na caixa de diálogo **Editor de Tarefa do Hive do Hadoop** .  
  
|Campo|Descrição|  
|-----------|-----------------|  
|**Conexão do Hadoop**|Especifique um gerenciador de conexões do Hadoop existente ou crie um novo. Esse gerenciador de conexões indica o local em que o serviço WebHCat está hospedado.|  
|**SourceType**|Especifique o tipo de fonte da consulta. Os valores disponíveis são **ScriptFile** e **DirectInput**.|  
|**InlineScript**|Quando o valor de **SourceType** for **DirectInput**, especifique o script do Hive.|  
|**HadoopScriptFilePath**|Quando o valor de **SourceType** for **ScriptFile**, especifique o caminho do arquivo de script no Hadoop.|  
|**TimeoutInMinutes**|Especifique um valor de tempo limite em minutos. O trabalho do Hadoop para se não tiver sido concluído antes do tempo limite ser decorrido. Especifique 0 para agendar o trabalho do Hadoop para executar de forma assíncrona.|  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciador de conexões do Hadoop](../../integration-services/connection-manager/hadoop-connection-manager.md)  
  
  
