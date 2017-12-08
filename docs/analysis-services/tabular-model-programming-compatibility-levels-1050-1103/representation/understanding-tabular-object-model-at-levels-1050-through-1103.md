---
title: "Noções básicas sobre o modelo de objeto de tabela em níveis 1050 por meio de 1103 | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 6077b7e8-cb3e-4480-a5de-bb602cf9d69a
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4c6d64d576aa1b95cabb9e343ffb514b11125be6
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="understanding-tabular-object-model-at-levels-1050-through-1103"></a>Noções básicas sobre o modelo de objeto de tabela em níveis 1050 por meio de 1103

[!INCLUDE[ssas-appliesto-sqlas-all](../../../includes/ssas-appliesto-sqlas-all.md)]

  Um modelo de tabela é uma representação lógica de tabelas, relações, hierarquias, perspectivas, medidas, e Chave de Desempenho. Esta seção apresenta a implementação interna usando AMO. Consulte [desenvolvimento com o Analysis Management Objects &#40; AMO &#41; ](../../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md) se você não tiver usado AMO antes.  
  
 A abordagem aqui é invertida, todos os objetos pertinentes no modelo de tabela são mapeados logicamente para objetos AMO e a interação ou o fluxo de trabalho necessário explicada. Um exemplo de código fonte para criar um modelo de tabela usando AMO, exemplo AMO para tabela está disponível no Codeplex. Uma observação importante sobre o código no exemplo: ele é fornecido apenas como um suporte aos conceitos lógicos explicados aqui e não deve ser usado em um ambiente de produção. O exemplo é fornecido sem suporte ou garantia.  
  
## <a name="database-representation"></a>Representação de banco de dados  
 Um banco de dados fornece o objeto de contêiner para o modelo de tabela. Todos os objetos em um modelo de tabela estão contidos no banco de dados. Em termos de objetos AMO, uma representação de banco de dados tem uma relação de mapeamento de um para um com <xref:Microsoft.AnalysisServices.Database> e nenhum outro objeto AMO principal é necessário. É importante observar que isso não significa que todos os objetos contidos no banco de dados AMO podem ser usados durante a modelagem de tabela.  
  
 Consulte [representação &#40; do banco de dados Tabela &#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/database-representation-tabular.md) para obter uma explicação detalhada sobre como criar e manipular a representação de banco de dados.  
  
## <a name="connection-representation"></a>Representação de conexão  
 Uma conexão estabelece a relação entre os dados a serem incluídos em uma solução de modelo de tabela e o modelo em si. Em termos de objetos AMO, uma conexão tem uma relação de mapeamento de um para um com <xref:Microsoft.AnalysisServices.DataSource> e nenhum outro objeto AMO principal é necessário. É importante observar que isso não significa que todos os objetos contidos na fonte de dados AMO podem ser usados durante a modelagem.  
  
 Consulte [representação de Conexão &#40; Tabela &#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/connection-representation-tabular.md) para obter uma explicação detalhada sobre como criar e manipular a representação de fonte de dados.  
  
## <a name="table-representation"></a>Representação de tabela  
 Tabelas são objetos de banco de dados que contêm os dados no banco de dados. Em termos de objetos AMO, uma tabela tem uma relação de mapeamento um para muitos. Uma tabela é representada pelo uso dos seguintes objetos AMO: <xref:Microsoft.AnalysisServices.DataSourceView>, <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.CubeDimension>, <xref:Microsoft.AnalysisServices.MeasureGroup> e <xref:Microsoft.AnalysisServices.Partition> são os objetos necessários principais; entretanto, é importante notar que isso não significa que todos os objetos contidos nos objetos AMO mencionados antes podem ser usados na modelagem de tabela.  
  
 Consulte [tabelas representação &#40; Tabela &#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/tables-representation-tabular.md) para obter uma explicação detalhada sobre como criar e manipular a representação de tabela.  
  
### <a name="calculated-column-representation"></a>Representação de coluna calculada  
 Colunas calculadas são expressões avaliadas que geram uma coluna em uma tabela, onde um novo valor é calculado e armazena para cada linha na tabela. Em termos de objetos AMO, uma coluna calculada tem uma relação de mapeamento um para muitos. Uma coluna calculada é representada pelo uso dos seguintes objetos AMO: <xref:Microsoft.AnalysisServices.Dimension> e <xref:Microsoft.AnalysisServices.MeasureGroup> são os objetos necessários principais. É importante observar que isso não significa que todos os objetos contidos nos objetos AMO mencionados anteriormente podem ser usados durante a modelagem.  
  
 Consulte [calculado representação de coluna &#40; Tabela &#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/tables-calculated-column-representation.md) para obter uma explicação detalhada sobre como criar e manipular a representação de coluna calculada.  
  
### <a name="calculated-measure-representation"></a>Representação de medida calculada  
 Medidas calculadas são expressões armazenadas que são avaliadas mediante solicitação quando modelo é implantado. Em termos de objetos AMO, uma medida calculada tem uma relação de mapeamento um para muitos. Uma coluna calculada é representada pelo uso dos seguintes objetos AMO: <xref:Microsoft.AnalysisServices.MdxScript.Commands%2A> e <xref:Microsoft.AnalysisServices.MdxScript.CalculationProperties%2A> são os objetos necessários principais. É importante observar que isso não significa que todos os objetos contidos nos objetos AMO mencionados anteriormente podem ser usados durante a modelagem.  
  
> [!NOTE]  
>  Os objetos <xref:Microsoft.AnalysisServices.Measure> não têm nenhuma relação com as medidas calculadas em modelos de tabela e não têm suporte nesses modelos.  
  
 Consulte [calculado representação de medida &#40; Tabela &#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/tables-calculated-measure-representation.md) para obter uma explicação detalhada sobre como criar e manipular a representação de medida calculada.  
  
### <a name="hierarchy-representation"></a>Representação de hierarquia  
 Hierarquias são um mecanismo para fornecer uma experiência de busca detalhada/drill up mais enriquecedora ao usuário final. Em termos de objetos AMO, uma representação de hierarquia tem uma relação de mapeamento de um para um com <xref:Microsoft.AnalysisServices.Hierarchy> e nenhum outro objeto AMO principal é necessário. É importante observar que isso não significa que todos os objetos contidos no banco de dados AMO podem ser usados durante a modelagem de tabela.  
  
 Consulte [representação de hierarquia &#40; Tabela &#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/tables-hierarchy-representation.md) para obter uma explicação detalhada sobre como criar e manipular a representação de hierarquia.  
  
### <a name="key-performance-indicator-kpi--representation"></a>Representação de KPI (indicador chave de desempenho)  
 Um KPI é usado para medir o desempenho de um valor, definido por uma medida base, em relação a um valor de destino. Em termos de objetos AMO, uma representação de KPI tem uma relação de mapeamento um-para-muitos. Um KPI é representado pelo uso dos seguintes objetos AMO: <xref:Microsoft.AnalysisServices.MdxScript.Commands%2A>e <xref:Microsoft.AnalysisServices.MdxScript.CalculationProperties%2A> são os principais objetos necessários.  É importante observar que isso não significa que todos os objetos contidos nos objetos AMO mencionados anteriormente podem ser usados durante a modelagem.  
  
> [!NOTE]  
>  Além disso, uma distinção importante, os objetos <xref:Microsoft.AnalysisServices.Kpi> não têm nenhuma relação com os KPIs em modelos de tabela. E eles não têm suporte em modelos de tabela.  
  
 Consulte [representação de indicador de desempenho &#40; da chave Tabela &#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/tables-key-performance-indicator-representation.md) para obter uma explicação detalhada sobre como criar e manipular a representação de KPI.  
  
### <a name="partition-representation"></a>Representação de partição  
 Para fins operacionais, uma tabela pode ser dividida em subconjuntos diferentes de linhas que, quando combinados formam a tabela. Cada um desses subconjuntos é uma partição da tabela. Em termos de objetos AMO, uma representação de partição tem uma relação de mapeamento com <xref:Microsoft.AnalysisServices.Partition> e nenhum outro objeto AMO principal é necessário. É importante observar que isso não significa que todos os objetos contidos no banco de dados AMO podem ser usados durante a modelagem de tabela.  
  
 Consulte [partição representação &#40; Tabela &#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/tables-partition-representation.md) para obter uma explicação detalhada sobre como criar e manipular a representação de partição.  
  
## <a name="relationship-representation"></a>Representação de relação  
 Uma relação é uma conexão entre duas tabelas de dados. A relação estabelece como os dados nas duas tabelas devem ser correlacionados.  
  
 Em modelos de tabela, podem ser definidas várias relações entre duas tabelas. Quando várias relações entre duas tabelas são definidas, apenas uma pode ser definida como a relação ativa padrão. Todas as outras relações estão inativas.  
  
 Em termos de objetos AMO, todas as relações inativas têm uma representação de uma relação de mapeamento de um para um com <xref:Microsoft.AnalysisServices.Relationship> e nenhum outro objeto AMO principal é necessário. Para a relação ativa, há outros requisitos e um mapeamento para <xref:Microsoft.AnalysisServices.ReferenceMeasureGroupDimension> é necessário também. É importante observar que isso não significa que todos os objetos contidos na relação AMO ou objeto referenceMeasureGroupDimension podem ser usados durante a modelagem de tabela.  
  
 Consulte [representação de relação &#40; Tabela &#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/relationship-representation-tabular.md) para obter uma explicação detalhada sobre como criar e manipular a representação de relação.  
  
## <a name="perspective-representation"></a>Representação de perspectiva  
 Uma perspectiva é um mecanismo para simplificar ou focar o modo. Em termos de objetos AMO, uma representação de relação tem uma relação de mapeamento de um para um com <xref:Microsoft.AnalysisServices.Perspective> e nenhum outro objeto AMO principal é necessário. É importante observar que isso não significa que todos os objetos contidos no objeto de perspectiva AMO podem ser usados durante a modelagem de tabela.  
  
 Consulte [representação de perspectiva &#40; Tabela &#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/perspective-representation-tabular.md) para obter uma explicação detalhada sobre como criar e manipular a representação de perspectiva.  
  
> [!WARNING]  
>  Perspectivas não são um mecanismo de segurança; objetos fora da perspectiva ainda podem ser acessados pelo usuário através de outras interfaces.  
  
  
