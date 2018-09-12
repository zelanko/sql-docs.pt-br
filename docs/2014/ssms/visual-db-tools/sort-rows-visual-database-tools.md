---
title: Classificar Linhas (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- sorting rows [SQL Server]
- sorting query results [SQL Server]
ms.assetid: 780ef467-f96e-4373-8235-6dacbedb05a2
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 611cae35eb3da42f1a9e5772ec6c4b2e148cb730
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43815852"
---
# <a name="sort-rows-visual-database-tools"></a>Classificar linhas (Visual Database Tools)
  Você pode classificar linhas em um resultado de consulta. Isto é, você pode nomear uma coluna particular ou conjunto de colunas cujos valores determinam a classificação das linhas no conjunto de resultados.  
  
> [!NOTE]  
>  A ordem de classificação é determinada em parte pela sequência de agrupamento da coluna. Você pode alterar a sequência de agrupamento na [Caixa de Diálogo de Agrupamento](visual-database-tools.md).  
  
 Existem vários modos onde você pode classificar resultados de consulta:  
  
-   **Você pode organizar linhas em ordem crescente ou decrescente** . Por padrão, o SQL usa colunas classificar por para organizar linhas em ordem crescente. Por exemplo, para organizar os títulos de livros por preço crescente, simplesmente classifique as linhas pela coluna de preço. O SQL resultante pode ter esta aparência:  
  
    ```  
    SELECT *  
    FROM titles  
    ORDER BY price  
  
    ```  
  
     Por outro lado, se você quiser organizar os títulos com os livros mais caros primeiro, você poderá especificar expressamente uma classificação de primeiro os mais caros. Isto é, você indica se as linhas de resultado devem ser organizadas pelos valores decrescentes da coluna de preço. O SQL resultante pode ter esta aparência:  
  
    ```  
    SELECT *  
    FROM titles  
    ORDER BY price DESC  
  
    ```  
  
-   **Você pode fazer a classificação por várias colunas** .   Por exemplo, você pode criar um conjunto de resultados com uma linha para cada autor, classificando primeiro por estado e, em seguida, por cidade. O SQL resultante pode ter esta aparência:  
  
    ```  
    SELECT *  
    FROM authors   
    ORDER BY state, city  
  
    ```  
  
-   **Você pode classificar por colunas que não aparecem no conjunto de resultados** .   Por exemplo, você pode criar um conjunto de resultados com os títulos mais caros primeiro, mesmo se os preços não aparecerem. O SQL resultante pode ter esta aparência:  
  
    ```  
    SELECT title_id, title  
    FROM titles  
    ORDER BY price DESC  
  
    ```  
  
-   **Você pode classificar por colunas derivadas** .   Por exemplo, você pode criar um conjunto de resultados onde cada linha contenha um título de livro – com os livros que pagam royalty mais alto por cópia aparecendo primeiro. O SQL resultante pode ter esta aparência:  
  
    ```  
    SELECT title, price * royalty / 100 as royalty_per_unit  
    FROM titles  
    ORDER BY royalty_per_unit DESC  
  
    ```  
  
     (A fórmula para calcular royalty que cada livro ganha por cópia está destacada.)  
  
     Para calcular uma coluna derivada, você pode usar sintaxe SQL, como no exemplo anterior, ou pode usar uma função definida pelo usuário que retorna um valor escalar. Para obter mais informações sobre funções definidas pelo usuário, consulte a documentação do SQL Server.  
  
-   **Você pode classificar linhas agrupadas** .   Por exemplo; você pode criar um conjunto de resultados onde cada linha descreve uma cidade, mais o número de autores naquela cidade – com as cidades contendo muitos autores que aparecem primeiro. O SQL resultante pode ter esta aparência:  
  
    ```  
    SELECT city, state, COUNT(*)  
    FROM authors  
    GROUP BY city, state  
    ORDER BY COUNT(*) DESC, state  
  
    ```  
  
     Observe que a consulta usa `state` como uma coluna de classificação secundária. Assim, se dois estados tiverem o mesmo número de autores, esses estados aparecerão em ordem alfabética.  
  
-   **Você pode classificar usando dados internacionais** .   Isto é, você pode classificar uma coluna usando convenções de exame que diferem das convenções padrão daquela coluna. Por exemplo, você pode escrever uma consulta que recupera todos os títulos de livro de Jaime Patiño. Para exibir os títulos em ordem alfabética, você usa uma sequência de exame espanhol para a coluna de título. O SQL resultante pode ter esta aparência:  
  
    ```  
    SELECT title  
    FROM   
        authors   
        INNER JOIN   
            titleauthor   
            ON authors.au_id   
            =  titleauthor.au_id   
            INNER JOIN  
                titles   
                ON titleauthor.title_id   
                =  titles.title_id   
    WHERE   
         au_fname = 'Jaime' AND   
         au_lname = 'Patiño'  
    ORDER BY   
         title COLLATE SQL_Spanish_Pref_CP1_CI_AS  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Classificar e agrupar resultados da consulta &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)   
 [Tópicos de instruções de como criar consultas e exibições &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
