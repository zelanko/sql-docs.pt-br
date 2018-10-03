---
title: SQL Server Profiler - caixa de diálogo Localizar | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.find.f1
helpviewer_keywords:
- Find dialog box
ms.assetid: dfaeec04-93d3-4214-9fc1-38b80179b36b
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 23bbfd748bcb649e5f7d103683d20413764a62a8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48078918"
---
# <a name="sql-server-profiler---find-dialog-box"></a>SQL Server Profiler - Caixa de diálogo Localizar
  Use a caixa de diálogo **Localizar** para pesquisar um rastreamento para caracteres ou palavras específicos. Para cancelar uma pesquisa em andamento, pressione ESC.  
  
 Para abrir essa caixa de diálogo no [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)], no menu **Editar**, clique em **Localizar**.  
  
## <a name="options"></a>Opções  
 **Localizar**  
 Insira o texto que deseja pesquisar. A pesquisa corresponde a qualquer cadeia de caracteres que contenha a cadeia especificada. Por exemplo, a pesquisa por "Concluído" corresponde a "SQL:LoteConcluído". Caracteres curinga (*, ?, etc.) não têm suporte.  
  
 **Pesquisar na coluna**  
 Clique em uma coluna de dados para pesquisar ou em **\<Todas as colunas>** para pesquisar todas as colunas de dados no rastreamento.  
  
 **Diferenciar maiúsculas de minúsculas**  
 Localiza texto que tem maiúsculas e minúsculas iguais às da caixa **Localizar** . Desmarque essa caixa de seleção para localizar exemplos no rastreamento que tenham caracteres de texto tanto com letras maiúsculas como com minúsculas.  
  
 **Coincidir palavra inteira**  
 Restringe a pesquisa a palavras inteiras. Desmarque a caixa de seleção **Coincidir palavra inteira** para pesquisar caracteres em uma palavra.  
  
 **Localizar Próximo**  
 Localiza o próximo exemplo dos caracteres na caixa **Localizar** .  
  
 **Localizar Anterior**  
 Pesquisa para trás no rastreamento, para localizar o exemplo anterior dos caracteres na caixa **Localizar** .  
  
## <a name="see-also"></a>Consulte também  
 [Localizar um valor ou uma coluna de dados durante um rastreamento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/find-a-value-or-data-column-while-tracing-sql-server-profiler.md)   
 [Criar um rastreamento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)   
 [Abrir uma tabela de rastreamento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)   
 [Abrir um arquivo de rastreamento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)   
 [Modelos e permissões do SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
