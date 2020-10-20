---
title: Componentes internos do OLTP in-memory do SQL Server
description: Saiba mais sobre a implementação da tecnologia OLTP in-memory do SQL Server, que declara tabelas como otimizadas para memória para habilitar recursos OLTP in-memory.
ms.custom: seo-dt-2019
ms.date: 09/14/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: b14da361-a6b8-4d85-b196-7f2f13650f44
author: kevin-farlee
ms.author: kfarlee
ms.openlocfilehash: 1df603174fb4f17fef0f04ea41fa4b95154ab247
ms.sourcegitcommit: 2b6760408de3b99193edeccce4b92a2f9ed5bcc6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92175960"
---
# <a name="sql-server-in-memory-oltp-internals-for-sql-server-2016"></a>Visão geral interna do OLTP na memória do SQL Server para SQL Server 2016
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

**Resumo:** O OLTP in-memory, frequentemente referenciado pelo codinome "Hekaton", foi introduzido no SQL Server 2014.
Essa poderosa tecnologia permite que você tire proveito de grandes quantidades de memória e várias dezenas de núcleos para aumentar o desempenho de operações de OLTP em 30 a 40 vezes! O SQL Server 2016 continua o investimento em OLTP na memória, removendo muitas das limitações encontradas no SQL Server 2014 e melhorando algoritmos de processamento interno para que o OLTP na memória possa fornecer melhorias ainda maiores. Este documento descreve a implementação da tecnologia OLTP in-memory do SQL Server 2016 do SQL Server 2016 RTM. Usando OLTP in-memory, tabelas podem ser declaradas como 'otimizado para memória' para habilitar os recursos do OLTP in-memory. Tabelas com otimização de memória são totalmente transacionais e podem ser acessadas usando o Transact-SQL. Os procedimentos armazenados do Transact-SQL, gatilhos e UDFs escalares podem ser compilados no código do computador a fim de obter mais aprimoramentos em tabelas com otimização de memória. O mecanismo é projetado para alta simultaneidade com nenhum bloqueio.    
  
**Gravador:** Kalen Delaney  
  
**Revisores técnicos:** Sunil Agarwal e Jos de Bruijn  
  
**Publicado em:** Junho de 2016  
  
**Aplica-se a:** SQL Server 2016  
  
Para examinar o documento, baixe o documento [Visão geral interna do OLTP in-memory do SQL Server para SQL Server 2016](https://download.microsoft.com/download/8/3/6/8360731A-A27C-4684-BC88-FC7B5849A133/SQL_Server_2016_In_Memory_OLTP_White_Paper.pdf).   
