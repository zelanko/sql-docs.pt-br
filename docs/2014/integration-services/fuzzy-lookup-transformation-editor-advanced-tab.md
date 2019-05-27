---
title: Editor de transformação pesquisa difusa (guia Avançado) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzylookuptransformation.advanced.f1
helpviewer_keywords:
- Fuzzy Lookup Transformation Editor
ms.assetid: 0a2919be-2ea7-4c06-82b8-0ffad5f0dd83
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 26a7efa42215f1bc456cf4a4c47b3a71c62b94e7
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66058349"
---
# <a name="fuzzy-lookup-transformation-editor-advanced-tab"></a>Editor de Transformação Pesquisa Difusa (guia Avançado)
  Use a guia **Avançado** da caixa de diálogo **Editor de Transformação Pesquisa Difusa** para definir parâmetros para a pesquisa difusa.  
  
 Para saber mais sobre a transformação Pesquisa Difusa, consulte [Fuzzy Lookup Transformation](data-flow/transformations/lookup-transformation.md).  
  
## <a name="options"></a>Opções  
 **Número máximo de correspondências a produzir por pesquisa**  
 Especifique o número máximo de correspondências que a transformação pode retornar para cada linha de entrada. O padrão é **1**.  
  
 **Limite de similaridade**  
 Defina o limite de similaridade no nível de componente usando o controle deslizante. Quanto mais próximo de 1 for o valor, maior deverá ser a semelhança entre o valor de pesquisa e o valor da origem para a qualificação de correspondências. Aumentar o limite pode melhorar a velocidade de correspondência, já que menos registros serão considerados candidatos.  
  
 **Delimitadores de token**  
 Especifique os delimitadores usados pela transformação para criar tokens de valores de coluna.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de Transformação Pesquisa Difusa &#40;Guia Tabela de Referência&#41;](../../2014/integration-services/fuzzy-lookup-transformation-editor-reference-table-tab.md)   
 [Editor de Transformação Pesquisa Difusa &#40;guia Colunas&#41;](../../2014/integration-services/fuzzy-lookup-transformation-editor-columns-tab.md)  
  
  
