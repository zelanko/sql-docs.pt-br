---
title: CLOSE SYMMETRIC KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: f14d291cf70bcefb13404805aa717f2087695ce6
ms.sourcegitcommit: b2ab989264dd9d23c184f43fff2ec8966793a727
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/14/2020
ms.locfileid: "86380889"
---
# <a name="close-symmetric-key-transact-sql"></a>CLOSE SYMMETRIC KEY (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Fecha uma chave simétrica ou fecha todas as chaves simétricas abertas na sessão atual.  
  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
CLOSE { SYMMETRIC KEY key_name | ALL SYMMETRIC KEYS }  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *Key_name*  
 É o nome da chave simétrica a ser fechada.  
  
## <a name="remarks"></a>Comentários  
 As chaves simétricas abertas estão associadas à sessão que não está no contexto de segurança. Uma chave aberta continuará disponível até ser explicitamente fechada ou a sessão ser encerrada. CLOSE ALL SYMMETRIC KEYS fechará qualquer chave mestra do banco de dados que tenha sido aberta na sessão atual usando a instrução [OPEN MASTER KEY](../../t-sql/statements/open-master-key-transact-sql.md).  Informações sobre chaves abertas estão visíveis na exibição do catálogo [sys.openkeys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-openkeys-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Nenhuma permissão explícita é necessária para fechar uma chave simétrica.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-closing-a-symmetric-key"></a>a. Fechando uma chave simétrica  
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
  
## <a name="see-also"></a>Consulte Também  
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)  
  
  
