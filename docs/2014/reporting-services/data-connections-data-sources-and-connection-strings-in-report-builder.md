---
title: Conexões de dados, fontes de dados e cadeias de caracteres de Conexão no construtor de relatórios | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10421"
ms.assetid: 7e103637-4371-43d7-821c-d269c2cc1b34
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5e5fe086d16728a95b9ee8f2a52878d5a2c4bad4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63164918"
---
# <a name="data-connections-data-sources-and-connection-strings-in-report-builder"></a>Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios
  Para incluir dados em um relatório, crie conexões de dados e conjuntos de dados. Uma conexão de dados inclui informações sobre como acessar uma fonte de dados externa. Um conjunto de dados inclui um comando de consulta que especifica os dados a serem incluídos usando a conexão de dados.  
  
1.  **Fontes de dados no painel de Dados do Relatório** Uma fonte de dados é exibida no painel de Dados do Relatório depois que você cria uma fonte de dados inserida ou adiciona uma fonte de dados compartilhada.  
  
2.  **Caixa de diálogo Conexão** Use a caixa de diálogo Conexão para criar ou colar uma cadeia de conexão.  
  
3.  **Informações de conexão de dados** A cadeia de conexão é transmitida à extensão de dados.  
  
4.  **Credenciais** As credenciais são gerenciadas separadamente da cadeia de conexão.  
  
5.  **Extensão de dados/Provedor de Dados** A conexão com os dados pode ser feita por meio de várias camadas de acesso a dados.  
  
