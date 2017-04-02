---
title: "Editor de Transforma&#231;&#227;o Extra&#231;&#227;o de Termos (guia Avan&#231;ado) | Microsoft Docs"
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
  - "sql13.dts.designer.termextraction.advanced.f1"
helpviewer_keywords: 
  - "Editor de Transformação Extração de Termos"
ms.assetid: 87118281-6e3c-499e-bac4-fa4c24bb12c6
caps.latest.revision: 29
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 29
---
# Editor de Transforma&#231;&#227;o Extra&#231;&#227;o de Termos (guia Avan&#231;ado)
  Use a guia **Avançado** da caixa de diálogo **Editor de Transformação de Extração de Termos** para especificar propriedades de extração, como frequência, comprimento e se devem ser extraídas palavras ou frases.  
  
 Para saber mais sobre a transformação Extração de Termos, consulte [Term Extraction Transformation](../../../integration-services/data-flow/transformations/term-extraction-transformation.md).  
  
## Opções  
 **Substantivo**  
 Especifique que a transformação só extrai substantivos individuais.  
  
 **Frase substantivada**  
 Especifique que a transformação só extraia frases substantivadas.  
  
 **Substantivo e frase substantivada**  
 Especifique que a transformação extraia tanto substantivos como frases substantivadas.  
  
 **Frequência**  
 Especifique que a pontuação é a frequência do termo.  
  
 **TFIDF**  
 Especifique que a pontuação é o valor TFIDF do termo. A pontuação TFIDF é o produto da Frequência do Termo e da Frequência de Documento Inversa, definido como: TFIDF de um termo T = (frequência de T) * log ((nºs de linhas na Entrada) / (nº de linhas com T))  
  
 **Limite de frequência**  
 Especifique o número de vezes que uma palavra ou frase deve aparecer antes de ser extraída. O valor padrão é 2.  
  
 **Comprimento máximo do termo**  
 Especifique o comprimento máximo de uma frase em palavras. Esta opção só afeta frases substantivadas. O valor padrão é 12.  
  
 **Usar extração de termos com diferenciação de maiúsculas e minúsculas**  
 Especifique se a extração deve ser feita diferenciando maiúsculas e minúsculas. O padrão é **False**.  
  
 **Configurar Saída de Erro**  
 Use a caixa de diálogo [Configurar Saída de Erro](../Topic/Configure%20Error%20Output.md) para especificar tratamento de erro em linhas que causam erros.  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de Transformação Extração de Termos &#40;Guia Extração de Termos&#41;](../../../integration-services/data-flow/transformations/term-extraction-transformation-editor-term-extraction-tab.md)   
 [Editor de Transformação Extração de Termos &#40;Guia Exclusão&#41;](../../../integration-services/data-flow/transformations/term-extraction-transformation-editor-exclusion-tab.md)   
 [Transformação Pesquisa de Termo](../../../integration-services/data-flow/transformations/term-lookup-transformation.md)  
  
  