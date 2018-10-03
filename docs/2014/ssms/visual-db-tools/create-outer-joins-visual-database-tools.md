---
title: Criar junções externas (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- outer joins
- joins [SQL Server], outer
ms.assetid: 18de47b1-f936-427d-b852-fe6d20334f71
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 276c377b6963c2c58be26187079bc60bf619a90a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48141646"
---
# <a name="create-outer-joins-visual-database-tools"></a>Criar junções externas (Visual Database Tools)
  Por padrão, o [Designer de Consulta e Exibição](visual-database-tools.md) cria uma junção interna entre tabelas. As junções internas eliminam as linhas que não correspondem a uma linha da outra tabela. Entretanto, as junções externas retornam todas as linhas de pelo menos uma das tabelas ou exibições mencionadas na cláusula FROM, contanto que essas linhas atendam algum critério de pesquisa WHERE ou HAVING. Se você quiser incluir linhas de dados no conjunto de resultados que não tenha uma correspondência na tabela unida, será possível criar uma junção externa.  
  
 Quando você criar uma junção externa, a ordem em que as tabelas aparecem na instrução SQL (como refletido no painel SQL) é significante. A primeira tabela que você adiciona se torna a tabela "esquerda" e a segunda se torna a tabela "direita." (A ordem real em que as tabelas aparecem no [painel Diagrama](diagram-pane-visual-database-tools.md) não é significativa.) Quando você especificar uma junção externa esquerda ou direita, estará se referindo à ordem na qual as tabelas foram adicionadas à consulta e à ordem na qual elas aparecem na instrução SQL no [painel SQL](sql-pane-visual-database-tools.md).  
  
### <a name="to-create-an-outer-join"></a>Para criar uma junção externa  
  
1.  Crie a junção, automática ou manualmente. Para obter detalhes, consulte [Unir tabelas automaticamente &#40;Visual Database Tools&#41;](join-tables-automatically-visual-database-tools.md) ou [Unir tabelas manualmente &#40;Visual Database Tools&#41;](join-tables-manually-visual-database-tools.md).  
  
2.  Selecione a linha de junção no painel de diagrama e, em seguida, do **Designer de consulta** menu, escolha **selecionar todas as linhas da \<tablename >**, selecionando o comando que inclui a tabela cujo extra linhas que você deseja incluir.  
  
    -   Escolha a primeira tabela para criar uma junção externa esquerda.  
  
    -   Escolha a segunda tabela para criar uma junção externa direita.  
  
    -   Escolha ambas as tabelas para criar uma junção externa completa.  
  
 Quando você especificar uma junção externa, o Designer de Consulta e Exibição modificará a linha de junção para indicar uma junção externa.  
  
 Além disso, o Designer de Consulta e Exibição modifica a instrução SQL no painel SQL para refletir a mudança em tipo de junção, conforme mostrado na seguinte instrução:  
  
```  
SELECT employee.job_id, employee.emp_id,  
   employee.fname, employee.minit, jobs.job_desc  
FROM employee LEFT OUTER JOIN jobs ON   
    employee.job_id = jobs.job_id  
```  
  
 Como uma junção externa inclui linhas não correspondentes, você pode usá-la para encontrar linhas que violam as restrições de chave estrangeira. Para fazer isso, crie uma junção externa e, depois, adicione um critério de pesquisa para encontrar linhas em que a coluna de chave primária da tabela mais à direita seja nula. Por exemplo, a seguinte junção externa encontra linhas na tabela `employee` que não têm linhas correspondentes na tabela `jobs` :  
  
```  
SELECT employee.emp_id, employee.job_id  
FROM employee LEFT OUTER JOIN jobs   
   ON employee.job_id = jobs.job_id  
WHERE (jobs.job_id IS NULL)  
```  
  
## <a name="see-also"></a>Consulte também  
 [Consultar com junções &#40;Visual Database Tools&#41;](query-with-joins-visual-database-tools.md)   
 [Caixa de diálogo Unir &#40;Visual Database Tools&#41;](join-dialog-box-visual-database-tools.md)  
  
  
