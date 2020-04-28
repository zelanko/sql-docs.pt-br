---
title: Fontes de dados com suporte no Reporting Services (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SQL Server data processing extension [Reporting Services]
- XML data processing extension [Reporting Services]
- reports [Reporting Services], data
- data processing extensions [Reporting Services], data sources
- Oracle [Reporting Services]
- OLE DB data processing extension
- data sources [Reporting Services], about data sources
- ODBC data processing extension
- Reporting Services, data sources
ms.assetid: 9d11d055-a3be-45aa-99a7-46447a94ed42
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6e569240f708d209fc965fa3c6e393859044f528
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "70155117"
---
# <a name="data-sources-supported-by-reporting-services-ssrs"></a>Fontes de dados com suporte no Reporting Services (SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] recupera dados de relatório de fontes de dados por meio de uma camada de dados modular e extensível que usa extensões de processamento de dados. Para recuperar dados de relatório de uma fonte de dados, você deve selecionar uma extensão de processamento de dados que dá suporte ao tipo de fonte de dados, à versão do software em execução na fonte de dados e à plataforma da fonte de dados ( [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]de 32 bits ou 64 bits).  
  
 Ao implantar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], um conjunto de extensões de processamento de dados é instalado e registrado automaticamente no cliente de criação de relatório e no servidor de relatório para fornecer acesso a uma variedade de tipos de fonte de dados. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instala os seguintes tipos de fonte de dados:  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)]para modelos MDX, DMX [!INCLUDE[msCoName](../../includes/msconame-md.md)] , PowerPivot e tabular [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]data warehouse paralelos  
  
-   Oracle  
  
-   SAP NetWeaver BI  
  
-   [!INCLUDE[extEssbase](../../includes/extessbase-md.md)]  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Lista do SharePoint  
  
-   Teradata  
  
-   OLE DB  
  
-   ODBCODBC  
  
-   XML  
  
 Além disso, as extensões de processamento de dados personalizadas e os provedores de dados [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] padrão podem ser instalados e registrados por administradores do sistema. Para processar e exibir um relatório, as extensões de processamento de dados e os provedores de dados devem ser instalados e registrados no servidor de relatório; para visualizar um relatório, eles devem ser instalados e registrados no cliente de autoria de relatório. As extensões de processamento de dados e os provedores de dados devem ser compilados de forma nativa para a plataforma em que são instalados. Se você implantar uma fonte de dados programaticamente com o serviço Web SOAP, deverá definir a extensão de fonte de dados. Use valores de extensão de dados do arquivo **RSReportDesigner.config** . Por padrão, o arquivo está localizado na seguinte pasta:  
  
