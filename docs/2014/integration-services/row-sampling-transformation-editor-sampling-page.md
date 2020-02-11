---
title: Editor de transformação amostragem de linhas (página amostragem) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.ROWSAMPLINGTRANSFORMATION.COLUMNS.F1
- sql12.dts.designer.rowsamplingtransformation.f1
helpviewer_keywords:
- Row Sampling Transformation Editor
ms.assetid: 544c7709-6de0-4c08-bda3-759985be9a05
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 30163b4d65ac6a732efb3f7c67a018f433a42ac0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66056452"
---
# <a name="row-sampling-transformation-editor-sampling-page"></a>Editor de Transformação Amostragem de Linhas (página Amostragem)
  Use a caixa de diálogo **Editor de Transformação Amostragem de Linhas** para dividir uma parte de uma entrada em uma amostra usando um número de linhas especificado. Essa transformação divide a entrada em duas saídas separadas.  
  
 Para saber mais sobre a transformação Amostragem de Linhas, consulte [Row Sampling Transformation](data-flow/transformations/row-sampling-transformation.md).  
  
## <a name="options"></a>Opções  
 **Número de linhas**  
 Especifique o número de linhas da entrada a serem usadas como amostra.  
  
 O valor dessa propriedade pode ser especificado com uma expressão de propriedades.  
  
 **Nome de saída do exemplo**  
 Forneça um nome exclusivo para a saída que incluirá as linhas de amostra. O nome fornecido será exibido no Designer SSIS.  
  
 **Nome de saída não selecionado**  
 Forneça um nome exclusivo para a saída que conterá as linhas excluídas da amostragem. O nome fornecido será exibido no Designer SSIS.  
  
 **Usar a seguinte semente aleatória**  
 Especifique a semente de amostra para o gerador de números aleatórios que a transformação usa para criar uma amostra. Recomendado apenas para desenvolvimento e teste. A transformação usará a contagem de tiques do Microsoft Windows como semente se não for especificada uma semente aleatória.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [transformação Amostragem Percentual](data-flow/transformations/percentage-sampling-transformation.md)  
  
  
