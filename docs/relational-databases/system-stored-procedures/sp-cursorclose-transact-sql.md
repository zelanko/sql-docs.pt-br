---
title: sp_cursorclose (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_cursor_close_TSQL
- sp_cursor_close
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursorclose
ms.assetid: d9b7b44d-cdff-456e-97df-7031a3b9beb6
caps.latest.revision: 7
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 1d1e6f96076b01b01464b40bc4e3d65f3e1e2c42
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="spcursorclose-transact-sql"></a>sp_cursorclose (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fecha e desaloca o cursor, como também libera todos os recursos associados; ou seja, descarta a tabela temporária usada para oferecer suporte a KEYSET ou STATIC **cursor**. sp_cursorclose é invocado pela especificação de ID = 9 em um pacote de protocolo TDS de dados tabulares.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_cursorclose cursor  
```  
  
## <a name="arguments"></a>Argumentos  
 *cursor*  
 É um cursor *tratar* valor gerado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e retornado pelo procedimento sp_cursoropen. *cursor* é um parâmetro obrigatório que chama uma **int** valor de entrada.  
  
> [!NOTE]  
>  Um valor de entrada -1 será aplicado a todos os cursores na conexão atual.  
  
## <a name="remarks"></a>Remarks  
 *cursor* retornará a mensagem de erro se o procedimento foi executado após o cursor for fechado ou se um identificador inválido for especificado.  
  
 O status RPC indica êxito ou falha geral.  
  
 A contagem de linhas DONE é sempre 0.  
  
## <a name="see-also"></a>Consulte também  
 [sp_cursoropen &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