```  
<drive letter>\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssemblies  
```  
  
 Por exemplo, a extensão de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é OLEDB-MD.  
  
 Muitos provedores de dados [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] padrão de terceiros estão disponíveis como downloads no [Centro de Download da Microsoft](https://go.microsoft.com/fwlink/?linkid=51456) e em sites de terceiros. Também é possível pesquisar o fórum público do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para saber mais sobre provedores de dados de terceiros.  
  
> [!NOTE]  
>  Os provedores de dados do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] padrão não necessariamente oferecem suporte a toda a funcionalidade fornecida pelas extensões de processamento de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Além disso, alguns provedores de dados OLE DB e drivers ODBC podem ser usados para criar e visualizar relatórios, embora não sejam projetados para oferecer suporte a relatórios publicados em um servidor de relatório. Por exemplo, não há suporte para o Provedor [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB para Jet no servidor de relatório. Para obter mais informações, consulte [Extensões de processamento de dados e provedores de dados do .NET Framework &#40;SSRS&#41;](data-processing-extensions-and-net-framework-data-providers-ssrs.md).  
  
 Para obter mais informações sobre extensões de processamento de dados personalizadas, consulte [Implementando uma extensão de processamento de dados](../extensions/data-processing/implementing-a-data-processing-extension.md). Para obter mais informações sobre os provedores de dados [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] padrão, consulte o namespace <xref:System.Data> .  
  
 Para obter mais informações sobre extensões de processamento de dados com suporte do Construtor de Relatórios, consulte [Data Connections, Data Sources, and Connection Strings in Report Builder](../data-connections-data-sources-and-connection-strings-in-report-builder.md) [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios] na [documentação do Construtor de Relatórios](https://go.microsoft.com/fwlink/?LinkId=154494) no msdn.microsoft.com.  
  
## <a name="platform-support-for-report-data-sources"></a>Suporte da plataforma a fontes de dados de relatório  
 As fontes de dados que você pode usar em uma implantação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] variam de acordo com a edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , com a versão do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e com a plataforma. Para obter mais informações sobre os recursos [do, consulte recursos com suporte nas edições do SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md). Posteriormente neste tópico, uma tabela fornece informações sobre fontes de dados para as quais há suporte de acordo com a versão e a plataforma.  
  
 Considerações sobre plataforma em relação a fontes de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] são feitas separadamente para o cliente de criação do relatório e o para o servidor de relatório.  
  
### <a name="on-the-report-authoring-client"></a>Em relação ao cliente de criação do relatório  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] é um aplicativo de 32 bits. [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] não tem suporte em uma plataforma baseada em Itanium. Em uma plataforma x64, você precisa instalar provedores de dados de 32 bits no diretório da plataforma (x86) para editar e visualizar relatórios no Designer de Relatórios.  
  
### <a name="on-the-report-server"></a>Em relação ao servidor de relatório  
 Quando você implanta um relatório em um servidor de 64 bits (x86), o servidor de relatório deve contar com provedores de dados de 64 bits compilados nativos já instalados. Não há suporte para a disposição de um provedor de dados de 32 bits em interfaces de 64 bits. Para obter mais informações, consulte a documentação do provedor de dados.  
  
## <a name="supported-data-sources"></a>Fontes de dados com suporte  
 A seguinte tabela lista extensões de processamento e provedores de dados [!INCLUDE[msCoName](../../includes/msconame-md.md)] que você pode usar para recuperar dados referentes a conjuntos de dados e a modelos de relatório. Para obter mais informações sobre uma extensão ou provedor de dados, clique no link na segunda coluna. As colunas da tabela são descritas da seguinte forma:  
  
-   Fonte de dados de relatório: o tipo de dados acessados. Por exemplo, banco de dados relacional, banco de dados multidimensional, arquivo simples ou XML. Esta coluna responde à pergunta: "Quais tipos de dados [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] pode usar em um relatório?"  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Tipo de fonte de dados: Um dos tipos da fonte de dados exibido na lista suspensa quando você define uma fonte de dados no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. A lista é preenchida com DPEs instaladas e registradas, além de provedores de dados. Esta coluna responde à pergunta: "Que tipo de fonte de dados devo selecionar na lista suspensa ao criar uma fonte de dados de relatório?"  
  
-   Nome da extensão de processamento/provedor de dados: A extensão de processamento de dados [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou outro provedor de dados que corresponde ao tipo selecionado da fonte de dados [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Esta coluna responde à pergunta: "Ao selecionar um tipo de fonte de dados, qual extensão provedor ou processamento de dados correspondente é usada?"  
  
-   Versão do provedor de dados subjacente (opcional): alguns tipos de fonte de dados são compatíveis com mais de um provedor de dados. Essas versões poderiam ser diferentes do mesmo provedor ou implementações diferentes de terceiros em relação a um tipo de provedor de dados. O nome do provedor costuma ser exibido na cadeia de conexão após a configuração de uma fonte de dados. Esta coluna responde à pergunta: "Depois de selecionar o tipo de fonte de dados, qual provedor de dados devo selecionar na caixa de diálogo **Propriedades da Conexão**?"  
  
-   *\<Plataforma>* da fonte de dados: A plataforma da fonte de dados compatível com a extensão de processamento ou o provedor de dados em relação à fonte de dados de destino. Esta coluna responde à pergunta: "A extensão de processamento ou o provedor de dados podem recuperar dados de uma fonte nesse tipo de plataforma?"  
  
-   Versão da fonte de dados: a versão da fonte de dados de destino compatível com o DPE ou o provedor de dados. Esta coluna responde à pergunta: "Esse provedor de dados ou extensão de processamento de dados pode recuperar dados dessa versão da fonte de dados?"  
  
-   *\<Plataforma>* do RS: As plataformas do servidor de relatório e do cliente de criação do relatório em que é possível instalar uma DPE personalizada ou provedor de dados. As extensões de processamento de dados internas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] estão incluídas em todas as instalações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Uma extensão de processamento de dados personalizada ou um provedor de dados do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] deve ser compilado nativamente em relação a uma plataforma específica. Esta coluna responde à pergunta: "Esse provedor de dados ou extensão de processamento de dados pode ser instalado nesse tipo de plataforma?"  
  
###  <a name="types-of-data-sources"></a><a name="DataSourcesTable"></a> Tipos de fontes de dados  
  
|Fonte de<br /><br /> dados de relatório|Tipo da fonte de dados do Reporting Services|Nome da extensão de processamento/provedor de dados|Versão do provedor de dados subjacente<br /><br /> (Opcional)|Dados<br /><br /> Fonte<br /><br /> Plataforma x86|Dados<br /><br /> Fonte<br /><br /> Plataforma x64|Versão da fonte de dados|RS<br /><br /> Plataforma x86|RS<br /><br /> Plataforma x64|  
|-------------------------------|-----------------------------------------|------------------------------------------------------|-------------------------------------------------------|--------------------------------------|--------------------------------------|----------------------------|-------------------------|-------------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados relacional|[Microsoft SQL Server](#MicrosoftSQLServer)|Extensão de processamento de dados interna do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Estende System.Data.SqlClient|S|S|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e posterior.|S|S|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados relacional|[OLEDB](#OLEDBSQL)|Extensão de processamento de dados interna do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Estende System.Data.OledbClient|S|S|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e posterior.|S|S|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados relacional|[ODBC](#ODBC)|Extensão de processamento de dados interna do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Estende System.Data.OdbcClient|S|S|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e posterior.|S|S|  
|[!INCLUDE[ssSDS](../../includes/sssds-md.md)]|[Banco de Dados SQL do Azure](#Azure)|Extensão de processamento de dados interna do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Estende System.Data.SqlClient|N/D|N/D|[!INCLUDE[ssSDS](../../includes/sssds-md.md)]|S|S|  
|[!INCLUDE[ssDW](../../includes/ssdw-md.md)] dispositivo|[Microsoft Parallel Data Warehouse](#PWD)|Extensão de processamento de dados interna do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|N/D|N/D|N/D|[!INCLUDE[ssDWfull](../../includes/ssdwfull-md.md)]|S|S|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados multidimensional|[Microsoft SQL Server Analysis Services](#AnalysisServices)|Extensão de processamento de dados interna do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Usa ADOMD.NET|S|S|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]e posterior<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]e posterior|S|S|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados multidimensional|[OLEDB](#OLEDBAS9)|Extensão de processamento de dados interna do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Estende System.Data.OledbClient<br /><br /> Versão 10.0|S|S|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|S|S|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados multidimensional|[OLEDB](#OLEDBAS9)|Extensão de processamento de dados interna do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Estende System.Data.OledbClient<br /><br /> Versão 9,0|S|S|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|S|S|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados multidimensional|OLEDB|Extensão de processamento de dados interna do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Estende System.Data.OledbClient<br /><br /> Versão 8.0|S|N|N/D|S|N|  
|Listas do SharePoint|[Lista do Microsoft SharePoint](#SharePointList)|Extensão de processamento de dados interna do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Obtém dados do Lists.asmx ou de interfaces API do modelo de objeto do SharePoint.<br /><br /> Consulte a [Observação](#SharePointList).|N|S|Produtos do SharePoint 2013<br /><br /> Produtos do SharePoint 2010|S|S|  
|Listas do SharePoint|[Lista do Microsoft SharePoint](#SharePointList)|Extensão de processamento de dados interna do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Obtém dados do Lists.asmx ou de interfaces API do modelo de objeto do SharePoint.<br /><br /> Consulte a [Observação](#SharePointList).|S|S|[!INCLUDE[winSPServ](../../includes/winspserv-md.md)]3,0 e [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007|S|S|  
|XML|[XML](#XML)|Extensão de processamento de dados interna do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Fontes de dados XML não têm dependências de plataforma.|N/D|N/D|[!INCLUDE[vstecwebservices](../../includes/vstecwebservices-md.md)] ou documentos|S|S|  
|Modelo do Servidor de Relatório|Modelo de Relatório|Extensão de processamento de dados interna do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para um arquivo SMDL publicado|Fontes de dados para um uso modelo das extensões de processamento de dados internas.<br /><br /> Modelos baseados em Oracle exigem componentes do cliente da Oracle.<br /><br /> Modelos baseados em Teradata exigem o Provedor de Dados .NET para Teradata da Teradata.<br /><br /> Consulte a documentação da Teradata para obter suporte à plataforma.|N/D|N/D|Os modelos podem ser criados no:[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e posterior.<br /><br /> [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]<br /><br /> Oracle 9.2.0.3 ou versão posterior<br /><br /> Teradata V14, v13, v12 e v6.2|S|S|  
|Banco de dados multidimensional SAP|[SAP BI NetWeaver](#SapBINetWeaver)|Extensão de processamento de dados interna do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Consulte a documentação da SAP para obter suporte à plataforma.|N/D|N/D|SAP BI NetWeaver 3.5|S|N/D|  
|[!INCLUDE[extEssbase](../../includes/extessbase-md.md)]|[Hyperion Essbase](#Hyperion)|Extensão de processamento de dados interna do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Consulte a documentação da Hyperion para obter suporte à plataforma.|S|N/D|[!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 9.3.1|S|N/D|  
|Banco de dados relacional do Oracle|[Oracle](#OracleClient)|Extensão de processamento de dados interna do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Estende System.Data.OracleClient<br /><br /> Exige componentes do cliente da Oracle.|S|N/D|Oracle 10g, 9, 8.1.7|S|S|  
|Banco de dados relacional da Teradata|[Teradata](#Teradata)|Extensão de processamento de dados interna do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Estende o Provedor de Dados .NET para Teradata da Teradata.<br /><br /> Exige Provedor de Dados .NET para Teradata da Teradata.<br /><br /> Consulte a documentação da Teradata para obter suporte à plataforma.|S|N/D|Teradata v14<br /><br /> Teradata v13<br /><br /> Teradata versão 12<br /><br /> Teradata versão 6.20|S|N|  
|Banco de dados relacional do DB2|Nome de extensão de dados registrada personalizado||2004 Host Integration (HI) Server<br /><br /> Consulte a [documentação do HI Server](https://msdn.microsoft.com/library/gg241192\(v=bts.10\).aspx).|S|N/D|N/D|S|N|  
|Fonte de dados OLE DB genérica|[OLEDB](#OLEDBStandard)|Extensão de processamento de dados interna do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Qualquer fonte de dados que ofereça suporte a OLE DB.<br /><br /> Consulte a documentação da fonte de dados para obter suporte à plataforma.|S|N/D|Qualquer fonte de dados que ofereça suporte a OLE DB. Consulte a [Observação](#OLEDBStandard).|S|N/D|  
|Fonte de dados ODBC genérica|[ODBC](#ODBCGeneric)|Extensão de processamento de dados interna do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Qualquer fonte de dados que ofereça suporte a ODBC.<br /><br /> Consulte a documentação da fonte de dados para obter suporte à plataforma.|S|N/D|Qualquer fonte de dados que ofereça suporte a ODBC. Consulte a [Observação](#ODBCGeneric).|S|S|  
  
 Para obter informações sobre como usar uma fonte de dados tabular, consulte [conexões de dados, fontes de dados e cadeias de conexão no Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
 Para obter informações sobre como usar fontes de dados externas, consulte [Adicionar dados de fontes de dados externas &#40;SSRS&#41;](add-data-from-external-data-sources-ssrs.md).  
  
 Muitos provedores de dados [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] padrão são disponibilizados por terceiros. Para obter mais informações, pesquise os sites ou os fóruns dos terceiros.  
  
 Para instalar e registrar uma extensão de processamento de dados personalizada ou um provedor de dados [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] padrão, você precisará consultar a documentação de referência do provedor de dados. Para obter mais informações, consulte [Registrar um provedor de dados padrão do .NET Framework &#40;SSRS&#41;](register-a-standard-net-framework-data-provider-ssrs.md).  
  
 [Retornar à tabela de fontes de dados](#DataSourcesTable)  
  
## <a name="reporting-services-data-processing-extensions"></a>Extensões de processamento de dados do Reporting Services  
 As seguintes extensões de processamento de dados são instaladas automaticamente com o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e o [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]. Para obter mais informações e verificar a instalação, consulte [arquivo de configuração RSReportDesigner](../report-server/rsreportdesigner-configuration-file.md) e [arquivo de configuração RSReportServer](../report-server/rsreportserver-config-configuration-file.md).  
  
> [!NOTE]  
>  A extensão de processamento de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não tem suporte no momento.  
  
 Para obter mais informações sobre extensões de processamento de dados com suporte do Construtor de Relatórios, consulte [Data Connections, Data Sources, and Connection Strings in Report Builder](../data-connections-data-sources-and-connection-strings-in-report-builder.md) [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios] na [documentação do Construtor de Relatórios](https://go.microsoft.com/fwlink/?LinkId=154494) no msdn.microsoft.com.  
  
###  <a name="microsoft-sql-server-data-processing-extension"></a><a name="MicrosoftSQLServer"></a> Extensão de processamento de dados do Microsoft SQL Server  
 O tipo de fonte de dados **Microsoft SQL Server** encapsula e estende o Provedor de Dados [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa extensão de processamento de dados é compilada de maneira nativa e se destina à execução nas plataformas baseadas em x86 e em [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)].  
  
 No [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)], o designer de consulta associado a essa extensão de dados é o [Visual Database Tool designer](../../ssms/visual-db-tools/visual-database-tool-designers.md). Caso você use o designer de consulta em modo gráfico, a consulta é analisada e, possivelmente, reescrita. Use o designer de consultas com base em texto quando quiser controlar a sintaxe [!INCLUDE[tsql](../../includes/tsql-md.md)] exata usada em uma consulta. Para obter mais informações, consulte [Ferramentas do designer de consultas e de modos de exibição &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) e [Interface do usuário do designer de consultas gráficas](graphical-query-designer-user-interface.md).  
  
 Para obter mais informações, consulte [Tipo de conexão do SQL Server &#40;SSRS&#41;](sql-server-connection-type-ssrs.md).  
  
 No Construtor de Relatórios, o criador de consultas associado a esta extensão de dados é o Designer de Consulta Relacional. Para obter mais informações, consulte [Interface do usuário do designer de consultas relacionais](../relational-query-designer-user-interface.md).  
  
 [Retornar à tabela de fontes de dados](#DataSourcesTable)  
  
###  <a name="azure-sql-database-processing-extension"></a><a name="Azure"></a>Extensão de processamento do banco de dados SQL do Azure  
 O tipo **[!INCLUDE[ssSDS](../../includes/sssds-md.md)]** de fonte de dados é quebrado e [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] estende o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]provedor de dados para.  
  
 No [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)], o designer de consultas gráficas associado a essa extensão de dados é a [Interface do usuário do designer de consultas relacionais](../relational-query-designer-user-interface.md), e não o [Designer do Visual Database Tool](../../ssms/visual-db-tools/visual-database-tool-designers.md) que você usa com o tipo de fonte de dados **Microsoft SQL Server**.  
  
 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]diferencia automaticamente entre **[!INCLUDE[ssSDS](../../includes/sssds-md.md)]** e **Microsoft SQL Server** tipos de fonte de dados e abre o designer de consultas gráficas associado ao tipo de fonte de dados.  
  
 Caso você use o designer de consulta em modo gráfico, a consulta é analisada e, possivelmente, reescrita. Um designer de consulta com base em texto também está disponível para gravar consultas. Use o designer de consultas com base em texto quando quiser controlar a sintaxe [!INCLUDE[tsql](../../includes/tsql-md.md)] exata usada em uma consulta. Para obter mais informações, consulte [Interface do usuário do Designer de Consultas baseado em texto](../text-based-query-designer-user-interface.md).  
  
 A recuperação de dados do [!INCLUDE[ssSDS](../../includes/sssds-md.md)] e do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é semelhante, mas há alguns requisitos que se aplicam apenas ao [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Para obter mais informações, consulte [Tipo de conexão do SQL Azure &#40;SSRS&#41;](sql-azure-connection-type-ssrs.md).  
  
 [Retornar à tabela de fontes de dados](#DataSourcesTable)  
  
###  <a name="microsoft-sql-server-parallel-data-warehouse-processing-extension"></a><a name="PWD"></a> Extensão de processamento do Microsoft SQL Server Parallel Data Warehouse  
 No [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)], o designer de consultas gráficas associado a essa extensão de dados é a [Interface do usuário do designer de consultas relacionais](../relational-query-designer-user-interface.md), e não o [Designer do Visual Database Tool](../../ssms/visual-db-tools/visual-database-tool-designers.md) que você usa com o tipo de fonte de dados **Microsoft SQL Server**.  
  
 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]o diferencia automaticamente entre **SQL Server Data Warehouse paralelas** e **Microsoft SQL Server** tipos de fonte de dados e abre o designer de consultas gráficas associado ao tipo de fonte de dados.  
  
 Caso você use o designer de consulta em modo gráfico, a consulta é analisada e, possivelmente, reescrita. Um designer de consulta com base em texto também está disponível para gravar consultas. Use o designer de consultas com base em texto quando quiser controlar a sintaxe [!INCLUDE[tsql](../../includes/tsql-md.md)] exata usada em uma consulta. Para obter mais informações, consulte [Interface do usuário do Designer de Consultas baseado em texto](../text-based-query-designer-user-interface.md).  
  
 O [!INCLUDE[ssDWCurrentFull](../../includes/ssdwcurrentfull-md.md)] não oferece suporte ao uso de procedimentos armazenados e funções avaliadas por tabela em consultas. Para obter mais informações, consulte [Tipo de conexão do SQL Server Parallel Data Warehouse &#40;SSRS&#41;](sql-server-parallel-data-warehouse-connection-type-ssrs.md).  
  
 [Retornar à tabela de fontes de dados](#DataSourcesTable)  
  
###  <a name="microsoft-sql-server-analysis-services-data-processing-extension"></a><a name="AnalysisServices"></a> Extensão de processamento de dados do Microsoft SQL Server Analysis Services  
 Ao selecionar o tipo de fonte de dados **Microsoft SQL Server Analysis Services**, você seleciona uma extensão de processamento de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que estende o Provedor de Dados [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Essa extensão de processamento de dados é compilada de maneira nativa e se destina à execução nas plataformas baseadas em x64 e x86.  
  
 Esse provedor de dados usa o modelo de objeto ADOMD.NET par criar consultas que usam XMLA (XML for Analysis) versão 1.1. Os resultados são retornados como um conjunto de linhas bidimensional. Para obter mais informações, consulte [Tipo de conexão do Analysis Services para MDX &#40;SSRS&#41;](analysis-services-connection-type-for-mdx-ssrs.md), [Tipo de conexão do Analysis Services para DMX &#40;SSRS&#41;](analysis-services-connection-type-for-dmx-ssrs.md), [Interface do usuário do Designer de Consultas MDX do Analysis Services](analysis-services-mdx-query-designer-user-interface.md) e [Interface do usuário do Designer de Consultas DMX do Analysis Services](analysis-services-dmx-query-designer-user-interface.md).  
  
 Ao se conectar a uma fonte de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], a extensão de processamento de dados do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é compatível com os parâmetros de vários valores e mapeia as propriedades da célula e do membro para propriedades estendidas compatíveis com o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para obter mais informações, consulte [Propriedades de campos estendidos para um banco de dados do Analysis Services &#40;SSRS&#41;](extended-field-properties-for-an-analysis-services-database-ssrs.md).  
  
 Também é possível criar modelos de fontes de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
###  <a name="ole-db-data-processing-extension"></a><a name="OLEDBAll"></a> OLE DB Data Processing Extension  
 A extensão de processamento de dados do OLE DB requer a opção por uma camada de provedor de dados adicional com base na versão da fonte de dados que você deseja usar no relatório. Caso você não selecione um provedor de dados específico, é fornecido um padrão. Escolha um provedor de dados específico por meio da caixa de diálogo **Propriedades da conexão** , acessada por meio do botão **Editar** nas caixas de diálogo [fonte de dados](../data-source-properties-dialog-box-general.md) ou [fonte de dados compartilhada](../shared-data-source-properties-dialog-box-general.md) .  
  
 Para obter mais informações sobre o designer de consultas associado do OLE DB, consulte [Ferramentas do designer de consultas e de modos de exibição &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) e [Interface do usuário do designer de consultas gráficas](graphical-query-designer-user-interface.md). Para obter mais informações sobre suporte específico a provedores OLE DB, consulte [Visual Studio .NET Designer Tool Supports Specific OLE DB Providers](https://support.microsoft.com/default.aspx/kb/811241) [Ferramenta de designer .NET do Visual Studio dá suporte a provedores OLE DB específicos] na Base de Dados de Conhecimento [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 [Retornar à tabela de fontes de dados](#DataSourcesTable)  
  
####  <a name="ole-db-for-sql-server"></a><a name="OLEDBSQL"></a> OLE DB para SQL Server  
 Ao selecionar o tipo de fonte de dados **OLE DB**, você está selecionando uma extensão de processamento de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que estende o Provedor de Dados [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para OLE DB. Essa extensão de processamento de dados é compilada de maneira nativa e se destina à execução nas plataformas x86 e x64.  
  
 Para obter mais informações, consulte [Tipo de conexão OLE DB &#40;SSRS&#41;](ole-db-connection-type-ssrs.md).  
  
 [Retornar à tabela de fontes de dados](#DataSourcesTable)  
  
####  <a name="ole-db-for-analysis-services-90"></a><a name="OLEDBAS9"></a>OLE DB para Analysis Services 9,0  
 Para se conectar ao [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], selecione Provedor [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 9.0, selecione Provedor the data source type **OLE DB**e o provedor de dados subjacente pelo nome. Essa combinação entre a extensão de processamento e o provedor de dados é compilada de maneira nativa e se destina à execução nas plataformas x86 e x64.  
  
> [!NOTE]  
>  Essa extensão de processamento de dados não oferece suporte a agregações de servidor, a mapeamento automático das propriedades de campo estendidas e a parâmetros de consulta. O provedor de dados recomendado para uma fonte de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é o **Microsoft SQL Server Analysis Services**.  
  
 Para obter mais informações, consulte [Tipo de conexão OLE DB &#40;SSRS&#41;](ole-db-connection-type-ssrs.md).  
  
 [Retornar à tabela de fontes de dados](#DataSourcesTable)  
  
#### <a name="ole-db-for-olap-70"></a>OLE DB para OLAP 7.0  
 Não há suporte para Provedor OLE DB para OLAP Services 7.0.  
  
 [Retornar à tabela de fontes de dados](#DataSourcesTable)  
  
####  <a name="ole-db-for-oracle"></a><a name="OracleOLEDB"></a> OLE DB para Oracle  
 A extensão de processamento de dados OLE DB para Oracle não é compatível com os seguintes tipos de dados Oracle: BLOB, CLOB, NCLOB, BFILE, UROWID.  
  
 Há suporte para parâmetros sem-nome que dependam da posição. Essa extensão não oferece suporte a parâmetros nomeados. Para parâmetros nomeados, use a extensão de processamento de dados [Oracle](#OracleClient) .  
  
 Para obter informações sobre como configurar uma fonte de dados Oracle, consulte [Como usar o Reporting Services para configurar e acessar uma fonte de dados Oracle](https://support.microsoft.com/kb/834305). Para obter mais informações sobre a configuração de permissões adicionais, consulte [How to add permissions for the NETWORK SERVICE security principal](https://support.microsoft.com/kb/870668) [Como adicionar permissões à entidade de segurança SERVIÇO DE REDE] na Base de Dados de Conhecimento [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 [Retornar à tabela de fontes de dados](#DataSourcesTable)  
  
####  <a name="ole-db-standard-net-framework-data-provider"></a><a name="OLEDBStandard"></a> Provedor de dados .NET Framework padrão OLE DB  
 Para recuperar dados de uma fonte de dados com suporte a provedores de dados OLE DB [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] , use o tipo de fonte de dados **OLE DB** e selecione o provedor de dados padrão ou escolha um dos provedores de dados instalados na caixa de diálogo **Cadeia de Conexão** .  
  
> [!NOTE]  
>  Ainda que um provedor de dados possa oferecer suporte à visualização de um relatório no cliente de criação, nem todos os provedores de dados OLE DB foram projetados para oferecer suporte a relatórios publicados em um servidor de relatório.  
  
 [Retornar à tabela de fontes de dados](#DataSourcesTable)  
  
###  <a name="odbc-data-processing-extension"></a><a name="ODBC"></a> ODBC Data Processing Extension  
 Ao selecionar o tipo de fonte de dados **ODBC**, você está selecionando uma extensão de processamento de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que estende o Provedor de Dados [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para ODBC. Essa extensão de processamento de dados é compilada de maneira nativa e se destina à execução nas plataformas x86 e [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)] . Use essa extensão para se conectar a e recuperar dados de qualquer fonte que tenha um provedor ODBC.  
  
> [!NOTE]  
>  Ainda que um provedor de dados possa oferecer suporte à visualização de um relatório no cliente de criação, nem todos os provedores de dados ODBC foram projetados para oferecer suporte a relatórios publicados em um servidor de relatório.  
  
 [Retornar à tabela de fontes de dados](#DataSourcesTable)  
  
####  <a name="odbc-standard-net-framework-data-provider"></a><a name="ODBCGeneric"></a> Provedor de dados .NET Framework ODBC padrão  
 Para recuperar dados de uma fonte com suporte a um provedor de dados ODBC [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] padrão, use o tipo de fonte de dados **ODBC** e selecione o provedor de dados padrão ou escolha um dos provedores de dados instalados na caixa de diálogo **Cadeia de Conexão** .  
  
> [!NOTE]  
>  Ainda que um provedor de dados possa oferecer suporte à visualização de um relatório no cliente de criação, nem todos os provedores de dados ODBC foram projetados para oferecer suporte a relatórios publicados em um servidor de relatório.  
  
 [Retornar à tabela de fontes de dados](#DataSourcesTable)  
  
###  <a name="oracle-data-processing-extension"></a><a name="OracleClient"></a> Extensão de processamento de dados Oracle  
 Ao selecionar o tipo de fonte de dados **Oracle**, você está selecionando uma extensão de processamento de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que estende o Provedor de Dados [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para Oracle. A fonte de dados **Oracle** encapsula e estende as <xref:System.Data.OracleClient> classes necessárias pelo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para recuperar dados de relatório de um banco de dados Oracle, o administrador deve instalar as ferramentas do cliente Oracle. Esse provedor de dados usa a OCI (Oracle Call Interface) do Oracle 8i versão 3 conforme fornecido pelo software Oracle Client. A versão do aplicativo do cliente deve ser 8.1.7 ou posterior. Essas ferramentas devem ser instaladas no cliente de criação do relatório para visualizar relatórios e, no servidor de relatório, exibir relatórios publicados.  
  
 Essa extensão dá suporte a parâmetros nomeados. Para o Oracle versão 9 ou posterior, há suporte para parâmetros de vários valores. Para parâmetros sem nome dependentes de posição, use a extensão de processamento de dados OLE DB com o Provedor [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB para Oracle. Para obter informações sobre como configurar uma fonte de dados Oracle, consulte [Como usar o Reporting Services para configurar e acessar uma fonte de dados Oracle](https://support.microsoft.com/kb/834305). Para obter mais informações sobre a configuração de permissões adicionais, consulte [How to add permissions for the NETWORK SERVICE security principal](https://support.microsoft.com/kb/870668) [Como adicionar permissões à entidade de segurança SERVIÇO DE REDE] na Base de Dados de Conhecimento [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 É possível recuperar dados de procedimentos armazenados com vários parâmetros de entrada, mas o procedimento armazenado deve retornar apenas um cursor de saída. Para obter mais informações, consulte a seção Oracle em [Retrieving Data Using the DataReader](https://go.microsoft.com/fwlink/?LinkId=81758)[Recuperando dados usando o DataReader].  
  
 Para obter mais informações, consulte [Tipo de conexão Oracle &#40;SSRS&#41;](oracle-connection-type-ssrs.md). Para obter mais informações sobre o designer de consultas associado, consulte [Ferramentas do designer de consultas e de modos de exibição &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) e [Interface do usuário do designer de consultas gráficas](graphical-query-designer-user-interface.md).  
  
 Também é possível criar modelos com base em um banco de dados Oracle.  
  
 [Retornar à tabela de fontes de dados](#DataSourcesTable)  
  
###  <a name="teradata-data-processing-extension"></a><a name="Teradata"></a> Extensão de processamento de dados Teradata  
 Ao selecionar o tipo de fonte de dados **Teradata**, você está selecionando uma extensão de processamento de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que estende o Provedor de Dados .NET Framework para Teradata. Para recuperar dados de relatório de um banco de dados Teradata, o administrador do sistema deve instalar o Provedor de Dados .NET Framework para Teradata no cliente de criação do relatório para editar e visualizar relatórios e, no servidor de relatório, exibir relatórios publicados.  
  
 Para projetos de servidor de relatório, não há um designer de consultas gráficas disponível para essa extensão. Você deve usar o designer de consulta baseado em texto para criar consultas.  
  
 A seguinte tabela mostra quais versões do Provedor de Dados .NET para Teradata têm suporte para definir uma fonte de dados em uma definição de relatório no [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]:  
  
|Versão do [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]|Versão do banco de dados Teradata|Versão do .NET Framework Data Provider para Teradata|  
|-----------------------------------|-------------------------------|-------------------------------------------------------|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|12,00|12,00|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|6.20|12,00|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|12,00|12.00.01|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|6.20|12.00.01|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|13.00|13.0.0.1|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|12,00|12.00.01|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|6.20|12.00.01|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|13.00|13.0.0.1|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|6.20|12.00.01|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|12,00|12.00.01|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|13.00|13.0.0.1|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|14.00|14.00.01|  
  
 Essa extensão oferece suporte a parâmetros de vários valores. Macros podem ser especificadas em uma consulta usando o comando EXECUTAR em modo de consulta TEXTO.  
  
 Para obter mais informações, consulte [Tipo de conexão Teradata &#40;SSRS&#41;](teradata-connection-type-ssrs.md).  
  
 Também é possível criar modelos com base em um banco de dados Teradata. Para obter mais informações, consulte o seguinte white paper no site da Teradata: [Microsoft SQL Server 2012 Reporting Services and Teradata Corporation](http://www.teradata.com/white-papers/Microsoft-SQL-Server-2012-Reporting-Services-and-Teradata-Corporation/?type=WP)[Microsoft SQL Server 2012 Reporting Services e Teradata Corporation].  
  
 [Retornar à tabela de fontes de dados](#DataSourcesTable)  
  
###  <a name="sharepoint-list-data-extension"></a><a name="SharePointList"></a> Extensão de dados de lista do SharePoint  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] inclui a Extensão de Dados de Lista do SharePoint do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para que você possa usar as listas do SharePoint como uma fonte de dados em um relatório. Você pode recuperar dados da lista do seguinte:  
  
-   [!INCLUDE[SPS2013](../../includes/sps2013-md.md)]  
  
-   [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] e [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]  
  
-   [!INCLUDE[winSPServ](../../includes/winspserv-md.md)]3,0 e [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007  
  
 Há três implementações do provedor de dados de Lista do SharePoint.  
  
1.  De um ambiente de criação de relatórios, como o Construtor de Relatórios ou o Designer de Relatórios no [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)], ou para um servidor de relatório configurado em modo nativo, os dados da lista têm origem no serviço Web Lists.asmx para o site do SharePoint.  
  
2.  Em um servidor de relatório que é configurado em modo Integrado do SharePoint, dados da lista têm origem no serviço Web de Lists.asmx correspondente ou em chamadas programáticas à SharePoint API. Neste modo, você pode recuperar dados da lista de um farm do SharePoint.  
  
3.  Para [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] o [!INCLUDE[SPS2013](../../includes/sps2013-md.md)]e o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , o suplemento para [!INCLUDE[msCoName](../../includes/msconame-md.md)] tecnologias do SharePoint permite que você recupere dados da lista de um serviço Web Lists. asmx para um site do SharePoint ou do site do SharePoint que faz parte de um farm do SharePoint. Esse cenário também é conhecido como *modo local* , uma vez que não há necessidade de um servidor de relatório.  
  
 As credenciais que você pode especificar dependem da implementação que o aplicativo cliente usa. Para obter mais informações, consulte [Tipo de conexão de lista do SharePoint &#40;SSRS&#41;](sharepoint-list-connection-type-ssrs.md).  
  
###  <a name="xml-data-processing-extension"></a><a name="XML"></a> Extensão de processamento de dados XML  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] inclui uma extensão de processamento de dados XML para permitir o uso de dados XML em um relatório. Os dados podem ser recuperados de um documento XML, de um serviço Web ou de um aplicativo baseado na Web que possa ser acessado por meio de uma URL. Para obter mais informações, consulte [Tipo de conexão XML &#40;SSRS&#41;](xml-connection-type-ssrs.md). Para obter mais informações sobre o designer de consultas associado, consulte a seção sobre o designer de consultas baseado em texto em [Interface do usuário do designer de consultas gráficas](graphical-query-designer-user-interface.md). Para obter exemplos, consulte [Reporting Services: Using XML and Web Service Data Sources](https://go.microsoft.com/fwlink/?LinkId=81654)[Reporting Services: usando fontes de dados XML e de serviço Web].  
  
 [Retornar à tabela de fontes de dados](#DataSourcesTable)  
  
###  <a name="sap-netweaver-business-intelligence-data-processing-extension"></a><a name="SapBINetWeaver"></a>Extensão de processamento de dados do SAP NetWeaver Business Intelligence  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] inclui uma extensão de processamento de dados que permite a você usar dados de uma fonte do [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)] em um relatório.  
  
 Para obter mais informações, consulte [Tipo de conexão SAP NetWeaver BI &#40;SSRS&#41;](sap-netweaver-bi-connection-type-ssrs.md). Para obter mais informações sobre o designer de consultas associado, consulte [Interface do usuário do designer de consultas do SAP NetWeaver BI](sap-netweaver-bi-query-designer-user-interface.md).  
  
 Para obter mais informações sobre o [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)], consulte [Using SQL Server 2008 Reporting Services with SAP NetWeaver Business Intelligence](https://go.microsoft.com/fwlink/?LinkId=167352)[Usando o SQL Server 2008 Reporting Services com o SAP NetWeaver Business Intelligence].  
  
 [Retornar à tabela de fontes de dados](#DataSourcesTable)  
  
###  <a name="hyperion-essbase-business-intelligence-data-processing-extension"></a><a name="Hyperion"></a> Extensão de processamento de dados Hyperion Essbase Business Intelligence  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] inclui uma extensão de processamento de dados que permite usar dados de uma fonte de dados [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] em um relatório.  
  
 Para obter mais informações, consulte [Tipo de conexão Hyperion Essbase &#40;SSRS&#41;](hyperion-essbase-connection-type-ssrs.md). Para obter mais informações sobre o designer de consultas associado, consulte [Interface do usuário do designer de consultas do Hyperion Essbase](hyperion-essbase-query-designer-user-interface.md).  
  
 Para obter mais informações sobre o [!INCLUDE[extEssbase](../../includes/extessbase-md.md)], consulte [Using SQL Server 2005 Reporting Services with Hyperion Essbase](https://go.microsoft.com/fwlink/?LinkId=81970)[Usando o SQL Server 2005 Reporting Services com o Hyperion Essbase].  
  
 [Retornar à tabela de fontes de dados](#DataSourcesTable)  
  
## <a name="see-also"></a>Consulte Também  
 [Conexões de dados, fontes de dados e cadeias de conexão no Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Adicionar dados a um relatório &#40;Construtor de Relatórios e SSRS&#41;](report-datasets-ssrs.md)  
  
  
