---
title: "Editor de Transforma&#231;&#227;o Pesquisa Difusa (guia Avan&#231;ado) | Microsoft Docs"
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
  - "sql13.dts.designer.fuzzylookuptransformation.advanced.f1"
helpviewer_keywords: 
  - "Editor de Transformação Pesquisa Difusa"
ms.assetid: 0a2919be-2ea7-4c06-82b8-0ffad5f0dd83
caps.latest.revision: 27
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 27
---
# Editor de Transforma&#231;&#227;o Pesquisa Difusa (guia Avan&#231;ado)
  Use a guia **Avançado** da caixa de diálogo **Editor de Transformação Pesquisa Difusa** para definir parâmetros para a pesquisa difusa.  
  
 Para saber mais sobre a transformação Pesquisa Difusa, consulte [Fuzzy Lookup Transformation](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md).  
  
## Opções  
 **Número máximo de correspondências a produzir por pesquisa**  
 Especifique o número máximo de correspondências que a transformação pode retornar para cada linha de entrada. O padrão é **1**.  
  
 **Limite de similaridade**  
 Defina o limite de similaridade no nível de componente usando o controle deslizante. Quanto mais próximo de 1 for o valor, maior deverá ser a semelhança entre o valor de pesquisa e o valor da origem para a qualificação de correspondências. Aumentar o limite pode melhorar a velocidade de correspondência, já que menos registros serão considerados candidatos.  
  
 **Delimitadores de token**  
 Especifique os delimitadores usados pela transformação para criar tokens de valores de coluna.  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de Transformação Pesquisa Difusa &#40;Guia Tabela de Referência&#41;](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation-editor-reference-table-tab.md)   
 [Editor de Transformação Pesquisa Difusa &#40;guia Colunas&#41;](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation-editor-columns-tab.md)  
  
  