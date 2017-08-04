---
title: Union All Transformation | Microsoft Docs
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
- sql13.dts.designer.unionalltrans.f1
helpviewer_keywords:
- merging datasets [Integration Services]
- combining datasets
- Union All transformation
- datasets [Integration Services], merging
ms.assetid: 942e4b90-9c41-4e9c-a6f3-80b3afe57f2f
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 049d9195499e7145f98258cb90f2fd7069569058
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="union-all-transformation"></a>transformação Unir Tudo
  A transformação Union All combina várias entradas em apenas uma saída. Por exemplo, as saídas provenientes de cinco origens de Arquivo Simples diferentes podem ser aplicadas à transformação Unir Tudo e combinadas em apenas uma saída.  
  
## <a name="inputs-and-outputs"></a>Entradas e saídas  
 As entradas da transformação são adicionadas à saída da transformação uma após a outra, sem reordenação das linhas. Se o pacote requerer uma saída ordenada, você deve usar a transformação Merge em vez da Union All.  
  
 A primeira entrada que você conectar à transformação Union All será a entrada da qual a transformação criará a saída. As colunas nas entradas que você conectar subsequentemente à transformação serão mapeadas para as colunas, na saída da transformação.  
  
 Para mesclar as entradas, você deve mapear as colunas nas entradas para as colunas na saída. Uma coluna com pelo menos uma entrada deve ser mapeada para cada coluna de saída. O mapeamento entre duas colunas requer que seus metadados tenham correspondência. Por exemplo, as colunas mapeadas devem ter o mesmo tipo de dados.  
  
 Se as colunas mapeadas contiverem dados de cadeia de caracteres e a coluna de saída for mais curta que a de entrada, a coluna da saída será aumentada automaticamente para comportar a coluna de entrada. As colunas de entrada que não forem mapeadas para as de saída serão definidas com valores nulos nas colunas de saída.  
  
 Essa transformação tem várias entradas e apenas uma saída. Não dá suporte a uma saída de erro.  
  
## <a name="configuration-of-the-union-all-transformation"></a>Configuração da transformação Unir Tudo  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Transformação Union All** , consulte [Editor de Transformação Union All](../../../integration-services/data-flow/transformations/union-all-transformation-editor.md).  
  
 Para obter mais informações sobre as propriedades que podem ser definidas programaticamente, consulte [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796).  
  
 Para obter mais informações sobre como definir propriedades, clique em um dos seguintes tópicos:  
  
-   [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
 [Mesclar dados por meio da transformação Unir Tudo](../../../integration-services/data-flow/transformations/merge-data-by-using-the-union-all-transformation.md)  
  
  
