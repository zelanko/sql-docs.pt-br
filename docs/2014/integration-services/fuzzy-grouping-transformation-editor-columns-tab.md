---
title: Editor de transformação Agrupamento Difuso (guia colunas) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzygroupingtransformation.columns.f1
helpviewer_keywords:
- Fuzzy Grouping Transformation Editor
ms.assetid: 24f4539f-2a9f-4acd-acc7-06228a07f7df
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 26ba2fc6a8cfdfb6855d7d5b29cc3be31f1d53da
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84966315"
---
# <a name="fuzzy-grouping-transformation-editor-columns-tab"></a>Editor de Transformação Agrupamento Difuso (guia Colunas)
  Use a guia **Colunas** da caixa de diálogo **Editor de Transformação Agrupamento Difuso** para especificar as colunas usadas para agrupar linhas com valores duplicados.  
  
 Para saber mais sobre a transformação Agrupamento Difuso, consulte [Fuzzy Grouping Transformation](data-flow/transformations/fuzzy-grouping-transformation.md).  
  
## <a name="options"></a>Opções  
 **Colunas de Entrada Disponíveis**  
 Selecione nesta lista as colunas de entrada usadas para agrupar linhas com valores duplicados.  
  
 **Nome**  
 Visualize os nomes das colunas de entrada disponíveis.  
  
 **Passagem**  
 Selecione se a coluna de entrada deve ser incluída na saída da transformação. Todas as colunas usadas para agrupar são copiadas automaticamente para a saída. Você pode incluir colunas adicionais, marcando esta coluna.  
  
 **Coluna de Entrada**  
 Selecione uma das colunas de entrada selecionadas anteriormente na lista **Colunas de Entrada Disponíveis** .  
  
 **Alias de saída**  
 Digite um nome descritivo para a coluna de saída correspondente. Por padrão, o nome da coluna de saída é idêntico ao nome da coluna de entrada.  
  
 **Alias de Saída de Grupo**  
 Digite um nome descritivo para a coluna que conterá o valor canônico para as duplicatas agrupadas. O nome padrão dessa coluna de saída é o nome da coluna de entrada acrescido de _clean.  
  
 **Associar Tipo**  
 Selecione correspondência difusa ou exata. As linhas serão consideradas duplicatas se forem suficientemente semelhantes em todas as colunas que têm tipo de correspondência difusa. Se você também especificar correspondência exata em certas colunas, apenas as linhas que contiverem valores idênticos nessas colunas serão consideradas possíveis duplicatas. Portanto, se souber que certa coluna não contém nenhum erro ou inconsistência, você poderá especificar correspondência exata nessa coluna para aumentar a exatidão da correspondência difusa nas outras colunas.  
  
 **Similaridade Mínima**  
 Defina o limite de similaridade no nível de junção, usando o controle deslizante. Quanto mais próximo de 1 for o valor, maior deverá ser a semelhança entre o valor de pesquisa e o valor da origem para a qualificação de correspondências. Aumentar o limite pode melhorar a velocidade de correspondência, já que menos registros serão considerados candidatos.  
  
 **Alias de Saída de Similaridade**  
 Especifique o nome da nova coluna de saída que conterá as pontuações de similaridade da junção selecionada. Se você deixar este valor vazio, a coluna de saída não será criada.  
  
 **Numerais**  
 Especifique a significância dos numerais à esquerda e à direita na comparação dos dados da coluna. Por exemplo, se os numerais à esquerda forem significativos, "123 Main Street" não será grupado com "456 Main Street".  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Nenhum**|Numerais à esquerda e à direita não são significativos.|  
|**Conceitua**|Apenas numerais à esquerda são significativos.|  
|**À Direita**|Apenas numerais à direita são significativos.|  
|**À Esquerda e À Direita**|Numerais tanto à esquerda, quanto à direita são significativos.|  
  
 **Sinalizadores de Comparação**  
 Para obter mais informações sobre as opções de comparação de cadeias de caracteres, consulte [Comparando dados de cadeia de caracteres](data-flow/comparing-string-data.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Identificar linhas de dados semelhantes por meio da transformação Agrupamento Difuso](data-flow/transformations/identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation.md)  
  
  
