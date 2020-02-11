---
title: Criando agregações (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- statistical information [XML for Analysis]
- batches [XML for Analysis]
- aggregations [Analysis Services], XML for Analysis
- XMLA, aggregations
- queries [XMLA]
- XML for Analysis, aggregations
- iterative aggregation process [XMLA]
ms.assetid: 4dd27afa-10c7-408d-bc24-ca74217ddbcb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 81450789395dfef84f81896990fa251514d3489e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62702126"
---
# <a name="designing-aggregations-xmla"></a>Criando agregações (XMLA)
  Designs de agregação estão associados a partições de um determinado grupo de medidas para garantir que as partições usem a mesma estrutura ao armazenarem agregações. Usar a mesma estrutura de armazenamento para partições permite que você defina facilmente as partições que podem ser mescladas posteriormente usando o comando [MergePartitions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/mergepartitions-element-xmla) . Para obter mais informações sobre designs de agregação, consulte [agregações e designs de agregação](../multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md).  
  
 Para definir agregações para um design de agregação, você pode usar o comando [DesignAggregations](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/designaggregations-element-xmla) no XML for Analysis (XMLA). O comando `DesignAggregations` tem propriedades que identificam o design de agregação a ser usado como referência e mostram como controlar o processo de design com base nessa referência. Usando o comando `DesignAggregations` e suas propriedades, você pode criar agregações iterativamente ou em lote e depois exibir as estatísticas do design resultante para avaliar o processo de design.  
  
## <a name="specifying-an-aggregation-design"></a>Especificando um design de agregação  
 A propriedade [Object](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) do `DesignAggregations` comando deve conter uma referência de objeto para um design de agregação existente. A referência de objeto contém um identificador de banco de dados, um identificador de cubo, um identificador de grupo de medidas e um identificador de design de agregação. Se o design de agregação ainda não existir, ocorrerá um erro.  
  
## <a name="controlling-the-design-process"></a>Controlando o processo de design  
 Você pode usar as seguintes propriedades do comando `DesignAggregations` para controlar o algoritmo usado na definição de agregações para o design de agregação:  
  
-   A propriedade [Steps](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/steps-element-xmla) determina quantas iterações `DesignAggregations` o comando deve executar antes de retornar o controle ao aplicativo cliente.  
  
-   A propriedade [time](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/time-element-xmla) determina quantos milissegundos o `DesignAggregations` comando deve levar antes de retornar o controle ao aplicativo cliente.  
  
-   A propriedade [Optimization](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/optimization-element-xmla) determina a porcentagem estimada de melhoria de `DesignAggregations` desempenho que o comando deve tentar alcançar. Se você estiver criando agregações iterativamente, só terá de enviar essa propriedade no primeiro comando.  
  
-   A propriedade de [armazenamento](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/storage-element-xmla) determina a quantidade estimada de armazenamento em disco, em bytes, `DesignAggregations` usada pelo comando. Se você estiver criando agregações iterativamente, só terá de enviar essa propriedade no primeiro comando.  
  
-   A propriedade [materializar](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/materialize-element-xmla) determina se `DesignAggregations` o comando deve criar as agregações definidas durante o processo de design. Se estiver criando agregações iterativamente, essa propriedade deve ser definida como falsa até que você esteja pronto para salvar as agregações criadas. Quando definida como verdadeira, o processo de design atual terminará e as agregações definidas serão adicionadas ao design de agregação especificado.  
  
## <a name="specifying-queries"></a>Especificando consultas  
 O comando DesignAggregations dá suporte ao comando de otimização com base no uso, `Query` incluindo um ou mais elementos na propriedade [queries](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/queries-element-xmla) . A `Queries` propriedade pode conter um ou mais elementos de [consulta](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/query-element-xmla) . Se a propriedade `Queries` não contiver elementos de `Query`, o design de agregação especificado no elemento de `Object` usará uma estrutura padrão com um conjunto geral de agregações. Esse conjunto geral de agregações é criado para atender aos critérios especificados nas propriedades `Optimization` e `Storage` do comando `DesignAggregations`.  
  
 Cada elemento `Query` representa uma meta de consulta usada pelo processo de design para definir agregações que se destinam às consultas usadas com mais frequência. Você pode especificar suas próprias consultas de meta ou pode usar as informações armazenadas por uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no log de consultas para recuperar informações sobre as consultas usadas com mais frequência. O Assistente de Otimização com Base no Uso usa o log de consultas para recuperar consultas de meta com base no tempo, no uso ou em um usuário especificado quando envia um comando `DesignAggregations`. Para obter mais informações, consulte [Ajuda F1 do assistente de otimização com base no uso](../usage-based-optimization-wizard-f1-help.md).  
  
 Se estiver projetando agregações de modo iterativo, você deve transmitir metas de consulta somente no primeiro comando `DesignAggregations` porque a instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] armazena essas metas e utiliza essas consultas durante comandos `DesignAggregations` subsequentes. Após transmitir as metas de consulta no primeiro comando `DesignAggregations` de um processo iterativo, qualquer comando `DesignAggregations` subsequente que contém metas de consulta na propriedade `Queries` gerará um erro.  
  
 O elemento `Query` contém um valor delimitado por vírgula com os seguintes argumentos:  
  
 *Frequency*,*DataSet*[,*DataSet*...]  
  
 *Frequência*  
 Um fator de ponderação que corresponde ao número de vezes que a consulta foi executada previamente. Se o `Query` elemento representa uma nova consulta, o valor de *Frequency* representa o fator de ponderação usado pelo processo de design para avaliar a consulta. À medida que o valor de frequência fica maior, o peso colocado na consulta durante processo de design aumenta.  
  
 *DataSet*  
 Uma sequência numérica que especifica quais atributos de uma dimensão devem ser incluídos na consulta. Essa sequência deve ter o mesmo número de caracteres do número de atributos na dimensão. Zero (0) indica que o atributo na posição ordinal especificada não está incluído na consulta para a dimensão especificada e um (1) indica que o atributo na posição ordinal especificada está incluído na consulta para a dimensão especificada.  
  
 Por exemplo, a sequência “011” faz referência a uma consulta que envolve uma dimensão com três atributos, dos quais o segundo e o terceiro estão incluídos na consulta.  
  
