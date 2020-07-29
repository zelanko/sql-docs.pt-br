---
title: Criar subconsultas
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search criteria [SQL Server], subqueries
- nested queries
- subqueries [SQL Server], SQL pane
ms.assetid: 34f6b9b4-ca3a-4a4f-9594-36e513f1c547
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: ecee42edc9a27cb746615b7343c5014893e23c17
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85999993"
---
# <a name="create-subqueries-visual-database-tools"></a>Criar subconsultas (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Você pode usar os resultados de uma consulta como entrada para outra. Pode usar os resultados de uma subconsulta como uma instrução que usa a função IN( ), o operador EXISTS ou a cláusula FROM.  
  
Você pode criar uma subconsulta inserindo-a diretamente no painel de SQL ou copiando uma consulta e colando-a em outra.  
  
### <a name="to-define-a-subquery-in-the-sql-pane"></a>Para definir uma subconsulta no painel SQL  
  
1.  Crie a consulta primária.  
  
2.  No painel SQL, selecione a instrução SQL e use **Copiar** para mover a consulta para a Área de Transferência.  
  
3.  Inicie a consulta nova e use **Colar** para mover a primeira consulta à nova consulta da cláusula WHERE ou FROM.  
  
    Por exemplo, imagine que você tem duas tabelas, `products` e `suppliers`, e deseja criar uma consulta que mostre todos os produtos de fornecedores da Suécia. Crie a primeira consulta na tabela `suppliers` para achar todos os fornecedores suecos:  
  
    ```  
    SELECT supplier_id  
    FROM supplier  
    WHERE (country = 'Sweden')  
    ```  
  
    Use o comando Copiar para mover essa consulta à Área de Transferência. Crie a segunda consulta usando a tabela `products` , relacionando as informações que você precisa sobre os produtos:  
  
    ```  
    SELECT product_id, supplier_id, product_name  
    FROM products  
    ```  
  
    No painel SQL, adicione uma cláusula WHERE à segunda consulta e cole a primeira consulta da Área de Transferência. Delimite com parênteses a primeira consulta, de forma que o resultado final tenha esta aparência:  
  
    ```  
    SELECT product_id, supplier_id, product_name  
    FROM products  
    WHERE supplier_id IN  
       (SELECT supplier_id  
      FROM supplier  
      WHERE (country = 'Sweden'))  
    ```  
  
## <a name="see-also"></a>Consulte Também  
[Tipos de consulta com suporte &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[Especificar critérios de pesquisa &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
