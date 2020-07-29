---
title: Incluir ou excluir linhas
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search criteria [SQL Server], excluding rows
- search criteria [SQL Server], WHERE clause
- included rows
- search conditions [SQL Server], HAVING clause
- search criteria [SQL Server], including rows
- row excluded in search [SQL Server]
- search criteria [SQL Server], HAVING clause
- search conditions [SQL Server], WHERE clause
- row included in search [SQL Server]
- excluding rows
ms.assetid: ba4e1202-31a2-444d-8365-c68a530ef223
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 2a58e332836d99b236eb0a09916ec6f16f2a8761
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86011726"
---
# <a name="include-or-exclude-rows-visual-database-tools"></a>Incluir ou excluir linhas (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Para restringir o número de linhas que uma consulta SELECT deve retornar, crie critérios de pesquisa ou de filtro. No SQL, os critérios de pesquisa aparecem na cláusula WHERE da instrução, ou quando se está criando uma consulta de agregação na cláusula HAVING.  
  
> [!NOTE]  
> É igualmente possível usar critérios de pesquisa para indicar quais linhas são afetadas por consultas Atualizar, Inserir Resultados, Inserir Valores, Excluir ou Criar Tabela.  
  
Quando a consulta é executada, o [!INCLUDE[ssDE](../../includes/ssde_md.md)] examina e aplica o critério de pesquisa a todas as linhas das tabelas que você está pesquisando. Se a linha atender aos critérios, será incluída na consulta. Por exemplo, um critério de pesquisa que localizasse todos os funcionários de uma determinada região poderia ser:  
  
```  
region = 'UK'  
```  
  
Para estabelecer os critérios de inclusão de linhas em resultado, vários critérios de pesquisa podem ser utilizados. Por exemplo, o critério de pesquisa a seguir consiste em dois critérios de pesquisa. A consulta incluirá uma linha no conjunto de resultados apenas se aquela linha atender às condições.  
  
```  
region = 'UK' AND product_line = 'Housewares'  
```  
  
Você pode combinar essas condições com AND ou OR. O exemplo anterior utiliza AND. Por outro lado, o critério a seguir usa OR. O conjunto de resultados incluirá todas as linhas que atenderem um ou outro ou a ambos os critérios de pesquisa:  
  
```  
region = 'UK' OR product_line = 'Housewares'  
```  
  
É possível combinar critérios de pesquisa até mesmo em uma única coluna. Por exemplo, o critério seguinte combina duas condições na coluna de região:  
  
```  
region = 'UK' OR region = 'US'  
```  
  
Para obter detalhes sobre como combinar critérios de pesquisa, consulte os seguintes tópicos:  
  
-   [Convenções para combinar critérios de pesquisa no painel Critérios &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)  
  
-   [Especificar vários critérios de pesquisa para uma coluna &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-multiple-search-conditions-for-one-column-visual-database-tools.md)  
  
-   [Especificar vários critérios de pesquisa para várias colunas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-multiple-search-conditions-for-multiple-columns-visual-database-tools.md)  
  
-   [Combinar condições quando AND tem precedência &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/combine-conditions-when-and-has-precedence-visual-database-tools.md)  
  
-   [Combinar condições quando OR tem precedência &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/combine-conditions-when-or-has-precedence-visual-database-tools.md)  
  
## <a name="examples"></a>Exemplos  
A seguir, alguns exemplos de consultas que usam vários operadores e critérios de linha:  
  
-   **Literal** Valor de texto único, numérico, de data ou lógico. O exemplo a seguir utiliza um literal para localizar todas as linhas de funcionários do Reino Unido:  
  
    ```  
    WHERE region = 'UK'  
    ```  
  
-   **Referência de coluna** Compara os valores de uma coluna com os valores de outra. O exemplo a seguir pesquisa uma tabela de `products` para todas as linhas nas quais o valor do custo de produção seja inferior ao custo de remessa:  
  
    ```  
    WHERE prod_cost < ship_cost  
    ```  
  
-   **Função** Referência a uma função que um back-end de banco de dados pode resolver para calcular o valor da pesquisa. A função pode ser uma função definida pelo servidor de banco de dados ou uma função definida pelo usuário que retorne um valor escalar. O exemplo seguinte pesquisa os pedidos feitos hoje (a função GETDATE( ) retorna dados atuais):  
  
    ```  
    WHERE order_date = GETDATE()  
    ```  
  
-   **NULL** O exemplo seguinte pesquisa uma tabela `authors` de todos os autores que têm um nome no arquivo:  
  
    ```  
    WHERE au_fname IS NOT NULL  
    ```  
  
-   **Cálculo** O resultado de um cálculo que pode envolver literais, referências de coluna ou outras expressões. O exemplo seguinte pesquisa uma tabela de `products` para localizar todas as linhas nas quais o preço de vendas no varejo é superior a duas vezes o custo de produção:  
  
    ```  
    WHERE sales_price > (prod_cost * 2)  
    ```  
  
## <a name="see-also"></a>Consulte Também  
[Tópicos de instruções de como criar consultas e exibições &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Especificar critérios de pesquisa &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[Consultar com parâmetros &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-parameters-visual-database-tools.md)  
  
