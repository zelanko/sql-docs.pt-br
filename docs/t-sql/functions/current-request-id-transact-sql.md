---
title: CURRENT_REQUEST_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CURRENT_REQUEST_ID_TSQL
- CURRENT_REQUEST_ID
dev_langs:
- TSQL
helpviewer_keywords:
- CURRENT_REQUEST_ID
ms.assetid: 949f6e5f-bf5f-49d6-a763-c443d1d51fe2
caps.latest.revision: 13
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2761901c3b04b0b38fc92f08238a968d8efb6786
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37791807"
---
# <a name="currentrequestid-transact-sql"></a>CURRENT_REQUEST_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Esta função retorna a ID da solicitação atual na sessão atual.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
CURRENT_REQUEST_ID()  
```  
  
## <a name="return-types"></a>Tipos de retorno
**smallint**
  
## <a name="remarks"></a>Remarks  
Para localizar as informações exatas sobre a sessão atual, use @@SPID. Para ter informações exatas sobre a solicitação atual, use CURRENT_REQUEST_ID().
  
## <a name="see-also"></a>Confira também
[@@SPID &#40;Transact-SQL&#41;](../../t-sql/functions/spid-transact-sql.md)
  
  
