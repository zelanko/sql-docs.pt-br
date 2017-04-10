---
title: "Tipo de conex&#227;o Teradata (SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b02779c2-a6b9-453c-815f-adad53353952
caps.latest.revision: 10
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 9
---
# Tipo de conex&#227;o Teradata (SSRS)
  Para incluir dados de um banco de dados relacional Teradata no seu relatório, é necessário ter um conjunto de dados baseado na fonte de dados do relatório do tipo Teradata. Esse tipo de fonte de dados interna é baseado na extensão de processamento de dados do Provedor Gerenciados do .NET para Teradata.  
  
 Use as informações deste tópico para criar uma fonte de dados. Para obter instruções passo a passo, consulte [Adicionar e verificar uma conexão de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a> Cadeia de Conexão  
 Contate o administrador do banco de dados para obter informações sobre a conexão e as credenciais que devem ser usadas para se conectar à fonte de dados. O exemplo de cadeia de conexão seguinte define um banco de dados Teradata no servidor especificado com um endereço IP:  
  
```  
data source=<IP Address>  
```  
  
 Para obter mais exemplos de cadeias de conexão, consulte [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](../Topic/Data%20Connections,%20Data%20Sources,%20and%20Connection%20Strings%20in%20Report%20Builder.md).  
  
##  <a name="Credentials"></a> Credenciais  
 As credenciais são necessárias para executar consultas, visualizar o relatório localmente e visualizá-lo no servidor de relatório.  
  
 Após a publicação do relatório, talvez seja necessário alterar as credenciais da fonte de dados para que, quando o relatório for executado no servidor de relatório, as permissões recuperadas sejam válidas.  
  
 Para obter mais informações, consulte [Conexões de dados, fontes de dados e cadeias de conexão &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) ou [Especificar as credenciais no Construtor de Relatórios](../Topic/Specify%20Credentials%20in%20Report%20Builder.md).  
  
 ![Ícone de seta usado com o link Voltar ao Início](../../analysis-services/instances/media/uparrow16x16.png "Ícone de seta usado com o link Voltar ao Início") [Voltar ao Início](#BackToTop)  
  
##  <a name="Remarks"></a> Comentários  
 Para que você possa se conectar a uma fonte de dados Teradata, o administrador do sistema deve ter instalado a versão do Provedor de Dados .NET para Teradata que dá suporte à recuperação de dados do banco de dados Teradata. O provedor de dados deve ser instalado no mesmo computador que o Construtor de Relatórios e também no servidor de relatório.  
  
 Nem todos os modos de entrega de relatório são suportados por esse provedor de dados. Não há suporte para a entrega de relatórios através de assinaturas controladas por dados para essa extensão de processamento de dados. Para obter mais informações, consulte [Usar uma fonte de dados externa para obter dados de assinante &#40;Assinatura controlada por dados&#41;](../../reporting-services/subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md) na documentação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nos [Manuais Online](http://go.microsoft.com/fwlink/?linkid=121312) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de seta usado com o link Voltar ao Início](../../analysis-services/instances/media/uparrow16x16.png "Ícone de seta usado com o link Voltar ao Início") [Voltar ao Início](#BackToTop)  
  
##  <a name="Models"></a> Modelos de relatório  
 Para criar um conjunto de dados de um modelo de relatório baseado em uma fonte de dados Teradata, o modelo deve ser criado em Designer Modelo em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e deve ser publicado em um servidor de relatório.  
  
 ![Ícone de seta usado com o link Voltar ao Início](../../analysis-services/instances/media/uparrow16x16.png "Ícone de seta usado com o link Voltar ao Início") [Voltar ao Início](#BackToTop)  
  
##  <a name="Related"></a> Seções relacionadas  
 Estas seções da documentação fornecem informações conceituais detalhadas sobre dados de relatório, bem como informações de procedimentos sobre como definir, personalizar e usar partes de um relatório relacionadas aos dados.  
  
 [Conjuntos de dados de relatório &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
 Fornece uma visão geral de como acessar dados de seu relatório.  
  
 [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](../Topic/Data%20Connections,%20Data%20Sources,%20and%20Connection%20Strings%20in%20Report%20Builder.md)  
 Fornece informações sobre conexões de dados e fontes de dados.  
  
 [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Fornece informações sobre conjuntos de dados inseridos e compartilhados.  
  
 [Coleção de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 Fornece informações sobre a coleção de campos gerada pela consulta do conjunto de dados.  
  
 [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md) na documentação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nos [Manuais Online](http://go.microsoft.com/fwlink/?linkid=121312) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
 Fornece informações detalhadas sobre suporte à plataforma e à versão para cada extensão de dados.  
  
 [Usando o SQL Server 2008 Reporting Services com o Provedor de Dados do .NET Framework para Teradata](http://go.microsoft.com/fwlink/?LinkID=130848)  
 Fornece informações detalhadas sobre como trabalhar com esta extensão de dados.  
  
 ![Ícone de seta usado com o link Voltar ao Início](../../analysis-services/instances/media/uparrow16x16.png "Ícone de seta usado com o link Voltar ao Início") [Voltar ao Início](#BackToTop)  
  
## Consulte também  
 [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  