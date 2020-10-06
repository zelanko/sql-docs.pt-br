---
description: OPEN SYMMETRIC KEY (Transact-SQL)
title: OPEN SYMMETRIC KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- OPEN SYMMETRIC KEY
- OPEN_SYMMETRIC_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- symmetric keys [SQL Server], opening
- OPEN SYMMETRIC KEY statement
ms.assetid: ff019a7c-c373-46c7-ac43-ffb7e2ee60b3
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: aead1bff6950305af650040bffb65d92a436f769
ms.sourcegitcommit: b93beb4f03aee2c1971909cb1d15f79cd479a35c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91498087"
---
# <a name="open-symmetric-key-transact-sql"></a>OPEN SYMMETRIC KEY (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Descriptografa uma chave simétrica e a disponibiliza para uso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
OPEN SYMMETRIC KEY Key_name DECRYPTION BY <decryption_mechanism>  
  
<decryption_mechanism> ::=  
    CERTIFICATE certificate_name [ WITH PASSWORD = 'password' ]  
    |  
    ASYMMETRIC KEY asym_key_name [ WITH PASSWORD = 'password' ]  
    |  
    SYMMETRIC KEY decrypting_Key_name  
    |  
    PASSWORD = 'decryption_password'  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *Key_name*  
 É o nome da chave simétrica a ser aberta.  
  
 CERTIFICATE *certificate_name*  
 É o nome de um certificado cuja chave privada será usada para descriptografar a chave simétrica.  
  
 ASYMMETRIC KEY *asym_key_name*  
 É o nome de uma chave assimétrica cuja chave privada será usada para descriptografar a chave simétrica.  
  
 WITH PASSWORD ='*password*'  
 É a senha que foi usada para criptografar a chave privada do certificado ou chave assimétrica.  
  
 SYMMETRIC KEY *decrypting_key_name*  
 É o nome de uma chave simétrica que será usada para descriptografar a chave simétrica sendo aberta.  
  
 PASSWORD ='*password*'  
 É a senha que foi usada para proteger a chave simétrica.  
  
## <a name="remarks"></a>Comentários  
 As chaves simétricas abertas estão associadas à sessão que não está no contexto de segurança. Uma chave aberta continuará disponível até ser explicitamente fechada ou a sessão ser encerrada. Se você abrir uma chave simétrica e alterar o contexto, ela permanecerá aberta e estará disponível no contexto representado. Informações sobre chaves simétricas abertas estão visíveis na exibição do catálogo [sys.openkeys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-openkeys-transact-sql.md).  
  
 Se a chave simétrica tiver sido criptografada com outra chave, essa chave deverá ser aberta primeiro.  
  
 Se a chave simétrica já estiver aberta, a consulta será um **NO_OP**.  
  
 Se a senha, chave ou certificado fornecido para descriptografar a chave simétrica estiver incorreto, a consulta falhará.  
  
 As chaves simétricas criadas de provedores de criptografia não podem ser abertas. As operações de criptografia e descriptografia que usam esse tipo de chave simétrica dão certo sem a instrução **OPEN** porque o provedor de criptografia está abrindo e fechando a chave.  
  
## <a name="permissions"></a>Permissões  
 O chamador deve ter alguma permissão na chave, e a permissão VIEW DEFINITION não deve ter sido negada a ele na chave. Os requisitos adicionais variam, dependendo do mecanismo de descriptografia:  
  
-   DECRYPTION BY CERTIFICATE: permissão CONTROL no certificado e conhecimento da senha que criptografa sua chave privada.  
  
-   DECRYPTION BY ASYMMETRIC KEY: permissão CONTROL na chave assimétrica e conhecimento da senha que criptografa sua chave privada.  
  
-   DECRYPTION BY PASSWORD: conhecimento de uma das senhas usadas para criptografar a chave simétrica.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-opening-a-symmetric-key-by-using-a-certificate"></a>a. Abrindo uma chave simétrica com o uso de um certificado  
 O exemplo seguinte abre a chave simétrica `SymKeyMarketing3` e a descriptografa usando a chave privada de certificado `MarketingCert9`.  
  
```sql  
USE AdventureWorks2012;  
OPEN SYMMETRIC KEY SymKeyMarketing3   
    DECRYPTION BY CERTIFICATE MarketingCert9;  
GO  
```  
  
### <a name="b-opening-a-symmetric-key-by-using-another-symmetric-key"></a>B. Abrindo uma chave simétrica com o uso de outra chave simétrica  
 O exemplo seguinte abre a chave simétrica `MarketingKey11` e a descriptografa usando a chave simétrica `HarnpadoungsatayaSE3`.  
  
```sql  
USE AdventureWorks2012;  
-- First open the symmetric key that you want for decryption.  
OPEN SYMMETRIC KEY HarnpadoungsatayaSE3   
    DECRYPTION BY CERTIFICATE sariyaCert01;  
-- Use the key that is already open to decrypt MarketingKey11.  
OPEN SYMMETRIC KEY MarketingKey11   
    DECRYPTION BY SYMMETRIC KEY HarnpadoungsatayaSE3;  
GO   
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [CLOSE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/close-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Gerenciamento Extensível de Chaves &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
  
