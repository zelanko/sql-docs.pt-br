---
title: Criando agregações (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b9f681b3c99bd0e8351a844f28b16be6249de199
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63288499"
---
# <a name="designing-aggregations-xmla"></a>Criando agregações (XMLA)
  Designs de agregação estão associados a partições de um determinado grupo de medidas para garantir que as partições usem a mesma estrutura ao armazenarem agregações. Usando a mesma estrutura de armazenamento para partições permite que você defina com facilidade partições que podem ser mescladas posteriormente usando o [MergePartitions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/mergepartitions-element-xmla) comando. Para obter mais informações sobre designs de agregação, consulte [agregações e Designs de agregação](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md).  
  
 Para definir agregações para um design de agregação, você pode usar o [DesignAggregations](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/designaggregations-element-xmla) no XML for Analysis (XMLA). O **DesignAggregations** comando tem propriedades que identificam o design de agregação a ser usado como uma referência e como controlar o processo de design com base nessa referência. Usando o **DesignAggregations** comando e suas propriedades, você pode criar agregações iterativamente ou em lote e, em seguida, exibir as estatísticas de design resultante para avaliar o processo de design.  
  
## <a name="specifying-an-aggregation-design"></a>Especificando um design de agregação  
 O [objeto](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) propriedade da **DesignAggregations** comando deve conter uma referência de objeto para um design de agregação existente. A referência de objeto contém um identificador de banco de dados, um identificador de cubo, um identificador de grupo de medidas e um identificador de design de agregação. Se o design de agregação ainda não existir, ocorrerá um erro.  
  
## <a name="controlling-the-design-process"></a>Controlando o processo de design  
 Você pode usar as seguintes propriedades do **DesignAggregations** comando para controlar o algoritmo usado para definir agregações para o design de agregação:  
  
-   O [etapas](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/steps-element-xmla) propriedade determina quantas iterações a **DesignAggregations** comando deve executar antes de devolver o controle ao aplicativo cliente.  
  
-   O [tempo](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/time-element-xmla) propriedade determina quantos milissegundos o **DesignAggregations** comando deve executar antes de devolver o controle ao aplicativo cliente.  
  
-   O [otimização](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/optimization-element-xmla) propriedade determina a porcentagem estimada de aperfeiçoamento de desempenho a **DesignAggregations** comando deve tentar alcançar. Se você estiver criando agregações iterativamente, só terá de enviar essa propriedade no primeiro comando.  
  
-   O [armazenamento](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/storage-element-xmla) propriedade determina a quantidade estimada de armazenamento em disco, em bytes, usada pelo **DesignAggregations** comando. Se você estiver criando agregações iterativamente, só terá de enviar essa propriedade no primeiro comando.  
  
-   O [materializar](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/materialize-element-xmla) propriedade determina se o **DesignAggregations** comando deve criar as agregações definidas durante o processo de design. Se estiver criando agregações iterativamente, essa propriedade deve ser definida como falsa até que você esteja pronto para salvar as agregações criadas. Quando definida como verdadeira, o processo de design atual terminará e as agregações definidas serão adicionadas ao design de agregação especificado.  
  
## <a name="specifying-queries"></a>Especificando consultas  
 O comando DesignAggregations dá suporte ao comando de otimização com base no uso, incluindo um ou mais **consulta** elementos na [consultas](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/queries-element-xmla) propriedade. O **consultas** propriedade pode conter um ou mais [consulta](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/query-element-xmla) elementos. Se o **consultas** propriedade não contém nenhum **consulta** elementos, o design de agregação especificado no **objeto** elemento usa uma estrutura padrão que contém um conjunto geral de agregações. Esse conjunto geral de agregações foi projetado para atender aos critérios especificados na **otimização** e **armazenamento** propriedades do **DesignAggregations** comando.  
  
 Cada elemento **Query** representa uma meta de consulta usada pelo processo de design para definir agregações que se destinam às consultas usadas com mais frequência. Você pode especificar suas próprias metas ou usar as informações armazenadas por uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no log de consultas para recuperar informações sobre as consultas usadas com mais frequência. O Assistente de otimização com base no uso usa o log de consulta para recuperar as metas de consulta com base no tempo, uso ou um usuário especificado quando envia um **DesignAggregations** comando. Para obter mais informações, consulte [ajuda de F1 do Assistente de otimização com base no uso](http://msdn.microsoft.com/library/e5f5a938-ae7c-4f4e-9416-a7f94ac82763).  
  
 Se estiver projetando agregações de modo iterativo, você deve transmitir metas de consulta somente no primeiro comando **DesignAggregations** porque a instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] armazena essas metas e utiliza essas consultas durante comandos **DesignAggregations** subsequentes. Após transmitir as metas de consulta no primeiro comando **DesignAggregations** de um processo iterativo, qualquer comando **DesignAggregations** subsequente que contém metas de consulta na propriedade **Queries** gerará um erro.  
  
 O elemento **Query** contém um valor delimitado por vírgula com os seguintes argumentos:  
  
 *Frequency*,*Dataset*[,*Dataset*...]  
  
 *Frequência*  
 Um fator de ponderação que corresponde ao número de vezes que a consulta foi executada previamente. Se o elemento **Query** representa uma nova consulta, o valor *Frequency* representa o fator de ponderação usado pelo processo de design para avaliar a consulta. À medida que o valor de frequência fica maior, o peso colocado na consulta durante processo de design aumenta.  
  
 *Conjunto de dados*  
 Uma sequência numérica que especifica quais atributos de uma dimensão devem ser incluídos na consulta. Essa sequência deve ter o mesmo número de caracteres do número de atributos na dimensão. Zero (0) indica que o atributo na posição ordinal especificada não está incluído na consulta para a dimensão especificada e um (1) indica que o atributo na posição ordinal especificada está incluído na consulta para a dimensão especificada.  
  
 Por exemplo, a sequência “011” faz referência a uma consulta que envolve uma dimensão com três atributos, dos quais o segundo e o terceiro estão incluídos na consulta.  
  
> [!NOTE]  
>  Alguns atributos não são considerados no conjunto de dados. Para obter mais informações sobre os atributos excluídos, consulte [elemento Query &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/query-element-xmla).  
  
 Cada dimensão no grupo de medidas que contém o design de agregação é representado por um valor *Dataset* no elemento **Query** . A ordem de valores *Dataset* deve coincidir com a ordem de dimensões incluída no grupo de medidas.  
  
## <a name="designing-aggregations-using-iterative-or-batch-processes"></a>Criando agregações usando processos iterativos ou em lote  
 Você pode usar o **DesignAggregations** comando como parte de um processo iterativo ou um processo em lote, dependendo da interatividade exigida pelo processo de design.  
  
### <a name="designing-aggregations-using-an-iterative-process"></a>Criando agregações usando um processo iterativo  
 Para agregações de design iterativamente, enviar várias **DesignAggregations** comandos para fornecer controle refinado sobre o processo de design. O Assistente de Design de Agregação usa essa mesma abordagem para fornecer controle refinado sobre o processo de design. Para obter mais informações, consulte [ajuda de F1 do Assistente de Design de agregação](http://msdn.microsoft.com/library/39e23cf1-6405-4fb6-bc14-ba103314362d).  
  
> [!NOTE]  
>  Uma sessão explícita é necessária para a criação iterativa de agregações. Para obter mais informações sobre sessões explícitas, consulte [Gerenciando conexões e sessões &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md).  
  
 Para iniciar o processo iterativo, você deve enviar para um **DesignAggregations** comando que contém as seguintes informações:  
  
-   O **armazenamento** e **otimização** valores de propriedade que o processo de design inteira é destinado.  
  
-   O **etapas** e **tempo** valores de propriedade em que a primeira etapa do processo de design é limitada.  
  
-   Se você quiser otimização baseada em uso, o **consultas** consultas de propriedade que contém a meta que o processo de design inteira é destinado.  
  
-   O **materializar** propriedade definida como false. A definição dessa propriedade como falsa indica que o processo de design não salvará as agregações definidas no design de agregação quando o comando for concluído.  
  
 Quando a primeira **DesignAggregations** comando terminar, o comando retorna um conjunto de linhas que contém estatísticas de design. Você pode avaliar essas estatísticas de design para determinar se o processo de design deve continuar ou se ele foi concluído. Se o processo deve continuar, em seguida, envie outro **DesignAggregations** comando que contém o **etapas** e **tempo** valores com o qual processar esta etapa do design é limitado. Avalie as estatísticas resultantes e determine se o processo de design deve continuar. Esse processo iterativo de envio **DesignAggregations** comandos e avaliar os resultados continuará até que você atinja suas metas e tenha um conjunto apropriado de agregações definido.  
  
 Depois de ter atingido o conjunto de agregações que você deseja, você envia um final **DesignAggregations** comando. Esse último **DesignAggregations** comando deve ter seu **etapas** propriedade definida como 1 e sua **materializar** propriedade definida como verdadeira. Usando essas configurações, finais nesse **DesignAggregations** comando conclui o processo de design e salva a agregação definida para o design de agregação.  
  
### <a name="designing-aggregations-using-a-batch-process"></a>Criando agregações usando um processo em lote  
 Você também pode criar agregações em um processo em lote ao enviar um único **DesignAggregations** comando que contém o **etapas**, **tempo**, **armazenamento** , e **otimização** no qual o processo de design inteira é direcionado e limitado de valores de propriedade. Se você quiser otimização baseada em uso, as consultas de meta no qual o processo de design se destina também devem ser incluídas na **consultas** propriedade. Também verifique se o **materializar** propriedade é definida como true, para que o processo de design salve as agregações definidas para o design de agregação quando o comando for concluído.  
  
 Você pode criar agregações usando um processo em lote em uma sessão implícita ou em uma sessão explícita. Para obter mais informações sobre sessões implícitas e explícitas, consulte [Gerenciando conexões e sessões &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md).  
  
## <a name="returning-design-statistics"></a>Retornando estatísticas de design  
 Quando o **DesignAggregations** comando retorna o controle para o aplicativo cliente, o comando retorna um conjunto de linhas que contém uma única linha que representa as estatísticas de design para o comando. O conjunto de linhas contém as colunas listadas na tabela a seguir.  
  
|coluna|Data type|Descrição|  
|------------|---------------|-----------------|  
|Etapas|Integer|O número de etapas executadas pelo comando antes que ele devolva o controle ao aplicativo cliente.|  
|Hora|Long integer|O número de milissegundos que o comando leva antes de devolver o controle ao aplicativo cliente.|  
|Optimization|Double|A porcentagem estimada de aperfeiçoamento de desempenho atingida pelo comando antes de devolver o controle ao aplicativo cliente.|  
|Armazenamento|Long integer|O número estimado de bytes que o comando leva antes de devolver o controle ao aplicativo cliente.|  
|Agregações|Long integer|O número de agregações definido pelo comando antes de devolver o controle ao aplicativo cliente.|  
|LastStep|Booliano|Indica se os dados do conjunto de linhas representam a última etapa no processo de design. Se o **materializar** propriedade do comando foi definida como true, o valor desta coluna é definido como true.|  
  
 Você pode usar as estatísticas de design que estão contidas no conjunto de linhas retornado depois de cada **DesignAggregations** comando iterativo e design em lote. No design iterativo, você pode usar as estatísticas de design para determinar e exibir o andamento. Quando estiver criando agregações em lote, poderá usar as estatísticas de design para determinar o número de agregações criadas pelo comando.  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolvendo com XMLA no Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
