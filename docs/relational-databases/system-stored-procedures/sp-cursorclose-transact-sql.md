---
description: sp_cursorclose (Transact-SQL)
title: sp_cursorclose (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_close_TSQL
- sp_cursor_close
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursorclose
ms.assetid: d9b7b44d-cdff-456e-97df-7031a3b9beb6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0363b69839d6cf58eebaa0394a591050c3443cd6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536612"
---
# <a name="sp_cursorclose-transact-sql"></a>sp_cursorclose (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Fecha e desaloca o cursor, além de liberar todos os recursos associados; ou seja, ele remove a tabela temporária usada para dar suporte ao conjunto de chaves ou ao **cursor**estático. sp_cursorclose é invocado especificando ID = 9 em um pacote TDS (tabela de dados tabulares).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_cursorclose cursor  
```  
  
## <a name="arguments"></a>Argumentos  
 *cursor*  
 É um valor de *identificador* de cursor gerado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e retornado pelo procedimento de sp_cursoropen. *cursor* é um parâmetro necessário que chama um valor de entrada **int** .  
  
> [!NOTE]  
>  Um valor de entrada -1 será aplicado a todos os cursores na conexão atual.  
  
## <a name="remarks"></a>Comentários  
 o *cursor* retornará mensagens de erro se o procedimento tiver sido executado depois que o cursor tiver sido fechado ou se um identificador inválido for especificado.  
  
 O status RPC indica êxito ou falha geral.  
  
 A contagem de linhas DONE é sempre 0.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_cursoropen ](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
