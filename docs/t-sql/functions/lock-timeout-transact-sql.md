---
title: '@@LOCK_TIMEOUT (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/19/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@LOCK_TIMEOUT'
- '@@LOCK_TIMEOUT_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- timeout options [SQL Server], locks
- '@@LOCK_TIMEOUT function'
- current lock time-out setting
- locking [SQL Server], time-outs
ms.assetid: 6bf8bf97-60b8-40c1-b89d-8f5a00bcae2e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 08822357b12dba17e39493929db8841f5803f484
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47677984"
---
# <a name="x40x40locktimeout-transact-sql"></a>&#x40;&#x40;LOCK_TIMEOUT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna a configuração de tempo limite do bloqueio atual em milissegundos para a sessão atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
@@LOCK_TIMEOUT  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 **inteiro**  
  
## <a name="remarks"></a>Remarks  
 A configuração SET LOCK_TIMEOUT permite que um aplicativo defina o tempo máximo que uma instrução espera em um recurso bloqueado. Quando uma instrução espera por mais tempo do que a configuração LOCK_TIMEOUT, a instrução bloqueada é cancelada automaticamente e uma mensagem de erro é retornada ao aplicativo.  
  
 @@LOCK_TIMEOUT retorna um valor igual a -1 se SET LOCK_TIMEOUT ainda não foi executado na sessão atual.  
  
## <a name="examples"></a>Exemplos  
 Este exemplo mostra o conjunto de resultados quando um valor LOCK_TIMEOUT não foi definido.  
  
```  
SELECT @@LOCK_TIMEOUT AS [Lock Timeout];  
GO  
```  
  
 Este é o conjunto de resultados:  
  
```  
Lock Timeout  
------------  
-1  
```  
  
 Este exemplo define LOCK_TIMEOUT com 1.800 milissegundos e, em seguida, chama @@LOCK_TIMEOUT.  
  
```  
SET LOCK_TIMEOUT 1800;  
SELECT @@LOCK_TIMEOUT AS [Lock Timeout];  
GO  
```  
  
 Este é o conjunto de resultados:  
  
```  
Lock Timeout  
------------  
1800          
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções de configuração &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [SET LOCK_TIMEOUT &#40;Transact-SQL&#41;](../../t-sql/statements/set-lock-timeout-transact-sql.md)  
  
  
