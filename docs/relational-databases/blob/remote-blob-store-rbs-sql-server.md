---
title: RBS (Armazenamento de Blobs Remoto) (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 11/03/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- Remote Blob Store (RBS) [SQL Server]
- RBS (Remote Blob Store) [SQL Server]
ms.assetid: 31c947cf-53e9-4ff4-939b-4c1d034ea5b1
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: fc6bb3164b54f0799073e8b959f68b0dd625c47e
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75258180"
---
# <a name="remote-blob-store-rbs-sql-server"></a>RBS (Armazenamento de Blob Remoto) [SQL Server]
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  O[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Remote BLOB Store (RBS) é um componente complementar opcional que permite aos administradores de bancos de dados armazenar objetos binários grandes em soluções de armazenamento de mercadorias, e não diretamente no servidor de banco de dados principal.  
  
 O RBS está incluído na mídia de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , mas não é instalado pelo programa de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Pesquise RBS.msi na mídia de instalação para localizar o arquivo de instalação.

 Se você não tiver a mídia de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], baixe o RBS em uma das seguintes localizações:

| Versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] | Local de download do RBS |
|:---|:---|
| [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] | [[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Feature Pack SP2](https://www.microsoft.com/download/details.aspx?id=56833) |
| [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] | [[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] Feature Pack](https://www.microsoft.com/download/details.aspx?id=55992) |
| [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] | [[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] Página de download do RBS](https://go.microsoft.com/fwlink/?linkid=2109005) |
| &nbsp; | &nbsp; |
  
 
  
## <a name="why-rbs"></a>Por que RBS?  
  
### <a name="optimized-database-storage-and-performance"></a>Armazenamento e desempenho de banco de dados otimizados  
 O armazenamento de BLOBs no banco de dados pode consumir muito espaço em arquivo e envolver recursos caros de servidor. O RBS transfere os BLOBs para uma solução de armazenamento dedicada de sua preferência e armazena as referências aos BLOBs no banco de dados. Isso libera armazenamento do servidor para dados estruturados e também libera recursos do servidor para operações de banco de dados.  
  
### <a name="efficient-blob-management"></a>Gerenciamento eficiente de BLOBs  
 Vários recursos do RBS oferecem suporte ao gerenciamento de BLOBs:  
  
-   BLOBS são gerenciados com transações ACID (atômicas, consistentes, isoláveis e duráveis).  
  
-   BLOBs são organizados em coleções.  
  
-   São incluídas a coleta de lixo, a verificação de consistência e outras funções de manutenção.  
  
### <a name="standardized-api"></a>API padronizada  
 O RBS define um conjunto de APIs que fornecem um modelo de programação padronizado para que os aplicativos acessem e modifiquem qualquer repositório de BLOB. Cada repositório de BLOB pode especificar sua própria biblioteca de provedores, que se conecta à biblioteca cliente RBS e especifica como os BLOBs são armazenados e acessados.  
  
 Vários fornecedores de solução de armazenamento de terceiros desenvolveram provedores RBS que estão em conformidade com estas APIs padrão e oferecem suporte ao armazenamento de BLOB em várias plataformas de armazenamento.  
  
## <a name="rbs-requirements"></a>Requisitos de RBS  
 - O RBS requer o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise para o servidor de banco de dados principal no qual os metadados de BLOB são armazenados.  Porém, se você usar o provedor FILESTREAM fornecido, poderá armazenar os próprios BLOBs no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard. Para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o RBS exige, no mínimo, a versão do driver ODBC 11 para o [!INCLUDE[ssSQL14_md](../../includes/sssql14-md.md)] e a versão do driver ODBC 13 para o [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]. Os drivers estão disponíveis em [Baixar o driver ODBC para SQL Server](https://msdn.microsoft.com/library/mt703139.aspx).    
  
 O RBS inclui um provedor FILESTREAM que permite usar o RBS para armazenar BLOBs em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Caso deseje usar o RBS para armazenar BLOBs em uma solução de armazenamento diferente, utilize um provedor RBS de terceiros desenvolvido para essa solução de armazenamento ou desenvolva um provedor RBS personalizado usando a API do RBS. Um provedor de exemplo que armazena BLOBs no sistema de arquivos NTFS está disponível como um recurso de aprendizagem em [Codeplex](https://go.microsoft.com/fwlink/?LinkId=210190).  
  
## <a name="rbs-security"></a>Segurança do RBS  
 O blog da equipe do SQL Remote Blob Storage é uma boa fonte de informações sobre esse recurso. O modelo de segurança do RBS é descrito na postagem em [Modelo de Segurança do RBS](https://blogs.msdn.com/b/sqlrbs/archive/2010/08/05/rbs-security-model.aspx).  
  
### <a name="custom-providers"></a>Provedores personalizados  
 Quando você usa um provedor personalizado para armazenar BLOBs fora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], certifique-se de proteger os BLOBs armazenados com permissões e opções de criptografia apropriadas para a mídia de armazenamento usada pelo provedor personalizado.  
  
### <a name="credential-store-symmetric-key"></a>Chave simétrica do repositório de credenciais  
 Se um provedor requer a instalação e o uso de um segredo armazenado no repositório de credenciais, o RBS usará uma chave simétrica para criptografar os segredos de provedor que um cliente pode usar para obter autorização para o repositório de blob do provedor.  
  
-   O RBS 2016 usa uma chave simétrica do **AES_128** . [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] não permite a criação de novas chaves do **TRIPLE_DES** , exceto por motivos de compatibilidade com versões anteriores. Para obter mais informações, consulte [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md).  
  
-   O RBS 2014 e versões anteriores usam um repositório de credenciais que mantém os segredos criptografados usando o algoritmo de chave simétrica **TRIPLE_DES** que está desatualizado. Se no momento você estiver usando o **TRIPLE_DES**, [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que você aperfeiçoe a segurança, seguindo as etapas deste tópico para girar sua chave para um método de criptografia mais forte.  
  
 Você pode determinar as propriedades de chave simétrica de repositório de credenciais do RBS executando a seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] no banco de dados RBS:   
`SELECT * FROM sys.symmetric_keys WHERE name = 'mssqlrbs_encryption_skey';` Se a saída dessa instrução mostrar que **TRIPLE_DES** ainda é usado, então você deverá girar essa chave.  
  
### <a name="rotating-the-symmetric-key"></a>Girando a chave simétrica  
 Ao usar o RBS, você deve girar periodicamente a chave simétrica do repositório de credenciais. Essa é uma melhor prática comum de segurança para atender às políticas de segurança organizacional.  Um modo de girar a chave simétrica do repositório de credenciais do RBS é usar o [script abaixo](#Key_rotation) no banco de dados RBS.  Você também pode usar esse script para migrar para propriedades com nível de criptografia mais forte, como o comprimento da chave ou algoritmo. Faça backup de seu banco de dados antes da rotação de chaves.  Na conclusão do seu script, ele tem algumas etapas de verificação.  
Se suas políticas de segurança exigem diferentes propriedades de chave (por exemplo, comprimento de chave ou algoritmo) daquelas fornecidas, o script pode ser usado como um modelo. Modifique as propriedades de chave em dois locais: 1) a criação da chave temporária 2) a criação da chave permanente.  
  
##  <a name="rbsresources"></a> Recursos do RBS  
  
 **Exemplos do RBS**  
 Os exemplos do RBS disponíveis em [Codeplex](https://go.microsoft.com/fwlink/?LinkId=210190) demonstram como desenvolver um aplicativo RBS, e como desenvolver e instalar um provedor RBS personalizado.  
  
 **Blog do RBS**  
 O [blog do RBS](https://go.microsoft.com/fwlink/?LinkId=210315) fornece informações adicionais para ajudá-lo a compreender, implantar e manter o RBS.  
  
##  <a name="Key_rotation"></a> Script de rotação de chaves  
 Este exemplo cria um procedimento armazenado denominado `sp_rotate_rbs_symmetric_credential_key` para substituir a chave simétrica do repositório de credenciais do RBS usada atualmente  
por uma de sua escolha.  Você talvez queira fazer isso se houver uma política de segurança que exija   
a rotação de chaves periódica ou se houver requisitos de algoritmo específico.  
 Neste procedimento armazenado, uma chave simétrica usando **AES_256** substituirá a atual.  Como resultado  
da substituição de chave simétrica, segredos precisam ser criptografados novamente com a nova chave.  Esse   
procedimento armazenado também criptografará novamente os segredos.  Deve-se fazer backup do banco de dados antes da rotação de chaves.  
  
```  
CREATE PROC sp_rotate_rbs_symmetric_credential_key  
AS  
BEGIN  
BEGIN TRANSACTION;  
BEGIN TRY  
CLOSE ALL SYMMETRIC KEYS;  
  
/* Prove that all secrets can be re-encrypted, by creating a   
temporary key (#mssqlrbs_encryption_skey) and create a   
temp table (#myTable) to hold the re-encrypted secrets.    
Check to see if all re-encryption worked before moving on.*/  
  
CREATE TABLE #myTable(sql_user_sid VARBINARY(85) NOT NULL,  
    blob_store_id SMALLINT NOT NULL,  
    credential_name NVARCHAR(256) COLLATE Latin1_General_BIN2 NOT NULL,  
    old_secret VARBINARY(MAX), -- holds secrets while existing symmetric key is deleted  
    credential_secret VARBINARY(MAX)); -- holds secrets with the new permanent symmetric key  
  
/* Create a new temporary symmetric key with which the credential store secrets   
can be re-encrypted. These will be used once the existing symmetric key is deleted.*/  
CREATE SYMMETRIC KEY #mssqlrbs_encryption_skey    
    WITH ALGORITHM = AES_256 ENCRYPTION BY   
    CERTIFICATE [cert_mssqlrbs_encryption];  
  
OPEN SYMMETRIC KEY #mssqlrbs_encryption_skey    
    DECRYPTION BY CERTIFICATE [cert_mssqlrbs_encryption];  
  
INSERT INTO #myTable   
    SELECT cred_store.sql_user_sid, cred_store.blob_store_id, cred_store.credential_name,   
    encryptbykey(  
        key_guid('#mssqlrbs_encryption_skey'),   
        decryptbykeyautocert(cert_id('cert_mssqlrbs_encryption'),   
            NULL, cred_store.credential_secret)  
        ),   
    NULL  
    FROM [mssqlrbs_resources].[rbs_internal_blob_store_credentials] AS cred_store;  
  
IF( EXISTS(SELECT * FROM #myTable WHERE old_secret IS NULL))  
BEGIN  
    PRINT 'Abort. Failed to read some values';  
    SELECT * FROM #myTable;  
    ROLLBACK;  
END;  
ELSE  
BEGIN  
/* Re-encryption worked, so go ahead and drop the existing RBS credential store   
 symmetric key and replace it with a new symmetric key.*/  
DROP SYMMETRIC KEY [mssqlrbs_encryption_skey];  
  
CREATE SYMMETRIC KEY [mssqlrbs_encryption_skey]   
WITH ALGORITHM = AES_256   
ENCRYPTION BY CERTIFICATE [cert_mssqlrbs_encryption];  
  
OPEN SYMMETRIC KEY [mssqlrbs_encryption_skey]   
DECRYPTION BY CERTIFICATE [cert_mssqlrbs_encryption];  
  
/*Re-encrypt using the new permanent symmetric key.    
Verify if encryption provided a result*/  
UPDATE #myTable   
SET [credential_secret] =   
    encryptbykey(key_guid('mssqlrbs_encryption_skey'), decryptbykey(old_secret))  
  
IF( EXISTS(SELECT * FROM #myTable WHERE credential_secret IS NULL))  
BEGIN  
    PRINT 'Aborted. Failed to re-encrypt some values'  
    SELECT * FROM #myTable  
    ROLLBACK  
END  
ELSE  
BEGIN  
  
/* Replace the actual RBS credential store secrets with the newly   
encrypted secrets stored in the temp table #myTable.*/                
SET NOCOUNT ON;  
DECLARE @sql_user_sid varbinary(85);  
DECLARE @blob_store_id smallint;  
DECLARE @credential_name varchar(256);  
DECLARE @credential_secret varbinary(256);  
DECLARE curSecretValue CURSOR   
    FOR SELECT sql_user_sid, blob_store_id, credential_name, credential_secret   
FROM #myTable ORDER BY sql_user_sid, blob_store_id, credential_name;  
  
OPEN curSecretValue;  
FETCH NEXT FROM curSecretValue   
    INTO @sql_user_sid, @blob_store_id, @credential_name, @credential_secret  
WHILE @@FETCH_STATUS = 0  
BEGIN  
    UPDATE [mssqlrbs_resources].[rbs_internal_blob_store_credentials]   
        SET [credential_secret] = @credential_secret   
        FROM [mssqlrbs_resources].[rbs_internal_blob_store_credentials]   
        WHERE sql_user_sid = @sql_user_sid AND blob_store_id = @blob_store_id AND   
            credential_name = @credential_name  
FETCH NEXT FROM curSecretValue   
    INTO @sql_user_sid, @blob_store_id, @credential_name, @credential_secret  
END  
CLOSE curSecretValue  
DEALLOCATE curSecretValue  
  
DROP TABLE #myTable;  
CLOSE ALL SYMMETRIC KEYS;  
DROP SYMMETRIC KEY #mssqlrbs_encryption_skey;  
  
/* Verify that you can decrypt all encrypted credential store entries using the certificate.*/  
IF( EXISTS(SELECT * FROM [mssqlrbs_resources].[rbs_internal_blob_store_credentials]   
WHERE decryptbykeyautocert(cert_id('cert_mssqlrbs_encryption'),   
    NULL, credential_secret) IS NULL))  
BEGIN  
    print 'Aborted. Failed to verify key rotation'  
    ROLLBACK;  
END;  
ELSE  
    COMMIT;  
END;  
END;  
END TRY  
BEGIN CATCH  
     PRINT 'Exception caught: ' + cast(ERROR_NUMBER() as nvarchar) + ' ' + ERROR_MESSAGE();  
     ROLLBACK  
END CATCH  
END;  
GO  
```  
  
 Agora, você pode usar o procedimento armazenado `sp_rotate_rbs_symmetric_credential_key` para girar a chave simétrica do repositório de credenciais do RBS, enquanto os segredos permanecem os mesmos de antes e após a rotação de chaves.  
  
```  
SELECT *, decryptbykeyautocert(cert_id('cert_mssqlrbs_encryption'), NULL, credential_secret)   
FROM [mssqlrbs_resources].[rbs_internal_blob_store_credentials];  
  
EXEC sp_rotate_rbs_symmetric_credential_key;  
  
SELECT *, decryptbykeyautocert(cert_id('cert_mssqlrbs_encryption'), NULL, credential_secret)   
FROM [mssqlrbs_resources].[rbs_internal_blob_store_credentials];  
  
/* See that the RBS credential store symmetric key properties reflect the new changes*/  
SELECT * FROM sys.symmetric_keys WHERE name = 'mssqlrbs_encryption_skey';  
```  
  
## <a name="see-also"></a>Consulte Também  
[Armazenamento de Blobs Remoto e Grupos de Disponibilidade AlwaysOn (SQL Server)](../../database-engine/availability-groups/windows/remote-blob-store-rbs-and-always-on-availability-groups-sql-server.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
  
