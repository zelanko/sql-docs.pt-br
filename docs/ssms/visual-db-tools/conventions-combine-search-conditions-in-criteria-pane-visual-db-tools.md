---
title: "Convenções para combinar condições de pesquisa no painel Critérios | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- search conditions [SQL Server], combining
- precedence [SQL Server], Criteria pane
- search criteria [SQL Server], combining conditions
- multiple OR clauses
- combining search conditions
- OR operator
- AND, Criteria pane
- multiple AND clauses
ms.assetid: d4859be5-ff5b-48b2-a101-ad40c6dbcc68
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8d99326f7d045aff95bf753d7f1ff68826f313af
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/17/2018
---
# <a name="conventions-for-combining-search-conditions-in-the-criteria-pane-visual-database-tools"></a>Convenções para combinar critérios de pesquisa no painel de Critérios (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Você pode criar consultas que incluam qualquer número de critérios de pesquisa, interligadas com qualquer número de operadores AND e OR. Uma consulta com uma combinação de cláusulas AND e OR pode se tornar complexa, então é útil entender como tal consulta é interpretada quando você a executa, e como tal consulta é representada no [Painel Critérios](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md) e no [Painel SQL](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md).  
  
> [!NOTE]  
> Para obter detalhes sobre os critérios de pesquisa que contêm apenas um operador AND ou OR, consulte [Especificar vários critérios de pesquisa para uma coluna &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-multiple-search-conditions-for-one-column-visual-database-tools.md) e [Especificar vários critérios de pesquisa para várias colunas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-multiple-search-conditions-for-multiple-columns-visual-database-tools.md).  
  
Abaixo você achará informações sobre:  
  
-   A precedência de AND e OR em consultas que contenham ambos.  
  
-   Como as condições em cláusulas AND e OR se relacionam logicamente uma a outra.  
  
-   Como os Designers de Consulta e Exibição representam nas consultas do Painel de Critérios que contenham ambos AND e OR  
  
Para ajudá-lo a entender a discussão abaixo, imagine que está trabalhando com uma tabela `employee` contendo as colunas `hire_date`, `job_lvl`, e `status`. Os exemplos supõem que você precisa conhecer informações como quanto tempo um funcionário trabalha para a companhia (quer dizer, qual a data de contratação do funcionário), que tipo de tarefa que o funcionário executa (qual é o nível do emprego) e o estado do empregado (por exemplo, aposentado).  
  
## <a name="precedence-of-and-and-or"></a>Precedência de AND e OR  
Quando uma consulta é executada, ela primeiro avalia as cláusulas unidas com AND, e então aquelas unidas com OR.  
  
> [!NOTE]  
> O operador NOT tem precedência sobre AND e OR.  
  
Por exemplo, para encontrar quais funcionários estão trabalhando para a empresa por mais de cinco anos em funções de níveis menores, ou funcionários com funções de níveis intermediários, sem levar em contar as suas datas de contratação, você pode construir uma cláusula WHERE como a seguinte:  
  
```  
WHERE   
   hire_date < '01/01/95' AND   
   job_lvl = 100 OR  
   job_lvl = 200  
```  
  
Para anular a precedência padrão de AND sobre OR, você pode pôr parênteses ao redor das condições específicas no painel SQL. As condições entre parênteses são sempre avaliadas em primeiro lugar. Por exemplo, para encontrar todos os funcionários trabalhando para a empresa por mais de cinco anos tanto em funções de nível inferior quanto de níveis intermediários, você pode construir cláusulas WHERE como nos exemplos seguintes:  
  
```  
WHERE   
   hire_date < '01/01/95' AND   
   (job_lvl = 100 OR job_lvl = 200)  
```  
  
> [!TIP]  
> É recomendado que, para uma maior clareza, você sempre inclua parênteses ao combinar cláusulas AND e OR em vez de confiar na precedência padrão.  
  
## <a name="how-and-works-with-multiple-or-clauses"></a>Como AND trabalha com múltiplas cláusulas OR  
Compreender como as cláusulas AND e OR são relacionadas quando combinadas pode ajudar você a construir e entender consultas complexas no Designer de Exibição e Consulta.  
  
Se você vincular condições múltiplas que usam AND, o primeiro conjunto de condições vinculadas à AND se aplicará a todas as condições no segundo conjunto. Em outras palavras, uma condição vinculada à AND a outra condição é distribuída a todas as condições no segundo conjunto. Por exemplo, a representação esquemática seguinte mostra uma condição AND vinculada a um conjunto de condições OR:  
  
```  
A AND (B OR C)  
```  
  
A representação acima é logicamente equivalente à representação esquemática seguinte, que mostra como a condição AND é distribuída ao segundo conjunto de condições:  
  
```  
(A AND B) OR (A AND C)  
```  
  
Este princípio distributivo afeta como você usa o Designer de Consulta e Exibição. Por exemplo, imagine que você pretenda localizar todo os funcionários que trabalhe para a empresa há mais de cinco anos, em cargos de nível inferior ou intermediário. Você entra a seguinte cláusula WHERE na instrução do painel SQL:  
  
```  
WHERE (hire_date < '01/01/95' ) AND   
   (job_lvl = 100 OR job_lvl = 200)  
```  
  
