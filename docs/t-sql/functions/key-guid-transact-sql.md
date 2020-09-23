---
description: KEY_GUID (Transact-SQL)
title: KEY_GUID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Key_GUID_TSQL
- Key_GUID
dev_langs:
- TSQL
helpviewer_keywords:
- symmetric keys [SQL Server], GUIDs
- KEY_GUID function
- GUIDs [SQL Server]
ms.assetid: 9246c7b2-7098-42c4-a222-cbf30267c46a
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: ec78a9cd0dc6c0b08b61e4d1ca79748350bbb6ea
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91115159"
---
# <a name="key_guid-transact-sql"></a>KEY_GUID (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna o GUID de uma chave simétrica no banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
Key_GUID( 'Key_Name' )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 **'** *Key_Name* **'**  
 Nome de uma chave simétrica no banco de dados.  
  
## <a name="return-types"></a>Tipos de retorno  
 **uniqueidentifier**  
  
## <a name="remarks"></a>Comentários  
 Se um valor de identidade for especificado quando a chave é criada, seu GUID será um hash MD5 desse valor de identidade. Se nenhum valor de identidade for especificado, o servidor irá gerar o GUID.  
  
 Se a chave for uma chave temporária, o nome da chave deverá iniciar com um sinal de cerquilha (#).  
  
## <a name="permissions"></a>Permissões  
 Como as chaves temporárias estão disponíveis somente na sessão em que foram criadas, nenhuma permissão é necessária para acessá-las. Para acessar uma chave que não é temporária, o chamador requer algumas permissões na chave e não deve ter a permissão VIEW negada na chave.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna o GUID de uma chave simétrica chamada `ABerglundKey1`.  
  
```sql  
SELECT Key_GUID('ABerglundKey1');  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [sys.symmetric_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [sys.key_encryptions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-key-encryptions-transact-sql.md)  
  
  
