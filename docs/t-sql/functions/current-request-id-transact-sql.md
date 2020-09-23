---
description: CURRENT_REQUEST_ID (Transact-SQL)
title: CURRENT_REQUEST_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CURRENT_REQUEST_ID_TSQL
- CURRENT_REQUEST_ID
dev_langs:
- TSQL
helpviewer_keywords:
- CURRENT_REQUEST_ID
ms.assetid: 949f6e5f-bf5f-49d6-a763-c443d1d51fe2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9a5628ef19aa267e326e3164d0a1f3ad95d88e23
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91115261"
---
# <a name="current_request_id-transact-sql"></a>CURRENT_REQUEST_ID (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Esta função retorna a ID da solicitação atual na sessão atual.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
CURRENT_REQUEST_ID()  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno
**smallint**
  
## <a name="remarks"></a>Comentários  
Para localizar as informações exatas sobre a sessão atual, use @@SPID. Para ter informações exatas sobre a solicitação atual, use CURRENT_REQUEST_ID().
  
## <a name="see-also"></a>Confira também
[@@SPID &#40;Transact-SQL&#41;](../../t-sql/functions/spid-transact-sql.md)
  
  
