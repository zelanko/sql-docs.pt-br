---
title: Feature Pack do Azure | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SQL11.SSIS.AZURE.F1
- SQL12.SSIS.AZURE.F1
ms.assetid: 31de555f-ae62-4f2f-a6a6-77fea1fa8189
caps.latest.revision: 53
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 43ddc105e442e510b54a70ed22ef27336f1497bf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010494"
---
# <a name="azure-feature-pack"></a>Feature Pack do Azure
O Feature Pack do SSIS (SQL Server Integration Services) para Azure é uma extensão que oferece os componentes listados nesta página para o SSIS se conectar aos serviços do Azure, transferir dados entre o Azure e fontes de dados locais e processar dados armazenados no Azure.

## <a name="components-in-the-feature-pack"></a>Componentes no Feature Pack
  
-   Gerenciadores de conexões  
  
    -   [Gerenciador de conexões do Armazenamento do Azure](connection-manager/azure-storage-connection-manager.md)  
  
    -   [Gerenciador de Conexões da Assinatura do Azure](connection-manager/azure-subscription-connection-manager.md)  
    
    -   [Gerenciador de conexões do Azure Data Lake Store](../../2014/integration-services/azure-data-lake-store-connection-manager.md)
    
    -   [Gerenciador de Conexões do Azure Resource Manager](../../2014/integration-services/azure-resource-manager-connection-manager.md)
    
    -   [Gerenciador de Conexões do Microsoft Azure HDInsight](../../2014/integration-services/azure-hdinsight-connection-manager.md)
  
-   Tarefas  
  
    -   [Tarefa de Upload de Blobs do Azure](control-flow/azure-blob-upload-task.md)  
  
    -   [Tarefa de Download do Blob do Azure](control-flow/azure-blob-download-task.md)  
  
    -   [Tarefa do Hive do Azure HDInsight](control-flow/azure-hdinsight-hive-task.md)  
  
    -   [Tarefa de Pig de HDInsight do Azure](https://msdn.microsoft.com/library/mt146781(v=sql.120).aspx)
  
    -   [Tarefa Criar Cluster do Azure HDInsight](control-flow/azure-hdinsight-create-cluster-task.md)  
  
    -   [Tarefa Excluir Cluster do Azure HDInsight](control-flow/azure-hdinsight-delete-cluster-task.md)
    
    -   [Tarefa de Upload do DW no SQL Azure](../../2014/integration-services/azure-sql-dw-upload-task.md)    
    
    -   [Tarefa do sistema de arquivos do Azure Data Lake Store](control-flow/file-system-task.md)    
  
-   Componentes de fluxo de dados  
  
    -   [Fonte de Blobs do Azure](https://msdn.microsoft.com/library/mt146775(v=sql.120).aspx)  
  
    -   [Destino de Blob do Azure](data-flow/azure-blob-destination.md)  
    
    -   [Fonte do Azure Data Lake Store](../../2014/integration-services/azure-data-lake-store-source.md)
    
    -   [Destino do Azure Data Lake Store](../../2014/integration-services/azure-data-lake-store-destination.md)
  
-   Enumerador de BLOBs do Azure & ADLS enumerador de arquivo. Consulte [Foreach Loop Container](control-flow/foreach-loop-container.md).  
  
 
## <a name="download-the-feature-pack"></a>Baixe o Feature Pack  
Baixe o SQL Server Integration Services (SSIS) Feature Pack para o Azure.  
  
-   [Microsoft SQL Server 2014 Integration Services Feature Pack para Azure](https://www.microsoft.com/download/details.aspx?id=47366)  

## <a name="prerequisites"></a>Prerequisites  
Você deve instalar os seguintes pré-requisitos antes de instalar este feature pack.  
  
-   SQL Server Integration Services  
-   .Net Framework 4.5  
  
## <a name="scenarios"></a>Cenários  
  
### <a name="big-data-processing"></a>Processamento de Big Data  
 Use o Conector do Azure para concluir o seguinte trabalho de processamento de Big Data:  
  
1.  Use a tarefa de upload de blobs do Azure para carregar dados de entrada para o armazenamento de blobs do Azure.  
  
2.  Use a tarefa Criar Cluster do Azure HDInsight para criar um cluster do Azure HDInsight. Esta etapa é opcional se você quiser usar seu próprio cluster.  
  
3.  Use a tarefa Hive ou Pig do Azure HDInsight para invocar uma tarefa de Pig ou Hive no cluster do Azure HDInsight .  
  
4.  Use a tarefa Excluir Cluster do Azure HDInsight para excluir o cluster do HDInsight após o uso, se você tiver criado um cluster de HDInsight sob demanda na etapa 2.  
  
5.  Use a tarefa Download de Blob do Azure HDInsight para baixar dados de saída de Pig/Hive do armazenamento de blobs do Azure.  
  
 ![SSIS-AzureConnector-BigDataScenario](media/ssis-azureconnector-bigdatascenario.png "BigDataScenario de AzureConnector de SSIS")  
  
### <a name="cloud-data-archiving"></a>Arquivamento de dados em nuvem  
 Use o destino de blob do Azure em um pacote do SSIS para gravar dados de saída em um armazenamento de blobs do Azure ou use a fonte de blob do Azure para ler dados de um armazenamento de blobs do Azure.  
  
 ![SSIS-AzureConnector-CloudArchive-1](media/ssis-azureconnector-cloudarchive-1.png "SSIS-AzureConnector-CloudArchive-1")  
  
 ![SSIS-AzureConnector-CloudArchive-2](media/ssis-azureconnector-cloudarchive-2.png "SSIS-AzureConnector-CloudArchive-2")  
  
 E use o contêiner Loop Foreach com o enumerador de blob do Azure para processar dados em vários arquivos de blob.  
  
 ![SSIS-AzureConnector-CloudArchive-3](media/ssis-azureconnector-cloudarchive-3.png "SSIS-AzureConnector-CloudArchive-3")  
  
  