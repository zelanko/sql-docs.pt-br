---
title: ASYMKEY_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- AsymKey_ID
- ASYMKEY_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- asymmetric keys [SQL Server], AsymKey_ID
- ASYMKEY_ID function
- encryption [SQL Server], asymmetric keys
- identification numbers [SQL Server], asymmetric keys
- IDs [SQL Server], asymmetric keys
- cryptography [SQL Server], asymmetric keys
ms.assetid: d697daf8-2106-4ebb-b09a-ca0be465d747
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 2693cdfe7ec99d37fbd59d4889cf5c2ad1228a0e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85734219"
---
# <a name="asymkey_id-transact-sql"></a>ASYMKEY_ID (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Retorna a ID de uma chave assimétrica.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
ASYMKEY_ID ( 'Asym_Key_Name' )  
```  
  
## <a name="arguments"></a>Argumentos  
*Asym_Key_Name*  
O nome de uma chave assimétrica no banco de dados.
  
## <a name="return-types"></a>Tipos de retorno
 **int**  
  
## <a name="permissions"></a>Permissões  
Requer permissões adequadas na chave assimétrica e que a permissão VIEW não tenha sido negada para o chamador na chave assimétrica. Veja [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md) para obter mais informações sobre permissões de chaves assimétricas.
  
## <a name="examples"></a>Exemplos  
Este exemplo retorna a ID da chave assimétrica `ABerglundKey11`.
  
```sql
SELECT ASYMKEY_ID('ABerglundKey11');  
GO  
```  
  
## <a name="see-also"></a>Confira também
[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)  
[ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)  
[DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)  
[SIGNBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/signbyasymkey-transact-sql.md)  
[VERIFYSIGNEDBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/verifysignedbyasymkey-transact-sql.md)  
[Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
[sys.asymmetric_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-asymmetric-keys-transact-sql.md)  
[Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)  
[ASYMKEYPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/asymkeyproperty-transact-sql.md)  
[KEY_ID &#40;Transact-SQL&#41;](../../t-sql/functions/key-id-transact-sql.md)
  
  
