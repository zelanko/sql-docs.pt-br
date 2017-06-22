---
title: "Regras para atualização de resultados (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- View Designer, Results pane
- updating query results
- Query Designer [SQL Server], Results pane
- Results pane
ms.assetid: de131ef0-ccbd-446f-9400-b93c7b8fa537
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f617973f041218de7b77b64350b8953dbaa0d149
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="rules-for-updating-results-visual-database-tools"></a>Regras para atualização de resultados (Visual Database Tools)
Em muitos casos, você pode atualizar o conjunto de resultados exibido no [Painel de Resultados](../../ssms/visual-db-tools/results-pane-visual-database-tools.md). Porém, em alguns casos você não pode.  
  
No geral, para poder atualizar os resultados, o [Designer de Consulta e Exibição](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) deve ter informações suficientes para identificar exclusivamente a linha na tabela. Um exemplo será se a consulta incluir uma chave primária na lista de saída. Além disso, você deve ter permissão suficiente para atualizar o banco de dados.  
  
Se sua consulta for baseada em uma exibição, você poderá atualizá-la. As mesmas diretrizes se aplicam, exceto que elas se aplicam às tabelas subjacentes na exibição, não somente à exibição em si.  
  
> [!NOTE]  
> O Designer de Consulta e Exibição não pode determinar antecipadamente se você pode atualizar um conjunto de resultados baseado em uma exibição. Então, ele mostra todas as exibições, embora talvez você não possa atualizá-las.  
  
A tabela seguinte resume instâncias específicas nas quais você poderá ou não atualizar os resultados de consulta no painel de Resultados. Em muitos casos, o banco de dados que você está usando é quem determina se você pode atualizar os resultados de consulta ou não.  
  
|Consulta|Os resultados podem ser atualizados?|  
|---------|---------------------------|  
|Consulta baseada em uma tabela com chave primária na lista de saída|Sim (exceto como listado abaixo).|  
|Consulta baseada em uma tabela sem índice exclusivo e sem uma chave primária|Depende da consulta e do banco de dados. Alguns bancos de dados permitem atualizações se informações suficiente estiverem disponíveis para identificar registros exclusivamente.|  
|Consulta baseada em tabelas múltiplas que não estão unidas|Nenhum.|  
|Consulta baseada em dados marcados como somente de leitura no banco de dados|Nenhum.|  
|Consulta baseada em uma exibição que envolve uma tabela sem restrições|Sim (exceto como listado abaixo).|  
|Consulta baseada em tabelas unidas com uma relação um-para-um|Sim (exceto como listado abaixo).|  
|Consulta baseada em tabelas unidas com uma relação um-para-um|Geralmente.|  
|Consulta baseada em três ou mais tabelas nas quais há uma relação muitos para muitos|Nenhum.|  
|Consulta baseada em uma tabela para a qual não é concedida a permissão de atualização|Pode excluir mas não atualizar.|  
|Consulta baseada em uma tabela para a qual não é concedida a permissão de exclusão|Pode atualizar mas não excluir.|  
|Consulta de agregação|Nenhum.|  
|Consulta baseada em uma subconsulta que contém funções de agregação ou totais|Nenhum.|  
|Consulta que inclui a palavra-chave DISTINCT para excluir filas duplicadas|Nenhum.|  
|Consulta cuja cláusula FROM inclui uma função definida pelo usuário que retorna uma tabela e a função definida pelo usuário contém múltiplas instruções select|Nenhum.|  
|Consulta cuja cláusula FROM inclui um função embutida definida pelo usuário|Sim.|  
  
Além disso, talvez você pode não possa atualizar colunas específicas no resultados de consulta. A lista seguinte resume os tipos específicos de colunas que você não pode atualizar no painel Resultados.  
  
-   Colunas baseadas em expressões  
  
-   Colunas baseadas em funções escalares definidas pelo usuário  
  
-   Filas ou colunas excluídas por outro usuário  
  
-   Filas ou colunas bloqueadas por outro usuário (normalmente filas bloqueadas podem ser atualizadas logo que sejam desbloqueadas)  
  
-   Carimbo de data/hora ou colunas BLOB  
  
## <a name="see-also"></a>Consulte também  
[Tópicos de instruções de como criar consultas e exibições &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  

