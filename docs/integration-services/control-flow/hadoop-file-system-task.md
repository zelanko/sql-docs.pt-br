---
title: Tarefa do Sistema de Arquivos Hadoop | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hadoopfiletask.f1
ms.assetid: 594aaf5d-7703-4788-897d-fb95aca798c5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 006c9d5ae0ade37cc3ecbe4d7912c49eafbf4069
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86918190"
---
# <a name="hadoop-file-system-task"></a>Tarefas do Sistema de Arquivos Hadoop

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  A Tarefa do Sistema de Arquivos Hadoop habilita um pacote do SSIS a copiar arquivos de, para ou dentro de um cluster Hadoop.  
  
 Para adicionar uma Tarefa do Sistema de Arquivos Hadoop, arraste-a e solte-a no designer. Em seguida, clique duas vezes na tarefa ou clique com o botão direito do mouse e clique em **Editar**para abrir a caixa de diálogo **Editor de Tarefa do Sistema de Arquivos Hadoop** .  
  
 ![Editor de Tarefa do Sistema de Arquivos Hadoop](../../integration-services/control-flow/media/hadoop-filesystem-task.png "Editor de Tarefa do Sistema de Arquivos Hadoop")  
  
## <a name="options"></a>Opções  
 Configure as opções a seguir na caixa de diálogo **Tarefa do Sistema de Arquivos Hadoop** .  
  
|Campo|DESCRIÇÃO|  
|-----------|-----------------|  
|**Conexão do Hadoop**|Especifique um gerenciador de conexões do Hadoop existente ou crie um novo. Esse gerenciador de conexões indica onde os arquivos de destino estão hospedados.|  
|**Caminho de arquivo do Hadoop**|Especifique o caminho de arquivo ou diretório no HDFS.|  
|**Tipo de arquivo do Hadoop**|Especifique se o objeto do sistema de arquivos HDFS é um arquivo ou diretório.|  
|**Substituir o Destino**|Especifique se deseja substituir o arquivo de destino, caso ele já exista.|  
|**Operação**|Especifique a operação. As operações disponíveis são **CopyToHDFS**, **CopyFromHDFS**e **CopyWithinHDFS**.|  
|**Conexão de arquivo local**|Especifique um Gerenciador de Conexões de Arquivo existente ou crie um novo. Esse gerenciador de conexões indica onde os arquivos de origem estão hospedados.|  
|**É Recursivo**|Especifique se deseja copiar todas as subpastas de forma recursiva.|  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciador de conexões do Hadoop](../../integration-services/connection-manager/hadoop-connection-manager.md)   
 [Gerenciador de Conexões de Arquivos](../../integration-services/connection-manager/file-connection-manager.md)  
  
  