> [!NOTE]  
>  Alguns atributos não são considerados no conjunto de dados. Para obter mais informações sobre atributos excluídos, consulte [elemento Query &#40;&#41;XMLA ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/query-element-xmla).  
  
 Cada dimensão no grupo de medidas que contém o design de agregação é representada ** por um valor de `Query` conjunto de valores no elemento. A ordem de valores *Dataset* deve coincidir com a ordem de dimensões incluída no grupo de medidas.  
  
## <a name="designing-aggregations-using-iterative-or-batch-processes"></a>Criando agregações usando processos iterativos ou em lote  
 Você pode usar o comando `DesignAggregations` como parte de um processo iterativo ou de um processo em lote, dependendo da interatividade exigida pelo processo de design.  
  
### <a name="designing-aggregations-using-an-iterative-process"></a>Criando agregações usando um processo iterativo  
 Para criar agregações de design de forma iterativa, envie diversos comandos `DesignAggregations` para oferecer um controle refinado sobre o processo de design. O Assistente de Design de Agregação usa essa mesma abordagem para fornecer controle refinado sobre o processo de design. Para obter mais informações, consulte [Ajuda F1 do assistente de design de agregação](../aggregation-design-wizard-f1-help.md).  
  
> [!NOTE]  
>  Uma sessão explícita é necessária para a criação iterativa de agregações. Para obter mais informações sobre sessões explícitas, consulte [Managing Connections and sessions &#40;XMLA&#41;](managing-connections-and-sessions-xmla.md).  
  
 Para iniciar o processo iterativo, primeiro envie um comando `DesignAggregations` com as seguintes informações:  
  
-   Os valores das propriedades `Storage` e `Optimization` para os quais todo o processo de design é destinado.  
  
-   Os valores das propriedades `Steps` e `Time` aos quais a primeira etapa do processo de design se limita.  
  
-   Se você quiser otimização baseada em uso, a propriedade `Queries` que contém as consultas de meta para as quais todo o processo de design é destinado.  
  
-   A propriedade `Materialize` definida como falsa. A definição dessa propriedade como falsa indica que o processo de design não salvará as agregações definidas no design de agregação quando o comando for concluído.  
  
 Quando o primeiro comando `DesignAggregations` termina, retorna um conjunto de linhas com as estatísticas de design. Você pode avaliar essas estatísticas de design para determinar se o processo de design deve continuar ou se ele foi concluído. Se o processo tiver de continuar, envie outro comando `DesignAggregations` com os valores `Steps` e `Time` aos quais esta etapa do processo de design se limita. Avalie as estatísticas resultantes e determine se o processo de design deve continuar. Esse processo iterativo de enviar comandos `DesignAggregations` e de avaliar os resultados continuará até que você atinja suas metas e tenha um conjunto apropriado de agregações definido.  
  
 Depois de obter o conjunto de agregações desejado, envie um comando `DesignAggregations` final. Esse comando `DesignAggregations` final deve ter sua propriedade `Steps` definida como 1 e sua propriedade `Materialize` definida como verdadeira. Usando essas configurações, esse comando `DesignAggregations` final completa o processo de design e salva a agregação definida para o design de agregação.  
  
### <a name="designing-aggregations-using-a-batch-process"></a>Criando agregações usando um processo em lote  
 Você também pode criar agregações em um processo em lote ao enviar um único comando `DesignAggregations` com os valores das propriedades `Steps`, `Time`, `Storage` e `Optimization` aos quais todo o processo de design se destina e está limitado. Se você quiser otimização fundada em uso, as consultas de meta as quais o processo de design se destina também deverão ser incluídas na propriedade `Queries`. Além disso, verifique se a propriedade `Materialize` foi definida como verdadeira, para que o processo de design salve as agregações definidas para o design de agregação quando o comando terminar.  
  
 Você pode criar agregações usando um processo em lote em uma sessão implícita ou em uma sessão explícita. Para obter mais informações sobre sessões implícitas e explícitas, consulte [Managing Connections and sessions &#40;XMLA&#41;](managing-connections-and-sessions-xmla.md).  
  
## <a name="returning-design-statistics"></a>Retornando estatísticas de design  
 Quando o comando `DesignAggregations` devolve o controle ao aplicativo cliente, retorna um conjunto de linhas com uma única linha, que representa as suas estatísticas de design. O conjunto de linhas contém as colunas listadas na tabela a seguir.  
  
|Coluna|Tipo de dados|DESCRIÇÃO|  
|------------|---------------|-----------------|  
|Etapas|Integer|O número de etapas executadas pelo comando antes que ele devolva o controle ao aplicativo cliente.|  
|Hora|Long integer|O número de milissegundos que o comando leva antes de devolver o controle ao aplicativo cliente.|  
|Otimização|DOUBLE|A porcentagem estimada de aperfeiçoamento de desempenho atingida pelo comando antes de devolver o controle ao aplicativo cliente.|  
|Armazenamento|Long integer|O número estimado de bytes que o comando leva antes de devolver o controle ao aplicativo cliente.|  
|Agregações|Long integer|O número de agregações definido pelo comando antes de devolver o controle ao aplicativo cliente.|  
|LastStep|Boolean|Indica se os dados do conjunto de linhas representam a última etapa no processo de design. Se a propriedade `Materialize` do comando foi definida como verdadeira, o valor dessa coluna será definido como true.|  
  
 Você pode usar as estatísticas de design contidas no conjunto de linhas retornadas depois de cada comando `DesignAggregations` no design iterativo e no design em lote. No design iterativo, você pode usar as estatísticas de design para determinar e exibir o andamento. Quando estiver criando agregações em lote, poderá usar as estatísticas de design para determinar o número de agregações criadas pelo comando.  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolvendo com XMLA no Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
