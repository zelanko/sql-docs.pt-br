---
title: Tarefa do Pig do Hadoop | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hadooppigtask.f1
ms.assetid: 90646316-9822-48aa-9900-295a33750780
author: janinezhang
ms.author: janinez
ms.openlocfilehash: a8746d50744a5498b0f36a7d19103f653b866d33
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67929909"
---
# <a name="hadoop-pig-task"></a>Tarefa de Pig do Hadoop

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Use a Tarefa de Pig do Hadoop para executar o script de Pig em um cluster Hadoop.  
  
 Para adicionar uma Tarefa de Pig do Hadoop, arraste-a e solte-a para o designer. Em seguida, clique duas vezes na tarefa ou com o botão direito do mouse e clique em **Editar**para ver a caixa de diálogo **Editor de Tarefa de Pig do Hadoop** .  
  
 ![Editor de Tarefa de Pig do Hadoop](../../integration-services/control-flow/media/hadoop-pig-task.png "Editor de Tarefa de Pig do Hadoop")  
  
## <a name="options"></a>Opções  
 Configure as seguintes opções na caixa de diálogo **Editor de Tarefa do Pig do Hadoop** .  
  
|Campo|Descrição|  
|-----------|-----------------|  
|**Conexão do Hadoop**|Especifique um gerenciador de conexões do Hadoop existente ou crie um novo. Esse gerenciador de conexões indica onde o serviço WebHCat está hospedado.|  
|**SourceType**|Especifique o tipo de fonte da consulta. Os valores disponíveis são **ScriptFile** e **DirectInput**.|  
|**InlineScript**|Quando o valor de **SourceType** for **DirectInput**, especifique o pig do Hive.|  
|**HadoopScriptFilePath**|Quando o valor de **SourceType** for **ScriptFile**, especifique o caminho do arquivo de script no Hadoop.|  
|**TimeoutInMinutes**|Especifique um valor de tempo limite em minutos. O trabalho do Hadoop para se não tiver sido concluído antes do tempo limite ser decorrido. Especifique 0 para agendar o trabalho do Hadoop para executar de forma assíncrona.|  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciador de conexões do Hadoop](../../integration-services/connection-manager/hadoop-connection-manager.md)  
  
  
