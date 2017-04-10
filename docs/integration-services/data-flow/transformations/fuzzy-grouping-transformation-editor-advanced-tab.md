---
title: "Editor de Transforma&#231;&#227;o Agrupamento Difuso (guia Avan&#231;ado) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.fuzzygroupingtransformation.advanced.f1"
helpviewer_keywords: 
  - "Editor de Transformação Agrupamento Difuso"
ms.assetid: dd820d75-b8a7-4515-aea4-3553ba5b442e
caps.latest.revision: 28
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 28
---
# Editor de Transforma&#231;&#227;o Agrupamento Difuso (guia Avan&#231;ado)
  Use a guia **Avançado** da caixa de diálogo **Editor de Transformação Agrupamento Difuso** para especificar colunas de entrada e saída, definir limites de similaridade e definir delimitadores.  
  
> [!NOTE]  
>  As propriedades **Exhaustive** e **MaxMemoryUsage** da transformação Agrupamento Difuso não estão disponíveis no **Editor de Transformação Agrupamento Difuso**, mas podem ser definidas por meio do **Editor Avançado**. Para obter mais informações sobre essas propriedades, consulte a seção Transformação Agrupamento Difuso em [Transformation Custom Properties](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Para saber mais sobre a transformação Agrupamento Difuso, consulte [Fuzzy Grouping Transformation](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md).  
  
## Opções  
 **Nome da coluna da chave de entrada**  
 Especifique o nome de uma coluna de saída que contém o identificador exclusivo para cada coluna de entrada. A coluna **_key_in** tem um valor que identifica exclusivamente cada linha.  
  
 **Nome da coluna da chave de saída**  
 Especifique o nome de uma coluna de saída que contém um identificador exclusivo para a linha canônica de um grupo de linhas duplicadas. A coluna **_key_out** corresponde ao valor **_key_in** da linha de dados canônica.  
  
 **Nome da coluna de pontuação de similaridade**  
 Especifique um nome para a coluna que contém a pontuação de similaridade. A pontuação de similaridade é um valor entre 0 e 1 que indica a similaridade da linha de entrada à linha canônica. Quanto mais próxima de 1 for a pontuação, mais próxima será a correspondência da fila com a fila canônica.  
  
 **Limite de similaridade**  
 Defina o limite de similaridade usando o controle deslizante. Quanto mais próximo de 1 for o limite, mais linhas deverão ser similares umas às outras para se qualificarem como duplicatas. Aumentar o limite pode melhorar a velocidade de correspondência, pois menos registros candidatos precisam ser considerados.  
  
 **Delimitadores de token**  
 A transformação fornece um conjunto padrão de delimitadores para criar tokens de dados, mas você pode adicionar ou remover delimitadores, conforme a necessidade, editando a lista.  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Identificar linhas de dados semelhantes por meio da transformação Agrupamento Difuso](../../../integration-services/data-flow/transformations/identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation.md)  
  
  