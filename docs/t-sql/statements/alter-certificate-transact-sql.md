---
title: ALTER CERTIFICATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/22/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_CERTIFICATE_TSQL
- ALTER CERTIFICATE
dev_langs:
- TSQL
helpviewer_keywords:
- ENCRYPTION BY PASSWORD option
- encryption [SQL Server], certificates
- modifying certificates
- private keys [SQL Server]
- ALTER CERTIFICATE statement
- certificates [SQL Server], modifying
ms.assetid: da4dc25e-72e0-4036-87ce-22de83160836
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2711a9b2bb1530b979a8294b2d3f9a08f764ec6c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68065962"
---
# <a name="alter-certificate-transact-sql"></a>ALTER CERTIFICATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

  Altera a senha usada para criptografar a chave privada de um certificado, remove a chave privada ou importa a chave privada, caso nenhuma esteja presente. Altera a disponibilidade de um certificado para [!INCLUDE[ssSB](../../includes/sssb-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
ALTER CERTIFICATE certificate_name   
      REMOVE PRIVATE KEY  
    | WITH PRIVATE KEY ( <private_key_spec> )  
    | WITH ACTIVE FOR BEGIN_DIALOG = { ON | OFF }  
  
<private_key_spec> ::=   
      {   
        { FILE = 'path_to_private_key' | BINARY = private_key_bits }  
         [ , DECRYPTION BY PASSWORD = 'current_password' ]  
         [ , ENCRYPTION BY PASSWORD = 'new_password' ]  
      }  
    |  
      {  
         [ DECRYPTION BY PASSWORD = 'current_password' ]  
         [ [ , ] ENCRYPTION BY PASSWORD = 'new_password' ]  
      }  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
ALTER CERTIFICATE certificate_name   
{  
      REMOVE PRIVATE KEY  
    | WITH PRIVATE KEY (   
        FILE = '<path_to_private_key>',  
        DECRYPTION BY PASSWORD = '<key password>' )
}  
```  
  
## <a name="arguments"></a>Argumentos  
 *certificate_name*  
 É o nome exclusivo pelo qual o certificado é conhecido no banco de dados.  
  
 REMOVE PRIVATE KEY  
 Especifica que a chave privada não deve mais ser mantida dentro do banco de dados.  
  
 WITH PRIVATE KEY especifica que a chave privada do certificado está carregada no SQL Server.

 FILE ='*path_to_private_key*'  
 Especifica o caminho completo, incluindo o nome de arquivo, até a chave privada. Esse parâmetro pode ser um caminho local ou um caminho de UNC a um local de rede. Esse arquivo será acessado dentro do contexto de segurança da conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ao usar essa opção, verifique se a conta de serviço tem acesso ao arquivo especificado.
 
 Se apenas um nome de arquivo for especificado, o arquivo será salvo na pasta de dados de usuário padrão para a instância. Essa pasta pode (ou não) ser a pasta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DATA. Para o SQL Server Express LocalDB, a pasta de dados de usuário padrão para a instância é o caminho especificado pela variável de ambiente `%USERPROFILE%` para a conta que criou a instância.  
  
 BINARY ='*private_key_bits*'  
 **Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Bits de chave privada especificados como constante binária. Estes bits podem estar no formato criptografado. Se criptografado, o usuário deve fornecer uma senha de descriptografia. Verificações de diretiva de senha não são executadas nesta senha. Os bits de chave privada devem estar em um formato de arquivo PVK.  
  
 DECRYPTION BY PASSWORD ='*current_password*'  
 Especifica a senha que é obrigatória para descriptografar a chave privada.  
  
 ENCRYPTION BY PASSWORD ='*new_password*'  
 Especifica a senha usada para criptografar a chave privada do certificado no banco de dados. A *new_password* deve atender aos requisitos da política de senha do Windows do computador que executa a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Password Policy](../../relational-databases/security/password-policy.md).  
  
 ACTIVE FOR BEGIN_DIALOG **=** { ON | OFF }  
 Disponibiliza o certificado para o iniciador de uma conversa de caixa de diálogo do [!INCLUDE[ssSB](../../includes/sssb-md.md)].  
  
## <a name="remarks"></a>Remarks  
 A chave privada deve corresponder à chave pública especificada por *certificate_name*.  
  
 A cláusula DECRYPTION BY PASSWORD pode ser omitida se a senha no arquivo estiver protegida com uma senha nula.  
  
 Quando a chave privada de um certificado que já existe no banco de dados for importada, a chave privada será protegida automaticamente pela chave mestra do banco de dados. Para proteger a chave privada com uma senha, use a cláusula ENCRYPTION BY PASSWORD.  
  
 A opção REMOVE PRIVATE KEY exclui a chave privada do certificado do banco de dados. Você pode remover a chave privada quando o certificado for usado para confirmar assinaturas ou em cenários do [!INCLUDE[ssSB](../../includes/sssb-md.md)] que não requerem uma chave privada. Não remova a chave privada de um certificado que protege uma chave simétrica. A chave privada precisará ser restaurada para assinar quaisquer módulos ou cadeias de caracteres adicionais que devam ser verificados com o certificado ou para descriptografar um valor que foi criptografado com o certificado.   
  
 Não é necessário especificar uma senha de descriptografia quando a chave privada for criptografada com a chave mestra do banco de dados.  
 
 Para alterar a senha usada para criptografar a chave privada, não especifique as cláusulas FILE ou BINARY.
  
> [!IMPORTANT]  
>  Sempre faça uma cópia de arquivamento de uma chave privada antes de removê-la de um banco de dados. Para obter mais informações, veja [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md) e [CERTPRIVATEKEY &#40;Transact-SQL&#41;](../../t-sql/functions/certprivatekey-transact-sql.md).  
  
 A opção WITH PRIVATE KEY não está disponível em um banco de dados independente.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER no certificado.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-removing-the-private-key-of-a-certificate"></a>A. Removendo a chave privada de um certificado  
  
```  
ALTER CERTIFICATE Shipping04   
    REMOVE PRIVATE KEY;  
GO  
```  
  
### <a name="b-changing-the-password-that-is-used-to-encrypt-the-private-key"></a>B. Alterando a senha usada para criptografar a chave privada  
  
```  
ALTER CERTIFICATE Shipping11   
    WITH PRIVATE KEY (DECRYPTION BY PASSWORD = '95hkjdskghFDGGG4%',  
    ENCRYPTION BY PASSWORD = '34958tosdgfkh##38');  
GO  
```  
  
### <a name="c-importing-a-private-key-for-a-certificate-that-is-already-present-in-the-database"></a>C. Importando uma chave privada para um certificado que já está existe no banco de dados  
  
```  
ALTER CERTIFICATE Shipping13   
    WITH PRIVATE KEY (FILE = 'c:\importedkeys\Shipping13',  
    DECRYPTION BY PASSWORD = 'GDFLKl8^^GGG4000%');  
GO  
```  
  
### <a name="d-changing-the-protection-of-the-private-key-from-a-password-to-the-database-master-key"></a>D. Alterando a proteção da chave privada de uma senha para a chave mestra de banco de dados  
  
```  
ALTER CERTIFICATE Shipping15   
    WITH PRIVATE KEY (DECRYPTION BY PASSWORD = '95hk000eEnvjkjy#F%');  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
 [DROP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-certificate-transact-sql.md)  
 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)  
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
 [CERTENCODED &#40;Transact-SQL&#41;](../../t-sql/functions/certencoded-transact-sql.md)  
 [CERTPRIVATEKEY &#40;Transact-SQL&#41;](../../t-sql/functions/certprivatekey-transact-sql.md)  
 [CERT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/cert-id-transact-sql.md)  
 [CERTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/certproperty-transact-sql.md)  
  
  

