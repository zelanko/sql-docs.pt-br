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
ms.openlocfilehash: 24c35eb9b1df9f250d21e95b591ec2cc40026038
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84966296"
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
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de transformação pesquisa difusa &#40;guia tabela de referência&#41;](../../2014/integration-services/fuzzy-lookup-transformation-editor-reference-table-tab.md)   
 [Editor de Transformação Pesquisa Difusa &#40;guia Colunas&#41;](../../2014/integration-services/fuzzy-lookup-transformation-editor-columns-tab.md)  
  
  
