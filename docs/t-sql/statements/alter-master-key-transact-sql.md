---
title: ALTER MASTER KEY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER MASTER KEY
- ALTER_MASTER_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- REGENERATE phrase
- ALTER MASTER KEY statement
- decryption [SQL Server], Database Master Key
- FORCE option
- encryption [SQL Server], Database Master Key
- database master key [SQL Server], modifying
- cryptography [SQL Server], Database Master Key
- modifying Database Master Key
- service master key [SQL Server], modifying
- DROP ENCRYPTION BY SERVICE MASTER KEY phrase
ms.assetid: 8ac501c3-4280-4d5b-b58a-1524fa715b50
caps.latest.revision: 49
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 638449f85daf7b13abc37c5750eb32ec5603d7ef
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="alter-master-key-transact-sql"></a>ALTER MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-_md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Altera as propriedades de uma chave mestra do banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server  
  
ALTER MASTER KEY <alter_option>  
  
<alter_option> ::=  
    <regenerate_option> | <encryption_option>  
  
<regenerate_option> ::=  
    [ FORCE ] REGENERATE WITH ENCRYPTION BY PASSWORD = 'password'  
  
<encryption_option> ::=  
    ADD ENCRYPTION BY { SERVICE MASTER KEY | PASSWORD = 'password' }  
    |   
    DROP ENCRYPTION BY { SERVICE MASTER KEY | PASSWORD = 'password' }  
```  
```  
-- Syntax for Azure SQL Database
-- Note: DROP ENCRYPTION BY SERVICE MASTER KEY is not supported on Azure SQL Database.
  
ALTER MASTER KEY <alter_option>  
  
<alter_option> ::=  
    <regenerate_option> | <encryption_option>  
  
<regenerate_option> ::=  
    [ FORCE ] REGENERATE WITH ENCRYPTION BY PASSWORD = 'password'  
  
<encryption_option> ::=  
    ADD ENCRYPTION BY { SERVICE MASTER KEY | PASSWORD = 'password' }  
    |   
    DROP ENCRYPTION BY { PASSWORD = 'password' }  
```  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ALTER MASTER KEY <alter_option>  
  
<alter_option> ::=  
    <regenerate_option> | <encryption_option>  
  
<regenerate_option> ::=  
    [ FORCE ] REGENERATE WITH ENCRYPTION BY PASSWORD ='password'<encryption_option> ::=  
    ADD ENCRYPTION BY SERVICE MASTER KEY   
    |   
    DROP ENCRYPTION BY SERVICE MASTER KEY  
```  
  
## <a name="arguments"></a>Argumentos  
 SENHA ='*senha*'  
 Especifica uma senha com criptografia ou descriptografia da chave mestra do banco de dados. *senha* devem atender aos requisitos da política de senha do Windows do computador que está executando a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="remarks"></a>Comentários  
 A opção REGENERATE recria a chave mestra do banco de dados e todas as chaves protegidas por ela. As chaves são decifradas primeiro com a chave mestra antiga e depois criptografadas com a nova chave mestra. Essa operação de uso intensivo de recursos deve ser agendada durante um período de baixa demanda, a menos que a chave mestra esteja comprometida.  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] usa o algoritmo de criptografia AES para proteger a SMK (chave mestra de serviço) e a DMK (chave mestra de banco de dados). O AES é um algoritmo de criptografia mais novo que o 3DES usado em versões anteriores. Depois de atualizar uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , o SMK e o DMK devem ser regenerados para atualizar as chave mestras para AES. Para obter mais informações sobre a regeneração do SMK, consulte [ALTER SERVICE MASTER KEY &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-service-master-key-transact-sql.md).  
  
 Quando a opção FORCE é usada, a regeneração de chave continuará mesmo que a chave mestra não esteja disponível ou o servidor não possa descriptografar todas as chaves privadas criptografadas. Se a chave mestra não pode ser aberta, use o [RESTORE MASTER KEY](../../t-sql/statements/restore-master-key-transact-sql.md) instrução para restaurar a chave mestra de um backup. Use a opção de FORCE somente se a chave mestra for irrecuperável ou se descriptografia falhar. As informações que só são criptografadas por uma chave irrecuperável serão perdidas.  
  
 A opção DROP ENCRYPTION BY SERVICE MASTER KEY remove a criptografia da chave mestra de banco de dados através da chave mestra de serviço.  
  
 ADD ENCRYPTION BY SERVICE MASTER KEY faz com que uma cópia da chave mestra seja criptografada usando a chave mestra de serviço e armazenada no banco de dados atual e mestre.  
  
## <a name="permissions"></a>Permissões  
 Exige a permissão CONTROL no banco de dados. Se a chave mestra de banco de dados for criptografada com uma senha, o conhecimento dessa senha também será necessário.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma nova chave mestra de banco de dados para a `AdventureWorks` e criptografa novamente as chaves abaixo dela na hierarquia de criptografia.  
  
```  
USE AdventureWorks2012;  
ALTER MASTER KEY REGENERATE WITH ENCRYPTION BY PASSWORD = 'dsjdkflJ435907NnmM#sX003';  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir cria uma nova chave mestra de banco de dados para `AdventureWorksPDW2012` e criptografa novamente as chaves abaixo na hierarquia de criptografia.  
  
```  
USE master;  
ALTER MASTER KEY REGENERATE WITH ENCRYPTION BY PASSWORD = 'dsjdkflJ435907NnmM#sX003';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [Abra a chave MESTRA &#40; Transact-SQL &#41;](../../t-sql/statements/open-master-key-transact-sql.md)   
 [CLOSE MASTER KEY &#40; Transact-SQL &#41;](../../t-sql/statements/close-master-key-transact-sql.md)   
 [BACKUP MASTER KEY &#40; Transact-SQL &#41;](../../t-sql/statements/backup-master-key-transact-sql.md)   
 [RESTORE MASTER KEY &#40; Transact-SQL &#41;](../../t-sql/statements/restore-master-key-transact-sql.md)   
 [DROP MASTER KEY &#40; Transact-SQL &#41;](../../t-sql/statements/drop-master-key-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  


