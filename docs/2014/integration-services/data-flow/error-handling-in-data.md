---
title: Tratamento de erro em dados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- truncating data
- data conversion errors [Integration Services]
- errors [Integration Services], data flow components
- lookups [Integration Services]
- errors [Integration Services]
- errors [Integration Services], data flow outputs
- error outputs [Integration Services]
- data flow [Integration Services], errors
- expressions [Integration Services], errors
ms.assetid: c61667b4-25cb-4d45-a52f-a733e32863f4
caps.latest.revision: 57
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 125bcb31a9edb23e4ffe3ba05cdc46227da33cac
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012730"
---
# <a name="error-handling-in-data"></a>Tratamento de erros em dados
  Quando um componente de fluxo de dados aplica uma transformação aos dados da coluna, extrai dados de fontes ou carrega dados nos destinos, podem ocorrer erros. Frequentemente, os erros ocorrem por causa de valores de dados inesperados. Por exemplo, uma conversão de dados falha porque uma coluna contém uma cadeia de caracteres em vez de um número, uma inserção em uma coluna de banco de dados falha porque os dados são uma data e a coluna tem um tipo de dados numéricos, ou uma expressão não é avaliada porque o valor de uma coluna é zero, resultando em uma operação matemática que não é válida.  
  
 Em geral, os erros se enquadram nas categorias a seguir:  
  
-   Erros de conversão de dados, que ocorrem se uma conversão resulta em perda de dígitos significativos, perda de dígitos insignificantes e truncamento de cadeias de caracteres. Os erros de conversão de dados também ocorrem se não houver suporte para a conversão solicitada.  
  
-   Erros de avaliação de expressão, que ocorrem se expressões avaliadas em tempo de execução realizarem operações inválidas ou se tornarem sintaticamente incorretas devido a valores de dados ausentes ou incorretos.  
  
-   Erros de pesquisa, que ocorrem se uma operação de pesquisa não conseguir localizar uma tabela de pesquisa correspondente.  
  
 Muitos componentes de fluxo de dados dão suporte a saídas de erro, que permitem controlar como o componente manipula erros no nível da linha, em dados de entrada e de saída. Para especificar como o componente se comporta quando ocorre um truncamento ou erro, defina as opções de colunas individuais na entrada ou saída. Por exemplo, você pode especificar que o componente deve falhar se os dados com o nome do cliente estão truncados, mas ignorar erros em outra coluna que contenha dados menos importantes.  
  
 A saída de erro pode ser conectada à entrada de outra transformação ou carregada em um destino diferente do que a saída de não erro. Por exemplo, a saída de erro pode estar conectada a uma transformação Coluna Derivada que fornece uma cadeia de caracteres para uma coluna que esteja em branco.  
  
 O diagrama a seguir mostra um fluxo de dados simples incluindo uma saída de erro.  
  
 ![Fluxo de dados com saída de erro](../media/mw-dts-11.gif "Fluxo de dados com saída de erro")  
  
 Além das colunas de dados, a saída de erro inclui as colunas **ErrorCode** e **ErrorColumn** . A coluna **ErrorCode** identifica o erro e a coluna **ErrorColumn** contém o identificador de linhagem da coluna de erro. Para exibir os metadados dessas colunas, clique no caminho que conecta a saída de erro ao próximo componente no fluxo de dados. Em algumas circunstâncias, o valor da coluna **ErrorColumn** é definido como zero. Isto acontece quando a condição de erro afeta a linha inteira em vez de uma única coluna. Um exemplo é quando uma pesquisa falha na transformação Pesquisa.  
  
 Para obter mais informações, consulte [Fluxo de Dados](data-flow.md) e [Caminhos do Integration Services](integration-services-paths.md).  
  
 Para obter uma lista de erros, avisos e outras mensagens do Integration Services, consulte [Referência de mensagens e erros do Integration Services](../integration-services-error-and-message-reference.md).  
  
## <a name="error-and-truncation-options"></a>Opções de erro e truncamento  
 Os erros fazem parte de uma de duas categorias: erros ou truncamentos. Um erro indica uma falha inequívoca e gera um resultado NULL. Esses erros podem incluir erros de conversão de dados ou erros de avaliação de expressão. Por exemplo, uma tentativa de converter uma cadeia de caracteres que contém caracteres alfabéticos em um número causa um erro. Conversões de dados, avaliações de expressão e atribuições de resultados de expressão para variáveis, propriedades e colunas de dados podem falhar por causa de lançamentos ilegais e tipos incompatíveis de dados. Para obter mais informações, consulte [Conversão &#40;Expressão SSIS&#41;](../expressions/cast-ssis-expression.md), [Tipos de dados do Integration Services em expressões](../expressions/integration-services-data-types-in-expressions.md) e [Tipos de dados do Integration Services](integration-services-data-types.md).  
  
 Um truncamento é menos grave que um erro. Um truncamento gera resultados que podem ser utilizáveis ou até mesmo desejáveis. Você pode optar por tratar truncamentos como erros ou como condições aceitáveis. Por exemplo, se você estiver inserindo uma cadeia de caracteres com 15 caracteres em uma coluna que só tem 1 caractere de comprimento, poderá optar por truncar a cadeia de caracteres.  
  
 Você pode configurar como fontes, transformações e destinos manipulam erros e truncamentos. A tabela a seguir descreve as opções.  
  
|Opção|Description|  
|------------|-----------------|  
|Falha no Componente|A tarefa Fluxo de Dados falha quando ocorre um erro ou um truncamento. Falha é a opção padrão para um erro e um truncamento.|  
|Ignorar Falha|O erro ou truncamento é ignorado e a linha de dados é direcionada para a saída da transformação ou fonte.|  
|Redirecionar Linha|O erro ou truncamento da linha de dados é direcionado para a saída de erro da fonte, transformação ou destino.|  
  
## <a name="adding-the-error-description"></a>Adicionando a descrição do erro  
 Por padrão, uma saída de erro fornece o código de erro numérico e costuma conter o identificador da coluna na qual o erro ocorreu. Você pode usar o componente Script para incluir a descrição do erro em uma coluna adicional, usando uma única linha de script para chamar o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.GetErrorDescription%2A> da interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>.  
  
 O componente Script pode ser adicionado ao segmento de erro do fluxo de dados em qualquer downstream dos componentes de fluxo de dados cujos erros você quer capturar, mas geralmente é posicionado imediatamente antes de as linhas de erro serem gravadas em um destino. Deste modo, o script pesquisa só descrições para linhas de erro que estão gravadas. Por exemplo, o segmento de erro do fluxo de dados pode corrigir alguns erros e não gravar essas linhas em um destino de erro. Para obter mais informações, consulte [aprimorando uma saída de erro com o componente Script](../extending-packages-scripting-data-flow-script-component-examples/enhancing-an-error-output-with-the-script-component.md).  
  
### <a name="to-configure-an-error-output"></a>Para configurar uma saída de erro  
  
-   [Configurar uma saída de erro em um componente de fluxo de dados](../configure-an-error-output-in-a-data-flow-component.md)  
  
## <a name="see-also"></a>Consulte também  
 [Fluxo de Dados](data-flow.md)   
 [Transformar Dados com Transformações](transformations/transform-data-with-transformations.md)   
 [Conectar componentes com caminhos](../connect-components-with-paths.md)   
 [Tarefa de Fluxo de Dados](../control-flow/data-flow-task.md)   
 [Fluxo de Dados](data-flow.md)  
  
  