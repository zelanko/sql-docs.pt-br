---
title: Acesso a dados modelo tabular | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 6ae74a8b-0025-450d-94a5-4e601831d420
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5dc6ccd51a1ce8c64ef301e7435ee9ce21879cb5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62756827"
---
# <a name="tabular-model-data-access"></a>Acesso a dados de modelo de tabela
  Os bancos de dados modelo de tabela no Analysis Services podem ser acessados pela maioria dos mesmos clientes, interfaces e idiomas que você usa para recuperar dados ou metadados de um modelo multidimensional. Para obter mais informações, consulte [Acesso a dados de modelo multidimensional &#40;Analysis Services – dados multidimensionais 41](../multidimensional-models/mdx/multidimensional-model-data-access-analysis-services-multidimensional-data.md).  
  
 Este tópico descreve os clientes, as linguagens de consulta e as interfaces programáticas que trabalham com modelos de tabela.  
  
## <a name="clients"></a>Clientes  
 Os aplicativos cliente da Microsoft a seguir oferecem suporte a conexões nativas com bancos de dados modelo de tabela do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
### <a name="excel"></a>Excel  
 Você pode se conectar a bancos de dados modelo de tabela do Excel, usando a visualização de dados e recursos de análise no Excel para trabalhar com seus dados. Para acessar os dados, você define uma conexão de dados do Analysis Services, especifica um servidor que é executado em modo de servidor de tabela e escolhe o banco de dados a ser usado. Para obter mais informações, consulte [Conectar ou importar dados do SQL Server Analysis Services](https://go.microsoft.com/fwlink/?linkID=215150).  
  
 O Excel também é o aplicativo indicado para procurar modelos de tabela no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. A ferramenta inclui uma opção **Analisar no Excel** que inicia uma nova instância do Excel, cria uma pasta de trabalho do Excel e abre uma conexão de dados da pasta de trabalho para o banco de dados de workspace do modelo. Ao procurar dados modelo de tabela no Excel, lembre-se de que o Excel emite consultas no modelo usando o cliente Tabela Dinâmica do Excel. Consequentemente, as operações dentro da pasta de trabalho do Excel resultam em consultas MDX que são enviadas ao banco de dados de workspace, não consultas DAX. Se você estiver usando o SQL Profiler ou outra ferramenta de monitoramento para monitorar consultas, poderá encontrar o MDX e não o DAX no rastreamento do profiler. Para obter mais informações sobre o recurso Análise no Excel, consulte [Análise no Excel  40Tabela do SSAS 41](analyze-in-excel-ssas-tabular.md).  
  
### <a name="power-view"></a>Power View  
 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] é um aplicativo cliente de relatórios do Reporting Services executado em um ambiente do SharePoint 2010. Ele combina exploração de dados, design de consulta e layout de apresentação em uma experiência de relatórios ad hoc integrados. [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] pode usar modelos de tabela como fontes de dados, independentemente de o modelo estar hospedado em uma instância do Analysis Services em modo de tabela, ou ser recuperado de um repositório de dados relacional usando o modo DirectQuery. Para conectar a um modelo de tabela no [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], crie um arquivo de conexão que contém o local do servidor e o nome do banco de dados. Você pode criar a fonte de dados compartilhada do Reporting Services ou o arquivo de conexão de modelos semânticos de BI no SharePoint. Para obter mais informações sobre conexões de modelo semântico de BI, consulte [Conexão de modelo semântico do PowerPivot BI &#40;. bism&#41;](../power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md).  
  
 O cliente do [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] determina a estrutura do modelo especificado enviando uma solicitação à fonte de dados especificada, que retorna um esquema que pode ser usado pelo cliente para criar consultas no modelo como uma fonte de dados e executar operações baseadas nos dados. As operações subsequentes na interface do usuário do [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] para filtrar dados, executar cálculos ou agregações e exibir dados associados são controlados pelo cliente e não são manipulados programaticamente.  
  
 As consultas que são enviadas pelo cliente do [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] ao modelo são emitidas como instruções DAX, que você pode monitorar definindo um rastreamento no modelo.  O cliente também emite uma solicitação ao servidor para a definição de esquema inicial, que é apresentada de acordo com o CSDL (linguagem de definição de esquema conceitual). Para obter mais informações, consulte [CSDL Annotations for Business Intelligence &#40;CSDLBI&#41;](https://docs.microsoft.com/bi-reference/csdl/csdl-annotations-for-business-intelligence-csdlbi)  
  
### <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 Você pode usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para gerenciar instâncias que hospedam modelos de tabela e para consultar os metadados e os dados neles. Você pode processar modelos ou os objetos em um modelo, pode criar e gerenciar partições, e definir a segurança que pode ser usada para gerenciar o acesso a dados. Para mais informações, consulte os seguintes tópicos:  
  
-   [Determina o Modo de Servidor de uma instância do Analysis Services.](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
-   [Conectar ao Analysis Services](../instances/connect-to-analysis-services.md)  
  
-   [Monitorar uma instância do Analysis Services](../instances/monitor-an-analysis-services-instance.md)  
  
 Você pode usar as janelas de consulta MDX e XMLA no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para recuperar dados e metadados de um banco de dados modelo de tabela. Entretanto, observe as seguintes restrições:  
  
-   As instruções que usam MDX e DMX não têm suporte para modelos que foram implantados em modo DirectQuery; portanto, se você precisar criar uma consulta em um modelo de tabela em modo DirectQuery, use uma janela **Consulta XMLA** .  
  
-   Você não pode alterar o contexto de banco de dados da janela Consulta XMLA depois de abrir a janela **Consulta** . Portanto, se você precisar enviar uma consulta para um banco de dados diferente ou para uma instância diferente, deve abrir esse banco de dados ou instância usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e abrir uma nova janela **Consulta XMLA** dentro desse contexto.  
  
 Você pode criar rastreamentos em um modelo de tabela do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] assim como o faria em uma solução multidimensional. Nesta versão, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornece muitos novos eventos que podem ser usados para rastrear o uso de memória, operações de consulta e processamento, e uso de arquivo. Para obter mais informações, consulte [Eventos de rastreamento do Analysis Services](https://docs.microsoft.com/bi-reference/trace-events/analysis-services-trace-events).  
  
> [!WARNING]  
>  Se você colocar um rastreamento em um banco de dados modelo de tabela, poderá ver alguns eventos que são categorizados como consultas DMX. Porém, a mineração de dados não tem suporte em dados de modelo de tabela e as consultas DMX executadas no banco de dados são limitadas a instruções SELECT nos metadados do modelo. Os eventos só são categorizados como DMX porque a mesma estrutura de analisador é usada para MDX.  
  
## <a name="query-languages"></a>Linguagens de consulta  
 Os modelos de tabela do Analysis Services dão suporte à maioria das mesmas linguagens de consulta que são fornecidas para acessar modelos multidimensionais. As exceções são os modelos de tabela que foram implantados em modo DirectQuery que não recuperam dados de uma repositório de dados do Analysis Services, mas recuperam dados diretamente de uma fonte de dados do SQL Server. Você não pode consultar esses modelos usando MDX, mas deve usar um cliente que dê suporte à conversão de expressões DAX em instruções Transact-SQL, como o cliente do [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] .  
  
### <a name="dax"></a>DAX  
 Você pode usar DAX para criar expressões e fórmulas em todos os tipos de modelos de tabela, independentemente de o modelo ser armazenado no SharePoint como uma pasta de trabalho do Excel habilitada para PowerPivot, ou em uma instância do Analysis Services.  
  
 Além disso, você pode usar expressões DAX dentro do contexto de uma instrução de comando XMLA EXECUTE para enviar consultas a um modelo de tabela que foi implantado em modo DirectQuery.  
  
 Para obter exemplos de consultas em um modelo de tabela usando DAX, consulte [Referência de sintaxe de consulta DAX](https://msdn.microsoft.com/library/ee634217.aspx).  
  
### <a name="mdx"></a>MDX  
 Você pode usar MDX para criar consultas em modelos de tabela que usam o cache na memória como o método de consulta preferido (ou seja, modelos que não foram implantados em modo DirectQuery). Embora clientes como o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] usem o DAX para criar agregações e para consultar o modelo como uma fonte de dados, se você estiver familiarizado com o MDX, isso poderá ser um atalho para criar consultas de exemplo no MDX, consulte [Criando medidas no MDX](../multidimensional-models/mdx/mdx-building-measures.md).  
  
### <a name="csdl"></a>CSDL  
 O CSDL (linguagem de definição de esquema conceitual) não é uma linguagem de consulta propriamente dita, mas pode ser usado para recuperar informações sobre o modelo e os metadados do modelo, que podem ser usados posteriormente para criar relatórios ou criar consultas no modelo.  
  
 Para obter informações sobre como o CSDL é usado em modelos de tabela, consulte [CSDL Annotations for Business Intelligence &#40;CSDLBI&#41;](https://docs.microsoft.com/bi-reference/csdl/csdl-annotations-for-business-intelligence-csdlbi).  
  
## <a name="programmatic-interfaces"></a>Interfaces programáticas  
 As interfaces principais que são usadas para interagir com modelos de tabela do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] são os conjuntos de linhas de esquema, XMLA e os clientes de consulta e ferramentas de consulta fornecidos pelo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e pelo [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
### <a name="data-and-metadata"></a>Dados e metadados  
 Você pode recuperar dados e metadados de modelos de tabela em aplicativos gerenciados usando ADOMD.NET. Para obter exemplos de aplicativos que criam e modificam objetos em um modelo de tabela, consulte os seguintes recursos:  
  
-   Exemplo AMO de modelo de tabela no Codeplex  
  
-   [Usar DMVs &#40;Exibições de Gerenciamento Dinâmico&#41; para monitorar o Analysis Services](../instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)  
  
 Você pode usar o provedor OLE DB do Analysis Services 9.0 em aplicativos cliente não gerenciados para dar suporte ao acesso OLE DB para modelos de tabela. Uma versão atualizada do provedor OLE DB do Analysis Services é necessária para permitir acesso a modelos de tabela. Para obter mais informações sobre os provedores usados com modelos de tabela, consulte [Instalar o Analysis Services OLE DB Provider em SharePoint Servers](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md) .  
  
 Você também pode recuperar dados diretamente de uma instância do Analysis Services em um formato baseado em XML. Você pode recuperar o esquema do modelo de tabela usando o conjunto de linhas de DISCOVER_CSDL_METADATA ou pode usar um comando EXECUTE ou DISCOVER com elementos, objetos ou propriedades ASSL existentes. Para obter mais informações, consulte os seguintes recursos:  
  
-   [Anotações CSDLBI &#40;CSDL para Business Intelligence&#41;](https://docs.microsoft.com/bi-reference/csdl/csdl-annotations-for-business-intelligence-csdlbi)  
  
### <a name="manipulate-analysis-services-objects"></a>Manipular objetos do Analysis Services  
 Você pode criar, modificar, excluir e processar modelos de tabela e objetos neles, inclusive tabelas, colunas, perspectivas, medidas e partições, usando comandos XMLA, ou usando AMO. AMO e XMLA foram atualizados para dar suporte a propriedades adicionais que são usadas em modelos de tabela para relatório e modelagem aprimorados.  
  
 Para obter exemplos de como objetos tabulares podem ser controlados por script usando AMO e XMLA, consulte os recursos a seguir:  
  
-   Exemplo AMO de modelo de tabela no Codeplex  
  
-   Exemplos do AdventureWorks no CodePlex  
  
 Você pode usar o PowerShell para gerenciar e monitorar instâncias do Analysis Services, assim como para criar e monitorar a segurança usada para acesso a modelos de tabela. Para obter mais informações, consulte [Analysis Services PowerShell](../analysis-services-powershell.md).  
  
### <a name="schema-rowsets"></a>Conjuntos de linhas de esquema  
 Os aplicativos cliente podem usar os conjuntos de linhas de esquema para examinar os metadados de modelos de tabela e para recuperar as informações de suporte e monitoramento a partir do servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Nesta versão do SQL Server, novos conjuntos de linhas de esquema foram adicionados e conjuntos de linhas de esquema existentes foram estendidos para dar suporte a recursos relacionados a modelos de tabela, e para aprimorar o monitoramento e a análise de desempenho no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
-   [Conjunto de linhas DISCOVER_CALC_DEPENDENCY](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-calc-dependency-rowset)  
  
     Novo conjunto de linhas de esquema para rastrear as dependências entre as colunas e as referências em um modelo de tabela  
  
-   [Conjunto de linhas DISCOVER_CSDL_METADATA](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-csdl-metadata-rowset)  
  
     Novo conjunto de linhas de esquema para obter a representação de CSDL de um modelo de tabela  
  
-   [Conjunto de linhas DISCOVER_XEVENT_TRACE_DEFINITION](../dev-guide/discover-xevent-trace-definition-rowset.md)  
  
     Novo conjunto de linhas de esquema para monitorar os Eventos Estendidos do SQL Server. Para obter mais informações, consulte [Use SQL Server Extended Events &#40;XEvents&#41; para monitorar o Analysis Services](../instances/monitor-analysis-services-with-sql-server-extended-events.md).  
  
-   [Conjunto de linhas DISCOVER_TRACES](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-traces-rowset)  
  
     A nova coluna `Type` permite filtrar os rastreamentos por categoria. Para obter mais informações, consulte [Criar rastreamentos do Profiler para reprodução &#40;Analysis Services&#41;](../instances/create-profiler-traces-for-replay-analysis-services.md).  
  
-   [Conjunto de linhas MDSCHEMA_HIERARCHIES](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-hierarchies-rowset)  
  
     A nova enumeração `STRUCTURE_TYPE` dá suporte à identificação de hierarquias definidas pelo usuário criadas em modelos de tabela. Para obter mais informações, consulte [Hierarquias &#40;SSAS Tabular&#41;](hierarchies-ssas-tabular.md).  
  
 Não há nenhuma atualização para os conjuntos de linhas do esquema OLE DB para Mineração de Dados nesta versão.  
  
> [!WARNING]  
>  Você não pode usar as consultas MDX ou DMX em um banco de dados que foi implantado em modo DirectQuery; portanto, se você precisar executar uma consulta em um modelo DirectQuery usando os conjuntos de linhas de esquema, deve usar XMLA, e não o DMV associado. Para DMVs que retornam resultados para o servidor como um todo, como SELECT * de $ $system.DBSCHEMA_CATALOGS ou DISCOVER_TRACES, você pode executar a consulta no conteúdo de um banco de dados que é implantado em um modo armazenado em cache.  
  
## <a name="see-also"></a>Consulte também  
 [Conectar a um modelo de banco de dados de tabela &#40;SSAS&#41;](connect-to-a-tabular-model-database-ssas.md)   
 [Acesso a dados PowerPivot](../power-pivot-sharepoint/power-pivot-data-access.md)   
 [Conectar ao Analysis Services](../instances/connect-to-analysis-services.md)  
  
  
