---
title: sp_cursorunprepare (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursorunprepare_TSQL
- sp_cursorunprepare
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursorunprepare
ms.assetid: b46d4813-c4a9-4f9d-9979-2b5082ecf06a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8bfdcafb37b6ff7b495f1306d5d8339725e55e10
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108390"
---
# <a name="spcursorunprepare-transact-sql"></a>sp_cursorunprepare (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Descarta o plano de execução desenvolvido na sp_cursorprepare o procedimento armazenado. sp_cursorunprepare é invocado pela especificação de ID = 6 em um pacote do protocolo TDS.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_cursorunprepare handle  
```  
  
## <a name="arguments"></a>Argumentos  
 *Identificador*  
 É o *manipular* valor é retornado por sp_cursorprepare quando a instrução está preparada.  
  
## <a name="see-also"></a>Consulte também  
 [sp_cursorprepare &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorprepare-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
