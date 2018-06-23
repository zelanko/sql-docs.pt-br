---
title: Classes de mineração de dados AMO | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data mining [AMO]
- AMO, data mining
- Analysis Management Objects, data mining
ms.assetid: e4108825-b722-417c-9647-ab30ce35e549
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 091d68fedffc16d57834a02cfcbd8ef3a6c2d087
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119220"
---
# <a name="amo-data-mining-classes"></a>Classes de mineração de dados AMO
  As classes de mineração de dados ajudam você a criar, modificar, excluir e processar objetos de mineração de dados. O trabalho com objetos de mineração de dados inclui a criação de estruturas de mineração de dados, a criação de modelos de mineração de dados e o processamento dos modelos.  
  
 Para obter mais informações sobre como configurar o ambiente e sobre <xref:Microsoft.AnalysisServices.Server>, <xref:Microsoft.AnalysisServices.Database>, <xref:Microsoft.AnalysisServices.DataSource>, e <xref:Microsoft.AnalysisServices.DataSourceView> objetos, consulte [as Classes fundamentais AMO](amo-fundamental-classes.md).  
  
 A definição de objetos no AMO (Objetos de Gerenciamento de Análise) exige a definição de várias propriedades em cada objeto para a configuração do contexto correto. Os objetos complexos, como os objetos OLAP e de mineração de dados, exigem uma codificação longa e detalhada.  
  
  
 A ilustração a seguir mostra o relacionamento das classes explicadas neste tópico.  
  
 ![Classes DataMining AMO](../../../analysis-services/dev-guide/media/amo-dataminingclasses.gif "Classes DataMining AMO")  
  
##  <a name="MiningStructure"></a> Objetos MiningStructure  
 Uma estrutura de mineração é o contêiner para modelos de mineração. A estrutura define todas as colunas possíveis que os modelos de mineração podem usar. Cada modelo de mineração define suas próprias colunas a partir do conjunto de colunas definidas na estrutura.  
  
 Um objeto simples <xref:Microsoft.AnalysisServices.MiningStructure> é composto de: informações básicas, uma exibição da fonte de dados, um ou mais <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>, nenhum ou mais <xref:Microsoft.AnalysisServices.TableMiningStructureColumn> e um <xref:Microsoft.AnalysisServices.MiningModelCollection>.  
  
 As informações básicas incluem o nome e o ID (identificador interno) do objeto <xref:Microsoft.AnalysisServices.MiningStructure>.  
  
 O objeto <xref:Microsoft.AnalysisServices.DataSourceView> armazena o modelo de dados subjacente para a estrutura de mineração.  
  
 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn> são colunas ou atributos com valores únicos.  
  
 <xref:Microsoft.AnalysisServices.TableMiningStructureColumn> são colunas ou atributos com diversos valores para cada caso.  
  
 <xref:Microsoft.AnalysisServices.MiningModelCollection> contém todos os modelos de mineração criados a partir dos mesmos dados.  
  
 Um objeto <xref:Microsoft.AnalysisServices.MiningStructure> é criado ao ser adicionado a <xref:Microsoft.AnalysisServices.MiningStructureCollection> do banco de dados e pela atualização do objeto de <xref:Microsoft.AnalysisServices.MiningStructure> no servidor por meio do método Update.  
  
 Para remover um objeto <xref:Microsoft.AnalysisServices.MiningStructure>, ele deverá ser descartado por meio do método Drop do objeto <xref:Microsoft.AnalysisServices.MiningStructure>. A remoção de um objeto <xref:Microsoft.AnalysisServices.MiningStructure> da coleção não afetará o servidor.  
  
 <xref:Microsoft.AnalysisServices.MiningStructure> pode ser processado por seu próprio método de acesso, ou pode ser processado quando um objeto pai processa a si mesmo usando seu próprio método de processamento.  
  
### <a name="columns"></a>Colunas  
 As colunas armazenam os dados para o modelo e podem ser de tipos diferentes, dependendo do uso: Key, Input, Predictable ou InputPredictable. As colunas previsíveis são o destino da criação do modelo de mineração.  
  
 As colunas de valor único são conhecidas como <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn> no AMO. As colunas de diversos valores são conhecidas como <xref:Microsoft.AnalysisServices.TableMiningStructureColumn>.  
  
