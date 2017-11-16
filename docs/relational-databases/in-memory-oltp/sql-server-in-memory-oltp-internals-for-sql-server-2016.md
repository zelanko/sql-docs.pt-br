---
title: "Visão geral interna do OLTP in-memory do SQL Server para SQL Server 2016 | Microsoft Docs"
ms.custom: 
ms.date: 09/14/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b14da361-a6b8-4d85-b196-7f2f13650f44
caps.latest.revision: "2"
author: jodebrui
ms.author: jodebrui
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d0f5f5a2ca4877d83bfd6479cfab7297f7218497
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="sql-server-in-memory-oltp-internals-for-sql-server-2016"></a>Visão geral interna do OLTP na memória do SQL Server para SQL Server 2016
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

**Resumo:** o OLTP na memória, frequentemente referenciado por seu codinome "Hekaton", foi introduzido no SQL Server 2014.
Essa poderosa tecnologia permite que você tire proveito de grandes quantidades de memória e várias dezenas de núcleos para aumentar o desempenho de operações de OLTP em 30 a 40 vezes! O SQL Server 2016 continua o investimento em OLTP na memória, removendo muitas das limitações encontradas no SQL Server 2014 e melhorando algoritmos de processamento interno para que o OLTP na memória possa fornecer melhorias ainda maiores. Este documento descreve a implementação da tecnologia OLTP na memória do SQL Server 2016 a partir do SQL Server 2016 RTM. Usando OLTP na memória, tabelas podem ser declaradas como 'memória otimizada' para habilitar os recursos do OLTP na memória. Tabelas com otimização de memória são totalmente transacionais e podem ser acessadas usando o Transact-SQL. Os procedimentos armazenados do Transact-SQL, gatilhos e UDFs escalares podem ser compilados nem código de computador para mais melhorias em tabelas com otimização de memória. O mecanismo é projetado para alta simultaneidade com nenhum bloqueio.    
  
**Escritor:** Kalen Delaney  
  
**Revisores técnicos:** Sunil Agarwal e Jos de Bruijn  
  
**Publicado em:** junho de 2016  
  
**Aplica-se a:** SQL Server 2016  
  
Para examinar o documento, faça o download do documento [Visão geral interna do OLTP na memória do SQL Server para SQL Server 2016](http://download.microsoft.com/download/8/3/6/8360731A-A27C-4684-BC88-FC7B5849A133/SQL_Server_2016_In_Memory_OLTP_White_Paper.pdf) .   
