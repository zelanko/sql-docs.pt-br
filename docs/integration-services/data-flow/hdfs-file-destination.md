---
title: Destino de arquivo HDFS | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ssis.designer.hdfsfiledest.f1
ms.assetid: 4338ce9f-c077-4301-aca5-47ed070ec94d
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 02a2ecf62d91110bfd7e8a1429d5e1b835e4244e
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="hdfs-file-destination"></a>Destino de Arquivo HDFS
  O componente Destino de Arquivo HDFS permite que um pacote do SSIS grave dados de um arquivo HDFS. Os formatos de arquivo com suporte são Texto, Avro e ORC.  
  
 Para configurar o Destino de Arquivo HDFS, arraste e solte a Origem de Arquivo HDFS no designer de fluxo de dados e clique duas vezes no componente para abrir o editor.  
  
 ![Editor de destino do arquivo HDFS](../../integration-services/data-flow/media/hdfs-file-dest.png "Editor de destino do arquivo HDFS")  
  
## <a name="options"></a>Opções  
 Configure as seguintes opções na guia **Geral** da caixa de diálogo **Editor de Destino de Arquivo Hadoop** .  
  
|Campo|Description|  
|-----------|-----------------|  
|**Conexão do Hadoop**|Especifique um gerenciador de conexões do Hadoop existente ou crie um novo. Esse gerenciador de conexões indica onde os arquivos HDFS estão hospedados.|  
|**Caminho do Arquivo**|Especifique o nome do arquivo HDFS.|  
|**Formato do arquivo**|Especifique o formato do arquivo HDFS. As opções disponíveis são Texto, Avro e ORC.|  
|**Caractere delimitador de coluna**|Se você selecionar o formato Texto, especifique o caractere delimitador de coluna.|  
|**Nomes de coluna na primeira linha de dados**|Se você selecionar o formato Texto, indique se a primeira linha no arquivo conterá nomes de coluna.|  
  
 Depois de configurar essas opções, selecione a guia **Colunas** para mapear colunas de origem para colunas de destino no fluxo de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciador de conexões do Hadoop](../../integration-services/connection-manager/hadoop-connection-manager.md)   
 [Origem do arquivo HDFS](../../integration-services/data-flow/hdfs-file-source.md)  
  
  

