---
title: Noções básicas sobre o Power View para modelos multidimensionais | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f8874a442897bd5dd887d7e9903777f81824cb46
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68165089"
---
# <a name="understanding-power-view-for-multidimensional-models"></a>Noções básicas sobre o Power View para modelos multidimensionais
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Este artigo descreve o recurso Power View para Modelos Multidimensionais no SQL Server e oferece informações importantes para profissionais de BI e administradores que pretendem implementar o Power View para Modelos Multidimensionais na respectiva organização.  
  
 Os modelos multidimensionais oferecem modelagem de dados OLAP, armazenamento e soluções de análise líderes de mercado. Os modelos multidimensionais no SQL Server oferecem suporte à análise de dados ad-hoc, exploração e visualização usando o Microsoft Power View.  
  
 O Power View é um cliente Web fino iniciado diretamente no navegador de um arquivo de Fonte de Dados de Relatório (.rsds) compartilhado em uma biblioteca do SharePoint. A Fonte de Dados de Relatório age como uma ponte entre o cliente e a fonte de dados de back-end. A fonte de dados de back-end pode ser uma pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no SharePoint, um modelo Tabular em um servidor do Analysis Services executado em modo Tabular ou um modelo Multidimensional em um servidor do Analysis Services executado em modo Multidimensional. Os relatórios do Power View podem então ser salvos em uma biblioteca ou galeria do SharePoint e compartilhados com outros membros de sua organização.  
  
 **Power View para arquitetura de Modelos Multidimensionais**  
  
 ![Power View para arquitetura de modelos multidimensionais](../../analysis-services/multidimensional-models/media/daxmd-architecture.gif "Power View para arquitetura de modelos multidimensionais")  
  
## <a name="prerequisites"></a>Pré-requisitos  
 **Requisitos do servidor**  
  
-   Microsoft SQL Server 2016 Analysis Services em execução no modo Multidimensional.  
  
-   Suplemento Microsoft SQL Server 2016 Reporting Services para Microsoft SharePoint Server 2010 ou Enterprise Edition posterior.  
  
 **Requisitos de cliente**  
  
-   A funcionalidade de cliente do Power View exige o Microsoft Silverlight 5. Para obter mais informações, veja [Suporte ao navegador para Reporting Services e Power View](../../reporting-services/browser-support-for-reporting-services-and-power-view.md).  
  
