---
title: "Integration Services (SSIS) conexões | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.connectionmanager.f1
- sql13.dts.designer.adddtsconnection.f1
helpviewer_keywords:
- Integration Services packages, connections
- SSIS packages, connections
- sources [Integration Services], connections
- packages [Integration Services], connections
- destinations [Integration Services], connections
- tasks [Integration Services], connections
- connections [Integration Services], about connections
- connections [Integration Services]
- SQL Server Integration Services packages, connections
ms.assetid: 72f5afa3-d636-410b-9e81-2ffa27772a8c
caps.latest.revision: 92
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 34233d51def3269b21432ac3b297d641dfd74687
ms.contentlocale: pt-br
ms.lasthandoff: 09/21/2017

---
# <a name="integration-services-ssis-connections"></a>Conexões do SSIS (Integration Services)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usam conexões para executar diferentes tarefas e implementar recursos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
-   Conectar com armazenamentos de dados de origem e de destino, como texto, XML, pastas de trabalho do Excel e bancos de dados relacionais para extrair e carregar dados.  
  
-   Conectar com bancos de dados relacionais que contêm dados de referência para executar pesquisas exatas ou difusas.  
  
-   Conectar com bancos de dados relacionais para executar instruções SQL, como os comandos SELECT, DELETE e INSERT e também procedimentos armazenados.  
  
-   Conectar com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para executar tarefas de manutenção e transferência, como backup de bancos de dados e transferência de logons.  
  
-   Gravar entradas de log em arquivos de texto e XML e tabelas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e configurações de pacote em tabelas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Conectar com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para criar tabelas de trabalho temporárias, exigidas por algumas transformações para fazer o seu trabalho.  
  
-   Conectar com projetos e bancos de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para acessar modelos de mineração de dados, cubos e dimensões de processo e para executar códigos DDL.  
  
-   Especificar arquivos e pastas existentes ou criar novos para usar com enumeradores e tarefas Loop Foreach.  
  
-   Conectar com filas de mensagens e com a WMI (Instrumentação de Gerenciamento do Windows), o SMO ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects), a Web e servidores de email.  
  
 Para estabelecer essas conexões, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa gerenciadores de conexões, conforme descrito na próxima seção.  
  
## <a name="connection-managers"></a>Gerenciadores de conexões  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa o gerenciador de conexões como uma representação lógica de uma conexão. Em tempo de design, você define as propriedades de um gerenciador de conexões para descrever a conexão física que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria quando o pacote é executado. Por exemplo, um gerenciador de conexões inclui a propriedade **ConnectionString** que você define em tempo de design; em tempo de execução, uma conexão física é criada usando o valor na propriedade da cadeia de conexão.  
  
 Um pacote pode usar várias instâncias de um tipo de gerenciador de conexões e você pode definir as propriedades em cada instância. Em tempo de execução, cada instância de um tipo de gerenciador de conexões cria uma conexão que tem atributos diferentes.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece diferentes tipos de gerenciadores de conexões que permitem a conexão de pacotes com várias fontes de dados e servidores.  
  
-   Há gerenciadores de conexões internos que a Instalação instala durante a instalação do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
-   Há gerenciadores de conexões disponíveis para download no site da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
-   Você poderá criar seu próprio gerenciador de conexões personalizado se os gerenciadores de conexões existentes não atenderem às suas necessidades.  

### <a name="package-level-and-project-level-connection-managers"></a>Nível de pacote e projeto de nível de gerenciadores de conexão
Um gerenciador de conexões pode ser criado no nível de pacote ou no nível de projeto. O gerenciador de conexões criado no nível de projeto está disponível para todos os pacotes no projeto. Por outro lado, o gerenciador de conexões criado no nível de pacote está disponível para aquele pacote específico.  
  
 Use gerenciadores de conexões que são criados no nível de projeto em vez de fontes de dados, para compartilhar conexões com origens. Para adicionar um gerenciador de conexões no nível de projeto, o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] deve usar o modelo de implantação de projeto. Quando um projeto é configurado para usar este modelo, a pasta **Gerenciadores de Conexões** é exibida no **Gerenciador de Soluções**e a pasta **Fontes de Dados** é removida do **Gerenciador de Soluções**.  
  
> [!NOTE]  
>  Se você quiser usar fontes de dados em seu pacote, precisará converter o projeto para o modelo de implantação do pacote.  
>   
>  Para obter mais informações sobre os dois modelos e sobre como converter um projeto para o modelo de implantação de projeto, consulte [implantar Integration Services (SSIS) projetos e pacotes](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md).

