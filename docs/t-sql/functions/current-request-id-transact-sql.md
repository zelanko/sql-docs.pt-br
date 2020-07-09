---
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
ms.openlocfilehash: 24f7edd211a2668809f47af2ed964d94da93c961
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85895131"
---
# <a name="current_request_id-transact-sql"></a>CURRENT_REQUEST_ID (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Esta função retorna a ID da solicitação atual na sessão atual.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
CURRENT_REQUEST_ID()  
```  
  
## <a name="return-types"></a>Tipos de retorno
**smallint**
  
## <a name="remarks"></a>Comentários  
Para localizar as informações exatas sobre a sessão atual, use @@SPID. Para ter informações exatas sobre a solicitação atual, use CURRENT_REQUEST_ID().
  
## <a name="see-also"></a>Confira também
[@@SPID &#40;Transact-SQL&#41;](../../t-sql/functions/spid-transact-sql.md)
  
  
