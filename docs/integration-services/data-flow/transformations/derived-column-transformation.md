---
title: Transformação de Coluna Derivada | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.derivedcolumntrans.f1
- sql13.dts.designer.derivedcolumntransformation.f1
helpviewer_keywords:
- multiple derived columns
- expressions [Integration Services], derived columns
- derived columns
- columns [Integration Services], derivations
- Derived Column transformation
ms.assetid: 8eba755e-8e48-4233-bd1e-09a46bf2692f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5b1c27ff60b3e1c4dc99478d2df0377ae05a77f8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47713554"
---
# <a name="derived-column-transformation"></a>Transformação Coluna Derivada
  A transformação Coluna Derivada cria novos valores de coluna aplicando expressões às colunas de entrada de transformação. Uma expressão pode conter qualquer combinação de variáveis, funções, operadores e colunas da entrada de transformação. O resultado pode ser adicionado como uma coluna nova ou adicionado a uma coluna existente como um valor de substituição. A transformação Coluna Derivada pode definir várias colunas derivadas, e qualquer variável ou coluna de entrada pode aparecer em várias expressões.  
  
 É possível usar essa transformação para executar as seguintes tarefas:  
  
-   Concatenar dados de colunas diferentes em uma coluna derivada. Por exemplo, você pode combinar valores das colunas **FirstName** e **LastName** em uma única coluna derivada chamada **FullName**usando a expressão `FirstName + " " + LastName`.  
  
-   Extrair caracteres de dados de cadeia de caracteres utilizando funções, como SUBSTRING, e armazenar o resultado em uma coluna derivada. Por exemplo, é possível extrair a inicial de uma pessoa da coluna **FirstName** utilizando a expressão `SUBSTRING(FirstName,1,1)`.  
  
-   Aplicar funções matemáticas a dados numéricos e armazenar o resultado em uma coluna derivada. Por exemplo, você pode alterar o comprimento e a precisão de uma coluna numérica, **SalesTax**, para um número com duas casas decimais utilizando a expressão `ROUND(SalesTax, 2)`.  
  
-   Criar expressões que comparam colunas de entrada e variáveis. Por exemplo, você pode comparar a variável **Version** com os dados na coluna **ProductVersion**e, dependendo do resultado da comparação, utilizar o valor de **Version** ou de **ProductVersion**utilizando a expressão `ProductVersion == @Version? ProductVersion : @Version`.  
  
-   Extrair partes de um valor de data e hora. Por exemplo, você pode usar as funções GETDATE e DATEPART para extrair o ano atual por meio da expressão `DATEPART("year",GETDATE())`.  
  
-   Converta cadeias de caracteres de dados em um formato específico usando uma expressão.  
  
## <a name="configuration-of-the-derived-column-transformation"></a>Configuração da transformação Coluna Derivada  
 Você pode configurar a transformação Coluna Derivada das seguintes maneiras:  
  
-   Forneça uma expressão para cada coluna de entrada ou coluna nova a ser alterada. Para obter mais informações, consulte [Expressões do Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md).  
  
    > [!NOTE]  
    >  Se uma expressão fizer referência a uma coluna de entrada substituída pela transformação Coluna Derivada, a expressão utilizará o valor original da coluna e não o valor derivado.  
  
-   Se estiver adicionando resultados às novas colunas e o tipo de dados for **string**, especifique uma página de código. Para obter mais informações, consulte [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md).  
  
 A transformação Coluna Derivada inclui a propriedade personalizada FriendlyExpression. Essa propriedade pode ser atualizada por uma expressão de propriedade quando o pacote é carregado. Para obter mais informações, consulte [Usar expressões de propriedade em pacotes](../../../integration-services/expressions/use-property-expressions-in-packages.md)e [Propriedades personalizadas da transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Essa transformação tem uma entrada, uma saída comum e uma saída de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas de Transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Para obter mais informações sobre como definir propriedades, clique em um dos seguintes tópicos:  
  
-   [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Derivar valores de coluna por meio da transformação Coluna Derivada](../../../integration-services/data-flow/transformations/derive-column-values-by-using-the-derived-column-transformation.md)  
  
## <a name="derived-column-transformation-editor"></a>Editor de Transformação Colunas Derivadas
  Use a caixa de diálogo **Editor de Transformação Colunas Derivadas** para criar expressões que populem colunas novas ou de substituição.  
  
### <a name="options"></a>Opções  
 **Variáveis e Colunas**  
 Crie uma expressão que use uma variável ou uma coluna de entrada arrastando a variável ou coluna da lista de variáveis e colunas disponíveis para uma linha de tabela existente no painel abaixo, ou para uma linha nova no final da lista.  
  
 **Funções e operadores**  
 Crie uma expressão que use uma função ou um operador para avaliar dados de entrada e dados de saída diretos arrastando funções e operadores da lista para o painel abaixo.  
  
 **Nome de Coluna Derivada**  
 Forneça um nome de coluna derivada. O padrão é uma lista numerada de colunas derivadas; no entanto, é possível escolher qualquer nome descritivo exclusivo.  
  
 **Coluna Derivada**  
 Selecione uma coluna derivada da lista. Escolha se deseja adicionar a coluna derivada como uma nova coluna de saída ou substituir os dados em uma coluna existente.  
  
 **Expression**  
 Digite uma expressão ou compile uma arrastando da lista anterior de colunas, variáveis, funções e operadores disponíveis.  
  
 O valor dessa propriedade pode ser especificado com uma expressão de propriedades.  
  
 **Tópicos relacionados**: [Expressões do Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Operadores &#40;Expressão SSIS&#41;](../../../integration-services/expressions/operators-ssis-expression.md) e [Funções &#40;Expressão SSIS&#41;](../../../integration-services/expressions/functions-ssis-expression.md)  
  
 **Tipo de Dados**  
 Se acrescentar dados a uma nova coluna, a caixa de diálogo **TransformationEditor de Coluna Derivada** avaliará a expressão automaticamente e definirá o tipo de dados adequadamente. O valor desta coluna é somente leitura. Para obter mais informações, consulte [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md).  
  
 **Comprimento**  
 Se acrescentar dados a uma nova coluna, a caixa de diálogo **TransformationEditor de Coluna Derivada** avaliará a expressão automaticamente e definirá a largura de coluna para os dados da cadeia de caracteres. O valor desta coluna é somente leitura.  
  
 **Precisão**  
 Se acrescentar dados a uma nova coluna, a caixa de diálogo **TransformationEditor de Coluna Derivada** automaticamente definirá a precisão de dados numéricos com base no tipo de dados. O valor desta coluna é somente leitura.  
  
 **Escala**  
 Se acrescentar dados a uma nova coluna, a caixa de diálogo **TransformationEditor de Coluna Derivada** automaticamente definirá a escala dos dados numéricos com base no tipo de dados. O valor desta coluna é somente leitura.  
  
 **Página de Código**  
 Se acrescentar dados a uma nova coluna, a caixa de diálogo **TransformationEditor de Coluna Derivada** automaticamente definirá a página de código para o tipo de dados DT_STR. Será possível atualizar a **Página de Código**.  
  
 **Configurar saída de erro**  
 Especifique como tratar os erros usando a caixa de diálogo [Configurar Saída de Erro](http://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) .  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Artigo técnico, [Exemplos de expressões SSIS](http://go.microsoft.com/fwlink/?LinkId=220761), em social.technet.microsoft.com  
