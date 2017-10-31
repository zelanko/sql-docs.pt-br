---
title: "ALTERAR a chave ASSIMÉTRICA (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 04/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_ASYMMETRIC_KEY_TSQL
- ALTER ASYMMETRIC KEY
dev_langs:
- TSQL
helpviewer_keywords:
- ENCRYPTION BY PASSWORD option
- passwords [SQL Server], asymmetric keys
- encryption [SQL Server], asymmetric keys
- DECRYPTION BY PASSWORD option
- ALTER ASYMMETRIC KEY statement
- asymmetric keys [SQL Server], modifying
ms.assetid: 958e95d6-fbe6-43e8-abbd-ccedbac2dbac
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 81ae1caa65cac678ecd1ddeef0326d68e291ba36
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="alter-asymmetric-key-transact-sql"></a>ALTER ASYMMETRIC KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Altera as propriedades de uma chave assimétrica.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
ALTER ASYMMETRIC KEY Asym_Key_Name <alter_option>  
  
<alter_option> ::=  
      <password_change_option>   
    | REMOVE PRIVATE KEY   

<password_change_option> ::=  
    WITH PRIVATE KEY ( <password_option> [ , <password_option> ] )  

<password_option> ::=  
      ENCRYPTION BY PASSWORD = 'strongPassword'  
    | DECRYPTION BY PASSWORD = 'oldPassword'  
```  
  
## <a name="arguments"></a>Argumentos  
 *Asym_Key_Name*  
 É o nome pelo qual a chave assimétrica é conhecida no banco de dados.  
  
 REMOVE PRIVATE KEY  
 Remove a chave privada da chave assimétrica. A chave pública não é removida.  
  
 WITH PRIVATE KEY  
 Altera a proteção da chave privada.  
  
 CRIPTOGRAFIA por senha **='***stongPassword***'**  
 Especifica uma nova senha para proteção da chave privada. *senha* devem atender aos requisitos da política de senha do Windows do computador que está executando a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se esta opção for omitida, a chave privada será criptografada pela chave mestra do banco de dados.  
  
 DECRYPTION BY PASSWORD **='***Senha_atual***'**  
 Especifica a senha antiga com a qual a chave privada está protegida atualmente. Não será necessária se a chave privada for criptografada com a chave mestra do banco de dados.  
  
## <a name="remarks"></a>Comentários  
 Se não houver nenhuma chave mestra do banco de dados a opção ENCRYPTION BY PASSWORD será necessária e a operação falhará se nenhuma senha for fornecida. Para obter informações sobre como criar uma chave mestra de banco de dados, consulte [CREATE MASTER KEY &#40; Transact-SQL &#41; ](../../t-sql/statements/create-master-key-transact-sql.md).  
  
 É possível usar ALTER ASYMMETRIC KEY para alterar a proteção da chave privada especificando as opções PRIVATE KEY conforme mostrado na tabela a seguir.  
  
|Alterar a proteção de|ENCRYPTION BY PASSWORD|DECRYPTION BY PASSWORD|  
|----------------------------|----------------------------|----------------------------|  
|Senha antiga para senha nova|Obrigatório|Required|  
|Senha para chave mestra|Omitir|Required|  
|Chave mestra para senha|Required|Omitir|  
  
 A chave mestra do banco de dados deve ser aberta antes de poder ser usada para proteger uma chave privada. Para obter mais informações, consulte [OPEN MASTER KEY &#40; Transact-SQL &#41; ](../../t-sql/statements/open-master-key-transact-sql.md).  
  
 Para alterar a propriedade de uma chave assimétrica, use [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requerer a permissão CONTROL na chave assimétrica quando a chave privada é removida.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-changing-the-password-of-the-private-key"></a>A. Alterando a senha da chave privada  
 O exemplo a seguir altera a senha usada para proteger a chave privada da chave assimétrica `PacificSales09`. A senha nova será `<enterStrongPasswordHere>`.  
  
```  
ALTER ASYMMETRIC KEY PacificSales09   
    WITH PRIVATE KEY (  
    DECRYPTION BY PASSWORD = '<oldPassword>',  
    ENCRYPTION BY PASSWORD = '<enterStrongPasswordHere>');  
GO  
```  
  
### <a name="b-removing-the-private-key-from-an-asymmetric-key"></a>B. Removendo a chave privada de uma chave assimétrica  
 O exemplo a seguir remove a chave privada de `PacificSales19`, deixando apenas a chave pública.  
  
```  
ALTER ASYMMETRIC KEY PacificSales19 REMOVE PRIVATE KEY;  
GO  
```  
  
### <a name="c-removing-password-protection-from-a-private-key"></a>C. Removendo a proteção de senha de uma chave privada  
 O exemplo a seguir remove a proteção de senha de uma chave privada e a protege com a chave mestra do banco de dados.  
  
```  
OPEN MASTER KEY;  
ALTER ASYMMETRIC KEY PacificSales09 WITH PRIVATE KEY (  
    DECRYPTION BY PASSWORD = '<enterStrongPasswordHere>' );  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [Chaves de criptografia do SQL Server e banco de dados &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [Abra a chave MESTRA &#40; Transact-SQL &#41;](../../t-sql/statements/open-master-key-transact-sql.md)   
 [Gerenciamento Extensível de Chaves &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
  

