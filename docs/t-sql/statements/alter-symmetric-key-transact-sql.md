---
title: "ALTERAR a chave SIMÉTRICA (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER SYMMETRIC KEY
- ALTER_SYMMETRIC_KEY_TSQL
dev_langs: TSQL
helpviewer_keywords:
- modifying symmetric keys
- encryption [SQL Server], symmetric keys
- symmetric keys [SQL Server], modifying
- cryptography [SQL Server], symmetric keys
- ALTER SYMMETRIC KEY statement
ms.assetid: d3c776a4-7d71-4e6f-84fc-1db47400c465
caps.latest.revision: "44"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: db9fc587fcc855e73ca82820d78f2aa7001c78db
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="alter-symmetric-key-transact-sql"></a>ALTER SYMMETRIC KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Altera as propriedades de uma chave simétrica.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ALTER SYMMETRIC KEY Key_name <alter_option>  
  
<alter_option> ::=  
   ADD ENCRYPTION BY <encrypting_mechanism> [ , ... n ]  
   |   
   DROP ENCRYPTION BY <encrypting_mechanism> [ , ... n ]  
<encrypting_mechanism> ::=  
   CERTIFICATE certificate_name  
   |  
   PASSWORD = 'password'  
   |  
   SYMMETRIC KEY Symmetric_Key_Name  
   |  
   ASYMMETRIC KEY Asym_Key_Name  
```  
  
## <a name="arguments"></a>Argumentos  
 *Key_name*  
 É o nome pelo qual a chave simétrica a ser alterada é conhecida no banco de dados.  
  
 ADD ENCRYPTION BY  
 Adiciona a criptografia usando o método especificado.  
  
 DROP ENCRYPTION BY  
 Descarta a criptografia pelo método especificado. Você não pode remover todas as criptografias de uma chave simétrica.  
  
 CERTIFICADO *Certificate_name*  
 Especifica o certificado que é usado para criptografar a chave simétrica. Esse certificado já deve existir no banco de dados.  
  
 SENHA **='***senha***'**  
 Especifica a senha usada para criptografar a chave simétrica. *senha* devem atender aos requisitos da política de senha do Windows do computador que está executando a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 CHAVE SIMÉTRICA *Symmetric_Key_Name*  
 Especifica a chave simétrica usada para criptografar a chave simétrica que está sendo alterada. Essa chave simétrica já deve existir no banco de dados e deve estar aberta.  
  
 CHAVE ASSIMÉTRICA *Asym_Key_Name*  
 Especifica a chave assimétrica que é usada para criptografar a chave simétrica que está sendo alterada. Essa chave assimétrica já deve existir no banco de dados.  
  
## <a name="remarks"></a>Comentários  
  
> [!CAUTION]  
>  Quando uma chave simétrica é criptografada com uma senha, e não com a chave pública da chave mestre do banco de dados, o algoritmo de criptografia TRIPLE_DES é usado. Por esse motivo, as chaves criadas com um algoritmo de criptografia forte, como AES, são protegidas por um algoritmo mais fraco.  
  
 Para alterar a criptografia da chave simétrica, use as frases ADD ENCRYPTION e DROP ENCRYPTION. Nunca é possível uma chave estar totalmente sem criptografia. Devido a isso, o melhor a fazer é adicionar uma nova forma de criptografia antes de remover a forma antiga.  
  
 Para alterar o proprietário de uma chave simétrica, use [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
> [!NOTE]  
>  O algoritmo RC4 tem suporte somente para compatibilidade com versões anteriores. O novo material só pode ser criptografado por meio do algoritmo RC4 ou RC4_128 quando o banco de dados está no nível de compatibilidade 90 ou 100. (Não recomendável.) Use um algoritmo mais recente; por exemplo, um dos algoritmos AES. No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], o material criptografado por meio do algoritmo RC4 ou RC4_128 pode ser descriptografado em qualquer nível de compatibilidade.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER na chave simétrica. Se a criptografia for adicionada por um certificado ou chave assimétrica, requer a permissão VIEW DEFINITION no certificado ou na chave assimétrica. Se a criptografia for descartada por um certificado ou chave assimétrica, requer a permissão CONTROL no certificado ou na chave assimétrica.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir altera o método de criptografia que é usado para proteger uma chave simétrica. A chave simétrica `JanainaKey043` foi criptografada pelo certificado `Shipping04` quando a chave foi criada. Como a chave nunca pode ser armazenada sem estar criptografada, neste exemplo, a criptografia é adicionada por senha e, em seguida, removida por certificado.  
  
```  
CREATE SYMMETRIC KEY JanainaKey043 WITH ALGORITHM = AES_256   
    ENCRYPTION BY CERTIFICATE Shipping04;  
-- Open the key.   
OPEN SYMMETRIC KEY JanainaKey043 DECRYPTION BY CERTIFICATE Shipping04  
    WITH PASSWORD = '<enterStrongPasswordHere>';   
-- First, encrypt the key with a password.  
ALTER SYMMETRIC KEY JanainaKey043   
    ADD ENCRYPTION BY PASSWORD = '<enterStrongPasswordHere>';  
-- Now remove encryption by the certificate.  
ALTER SYMMETRIC KEY JanainaKey043   
    DROP ENCRYPTION BY CERTIFICATE Shipping04;  
CLOSE SYMMETRIC KEY JanainaKey043;  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-symmetric-key-transact-sql.md)   
 [CLOSE SYMMETRIC KEY &#40; Transact-SQL &#41;](../../t-sql/statements/close-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
