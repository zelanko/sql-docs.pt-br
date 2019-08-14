---
title: Feature Pack do Azure para o SSIS (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.SSIS.AZURE.F1
- SQL14.SSIS.AZURE.F1
ms.assetid: 31de555f-ae62-4f2f-a6a6-77fea1fa8189
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 9241725a9f1da67ef93701b62c5cc4e8d9093a7a
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892736"
---
# <a name="azure-feature-pack-for-integration-services-ssis"></a>Feature Pack do Azure para o Integration Services (SSIS)

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


O Feature Pack do SSIS (SQL Server Integration Services) para Azure é uma extensão que oferece os componentes listados nesta página para o SSIS se conectar aos serviços do Azure, transferir dados entre o Azure e fontes de dados locais e processar dados armazenados no Azure.

[![Baixar o Feature Pack do SSIS para Azure](https://docs.microsoft.com/analysis-services/analysis-services/media/download.png)](https://www.microsoft.com/download/details.aspx?id=54798) **Baixar**

- Para SQL Server 2017 – [Feature Pack Microsoft SQL Server 2017 Integration Services para o Azure](https://www.microsoft.com/download/details.aspx?id=54798)
- Para SQL Server 2016 – [Feature Pack Microsoft SQL Server 2016 Integration Services para o Azure](https://www.microsoft.com/download/details.aspx?id=49492)
- Para SQL Server 2014 – [Feature Pack Microsoft SQL Server 2014 Integration Services para o Azure](https://www.microsoft.com/download/details.aspx?id=47366)
- Para SQL Server 2012 – [Feature Pack Microsoft SQL Server 2012 Integration Services para o Azure](https://www.microsoft.com/download/details.aspx?id=47367)

As páginas de download também incluem informações sobre pré-requisitos. Certifique-se de instalar o SQL Server antes de instalar o Azure Feature Pack em um servidor ou os componentes no Feature Pack talvez não estejam disponíveis quando você implantar pacotes para o banco de dados do Catálogo do SSIS, SSISDB, no servidor.

## <a name="components-in-the-feature-pack"></a>Componentes no Feature Pack
-   Gerenciadores de conexões

    -   [Gerenciador de Conexão do Azure Data Lake Analytics](connection-manager/azure-data-lake-analytics-connection-manager.md)

    -   [Gerenciador de conexões do Azure Data Lake Store](../integration-services/connection-manager/azure-data-lake-store-connection-manager.md)
    
    -   [Gerenciador de Conexões do Microsoft Azure HDInsight](../integration-services/connection-manager/azure-hdinsight-connection-manager.md)

    -   [Gerenciador de Conexões do Azure Resource Manager](../integration-services/connection-manager/azure-resource-manager-connection-manager.md)
    
    -   [Gerenciador de conexões do Armazenamento do Azure](../integration-services/connection-manager/azure-storage-connection-manager.md)

    -   [Gerenciador de Conexões da Assinatura do Azure](../integration-services/connection-manager/azure-subscription-connection-manager.md)
    
-   Tarefas

    -   [Tarefa de Download do Blob do Azure](../integration-services/control-flow/azure-blob-download-task.md)

    -   [Tarefa de Upload de Blobs do Azure](../integration-services/control-flow/azure-blob-upload-task.md)

    -   [Tarefa do Azure Data Lake Analytics](control-flow/azure-data-lake-analytics-task.md)

    -   [Tarefa do sistema de arquivos do Azure Data Lake Store](../integration-services/control-flow/azure-data-lake-store-file-system-task.md)

    -   [Tarefa Criar Cluster do Azure HDInsight](../integration-services/control-flow/azure-hdinsight-create-cluster-task.md)

    -   [Tarefa Excluir Cluster do Azure HDInsight](../integration-services/control-flow/azure-hdinsight-delete-cluster-task.md)
    
    -   [Tarefa do Hive do Azure HDInsight](../integration-services/control-flow/azure-hdinsight-hive-task.md)

    -   [Tarefa de Pig de HDInsight do Azure](../integration-services/control-flow/azure-hdinsight-pig-task.md)

    -   [Tarefa de Upload do DW no SQL Azure](../integration-services/control-flow/azure-sql-dw-upload-task.md)

    -   [Tarefa Arquivo Flexível](../integration-services/control-flow/flexible-file-task.md)

-   Componentes de fluxo de dados

    -   [Fonte de Blobs do Azure](../integration-services/data-flow/azure-blob-source.md)

    -   [Destino de Blob do Azure](../integration-services/data-flow/azure-blob-destination.md)
    
    -   [Fonte do Azure Data Lake Store](../integration-services/data-flow/azure-data-lake-store-source.md)
    
    -   [Destino do Azure Data Lake Store](../integration-services/data-flow/azure-data-lake-store-destination.md)

    -   [Origem de Arquivo Flexível](../integration-services/data-flow/flexible-file-source.md)

    -   [Destino de Arquivo Flexível](../integration-services/data-flow/flexible-file-destination.md)

-   Enumerador de Arquivos do Blob do Azure, Azure Data Lake Storage e Data Lake Storage Gen2. Consulte [Contêiner do Loop Foreach](../integration-services/control-flow/foreach-loop-container.md)

## <a name="use-tls-12"></a>Usar TLS 1.2

A versão do TLS usada pelo Feature Pack do Azure segue as configurações do .NET Framework do sistema.
Para usar o TLS 1.2, adicione um valor de `REG_DWORD` chamado `SchUseStrongCrypto` com os dados `1` sob as duas chaves do Registro a seguir.

1. `HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319`
2. `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319`

## <a name="dependency-on-java"></a>Dependência do Java

O Java é necessário para usar determinados recursos.
A arquitetura (32/64 bits) do build Java deve corresponder àquela do tempo de execução do SSIS para usar.
Os builds Java a seguir foram testados.

- [OpenJDK 8u192 do Zulu](https://www.azul.com/downloads/zulu/zulu-windows/)
- [Ambiente de Tempo de Execução Java do Oracle 8u192](https://www.oracle.com/technetwork/java/javase/downloads/java-archive-javase8-2177648.html)

### <a name="set-up-zulus-openjdk"></a>Configurar o OpenJDK do Zulu

1. Baixe e extraia o pacote de instalação zip.
2. No Prompt de Comando, execute `sysdm.cpl`.
3. Na guia **Avançado**, selecione **Variáveis de Ambiente**.
4. Na seção **Variáveis do sistema** seção, selecione **Novo**.
5. Insira `JAVA_HOME` para o **Nome da variável**.
6. Selecione **Procurar Diretório**, navegue até a pasta extraída e selecione a subpasta `jre`.
   Em seguida, selecione **OK** e o **Valor da variável** será preenchido automaticamente.
7. Selecione **OK** para fechar a caixa de diálogo **Nova Variável do Sistema**.
8. Selecione **OK** para fechar a caixa de diálogo **Variáveis de Ambiente**.
9. Selecione **OK** para fechar a caixa de diálogo **Propriedades do Sistema**.

### <a name="set-up-zulus-openjdk-on-azure-ssis-integration-runtime"></a>Configurar OpenJDK do Zulu no Azure-SSIS Integration Runtime

Isso deve ser feito por meio da [interface de instalação personalizada](https://docs.microsoft.com/azure/data-factory/how-to-configure-azure-ssis-ir-custom-setup) para o Azure-SSIS Integration Runtime.
Suponha que `zulu8.33.0.1-jdk8.0.192-win_x64.zip` seja usado.
O contêiner de blobs pode ser organizado da seguinte maneira.

~~~
main.cmd
install_openjdk.ps1
zulu8.33.0.1-jdk8.0.192-win_x64.zip
~~~

Como ponto de entrada, `main.cmd` dispara a execução do script `install_openjdk.ps1` do PowerShell que, por sua vez, `zulu8.33.0.1-jdk8.0.192-win_x64.zip` extrai e define `JAVA_HOME` de acordo.

**main.cmd**

~~~
powershell.exe -file install_openjdk.ps1
~~~

**install_openjdk.ps1**

~~~
Expand-Archive zulu8.33.0.1-jdk8.0.192-win_x64.zip -DestinationPath C:\
[Environment]::SetEnvironmentVariable("JAVA_HOME", "C:\zulu8.33.0.1-jdk8.0.192-win_x64\jre", "Machine")
~~~

### <a name="set-up-oracles-java-se-runtime-environment"></a>Configurar o Ambiente de Tempo de Execução Java SE do Oracle

1. Baixe e execute o instalador exe.
2. Siga as instruções do instalador para concluir a instalação.

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
  
