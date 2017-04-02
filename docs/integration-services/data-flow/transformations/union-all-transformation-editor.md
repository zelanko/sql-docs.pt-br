---
title: "Editor de Transforma&#231;&#227;o Union All | Microsoft Docs"
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
  - "sql13.dts.designer.unionalltransformation.f1"
helpviewer_keywords: 
  - "Editor de Transformação Union All"
ms.assetid: 32fbc1c1-da83-4684-9479-31fc3e2df98c
caps.latest.revision: 26
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 26
---
# Editor de Transforma&#231;&#227;o Union All
  Use a caixa de diálogo **Editor de Transformação Union All** para mesclar vários conjuntos de linhas de entrada em um único conjunto de linhas de saída. Incluindo a transformação Union All em um fluxo de dados, é possível mesclar dados de vários fluxos de dados, criar conjuntos de dados complexos aninhando transformações Union All e mesclar as linhas novamente após corrigir erros nos dados.  
  
 Para saber mais sobre a transformação Union All, consulte [Union All Transformation](../../../integration-services/data-flow/transformations/union-all-transformation.md).  
  
## Opções  
 **Nome da Coluna de Saída**  
 Digite um alias para cada coluna. O padrão é o nome da coluna de entrada da primeira entrada (referência); contudo, é possível escolher qualquer nome descritivo exclusivo.  
  
 **Union All Entrada 1**  
 Selecione a partir da lista de colunas de entrada disponíveis na primeira entrada (referência). Os metadados das colunas mapeadas devem ser correspondentes.  
  
 **Union All Entrada n**  
 Selecione a partir da lista de colunas de entrada disponíveis na segunda entrada e adicionais. Os metadados das colunas mapeadas devem ser correspondentes.  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Mesclar dados por meio da transformação Unir Tudo](../../../integration-services/data-flow/transformations/merge-data-by-using-the-union-all-transformation.md)   
 [Transformação Mesclar](../../../integration-services/data-flow/transformations/merge-transformation.md)   
 [Transformação Junção de Mesclagem](../../../integration-services/data-flow/transformations/merge-join-transformation.md)  
  
  