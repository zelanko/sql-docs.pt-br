---
title: "Excluir uma tabela (SSAS tabular) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: be4ed45f-fde3-466c-9869-49bd3ddb505e
caps.latest.revision: 9
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 9
---
# Excluir uma tabela (SSAS tabular)
  No designer de modelo, você pode excluir tabelas em seu banco de dados de espaço de trabalho modelo que você não precisa mais. A exclusão de uma tabela não afeta os dados de origem originais, somente os dados que você importou e com os quais estava trabalhando. Não é possível desfazer a exclusão de uma tabela.  
  
### Para excluir uma tabela  
  
-   Clique com o botão direito do mouse na guia, na parte inferior do designer de modelo para a tabela que você deseja excluir, e clique em **Excluir**.  
  
## Considerações ao excluir tabelas  
  
-   Quando você excluir uma tabela, a guia inteira na qual a tabela se encontra será excluída.  
  
-   Se houver uma medida associada a essa tabela, a definição da medida também será excluída.  
  
-   Se você criou qualquer coluna calculada usando essa tabela, as colunas dessa tabela também serão excluídas; as colunas calculadas de outras tabelas que usam colunas da tabela excluída exibirão um erro.  
  
## Consulte também  
 [Tabelas e colunas &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)  
  
  