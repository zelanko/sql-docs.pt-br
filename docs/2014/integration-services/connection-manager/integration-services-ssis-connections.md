---
title: Conexões do SSIS (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 33757a58353f962bf82a57a16039f92d64a8686d
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53356192"
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
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa o gerenciador de conexões como uma representação lógica de uma conexão. Em tempo de design, você define as propriedades de um gerenciador de conexões para descrever a conexão física que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria quando o pacote é executado. Por exemplo, um gerenciador de conexões inclui a propriedade `ConnectionString` que você define em tempo de design; em tempo de execução, uma conexão física é criada usando o valor na propriedade da cadeia de conexão.  
  
 Um pacote pode usar várias instâncias de um tipo de gerenciador de conexões e você pode definir as propriedades em cada instância. Em tempo de execução, cada instância de um tipo de gerenciador de conexões cria uma conexão que tem atributos diferentes.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece diferentes tipos de gerenciadores de conexões que permitem a conexão de pacotes com várias fontes de dados e servidores.  
  
-   Há gerenciadores de conexões internos que a Instalação instala durante a instalação do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
-   Há gerenciadores de conexões disponíveis para download no site da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
-   Você poderá criar seu próprio gerenciador de conexões personalizado se os gerenciadores de conexões existentes não atenderem às suas necessidades.  
  
### <a name="built-in-connection-managers"></a>Gerenciadores de conexões internos  
 A tabela a seguir lista os tipos de gerenciadores de conexões fornecidos pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
|Tipo|Descrição|Tópico|  
|----------|-----------------|-----------|  
|ADO|Conecta-se a objetos ActiveX Data Objects (ADO).|[Gerenciador de conexões ADO](ado-connection-manager.md)|  
|ADO.NET|Conecta-se a uma fonte de dados usando um provedor .NET.|[Gerenciador de conexões ADO.NET](ado-net-connection-manager.md)|  
|CACHE|Lê dados do fluxo de dados ou de um arquivo de cache (.caw) e pode salvar esses dados em um arquivo de cache.|[Gerenciador de conexões de cache](cache-connection-manager.md)|  
|DQS|Conecta-se a um servidor a um banco de dados do Data Quality Services no servidor.|[Gerenciador de Conexões de Limpeza DQS](dqs-cleansing-connection-manager.md)|  
|EXCEL|Conecta-se a um arquivo da pasta de trabalho do Excel.|[Gerenciador de conexões do Excel](excel-connection-manager.md)|  
|FILE|Conecta-se a um arquivo ou uma pasta.|[Gerenciador de Conexões de Arquivos](file-connection-manager.md)|  
|FLATFILE|Conecta-se a dados em um único arquivo simples.|[Gerenciador de Conexões de Arquivos Simples](flat-file-connection-manager.md)|  
|FTP|Conecta-se a um servidor FTP.|[Gerenciador de Conexões de FTP](ftp-connection-manager.md)|  
|HTTP|Conecta-se a um servidor Web.|[Gerenciador de conexões HTTP](http-connection-manager.md)|  
|MSMQ|Conecta-se a uma fila de mensagens.|[Gerenciador de Conexões MSMQ](msmq-connection-manager.md)|  
|MSOLAP100|Conecta-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou a um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|[Gerenciador de Conexões do Analysis Services](analysis-services-connection-manager.md)|  
|MULTIFILE|Conecta-se a vários arquivos e pastas.|[Gerenciador de Conexões de Vários Arquivos](multiple-files-connection-manager.md)|  
|MULTIFLATFILE|Conecta-se a vários arquivos e pastas de dados.|[Gerenciador de Conexões de Vários Arquivos Simples](multiple-flat-files-connection-manager.md)|  
|OLEDB|Conecta-se a uma fonte de dados usando um provedor OLE DB.|[Gerenciador de Conexões OLE DB](ole-db-connection-manager.md)|  
|ODBC|Conecta-se a uma fonte de dados usando ODBC.|[Gerenciador de Conexões ODBC](odbc-connection-manager.md)|  
|SMOServer|Conecta-se a um servidor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects (SMO).|[Gerenciador de conexões SMO](smo-connection-manager.md)|  
|SMTP|Conecta-se a um servidor de email SMTP.|[Gerenciador de conexões SMTP](smtp-connection-manager.md)|  
|SQLMOBILE|Conecta-se a um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.|[Gerenciador de Conexões do SQL Server Compact Edition](sql-server-compact-edition-connection-manager.md)|  
|WMI|Conecta-se a um servidor e especifica o escopo de gerenciamento de Instrumentação de Gerenciamento do Windows (WMI) no servidor.|[Gerenciador de Conexões WMI](wmi-connection-manager.md)|  
  
### <a name="connection-managers-available-for-download"></a>Gerenciadores de conexão disponíveis para download  
 A tabela a seguir lista tipos adicionais de gerenciadores de conexões que podem ser baixados no site da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
> [!IMPORTANT]  
>  Os gerenciadores de conexões listados na tabela a seguir funcionam apenas com o [!INCLUDE[ssEnterpriseEd11](../../includes/ssenterpriseed11-md.md)] e o [!INCLUDE[ssDeveloperEd11](../../includes/ssdevelopered11-md.md)].  
  
|Tipo|Descrição|Tópico|  
|----------|-----------------|-----------|  
|ORACLE|Conecta-se a um Oracle \<informações de versão > servidor.|O gerenciador de conexões Oracle é o componente de gerenciador de conexões do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector para Oracle da Attunity. O [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector para Oracle da Attunity também inclui uma origem e um destino. Para obter mais informações, consulte a página de download de [Microsoft Connectors para Oracle e Teradata da Attunity](https://go.microsoft.com/fwlink/?LinkId=251526).|  
|SAPBI|Conecta a um sistema SAP NetWeaver BI versão 7.|O gerenciador de conexões SAP BI é o componente de gerenciador de conexões do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector para SAP BI. O [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector para SAP BI também inclui uma origem e um destino. Para obter mais informações, consulte a página de download [Microsoft SQL Server 2008 Feature Pack](https://go.microsoft.com/fwlink/?LinkId=262016).|  
|TERADATA|Conecta-se a um Teradata \<informações de versão > servidor.|O gerenciador de conexões Teradata é o componente de gerenciador de conexões do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector para Teradata da Attunity. O [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector para Teradata da Attunity também inclui uma origem e um destino. Para obter mais informações, consulte a página de download de [Microsoft Connectors para Oracle e Teradata da Attunity](https://go.microsoft.com/fwlink/?LinkId=251526).|  
  
### <a name="custom-connection-managers"></a>Gerenciadores de conexões personalizados  
 Também é possível escrever gerenciadores de conexões personalizados. Para obter mais informações, consulte [Developing a Custom Connection Manager](../extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md).  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter detalhes sobre como adicionar ou excluir um gerenciador de conexões em um pacote, consulte [Adicionar, excluir ou compartilhar um Gerenciador de Conexões em um pacote](../add-delete-or-share-a-connection-manager-in-a-package.md).  
  
 Para obter detalhes sobre como definir as propriedades de um gerenciador de conexões em um pacote, consulte [Definir as propriedades de um Gerenciador de Conexões](../set-the-properties-of-a-connection-manager.md).  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   Vídeo, [Aproveite o Microsoft Connector para Oracle da Attunity para melhorar o desempenho do pacote](https://technet.microsoft.com/sqlserver/gg598963.aspx), em technet.microsoft.com  
  
-   Artigos do Wiki, [Conectividade de SSIS](https://social.technet.microsoft.com/wiki/contents/articles/sql-server-integration-services-ssis.aspx#Connectivity), em social.technet.microsoft.com  
  
-   Entrada de blog, [Conectando ao MySQL a partir do SSIS](https://go.microsoft.com/fwlink/?LinkId=217669), em blogs.msdn.com.  
  
-   Artigo técnico, [Extraindo e carregando dados do SharePoint nos SQL Server Integration Services](https://go.microsoft.com/fwlink/?LinkId=247826), em msdn.microsoft.com.  
  
-   Artigo técnico, [Você obtém a mensagem de erro "DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER" ao usar o gerenciador de conexões Oracle no SSIS](https://go.microsoft.com/fwlink/?LinkId=233696), em support.microsoft.com.  
  
  