#### <a name="scalarminingstructurecolumn"></a>ScalarMiningStructureColumn  
 Um objeto simples <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn> é composto de informações básicas, tipo, conteúdo e associação de dados.  
  
 As informações básicas incluem o nome e o ID (identificador interno) de <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>.  
  
 O tipo é o tipo de dados do valor: LONG, BOOLEAN, TEXT, DOUBLE, DATE.  
  
 O conteúdo diz ao mecanismo como a coluna pode ser modelada. Os valores podem ser: Discrete, Continuous, Discretized, Ordered, Cyclical, Probability, Variance, StdDev, ProbabilityVariance, ProbabilityStdDev, Support, Key.  
  
 A associação de dados é a vinculação da coluna de mineração de dados com o modelo de dados subjacente usando um elemento de exibição da fonte de dados.  
  
 Um <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn> é criado ao ser adicionado ao <xref:Microsoft.AnalysisServices.MiningStructureCollection> pai e pela atualização do objeto <xref:Microsoft.AnalysisServices.MiningStructure> pai no servidor por meio do método Update.  
  
 Para remover um <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>, ele deve ser removido da coleção do pai <xref:Microsoft.AnalysisServices.MiningStructure>e o pai <xref:Microsoft.AnalysisServices.MiningStructure> objeto deve ser atualizado para o servidor usando o método de atualização.  
  
#### <a name="tableminingstructurecolumn"></a>TableMiningStructureColumn  
 Um objeto simples <xref:Microsoft.AnalysisServices.TableMiningStructureColumn> é composto de informações básicas e de colunas escalares.  
  
 As informações básicas incluem o nome e o ID (identificador interno) de <xref:Microsoft.AnalysisServices.TableMiningStructureColumn>.  
  
 As colunas escalares são <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>.  
  
 Um <xref:Microsoft.AnalysisServices.TableMiningStructureColumn> é criado ao ser adicionado à coleção <xref:Microsoft.AnalysisServices.MiningStructure> pai e pela atualização do objeto <xref:Microsoft.AnalysisServices.TableMiningStructureColumn> pai no servidor por meio do método Update.  
  
 Para remover um <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>, ele terá de ser removido da coleção do <xref:Microsoft.AnalysisServices.MiningStructure> pai e o objeto <xref:Microsoft.AnalysisServices.MiningStructure> pai terá de ser atualizado no servidor por meio do método Update.  
  
##  <a name="MiningModel"></a> Objetos MiningModel  
 Um <xref:Microsoft.AnalysisServices.MiningModel> é o objeto que permite a você escolher que colunas da estrutura serão usadas, quais serão os algoritmos usados e, opcionalmente, especificar parâmetros para ajustar o modelo. Por exemplo, talvez você queira definir vários modelos de mineração na mesma estrutura de mineração que usa os mesmos algoritmos, mas para ignorar algumas colunas da estrutura de mineração de um modelo, use-as como entradas em outro modelo e use-as como entrada e faça a previsão de um terceiro modelo. Isso pode ser útil se você quiser tratar uma coluna como contínua em um modelo de mineração, mas como diferenciada em outro.  
  
 Um objeto simples <xref:Microsoft.AnalysisServices.MiningModel> é composto de: informações básicas, definição de algoritmo e colunas.  
  
 As informações básicas incluem o nome e o ID (identificador interno) do modelo de mineração.  
  
 Uma definição de algoritmo se refere a qualquer um dos algoritmos padrão fornecidos pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ou a qualquer algoritmo personalizado habilitado no servidor.  
  
 As colunas são uma coleção das colunas usadas pelo algoritmo e sua definição de uso.  
  
 Um <xref:Microsoft.AnalysisServices.MiningModel> é criado ao ser adicionado a <xref:Microsoft.AnalysisServices.MiningModelCollection> do banco de dados e pela atualização do objeto de <xref:Microsoft.AnalysisServices.MiningModel> no servidor por meio do método Update.  
  
 Para remover um <xref:Microsoft.AnalysisServices.MiningModel>, ele terá de ser descartado por meio do método Drop de <xref:Microsoft.AnalysisServices.MiningModel>. A remoção de um <xref:Microsoft.AnalysisServices.MiningModel> da coleção não afetará o servidor.  
  
 Depois de criado, um <xref:Microsoft.AnalysisServices.MiningModel> poderá ser processado por meio de seu próprio método de processamento, ou poderá ser processado quando um objeto pai processar a si mesmo com seu próprio método de processamento.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.AnalysisServices>   
 [Classes fundamentais AMO](amo-fundamental-classes.md)   
 [Programando objetos de mineração de dados AMO](programming-amo-data-mining-objects.md)   
 [Introdução às Classes AMO](amo-classes-introduction.md)   
 [Arquitetura lógica &#40; Analysis Services - dados multidimensionais &#41;](../olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Objetos de banco de dados &#40; Analysis Services - dados multidimensionais &#41;](../olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  