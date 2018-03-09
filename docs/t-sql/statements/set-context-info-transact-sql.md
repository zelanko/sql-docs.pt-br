---
title: SET CONTEXT_INFO (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET_CONTEXT_INFO_TSQL
- SET CONTEXT_INFO
dev_langs:
- TSQL
helpviewer_keywords:
- context information [SQL Server]
- CONTEXT_INFO option
- SET CONTEXT_INFO statement
ms.assetid: a0b7b9f3-dbda-4350-a274-bd9ecd5c0a74
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4a93e9f40690f37c0c161c635aea95589d47ef1e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="set-contextinfo-transact-sql"></a>SET CONTEXT_INFO (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Associa até 128 bytes de informações binárias à sessão ou conexão atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET CONTEXT_INFO { binary_str | @binary_var }  
```  
  
## <a name="arguments"></a>Argumentos  
 *binary_str*  
 É um **binário** constante ou uma constante que é implicitamente conversível em **binário**, para associar a sessão atual ou a conexão.  
  
 **@***binary_var*  
 É um **varbinary** ou **binário** variável que contém um valor de contexto para associar a sessão atual ou a conexão.  
  
## <a name="remarks"></a>Comentários  
 O modo preferido de recuperar as informações de contexto para a sessão atual é usar a função CONTEXT_INFO. Informações de contexto de sessão também são armazenadas no **context_info** colunas nas exibições do sistema a seguir:  
  
-   **sys.dm_exec_requests**  
  
-   **sys.dm_exec_sessions**  
  
-   **sys.sysprocesses**  
  
 SET CONTEXT_INFO não pode ser especificado em uma função definida pelo usuário. Não é possível fornecer um valor nulo para SET CONTEXT_INFO porque as exibições que mantêm os valores não permitem valores nulos.  
  
 SET CONTEXT_INFO não aceita expressões diferentes de constantes ou nomes de variável. Para definir as informações de contexto para o resultado de uma chamada de função, você primeiro deve incluir o resultado da chamada de função em um **binário** ou **varbinary** variável.  
  
 Ao emitir SET CONTEXT_INFO em um procedimento armazenado ou disparador, diferentemente de outras instruções SET, o novo valor definido para as informações de contexto persiste depois que o procedimento armazenado ou disparador é concluído.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-setting-context-information-by-using-a-constant"></a>A. Definindo informações de contexto com o uso de uma constante  
 O exemplo a seguir demonstra `SET CONTEXT_INFO` definindo o valor e exibindo os resultados. Observe que consultar `sys.dm_exec_sessions` requer as permissões SELECT e VIEW SERVER STATE, enquanto que usar a função CONTEXT_INFO não requer.  
  
```  
SET CONTEXT_INFO 0x01010101;  
GO  
SELECT context_info   
FROM sys.dm_exec_sessions  
WHERE session_id = @@SPID;  
GO  
```  
  
### <a name="b-setting-context-information-by-using-a-function"></a>B. Definindo informações de contexto com o uso de uma função  
 O exemplo a seguir demonstra como usar a saída de uma função para definir o valor de contexto, onde o valor da função deve primeiro ser colocado em um **binário** variável.  
  
```  
DECLARE @BinVar varbinary(128);  
SET @BinVar = CAST(REPLICATE( 0x20, 128 ) AS varbinary(128) );  
SET CONTEXT_INFO @BinVar;  
  
SELECT CONTEXT_INFO() AS MyContextInfo;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [exec_requests &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sys.DM exec_sessions &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [CONTEXT_INFO &#40; Transact-SQL &#41;](../../t-sql/functions/context-info-transact-sql.md)  
  
  
