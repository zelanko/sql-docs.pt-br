---
title: "Transformação de difusão seletiva | Microsoft Docs"
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
- sql13.dts.designer.multicasttrans.f1
helpviewer_keywords:
- multiple outputs
- Multicast transformation
- datasets [Integration Services], multiple outputs
- multiple transformations
ms.assetid: 32194784-1684-40cd-9f91-1aba4d8360d3
caps.latest.revision: 45
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8619a0ed02ffc73126eb151f4a83a0b6b24c4be8
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="multicast-transformation"></a>Transformação Difusão Seletiva
  A transformação Multicast distribui sua entrada em uma ou mais saídas. Essa transformação é semelhante à transformação de divisão condicional. Ambas as transformações dirigem uma entrada para saídas múltiplas. A diferença entre as duas é que a transformação de difusão seletiva dirige todas as linhas para todas as saídas e a divisão condicional dirige uma linha para uma única saída. Para obter mais informações, consulte [Conditional Split Transformation](../../../integration-services/data-flow/transformations/conditional-split-transformation.md).  
  
 Configura-se a transformação de difusão seletiva adicionando saídas.  
  
 Usando a transformação de difusão seletiva, um pacote pode criar cópias lógicas de dados. Essa capacidade é útil quando o pacote precisar aplicar vários conjuntos de transformações aos mesmos dados. Por exemplo, uma cópia dos dados é agregada e somente o resumo informativo é carregado em seu destino, enquanto outra cópia dos dados é estendida com valores de pesquisa e colunas derivadas antes que seja carregada em seu destino.  
  
 Essa transformação tem uma entrada e múltiplas saídas. Não dá suporte a uma saída de erro.  
  
## <a name="configuration-of-the-multicast-transformation"></a>Configuração da transformação Multicast  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Transformação Multicast** , consulte [Multicast Transformation Editor](../../../integration-services/data-flow/transformations/multicast-transformation-editor.md).  
  
 Para obter informações sobre as propriedades que podem ser definidas programaticamente, consulte [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796).  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
 Para obter informações sobre como definir as propriedades deste componente, consulte [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Consulte também  
 [Fluxo de Dados](../../../integration-services/data-flow/data-flow.md)   
 [Transformações do Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
