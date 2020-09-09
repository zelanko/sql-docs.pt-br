---
description: sp_cursorunprepare (Transact-SQL)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a34376a8c7c6f88c89ffc2934abc3324141b2405
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549914"
---
# <a name="sp_cursorunprepare-transact-sql"></a>sp_cursorunprepare (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Descarta o plano de execução desenvolvido no procedimento armazenado sp_cursorprepare. sp_cursorunprepare é invocado especificando ID = 6 em um pacote TDS (tabela de dados tabulares).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_cursorunprepare handle  
```  
  
## <a name="arguments"></a>Argumentos  
 *processamento*  
 É o valor do *identificador* que é retornado por sp_cursorprepare quando a instrução é preparada.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_cursorprepare ](../../relational-databases/system-stored-procedures/sp-cursorprepare-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
