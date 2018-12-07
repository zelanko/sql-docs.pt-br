---
title: Criar autojunções manualmente (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- self-joins
- manual joins [SQL Server]
- joins [SQL Server], self
ms.assetid: 910ed516-cb84-481b-95d0-cba3e89afdba
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cd175d4d66cfea79f1449ae7da9d06d5c9f247c3
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52542279"
---
# <a name="create-self-joins-manually-visual-database-tools"></a>Criar autojunções manualmente (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
A autojunção de uma tabela pode ser feita, mesmo se a tabela não tiver uma relação reflexiva no banco de dados. Por exemplo, você pode usar uma autojunção para encontrar pares de autores que moram na mesma cidade.  
  
Como com qualquer junção, uma autojunção requer pelo menos duas tabelas. A diferença é que, em vez de acrescentar uma segunda tabela à consulta, você adicionar uma segunda instância da mesma tabela. Dessa forma, você pode comparar uma coluna na primeira instância da tabela para a mesma coluna na segunda instância, o que permite comparar os valores em uma coluna entre si. O [Designer de Consulta e Exibição](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) atribui um alias à segunda instância da tabela.  
  
Por exemplo, se você estiver criando uma autojunção para encontrar todos os pares de autores em Berkeley, você comparará a coluna `city` na primeira instância da tabela com a coluna `city` na segunda instância. A consulta resultante pode ter a seguinte aparência:  
  
```  
SELECT   
         authors.au_fname,   
         authors.au_lname,   
         authors1.au_fname AS Expr2,   
         authors1.au_lname AS Expr3  
      FROM   
         authors   
            INNER JOIN  
            authors authors1   
               ON authors.city   
                = authors1.city  
      WHERE  
         authors.city = 'Berkeley'  
```  
  
A criação de uma autojunção normalmente requer várias condições de junção. Para entender o porquê, considere o resultado da consulta anterior:  
  
```  
Cheryl Carson       Cheryl Carson  
   Abraham Bennet      Abraham Bennet  
   Cheryl Carson       Abraham Bennet  
   Abraham Bennet      Cheryl Carson  
```  
  
A primeira linha é inútil; indica que Cheryl Carson mora na mesma cidade de Cheryl Carson. A segunda linha é igualmente inútil. Para eliminar esses dados inúteis, você adiciona outra condição que retém somente as linhas de resultado onde os nomes de dois autores descrevem autores diferentes. A consulta resultante pode ter a seguinte aparência:  
  
```  
SELECT   
         authors.au_fname,   
         authors.au_lname,   
         authors1.au_fname AS Expr2,   
         authors1.au_lname AS Expr3  
      FROM   
         authors   
            INNER JOIN  
            authors authors1   
               ON authors.city   
                = authors1.city  
               AND authors.au_id  
                <> authors1.au_id  
      WHERE  
         authors.city = 'Berkeley'  
```  
  
O conjunto de resultados é aprimorado.  
  
```  
Cheryl Carson       Abraham Bennet  
   Abraham Bennet      Cheryl Carson  
```  
  
Mas as duas linhas de resultado são redundantes. A primeira diz que Carson mora na mesma cidade de Bennet, e a segunda diz que Bennet mora na mesma cidade de Carson. Para eliminar essa redundância, você pode alterar a segunda condição de junção de “não igual” para “menor que”. A consulta resultante pode ter a seguinte aparência:  
  
```  
SELECT   
         authors.au_fname,   
         authors.au_lname,   
         authors1.au_fname AS Expr2,   
         authors1.au_lname AS Expr3  
      FROM   
         authors   
            INNER JOIN  
            authors authors1   
               ON authors.city   
                = authors1.city  
               AND authors.au_id  
                < authors1.au_id  
      WHERE  
         authors.city = 'Berkeley'  
```  
  
E o conjunto de resultados tem a seguinte aparência:  
  
```  
Cheryl Carson       Abraham Bennet  
```  
  
### <a name="to-create-a-self-join-manually"></a>Para criar uma autojunção manualmente  
  
1.  Adicione ao painel [Diagrama](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md) a tabela ou o objeto com valor de tabela com os quais você deseja trabalhar.  
  
2.  Adicione a mesma tabela novamente, de forma que o painel Diagrama exiba a mesma tabela ou o mesmo objeto com valor de tabela duas vezes no painel Diagrama.  
  
    O Designer de Consulta e Exibição atribui um alias à segunda instância adicionando um número sequencial ao nome da tabela. Além disso, o Designer de Consulta e Exibição cria uma linha de junção entre as duas ocorrências da tabela ou do objeto com valor de tabela dentro do painel Diagrama.  
  
3.  Clique com o botão direito do mouse na linha de junção e escolha **Propriedades** no menu de atalho.  
  
4.  Na janela Propriedades, clique em **Condição e Tipo de Junção** e clique nas **reticências (…)** à direita da propriedade.  
  
5.  Na caixa de diálogo [Junção](../../ssms/visual-db-tools/join-dialog-box-visual-database-tools.md) , altere o operador de comparação entre as chaves primárias conforme requerido. Por exemplo, você pode alterar o operador para menor que (<).  
  
6.  Crie a condição de junção adicional (por exemplo, authors.zip = authors1.zip) arrastando o nome da coluna de junção primária na primeira ocorrência da tabela ou objeto com valor de tabela, soltando na coluna correspondente na segunda ocorrência.  
  
7.  Especifique outras opções para a consulta, como colunas de saída, critérios de pesquisa e ordem de classificação.  
  
## <a name="see-also"></a>Consulte Também  
[Criar autojunções automaticamente &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-self-joins-automatically-visual-database-tools.md)  
[Consultar com junções &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