## <a name="features"></a>Recursos  
 **Suporte nativo para o Power View**  
  
 Com esta versão, os modelos multidimensionais oferecem suporte à análise e à visualização usando o Power View no modo SharePoint. Nenhuma configuração especial dos seus modelos multidimensionais é necessária. Entretanto, existem algumas diferenças na forma como os objetos do modelo multidimensional são exibidos no Power View em comparação a outras ferramentas cliente, como o Microsoft Excel e o Microsoft Performance Point. Esta versão não dá suporte à análise e à visualização de modelos multidimensionais usando o Power View no Excel.  
  
 **Suporte nativo para consultas DAX**  
  
 Com esta versão, os modelos multidimensionais dão suporte às consultas e às funções DAX, além de suporte às consultas MDX mais tradicionais. Algumas funções DAX, como PATH, não se aplicam na modelagem multidimensional. Para compreender melhor o DAX e como ele se compara ao MDX, consulte [Expressões de Análise de Dados e MDX](http://msdn.microsoft.com/library/ff487170\(SQL.105\).aspx).  
  
## <a name="multidimensional-to-tabular-object-mapping"></a>Mapeamento de objeto multidimensional a tabular  
 O Analysis Services oferece uma representação de metadados de modelo tabular de um modelo multidimensional. Os objetos em um modelo multidimensional são representados como objetos tabulares no Power View e no CSDL de saída com anotações de BI.  
  
 **Resumo de mapeamento de objeto**  
  
|Objeto multidimensional|Objeto tabular|  
|-----------------------------|--------------------|  
|Cube|Modelo|  
|Dimensão do cubo|Tabela|  
|Atributos de dimensão (chave(s), nome)|coluna|  
|Grupo de Medidas|Tabela|  
|Measure|Measure|  
|Medida sem um grupo de medidas|Em uma tabela chamada Medidas|  
|Grupo de Medidas Cubo Dimensão Relação|Relação|  
|Perspectiva|Perspectiva|  
|KPI|KPI|  
|Hierarquias pai-filho/usuário|Hierarquia|  
|Exibir Pasta|Exibir Pasta|  
  
## <a name="measures-measure-groups-and-kpis"></a>Medidas, grupos de medidas e KPIs  
  
> [!NOTE]  
>  Algumas imagens e textos deste artigo referem-se ao Modelo Multidimensional da Adventure Works para o banco de dados de exemplo do SQL Server 2012.  
  
 Os grupos de medidas em um cubo multidimensional são vistos na Lista de Campos do Power View como tabelas com o sinal sigma (∑).  
  
 **Grupos de medidas na Lista de Campos do Power View**  
  
 ![Campo de lista no Power View](../../analysis-services/multidimensional-models/media/daxmd-powerviewfieldlist.gif "campo lista no Power View")  
  
 Medidas em um grupo de medidas aparecem como medidas. Se houver medidas calculadas que não tenham um grupo de medidas associado, elas serão agrupadas em uma tabela especial chamada Medidas.  
  
 Para ajudar a simplificar modelos multidimensionais mais complexos, os autores do modelo poderão definir um conjunto de medidas ou KPIs em um cubo a ser colocado em uma pasta de exibição. O Power View pode mostrar pastas de exibição e medidas e KPIs nelas.  
  
 **Medidas e KPIs em um grupo de medidas**  
  
 ![Grupo de medidas na lista de campos do Power View](../../analysis-services/multidimensional-models/media/daxmd-fieldlist-group.gif "grupo de medidas na lista de campos do Power View")  
  
### <a name="measures-as-variants"></a>Medidas como variantes  
 As medidas em modelos multidimensionais são variantes. Isso significa que as medidas não são fortemente tipadas e podem ter tipos de dados diferentes. Por exemplo, na imagem abaixo, a medida de valor na tabela relatórios financeiros por padrão é o tipo de dados Currency, mas também tem um valor de cadeia de caracteres "NA" para o subtotal de "Contas estatísticas", que é o tipo de dados de cadeia de caracteres. O Power View reconhece determinadas medidas como variantes e mostra os valores corretos e a formatação nas visualizações diferentes.  
  
 **Medida como variante**  
  
 ![Hierarquia não agregável no Power View](../../analysis-services/multidimensional-models/media/daxmd-nonaggrattrib.gif "Hierarquia não agregável no Power View")  
  
### <a name="implicit-measures"></a>Medidas implícitas  
 Os modelos tabulares oferece aos usuários a capacidade de criar medidas *implícitas* como contagem, soma ou média em campos. Para modelos multidimensionais, como dados de atributo de dimensão são armazenados de forma diferente, consultar as medidas implícitas pode levar muito tempo. Por causa disso, as medidas implícitas não estão disponíveis no Power View.  
  
## <a name="dimensions-attributes-and-hierarchies"></a>Dimensões, atributos e hierarquias  
 As dimensões de cubo são expostas como tabelas em metadados tabulares. Na Lista de Campos do Power View, os atributos de dimensão são mostrados como colunas nas pastas de exibição.  Os atributos de dimensão que têm a propriedade AttributeHierarchyEnabled definida como false; Por exemplo: Atributo de data de nascimento na dimensão cliente ou a propriedade AttributeHierarchyVisible definida como false não aparecerão na lista de campo do Power View. Hierarquias de vários níveis ou hierarquias de usuário; por exemplo, Geografia do Cliente na dimensão Cliente, são expostas como hierarquias na Lista de Campos do Power View. UnknownMembers ocultos de um atributo de dimensão são expostos em Consultas DAX e no Power View.  
  
 **Dimensão, atributos e hierarquias no SQL Server Data Tools (SSDT) e na Lista de Campos do Power View**  
  
 ![Dimensões no SSDT e na lista de campos do Power View](../../analysis-services/multidimensional-models/media/daxmd-ssdt-dimensions.gif "dimensões no SSDT e na lista de campos do Power View")  
  
### <a name="dimension-attribute-type"></a>Tipo de atributo de dimensão  
 Os modelos multidimensionais dão suporte à associação de atributos de dimensão com tipos de atributo de dimensão específicos. A imagem abaixo mostra a dimensão Geografia, onde os atributos de dimensão Cidade, Estado-Província, País e CEP têm tipos geográficos associados a eles. Eles serão expostos nos metadados tabulares. O Power View reconhece os metadados, permitindo que os usuários criem visualizações de mapa. Isso é indicado pelo ícone de mapa ao lado das colunas Cidade, País, CEP e Estado-Província na tabela Geografia da Lista de Campos do Power View.  
  
 **Tipos de geografia de atributo de dimensão no SSDT e Lista de Campos do Power View**  
  
 ![Tipos de Geografia de atributo de dimensão](../../analysis-services/multidimensional-models/media/daxmd-ssdt-attribute-geog-types.gif "tipos de Geografia de atributo de dimensão")  
  
### <a name="dimension-calculated-members"></a>Membros calculados de dimensão  
 Os modelos multidimensionais dão suporte a membros calculados para filhos de Todos com um único membro real. As restrições adicionais durante a exposição deste tipo de membro calculado são:  
  
-   Deve ser um único membro real quando a dimensão tiver mais de um atributo.  
  
-   Um atributo com membros calculados não poderá ser o atributo de chave da dimensão, a menos que seja o único atributo.  
  
-   Um atributo com membros calculados não pode ser um atributo pai-filho.  
  
 Membros calculados de hierarquias de usuário não são expostos no Power View; entretanto, os usuários finais ainda poderão se conectar a um cubo com membros calculados em hierarquias de usuário.  
  
 A imagem abaixo mostra um relatório do Power View para um cubo que contém membros calculados de inteligência de tempo no atributo de dimensão "Cálculos de data Fiscal" na dimensão Data.  
  
 **Relatório do Power View com membros calculados**  
  
 ![Membros calculados na Power View](../../analysis-services/multidimensional-models/media/daxmd-calcmembersinpowerview.gif "membros calculados na Power View")  
  
### <a name="default-members"></a>Membros padrão  
 Membros padrão de suporte a modelos multidimensionais para atributos de dimensão. O membro padrão é usado pelo Analysis Services durante a agregação de dados para uma consulta. O membro padrão de um atributo de dimensão é exposto como o valor ou o filtro padrão para a coluna correspondente nos metadados tabulares.  
  
 O Power View se comporta de forma bem semelhante às Tabelas Dinâmicas do Excel quando atributos são aplicados. Quando um usuário adiciona uma coluna a uma visualização do Power View (tabela, matriz ou gráfico) que contenha um valor padrão, o valor padrão não será aplicado e todos os valores disponíveis serão mostrados. Se o usuário adicionar a coluna a Filtros, o valor padrão será aplicado.  
  
### <a name="dimension-security"></a>Segurança de dimensão  
 Dimensão de suporte a modelos multidimensionais e segurança no nível da célula por meio de funções. Um usuário que estiver se conectando a um cubo usando o Power View é autenticado e avaliado para obtenção das permissões adequadas. Quando a segurança de dimensão for aplicada, os respectivos membros da dimensão não serão vistos pelo usuário no Power View; entretanto, se um usuário tiver uma permissão de segurança de célula definida onde determinadas células estiverem restritas, então esse usuário não poderá se conectar ao cubo usando o Power View. Em alguns casos, os usuários poderão agregar dados quando partes desses dados forem calculados a partir dos dados protegidos.  
  
### <a name="non-aggregatable-attributeshierarchies"></a>Atributos/hierarquias não agregáveis  
 Em um modelo multidimensional, atributos de uma dimensão podem ter a propriedade IsAggregatable definida como falsa. Isso significa que o autor do modelo especificou que aplicativos cliente não devem agregar os dados entre hierarquias (no nível do atributos ou em vários níveis) quando consultarem os dados. No Power View, esse atributo de dimensão é exposto como uma coluna para a qual subtotais não estão disponíveis. Na imagem abaixo, você pode ver um exemplo de uma hierarquia não agregável: Contas. O nível superior da hierarquia pai-filho de Contas é não agregável, enquanto os outros níveis são agregáveis. em uma visualização em matriz da hierarquia de Contas (os dois primeiros níveis), você verá subtotais para o Nível de Conta 02, mas não para o nível superior, Nível de Conta 01.  
  
 **Hierarquia não agregável no Power View**  
  
 ![Hierarquia não agregável no Power View](../../analysis-services/multidimensional-models/media/daxmd-nonaggrattrib.gif "Hierarquia não agregável no Power View")  
  
## <a name="images"></a>Imagens  
 O Power View fornece a capacidade de renderizar imagens. Em modelos multidimensionais, uma das maneiras de poder fornecer imagens ao Power View é expor colunas com URLs das imagens. Com esta versão, o Analysis Services dá suporte à marcação de atributos de dimensão, como o tipo ImageURL. Esse tipo de dados é então fornecido ao Power View nos metadados tabulares. O Power View pode então baixar e exibir as imagens especificadas nas URLs nas visualizações.  
  
 **Tipo de atributo de dimensão ImageURL no SSDT**  
  
 ![Propriedades de atributo de dimensão](../../analysis-services/multidimensional-models/media/daxmd-dimattribute-properties.gif "propriedades de atributo de dimensão")  
  
## <a name="parent-child-hierarchies"></a>Hierarquias pai-filho  
 Os modelos multidimensionais dão suporte a hierarquias pai-filho, que são expostas como uma hierarquia nos metadados tabulares. Cada nível da hierarquia pai-filho é exposta como uma coluna oculta. O atributo de chave da dimensão pai-filho não é exposto nos metadados tabulares.  
  
 **Hierarquias pai-filho no Power View**  
  
 ![Hierarquias pai-filho](../../analysis-services/multidimensional-models/media/daxmd-ssdt-hierarchies.gif "Hierarquias pai-filho")  
  
## <a name="perspectives-and-translations"></a>Perspectivas e traduções  
 As perspectivas são exibições de cubos, onde somente determinadas dimensões ou grupos de medidas estão visíveis em ferramentas de cliente. Você pode especificar um nome de perspectiva como um valor para a propriedade da cadeia de conexão de Cubo. Por exemplo, na cadeia de conexão a seguir, 'Vendas diretas' é uma perspectiva no modelo multidimensional:  
  
 `Data Source=localost;Initial Catalog=AdventureWorksDW-MD;Cube='Direct Sales'`  
  
 Os cubos podem ter metadados e traduções de dados especificadas para os diversos Idiomas no modelo. Para ver as traduções (dados e metadados), você precisará adicionar a propriedade "Identificador de localidade" opcional à cadeia de conexão no arquivo RSDS como mostrado abaixo.  
  
 `Data Source=localost;Initial Catalog=AdventureWorksDW-MD;Cube='Adventure Works'; Locale Identifier=3084`  
  
 Quando o Power View se conectar a um modelo multidimensional com um arquivo .rsds com um Identificador de Localidade, e se uma tradução correspondente estiver contida no cubo, os usuários verão as traduções no Power View.  
  
 Para obter mais informações, consulte [Create a Report Data Source](../../analysis-services/multidimensional-models/create-a-report-data-source.md).  
  
## <a name="power-view-pinned-filters"></a>Filtros fixados no Power View  
 Os relatórios do Power View podem conter várias exibições. Com esta versão, o recurso *Fixar Filtro* para os modelos tabulares e multidimensionais oferece a capacidade de criar filtros que se apliquem a todas as exibições em um relatório. A imagem abaixo mostra o botão de alternância Fixar filtro para um filtro de exibição. Por padrão, um filtro de exibição é desafixado e se aplica somente àquela exibição. A fixação de um filtro de exibição o aplica a todas as exibições; desafixá-lo o removerá de outras exibições.  
  
 **Filtros Fixados**  
  
 ![Fixado filtro](../../analysis-services/multidimensional-models/media/daxmd-pinnedfilterinpowerview.gif "fixado filtro")  
  
## <a name="unsupported-features"></a>Recursos sem suporte  
 **Power View no Excel 2013** -não oferece suporte a conexão e à criação de relatórios para modelos multidimensionais. No entanto, **Power View no Excel 2016** não dá suporte à conexão e à criação de relatórios para modelos multidimensionais. Para saber mais, confira [Power View e OLAP no Excel 2016](https://support.office.com/en-us/article/power-view-and-olap-in-excel-2016-ea5ff7a5-ea5f-48d4-aeb0-98c89ab738ac)  
  
 **Ações** – não têm suporte em relatórios do Power View ou em consultas DAS em um modelo multidimensional.  
  
 **Conjuntos nomeados** – em modelos multidimensionais, não têm suporte no Power View ou em consultas DAX em um modelo multidimensional.  
  
> [!NOTE]  
>  Ações Sem Suporte e Conjuntos Nomeados não impedem que os usuários se conectem a modelos multidimensionais e os explorem usando o Power View.  
  
 **Segurança em nível de célula** -não há suporte para relatórios do Power View.  
  
## <a name="csdlbi-annotations"></a>Anotações de CSDLBI  
 Os metadados de cubo multidimensional são expostos como um modelo conceitual baseado em EDM (Modelo de Dados de Entidade) por anotações de CSDLBI (Linguagem de Definição de Esquema Conceitual com Business Intelligence).  
  
 Os metadados multidimensionais são representados como um namespace de modelo tabular em um documento CSDLBI, ou CSDL de saída, quando uma solicitação DISCOVER_CSDL_METADATA for enviada para a instância do Analysis Services.  
  
 **Solicitação DISCOVER_CSDL_METADATA de exemplo**  
  
```  
<Envelopexmlns="http://schemas.xmlsoap.org/soap/envelope/">  
   <Body>  
      <Discoverxmlns="urn:schemas-microsoft-com:xml-analysis">  
         <RequestType>DISCOVER_CSDL_METADATA</RequestType>  
         <Restrictions>  
            <RestrictionList>  
              <CATALOG_NAME>"catalogname"<CATALOG_NAME>  
            </RestrictionList>  
         </Restrictions>  
         <Properties>  
            <PropertyList>  
            </PropertyList>  
         </Properties>  
      </Discover>  
   </Body>  
</Envelope>  
  
```  
  
 A solicitação DISCOVER_CSDL_METADATA tem as seguintes restrições:  
  
|Name|Obrigatório|Descrição|  
|----------|--------------|-----------------|  
|CATALOG_NAME|Sim|O nome do catálogo/banco de dados.|  
|PERSPECTIVE_NAME|Sim, se o cubo contiver mais de uma perspectiva. Opcional se houver somente um cubo ou se houver uma perspectiva padrão.|O nome do cubo ou o nome da perspectiva no banco de dados multidimensional.|  
|VERSION|Sim|Versão de CSDL solicitada pelo cliente. Recursos e construções multidimensionais têm suporte na versão 2.0.|  
  
 O documento CSDL de saída de retorno representa o modelo como um namespace, que contém entidades, associações e propriedades.  
  
 Para obter mais informações sobre anotações de CSDLBI para modelos de tabela, consulte [referência técnica para anotações de BI para CSDL](https://docs.microsoft.com/bi-reference/csdl/technical-reference-for-bi-annotations-to-csdl) no MSDN, e [ \[MS-CSDLBI\]: Definições de esquema conceitual formato de arquivo com anotações de Business Intelligence](http://msdn.microsoft.com/library/jj161299\(SQL.105\).aspx).  
  
## <a name="client-help-on-officecom"></a>Ajuda do cliente no Office.com  
 Os artigos a seguir são fornecidos no site Office.com para ajudar os usuários a descobrir como os objetos do Modelo Multidimensional aparecem no Power View e como criar relatório de exemplo:  
  
 [Noções básicas sobre objetos do Modelo Multidimensional no Power View](http://office.microsoft.com/en-us/excel-help/understanding-multidimensional-model-objects-in-power-view-HA104018589.aspx)  
  
 [Explore o Modelo Multidimensional da Adventure Works usando o Power View](http://office.microsoft.com/excel-help/explore-the-adventure-works-multidimensional-model-by-using-power-view-HA104046830.aspx)  
  
  
