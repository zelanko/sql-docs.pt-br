---
title: Níveis de isolamento da transação | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- locking [SQL Server], hints
- isolation levels [SQL Server], metadata access
- hints [SQL Server], locking
ms.assetid: 02bb71fa-1e92-4782-a9cf-6e256cc1f3ea
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1634e8bbb524744e637d1b9d0b5f7ef213ca62f4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65981402"
---
# <a name="transaction-isolation-levels"></a>Níveis de isolamento da transação
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não garante que as dicas de bloqueio serão cumpridas em consultas que acessam metadados por exibições do catálogo, exibições de compatibilidade, exibições de esquema de informações, funções internas que emitem metadados.  
  
 Internamente, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] cumpre apenas o nível de isolamento READ COMMITTED para acesso a metadados. Se uma transação tiver um nível de isolamento que seja, por exemplo, SERIALIZABLE e, dentro da transação, for feita uma tentativa de acessar os metadados usando exibições do catálogo ou funções internas que emitem metadados, essas consultas serão executadas até serem concluídas como READ COMMITTED. Porém, no isolamento de instantâneo, o acesso aos metadados pode falhar por causa de operações de DDL simultâneas. Isso porque os metadados não são controlados por versão. Portanto, pode haver falha ao acessar o seguinte no isolamento de instantâneo:  
  
-   Exibições do catálogo  
  
-   Exibições de compatibilidade  
  
-   Exibições do esquema de informações  
  
-   Funções internas que emitem metadados  
  
-   Grupo **sp_help** de procedimentos armazenados  
  
-   Procedimentos de catálogo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client  
  
-   Exibições e funções de gerenciamento dinâmico  
  
 Para obter mais informações sobre os níveis de isolamento, confira [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).  
  
 A tabela a seguir fornece um resumo do acesso aos metadados em vários níveis de isolamento.  
  
|Nível de isolamento|Tem suporte|Cumprido|  
|---------------------|---------------|-------------|  
|READ UNCOMMITTED|Não|Não garantido|  
|READ COMMITTED|Sim|Sim|  
|REPEATABLE READ|Não|Não|  
|SNAPSHOT ISOLATION|Não|Não|  
|SERIALIZABLE|Não|Não|  
  
  