A cláusula vinculada com AND se aplica a ambas as cláusulas vinculadas com OR. Um modo explícito para expressar isto é repetir a condição AND uma vez para cada condição na cláusula OR. A instrução seguinte é mais explícita (e maior) que a instrução anterior, mas é logicamente equivalente à ela:  
  
```  
WHERE    (hire_date < '01/01/95' ) AND  
  (job_lvl = 100) OR   
  (hire_date < '01/01/95' ) AND   
  (job_lvl = 200)  
```  
  
O princípio de distribuir cláusulas AND para cláusulas OR vinculadas se aplica, não importando quantas condições individuais estão envolvidas. Por exemplo, imagine que você queira localizar os funcionários, de funções de nível superior ou intermediário,que trabalhem para a empresa há mais de cinco anos ou que estejam aposentados. A cláusula WHERE pode parecer assim:  
  
```  
WHERE   
   (job_lvl = 200 OR job_lvl = 300) AND  
   (hire_date < '01/01/95' ) OR (status = 'R')  
```  
  
Após as condições vinculadas com AND tiverem sido distribuídas, a cláusula WHERE se parecerá com:  
  
```  
WHERE   
   (job_lvl = 200 AND hire_date < '01/01/95' ) OR  
   (job_lvl = 200 AND status = 'R') OR  
   (job_lvl = 300 AND hire_date < '01/01/95' ) OR  
   (job_lvl = 300 AND status = 'R')  
```  
  
## <a name="how-multiple-and-and-or-clauses-are-represented-in-the-criteria-pane"></a>Como são representadas as cláusulas múltiplas AND e OR no Painel de Critérios  
O Designer de Consulta e Exibição representa os critérios de pesquisa no [Painel Critérios](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md). Porém, em alguns casos que envolvem cláusulas múltiplas vinculadas com AND e OR, a representação no Painel de Critérios pode não ser o que você espera. Além disso, se você modificar sua consulta no Painel Critérios ou no [Painel Diagrama](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md), poderá descobrir que a instrução SQL que você inseriu foi alterada.  
  
Em geral, estas regras ditam como as cláusulas AND e OR aparecem no Painel de Critérios:  
  
-   Todas as condições vinculadas com AND aparecem na coluna de grade **Filtro** ou na mesma coluna **Ou...** .  
  
-   Todas as condições vinculadas com OR aparecem em colunas **Ou...** separadas.  
  
-   Se o resultado lógico de uma combinação de cláusulas AND e OR cláusulas for que AND seja distribuído em várias cláusulas OR, o Painel de Critérios representará isto explicitamente repetindo a cláusula AND tantas vezes quanto necessário.  
  
Por exemplo, no painel SQL você pode criar um critério de pesquisa como o seguinte, no qual duas cláusulas vinculadas com AND têm precedência sobre uma terceira vinculada com OR:  
  
```  
WHERE (hire_date < '01/01/95' ) AND   
  (job_lvl = 100) OR   
  (status = 'R')  
```  
  
O Designer de Consulta e Exibição representa essa cláusula WHERE no Painel de Critérios como segue:  
  
![Precedência da cláusula OR no painel Critérios](../../ssms/visual-db-tools/media/vs_criteriapane1.gif "Precedência da cláusula OR no painel Critérios")  
  
Porém, se as cláusulas OR têm precedência sobre uma cláusula AND, a cláusula AND é repetida para cada cláusula OR. Isto faz com que a cláusula AND seja distribuída para cada cláusula OR. Por exemplo, no painel SQL você poderá criar uma cláusula WHERE como a seguinte:  
  
```  
WHERE (hire_date < '01/01/95' ) AND   
  ( (job_lvl = 100) OR   
  (status = 'R') )  
```  
  
O Designer de Consulta e Exibição representa essa cláusula WHERE no Painel de Critérios como segue:  
  
![Múltiplas cláusulas AND e OR no painel Critérios](../../ssms/visual-db-tools/media/vs_criteriapane2.gif "Múltiplas cláusulas AND e OR no painel Critérios")  
  
Se as cláusulas vinculadas OR envolverem só uma coluna de dados, o Designer de Consulta e Exibição pode colocar a toda a cláusula OR em uma única célula da grade, evitando a necessidade de repetir a cláusula AND. Por exemplo, no painel SQL você poderá criar uma cláusula WHERE como a seguinte:  
  
```  
WHERE (hire_date < '01/01/95' ) AND   
  ((status = 'R') OR (status = 'A'))  
```  
  
O Designer de Consulta e Exibição representa essa cláusula WHERE no Painel de Critérios como segue:  
  
![Cláusulas OR vinculadas definidas no painel Critérios](../../ssms/visual-db-tools/media/vs_criteriapane3.gif "Cláusulas OR vinculadas definidas no painel Critérios")  
  
Se você fizer uma mudança na consulta (como alterar um dos valores no Painel de Critérios), o Designer de Consulta e Exibição recriará a instrução SQL no painel SQL. A instrução SQL recriada se assemelhará à exibição do Painel de Critérios em vez de sua instrução original. Por exemplo, se o Painel de Critérios contiver cláusulas AND distribuídas, a instrução resultante no painel SQL será recriada com cláusulas AND explicitamente distribuídas. Para detalhes, consulte "Como AND funciona com múltiplas cláusulas OR" anteriormente neste tópico.  
  
## <a name="see-also"></a>Consulte Também  
[Especificar critérios de pesquisa &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
