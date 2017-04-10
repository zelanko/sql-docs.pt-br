---
title: "Editor de Transforma&#231;&#227;o Amostragem de Linhas (p&#225;gina Amostragem) | Microsoft Docs"
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
  - "sql13.DTS.DESIGNER.ROWSAMPLINGTRANSFORMATION.COLUMNS.F1"
  - "sql13.dts.designer.rowsamplingtransformation.f1"
helpviewer_keywords: 
  - "Editor de Transformação Amostragem de Linhas"
ms.assetid: 544c7709-6de0-4c08-bda3-759985be9a05
caps.latest.revision: 23
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 23
---
# Editor de Transforma&#231;&#227;o Amostragem de Linhas (p&#225;gina Amostragem)
  Use a caixa de diálogo **Editor de Transformação Amostragem de Linhas** para dividir uma parte de uma entrada em uma amostra usando um número de linhas especificado. Essa transformação divide a entrada em duas saídas separadas.  
  
 Para saber mais sobre a transformação Amostragem de Linhas, consulte [Row Sampling Transformation](../../../integration-services/data-flow/transformations/row-sampling-transformation.md).  
  
## Opções  
 **Número de linhas**  
 Especifique o número de linhas da entrada a serem usadas como amostra.  
  
 O valor dessa propriedade pode ser especificado com uma expressão de propriedades.  
  
 **Nome de saída do exemplo**  
 Forneça um nome exclusivo para a saída que incluirá as linhas de amostra. O nome fornecido será exibido no Designer SSIS.  
  
 **Nome de saída não selecionado**  
 Forneça um nome exclusivo para a saída que conterá as linhas excluídas da amostragem. O nome fornecido será exibido no Designer SSIS.  
  
 **Usar a seguinte semente aleatória**  
 Especifique a semente de amostra para o gerador de números aleatórios que a transformação usa para criar uma amostra. Recomendado apenas para desenvolvimento e teste. A transformação usará a contagem de tiques do Microsoft Windows como semente se não for especificada uma semente aleatória.  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Transformação Amostragem Percentual](../../../integration-services/data-flow/transformations/percentage-sampling-transformation.md)  
  
  