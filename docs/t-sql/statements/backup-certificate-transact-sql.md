---
title: O certificado de BACKUP (Transact-SQL) | Microsoft Docs
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
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0711d429f689fa0aaf0d4332ff2243835d231338
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="backup-certificate-transact-sql"></a>BACKUP CERTIFICATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Exporta um certificado para um arquivo.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
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
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
BACKUP CERTIFICATE certname TO FILE ='path_to_file'  
      WITH PRIVATE KEY   
      (   
        FILE ='path_to_private_key_file',  
        ENCRYPTION BY PASSWORD ='encryption_password'   
      )   
```  
  
## <a name="arguments"></a>Argumentos  
 *path_to_file*  
 Especifica o caminho completo, incluindo o nome, do arquivo no qual o certificado deve ser salvo. Esse pode ser um caminho local ou um caminho UNC para um local de rede. O padrão é o caminho da pasta DATA do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *path_to_private_key_file*  
 Especifica o caminho completo, incluindo o nome, do arquivo no qual a chave privada deve ser salva. Esse pode ser um caminho local ou um caminho UNC para um local de rede. O padrão é o caminho da pasta DATA do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *encryption_password*  
 É a senha usada para criptografar a chave privada antes de gravá-la no arquivo de backup. A senha está sujeita a verificações de complexidade.  
  
 *decryption_password*  
 É a senha usada para descriptografar a chave privada antes do backup da chave.  
  
## <a name="remarks"></a>Comentários  
 Se a chave privada estiver criptografada com uma senha no banco de dados, a senha de descriptografia deverá ser especificada.  
  
 Quando você faz backup da chave privada em um arquivo, a criptografia é necessária. A senha usada para proteger o certificado de backup não é a mesma senha usada para criptografar a chave privada do certificado.  
  
 Para restaurar o backup de um certificado, use o [CREATE CERTIFICATE](../../t-sql/statements/create-certificate-transact-sql.md)instrução.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL no certificado e o conhecimento da senha que é usada para criptografar a chave privada. Se for feito backup somente da parte pública do certificado, será necessário ter alguma permissão no certificado e que a permissão VIEW não seja negada ao chamador no certificado.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-exporting-a-certificate-to-a-file"></a>A. Exportando um certificado para um arquivo  
 O exemplo a seguir exporta um certificado para um arquivo.  
  
```  
BACKUP CERTIFICATE sales05 TO FILE = 'c:\storedcerts\sales05cert';  
GO  
```  
  
### <a name="b-exporting-a-certificate-and-a-private-key"></a>B. Exportando um certificado e uma chave privada  
 No exemplo a seguir, a chave privada do certificado do qual é feito backup será criptografada com a senha `997jkhUbhk$w4ez0876hKHJH5gh`.  
  
```  
BACKUP CERTIFICATE sales05 TO FILE = 'c:\storedcerts\sales05cert'  
    WITH PRIVATE KEY ( FILE = 'c:\storedkeys\sales05key' ,   
    ENCRYPTION BY PASSWORD = '997jkhUbhk$w4ez0876hKHJH5gh' );  
GO  
```  
  
### <a name="c-exporting-a-certificate-that-has-an-encrypted-private-key"></a>C. Exportando um certificado que tem uma chave privada criptografada  
 No exemplo a seguir, a chave privada do certificado é criptografada no banco de dados. A chave privada deve ser descriptografada com a senha `9875t6#6rfid7vble7r`. Quando o certificado for armazenado no arquivo de backup, a chave privada será criptografada com a senha `9n34khUbhk$w4ecJH5gh`.  
  
```  
BACKUP CERTIFICATE sales09 TO FILE = 'c:\storedcerts\sales09cert'   
    WITH PRIVATE KEY ( DECRYPTION BY PASSWORD = '9875t6#6rfid7vble7r' ,  
    FILE = 'c:\storedkeys\sales09key' ,   
    ENCRYPTION BY PASSWORD = '9n34khUbhk$w4ecJH5gh' );  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-exporting-a-certificate-and-a-private-key"></a>D. Exportando um certificado e uma chave privada  
 No exemplo a seguir, a chave privada do certificado do qual é feito backup será criptografada com a senha `997jkhUbhk$w4ez0876hKHJH5gh`.  
  
```  
BACKUP CERTIFICATE sales05 TO FILE = '\\ServerA7\storedcerts\sales05cert'  
    WITH PRIVATE KEY ( FILE = '\\ServerA7\storedkeys\sales05key' ,   
    ENCRYPTION BY PASSWORD = '997jkhUbhk$w4ez0876hKHJH5gh' );  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [Remover certificado &#40; Transact-SQL &#41;](../../t-sql/statements/drop-certificate-transact-sql.md)  
  
  


