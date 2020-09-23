---
title: Criar cadeias de conexão de dados – Construtor de Relatórios e SSRS | Microsoft Docs
description: Saiba como criar cadeias de conexão de dados e obtenha informações importantes sobre as credenciais de fonte de dados.
ms.date: 05/21/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4b544e7220d82d8368aec2a44c861e44b1e96398
ms.sourcegitcommit: 822d4b3cfa53269535500a3db5877a82b5076728
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87988444"
---
# <a name="create-data-connection-strings---report-builder--ssrs"></a>Criar cadeias de conexão de dados – Construtor de Relatórios e SSRS

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

  Para incluir dados em relatórios paginados [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], primeiro você deve criar uma *cadeia de conexão* para a *fonte de dados*. Este artigo explica como criar cadeias de conexão de dados e tem informações importantes sobre as credenciais de fonte de dados. Uma fonte de dados inclui o tipo da fonte de dados, informações da conexão e o tipo de credenciais a serem usadas. Para saber mais detalhes, confira [Introdução aos dados de relatório no SSRS (SQL Server Reporting Services)](report-data-ssrs.md).
  
##  <a name="built-in-data-extensions"></a><a name="bkmk_DataConnections"></a> Extensões de dados internas  
 As extensões de dados padrão no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] incluem Microsoft SQL Server, Banco de Dados SQL do Microsoft Azure e Microsoft SQL Server Analysis Services. Para obter uma lista completa de fontes de dados e versões aos quais o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] dá suporte, consulte [Fontes de dados com suporte no Reporting Services e &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).  
  
##  <a name="common-connection-string-examples"></a><a name="bkmk_connection_examples"></a> Exemplos comuns de cadeia de conexão  
 Cadeias de conexão são a representação de texto de propriedades de conexão para um provedor de dados. A tabela a seguir lista exemplos de cadeias de conexão para vários tipos de conexão de dados.  
 
 > [!NOTE]  
