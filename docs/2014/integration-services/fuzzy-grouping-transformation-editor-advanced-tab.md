---
title: Editor de transformação Agrupamento Difuso (guia Avançado) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzygroupingtransformation.advanced.f1
helpviewer_keywords:
- Fuzzy Grouping Transformation Editor
ms.assetid: dd820d75-b8a7-4515-aea4-3553ba5b442e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: dcebe499eb80fbe01b9aa36a4e07785846eaf621
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66058365"
---
# <a name="fuzzy-grouping-transformation-editor-advanced-tab"></a>Editor de Transformação Agrupamento Difuso (guia Avançado)
  Use a guia **Avançado** da caixa de diálogo **Editor de Transformação Agrupamento Difuso** para especificar colunas de entrada e saída, definir limites de similaridade e definir delimitadores.  
  
> [!NOTE]  
>  As `Exhaustive` `MaxMemoryUsage` Propriedades e da transformação Agrupamento Difuso não estão disponíveis no **Editor de transformação Agrupamento Difuso**, mas podem ser definidas usando o **Editor avançado**. Para obter mais informações sobre essas propriedades, consulte a seção Transformação Agrupamento Difuso em [Transformation Custom Properties](data-flow/transformations/transformation-custom-properties.md).  
  
 Para saber mais sobre a transformação Agrupamento Difuso, consulte [Fuzzy Grouping Transformation](data-flow/transformations/fuzzy-grouping-transformation.md).  
  
## <a name="options"></a>Opções  
 **Nome da coluna da chave de entrada**  
 Especifique o nome de uma coluna de saída que contém o identificador exclusivo para cada coluna de entrada. A coluna `_key_in` tem um valor que identifica exclusivamente cada linha.  
  
 **Nome da coluna da chave de saída**  
 Especifique o nome de uma coluna de saída que contém um identificador exclusivo para a linha canônica de um grupo de linhas duplicadas. A coluna `_key_out` corresponde ao valor `_key_in` da linha de dados canônica.  
  
 **Nome da coluna de pontuação de similaridade**  
 Especifique um nome para a coluna que contém a pontuação de similaridade. A pontuação de similaridade é um valor entre 0 e 1 que indica a similaridade da linha de entrada à linha canônica. Quanto mais próxima de 1 for a pontuação, mais próxima será a correspondência da fila com a fila canônica.  
  
 **Limite de similaridade**  
 Defina o limite de similaridade usando o controle deslizante. Quanto mais próximo de 1 for o limite, mais linhas deverão ser similares umas às outras para se qualificarem como duplicatas. Aumentar o limite pode melhorar a velocidade de correspondência, pois menos registros candidatos precisam ser considerados.  
  
 **Delimitadores de token**  
 A transformação fornece um conjunto padrão de delimitadores para criar tokens de dados, mas você pode adicionar ou remover delimitadores, conforme a necessidade, editando a lista.  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Identificar linhas de dados semelhantes por meio da transformação Agrupamento Difuso](data-flow/transformations/identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation.md)  
  
  
