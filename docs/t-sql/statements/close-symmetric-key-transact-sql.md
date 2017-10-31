---
title: CLOSE SYMMETRIC KEY (Transact-SQL) | Microsoft Docs
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
- CLOSE SYMMETRIC KEY
- CLOSE_SYMMETRIC_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- closing symmetric keys
- encryption [SQL Server], symmetric keys
- symmetric keys [SQL Server], closing
- CLOSE SYMMETRIC KEY statement
- cryptography [SQL Server], symmetric keys
ms.assetid: 3b083cbb-3c6a-4f59-8d34-601db1efcc83
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 18a4215cf009ebf89bf6ce709c0517455731c4b5
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="close-symmetric-key-transact-sql"></a>CLOSE SYMMETRIC KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Fecha uma chave simétrica ou fecha todas as chaves simétricas abertas na sessão atual.  
  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
CLOSE { SYMMETRIC KEY key_name | ALL SYMMETRIC KEYS }  
```  
  
## <a name="arguments"></a>Argumentos  
 *Key_name*  
 É o nome da chave simétrica a ser fechada.  
  
## <a name="remarks"></a>Comentários  
 As chaves simétricas abertas estão associadas à sessão que não está no contexto de segurança. Uma chave aberta continuará disponível até ser explicitamente fechada ou a sessão ser encerrada. CLOSE ALL SYMMETRIC KEYS fechará qualquer chave mestra de banco de dados que foi aberta na sessão atual usando o [OPEN MASTER KEY](../../t-sql/statements/open-master-key-transact-sql.md) instrução.  Informações sobre chaves abertas estão visíveis no [sys.openkeys &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-openkeys-transact-sql.md) exibição do catálogo.  
  
## <a name="permissions"></a>Permissões  
 Nenhuma permissão explícita é necessária para fechar uma chave simétrica.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-closing-a-symmetric-key"></a>A. Fechando uma chave simétrica  
 O exemplo a seguir fecha a chave simétrica `ShippingSymKey04`.  
  
```  
CLOSE SYMMETRIC KEY ShippingSymKey04;  
GO  
```  
  
### <a name="b-closing-all-symmetric-keys"></a>B. Fechando todas as chaves simétricas  
 O exemplo a seguir fecha todas as chaves simétricas que estiverem abertas na sessão atual, bem como a chave mestra do banco de dados aberta explicitamente.  
  
```  
CLOSE ALL SYMMETRIC KEYS;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-symmetric-key-transact-sql.md)   
 [Remover chave SIMÉTRICA &#40; Transact-SQL &#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)  
  
  

