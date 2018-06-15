---
title: Níveis de isolamento da transação | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- locking [SQL Server], hints
- isolation levels [SQL Server], metadata access
- hints [SQL Server], locking
ms.assetid: 02bb71fa-1e92-4782-a9cf-6e256cc1f3ea
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1b0322843a6fd6493f3a4a72af723bbacc9dcdcd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33060523"
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
|READ UNCOMMITTED|não|Não garantido|  
|READ COMMITTED|Sim|Sim|  
|REPEATABLE READ|não|não|  
|SNAPSHOT ISOLATION|não|não|  
|SERIALIZABLE|não|não|  
  
  
