---
title: CLOSE MASTER KEY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CLOSE MASTER KEY
- CLOSE_MASTER_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- encryption [SQL Server], Database Master Key
- CLOSE MASTER KEY statement
- database master key [SQL Server], closing
- cryptography [SQL Server], Database Master Key
- closing Database Master Keys
ms.assetid: bb04ef7a-9f3a-437e-a6f9-ba0204082cb9
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9e1337667bc7dd03d9943f7b7f76f8a313eeb125
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="close-master-key-transact-sql"></a>CLOSE MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Fecha a chave mestra do banco de dados atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
CLOSE MASTER KEY  
```  
  
## <a name="arguments"></a>Argumentos  
 Não leva nenhum argumento.  
  
## <a name="remarks"></a>Comentários  
 Essa instrução inverte a operação executada por OPEN MASTER KEY. CLOSE MASTER KEY só tem êxito quando a chave mestra do banco de dados é aberta na sessão atual usando a instrução OPEN MASTER KEY.  
  
## <a name="permissions"></a>Permissões  
 Nenhuma permissão é necessária.  
  
## <a name="examples"></a>Exemplos  
  
```  
USE AdventureWorks2012;  
CLOSE MASTER KEY;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
```  
USE master;  
OPEN MASTER KEY DECRYPTION BY PASSWORD = '43987hkhj4325tsku7';  
GO   
CLOSE MASTER KEY;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [Abra a chave MESTRA &#40; Transact-SQL &#41;](../../t-sql/statements/open-master-key-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  


