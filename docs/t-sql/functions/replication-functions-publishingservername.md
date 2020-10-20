---
description: Funções de replicação – PUBLISHINGSERVERNAME
title: PUBLISHINGSERVERNAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PUBLISHINGSERVERNAME_TSQL
- PUBLISHINGSERVERNAME
dev_langs:
- TSQL
helpviewer_keywords:
- PUBLISHINGSERVERNAME function
- Publishers [SQL Server replication], names
ms.assetid: e7c278e5-ab23-419e-ab3e-3bb20b0636df
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: e6b42d4883053a32ec97f76278139fad8d0cf0f4
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036557"
---
# <a name="replication-functions---publishingservername"></a>Funções de replicação – PUBLISHINGSERVERNAME
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna o nome do Publicador de origem de um banco de dados publicado que participa de uma sessão de espelhamento de banco de dados. Esta função é executada em uma instância de Publicador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no banco de dados de publicação. Use-a para determinar o Publicador original do banco de dados publicado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
PUBLISHINGSERVERNAME()  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno
 **nvarchar**  
  
## <a name="remarks"></a>Comentários  
 PUBLISHINGSERVERNAME é usada em todos os tipos de replicação.  
  
 PUBLISHINGSERVERNAME é usada quando há uma sessão de espelhamento de banco de dados no banco de dados de publicação entre o Publicador e a instância parceira espelho.  
  
 Essa função deve ser executada dentro do contexto de um banco de dados de publicação. Quando PUBLISHINGSERVERNAME é executada em um banco de dados de publicação na instância de servidor espelho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o nome da instância do Publicador de origem do banco de dados publicado é retornado. Quando esta é executada em um banco de dados publicador na instância de servidor espelho não publicada ou que seja publicada pela instância de servidor espelho após um failover, o nome da instância de servidor de espelho é retornado. Quando esta função for executada na instância do Publicador original, o nome do Publicador será retornado.  
  
## <a name="see-also"></a>Consulte Também  
 [Espelhamento e replicação de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)   
 [Funções de Replicação &#40;Transact-SQL&#41;]()  
  
