---
title: "Transforma&#231;&#227;o Mesclar | Microsoft Docs"
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
  - "sql13.dts.designer.mergetrans.f1"
helpviewer_keywords: 
  - "mesclando conjuntos de dados [Integration Services]"
  - "mesclando dados [Integration Services]"
  - "Transformação Mesclar"
  - "combinando conjuntos de dados"
  - "conjuntos de dados [Serviços de Integração], mesclagem"
ms.assetid: cff8690c-07ac-46a0-aab5-20bd4848c677
caps.latest.revision: 43
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 43
---
# Transforma&#231;&#227;o Mesclar
  A Transformação Mesclagem combina dois conjuntos de dados classificados em um único conjunto de dados. As linhas de cada conjunto de dados estão inseridas na saída com base em valores de suas colunas-chave.  
  
 Incluindo a Transformação Mesclar em um fluxo de dados, você poderá executar as seguintes tarefas:  
  
-   Mesclar dados de duas fontes de dados, tais como tabelas e arquivos.  
  
-   Criar conjuntos de dados complexos aninhando transformações de Mesclar.  
  
-   Volte a mesclar as filas depois de corrigir erros nos dados.  
  
 A Transformação Mesclar é semelhante às transformações do Union All. Use a transformação do Union All em vez da Transformação Mesclar nas situações seguintes:  
  
-   As entradas de transformação não estão ordenadas.  
  
-   A saída combinada não precisa ser classificada.  
  
-   A transformação tem mais de duas entradas.  
  
## Requisitos de entrada  
 A Transformação Mesclar requer dados classificados para suas entradas. Para obter mais informações sobre este requisito importante, consulte [Classificar dados para as transformações Mesclagem e Junção de Mesclagem](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).  
  
 A Transformação Mesclar também requer que as colunas mescladas em suas entradas tenham metadados coincidentes. Por exemplo, você não pode mesclar uma coluna que tenha um tipo de dados numéricos com uma coluna que tenha um tipo de dados de caracteres. Se os dados tiverem um tipo de dados de cadeia de caracteres, o comprimento da coluna na segunda entrada deve ser menor, ou igual, ao comprimento da coluna na primeira entrada com a qual é intercalado.  
  
 No Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)], a interface do usuário para a transformação Mesclar mapeia automaticamente as colunas que contém os mesmos metadados. É possível então mapear manualmente outras colunas que tenham tipos de dados compatíveis.  
  
 Esta transformação tem duas entradas e uma saída. Não dá suporte a uma saída de erro.  
  
## Configuração da Transformação Mesclar  
 Você pode definir propriedades por meio do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Transformação Mesclar**, consulte [Editor de Transformação Mesclar](../../../integration-services/data-flow/transformations/merge-transformation-editor.md).  
  
 Para obter mais informações sobre as propriedades que podem ser definidas programaticamente, clique em um dos tópicos a seguir:  
  
-   [Propriedades comuns](../Topic/Common%20Properties.md)  
  
-   [Propriedades personalizadas de Transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## Tarefas relacionadas  
 Para obter detalhes sobre como definir propriedades, consulte os tópicos a seguir:  
  
-   [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [Classificar dados para as transformações Mesclagem e Junção de Mesclagem](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## Consulte também  
 [Transformação Junção de Mesclagem](../../../integration-services/data-flow/transformations/merge-join-transformation.md)   
 [Transformação Unir Tudo](../../../integration-services/data-flow/transformations/union-all-transformation.md)   
 [Fluxo de Dados](../../../integration-services/data-flow/data-flow.md)   
 [Transformações do Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  