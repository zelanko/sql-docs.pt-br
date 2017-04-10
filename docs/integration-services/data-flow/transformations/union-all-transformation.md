---
title: "Transforma&#231;&#227;o Unir Tudo | Microsoft Docs"
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
  - "sql13.dts.designer.unionalltrans.f1"
helpviewer_keywords: 
  - "mesclando conjuntos de dados [Integration Services]"
  - "combinando conjuntos de dados"
  - "transformação Unir Tudo"
  - "conjuntos de dados [Serviços de Integração], mesclagem"
ms.assetid: 942e4b90-9c41-4e9c-a6f3-80b3afe57f2f
caps.latest.revision: 39
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 39
---
# Transforma&#231;&#227;o Unir Tudo
  A transformação Union All combina várias entradas em apenas uma saída. Por exemplo, as saídas provenientes de cinco origens de Arquivo Simples diferentes podem ser aplicadas à transformação Unir Tudo e combinadas em apenas uma saída.  
  
## Entradas e saídas  
 As entradas da transformação são adicionadas à saída da transformação uma após a outra, sem reordenação das linhas. Se o pacote requerer uma saída ordenada, você deve usar a transformação Merge em vez da Union All.  
  
 A primeira entrada que você conectar à transformação Union All será a entrada da qual a transformação criará a saída. As colunas nas entradas que você conectar subsequentemente à transformação serão mapeadas para as colunas, na saída da transformação.  
  
 Para mesclar as entradas, você deve mapear as colunas nas entradas para as colunas na saída. Uma coluna com pelo menos uma entrada deve ser mapeada para cada coluna de saída. O mapeamento entre duas colunas requer que seus metadados tenham correspondência. Por exemplo, as colunas mapeadas devem ter o mesmo tipo de dados.  
  
 Se as colunas mapeadas contiverem dados de cadeia de caracteres e a coluna de saída for mais curta que a de entrada, a coluna da saída será aumentada automaticamente para comportar a coluna de entrada. As colunas de entrada que não forem mapeadas para as de saída serão definidas com valores nulos nas colunas de saída.  
  
 Essa transformação tem várias entradas e apenas uma saída. Não dá suporte a uma saída de erro.  
  
## Configuração da transformação Unir Tudo  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Transformação Union All**, consulte [Editor de Transformação Union All](../../../integration-services/data-flow/transformations/union-all-transformation-editor.md).  
  
 Para obter mais informações sobre as propriedades que podem ser definidas programaticamente, consulte [Common Properties](../Topic/Common%20Properties.md).  
  
 Para obter mais informações sobre como definir propriedades, clique em um dos seguintes tópicos:  
  
-   [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## Tarefas relacionadas  
 [Mesclar dados por meio da transformação Unir Tudo](../../../integration-services/data-flow/transformations/merge-data-by-using-the-union-all-transformation.md)  
  
  