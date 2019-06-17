---
title: Usar cláusulas HAVING e onde a mesma consulta (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search criteria [SQL Server], excluding rows
- search criteria [SQL Server], WHERE clause
- search conditions [SQL Server], HAVING clause
- row excluded in search [SQL Server]
- search criteria [SQL Server], HAVING clause
- HAVING clause, search criteria
- search conditions [SQL Server], WHERE clause
- WHERE clause, search criteria
- excluding rows
ms.assetid: 1e07cf56-b4b7-4c49-8ddd-c276812a7148
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f7aafcd72eff1d21dfe02c8957496398d327cf38
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63204634"
---
# <a name="use-having-and-where-clauses-in-the-same-query-visual-database-tools"></a>Usar cláusulas HAVING e WHERE na mesma consulta (Visual Database Tools)
  Em algumas instâncias, talvez você deseje excluir linhas individuais de grupos (usando uma cláusula WHERE) antes de aplicar um critério aos grupos como um todo (usando uma cláusula HAVING).  
  
 Uma cláusula HAVING é como uma cláusula WHERE, a diferença é que ela se aplica somente a grupos como um todo (ou seja, as linhas do conjunto de resultados que representam grupos), enquanto a cláusula WHERE se aplica a linhas individuais. Uma consulta pode conter uma cláusula WHERE e uma cláusula HAVING. Nesse caso:  
  
-   A cláusula WHERE é aplicada primeiro às linhas individuais nas tabelas ou objetos com valor de tabela no painel Diagrama. Apenas as linhas que atendem os critérios na cláusula WHERE são agrupadas.  
  
-   A cláusula HAVING é aplicada às linhas no conjunto de resultados. Somente os grupos que atendem os critérios de HAVING são exibidos na saída da consulta. Você pode aplicar apenas uma cláusula HAVING em colunas que também são exibidas na cláusula GROUP BY ou em uma função de agregação.  
  
 Por exemplo, imagine que você está unindo as tabelas `titles` e `publishers` para criar uma consulta que mostra o preço médio do livro de um conjunto de editoras. Você quer ver o preço médio de um único conjunto específico de editoras, talvez somente as editoras no estado da Califórnia. Além disso, desejar ver o preço médio apenas se estiver acima de R$ 10,00.  
  
 Você pode definir o primeiro critério incluindo uma cláusula WHERE, que descarta todas as editoras que não estejam na Califórnia, antes de calcular os preços médios. O segundo critério requer uma cláusula HAVING, porque o critério está baseado nos resultados de agrupamento e resumo dos dados. A instrução SQL resultante se parecerá com esta:  
  
```  
SELECT titles.pub_id, AVG(titles.price)  
FROM titles INNER JOIN publishers  
   ON titles.pub_id = publishers.pub_id  
WHERE publishers.state = 'CA'  
GROUP BY titles.pub_id  
HAVING AVG(price) > 10  
```  
  
 Você pode criar cláusulas HAVING e WHERE no painel Critérios. Por padrão, se você especificar um critério de pesquisa para uma coluna, o critério se tornará parte da cláusula HAVING. Porém, você pode alterar o critério para ser uma cláusula WHERE.  
  
 Você pode criar uma cláusula WHERE e uma cláusula HAVING envolvendo a mesma coluna. Para fazer isso, você deve adicionar a coluna duas vezes ao painel Critérios e, depois, especificar uma instância como parte da cláusula HAVING e a outra instância como parte da cláusula WHERE.  
  
### <a name="to-specify-a-where-condition-in-an-aggregate-query"></a>Para especificar um critério WHERE em uma consulta de agregação  
  
1.  Especifique os grupos para a sua consulta. Para obter detalhes, veja [Agrupar linhas em resultados da consulta &#40;Visual Database Tools&#41;](visual-database-tools.md).  
  
2.  Se já não estiver no painel Critérios, adicione a coluna na qual você deseja basear o critério WHERE.  
  
3.  Limpe a coluna **Saída** , a menos que a coluna de dados faça parte da cláusula GROUP BY ou esteja incluída em uma função de agregação.  
  
4.  Na coluna **Filtro** , especifique o critério WHERE. O Designer de Consulta e Exibição adiciona o critério à cláusula HAVING da instrução SQL.  
  
    > [!NOTE]  
    >  A consulta mostrada no exemplo para esse procedimento une duas tabelas, `titles` e `publishers`.  
  
     Neste momento da consulta, a instrução SQL contém uma cláusula HAVING:  
  
    ```  
    SELECT titles.pub_id, AVG(titles.price)  
    FROM titles INNER JOIN publishers   
       ON titles.pub_id = publishers.pub_id  
    GROUP BY titles.pub_id  
    HAVING publishers.state = 'CA'  
    ```  
  
5.  Na coluna **Agrupar por** , selecione **Where** na lista de opções de grupo e resumo. O Designer de Consulta e Exibição remove o critério da cláusula HAVING na instrução SQL e a adiciona à cláusula WHERE.  
  
     A instrução SQL é alterada para incluir uma cláusula WHERE em vez de:  
  
    ```  
    SELECT titles.pub_id, AVG(titles.price)  
    FROM titles INNER JOIN publishers   
       ON titles.pub_id = publishers.pub_id  
    WHERE publishers.state = 'CA'  
    GROUP BY titles.pub_id  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Classificar e agrupar resultados da consulta &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)   
 [Resumir resultados da consulta &#40;Visual Database Tools&#41;](summarize-query-results-visual-database-tools.md)  
  
  
