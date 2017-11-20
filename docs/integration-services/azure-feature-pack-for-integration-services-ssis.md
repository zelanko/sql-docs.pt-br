---
title: Feature Pack do Azure para o Integration Services (SSIS) | Microsoft Docs
ms.custom: 
ms.date: 08/22/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.SSIS.AZURE.F1
- SQL14.SSIS.AZURE.F1
ms.assetid: 31de555f-ae62-4f2f-a6a6-77fea1fa8189
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 4941d8eb846e9d47b008447fe0e346d43de5d87f
ms.openlocfilehash: d4204ba56e515025bed3ae3bf8e7a77d6da471be
ms.contentlocale: pt-br
ms.lasthandoff: 08/30/2017

---
# <a name="azure-feature-pack-for-integration-services-ssis"></a>Feature Pack do Azure para o Integration Services (SSIS)
SQL Server Integration Services (SSIS) Feature Pack para Azure é uma extensão que fornece os componentes listados nesta página para SSIS se conecte aos serviços do Azure, transferir dados entre o Azure e fontes de dados locais e processar dados armazenados no Azure.

[![Baixe o SSIS Feature Pack para Azure](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=54798) **baixar**

- Para o SQL Server de 2017 - [Microsoft SQL Server 2017 Integration Services Feature Pack para Azure](https://www.microsoft.com/download/details.aspx?id=54798)
- Para o SQL Server 2016 - [Microsoft SQL Server 2016 Integration Services Feature Pack para Azure](https://www.microsoft.com/download/details.aspx?id=49492)
- Para o SQL Server 2014 - [Microsoft SQL Server 2014 Integration Services Feature Pack para Azure](https://www.microsoft.com/en-us/download/details.aspx?id=47366)
- Para o SQL Server 2012 - [Microsoft SQL Server 2012 Integration Services Feature Pack para Azure](https://www.microsoft.com/en-us/download/details.aspx?id=47367)

## <a name="components-in-the-feature-pack"></a>Componentes no Feature Pack
-   Gerenciadores de conexões

    -   [Gerenciador de conexões do Armazenamento do Azure](../integration-services/connection-manager/azure-storage-connection-manager.md)

    -   [Gerenciador de Conexões da Assinatura do Azure](../integration-services/connection-manager/azure-subscription-connection-manager.md)
    
    -   [Gerenciador de conexões do Azure Data Lake Store](../integration-services/connection-manager/azure-data-lake-store-connection-manager.md)
    
    -   [Gerenciador de Conexão do Gerenciador de recursos do Azure](../integration-services/connection-manager/azure-resource-manager-connection-manager.md)
    
    -   [Gerenciador de Conexão de HDInsight do Azure](../integration-services/connection-manager/azure-hdinsight-connection-manager.md)

-   Tarefas

    -   [Tarefa de Upload de Blobs do Azure](../integration-services/control-flow/azure-blob-upload-task.md)

    -   [Tarefa de Download do Blob do Azure](../integration-services/control-flow/azure-blob-download-task.md)

    -   [Tarefa do Hive do Azure HDInsight](../integration-services/control-flow/azure-hdinsight-hive-task.md)

    -   [Tarefa de Pig de HDInsight do Azure](../integration-services/control-flow/azure-hdinsight-pig-task.md)

    -   [Tarefa Criar Cluster do Azure HDInsight](../integration-services/control-flow/azure-hdinsight-create-cluster-task.md)

    -   [Tarefa Excluir Cluster do Azure HDInsight](../integration-services/control-flow/azure-hdinsight-delete-cluster-task.md)
    
    -   [Tarefa de Upload do DW no SQL Azure](../integration-services/control-flow/azure-sql-dw-upload-task.md)

    -   [Tarefa de sistema de arquivos do repositório Azure Data Lake](../integration-services/control-flow/azure-data-lake-store-file-system-task.md)

-   Componentes de fluxo de dados

    -   [Fonte de Blobs do Azure](../integration-services/data-flow/azure-blob-source.md)

    -   [Destino de Blob do Azure](../integration-services/data-flow/azure-blob-destination.md)
    
    -   [Fonte do Azure Data Lake Store](../integration-services/data-flow/azure-data-lake-store-source.md)
    
    -   [Destino do Azure Data Lake Store](../integration-services/data-flow/azure-data-lake-store-destination.md)

-   & ADLS arquivo enumerador de BLOBs do Azure. Consulte [contêiner Loop Foreach](http://msdn.microsoft.com/library/95a19dde-61ca-4d9b-aa3d-131fa4264296)

## <a name="download-the-feature-pack"></a>Baixe o Feature Pack
 Baixe o SQL Server Integration Services (SSIS) Feature Pack do Azure.
 
- [SSIS Feature Pack para Azure](http://go.microsoft.com/fwlink/?LinkID=626967) para SQL Server 2016
- [SSIS Feature Pack para Azure](https://www.microsoft.com/en-us/download/details.aspx?id=54798) para[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

## <a name="prerequisites"></a>Pré-requisitos
 Você deve instalar os seguintes pré-requisitos antes de instalar este feature pack.

-   SQL Server Integration Services
-   .Net Framework 4.5

## <a name="scenario-processing-big-data"></a>Cenário: Processamento de Big Data
 Use o Conector do Azure para concluir o seguinte trabalho de processamento de Big Data:

1.  Use a tarefa de upload de blobs do Azure para carregar dados de entrada para o armazenamento de blobs do Azure.

2.  Use a tarefa Criar Cluster do Azure HDInsight para criar um cluster do Azure HDInsight. Esta etapa é opcional se você quiser usar seu próprio cluster.

3.  Use a tarefa Hive ou Pig do Azure HDInsight para invocar uma tarefa de Pig ou Hive no cluster do Azure HDInsight .

4.  Use a tarefa Excluir Cluster do Azure HDInsight para excluir o cluster do HDInsight após o uso, se você tiver criado um cluster de HDInsight sob demanda na etapa 2.

5.  Use a tarefa Download de Blob do Azure HDInsight para baixar dados de saída de Pig/Hive do armazenamento de blobs do Azure.

![SSIS-AzureConnector-BigDataScenario](../integration-services/media/ssis-azureconnector-bigdatascenario.png)
 
## <a name="scenario-managing-data-in-the-cloud"></a>Cenário: Gerenciamento de dados na nuvem
 Use o Destino de Blob do Azure em um pacote do SSIS para gravar dados de saída no Armazenamento de Blobs do Azure, ou use a Fonte de Blob do Azure para ler dados de um Armazenamento de Blobs do Azure.

![SSIS-AzureConnector-CloudArchive-1](../integration-services/media/ssis-azureconnector-cloudarchive-1.png)
 
 ![SSIS-AzureConnector-CloudArchive-2](../integration-services/media/ssis-azureconnector-cloudarchive-2.png)

 Use o contêiner Loop Foreach com o enumerador de Blob do Azure para processar dados em vários arquivos de blob.

![SSIS-AzureConnector-CloudArchive-3](../integration-services/media/ssis-azureconnector-cloudarchive-3.png)
  

