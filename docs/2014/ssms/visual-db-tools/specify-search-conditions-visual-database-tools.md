---
title: Especificar condições de pesquisa (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- choosing search criteria
- search conditions [SQL Server], specifying
- search criteria [SQL Server], specifying conditions
ms.assetid: 18e2c759-68ec-4efe-b208-2f73418cd9bd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 75b29477c7ead402f06c9df2505a84636b906978
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63163951"
---
# <a name="specify-search-conditions-visual-database-tools"></a>Especificar condições de pesquisa (Visual Database Tools)
  Você pode especificar as linhas de dados que aparecem em sua consulta especificando critérios de pesquisa. Por exemplo, se você estiver consultando uma tabela `employee` , será possível especificar que você quer localizar apenas os funcionários que trabalham em uma determinada região.  
  
 Você especifica critérios de pesquisa usando uma expressão. Geralmente, a expressão consiste em um operador e um valor de pesquisa. Por exemplo, para localizar os funcionários em uma região de vendas em particular, você poderia especificar o seguinte critério de pesquisa para a coluna `region` :  
  
```  
='UK'  
```  
  
> [!NOTE]  
>  Se você estiver trabalhando com várias tabelas, o Designer de Consulta e Exibição examinará cada critério de pesquisa para determinar se a comparação que você está fazendo resulta em uma junção. Nesse caso, o Designer de Consulta e Exibição converte automaticamente o critério de pesquisa em uma junção. Para obter mais informações, consulte [Unir tabelas automaticamente &#40;Visual Database Tools&#41;](visual-database-tools.md).  
  
### <a name="to-specify-search-conditions"></a>Para especificar os critérios de pesquisa  
  
1.  Se você ainda não o fez, adicione as colunas ou expressões que você quer usar no seu critério de pesquisa ao painel Critérios.  
  
     Se você estiver criando uma consulta selecionada e não quiser que as colunas ou as expressões pesquisadas apareçam na saída da consulta, limpe a coluna **Saída** de cada coluna ou expressão e as remova como colunas de saída.  
  
2.  Localize a linha que contém a coluna ou expressão de dados a ser pesquisada e, depois, na coluna **Filtro** insira um critério de pesquisa.  
  
    > [!NOTE]  
    >  Se você não inserir um operador, o Designer de Consulta e Exibição inserirá automaticamente o operador de igualdade "=".  
  
 O Designer de Consulta e Exibição atualiza a instrução SQL no [painel SQL](sql-pane-visual-database-tools.md) adicionado ou modificando a cláusula WHERE.  
  
## <a name="see-also"></a>Consulte também  
 [Regras para inserção de valores de pesquisa &#40;Visual Database Tools&#41;](rules-for-entering-search-values-visual-database-tools.md)   
 [Especificar critérios de pesquisa &#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md)  
  
  
