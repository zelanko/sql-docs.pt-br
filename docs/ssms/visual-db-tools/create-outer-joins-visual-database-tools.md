---
title: Criar junções externas (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- outer joins
- joins [SQL Server], outer
ms.assetid: 18de47b1-f936-427d-b852-fe6d20334f71
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cc45e2b6736c2423a8c4ec156075843991bf01e4
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="create-outer-joins-visual-database-tools"></a>Criar junções externas (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Por padrão, o [Designer de Consulta e Exibição](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) cria uma junção interna entre tabelas. As junções internas eliminam as linhas que não correspondem a uma linha da outra tabela. Entretanto, as junções externas retornam todas as linhas de pelo menos uma das tabelas ou exibições mencionadas na cláusula FROM, contanto que essas linhas atendam algum critério de pesquisa WHERE ou HAVING. Se você quiser incluir linhas de dados no conjunto de resultados que não tenha uma correspondência na tabela unida, será possível criar uma junção externa.  
  
Quando você criar uma junção externa, a ordem em que as tabelas aparecem na instrução SQL (como refletido no painel SQL) é significante. A primeira tabela que você adiciona se torna a tabela "esquerda" e a segunda se torna a tabela "direita." (A ordem real em que as tabelas aparecem no [painel Diagrama](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md) não é significativa.) Quando você especificar uma junção externa esquerda ou direita, estará se referindo à ordem na qual as tabelas foram adicionadas à consulta e à ordem na qual elas aparecem na instrução SQL no [painel SQL](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md).  
  
### <a name="to-create-an-outer-join"></a>Para criar uma junção externa  
  
1.  Crie a junção, automática ou manualmente. Para obter detalhes, consulte [Unir tabelas automaticamente &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-tables-automatically-visual-database-tools.md) ou [Unir tabelas manualmente &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-tables-manually-visual-database-tools.md).  
  
2.  Selecione a linha de junção no painel Diagrama e, depois, no menu **Designer de Consultas**, escolha **Selecionar Todas as Linhas de <tablename>**, selecionando o comando que inclui a tabela com as linhas extras que você deseja incluir.  
  
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
  
## <a name="see-also"></a>Consulte Também  
[Consultar com junções &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
[Caixa de diálogo Unir &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-dialog-box-visual-database-tools.md)  
  
