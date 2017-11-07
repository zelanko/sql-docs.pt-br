---
title: Classes OLAP AMO | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Analysis Management Objects, OLAP
- OLAP [AMO]
- AMO, OLAP
ms.assetid: 397509b7-a4fb-40de-aa30-c66dc9ed2105
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5ef144b4a141c15d9d84f4e3e226f654a8f4feff
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="amo-olap-classes"></a>Classes OLAP AMO
  As classes OLAP AMO (Objetos de Gerenciamento de Análise) ajudam você a criar, a modificar, a excluir e a processar cubos, dimensões e objetos relacionados como KPIs (Indicadores Chave de Desempenho), ações e cache.  
  
 Para obter mais informações sobre como configurar o ambiente de programação AMO, como estabelecer uma conexão com um servidor, acessar um banco de dados ou definindo dados de fontes e modos de exibição de fonte de dados, consulte [as Classes fundamentais AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-fundamental-classes.md).  
  
 Este tópico contém as seguintes seções:  
  
-   [Objetos de dimensão](#Dimensions)  
  
-   [Objetos de cubo](#Cubes)  
  
-   [Objetos MeasureGroup](#MeasureGroups)  
  
-   [Objetos de partição](#Partition)  
  
-   [Objetos AggregationDesign](#AggregationDesign)  
  
-   [Objetos de agregação](#Aggregation)  
  
-   [Objetos de ação](#Action)  
  
-   [Objetos KPI](#KPI)  
  
-   [Objetos de perspectiva](#Perspective)  
  
-   [Objetos de tradução](#Translation)  
  
-   [Objetos ProactiveCaching](#ProactiveCaching)  
  
 A ilustração a seguir mostra o relacionamento das classes explicadas neste tópico.  
  
 ![Classes OLAP no AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-olapclasses.gif "Classes OLAP no AMO")  
  
## <a name="basic-classes"></a>Classes básicas  
  
###  <a name="Dimensions"></a>Objetos de dimensão  
 Uma dimensão é criada ao ser adicionada à coleção de dimensões do banco de dados pai e pela atualização do objeto <xref:Microsoft.AnalysisServices.Dimension> no servidor por meio do método Update.  
  
 Para remover uma dimensão, ela terá de ser descartada por meio do método Drop de <xref:Microsoft.AnalysisServices.Dimension>. Remover uma <xref:Microsoft.AnalysisServices.Dimension> da coleção de dimensões do banco de dados usando o método Remove não a excluirá do servidor, somente do modelo de objeto AMO.  
  
 Um objeto <xref:Microsoft.AnalysisServices.Dimension> pode ser processado depois de criado. <xref:Microsoft.AnalysisServices.Dimension> pode ser processado por seu próprio método de acesso, ou pode ser processado com o método do processo do objeto pai, quando o objeto pai for processado.  
  
 Para obter mais informações sobre os métodos e as propriedades disponíveis, consulte <xref:Microsoft.AnalysisServices.Dimension> em <xref:Microsoft.AnalysisServices>.  
  
###  <a name="Cubes"></a>Objetos de cubo  
 Um cubo é criado ao ser adicionado à coleção de cubos do banco de dados, seguido pela atualização do objeto <xref:Microsoft.AnalysisServices.Cube> no servidor usando o método Update. O método Update do cubo pode incluir o parâmetro UpdateOptions.ExpandFull, que garante que todos os objetos do cubo modificados sejam atualizados no servidor nessa ação de atualização.  
  
 Para remover um cubo, ele terá de ser descartado por meio do método Drop de <xref:Microsoft.AnalysisServices.Cube>. A remoção de um cubo da coleção não afetará o servidor.  
  
 Um objeto <xref:Microsoft.AnalysisServices.Cube> pode ser processado depois de criado. <xref:Microsoft.AnalysisServices.Cube> pode ser processado por seu próprio método de acesso, ou pode ser processado quando um objeto pai processa a si mesmo usando seu próprio método Process.  
  
 Para obter mais informações sobre os métodos e as propriedades disponíveis, consulte <xref:Microsoft.AnalysisServices.Cube> em <xref:Microsoft.AnalysisServices>.  
  
###  <a name="MeasureGroups"></a>Objetos MeasureGroup  
 Um grupo de medidas é criado ao ser adicionado à coleção de grupos de medidas do cubo, seguido pela atualização do objeto <xref:Microsoft.AnalysisServices.MeasureGroup> no servidor por meio de seu próprio método Update. Um objeto <xref:Microsoft.AnalysisServices.MeasureGroup> é removido usando seu próprio método Drop.  
  
 Um objeto <xref:Microsoft.AnalysisServices.MeasureGroup> pode ser processado depois de criado. <xref:Microsoft.AnalysisServices.MeasureGroup> pode ser processado por seu próprio método Process, ou pode ser processado quando um objeto pai processa a si mesmo usando seu próprio método Process.  
  
 Para obter mais informações sobre os métodos e as propriedades disponíveis, consulte <xref:Microsoft.AnalysisServices.MeasureGroup> em <xref:Microsoft.AnalysisServices>.  
  
###  <a name="Partition"></a>Objetos de partição  
 Um objeto <xref:Microsoft.AnalysisServices.Partition> é criado ao ser adicionado à coleção de partições do grupo de medidas pai, seguido pela atualização do objeto <xref:Microsoft.AnalysisServices.Partition> no servidor por meio do método Update. Um objeto <xref:Microsoft.AnalysisServices.Partition> é removido por meio do método Drop.  
  
 Para obter mais informações sobre os métodos e as propriedades disponíveis, consulte <xref:Microsoft.AnalysisServices.Partition> em <xref:Microsoft.AnalysisServices>.  
  
###  <a name="AggregationDesign"></a>Objetos AggregationDesign  
 Os designs de agregação são criados por meio do método AggregationDesign a partir de um objeto <xref:Microsoft.AnalysisServices.AggregationDesign>.  
  
 Para obter mais informações sobre os métodos e as propriedades disponíveis, consulte <xref:Microsoft.AnalysisServices.AggregationDesign> em <xref:Microsoft.AnalysisServices>.  
  
###  <a name="Aggregation"></a>Objetos de agregação  
 Um objeto <xref:Microsoft.AnalysisServices.Aggregation> é criado ao ser adicionado à coleção de designs de agregação do grupo de medidas pai, seguido pela atualização do objeto do grupo de medidas pai no servidor por meio do método Update. Uma agregação é removida de <xref:Microsoft.AnalysisServices.AggregationCollection> usando o método Remove ou o método RemoveAt.  
  
 Para obter mais informações sobre os métodos e as propriedades disponíveis, consulte <xref:Microsoft.AnalysisServices.Aggregation> em <xref:Microsoft.AnalysisServices>.  
  
## <a name="advanced-classes"></a>Classes avançadas  
 As classes avançadas oferecem funcionalidade OLAP além da criação e da navegação de um cubo. A seguir, algumas das classes avançadas e os benefícios oferecidos por elas:  
  
-   As classes de ação são usadas para criar uma resposta ativa durante a navegação em certas áreas do cubo.  
  
-   Os KPIs (Indicadores Chave de Desempenho) permitem a análise de comparação entre valores de dados.  
  
-   As perspectivas oferece exibições selecionadas de um único cubo, de forma que os usuários possam se concentrar no que é importante para eles.  
  
-   As traduções permitem que o cubo seja personalizado de acordo com a localidade do usuário.  
  
-   As classes de cache pró-ativo podem fornecer um equilíbrio entre o bom desempenho do armazenamento MOLAP e a instantaneidade do armazenamento ROLAP e oferecem processamento de partição agendado.  
  
 O AMO é usado para criar as definições para esse comportamento avançado, mas a experiência real será definida pelo cliente de navegação que implementa todos esses aprimoramentos.  
  
###  <a name="Action"></a>Objetos de ação  
 Um objeto <xref:Microsoft.AnalysisServices.Action> é criado ao ser adicionado à coleção de ações do cubo, seguido pela atualização do objeto de <xref:Microsoft.AnalysisServices.Cube> no servidor por meio do método Update. O método Update do cubo pode incluir o parâmetro UpdateOptions.ExpandFull, que garante que todos os objetos do cubo modificados sejam atualizados no servidor por meio dessa ação de atualização.  
  
 Para remover um <xref:Microsoft.AnalysisServices.Action> do objeto, ele deve ser removido da coleção e o cubo pai deve ser atualizado.  
  
 Um cubo deve ser atualizado e processado antes que a ação possa ser usada a partir do cliente.  
  
 Para obter mais informações sobre os métodos e as propriedades disponíveis, consulte <xref:Microsoft.AnalysisServices.Action> em <xref:Microsoft.AnalysisServices>.  
  
###  <a name="KPI"></a>Objetos KPI  
 Um objeto <xref:Microsoft.AnalysisServices.Kpi> é criado ao ser adicionado à coleção de KPIs do cubo, seguido pela atualização do objeto de <xref:Microsoft.AnalysisServices.Cube> no servidor por meio do método Update. O método Update do cubo pode incluir o parâmetro UpdateOptions.ExpandFull, que garante que todos os objetos do cubo modificados sejam atualizados no servidor por meio dessa ação de atualização.  
  
 Para remover um <xref:Microsoft.AnalysisServices.Kpi> do objeto, ele deve ser removido da coleção, em seguida, e o cubo pai deve ser atualizado.  
  
 Um cubo deve ser atualizado e processado antes que o KPI possa ser usado.  
  
 Para obter mais informações sobre os métodos e as propriedades disponíveis, consulte <xref:Microsoft.AnalysisServices.Kpi> em <xref:Microsoft.AnalysisServices>.  
  
###  <a name="Perspective"></a>Objetos de perspectiva  
 Um objeto <xref:Microsoft.AnalysisServices.Perspective> é criado ao ser adicionado à coleção de perspectivas do cubo, seguido pela atualização do objeto <xref:Microsoft.AnalysisServices.Cube> no servidor por meio do método Update. O método Update do cubo pode incluir o parâmetro UpdateOptions.ExpandFull, que garante que todos os objetos do cubo modificados sejam atualizados no servidor por meio dessa ação de atualização.  
  
 Para remover um objeto <xref:Microsoft.AnalysisServices.Perspective>, ele deverá ser removido da coleção e o cubo pai deverá ser atualizado.  
  
 Um cubo tem que ser atualizado e processado antes que a perspectiva possa ser usada.  
  
 Para obter mais informações sobre os métodos e as propriedades disponíveis, consulte <xref:Microsoft.AnalysisServices.Perspective> em <xref:Microsoft.AnalysisServices>.  
  
###  <a name="Translation"></a>Objetos de tradução  
 Um objeto <xref:Microsoft.AnalysisServices.Translation> é criado ao ser adicionado à coleção de traduções do objeto desejado, seguido pela atualização do objeto pai principal mais próximo no servidor por meio do método Update. O método Update do objeto pai mais próximo pode incluir o parâmetro UpdateOptions.ExpandFull, que garante que todos os objetos filhos modificados sejam atualizados no servidor por meio dessa ação de atualização.  
  
 Para remover um objeto <xref:Microsoft.AnalysisServices.Translation>, ele deverá ser removido da coleção e o objeto pai mais próximo deverá ser atualizado.  
  
 Para obter mais informações sobre os métodos e as propriedades disponíveis, consulte <xref:Microsoft.AnalysisServices.Translation> em <xref:Microsoft.AnalysisServices>.  
  
###  <a name="ProactiveCaching"></a>Objetos ProactiveCaching  
 Um objeto <xref:Microsoft.AnalysisServices.ProactiveCaching> é criado ao ser adicionado à coleção de objetos de cache pró-ativo da dimensão ou da partição, seguido pela atualização do objeto da dimensão ou da partição no servidor por meio do método Update.  
  
 Para remover um objeto <xref:Microsoft.AnalysisServices.ProactiveCaching>, ele deverá ser removido da coleção e o objeto pai deverá ser atualizado.  
  
 Uma dimensão ou partição deve ser atualizada e processada antes que o cache pró-ativo seja habilitado e esteja pronto para ser usado.  
  
 Para obter mais informações sobre os métodos e as propriedades disponíveis, consulte <xref:Microsoft.AnalysisServices.ProactiveCaching> em <xref:Microsoft.AnalysisServices>.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.AnalysisServices>   
 [Introdução às Classes AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [Programando objetos OLAP AMO básicos](../../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-olap-basic-objects.md)   
 [Objetos de programação AMO OLAP avançados](../../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-olap-advanced-objects.md)   
 [Arquitetura lógica &#40; Analysis Services - dados multidimensionais &#41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Objetos de banco de dados &#40; Analysis Services - dados multidimensionais &#41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  

