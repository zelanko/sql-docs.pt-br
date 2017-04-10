---
title: "Tarefa de Pig do Hadoop | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.designer.hadooppigtask.f1"
ms.assetid: 90646316-9822-48aa-9900-295a33750780
caps.latest.revision: 6
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 6
---
# Tarefa de Pig do Hadoop
  Use a Tarefa de Pig do Hadoop para executar o script de Pig em um cluster Hadoop.  
  
 Para adicionar uma Tarefa de Pig do Hadoop, arraste-a e solte-a para o designer. Em seguida, clique duas vezes na tarefa ou com o botão direito do mouse e clique em **Editar** para ver a caixa de diálogo **Editor de Tarefa de Pig do Hadoop**.  
  
 ![Hadoop Pig Task Editor](../../integration-services/control-flow/media/hadoop-pig-task.png "Hadoop Pig Task Editor")  
  
## Opções  
 Configure as seguintes opções na caixa de diálogo **Editor de Tarefa do Pig do Hadoop** .  
  
|Campo|Description|  
|-----------|-----------------|  
|**Conexão do Hadoop**|Especifique um Gerenciador de Conexões do Hadoop existente ou crie um novo. Esse gerenciador de conexões indica onde o serviço WebHCat está hospedado.|  
|**SourceType**|Especifique o tipo de fonte da consulta. Os valores disponíveis são **ScriptFile** e **DirectInput**.|  
|**InlineScript**|Quando o valor de **SourceType** for **DirectInput**, especifique o pig do Hive.|  
|**HadoopScriptFilePath**|Quando o valor de **SourceType** for **ScriptFile**, especifique o caminho do arquivo de script no Hadoop.|  
|**TimeoutInMinutes**|Especifique um valor de tempo limite em minutos. O trabalho do Hadoop para se não tiver sido concluído antes do tempo limite ser decorrido. Especifique 0 para agendar o trabalho do Hadoop para executar de forma assíncrona.|  
  
## Consulte também  
 [Gerenciador de conexões do Hadoop](../../integration-services/connection-manager/hadoop-connection-manager.md)  
  
  