### <a name="built-in-connection-managers"></a>Gerenciadores de conexões internos  
 A tabela a seguir lista os tipos de gerenciadores de conexões fornecidos pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
|Tipo|Description|Tópico|  
|----------|-----------------|-----------|  
|ADO|Conecta-se a objetos ActiveX Data Objects (ADO).|[Gerenciador de conexões ADO](../../integration-services/connection-manager/ado-connection-manager.md)|  
|ADO.NET|Conecta-se a uma fonte de dados usando um provedor .NET.|[Gerenciador de conexões ADO.NET](../../integration-services/connection-manager/ado-net-connection-manager.md)|  
|CACHE|Lê dados do fluxo de dados ou de um arquivo de cache (.caw) e pode salvar esses dados em um arquivo de cache.|[Gerenciador de Conexões de Cache](../../integration-services/connection-manager/cache-connection-manager.md)|  
|DQS|Conecta-se a um servidor a um banco de dados do Data Quality Services no servidor.|[Gerenciador de Conexões de Limpeza DQS](../../integration-services/connection-manager/dqs-cleansing-connection-manager.md)|  
|EXCEL|Conecta-se a um arquivo da pasta de trabalho do Excel.|[Gerenciador de conexões do Excel](../../integration-services/connection-manager/excel-connection-manager.md)|  
|FILE|Conecta-se a um arquivo ou uma pasta.|[Gerenciador de conexões de arquivos](../../integration-services/connection-manager/file-connection-manager.md)|  
|FLATFILE|Conecta-se a dados em um único arquivo simples.|[Gerenciador de conexões de arquivos simples](../../integration-services/connection-manager/flat-file-connection-manager.md)|  
|FTP|Conecta-se a um servidor FTP.|[Gerenciador de conexões FTP](../../integration-services/connection-manager/ftp-connection-manager.md)|  
|HTTP|Conecta-se a um servidor Web.|[Gerenciador de conexões HTTP](../../integration-services/connection-manager/http-connection-manager.md)|  
|MSMQ|Conecta-se a uma fila de mensagens.|[Gerenciador de conexões MSMQ](../../integration-services/connection-manager/msmq-connection-manager.md)|  
|MSOLAP100|Conecta-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou a um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|[Gerenciador de conexões do Analysis Services](../../integration-services/connection-manager/analysis-services-connection-manager.md)|  
|MULTIFILE|Conecta-se a vários arquivos e pastas.|[Gerenciador de Conexões de vários arquivos](../../integration-services/connection-manager/multiple-files-connection-manager.md)|  
|MULTIFLATFILE|Conecta-se a vários arquivos e pastas de dados.|[Gerenciador de conexões de vários arquivos simples](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)|  
|OLEDB|Conecta-se a uma fonte de dados usando um provedor OLE DB.|[Gerenciador de conexões OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md)|  
|ODBC|Conecta-se a uma fonte de dados usando ODBC.|[Gerenciador de conexões ODBC](../../integration-services/connection-manager/odbc-connection-manager.md)|  
|SMOServer|Conecta-se a um servidor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects (SMO).|[Gerenciador de conexões SMO](../../integration-services/connection-manager/smo-connection-manager.md)|  
|SMTP|Conecta-se a um servidor de email SMTP.|[Gerenciador de conexões SMTP](../../integration-services/connection-manager/smtp-connection-manager.md)|  
|SQLMOBILE|Conecta-se a um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.|[Gerenciador de Conexões do SQL Server Compact Edition](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|  
|WMI|Conecta-se a um servidor e especifica o escopo de gerenciamento de Instrumentação de Gerenciamento do Windows (WMI) no servidor.|[Gerenciador de conexões WMI](../../integration-services/connection-manager/wmi-connection-manager.md)|  
  
### <a name="connection-managers-available-for-download"></a>Gerenciadores de conexão disponíveis para download  
 A tabela a seguir lista tipos adicionais de gerenciadores de conexões que podem ser baixados no site da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
> [!IMPORTANT]  
>  Os gerenciadores de conexões listados na tabela a seguir funcionam apenas com o [!INCLUDE[ssEnterpriseEd11](../../includes/ssenterpriseed11-md.md)] e o [!INCLUDE[ssDeveloperEd11](../../includes/ssdevelopered11-md.md)].  
  
|Tipo|Description|Tópico|  
|----------|-----------------|-----------|  
|ORACLE|Conecta-se a um Oracle \<informações de versão\> server.|O gerenciador de conexões Oracle é o componente de gerenciador de conexões do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector para Oracle da Attunity. O [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector para Oracle da Attunity também inclui uma origem e um destino. Para obter mais informações, consulte a página de download de [Microsoft Connectors para Oracle e Teradata da Attunity](http://go.microsoft.com/fwlink/?LinkId=251526).|  
|SAPBI|Conecta a um sistema SAP NetWeaver BI versão 7.|O gerenciador de conexões SAP BI é o componente de gerenciador de conexões do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector para SAP BI. O [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector para SAP BI também inclui uma origem e um destino. Para obter mais informações, consulte a página de download [Microsoft SQL Server 2008 Feature Pack](http://go.microsoft.com/fwlink/?LinkId=262016).|  
|TERADATA|Conecta-se a um Teradata \<informações de versão\> server.|O gerenciador de conexões Teradata é o componente de gerenciador de conexões do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector para Teradata da Attunity. O [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector para Teradata da Attunity também inclui uma origem e um destino. Para obter mais informações, consulte a página de download de [Microsoft Connectors para Oracle e Teradata da Attunity](http://go.microsoft.com/fwlink/?LinkId=251526).|  
  
### <a name="custom-connection-managers"></a>Gerenciadores de conexões personalizados  
 Também é possível escrever gerenciadores de conexões personalizados. Para obter mais informações, consulte [Developing a Custom Connection Manager](../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md).  
  
## <a name="create-connection-managers"></a>Criar gerenciadores de conexão
  O [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui uma variedade de gerenciadores de conexões adequados às necessidades das tarefas para se conectarem aos diferentes tipos de servidores e fontes de dados. Os gerenciadores de conexões são usados pelos componentes do fluxo de dados, que extraem e carregam dados em diferentes tipos de armazenamentos de dados, e pelos provedores de log que gravam logs em um servidor, tabela ou arquivo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Por exemplo, um pacote com uma tarefa Enviar Email usa um tipo de gerenciador de conexões para conectar-se a um servidor de protocolo SMTP (Simple Mail Transfer Protocol). Um pacote com uma tarefa Executar SQL pode usar um gerenciador de conexões OLE DB para conectar-se a um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [Integration Services &#40;SSIS&#41; Conexões](../../integration-services/connection-manager/integration-services-ssis-connections.md).  
  
 Para criar automaticamente e configurar gerenciadores de conexões ao criar um novo pacote, é possível usar o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O assistente também ajuda a criar e configurar origens e destinos que usam os gerenciadores de conexões. Para obter mais informações, consulte [Create Packages in SQL Server Data Tools](../../integration-services/create-packages-in-sql-server-data-tools.md).  
  
 Para criar manualmente um novo gerenciador de conexões e adicioná-lo a um pacote existente, use a área **Gerenciadores de Conexões** que aparece nas guias **Fluxo de Controle**, **Fluxo de Dados**e **Manipuladores de Eventos** do Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Na área **Gerenciador de Conexões** , você escolhe o tipo de gerenciador de conexões a ser criado e então define as propriedades do gerenciador de conexões usando uma caixa de diálogo que o Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] fornece. Para obter mais informações, consulte a seção “Usando a área Gerenciadores de Conexões”, mais adiante neste tópico.  
  
 Depois que o gerenciador de conexões for adicionado a um pacote, você poderá usá-lo em suas tarefas, contêineres Loop Foreach, fontes, transformações e destinos. Para obter mais informações, consulte [Tarefas do Integration Services](../../integration-services/control-flow/integration-services-tasks.md), [Contêiner Foreach Loop](../../integration-services/control-flow/foreach-loop-container.md) e [Fluxo de Dados](../../integration-services/data-flow/data-flow.md).  
  
### <a name="using-the-connection-managers-area"></a>Usando a área de gerenciadores de conexões  
 Você pode criar gerenciadores de conexões enquanto a guia **Fluxo de Controle**, **Fluxo de Dados**ou **Manipuladores de Eventos** do Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] estiver ativa.  
  
 O diagrama a seguir mostra a área **Gerenciadores de Conexões** na guia **Fluxo de Controle** do Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 ![Captura de tela do designer de fluxo de controle com pacote](../../integration-services/connection-manager/media/samplecontrolflow.gif "captura de tela do designer de fluxo de controle com pacote")    
  
### <a name="32-bit-and-64-bit-providers-for-connection-managers"></a>Provedores de 32 bits e 64 bits para gerenciadores de conexões  
 Muitos dos provedores que os gerenciadores de conexões usam estão disponíveis em versões de 32 bits e 64 bits. O ambiente de design do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é um ambiente de 32 bits e você visualiza apenas provedores de 32 bits enquanto está projetando um pacote. Portanto, você só poderá configurar um gerenciador de conexões para usar um provedor de 64 bits específico, se a versão de 32 bits do mesmo provedor também estiver instalada.  
  
 No tempo de execução, a versão correta é usada e não importa se você especificou a versão de 32 bits do provedor no tempo de design. A versão de 64 bits do provedor pode ser executada mesmo que o pacote esteja sendo executado no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Ambas as versões do provedor têm o mesmo ID. Para especificar se a [! INCLUIR[ssISnoversion](/sql-docs/docs/integration-services/integration-services-ssis-development-and-management-tools).  

## <a name="add-a-connection-manager"></a>Adicionar um Gerenciador de conexão
###  <a name="wizard"></a>Adicionar um Gerenciador de conexão quando você cria um pacote  
  
-   Usar o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]   
  
     Além de criar e configurar um gerenciador de conexões, o assistente também ajuda a criar e configurar origens e destinos que usam o gerenciador de conexões. Para obter mais informações, consulte [Create Packages in SQL Server Data Tools](../../integration-services/create-packages-in-sql-server-data-tools.md).  
  
###  <a name="package"></a>Adicionar um Gerenciador de conexão a um pacote existente  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo  
  
3.  No Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] , clique na guia **Controle de Fluxo** , na guia **Fluxo de Dados** , ou na guia **Manipulador de Eventos** para disponibilizar o **Gerenciador de Conexões** .  
  
4.  Clique com o botão direito do mouse em qualquer lugar na área **Gerenciadores de Conexões** e execute uma das seguintes ações:  
  
    -   Clique no tipo de gerenciador de conexões que será adicionado ao pacote.  
  
         — ou —  
  
    -   Se o tipo que deseja adicionar não estiver listado, clique em **Nova Conexão** para abrir a caixa de diálogo **Adicionar Gerenciador de Conexões SSIS** , selecione um tipo de gerenciador de conexões e clique em **OK**.  
  
     A caixa de diálogo personalizada para o tipo de gerenciador de conexões selecionado é aberta. Para obter mais informações sobre tipos de gerenciador de conexões e as opções que estão disponíveis, consulte a tabela de opções a seguir.  
  
    |Gerenciador de conexões|Opções|  
    |------------------------|-------------|  
    |[Gerenciador de conexões ADO](../../integration-services/connection-manager/ado-connection-manager.md)|[Configurar Gerenciador de Conexões OLE DB](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[Gerenciador de conexões ADO.NET](../../integration-services/connection-manager/ado-net-connection-manager.md)|[Configurar Gerenciador de Conexões ADO.NET](../../integration-services/connection-manager/configure-ado-net-connection-manager.md)|  
    |[Gerenciador de Conexões do Analysis Services](../../integration-services/connection-manager/analysis-services-connection-manager.md)|[Referência de IU da caixa de diálogo Adicionar Gerenciador de Conexões do Analysis Services](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Gerenciador de Conexões do Excel](../../integration-services/connection-manager/excel-connection-manager.md)|[Editor de Gerenciador de Conexão do Excel](../../integration-services/connection-manager/excel-connection-manager-editor.md)|  
    |[Gerenciador de Conexões de Arquivos](../../integration-services/connection-manager/file-connection-manager.md)|[Editor do Gerenciador de Conexão de arquivos](../../integration-services/connection-manager/file-connection-manager-editor.md)|  
    |[Gerenciador de Conexões de Vários Arquivos](../../integration-services/connection-manager/multiple-files-connection-manager.md)|[Referência de IU da caixa de diálogo Adicionar Gerenciador de Conexões de Arquivos](../../integration-services/connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[Gerenciador de Conexões de Arquivos Simples](../../integration-services/connection-manager/flat-file-connection-manager.md)|[Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Geral&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md)<br /><br /> [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Colunas&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Avançado&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Visualização&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md)|  
    |[Gerenciador de Conexões de Vários Arquivos Simples](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)|[Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Geral&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Colunas&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Avançado&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Visualização&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[Gerenciador de Conexões de FTP](../../integration-services/connection-manager/ftp-connection-manager.md)|[Editor do Gerenciador de Conexão de FTP](../../integration-services/connection-manager/ftp-connection-manager-editor.md)|  
    |[Gerenciador de Conexões de HTTP](../../integration-services/connection-manager/http-connection-manager.md)|[Editor do Gerenciador de Conexões HTTP &#40;Página Servidor&#41;](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)<br /><br /> [Editor do Gerenciador de Conexões HTTP &#40;Página Proxy&#41;](../../integration-services/connection-manager/http-connection-manager-editor-proxy-page.md)|  
    |[Gerenciador de Conexões MSMQ](../../integration-services/connection-manager/msmq-connection-manager.md)|[Editor de Gerenciador de Conexão do MSMQ](../../integration-services/connection-manager/msmq-connection-manager-editor.md)|  
    |[Gerenciador de Conexões ODBC](../../integration-services/connection-manager/odbc-connection-manager.md)|[Referência da interface do usuário do Gerenciador de Conexões ODBC](../../integration-services/connection-manager/odbc-connection-manager-ui-reference.md)|  
    |[Gerenciador de Conexões OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md)|[Configurar Gerenciador de Conexões OLE DB](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[Gerenciador de Conexões SMO](../../integration-services/connection-manager/smo-connection-manager.md)|[Editor do Gerenciador de Conexão de SMO](../../integration-services/connection-manager/smo-connection-manager-editor.md)|  
    |[Gerenciador de Conexões SMTP](../../integration-services/connection-manager/smtp-connection-manager.md)|[Editor do Gerenciador de Conexão de SMTP](../../integration-services/connection-manager/smtp-connection-manager-editor.md)|  
    |[Gerenciador de Conexões do SQL Server Compact Edition](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|[Editor do Gerenciador de Conexões do SQL Server Compact Edition &#40;Página de Conexão&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [Editor do Gerenciador de Conexões do SQL Server Compact Edition &#40;Página Tudo&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[Gerenciador de Conexões WMI](../../integration-services/connection-manager/wmi-connection-manager.md)|[Editor do Gerenciador de Conexão de WMI](../../integration-services/connection-manager/wmi-connection-manager-editor.md)|  
  
     A área **Gerenciadores de Conexões** lista o gerenciador de conexões adicionado.  
  
5.  Como opção, clique com o botão direito do mouse no gerenciador de conexões, clique em **Renomear**e modifique o nome padrão do gerenciador de conexões.  
  
6.  Para salvar o pacote atualizado, clique em **Salvar Item Selecionado** no menu **Arquivo** .  
  
###  <a name="project"></a>Adicionar um Gerenciador de conexão no nível de projeto  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
2.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Gerenciadores de Conexões**e clique em **Novo Gerenciador de Conexões**.  
  
3.  Na caixa de diálogo **Adicionar Gerenciador de Conexões SSIS** , selecione o tipo de gerenciador de conexões e clique em **Adicionar**.  
  
     A caixa de diálogo personalizada para o tipo de gerenciador de conexões selecionado é aberta. Para obter mais informações sobre tipos de gerenciador de conexões e as opções que estão disponíveis, consulte a tabela de opções a seguir.  
  
    |Gerenciador de conexões|Opções|  
    |------------------------|-------------|  
    |[Gerenciador de conexões ADO](../../integration-services/connection-manager/ado-connection-manager.md)|[Configurar Gerenciador de Conexões OLE DB](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[Gerenciador de conexões ADO.NET](../../integration-services/connection-manager/ado-net-connection-manager.md)|[Configurar Gerenciador de Conexões ADO.NET](../../integration-services/connection-manager/configure-ado-net-connection-manager.md)|  
    |[Gerenciador de Conexões do Analysis Services](../../integration-services/connection-manager/analysis-services-connection-manager.md)|[Referência de IU da caixa de diálogo Adicionar Gerenciador de Conexões do Analysis Services](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Gerenciador de Conexões do Excel](../../integration-services/connection-manager/excel-connection-manager.md)|[Editor de Gerenciador de Conexão do Excel](../../integration-services/connection-manager/excel-connection-manager-editor.md)|  
    |[Gerenciador de Conexões de Arquivos](../../integration-services/connection-manager/file-connection-manager.md)|[Editor do Gerenciador de Conexão de arquivos](../../integration-services/connection-manager/file-connection-manager-editor.md)|  
    |[Gerenciador de Conexões de Vários Arquivos](../../integration-services/connection-manager/multiple-files-connection-manager.md)|[Referência de IU da caixa de diálogo Adicionar Gerenciador de Conexões de Arquivos](../../integration-services/connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[Gerenciador de Conexões de Arquivos Simples](../../integration-services/connection-manager/flat-file-connection-manager.md)|[Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Geral&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md)<br /><br /> [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Colunas&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Avançado&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Visualização&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md)|  
    |[Gerenciador de Conexões de Vários Arquivos Simples](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)|[Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Geral&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Colunas&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Avançado&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Visualização&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[Gerenciador de Conexões de FTP](../../integration-services/connection-manager/ftp-connection-manager.md)|[Editor do Gerenciador de Conexão de FTP](../../integration-services/connection-manager/ftp-connection-manager-editor.md)|  
    |[Gerenciador de Conexões de HTTP](../../integration-services/connection-manager/http-connection-manager.md)|[Editor do Gerenciador de Conexões HTTP &#40;Página Servidor&#41;](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)<br /><br /> [Editor do Gerenciador de Conexões HTTP &#40;Página Proxy&#41;](../../integration-services/connection-manager/http-connection-manager-editor-proxy-page.md)|  
    |[Gerenciador de Conexões MSMQ](../../integration-services/connection-manager/msmq-connection-manager.md)|[Editor de Gerenciador de Conexão do MSMQ](../../integration-services/connection-manager/msmq-connection-manager-editor.md)|  
    |[Gerenciador de Conexões ODBC](../../integration-services/connection-manager/odbc-connection-manager.md)|[Referência da interface do usuário do Gerenciador de Conexões ODBC](../../integration-services/connection-manager/odbc-connection-manager-ui-reference.md)|  
    |[Gerenciador de Conexões OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md)|[Configurar Gerenciador de Conexões OLE DB](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[Gerenciador de Conexões SMO](../../integration-services/connection-manager/smo-connection-manager.md)|[Editor do Gerenciador de Conexão de SMO](../../integration-services/connection-manager/smo-connection-manager-editor.md)|  
    |[Gerenciador de Conexões SMTP](../../integration-services/connection-manager/smtp-connection-manager.md)|[Editor do Gerenciador de Conexão de SMTP](../../integration-services/connection-manager/smtp-connection-manager-editor.md)|  
    |[Gerenciador de Conexões do SQL Server Compact Edition](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|[Editor do Gerenciador de Conexões do SQL Server Compact Edition &#40;Página de Conexão&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [Editor do Gerenciador de Conexões do SQL Server Compact Edition &#40;Página Tudo&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[Gerenciador de Conexões WMI](../../integration-services/connection-manager/wmi-connection-manager.md)|[Editor do Gerenciador de Conexão de WMI](../../integration-services/connection-manager/wmi-connection-manager-editor.md)|  
  
     O gerenciador de conexões que você adicionou aparecerá sob o nó **Gerenciadores de Conexões** no **Gerenciador de Soluções**. Ele também aparecerá na guia **Gerenciadores de Conexões** na janela **Designer SSIS** para todos os pacotes no projeto. O nome do gerenciador de conexões nesta guia terá um prefixo **(projeto)** para diferenciar este gerenciador de conexões de nível de projeto dos gerenciadores de conexões de nível de pacote.  
  
4.  Como opção, clique com o botão direito do mouse no gerenciador de conexões na janela **Gerenciador de Soluções** no nó **Gerenciadores de Conexões** ou na guia **Gerenciadores de Conexões** da janela **Designer SSIS** , clique em **Renomear**e modifique o nome padrão do gerenciador de conexões.  
  
    > [!NOTE]  
    >  Na guia **Gerenciadores de Conexões** da janela **Designer SSIS** , você não poderá substituir o prefixo **(projeto)** do nome do gerenciador de conexões. Isso ocorre por design.  

### <a name="add-ssis-connection-manager-dialog-box"></a>Adicionar caixa de diálogo Gerenciador de Conexão do SSIS
Use a caixa de diálogo **Adicionar Gerenciador de Conexões SSIS** para selecionar o tipo de conexão a adicionar a um pacote.  
  
 Para saber mais sobre gerenciadores de conexões, consulte [Conexões do SSIS &#40;Integration Services&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md).  
  
#### <a name="options"></a>Opções  
 **Tipo de Gerenciador de Conexão**  
 Selecione um tipo de conexão e clique em **Adicionar**ou clique duas vezes em um tipo de conexão, para especificar propriedades de conexão usando o editor para cada tipo de conexão.  
  
 **Adicionar**  
 Especifique propriedades de conexão usando o editor para cada tipo de conexão.  
   
##  <a name="parameter"></a>Criar um parâmetro para uma propriedade de Gerenciador de conexão  
  
1.  Na área **Gerenciadores de Conexões** , clique com o botão direito do mouse no gerenciador de conexões para o qual você deseja criar um parâmetro e clique em **Definir Parâmetros**.  
  
2.  Configure os parâmetros na caixa de diálogo **Definir Parâmetros** . Para obter mais informações, consulte [Parameterize Dialog Box](http://msdn.microsoft.com/library/fac02b6d-d247-447a-8940-e8700c7ac350).  

## <a name="delete-a-connection-manager"></a>Excluir um Gerenciador de conexão 
###  <a name="DeletePackageLevel"></a>Excluir um Gerenciador de conexão de um pacote  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  No Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] , clique na guia **Controle de Fluxo** , na guia **Fluxo de Dados** , ou na guia **Manipulador de Eventos** para disponibilizar o **Gerenciador de Conexões** .  
  
4.  Clique com o botão direito do mouse no gerenciador de conexões que deseja excluir e clique em **Excluir**.  
  
     Ao excluir um gerenciador de conexões utilizado por um elemento do pacote, como uma tarefa Executar SQL ou uma fonte OLE DB, você terá os seguintes resultados:  
  
    -   Um ícone de erro aparece no elemento do pacote que usou o gerenciador de conexões excluído.  
  
    -   O pacote não é validado.  
  
    -   O pacote não pode ser executado.  
  
5.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
###  <a name="DeleteProjectLevel"></a>Excluir um Gerenciador de conexão compartilhada (Gerenciador de conexão de nível de projeto)  
  
1.  Para excluir um gerenciador de conexões de nível de projeto, clique com o botão direito do mouse no gerenciador de conexões no nó **Gerenciadores de Conexões** na janela **Gerenciador de Soluções** e clique em **Excluir**. [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]Exibe a mensagem de aviso a seguir:  
  
    > [!WARNING]  
    >  Quando você exclui um gerenciador de conexões de projeto, os pacotes que usam o gerenciador de conexões podem não ser executados. Você não pode desfazer essa ação. Você quer excluir o gerenciador de conexões?  
  
2.  Clique em OK para excluir o gerenciador de conexões ou em Cancelar para mantê-lo.  
  
    > [!NOTE]  
    >  Você também pode excluir um gerenciador de conexões de nível de projeto da guia **Gerenciador de Conexões** da janela **Designer SSIS** aberta para qualquer pacote no projeto. Isso é feito clicando-se com o botão direito do mouse no gerenciador de conexões na guia e clicando em **Excluir**. 
    
## <a name="set-the-properties-of-a-connection-manager"></a>Definir as propriedades de um Gerenciador de Conexões
Todos os gerenciadores de conexões podem ser configurados usando a janela **Propriedades** .  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]também fornece caixas de diálogo personalizadas para modificar os diferentes tipos de gerenciadores de conexão em [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. A caixa de diálogo tem um conjunto diferente de opções que dependem do tipo de gerenciador de conexões.  
  
### <a name="modify-a-connection-manager-using-the-properties-window"></a>Modificar um Gerenciador de conexão usando a janela Propriedades  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  No SSIS Designer, clique na guia **Fluxo de Controle** , na guia **Fluxo de Dados** , ou na guia **Manipulador de Evento** para disponibilizar a área do **Gerenciador de Conexões** .  
  
4.  Clique com o botão direito do mouse no gerenciador de conexões e clique em **Propriedades**.  
  
5.  Na janela **Propriedades** , edite os valores de propriedades. A janela **Propriedades** fornece acesso a algumas propriedades que não são configuráveis no editor padrão de um gerenciador de conexões.  
  
6.  Clique em **OK**.  
  
7.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
### <a name="modify-a-connection-manager-using-a-connection-manager-dialog-box"></a>Modificar um Gerenciador de conexão usando uma caixa de diálogo Gerenciador de conexão  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  No Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] , clique na guia **Controle de Fluxo** , na guia **Fluxo de Dados** , ou na guia **Manipulador de Eventos** para disponibilizar o **Gerenciador de Conexões** .  
  
4.  Na área **Gerenciador de Conexões** , clique duas vezes no gerenciador de conexões para abrir a caixa de diálogo **Gerenciador de Conexões** . Para obter informações sobre tipos específicos de gerenciador de conexões e as opções disponíveis para cada tipo, veja a tabela a seguir.  
  
    |Gerenciador de Conexões|Opções|  
    |------------------------|-------------|  
    |[Gerenciador de conexões ADO](../../integration-services/connection-manager/ado-connection-manager.md)|[Configurar Gerenciador de Conexões OLE DB](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[Gerenciador de conexões ADO.NET](../../integration-services/connection-manager/ado-net-connection-manager.md)|[Configurar Gerenciador de Conexões ADO.NET](../../integration-services/connection-manager/configure-ado-net-connection-manager.md)|  
    |[Gerenciador de Conexões do Analysis Services](../../integration-services/connection-manager/analysis-services-connection-manager.md)|[Referência de IU da caixa de diálogo Adicionar Gerenciador de Conexões do Analysis Services](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Gerenciador de Conexões do Excel](../../integration-services/connection-manager/excel-connection-manager.md)|[Editor de Gerenciador de Conexão do Excel](../../integration-services/connection-manager/excel-connection-manager-editor.md)|  
    |[Gerenciador de Conexões de Arquivos](../../integration-services/connection-manager/file-connection-manager.md)|[Editor do Gerenciador de Conexão de arquivos](../../integration-services/connection-manager/file-connection-manager-editor.md)|  
    |[Gerenciador de Conexões de Vários Arquivos](../../integration-services/connection-manager/multiple-files-connection-manager.md)|[Referência de IU da caixa de diálogo Adicionar Gerenciador de Conexões de Arquivos](../../integration-services/connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[Gerenciador de Conexões de Arquivos Simples](../../integration-services/connection-manager/flat-file-connection-manager.md)|[Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Geral&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md)<br /><br /> [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Colunas&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Avançado&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Visualização&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md)|  
    |[Gerenciador de Conexões de Vários Arquivos Simples](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)|[Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Geral&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Colunas&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Avançado&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Visualização&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[Gerenciador de Conexões de FTP](../../integration-services/connection-manager/ftp-connection-manager.md)|[Editor do Gerenciador de Conexão de FTP](../../integration-services/connection-manager/ftp-connection-manager-editor.md)|  
    |[Gerenciador de Conexões de HTTP](../../integration-services/connection-manager/http-connection-manager.md)|[Editor do Gerenciador de Conexões HTTP &#40;Página Servidor&#41;](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)<br /><br /> [Editor do Gerenciador de Conexões HTTP &#40;Página Proxy&#41;](../../integration-services/connection-manager/http-connection-manager-editor-proxy-page.md)|  
    |[Gerenciador de Conexões MSMQ](../../integration-services/connection-manager/msmq-connection-manager.md)|[Editor de Gerenciador de Conexão do MSMQ](../../integration-services/connection-manager/msmq-connection-manager-editor.md)|  
    |[Gerenciador de Conexões ODBC](../../integration-services/connection-manager/odbc-connection-manager.md)|[Referência da interface do usuário do Gerenciador de Conexões ODBC](../../integration-services/connection-manager/odbc-connection-manager-ui-reference.md)|  
    |[Gerenciador de Conexões OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md)|[Configurar Gerenciador de Conexões OLE DB](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[Gerenciador de Conexões SMO](../../integration-services/connection-manager/smo-connection-manager.md)|[Editor do Gerenciador de Conexão de SMO](../../integration-services/connection-manager/smo-connection-manager-editor.md)|  
    |[Gerenciador de Conexões SMTP](../../integration-services/connection-manager/smtp-connection-manager.md)|[Editor do Gerenciador de Conexão de SMTP](../../integration-services/connection-manager/smtp-connection-manager-editor.md)|  
    |[Gerenciador de Conexões do SQL Server Compact Edition](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|[Editor do Gerenciador de Conexões do SQL Server Compact Edition &#40;Página de Conexão&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [Editor do Gerenciador de Conexões do SQL Server Compact Edition &#40;Página Tudo&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[Gerenciador de Conexões WMI](../../integration-services/connection-manager/wmi-connection-manager.md)|[Editor do Gerenciador de Conexão de WMI](../../integration-services/connection-manager/wmi-connection-manager-editor.md)|  
  
5.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  

## <a name="related-content"></a>Conteúdo relacionado  
  
-   Vídeo, [Aproveite o Microsoft Connector para Oracle da Attunity para melhorar o desempenho do pacote](http://technet.microsoft.com/sqlserver/gg598963.aspx), em technet.microsoft.com  
  
-   Artigos do Wiki, [Conectividade de SSIS](http://social.technet.microsoft.com/wiki/contents/articles/sql-server-integration-services-ssis.aspx#Connectivity), em social.technet.microsoft.com  
  
-   Entrada de blog, [Conectando ao MySQL a partir do SSIS](http://go.microsoft.com/fwlink/?LinkId=217669), em blogs.msdn.com.  
  
-   Artigo técnico, [Extraindo e carregando dados do SharePoint nos SQL Server Integration Services](http://go.microsoft.com/fwlink/?LinkId=247826), em msdn.microsoft.com.  
  
-   Artigo técnico, [Você obtém a mensagem de erro "DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER" ao usar o gerenciador de conexões Oracle no SSIS](http://go.microsoft.com/fwlink/?LinkId=233696), em support.microsoft.com.  
  
  
