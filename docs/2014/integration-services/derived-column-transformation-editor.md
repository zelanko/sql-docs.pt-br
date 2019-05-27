---
title: Derivado de Editor de transformação de coluna | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.derivedcolumntransformation.f1
helpviewer_keywords:
- Derived Column Transformation Editor
ms.assetid: ff73923e-d245-43d8-bf24-af3bdc942e51
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4fc2701ad53cd0071be40100d168d5d5571d2958
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66059565"
---
# <a name="derived-column-transformation-editor"></a>Editor de Transformação Colunas Derivadas
  Use a caixa de diálogo **Editor de Transformação Colunas Derivadas** para criar expressões que populem colunas novas ou de substituição.  
  
 Para saber mais sobre a transformação Coluna Derivada, consulte [Transformação Coluna Derivada](data-flow/transformations/derived-column-transformation.md).  
  
## <a name="options"></a>Opções  
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
  
 **Tópicos relacionados:** [Expressões do Integration Services &#40;SSIS&#41;](expressions/integration-services-ssis-expressions.md), [Operadores &#40;Expressão SSIS&#41;](expressions/operators-ssis-expression.md) e [Funções &#40;Expressão SSIS&#41;](expressions/functions-ssis-expression.md)  
  
 **Tipo de Dados**  
 Se acrescentar dados a uma nova coluna, a caixa de diálogo **TransformationEditor de Coluna Derivada** avaliará a expressão automaticamente e definirá o tipo de dados adequadamente. O valor desta coluna é somente leitura. Para obter mais informações, consulte [Integration Services Data Types](data-flow/integration-services-data-types.md).  
  
 **Comprimento**  
 Se acrescentar dados a uma nova coluna, a caixa de diálogo **TransformationEditor de Coluna Derivada** avaliará a expressão automaticamente e definirá a largura de coluna para os dados da cadeia de caracteres. O valor desta coluna é somente leitura.  
  
 **Precisão**  
 Se acrescentar dados a uma nova coluna, a caixa de diálogo **TransformationEditor de Coluna Derivada** automaticamente definirá a precisão de dados numéricos com base no tipo de dados. O valor desta coluna é somente leitura.  
  
 **Escala**  
 Se acrescentar dados a uma nova coluna, a caixa de diálogo **TransformationEditor de Coluna Derivada** automaticamente definirá a escala dos dados numéricos com base no tipo de dados. O valor desta coluna é somente leitura.  
  
 **Página de Código**  
 Se acrescentar dados a uma nova coluna, a caixa de diálogo **TransformationEditor de Coluna Derivada** automaticamente definirá a página de código para o tipo de dados DT_STR. Será possível atualizar a **Página de Código**.  
  
 **Configurar saída de erro**  
 Especifique como tratar os erros usando a caixa de diálogo [Configurar Saída de Erro](../../2014/integration-services/configure-error-output.md) .  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Derivar valores de coluna por meio da transformação Coluna Derivada](data-flow/transformations/derive-column-values-by-using-the-derived-column-transformation.md)  
  
  