6.  **Fontes de dados internas** Recupera dados de bancos de dados relacionais, bancos de dados multidimensionais, listas do SharePoint, serviços Web ou modelos de relatório.  
  
 Para obter mais informações, consulte [fontes de dados e conexões de dados compartilhado ou inserido &#40;construtor de relatórios e SSRS&#41; ](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md) e [conexões de dados, fontes de dados e cadeias de caracteres de Conexão no Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
 Também é possível incluir dados em um relatório usando fontes de dados compartilhadas, conjuntos de dados compartilhados e partes de relatório predefinidos. Esses itens já têm as informações de conexão de dados necessárias. Para obter mais informações, consulte [adicionar dados a um relatório &#40;construtor de relatórios e SSRS&#41;](report-data/report-datasets-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
 ![rs_DataSourcesStory](media/rs-datasourcesstory.gif "rs_DataSourcesStory")  
  
##  <a name="ConnectionString"></a> Exemplos de cadeias de Conexão  
 Uma conexão de dados inclui uma cadeia de conexão que geralmente é fornecida pelo proprietário da fonte de dados externa. A tabela a seguir lista exemplos de cadeias de conexão para tipos diferentes de fontes de dados externas.  
  
|**Fonte de dados**|**Exemplo**|**Descrição**|  
|---------------------|-----------------|---------------------|  
|Banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no servidor local|`data source="(local)";initial catalog=AdventureWorks2012`|Defina o tipo da fonte de dados como `SQL Server`.|  
|Banco de dados de instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|`Data Source=localhost\MSSQL12.InstanceName; Initial Catalog= AdventureWorks2012`|Defina o tipo da fonte de dados como `SQL Server`.|  
|Banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express|`Data Source=localhost\MSSQL12.SQLEXPRESS; Initial Catalog= AdventureWorks2012`|Defina o tipo da fonte de dados como `SQL Server`.|  
|Banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no servidor local|`data source=localhost;initial catalog=Adventure Works DW 2012`|Defina o tipo da fonte de dados como `SQL Server Analysis Services`.|  
|Lista do SharePoint|`data source=http://MySharePointWeb/MySharePointSite/`|Defina o tipo da fonte de dados como `SharePoint List`.|  
||||  
|Modelos de relatório|Não aplicável.|Você não precisa de uma cadeia de conexão para um modelo de relatório. No Construtor de Relatórios, vá para o servidor de relatório e selecione o arquivo .smdl que é o modelo de relatório.|  
|Servidor do Oracle|`data source=myserver`|Defina o tipo da fonte de dados como `Oracle`. As ferramentas do cliente Oracle devem estar instaladas no computador do Construtor de Relatórios e no servidor de relatório.|  
|Fonte de dados do SAP NetWeaver BI|`DataSource=http://mySAPNetWeaverBIServer:8000/sap/bw/xml/soap/xmla`|Defina o tipo da fonte de dados como `SAP NetWeaver BI`.|  
|Fonte de dados do Hyperion Essbase|`Data Source=http://localhost:13080/aps/XMLA; Initial Catalog=Sample`|Defina o tipo da fonte de dados como `Hyperion Essbase`.|  
|Fonte de dados do Teradata|`data source=` *\<NN>.\<NNN>.\<NNN>.\<N>* `;`|Defina o tipo da fonte de dados como `Teradata`. A cadeia de conexão é um endereço IP no formulário de quatro campos, em que cada campo pode ter de um a três dígitos.|  
|Fonte de dados do Teradata|`Database=` *\<database name>* `; data source=` *\<NN*N *>.\<NNN>.\<NNN>.\<N*NN*>*`;Use X Views=False;Restrict to Default Database=True`|Defina o tipo de fonte de dados como `Teradata`, semelhante ao exemplo anterior. Use apenas o banco de dados padrão especificado na marca Database e não descubra automaticamente relações de dados.|  
|Fonte de dados XML, serviço Web|`data source=http://adventure-works.com/results.aspx`|Defina o tipo da fonte de dados como `XML`. A cadeia de conexão é uma URL para um serviço Web com suporte para WSDL.|  
|Fonte de dados XML, documento XML|`http://localhost/XML/Customers.xml`|Defina o tipo da fonte de dados como `XML`. A cadeia de conexão é uma URL para o documento XML.|  
|Fonte de dados XML, documento XML inserido|*Empty (vazio)*|Defina o tipo da fonte de dados como `XML`. Os dados XML são inseridos na definição do relatório.|  
  
 Para obter mais informações sobre cada tipo de conexão, consulte [adicionar dados de fontes de dados externas &#40;SSRS&#41; ](report-data/add-data-from-external-data-sources-ssrs.md) e [dados de fontes com suporte no Reporting Services &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md).  
  

  
##  <a name="Creating"></a> Criando fontes de dados  
 Para criar uma fonte de dados inserida, você deve ter uma cadeia de conexão e as credenciais necessárias para acessar os dados. Em geral, essas informações derivam do proprietário da fonte de dados. A conexão de dados é salva na definição do relatório como parte da fonte de dados. As credenciais são gerenciadas independentemente da conexão. Para obter instruções passo a passo, consulte [adicionar e verificar uma Conexão de dados ou uma fonte de dados &#40;construtor de relatórios e SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  Alguns tipos de credenciais talvez não ofereçam suporte a todos os cenários usados pelo Construtor de Relatórios: para executar uma consulta no designer de consulta, visualize um relatório no computador quando você não estiver conectado a um servidor de relatório e execute o relatório a partir do servidor de relatório. É recomendável usar fontes de dados compartilhadas sempre que possível. Você pode armazenar credenciais para uma fonte de dados compartilhada no servidor de relatório. Para obter mais informações, consulte [Especificar as credenciais no Construtor de Relatórios](../../2014/reporting-services/specify-credentials-in-report-builder.md).  
  
 Para criar uma fonte de dados compartilhada, você deve usar o Gerenciador de relatórios para criar a fonte de dados diretamente no servidor de relatório ou usar um ambiente de criação como o Designer de relatórios no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Para obter mais informações, consulte [criar uma fonte de dados compartilhada ou um inserido &#40;SSRS&#41;](../../2014/reporting-services/create-an-embedded-or-shared-data-source-ssrs.md).  
  

  
## <a name="see-also"></a>Consulte também  
 [Adicionar dados a um relatório &#40;relatórios e SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [Partes de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-parts-report-builder-and-ssrs.md)  
  
  
