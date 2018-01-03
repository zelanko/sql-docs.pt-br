---
title: "Especificar condições de pesquisa (Visual Database Tools) | Microsoft Docs"
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
- choosing search criteria
- search conditions [SQL Server], specifying
- search criteria [SQL Server], specifying conditions
ms.assetid: 18e2c759-68ec-4efe-b208-2f73418cd9bd
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 773ae71e94702da89b1e4a9cea350e1307881af6
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="specify-search-conditions-visual-database-tools"></a>Especificar condições de pesquisa (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Você pode especificar as linhas de dados que aparecem em sua consulta especificando condições de pesquisa. Por exemplo, se você estiver consultando uma tabela `employee` , será possível especificar que você quer localizar apenas os funcionários que trabalham em uma determinada região.  
  
Você especifica critérios de pesquisa usando uma expressão. Geralmente, a expressão consiste em um operador e um valor de pesquisa. Por exemplo, para localizar os funcionários em uma região de vendas em particular, você poderia especificar o seguinte critério de pesquisa para a coluna `region` :  
  
```  
='UK'  
```  
  
> [!NOTE]  
> Se você estiver trabalhando com várias tabelas, o Designer de Consulta e Exibição examinará cada critério de pesquisa para determinar se a comparação que você está fazendo resulta em uma junção. Nesse caso, o Designer de Consulta e Exibição converte automaticamente o critério de pesquisa em uma junção. Para obter mais informações, consulte [Unir tabelas automaticamente &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-tables-automatically-visual-database-tools.md).  
  
### <a name="to-specify-search-conditions"></a>Para especificar os critérios de pesquisa  
  
1.  Se você ainda não o fez, adicione as colunas ou expressões que você quer usar no seu critério de pesquisa ao painel Critérios.  
  
    Se você estiver criando uma consulta selecionada e não quiser que as colunas ou as expressões pesquisadas apareçam na saída da consulta, limpe a coluna **Saída** de cada coluna ou expressão e as remova como colunas de saída.  
  
2.  Localize a linha que contém a coluna ou expressão de dados a ser pesquisada e, depois, na coluna **Filtro** insira um critério de pesquisa.  
  
    > [!NOTE]  
    > Se você não inserir um operador, o Designer de Consulta e Exibição inserirá automaticamente o operador de igualdade "=".  
  
O Designer de Consulta e Exibição atualiza a instrução SQL no [painel SQL](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md) adicionado ou modificando a cláusula WHERE.  
  
## <a name="see-also"></a>Consulte Também  
[Regras para inserção de valores de pesquisa &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/rules-for-entering-search-values-visual-database-tools.md)  
[Especificar critérios de pesquisa &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