>  [Connectionstrings.com](https://www.connectionstrings.com/) é outro recurso para obter exemplos de cadeias de conexão. 
  
|**Fonte de dados**|**Exemplo**|**Descrição**|  
|---------------------|-----------------|---------------------|  
|Banco de dados do SQL Server no servidor local|`data source="(local)";initial catalog=AdventureWorks`|Defina o tipo de fonte de dados como **Microsoft SQL Server**. Para obter mais informações, consulte [Tipo de conexão do SQL Server &#40;SSRS&#41;](../../reporting-services/report-data/sql-server-connection-type-ssrs.md).|  
|Instância do SQL Server<br /><br /> Banco de Dados|`Data Source=localhost\MSSQL13.<InstanceName>; Initial Catalog=AdventureWorks`|Defina o tipo de fonte de dados como **Microsoft SQL Server**.|  
|Banco de Dados SQL do Azure|`Data Source=<host>;Initial Catalog=AdventureWorks; Encrypt=True`|Defina o tipo de fonte de dados como **Banco de Dados SQL do Microsoft Azure**. Confira mais informações em [Tipo de conexão &#40;SSRS&#41; do SQL Azure](../../reporting-services/report-data/sql-azure-connection-type-ssrs.md).|  
|SQL Server Parallel Data Warehouse|`HOST=<IP address>;database= AdventureWorks; port=<port>`|Defina o tipo de fonte de dados como **Microsoft SQL Server Parallel Data Warehouse**. Para obter mais informações, consulte [Tipo de conexão do SQL Server Parallel Data Warehouse &#40;SSRS&#41;](../../reporting-services/report-data/sql-server-parallel-data-warehouse-connection-type-ssrs.md).|  
|Banco de dados do Analysis Services no servidor local|`data source=localhost;initial catalog=Adventure Works DW`|Defina o tipo de fonte de dados como **Microsoft SQL Server Analysis Services**. Para obter mais informações, consulte [Tipo de conexão do Analysis Services para MDX &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md) ou [Tipo de conexão do Analysis Services para DMX &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-dmx-ssrs.md).|  
|Banco de dados modelo de tabela do Analysis Services com perspectiva de vendas|`Data source=<servername>;initial catalog= Adventure Works DW;cube='Sales'`|Defina o tipo de fonte de dados como **Microsoft SQL Server Analysis Services**. Especifique o nome da perspectiva na configuração de cube=. Para obter mais informações, consulte [Perspectivas &#40;SSAS de Tabela&#41;](https://docs.microsoft.com/analysis-services/tabular-models/perspectives-ssas-tabular).|  
|Servidor do Oracle|`data source=myserver`|Defina o tipo de fonte de dados como **Oracle**. As ferramentas do cliente Oracle devem estar instaladas no computador de Designer de Relatórios e no servidor de relatório. Para obter mais informações, consulte [Tipo de conexão Oracle &#40;SSRS&#41;](../../reporting-services/report-data/oracle-connection-type-ssrs.md).|  
|Fonte de dados do SAP NetWeaver BI|`DataSource=https://mySAPNetWeaverBIServer:8000/sap/bw/xml/soap/xmla`|Defina o tipo de fonte de dados como **SAP NetWeaver Bl**. Para obter mais informações, consulte [Tipo de conexão SAP NetWeaver BI &#40;SSRS&#41;](../../reporting-services/report-data/sap-netweaver-bi-connection-type-ssrs.md).|  
|Fonte de dados do Hyperion Essbase|`Data Source=https://localhost:13080/aps/XMLA; Initial Catalog=Sample`|Defina o tipo de fonte de dados como **Hyperion Essbase**. Para obter mais informações, consulte [Tipo de conexão Hyperion Essbase &#40;SSRS&#41;](../../reporting-services/report-data/hyperion-essbase-connection-type-ssrs.md).|  
|Fonte de dados do Teradata|`data source=`\<NNN>.\<NNN>.\<NNN>.\<NNN>`;`|Defina o tipo de fonte de dados como **Teradata**. A cadeia de conexão é um endereço IP no formulário de quatro campos, em que cada campo pode ter de um a três dígitos. Para obter mais informações, consulte [Tipo de conexão Teradata &#40;SSRS&#41;](../../reporting-services/report-data/teradata-connection-type-ssrs.md).|  
|Fonte de dados do Teradata|`Database=` *\<database name>* `; data source=` *\<NN*N*>.\<NNN>.\<NNN>.\<N*NN*>*`;Use X Views=False;Restrict to Default Database=True`|Defina o tipo de fonte de dados como **Teradata**, semelhante ao exemplo anterior. Use apenas o banco de dados padrão especificado na marca Database e não descubra automaticamente relações de dados.|  
|Fonte de dados XML, serviço Web|`data source=https://adventure-works.com/results.aspx`|Defina o tipo de fonte de dados como **XML**. A cadeia de conexão é uma URL para um serviço Web com suporte para WSDL. Para obter mais informações, consulte [Tipo de conexão XML &#40;SSRS&#41;](../../reporting-services/report-data/xml-connection-type-ssrs.md).|  
|Fonte de dados XML, documento XML|`https://localhost/XML/Customers.xml`|Defina o tipo de fonte de dados como **XML**. A cadeia de conexão é uma URL para o documento XML. 
|Fonte de dados XML, documento XML inserido|*Empty (vazio)*|Defina o tipo de fonte de dados como **XML**. Os dados XML são inseridos na definição do relatório.|  
|Lista do SharePoint|`data source=https://MySharePointWeb/MySharePointSite/`|Definir o tipo de fonte de dados como **lista do SharePoint**.|  
| Conjunto de dados do Power BI Premium (começando com o Reporting Services 2019 e o Servidor de Relatórios do Power BI de janeiro de 2020) | `Data Source=powerbi://api.powerbi.com/v1.0/myorg/<workspacename>;Initial Catalog=<datasetname>` | Defina o tipo de fonte de dados como **Microsoft SQL Server Analysis Services**. |

  
 Se não for possível conectar a um servidor de relatório que use **localhost**, verifique se o protocolo de rede TCP/IP está habilitado. Para obter mais informações, consulte [Configure Client Protocols](../../database-engine/configure-windows/configure-client-protocols.md).  
  
 Para saber mais sobre as configurações necessárias para se conectar a esses tipos de fonte de dados, confira o artigo de conexão de dados específicos em [Adicionar dados de fontes de dados externas &#40;SSRS&#41;](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md) ou [Fontes de dados compatíveis com o Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).  
  
##  <a name="special-characters-in-a-password"></a><a name="bkmk_special_password_characters"></a> Caracteres especiais em uma senha  
 Se você configurar a fonte de dados ODBC ou SQL para solicitar uma senha ou para incluir uma senha na cadeia de conexão e o usuário inserir a senha com caracteres especiais, como sinais de pontuação, alguns drivers de fonte de dados subjacentes não conseguirão validar os caracteres especiais. Quando você processar o relatório, a mensagem "Senha inválida" poderá indicar esse problema. Se não for possível alterar a senha, você poderá trabalhar com o administrador do banco de dados para armazenar as credenciais apropriadas no servidor como parte de um DSN (nome da fonte de dados) do sistema ODBC. Para saber mais, confira [OdbcConnection.ConnectionString](https://docs.microsoft.com/dotnet/api/system.data.odbc.odbcconnection.connectionstring) na documentação do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
##  <a name="expression-based-connection-strings"></a><a name="bkmk_Expressions_in_connection_strings"></a> Cadeias de conexão baseadas em expressão  
 Cadeias de conexão baseadas em expressão são avaliadas em tempo de execução. Por exemplo, você pode especificar a fonte de dados como um parâmetro, incluir a referência ao parâmetro na cadeia de conexão e permitir que o usuário escolha a fonte de dados para o relatório. Por exemplo, suponha que uma empresa multinacional tem servidores de dados em vários países. Com uma cadeia de conexão baseada em expressão, um usuário que está executando um relatório de vendas pode selecionar uma fonte de dados para um país específico antes de executar o relatório.  
  
 O exemplo a seguir ilustra o uso de uma expressão de fonte de dados em uma cadeia de conexão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O exemplo assume que você criou um parâmetro de relatório denominado `ServerName`:  
  
```  
="data source=" & Parameters!ServerName.Value & ";initial catalog=AdventureWorks"  
```  
  
 Expressões de fonte de dados são processadas em tempo de execução ou quando um relatório é visualizado. A expressão deve ser escrita no [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]. Use as seguintes diretrizes ao definir uma expressão de fonte de dados:  
  
-   Crie o relatório usando uma cadeia de conexão estática. Uma cadeia de conexão estática faz referência a uma cadeia de conexão que não é definida através de uma expressão (por exemplo, quando você segue as etapas para criar uma fonte de dados específica ao relatório ou compartilhada, você está definindo um cadeia de conexão estática. O uso de uma cadeia de conexão estática permite conectar à fonte de dados no Designer de Relatórios de forma que você possa obter os resultados da consulta necessários para criar o relatório.  
  
-   Ao definir a conexão da fonte de dados, não use uma fonte de dados compartilhada. Não é possível usar uma expressão de fonte de dados em uma fonte de dados compartilhada. Você deve definir uma fonte de dados inserida para o relatório.  
  
-   Especifique credenciais separadamente da cadeia de conexão. É possível usar credenciais armazenadas, credenciais solicitadas ou segurança integrada.  
  
-   Adicione um parâmetro de relatório para especificar uma fonte de dados. Para os valores dos parâmetros, você pode fornecer uma lista estática de valores disponíveis (neste caso, os valores disponíveis devem ser fontes de dados usadas com o relatório) ou definir uma consulta que recupere uma lista de fontes de dados em tempo de execução.  
  
-   Verifique se a lista de fontes de dados compartilha o mesmo esquema de banco de dados. Todo design de relatório começa com informações de esquema. Se houver uma incompatibilidade entre o esquema usado para definir o relatório e o esquema real usado pelo relatório em tempo de execução, o relatório poderá não ser executado.  
  
-   Antes de publicar o relatório, substitua a cadeia de conexão estática por uma expressão. Espere até a conclusão do design do relatório para substituir a cadeia de conexão estática por uma expressão. Ao usar uma expressão, você não pode executar a consulta no Designer de Relatórios. Além disso, a lista de campos no painel de dados do relatório e a lista de Parâmetros não serão atualizadas automaticamente.  

## <a name="next-steps"></a>Próximas etapas

[Introdução aos dados de relatório no SSRS (SQL Server Reporting Services)](report-data-ssrs.md)
[Criar e modificar fontes de dados compartilhadas](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)   
[Criar e modificar fontes de dados inseridas](../../reporting-services/report-data/create-and-modify-embedded-data-sources.md)   
[Definir propriedades de implantação](../../reporting-services/tools/set-deployment-properties-reporting-services.md)   
[Especificar informações de credenciais e de conexão para fontes de dados de relatório](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)  

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
