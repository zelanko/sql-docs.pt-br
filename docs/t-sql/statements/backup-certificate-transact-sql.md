---
description: BACKUP CERTIFICATE (Transact-SQL)
title: BACKUP CERTIFICATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/16/2020
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DUMP_CERTIFICATE_TSQL
- BACKUP CERTIFICATE
- sql13.swb.exportcertificate.f1
- DUMP CERTIFICATE
- BACKUP_CERTIFICATE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- encryption [SQL Server], certificates
- decryption [SQL Server], certificates
- exporting certificates
- certificates [SQL Server], exporting
- BACKUP CERTIFICATE statement
- backing up certificates [SQL Server]
- decryption [SQL Server]
- cryptography [SQL Server], certificates
ms.assetid: 509b9462-819b-4c45-baae-3d2d90d14a1c
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azure-sqldw-latest'
ms.openlocfilehash: 06776d309042483f879dd3d31d9f6bae62119037
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96124191"
---
# <a name="backup-certificate-transact-sql"></a>BACKUP CERTIFICATE (Transact-SQL)
[!INCLUDE [sql-asa-pdw](../../includes/applies-to-version/sql-asa-pdw.md)]

  Exporta um certificado para um arquivo.  
  
 ![Ícone de link](../../database-engine/configure-windows/media/topic-link.gif "ícone de link") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
-- Syntax for SQL Server  
  
BACKUP CERTIFICATE certname TO FILE = 'path_to_file'  
    [ WITH PRIVATE KEY   
      (   
        FILE = 'path_to_private_key_file' ,  
        ENCRYPTION BY PASSWORD = 'encryption_password'   
        [ , DECRYPTION BY PASSWORD = 'decryption_password' ]   
      )   
    ]  
```  
  
> [!Note]
> [!INCLUDE [Synapse preview note](../../includes/synapse-preview-note.md)]
   
```syntaxsql
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  
  
BACKUP CERTIFICATE certname TO FILE ='path_to_file'  
      WITH PRIVATE KEY   
      (   
        FILE ='path_to_private_key_file',  
        ENCRYPTION BY PASSWORD ='encryption_password'   
      )   
```  
[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *certname*  
 É o nome do certificado do qual fazer backup.

 TO FILE = '*path_to_file*'  
 Especifica o caminho completo, incluindo o nome, do arquivo no qual o certificado deve ser salvo. Esse pode ser um caminho local ou um caminho UNC para um local de rede. Se apenas um nome de arquivo for especificado, o arquivo será salvo na pasta de dados de usuário da instância padrão (que pode ou não ser a pasta DATA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]). Para o SQL Server Express LocalDB, a pasta de dados de usuário da instância padrão é o caminho especificado pela variável de ambiente `%USERPROFILE%` para a conta que criou a instância.  

 WITH PRIVATE KEY especifica que a chave privada do certificado deve ser salva em um arquivo. Esta cláusula é opcional.

 FILE = '*path_to_private_key_file*'  
 Especifica o caminho completo, incluindo o nome, do arquivo no qual a chave privada deve ser salva. Esse pode ser um caminho local ou um caminho UNC para um local de rede. Se apenas um nome de arquivo for especificado, o arquivo será salvo na pasta de dados de usuário da instância padrão (que pode ou não ser a pasta DATA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]). Para o SQL Server Express LocalDB, a pasta de dados de usuário da instância padrão é o caminho especificado pela variável de ambiente `%USERPROFILE%` para a conta que criou a instância.  

 ENCRYPTION BY PASSWORD = '*encryption_password*'  
 É a senha usada para criptografar a chave privada antes de gravá-la no arquivo de backup. A senha está sujeita a verificações de complexidade.  
  
 DECRYPTION BY PASSWORD = '*decryption_password*'  
 É a senha usada para descriptografar a chave privada antes do backup da chave. Esse argumento não será necessário se o certificado for criptografado pela chave mestra. 
  
## <a name="remarks"></a>Comentários  
 Se a chave privada estiver criptografada com uma senha no banco de dados, a senha de descriptografia deverá ser especificada.  
  
 Quando você faz backup da chave privada em um arquivo, a criptografia é necessária. A senha usada para proteger a chave privada no arquivo não é a mesma senha usada para criptografar a chave privada do certificado no banco de dados.  

 As chaves privadas são salvas no formato de arquivo PVK.

 Para restaurar um certificado de backup, com ou sem a chave privada, use a instrução [CREATE CERTIFICATE](../../t-sql/statements/create-certificate-transact-sql.md).
 
 Para restaurar uma chave privada para um certificado existente no banco de dados, use a instrução [ALTER CERTIFICATE](../../t-sql/statements/alter-certificate-transact-sql.md).
 
 Ao executar um backup, os arquivos serão colocados em uma ACL da conta de serviço da instância do SQL Server. Se você precisar restaurar o certificado para um servidor que está em execução em uma conta diferente, será necessário ajustar as permissões nos arquivos para que a nova conta consiga lê-los. 
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL no certificado e o conhecimento da senha que é usada para criptografar a chave privada. Se for feito backup somente da parte pública do certificado, será necessário que esse comando tenha alguma permissão no certificado e que a permissão VIEW não seja negada ao chamador no certificado.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-exporting-a-certificate-to-a-file"></a>a. Exportando um certificado para um arquivo  
 O exemplo a seguir exporta um certificado para um arquivo.  
  
```sql
BACKUP CERTIFICATE sales05 TO FILE = 'c:\storedcerts\sales05cert';  
GO  
```  
  
### <a name="b-exporting-a-certificate-and-a-private-key"></a>B. Exportando um certificado e uma chave privada  
 No exemplo a seguir, a chave privada do certificado do qual é feito backup será criptografada com a senha `997jkhUbhk$w4ez0876hKHJH5gh`.  
  
```sql
BACKUP CERTIFICATE sales05 TO FILE = 'c:\storedcerts\sales05cert'  
    WITH PRIVATE KEY ( FILE = 'c:\storedkeys\sales05key' ,   
    ENCRYPTION BY PASSWORD = '997jkhUbhk$w4ez0876hKHJH5gh' );  
GO  
```  
  
### <a name="c-exporting-a-certificate-that-has-an-encrypted-private-key"></a>C. Exportando um certificado que tem uma chave privada criptografada  
 No exemplo a seguir, a chave privada do certificado é criptografada no banco de dados. A chave privada deve ser descriptografada com a senha `9875t6#6rfid7vble7r`. Quando o certificado for armazenado no arquivo de backup, a chave privada será criptografada com a senha `9n34khUbhk$w4ecJH5gh`.  
  
```sql
BACKUP CERTIFICATE sales09 TO FILE = 'c:\storedcerts\sales09cert'   
    WITH PRIVATE KEY ( DECRYPTION BY PASSWORD = '9875t6#6rfid7vble7r' ,  
    FILE = 'c:\storedkeys\sales09key' ,   
    ENCRYPTION BY PASSWORD = '9n34khUbhk$w4ecJH5gh' );  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [DROP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-certificate-transact-sql.md)  
 [CERTENCODED &#40;Transact-SQL&#41;](../../t-sql/functions/certencoded-transact-sql.md)  
 [CERTPRIVATEKEY &#40;Transact-SQL&#41;](../../t-sql/functions/certprivatekey-transact-sql.md)  
 [CERT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/cert-id-transact-sql.md)  
 [CERTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/certproperty-transact-sql.md)  
  
  

