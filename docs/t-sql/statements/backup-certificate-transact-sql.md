---
title: BACKUP CERTIFICATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 73c9176400f5d0aeb9eeae9187cedea835492fd5
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39458370"
---
# <a name="backup-certificate-transact-sql"></a>BACKUP CERTIFICATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Exporta um certificado para um arquivo.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 É a senha usada para descriptografar a chave privada antes do backup da chave. Isso não será necessário se o certificado for criptografado pela chave mestra. 
  
## <a name="remarks"></a>Remarks  
 Se a chave privada estiver criptografada com uma senha no banco de dados, a senha de descriptografia deverá ser especificada.  
  
 Quando você faz backup da chave privada em um arquivo, a criptografia é necessária. A senha usada para proteger o certificado de backup não é a mesma senha usada para criptografar a chave privada do certificado.  
  
 Para restaurar um certificado de backup, use a instrução [CREATE CERTIFICATE](../../t-sql/statements/create-certificate-transact-sql.md).
 
 Ao executar um backup, os arquivos serão colocados em uma ACL da conta de serviço da instância do SQL Server. Se você precisar restaurar o certificado para um servidor que está executando em uma conta diferente, será necessário ajustar as permissões nos arquivos para que a nova conta consiga lê-los. 
  
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
  
## <a name="see-also"></a>Consulte Também  
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [DROP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-certificate-transact-sql.md)  
  
  

