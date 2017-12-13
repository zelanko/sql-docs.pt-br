---
title: Novidades do Integration Services no SQL Server 2016 | Microsoft Docs
ms.custom: SQL2016_New_Updated
ms.date: 09/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Integration Services, what's new
- what's new [Integration Services]
ms.assetid: da6999c7-e5e3-4a59-a284-1da635995af1
caps.latest.revision: "183"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 984807a0a75321b529c5e2519da71b81bed8a788
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="what39s-new-in-integration-services-in-sql-server-2016"></a>Novidades do Integration Services no SQL Server 2016
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../includes/feedback-stackoverflow-msdn-connect-md.md)]

Este tópico descreve os recursos adicionados ou atualizados no SQL Server 2016 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Ele também inclui recursos adicionados ou atualizados no [Azure Feature Pack para o SSIS &#40;Integration Services&#41;](../integration-services/azure-feature-pack-for-integration-services-ssis.md) durante o período de tempo do SQL Server 2016.  

## <a name="new-for-ssis-in-azure-data-factory"></a>Novidades do SSIS no Azure Data Factory

Com a visualização pública do Azure Data Factory versão 2 em setembro de 2017, agora você pode fazer o seguinte:
-   Implantar pacotes no SSISDB (banco de dados do Catálogo do SSIS) no Banco de Dados SQL do Azure.
-   Execute os pacotes implantados no Azure no Azure-SSIS Integration Runtime, um componente do Azure Data Factory versão 2.

Para obter mais informações, consulte [Migrar cargas de trabalho do SQL Server Integration Services por lift-and-shift para a nuvem](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md).

Essas novas funcionalidades exigem o SSDT (SQL Server Data Tools) versão 17.2 ou posterior, mas não exigem o SQL Server 2017 nem o SQL Server 2016. Quando você implanta pacotes no Azure, o Assistente de Implantação de Pacotes sempre faz upgrade dos pacotes para o formato de pacote mais recente.

## <a name="2016-improvements-by-category"></a>Aprimoramentos de 2016 agrupados por categoria  
  
-   **Capacidade de gerenciamento**  
  
    -   Melhor implantação  
  
        -   [Assistente de atualização do SSISDB](#ssisdbupgrwiz)  
  
        -   [Suporte para AlwaysOn no Catálogo do SSIS](#AlwaysOn)  
  
        -   [Implantação de pacotes incremental](#IncrementalDeployment)  
  
        -   [Suporte para Always Encrypted no Catálogo do SSIS](#encrypted)  
  
    -   Melhor depuração  
  
        -   [Nova função de nível de banco de dados ssis_logreader no catálogo do SSIS](#LogReader)  
  
        -   [Novo nível de log RuntimeLineage no catálogo do SSIS](#RuntimeLineage)  
  
        -   [Novo nível de log personalizado no catálogo do SSIS](#CustomLogging)  
  
        -   [Nomes de coluna para erros no fluxo de dados](#ErrorColumn)  
  
        -   [Suporte expandido para nomes de coluna de erro](#getidstring)  
  
        -   [Suporte para nível de log padrão em todo o servidor](#ServerLogLevel)  
  
        -   [Nova interface IDTSComponentMetaData130 na API](#CMD130)  
  
    -   Melhor gerenciamento de pacotes  
  
        -   [Experiência aprimorada para atualização de projeto](#ProjectUpgrade)  
  
        -   [A propriedade AutoAdjustBufferSize calcula automaticamente o tamanho do buffer do fluxo de dados](#BufferSize)  
  
        -   [Modelos de fluxo de controle reutilizáveis](#Templates)  
  
        -   [Novos modelos renomeados como partes](#Parts)  
  
-   **Conectividade**  
  
    -   Conectividade expandida local  
  
        -   [Suporte para fontes de dados OData v4](#ODatav4)  
  
        -   [Suporte explícito para fontes de dados do Excel 2013](#Excel2013)  
  
        -   [Suporte para o HDFS (sistema de arquivos do Hadoop)](#HDFS)  
  
        -   [Suporte expandido para Hadoop e HDFS](#more_hadoop)  
  
        -   [O Destino do Arquivo do HDFS agora dá suporte ao formato de arquivo ORC](#hdfsORC)  
  
        -   [Componentes ODBC atualizados para o SQL Server 2016](#odbc2016)  
  
        -   [Suporte explícito para fontes de dados do Excel 2016](#Excel2016)  
  
        -   [Conector para SAP BW para SQL Server 2016 liberado](#SAPBW)
        
        -   [Conectores v4.0 para Oracle e Teradata liberados](#oracleteradata)
        
        -   [Conectores para a Atualização 5 do Dispositivo do Analytics Platform System (PDW) liberados](#pdwau5)
  
    -   Conectividade expandida com a nuvem  
  
        -   Conectores de Armazenamento do Azure e tarefas Hive e Pig de HDInsight – [Azure Feature Pack para SSIS lançado para o SQL Server 2016](#AFP2016)
        
        -   [Suporte para recursos online do Microsoft Dynamics liberado no Service Pack 1](#dynamics)
        
        -   [Suporte para Azure Data Lake Store lançado](#datalakestore)
        
        -   [Suporte para Azure SQL Data Warehouse lançado](#sqldwupload)
  
-   **Usabilidade e produtividade**  
  
    -   Melhor experiência de instalação  
  
        -   [Atualização bloqueada quando o SSISDB pertence a um Grupo de Disponibilidade](#Upgrade)  
  
    -   Melhor experiência de design  
  
        -   [O Designer do SSIS cria e mantém os pacotes para o SQL Server 2016, 2014 ou 2012](#OneDesigner)  
  
        -   Várias correções de bug e aperfeiçoamentos do designer.  
  
    -   Melhor experiência de gerenciamento no SQL Server Management Studio
  
        -   [Desempenho aprimorado para exibições do Catálogo do SSIS](#CatViews)  
  
    -   Outros aprimoramentos  
  
        -   [A transformação do Distribuidor de Dados Equilibrado agora faz parte do SSIS](#BDDinbox)  
  
        -   [Os componentes de publicação de feed de dados agora fazem parte do SSIS](#ComplexFeedinbox)  
  
        -   [Suporte para o Armazenamento de Blobs do Azure no Assistente de Importação e Exportação do SQL Server](#AzureBlob)  
  
        -   [Change Data Capture Designer e Service para Oracle para Microsoft SQL Server 2016 liberados](#CDCOracle)  
  
        -   [Componentes CDC atualizados para o SQL Server 2016](#cdc2016)  
  
        -   [Tarefa Executar DDL do Analysis Services atualizada](#ASDDL)  
  
        -   [As tarefas do Analysis Services dão suporte a modelos de tabela](#ssasrc0)  
  
        -   [Suporte para R Services interno](#builtinR)  
  
        -   [Saída de validação de XML avançada na Tarefa XML](#ValidateXML)  
  
## <a name="manageability"></a>Capacidade de gerenciamento  

### <a name="better-deployment"></a>Melhor implantação

####  <a name="ssisdbupgrwiz"></a> Assistente de atualização do SSISDB  
 Execute o Assistente de atualização do SSISDB para atualizar o banco de dados do catálogo do SSIS, SSISDB, quando o banco de dados for mais antigo que a versão atual da instância do SQL Server. Isso ocorre quando uma das condições a seguir é verdadeira.  
  
-   Você restaurou o banco de dados de uma versão anterior do SQL Server.  
  
-   Você não removeu o banco de dados de um Grupo de Disponibilidade AlwaysOn antes de atualizar a instância do SQL Server. Isso impede a atualização automática do banco de dados. Para obter mais informações, consulte [Upgrading SSISDB in an availability group](../integration-services/service/ssis-catalog.md#Upgrade).  
  
 Para obter mais informações, consulte [Catálogo do SSIS &#40;SSISDB&#41;](../integration-services/service/ssis-catalog.md). 

####  <a name="AlwaysOn"></a> Suporte para AlwaysOn no Catálogo do SSIS  
 O recurso Grupos de Disponibilidade AlwaysOn é uma solução de alta disponibilidade e recuperação de desastres que fornece uma alternativa de nível corporativo para espelhamento de banco de dados. Um grupo de disponibilidade dá suporte a um ambiente de failover para um conjunto discreto de bancos de dados de usuário, conhecidos como bancos de dados de disponibilidade, que fazem failover juntos. Para obter mais informações, confira [AlwaysOn em grupos de disponibilidade](../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md).  
  
 No SQL Server 2016, o SSIS apresenta novos recursos que permitem a você implantar facilmente em um catálogo de SSIS centralizado (ou seja, banco de dados de usuário do SSISDB). Para fornecer alta disponibilidade ao banco de dados SSISDB e seu conteúdo - projetos, pacotes, logs de execução, etc. - você pode adicionar o banco de dados do SSISDB a um grupo de disponibilidade AlwaysOn, assim como faria com qualquer outro banco de dados de usuário. Quando ocorre um failover, um dos nós secundários automaticamente se torna o novo nó primário.  
  
 Para uma visão geral detalhada e instruções passo a passo para habilitar o Always On para SSISDB, consulte [Catálogo do SSIS](../integration-services/service/ssis-catalog.md).  

####  <a name="IncrementalDeployment"></a> Implantação de pacotes incremental  
O recurso de implantação de pacotes incremental permite que você implante um ou mais pacotes para um projeto novo ou existente, sem implantar o projeto inteiro. Você pode implantar pacotes incrementalmente usando as ferramentas a seguir.  
  
-   Assistente para Implantação  
  
-   SQL Server Management Studio (que usa o Assistente de Implantação)  
  
-   SQL Server Data Tools (Visual Studio) (que também usa o Assistente de Implantação)  
  
-   Procedimentos armazenados  
  
-   A API do MOM (modelo do objeto de gerenciamento)  
  
 Para obter mais informações, consulte [Implantar projetos e pacotes do SSIS (Integration Services)](../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md.  

####  <a name="encrypted"></a> Suporte para Always Encrypted no Catálogo do SSIS  
 O SSIS já dá suporte ao recurso Always Encrypted no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obter mais informações, consulte as postagens de blog a seguir.  
  
-   [SSIS com Always Encrypted](http://blogs.msdn.com/b/ssis/archive/2015/12/18/ssis-with-always.aspx)  
  
-   [Transformação de pesquisa com Always Encrypted](http://blogs.msdn.com/b/ssis/archive/2015/12/18/lookup-transformation-with-always-encrypted.aspx)  

### <a name="better-debugging"></a>Melhor depuração

####  <a name="LogReader"></a> Nova função de nível de banco de dados ssis_logreader no catálogo do SSIS  
 Nas versões anteriores do catálogo do SSIS, somente usuários na função **ssis_admin** podem acessar os modos de exibição que contêm a saída de log. Agora há uma nova função de nível de banco de dados **ssis_logreader** que você pode usar para conceder permissões para acessar os modos de exibição que contêm a saída de log para usuários que não são administradores.  
  
 Há também uma nova função **ssis_monitor** . Essa função dá suporte a AlwaysOn e é para uso interno, apenas pelo catálogo do SSIS.  

####  <a name="RuntimeLineage"></a> Novo nível de log RuntimeLineage no catálogo do SSIS  
 O novo nível de log **RuntimeLineage** no catálogo do SSIS coleta os dados necessários para rastrear informações de linhagem no fluxo de dados. Você pode analisar essas informações de linhagem para mapear o relacionamento de linhagem entre tarefas. ISVs e desenvolvedores podem compilar ferramentas de mapeamento de linhagem personalizadas com essas informações. 

####  <a name="CustomLogging"></a> Novo nível de log personalizado no catálogo do SSIS  
 Versões anteriores do catálogo do SSIS permitem que você escolha entre quatro níveis de log internos quando você executa um pacote: **Nenhum, Básico, Desempenho ou Detalhado**. O SQL Server 2016 adiciona o nível de log **RuntimeLineage**. Além disso, agora você pode criar e salvar vários níveis de log personalizados no catálogo do SSIS e escolher o nível de log para usar toda vez que você executar um pacote. Para cada nível de log personalizado, selecione apenas as estatísticas e eventos que você deseja capturar. Opcionalmente, inclua o contexto do evento para ver os valores de variáveis, cadeias de conexão e propriedades da tarefa. Para obter mais informações, consulte [Enable Logging for Package Execution on the SSIS Server](../integration-services/performance/integration-services-ssis-logging.md#server_logging). 

####  <a name="ErrorColumn"></a> Nomes de coluna para erros no fluxo de dados  
 Quando você redireciona as linhas no fluxo de dados que contêm erros de saída de erro, a saída contém um identificador numérico para a coluna na qual o erro ocorreu, mas não mostra o nome da coluna. Agora, há várias maneiras de localizar ou exibir o nome da coluna na qual ocorreu o erro.  
  
-   Quando você configura o log, selecione o evento **DiagnosticEx** para registro em log. Esse evento grava um mapa de coluna de fluxo de dados no log. Em seguida, você pode procurar o nome da coluna no mapa coluna usando o identificador da coluna capturado por uma saída de erro. Para obter mais informações, consulte [Tratamento de erro em dados](../integration-services/data-flow/error-handling-in-data.md).  
  
-   No Editor Avançado, você pode ver o nome da coluna para a coluna de upstream quando você exibe as propriedades de uma coluna de entrada ou saída de um componente de fluxo de dados.  
  
-   Para ver os nomes das colunas em que o erro ocorreu, anexe um Visualizador de Dados a uma saída de erro.  O Visualizador de Dados agora mostra tanto a descrição do erro quanto o nome da coluna na qual ocorreu o erro.  
  
-   No Componente de Script ou um componente de fluxo de dados personalizado, chame o novo método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData130.GetIdentificationStringByID%2A> da interface IDTSComponentMetadata100.  
  
 Para obter mais informações sobre esse aprimoramento, consulte a seguinte postagem de blog pelo desenvolvedor do SSIS Bo Fan: [Aprimoramentos de coluna de erro para fluxo de dados do SSIS](http://blogs.msdn.com/b/ssis/archive/2015/11/27/error-column-improvement-for-ssis-data-flow.aspx).  
  
> [!NOTE]  
>  (Esse suporte foi expandido em versões subsequentes. Para obter mais informações, consulte [Suporte estendido para nomes de coluna de erro](#getidstring) e [Nova interface IDTSComponentMetaData130 na API](#CMD130).)  

####  <a name="getidstring"></a> Suporte expandido para nomes de coluna de erro  
 O evento **DiagnosticEx** agora registra em log informações de coluna para todas as colunas de entrada e saída, não apenas as colunas de linhagem. Como resultado, podemos chamar agora a saída de um mapa da coluna do pipeline, em vez de um mapa da linhagem do pipeline.  
  
 O método GetIdentificationStringByLineageID foi renomeado para <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData130.GetIdentificationStringByID%2A>. Para obter mais informações, consulte [Nomes de coluna para erros no fluxo de dados](#ErrorColumn).  
  
 Para obter mais informações sobre essa alteração e sobre a melhoria da coluna de erro, consulte a postagem de blog atualizada a seguir. [Aprimoramentos de coluna de erro para o fluxo de dados do SSIS (atualizado para CTP3.3)](http://blogs.msdn.com/b/ssis/archive/2015/11/27/error-column-improvement-for-ssis-data-flow.aspx)  
  
> [!NOTE]  
>  (No RC0, esse método foi movido para a nova interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData130> . Para obter mais informações, consulte [Nova interface IDTSComponentMetaData130 na API](#CMD130).)  

####  <a name="ServerLogLevel"></a> Suporte para nível de log padrão em todo o servidor  
 Nas **Propriedades do Servidor**do SQL Server, sob a propriedade **Nível de log do servidor** , agora você pode selecionar um nível de log padrão para todo o servidor. Você pode escolher entre um dos níveis de logs internos - básico, nenhum, detalhado, desempenho ou linhagem de tempo de execução - ou você pode escolher um nível de log personalizado existente. O nível de log selecionado aplica-se a todos os pacotes implantados no Catálogo do SSIS. Ele também se aplica por padrão a uma etapa de trabalho do SQL Agent, que executa um pacote do SSIS.  

####  <a name="CMD130"></a> Nova interface IDTSComponentMetaData130 na API  
 O novo nível de log <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData130> adiciona a nova funcionalidade no SQL Server 2016 à interface existente <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> , especialmente o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData130.GetIdentificationStringByID%2A> . (O método **GetIdentificationStringByID** é movido para a nova interface da interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> .) Há também novas interfaces <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInputColumn130> e <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn130> , que fornecem a propriedade **LineageIdentificationString** . Para obter mais informações, consulte [Nomes de coluna para erros no fluxo de dados](#ErrorColumn).  

### <a name="better-package-management"></a>Melhor gerenciamento de pacotes

####  <a name="ProjectUpgrade"></a> Experiência aprimorada para atualização de projeto  
 Ao atualizar projetos do SSIS das versões anteriores para a versão atual, os gerenciadores de conexões de nível de projeto continuam a funcionar conforme o esperado e as anotações e o layout do pacote são mantidos.  

####  <a name="BufferSize"></a> A propriedade AutoAdjustBufferSize calcula automaticamente o tamanho do buffer do fluxo de dados  
 Quando você define o valor da nova propriedade **AutoAdjustBufferSize** para **true**, o mecanismo de fluxo de dados calcula automaticamente o tamanho do buffer para o fluxo de dados. Para obter mais informações, consulte [Data Flow Performance Features](../integration-services/data-flow/data-flow-performance-features.md).  

####  <a name="Templates"></a> Modelos de fluxo de controle reutilizáveis  
 Salve um contêiner ou tarefa de fluxo de controle frequentemente utilizada em um arquivo de modelo autônomo e reutilizar várias vezes em um ou mais pacotes em um projeto, pelo uso de modelos de fluxo de controle. Essa capacidade de reutilização facilita o desenvolvimento e manutenção dos pacotes do SSIS. Para obter mais informações, consulte [Reutilizar o fluxo de controle entre pacotes usando partes do pacote do fluxo de controle](../integration-services/reuse-control-flow-across-packages-by-using-control-flow-package-parts.md).  

####  <a name="Parts"></a> Novos modelos renomeados como partes  
 Os novos modelos de fluxo de controle reutilizáveis lançados no CTP 3.0 foram renomeados como partes do fluxo de controle ou partes do pacote. Para obter mais informações sobre esse recurso, consulte [Reutilizar o fluxo de controle entre pacotes usando partes do pacote do fluxo de controle](../integration-services/reuse-control-flow-across-packages-by-using-control-flow-package-parts.md).  

## <a name="connectivity"></a>Conectividade  

### <a name="expanded-connectivity-on-premises"></a>Conectividade expandida local

####  <a name="ODatav4"></a> Suporte para fontes de dados OData v4  
 A Origem do OData e o Gerenciador de Conexões OData agora dão suporte os protocolos v3 e v4 do OData.  
  
-   Para o protocolo V3 do OData, o componente dá suporte aos formatos de dados ATOM e JSON.  
  
-   Para o protocolo V4 do OData, o componente dá suporte ao formato de dados JSON.  
  
 Para obter mais informações, consulte [OData Source](../integration-services/data-flow/odata-source.md).  

####  <a name="Excel2013"></a> Suporte explícito para fontes de dados do Excel 2013  
 O Gerenciador de Conexões do Excel, a Origem do Excel, o Destino do Excel e o Assistente de Importação e Exportação do SQL Server agora fornecem suporte explícito para fontes de dados do Excel 2013. 

####  <a name="HDFS"></a> Suporte para o HDFS (sistema de arquivos do Hadoop)  
 O suporte para o HDFS contém gerenciadores de conexões para conectar-se a clusters do Hadoop e tarefas para executar operações comuns do HDFS. Para obter mais informações, consulte [Suporte para Hadoop e HDFS no Integration Services &#40;SSIS&#41;](../integration-services/hadoop-and-hdfs-support-in-integration-services-ssis.md).  

####  <a name="more_hadoop"></a> Suporte expandido para Hadoop e HDFS  
  
-   O Gerenciador de Conexões do Hadoop agora dá suporte à autenticação dos tipos Básica e Kerberos. Para obter mais informações, consulte [Hadoop Connection Manager](../integration-services/connection-manager/hadoop-connection-manager.md).  
  
-   A Origem do Arquivo HDFS e o Destino do Arquivo HDFS agora dão suporte a ambos os formatos Texto e Avro. Para obter mais informações, consulte  [HDFS File Source](../integration-services/data-flow/hdfs-file-source.md) e  [HDFS File Destination](../integration-services/data-flow/hdfs-file-destination.md).  
  
-   A tarefa de sistema de arquivos Hadoop agora dá suporte à opção CopyWithinHadoop, além das opções CopyToHadoop e CopyFromHadoop. Para obter mais informações, consulte [Hadoop File System Task](../integration-services/control-flow/hadoop-file-system-task.md).  

####  <a name="hdfsORC"></a> O Destino do Arquivo do HDFS agora dá suporte ao formato de arquivo ORC  
 O Destino do Arquivo HDFS agora dá suporte ao formato de arquivo ORC, além de Texto e Avro. (A Origem do Arquivo HDFS dá suporte apenas Texto e Avro.) Para obter mais informações sobre esse componente, consulte [HDFS File Destination](../integration-services/data-flow/hdfs-file-destination.md).  

####  <a name="odbc2016"></a> Componentes ODBC atualizados para o SQL Server 2016  
 Os componentes de Origem e Destino ODBC foram atualizadas para fornecer compatibilidade total com o SQL Server 2016. Não há nenhuma nova funcionalidade e não há alterações no comportamento.  

####  <a name="Excel2016"></a> Suporte explícito para fontes de dados do Excel 2016  
 O Gerenciador de Conexões do Excel, a Origem do Excel e o Destino do Excel agora fornecem suporte explícito para fontes de dados do Excel 2016.  

####  <a name="SAPBW"></a> Conector para SAP BW para SQL Server 2016 liberado  
 O Microsoft® Connector para SAP BW para Microsoft SQL Server® 2016 foi lançado como parte do SQL Server 2016 Feature Pack. Para baixar os componentes do Feature Pack, consulte [Microsoft® SQL Server® 2016 Feature Pack](http://go.microsoft.com/fwlink/?LinkID=746297).
 
#### <a name="oracleteradata"></a> Conectores v4.0 para Oracle e Teradata liberados
O Conectores v4.0 da Microsoft para Oracle e Teradata foram lançados. Para baixar os conectores, consulte [Conectores v4.0 da Microsoft para Oracle e Teradata](https://www.microsoft.com/download/details.aspx?id=52950).

### <a name="pdwau5"></a> Conectores para a Atualização 5 do Dispositivo do Analytics Platform System (PDW) liberados
Os adaptadores de destino para carregar dados em PDW com AU5 foram lançados. Para baixar os adaptadores, consulte [Documentação e ferramentas de cliente da Atualização 5 do dispositivo do Sistema de plataforma de análise](https://www.microsoft.com/download/details.aspx?id=51610).

### <a name="expanded-connectivity-to-the-cloud"></a>Conectividade expandida com a nuvem

####  <a name="AFP2016"></a> Azure Feature Pack para SSIS lançado para o SQL Server 2016  
 O Azure Feature Pack para o Integration Services foi lançado para o SQL Server 2016. O feature pack contém gerenciadores de conexões para conectar-se a fontes de dados do Azure e tarefas para realizar as operações comuns do Azure. Para obter mais informações, consulte [Feature Pack do Azure para o Integration Services &#40;SSIS&#41;](../integration-services/azure-feature-pack-for-integration-services-ssis.md).  

#### <a name="dynamics"></a> Suporte para recursos online do Microsoft Dynamics liberado no Service Pack 1

Com o SQL Server 2016 Service Pack 1 instalado, o Gerenciador de Fontes e de Conexões OData agora tem suporte para conexão aos feeds OData do Microsoft Dynamics AX Online e do Microsoft Dynamics CRM Online.

#### <a name="datalakestore"></a> Suporte para Azure Data Lake Store lançado

A versão mais recente do Feature Pack do Azure inclui um gerenciador de conexões, a origem e o destino para mover dados para e do Azure Data Lake Store. Para saber mais, veja [Feature Pack do Azure para o Integration Services &#40;SSIS&#41;](../integration-services/azure-feature-pack-for-integration-services-ssis.md)

#### <a name="sqldwupload"></a> Suporte para Azure SQL Data Warehouse lançado

A versão mais recente do Feature Pack do Azure inclui a tarefa de Upload do Azure SQL DW para preencher o SQL Data Warehouse com dados. Para saber mais, veja [Feature Pack do Azure para o Integration Services &#40;SSIS&#41;](../integration-services/azure-feature-pack-for-integration-services-ssis.md)

## <a name="usability-and-productivity"></a>Usabilidade e produtividade  
 
### <a name="better-install-experience"></a>Melhor experiência de instalação

####  <a name="Upgrade"></a> Atualização bloqueada quando o SSISDB pertence a um Grupo de Disponibilidade  
 Se o SSISDB (banco de dados de catálogo SSIS) pertencer a um Grupo de Disponibilidade AlwaysOn, você precisará remover o SSISDB do grupo de disponibilidade, atualizar o SQL Server e, em seguida, adicionar o SSISDB de volta ao grupo de disponibilidade. Para obter mais informações, consulte [Upgrading SSISDB in an availability group](../integration-services/service/ssis-catalog.md#Upgrade).  

### <a name="better-design-experience"></a>Melhor experiência de design

####  <a name="OneDesigner"></a> Suporte multiplataforma e a várias versões no Designer SSIS  
 Agora você pode usar o Designer SSIS no SSDT (SQL Server Data Tools) para Visual Studio 2015 para criar, manter e executar pacotes destinados ao SQL Server 2016, SQL Server 2014 ou SQL Server 2012. Para obter o SSDT, consulte [Baixar o SQL Server Data Tools mais recente](../ssdt/download-sql-server-data-tools-ssdt.md). 

 No Gerenciador de Soluções, clique com o botão direito do mouse em um projeto do Integration Services e selecione **Propriedades** para abrir as páginas de propriedades do projeto. Na guia **Geral** de **Propriedades de Configuração**, selecione a propriedade **TargetServerVersion** e, em seguida, escolha o SQL Server 2012, SQL Server 2014 ou SQL Server 2016.  
   
 ![Propriedade TargetServerVersion na caixa de diálogo de propriedades do projeto](../integration-services/media/targetserverversion2.png "Propriedade TargetServerVersion na caixa de diálogo de propriedades do projeto")  

>   [!IMPORTANT]
> Se você desenvolver extensões personalizadas para SSIS, consulte [Suporte multiplataforma em seus componentes personalizados](../integration-services/extending-packages-custom-objects/support-multi-targeting-in-your-custom-components.md) e [Obter extensões personalizadas do SSIS para suporte em várias versões do SSDT 2015 para SQL Server 2016](https://blogs.msdn.microsoft.com/ssis/2016/04/19/getting-your-ssis-custom-extensions-to-be-supported-by-the-multi-version-support-of-ssdt-2015-for-sql-server-2016/).  

### <a name="better-management-experience-in-sql-server-management-studio"></a>Melhor experiência de gerenciamento no SQL Server Management Studio

####  <a name="CatViews"></a> Desempenho aprimorado para exibições do Catálogo do SSIS  
 A maioria das exibições de catálogo do SSIS agora funcionam melhor quando são executadas por um usuário que não é um membro da função ssis_admin.  

### <a name="other-enhancements"></a>Outros aprimoramentos

####  <a name="BDDinbox"></a> A transformação do Distribuidor de Dados Equilibrado agora faz parte do SSIS  
 A transformação do Distribuidor de Dados Equilibrado, que exigia um download separado em versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], agora é instalado quando você instala o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Para obter mais informações, consulte [Balanced Data Distributor Transformation](../integration-services/data-flow/transformations/balanced-data-distributor-transformation.md).  
  
####  <a name="ComplexFeedinbox"></a> Os componentes de publicação de feed de dados agora fazem parte do SSIS  
 Os componentes de publicação de feed de dados, que exigiam um download separado em versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], agora são instalados quando você instala o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Para obter mais informações, consulte [Data Streaming Destination](../integration-services/data-flow/data-streaming-destination.md).  

####  <a name="AzureBlob"></a> Suporte para o Armazenamento de Blobs do Azure no Assistente de Importação e Exportação do SQL Server  
 O Assistente de Importação e Exportação do SQL Server agora pode importar dados de e salvar dados no Armazenamento de Blobs do Azure. Para obter mais informações, consulte [Escolha uma fonte de dados &#40;Assistente de Importação e Exportação do SQL Server&#41;](../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md) e [Escolha um destino &#40;Assistente de Importação e Exportação do SQL Server&#41;](../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md). 

####  <a name="CDCOracle"></a> Change Data Capture Designer e Service para Oracle para Microsoft SQL Server 2016 liberados  
 Microsoft® Change Data Capture Designer e Service for Oracle da Attunity para Microsoft SQL Server® 2016 foram lançados como parte do SQL Server 2016 Feature Pack.  Esses componentes agora dão suporte a Oracle 12c na instalação clássica. (Não há suporte para instalação multilocatário) Para baixar os componentes do Feature Pack, consulte [Microsoft® SQL Server® 2016 Feature Pack](http://go.microsoft.com/fwlink/?LinkID=746297).  
  
####  <a name="cdc2016"></a> Componentes CDC atualizados para o SQL Server 2016  
 Os componentes Control Task, Source e Splitter Transformation do CDC (Change Data Capture) foram atualizados para fornecer compatibilidade total com o SQL Server 2016. Não há nenhuma nova funcionalidade e não há alterações no comportamento.  
  
####  <a name="ASDDL"></a> Tarefa Executar DDL do Analysis Services atualizada  
 A Tarefa Executar DDL do Analysis Services foi atualizada para aceitar comandos de linguagem de script de modelo de tabela.

####  <a name="ssasrc0"></a> As tarefas do Analysis Services dão suporte a modelos de tabela  
 Agora você pode usar todas as tarefas e destinos SSIS que dão suporte ao SSAS (SQL Server Analysis Services) com modelos de tabela do SQL Server 2016. As tarefas SSIS foram atualizadas para representar objetos de tabela em vez de objetos multidimensionais. Por exemplo, quando você seleciona objetos a processar, a tarefa de processamento detecta automaticamente que é um modelo de tabela e exibe uma lista de objetos tabulares em vez de grupos de medidas e dimensões. O Destino de Processamento de Partições agora também mostra objetos tabulares e dá suporte ao envio de dados por push para uma partição.  
  
 O Destino de Processamento de Dimensões não funciona para modelos de tabela com o nível de compatibilidade do SQL 2016.  A Tarefa Processamento do Analysis Services e o Destino de Processamento de Partições são tudo o que você precisa para o processamento de tabelas. 

####  <a name="builtinR"></a> Suporte para R Services interno  
 O SSIS já dá suporte aos serviços do R internos no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Você pode usar o SSIS não apenas para extrair dados e carregar a saída da análise, mas para compilar, executar e periodicamente treinar novamente modelos do R. Para obter mais informações, consulte a postagem de blog a seguir. [Operacionalizar seu projeto de aprendizado de máquina usando o SQL Server 2016 SSIS e os Serviços do R](http://blogs.msdn.com/b/ssis/archive/2016/01/12/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services.aspx). 

####  <a name="ValidateXML"></a> Saída de validação de XML avançada na Tarefa XML  
 Valide documentos XML e obtenha saída de erros completa habilitando a propriedade **ValidationDetails** da tarefa XML. Antes da disponibilidade da propriedade **ValidationDetails** , a validação do XML pela tarefa XML retornava apenas um resultado true ou false, sem informações sobre erros ou suas localizações. Agora, quando você define **ValidationDetails** como true, o arquivo de saída contém informações detalhadas sobre cada erro, incluindo o número de linha e a posição. Você pode usar essas informações para entender, localizar e corrigir erros em documentos XML. Para obter mais informações, consulte [Validate XML with the XML Task](../integration-services/control-flow/validate-xml-with-the-xml-task.md).  
  
 O[!INCLUDE[ssIS](../includes/ssis-md.md)] introduziu a propriedade **ValidationDetails** no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Service Pack 2. Essa nova propriedade não foi anunciada ou documentada naquele momento. A propriedade **ValidationDetails** também está disponível em [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] e em [!INCLUDE[ssSQL15](../includes/sssql15-md.md)].   

## <a name="see-also"></a>Consulte também  
 [Novidades no SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)   
 [Edições e recursos com suporte para SQL Server 2016](../sql-server/editions-and-supported-features-for-sql-server-2016.md)
  
  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../includes/feedback-stackoverflow-msdn-connect-md.md)]

