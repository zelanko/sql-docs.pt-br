---
title: Editor de transformação extração de termos (guia Avançado) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.termextraction.advanced.f1
helpviewer_keywords:
- Term Extraction Transformation Editor
ms.assetid: 87118281-6e3c-499e-bac4-fa4c24bb12c6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ce44e2709013a6d56d47ad30c90ecf5d92825503
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48185326"
---
# <a name="term-extraction-transformation-editor-advanced-tab"></a>Editor de Transformação Extração de Termos (guia Avançado)
  Use a guia **Avançado** da caixa de diálogo **Editor de Transformação de Extração de Termos** para especificar propriedades de extração, como frequência, comprimento e se devem ser extraídas palavras ou frases.  
  
 Para saber mais sobre a transformação Extração de Termos, consulte [Term Extraction Transformation](data-flow/transformations/term-extraction-transformation.md).  
  
## <a name="options"></a>Opções  
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
 Especifique se a extração deve ser feita diferenciando maiúsculas e minúsculas. O padrão é `False`.  
  
 **Configurar Saída de Erro**  
 Use a caixa de diálogo [Configurar Saída de Erro](../../2014/integration-services/configure-error-output.md) para especificar tratamento de erro em linhas que causam erros.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de transformação extração de termo &#40;guia de extração de termos&#41;](../../2014/integration-services/term-extraction-transformation-editor-term-extraction-tab.md)   
 [Editor de transformação extração de termo &#40;guia de exclusão&#41;](../../2014/integration-services/term-extraction-transformation-editor-exclusion-tab.md)   
 [Transformação Pesquisa de Termos](data-flow/transformations/lookup-transformation.md)  
  
  
