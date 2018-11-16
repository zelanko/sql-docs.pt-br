---
title: Transformação Amostragem de Linhas | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.rowsamplingtrans.f1
- sql13.DTS.DESIGNER.ROWSAMPLINGTRANSFORMATION.COLUMNS.F1
- sql13.dts.designer.rowsamplingtransformation.f1
helpviewer_keywords:
- sampling seeds [Integration Services]
- random seeds
- random sampling
- sample data sets [Integration Services]
- Row Sampling transformation
- packages [Integration Services], samples
- datasets [Integration Services], sample
ms.assetid: b6caafd3-30b2-4368-82af-a44611d4cd39
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 60c2615cf141f145f2353df5309105b0ed535fc1
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/14/2018
ms.locfileid: "51641263"
---
# <a name="row-sampling-transformation"></a>Transformação Amostragem de Linhas
  A transformação Amostragem de Linhas é usada para obter um subconjunto selecionado aleatoriamente de um conjunto de dados de entrada. Você pode especificar o tamanho exato da amostra de saída e especificar uma semente para o gerador de números aleatórios.  
  
 Há muitos aplicativos para amostragem aleatória. Por exemplo, uma empresa que deseje selecionar 50 empregados aleatoriamente para receber prêmios em uma loteria poderia usar a transformação Amostragem de Linhas no banco de dados de empregados para gerar o número exato de vencedores.  
  
 A transformação Amostragem de Linhas também é útil durante o desenvolvimento de pacote para criar um conjunto de dados pequeno, mas representativo. Você pode testar a execução de pacote e transformação de dados com dados altamente representativos, porém mais rapidamente, porque uma amostra aleatória é usada em vez do conjunto de dados completo. Como o conjunto de dados de exemplo usado pelo pacote de teste é sempre do mesmo tamanho, o uso do subconjunto de exemplos também facilita a identificação de problemas de desempenho no pacote.  
  
 Essa transformação é semelhante à transformação Amostragem Percentual, que cria um exemplo de conjunto dados selecionando uma porcentagem de linhas de entrada. Consulte [Transformação Amostragem Percentual](../../../integration-services/data-flow/transformations/percentage-sampling-transformation.md).  
  
## <a name="configuring-the-row-sampling-transformation"></a>Configurando a transformação Amostragem de Linhas  
 A transformação Amostragem de Linhas cria um exemplo de conjunto de dados selecionando um número especificado de linhas de entrada de transformação. Como a seleção de linhas da entrada de transformação é aleatória, o exemplo resultante da entrada é representativo. Você também pode especificar a semente que será usada pelo gerador de números aleatórios para afetar a maneira como a transformação selecionará as linhas.  
  
 O uso da mesma semente aleatória na mesma entrada de transformação sempre cria a mesma saída de exemplo. Se nenhuma semente for especificada, a transformação usará a contagem de tiques do sistema operacional para criar o número aleatório. Portanto, você poderia usar a mesma semente durante o teste para verificar os resultados da transformação durante o desenvolvimento e teste do pacote e, em seguida, alterar para uma semente aleatória quando o pacote for colocado em produção.  
  
 A transformação Amostragem de Linha inclui a propriedade personalizada **SamplingValue** . Essa propriedade pode ser atualizada por uma expressão de propriedade quando o pacote é carregado. Para obter mais informações, consulte [Expressões do Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Usar expressões de propriedade em pacotes](../../../integration-services/expressions/use-property-expressions-in-packages.md) e [Propriedades personalizadas da transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Essa transformação tem uma entrada e duas saídas. Não tem nenhuma saída de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas de Transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Para obter mais informações sobre como definir propriedades, consulte.  
  
## <a name="row-sampling-transformation-editor-sampling-page"></a>Editor de Transformação Amostragem de Linhas (página Amostragem)
  Use a caixa de diálogo **Editor de Transformação Amostragem de Linhas** para dividir uma parte de uma entrada em uma amostra usando um número de linhas especificado. Essa transformação divide a entrada em duas saídas separadas.  
  
### <a name="options"></a>Opções  
 **Número de linhas**  
 Especifique o número de linhas da entrada a serem usadas como amostra.  
  
 O valor dessa propriedade pode ser especificado com uma expressão de propriedades.  
  
 **Nome de saída do exemplo**  
 Forneça um nome exclusivo para a saída que incluirá as linhas de amostra. O nome fornecido será exibido no Designer SSIS.  
  
 **Nome de saída não selecionado**  
 Forneça um nome exclusivo para a saída que conterá as linhas excluídas da amostragem. O nome fornecido será exibido no Designer SSIS.  
  
 **Usar a seguinte semente aleatória**  
 Especifique a semente de amostra para o gerador de números aleatórios que a transformação usa para criar uma amostra. Recomendado apenas para desenvolvimento e teste. A transformação usará a contagem de tiques do Microsoft Windows como semente se não for especificada uma semente aleatória.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
  
