---
title: "Transforma&#231;&#227;o Jun&#231;&#227;o de Mesclagem | Microsoft Docs"
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
  - "sql13.dts.designer.mergejointrans.f1"
helpviewer_keywords: 
  - "conjuntos de dados [Integration Services]"
  - "Transformação Junção de Mesclagem"
  - "conjuntos de dados [Integration Services], unindo"
  - "unindo conjuntos de dados [Integration Services]"
  - "junções [SQL Server], SSIS"
ms.assetid: cd8b0412-f83b-4bd2-b227-e53dcfd941a8
caps.latest.revision: 54
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 54
---
# Transforma&#231;&#227;o Jun&#231;&#227;o de Mesclagem
  A transformação Junção de Mesclagem fornece uma saída que é gerada unindo-se dois conjuntos de dados ordenados que usam uma junção FULL, LEFT ou INNER. Por exemplo, você pode usar uma associação de LEFT para unir uma tabela que inclui informações de produtos com uma tabela que lista o país/região no qual um produto foi fabricado. O resultado é uma tabela que lista todos os produtos e seu país/região de origem.  
  
 Você pode configurar a transformação Junção de Mesclagem das seguintes formas:  
  
-   Especificando se a associação é de FULL, LEFT ou de INNER.  
  
-   Especificando as colunas que a associação utiliza.  
  
-   Especificando se a transformação manipula valores nulos como iguais a outros nulos.  
  
    > [!NOTE]  
    >  Se os valores nulos não forem tratados como valores iguais, a transformação considera valores nulos como faz o Mecanismo de Banco de Dados do SQL Server.  
  
 Esta transformação tem duas entradas e uma saída. Não dá suporte a uma saída de erro.  
  
## Requisitos de entrada  
 A Transformação Junção de Mesclagem requer dados classificados para suas entradas. Para obter mais informações sobre este requisito importante, consulte [Classificar dados para as transformações Mesclagem e Junção de Mesclagem](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).  
  
## Requisições de junção  
 A transformação Junção de Mesclagem requer que as colunas unidas tenham metadados compatíveis. Por exemplo, você não pode unir uma coluna que tenha um tipo de dados numérico com uma coluna que tenha um tipo de dados de caracteres. Se os dados tiverem um tipo de dados de cadeia de caracteres, o comprimento da coluna na segunda entrada deve ser menor, ou igual, ao comprimento da coluna na primeira entrada com a qual é intercalado.  
  
## Limitação de buffer  
 Não é mais preciso configurar o valor da propriedade **MaxBuffersPerInput** , pois a Microsoft fez alterações que reduzem o risco de a transformação Junção de Mesclagem consumir memória excessiva. Esse problema algumas vezes ocorria quando as várias entradas da Junção de Mesclagem geravam dados a taxas irregulares.  
  
## Tarefas relacionadas  
 Você pode definir propriedades por meio do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer ou programaticamente.  
  
 Para obter mais informações sobre como definir as propriedades dessa transformação, clique em um dos tópicos a seguir:  
  
-   [Estender um conjunto de dados por meio da transformação Junção de Mesclagem](../../../integration-services/data-flow/transformations/extend-a-dataset-by-using-the-merge-join-transformation.md)  
  
-   [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [Classificar dados para as transformações Mesclagem e Junção de Mesclagem](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## Consulte também  
 [Editor de Transformação Mesclagem](../../../integration-services/data-flow/transformations/merge-join-transformation-editor.md)   
 [Transformação Mesclar](../../../integration-services/data-flow/transformations/merge-transformation.md)   
 [Transformação Unir Tudo](../../../integration-services/data-flow/transformations/union-all-transformation.md)   
 [Transformações do Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  