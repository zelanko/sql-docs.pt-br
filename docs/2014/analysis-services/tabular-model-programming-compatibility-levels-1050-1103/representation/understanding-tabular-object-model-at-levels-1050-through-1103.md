---
title: Compreendendo o modelo de objeto de tabela | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
ms.assetid: 6077b7e8-cb3e-4480-a5de-bb602cf9d69a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dcfd16ae7e49392c9ba0a001ea8d205c4fa88d1c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/25/2020
ms.locfileid: "62795337"
---
# <a name="understanding-the-tabular-object-model"></a>Compreendendo o modelo de objeto de tabela
  Um modelo de tabela é uma representação lógica de tabelas, relações, hierarquias, perspectivas, medidas, e Chave de Desempenho. Esta seção apresenta a implementação interna usando AMO. Consulte [desenvolvimento com Objetos de Gerenciamento de Análise &#40;amo&#41;](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo) se você ainda não usou o amo antes.  
  
 A abordagem aqui é invertida, todos os objetos pertinentes no modelo de tabela são mapeados logicamente para objetos AMO e a interação ou o fluxo de trabalho necessário explicada. Um exemplo de código-fonte para criar um modelo de tabela usando AMO, AMO para Tabela, está disponível em Codeplex. Uma observação importante sobre o código no exemplo: ele é fornecido apenas como um suporte aos conceitos lógicos explicados aqui e não deve ser usado em um ambiente de produção. O exemplo é fornecido sem suporte ou garantia.  
  
## <a name="database-representation"></a>Representação de banco de dados  
 Um banco de dados fornece o objeto de contêiner para o modelo de tabela. Todos os objetos em um modelo de tabela estão contidos no banco de dados. Em termos de objetos AMO, uma representação de banco de dados tem uma relação de mapeamento de um para um com <xref:Microsoft.AnalysisServices.Database> e nenhum outro objeto AMO principal é necessário. É importante observar que isso não significa que todos os objetos contidos no banco de dados AMO podem ser usados durante a modelagem de tabela.  
  
 Consulte [representação do banco de dados&#40;&#41;tabular](database-representation-tabular.md) para obter uma explicação detalhada sobre como criar e manipular a representação do banco de dados.  
  
## <a name="connection-representation"></a>Representação de conexão  
 Uma conexão estabelece a relação entre os dados a serem incluídos em uma solução de modelo de tabela e o modelo em si. Em termos de objetos AMO, uma conexão tem uma relação de mapeamento de um para um com <xref:Microsoft.AnalysisServices.DataSource> e nenhum outro objeto AMO principal é necessário. É importante observar que isso não significa que todos os objetos contidos na fonte de dados AMO podem ser usados durante a modelagem.  
  
 Consulte [representação de conexão &#40;&#41;tabular](connection-representation-tabular.md) para obter uma explicação detalhada sobre como criar e manipular a representação da fonte de dados.  
  
## <a name="table-representation"></a>Representação de tabela  
 Tabelas são objetos de banco de dados que contêm os dados no banco de dados. Em termos de objetos AMO, uma tabela tem uma relação de mapeamento um para muitos. Uma tabela é representada pelo uso dos seguintes objetos AMO: <xref:Microsoft.AnalysisServices.DataSourceView>, <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.CubeDimension>, <xref:Microsoft.AnalysisServices.MeasureGroup> e <xref:Microsoft.AnalysisServices.Partition> são os objetos necessários principais; entretanto, é importante notar que isso não significa que todos os objetos contidos nos objetos AMO mencionados antes podem ser usados na modelagem de tabela.  
  
 Consulte [representação de tabelas &#40;&#41;tabular](tables-representation-tabular.md) para obter uma explicação detalhada sobre como criar e manipular a representação da tabela.  
  
### <a name="calculated-column-representation"></a>Representação de coluna calculada  
 Colunas calculadas são expressões avaliadas que geram uma coluna em uma tabela, onde um novo valor é calculado e armazena para cada linha na tabela. Em termos de objetos AMO, uma coluna calculada tem uma relação de mapeamento um para muitos. Uma coluna calculada é representada pelo uso dos seguintes objetos AMO: <xref:Microsoft.AnalysisServices.Dimension> e <xref:Microsoft.AnalysisServices.MeasureGroup> são os objetos necessários principais. É importante observar que isso não significa que todos os objetos contidos nos objetos AMO mencionados anteriormente podem ser usados durante a modelagem.  
  
 Consulte [representação de coluna calculada &#40;&#41;tabular](tables-calculated-column-representation.md) para obter uma explicação detalhada sobre como criar e manipular a representação de coluna calculada.  
  
### <a name="calculated-measure-representation"></a>Representação de medida calculada  
 Medidas calculadas são expressões armazenadas que são avaliadas mediante solicitação quando modelo é implantado. Em termos de objetos AMO, uma medida calculada tem uma relação de mapeamento um para muitos. Uma coluna calculada é representada pelo uso dos seguintes objetos AMO: <xref:Microsoft.AnalysisServices.MdxScript.Commands%2A> e <xref:Microsoft.AnalysisServices.MdxScript.CalculationProperties%2A> são os objetos necessários principais. É importante observar que isso não significa que todos os objetos contidos nos objetos AMO mencionados anteriormente podem ser usados durante a modelagem.  
  
> [!NOTE]  
>  Os objetos <xref:Microsoft.AnalysisServices.Measure> não têm nenhuma relação com as medidas calculadas em modelos de tabela e não têm suporte nesses modelos.  
  
 Consulte [representação de medida calculada &#40;&#41;tabular](tables-calculated-measure-representation.md) para obter uma explicação detalhada sobre como criar e manipular a representação de medida calculada.  
  
### <a name="hierarchy-representation"></a>Representação de hierarquia  
 Hierarquias são um mecanismo para fornecer uma experiência de busca detalhada/drill up mais enriquecedora ao usuário final. Em termos de objetos AMO, uma representação de hierarquia tem uma relação de mapeamento de um para um com <xref:Microsoft.AnalysisServices.Hierarchy> e nenhum outro objeto AMO principal é necessário. É importante observar que isso não significa que todos os objetos contidos no banco de dados AMO podem ser usados durante a modelagem de tabela.  
  
 Consulte [representação de hierarquia &#40;&#41;de tabela](tables-hierarchy-representation.md) para obter uma explicação detalhada sobre como criar e manipular a representação de hierarquia.  
  
### <a name="key-performance-indicator--kpi--representation"></a>Indicador chave de desempenho-KPI-representação  
 Um KPI é usado para medir o desempenho de um valor, definido por uma medida base, em relação a um valor de destino. Em termos de objetos AMO, uma representação de KPI tem uma relação de mapeamento um-para-muitos. Um KPI é representado pelo uso dos seguintes objetos AMO: <xref:Microsoft.AnalysisServices.MdxScript.Commands%2A>e <xref:Microsoft.AnalysisServices.MdxScript.CalculationProperties%2A> são os principais objetos necessários.  É importante observar que isso não significa que todos os objetos contidos nos objetos AMO mencionados anteriormente podem ser usados durante a modelagem.  
  
> [!NOTE]  
>  Além disso, uma distinção importante, os objetos <xref:Microsoft.AnalysisServices.Kpi> não têm nenhuma relação com os KPIs em modelos de tabela. E eles não têm suporte em modelos de tabela.  
  
 Consulte [representação do indicador de desempenho chave &#40;&#41;de tabela](tables-key-performance-indicator-representation.md) para obter uma explicação detalhada sobre como criar e manipular a representação de KPI.  
  
### <a name="partition-representation"></a>Representação de partição  
 Para fins operacionais, uma tabela pode ser dividida em subconjuntos diferentes de linhas que, quando combinados formam a tabela. Cada um desses subconjuntos é uma partição da tabela. Em termos de objetos AMO, uma representação de partição tem uma relação de mapeamento de um para um com <xref:Microsoft.AnalysisServices.Partition> e nenhum outro objeto AMO principal é necessário. É importante observar que isso não significa que todos os objetos contidos no banco de dados AMO podem ser usados durante a modelagem de tabela.  
  
 Consulte [representação de partição &#40;&#41;tabular](tables-partition-representation.md) para obter uma explicação detalhada sobre como criar e manipular a representação de partição.  
  
## <a name="relationship-representation"></a>Representação de relação  
 Uma relação é uma conexão entre duas tabelas de dados. A relação estabelece como os dados nas duas tabelas devem ser correlacionados.  
  
 Em modelos de tabela, podem ser definidas várias relações entre duas tabelas. Quando várias relações entre duas tabelas são definidas, apenas uma pode ser definida como a relação ativa padrão. Todas as outras relações estão inativas.  
  
 Em termos de objetos AMO, todas as relações inativas têm uma representação de uma relação de mapeamento de um para um com <xref:Microsoft.AnalysisServices.Relationship> e nenhum outro objeto AMO principal é necessário. Para a relação ativa, há outros requisitos e um mapeamento para <xref:Microsoft.AnalysisServices.ReferenceMeasureGroupDimension> é necessário também. É importante observar que isso não significa que todos os objetos contidos na relação AMO ou objeto referenceMeasureGroupDimension podem ser usados durante a modelagem de tabela.  
  
 Consulte [representação de relação &#40;&#41;tabular](relationship-representation-tabular.md) para obter uma explicação detalhada sobre como criar e manipular a representação de relacionamento.  
  
## <a name="perspective-representation"></a>Representação de perspectiva  
 Uma perspectiva é um mecanismo para simplificar ou focar o modo. Em termos de objetos AMO, uma representação de relação tem uma relação de mapeamento de um para um com <xref:Microsoft.AnalysisServices.Perspective> e nenhum outro objeto AMO principal é necessário. É importante observar que isso não significa que todos os objetos contidos no objeto de perspectiva AMO podem ser usados durante a modelagem de tabela.  
  
 Consulte [representação em perspectiva &#40;&#41;tabular](perspective-representation-tabular.md) para obter uma explicação detalhada sobre como criar e manipular a representação de perspectiva.  
  
> [!WARNING]  
>  Perspectivas não são um mecanismo de segurança; objetos fora da perspectiva ainda podem ser acessados pelo usuário através de outras interfaces.  
  
  
