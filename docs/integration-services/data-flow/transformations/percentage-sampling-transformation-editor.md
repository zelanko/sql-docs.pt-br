---
title: "Editor de transformação amostragem percentual | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.percentagesamplingtransformation.f1
helpviewer_keywords:
- Percentage Sampling Transformation Editor
ms.assetid: 2c40d804-26a3-4d35-809b-bc923d83d451
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a3cf0dd802330585e50428b3301270930b31766d
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="percentage-sampling-transformation-editor"></a>Editor de Transformação Amostragem Percentual
  Use a caixa de diálogo **Editor de Transformação Amostragem Percentual** para dividir parte de uma entrada em uma amostra, usando uma porcentagem de linhas especificada. Essa transformação divide a entrada em duas saídas separadas.  
  
 Para saber mais sobre a transformação amostragem percentual, consulte [Percentage Sampling Transformation](../../../integration-services/data-flow/transformations/percentage-sampling-transformation.md).  
  
## <a name="options"></a>Opções  
 **Porcentagem de linhas**  
 Especifique a porcentagem de linhas na entrada a usar como amostra.  
  
 O valor dessa propriedade pode ser especificado com uma expressão de propriedades.  
  
 **Nome de saída do exemplo**  
 Forneça um nome exclusivo para a saída que incluirá as linhas de amostra. O nome fornecido será exibido no Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)] .  
  
 **Nome de saída não selecionado**  
 Forneça um nome exclusivo para a saída que conterá as linhas excluídas da amostragem. O nome fornecido será exibido no Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)] .  
  
 **Usar a seguinte semente aleatória**  
 Especifique a semente de amostra para o gerador de números aleatórios que a transformação usa para criar uma amostra. Recomendado apenas para desenvolvimento e teste. A transformação usará a contagem de tiques do Microsoft Windows se não for especificada uma semente aleatória.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Transformação Amostragem de Linhas](../../../integration-services/data-flow/transformations/row-sampling-transformation.md)  
  
  
