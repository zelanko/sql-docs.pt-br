---
title: Conexões de dados, fontes de dados e cadeias de caracteres de Conexão no Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- connections [Reporting Services], data sources
- reports [Reporting Services], data
- expressions [Reporting Services], data sources
- data sources [Reporting Services], connections
- connection strings [Reporting Services]
- shared data sources [Reporting Services]
- Reporting Services, data sources
- logins [Reporting Services]
ms.assetid: 4d8f0ae1-102b-4b3d-9155-fa584c962c9e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a89cb1d06b60d086c139b4d618b7bd716c04616e
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63462039"
---
# <a name="data-connections-data-sources-and-connection-strings-in-reporting-services"></a>Data Connections, Data Sources, and Connection Strings in Reporting Services
  Para incluir dados em um relatório do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , primeiro você deve criar *fontes de dados* e *conjuntos de dados*. Este tópico explica o tipo de fontes de dados, como criar fontes de dados e informações importantes relacionadas às credenciais de fontes de dados. Uma fonte de dados inclui o tipo da fonte de dados, informações da conexão e o tipo de credenciais a serem usadas. Há dois tipos de fontes de dados: inserida ou compartilhada. Um fonte de dados inserida é definida no relatório e usada apenas por esse relatório. Uma fonte de dados compartilhada é definida independentemente de um relatório e pode ser usada por vários relatórios. Para obter mais informações, consulte [Conexões de dados ou fontes de dados inseridas e compartilhadas &#40;Construtor de Relatórios e SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md) e [Conjuntos de dados inseridos e compartilhados &#40;Construtor de Relatórios e SSRS&#41;](report-data/embedded-and-shared-datasets-report-builder-and-ssrs.md).  
  
||  
|-|  
|**[!INCLUDE[applies](../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Modo nativo &#124; [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Modo do SharePoint|  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  

  
##  <a name="bkmk_data_sources"></a> Fontes de dados inseridas e compartilhadas  
 A diferença entre as fontes de dados inseridas e compartilhadas está em como elas são criadas, armazenadas e gerenciadas.  
  
-   No Designer de Relatórios, crie fontes de dados inseridas e compartilhadas como parte de um projeto do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] . Você pode controlar se elas devem ser usadas localmente para visualização ou implantadas como parte do projeto para um servidor de relatório ou site do SharePoint. Você pode usar extensões de dados personalizadas que foram instaladas em seu computador e no servidor de relatório ou site do SharePoint onde você implanta seus relatórios.  
  
     Os administradores do sistema podem instalar e configurar extensões de processamento de dados adicionais e provedores de dados do .NET Framework. Para obter mais informações, consulte [Extensões de processamento de dados e provedores de dados do .NET Framework &#40;SSRS&#41;](report-data/data-processing-extensions-and-net-framework-data-providers-ssrs.md).  
  
     Os desenvolvedores podem usar a API <xref:Microsoft.ReportingServices.DataProcessing> para criar extensões de processamento de dados para dar suporte a tipos de fonte de dados adicionais.  
  
-   No Construtor de Relatórios, navegue para um servidor de relatório ou site do SharePoint e selecione fontes de dados compartilhadas ou crie fontes de dados inseridas no relatório. Não é possível criar uma fonte de dados compartilhada no Construtor de Relatórios. Você não pode usar extensões de dados personalizadas no Construtor de Relatórios  
  
##  <a name="bkmk_DataConnections"></a> Extensões de dados internas  
 As extensões de dados padrão no [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] incluem os tipos de conexão de dados a seguir:  
  
-   Microsoft SQL Server  
  
-   Microsoft SQL Server Analysis Services  
  
-   Lista do Microsoft SharePoint  
  
-   [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)]  
  
-   Microsoft SQL Server Parallel Data Warehouse  
  
-   OLE DB  
  
-   Oracle  
  
-   SAP NetWeaver BI  
  
-   Hyperion Essbase  
  
-   Teradata  
  
-   XML  
  
-   ODBC  
  
-   Modelo semântico de BI da Microsoft para Power View: Em um site do SharePoint que tenha sido configurado para uma Galeria PowerPivot e [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)], esse tipo de fonte de dados está disponível. Esse tipo de fonte de dados é usado somente para apresentações do [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] . Para mais informações, consulte [Criando modelos semânticos de tabelas perfeitos de BI para Power View](https://technet.microsoft.com/video/building-the-perfect-bi-semantic-tabular-models-for-power-view.aspx).  
  
 Para obter uma lista completa de fontes de dados e versões aos quais o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] dá suporte, consulte [Fontes de dados com suporte no Reporting Services e &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md).  
  
##  <a name="bkmk_create_data_source"></a> Criar uma fonte de dados  
 Para criar uma fonte de dados, você deve ter as seguintes informações:  
  
-   **Tipo da fonte de dados** O tipo de conexão, por exemplo, [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Escolha esse valor na lista suspensa de tipos de conexão.  
  
-   **Informações de conexão** As informações de conexão incluem o nome e o local da fonte de dados e as propriedades de conexão específicas para cada provedor de dados. A *cadeia de conexão* é a representação de texto das informações de conexão. Por exemplo, se a fonte de dados for um banco de dados do SQL Server, você poderá especificar o nome do banco de dados. Para fontes de dados inseridas, também é possível gravar cadeias de conexão baseadas em expressão que são avaliadas em tempo de execução. Para obter mais informações, consulte [Cadeias de conexão baseadas em expressão](#bkmk_Expressions_in_connection_strings) mais adiante neste tópico.  
  
-   **Credenciais** Você fornece as credenciais necessárias para acessar os dados. O proprietário da fonte de dados deve ter concedido a você as permissões adequadas para acessar a fonte de dados e os dados específicos na fonte de dados. Por exemplo, para conectar-se ao banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] instalado em um servidor de rede, você deve ter permissão para conectar-se ao servidor e também permissão de leitura e gravação para acessar o banco de dados.  
  
    > [!NOTE]  
    >  Por design, as credenciais são gerenciadas de maneira independente das fontes de dados. As credenciais usadas para visualizar seu relatório em um sistema local podem ser diferentes das credenciais necessárias para exibir o relatório publicado. Depois de salvar uma fonte de dados no servidor de relatório ou site do SharePoint, pode ser necessário alterar as credenciais para trabalhar daquele local. Para obter mais informações, consulte [Credenciais para fontes de dados](#bkmk_credentials).  
  
> [!NOTE]  
>  Ao criar uma fonte de dados inserida para um relatório no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], você deve criar a fonte de dados no Designer de Relatórios no Gerenciador de Soluções ou no painel de dados do relatório, mas não no Gerenciador de Servidores. O Designer de Relatórios do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não dá suporte a fontes de dados do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] criadas no Gerenciador de Servidores.  
  
 O painel de dados do relatório exibe fontes de dados inseridas e referências a fontes de dados compartilhadas que foram adicionadas ao relatório. No Construtor de Relatórios, uma referência a uma fonte de dados compartilhada aponta para uma fonte de dados compartilhada em um servidor de relatório ou no site do SharePoint. No Designer de Relatórios, uma referência a uma fonte de dados compartilhada aponta para uma fonte de dados compartilhada no Gerenciador de Soluções na pasta Fonte de Dados Compartilhada.  
  
##  <a name="bkmk_credentials"></a> Credenciais para fontes de dados  
 Por design, as credenciais podem ser salvas e gerenciadas independentemente das informações de conexão. As credenciais são usadas para criar uma fonte de dados, para executar uma consulta de conjunto de dados e para visualizar um relatório.  
  
> [!NOTE]  
>  É recomendável não incluir informações de logon, como nomes de logon e senhas, às propriedades de conexão da fonte de dados. Use fontes de dados compartilhadas com credenciais armazenadas sempre que possível. Em um ambiente de criação, use a página Credenciais da caixa de diálogo **Fonte de Dados** para inserir credenciais ao criar uma conexão de dados ou ao executar uma consulta de conjunto de dados.  
  
 As credenciais inseridas para acesso a dados em seu computador são armazenados com segurança no arquivo de configuração do projeto local e são específicas a seu computador. Se você copiar os arquivos do projeto em outro computador, deverá redefinir as credenciais da fonte de dados.  
  
 Ao implantar um relatório no servidor de relatório ou site do SharePoint, suas fontes de dados inseridas e compartilhadas são gerenciadas de maneira independente. As credenciais da fonte de dados necessárias para acessar os dados de seu computador podem ser diferentes das credenciais necessárias para o servidor de relatório para acessar os dados.  
  
 ![Observação](media/rs-fyinote.png "Observação")uma prática recomendada é verificar se as conexões de fonte de dados continuam a se conectar com êxito depois de publicar um relatório. Se for necessário alterar as credenciais, você poderá modificá-las diretamente no servidor de relatório.  
  
 Para alterar as fontes de dados que usa um relatório, você pode modificar as propriedades do relatório no modo nativo do Gerenciador de relatórios ou de bibliotecas de documentos no modo do SharePoint. Para obter mais informações, consulte o seguinte:  
  
-   [Store credenciais em uma fonte de dados do Reporting Services](report-data/store-credentials-in-a-reporting-services-data-source.md) [Store credenciais em uma fonte de dados do Reporting Services](report-data/store-credentials-in-a-reporting-services-data-source.md)  
  
-   [Especificar informações de credenciais e de conexão para fontes de dados de relatório](report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
-   [Especificar conexões para extensões de processamento de dados personalizadas](report-data/specify-connections-for-custom-data-processing-extensions.md)  
  
-   [Especificar as credenciais no Construtor de Relatórios](../../2014/reporting-services/specify-credentials-in-report-builder.md)  
  
-   [Adicionar e verificar uma Conexão de dados ou uma fonte de dados &#40;relatórios e SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
##  <a name="bkmk_connection_examples"></a> Exemplos comuns de cadeia de conexão  
 Cadeias de conexão são a representação de texto de propriedades de conexão para um provedor de dados. A tabela a seguir lista exemplos de cadeias de conexão para vários tipos de conexão de dados.  
  
|**Fonte de dados**|**Exemplo**|**Descrição**|  
|---------------------|-----------------|---------------------|  
|Banco de dados do SQL Server no servidor local|`data source="(local)";initial catalog=AdventureWorks`|Defina o tipo da fonte de dados como `Microsoft SQL Server`. Para obter mais informações, consulte [Tipo de conexão do SQL Server &#40;SSRS&#41;](report-data/sql-server-connection-type-ssrs.md).|  
|Banco de dados do SQL Server no servidor local|`data source="(local)";initial catalog=AdventureWorks`|Defina o tipo da fonte de dados como `Microsoft SQL Server`.|  
|Instância do SQL Server<br /><br /> Banco de Dados|`Data Source=localhost\MSSQL10_50.InstanceName; Initial Catalog=AdventureWorks`|Defina o tipo da fonte de dados como `Microsoft SQL Server`.|  
|Banco de dados do SQL Server Express|`Data Source=localhost\MSSQL10_50.SQLEXPRESS; Initial Catalog=AdventureWorks`|Defina o tipo da fonte de dados como `Microsoft SQL Server`.|  
|[!INCLUDE[ssSDS](../includes/sssds-md.md)] na nuvem|`Data Source=<host>;Initial Catalog=AdventureWorks; Encrypt=True`|Defina o tipo da fonte de dados como `Windows Azure SQL Database`. Para obter mais informações, consulte [Tipo de conexão do SQL Azure &#40;SSRS&#41;](report-data/sql-azure-connection-type-ssrs.md).|  
|SQL Server Parallel Data Warehouse|`HOST=<IP address>;database= AdventureWorks; port=<port>`|Defina o tipo da fonte de dados como `Microsoft SQL Server Parallel Data Warehouse`. Para obter mais informações, consulte [Tipo de conexão do SQL Server Parallel Data Warehouse &#40;SSRS&#41;](report-data/sql-server-parallel-data-warehouse-connection-type-ssrs.md).|  
|Banco de dados do Analysis Services no servidor local|`data source=localhost;initial catalog=Adventure Works DW`|Defina o tipo da fonte de dados como `Microsoft SQL Server Analysis Services`. Para obter mais informações, consulte [Tipo de conexão do Analysis Services para MDX &#40;SSRS&#41;](report-data/analysis-services-connection-type-for-mdx-ssrs.md) ou [Tipo de conexão do Analysis Services para DMX &#40;SSRS&#41;](report-data/analysis-services-connection-type-for-dmx-ssrs.md).|  
|Banco de dados modelo de tabela do Analysis Services com perspectiva de vendas|`Data source=<servername>;initial catalog= Adventure Works DW;cube='Sales'`|Defina o tipo da fonte de dados como `Microsoft SQL Server Analysis Services`. Especifique o nome da perspectiva na configuração de cube=. Para obter mais informações, consulte [Perspectivas &#40;SSAS de Tabela&#41;](../analysis-services/tabular-models/perspectives-ssas-tabular.md).|  
|Fonte de dados de modelo de relatório em um servidor de relatório configurado em modo nativo|`Server=http://myreportservername/reportserver; datasource=/models/Adventure Works`|Especifique o servidor de relatório ou a URL da biblioteca de documentos e o caminho para o modelo publicado na pasta do servidor de relatório ou no namespace da pasta da biblioteca de documentos.
|Fonte de dados de modelo de relatório em um servidor de relatório configurado em modo integrado do SharePoint|`Server=http://server; datasource=http://server/site/documents/models/Adventure Works.smdl`|Especifique o servidor de relatório ou a URL da biblioteca de documentos e o caminho para o modelo publicado na pasta do servidor de relatório ou no namespace da pasta da biblioteca de documentos.|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 2000|`provider=MSOLAP.2;data source=<remote server name>;initial catalog=FoodMart 2000`|Defina o tipo da fonte de dados como `OLE DB Provider for OLAP Services 8.0`.<br /><br /> É possível obter uma conexão mais rápida a fontes de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 2000 se você definir a propriedade `ConnectTo` como `8.0`. Para definir essa propriedade, use a caixa de diálogo **Propriedades da Conexão** , guia **Propriedades Avançadas** .|  
|Servidor do Oracle|`data source=myserver`|Defina o tipo da fonte de dados como `Oracle`. As ferramentas do cliente Oracle devem estar instaladas no computador de Designer de Relatórios e no servidor de relatório. Para obter mais informações, consulte [Tipo de conexão Oracle &#40;SSRS&#41;](report-data/oracle-connection-type-ssrs.md).|  
|Fonte de dados do SAP NetWeaver BI|`DataSource=http://mySAPNetWeaverBIServer:8000/sap/bw/xml/soap/xmla`|Defina o tipo da fonte de dados como `SAP NetWeaver BI`. Para obter mais informações, consulte [Tipo de conexão SAP NetWeaver BI &#40;SSRS&#41;](report-data/sap-netweaver-bi-connection-type-ssrs.md).|  
|Fonte de dados do Hyperion Essbase|`Data Source=http://localhost:13080/aps/XMLA; Initial Catalog=Sample`|Defina o tipo da fonte de dados como `Hyperion Essbase`. Para obter mais informações, consulte [Tipo de conexão Hyperion Essbase &#40;SSRS&#41;](report-data/hyperion-essbase-connection-type-ssrs.md).|  
|Fonte de dados do Teradata|`data source=`\<NNN>.\<NNN>.\<NNN>.\<NNN>`;`|Defina o tipo da fonte de dados como `Teradata`. A cadeia de conexão é um endereço IP no formulário de quatro campos, em que cada campo pode ter de um a três dígitos. Para obter mais informações, consulte [Tipo de conexão Teradata &#40;SSRS&#41;](report-data/teradata-connection-type-ssrs.md).|  
|Fonte de dados XML, serviço Web|`data source=http://adventure-works.com/results.aspx`|Defina o tipo da fonte de dados como `XML`. A cadeia de conexão é uma URL para um serviço Web com suporte para WSDL. Para obter mais informações, consulte [Tipo de conexão XML &#40;SSRS&#41;](report-data/xml-connection-type-ssrs.md).|  
|Fonte de dados XML, documento XML|`http://localhost/XML/Customers.xml`|Defina o tipo da fonte de dados como `XML`. A cadeia de conexão é uma URL para o documento XML.|  
|Fonte de dados XML, documento XML inserido|*Empty (vazio)*|Defina o tipo da fonte de dados como `XML`. Os dados XML são inseridos na definição do relatório.|  
  
Se não for possível conectar a um servidor de relatório que use `localhost`, verifique se o protocolo de rede TCP/IP está habilitado. Para obter mais informações, consulte [Configure Client Protocols](../database-engine/configure-windows/configure-client-protocols.md).  
  
##  <a name="bkmk_special_password_characters"></a> Caracteres especiais em uma senha  
 Se você configurar a fonte de dados ODBC ou SQL para solicitar uma senha ou para incluir uma senha na cadeia de conexão e o usuário inserir a senha com caracteres especiais, como sinais de pontuação, alguns drivers de fonte de dados subjacentes não conseguirão validar os caracteres especiais. Quando você processar o relatório, a mensagem "Senha inválida" poderá indicar esse problema. Se não for possível alterar a senha, você poderá trabalhar com o administrador do banco de dados para armazenar as credenciais apropriadas no servidor como parte de um DSN (nome da fonte de dados) do sistema ODBC. Para obter mais informações, consulte "OdbcConnection.ConnectionString" na documentação do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] SDK.  
  
##  <a name="bkmk_Expressions_in_connection_strings"></a> Cadeias de conexão baseadas em expressão  
 Cadeias de conexão baseadas em expressão são avaliadas em tempo de execução. Por exemplo, você pode especificar a fonte de dados como um parâmetro, incluir a referência ao parâmetro na cadeia de conexão e permitir que o usuário escolha a fonte de dados para o relatório. Por exemplo, suponha que uma empresa multinacional tem servidores de dados em vários países. Com uma cadeia de conexão baseada em expressão, um usuário que está executando um relatório de vendas pode selecionar uma fonte de dados para um país específico antes de executar o relatório.  
  
 O exemplo a seguir ilustra o uso de uma expressão de fonte de dados em uma cadeia de conexão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . O exemplo assume que você criou um parâmetro de relatório denominado `ServerName`:  
  
```  
="data source=" & Parameters!ServerName.Value & ";initial catalog=AdventureWorks"  
```  
  
 Expressões de fonte de dados são processadas em tempo de execução ou quando um relatório é visualizado. A expressão deve ser escrita no [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]. Use as seguintes diretrizes ao definir uma expressão de fonte de dados:  
  
-   Crie o relatório usando uma cadeia de conexão estática. Uma cadeia de conexão estática faz referência a uma cadeia de conexão que não é definida através de uma expressão (por exemplo, quando você segue as etapas para criar uma fonte de dados específica ao relatório ou compartilhada, você está definindo um cadeia de conexão estática. O uso de uma cadeia de conexão estática permite conectar à fonte de dados no Designer de Relatórios de forma que você possa obter os resultados da consulta necessários para criar o relatório.  
  
-   Ao definir a conexão da fonte de dados, não use uma fonte de dados compartilhada. Não é possível usar uma expressão de fonte de dados em uma fonte de dados compartilhada. Você deve definir uma fonte de dados inserida para o relatório.  
  
-   Especifique credenciais separadamente da cadeia de conexão. É possível usar credenciais armazenadas, credenciais solicitadas ou segurança integrada.  
  
-   Adicione um parâmetro de relatório para especificar uma fonte de dados. Para os valores dos parâmetros, você pode fornecer uma lista estática de valores disponíveis (neste caso, os valores disponíveis devem ser fontes de dados usadas com o relatório) ou definir uma consulta que recupere uma lista de fontes de dados em tempo de execução.  
  
-   Verifique se a lista de fontes de dados compartilha o mesmo esquema de banco de dados. Todo design de relatório começa com informações de esquema. Se houver uma incompatibilidade entre o esquema usado para definir o relatório e o esquema real usado pelo relatório em tempo de execução, o relatório poderá não ser executado.  
  
-   Antes de publicar o relatório, substitua a cadeia de conexão estática por uma expressão. Espere até a conclusão do design do relatório para substituir a cadeia de conexão estática por uma expressão. Ao usar uma expressão, você não pode executar a consulta no Designer de Relatórios. Além disso, a lista de campos no painel de dados do relatório e a lista de Parâmetros não serão atualizadas automaticamente.  
  
## <a name="see-also"></a>Consulte também  
 [Conexões de dados ou fontes de dados inseridas e compartilhadas &#40;Construtor de Relatórios e SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)   
 [Gerenciar fontes de dados de relatório](report-data/manage-report-data-sources.md)   
 [Caixa de diálogo de propriedades de fonte de dados, credenciais](../../2014/reporting-services/data-source-properties-dialog-box-credentials.md)   
 [Caixa de diálogo de propriedades de fonte de dados compartilhada, credenciais](../../2014/reporting-services/shared-data-source-properties-dialog-box-credentials.md)   
 [Criar, modificar e excluir fontes de dados compartilhadas &#40;SSRS&#41;](report-data/create-modify-and-delete-shared-data-sources-ssrs.md)   
 [Definir propriedades de implantação &#40;Reporting Services&#41;](tools/set-deployment-properties-reporting-services.md)   
 [Especificar informações de credenciais e de conexão para fontes de dados de relatório](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Adicionar e verificar uma Conexão de dados ou uma fonte de dados &#40;relatórios e SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
