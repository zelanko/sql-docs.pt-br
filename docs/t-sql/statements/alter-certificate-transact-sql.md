---
title: ALTER CERTIFICATE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 04/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 39ab165b0587e31384c03235889bc9d7d6a240a9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="alter-certificate-transact-sql"></a>ALTER CERTIFICATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Altera a chave privada usada para criptografar um certificado ou adiciona uma se não houver nenhuma chave. Altera a disponibilidade de um certificado para [!INCLUDE[ssSB](../../includes/sssb-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
ALTER CERTIFICATE certificate_name   
      REMOVE PRIVATE KEY  
    | WITH PRIVATE KEY ( <private_key_spec> [ ,... ] )  
    | WITH ACTIVE FOR BEGIN_DIALOG = [ ON | OFF ]  
  
<private_key_spec> ::=   
      FILE = 'path_to_private_key'   
    | DECRYPTION BY PASSWORD = 'key_password'   
    | ENCRYPTION BY PASSWORD = 'password'   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
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
  
 ARQUIVO **='***path_to_private_key***'**  
 Especifica o caminho completo, incluindo o nome de arquivo, até a chave privada. Esse parâmetro pode ser um caminho local ou um caminho de UNC a um local de rede. Esse arquivo será acessado dentro do contexto de segurança da conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ao usar essa opção, verifique se a conta de serviço tem acesso ao arquivo especificado.  
  
 DECRYPTION BY PASSWORD **='***key_password***'**  
 Especifica a senha que é obrigatória para descriptografar a chave privada.  
  
 CRIPTOGRAFIA por senha **='***senha***'**  
 Especifica a senha usada para criptografar a chave privada do certificado no banco de dados. *senha* devem atender aos requisitos da política de senha do Windows do computador que está executando a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Password Policy](../../relational-databases/security/password-policy.md).  
  
 REMOVE PRIVATE KEY  
 Especifica que a chave privada não deve mais ser mantida dentro do banco de dados.  
  
 ACTIVE FOR BEGIN_DIALOG  **=**  {ON | OFF}  
 Disponibiliza o certificado para o iniciador de uma conversa de caixa de diálogo do [!INCLUDE[ssSB](../../includes/sssb-md.md)].  
  
## <a name="remarks"></a>Comentários  
 A chave privada deve corresponder à chave pública especificada por *certificate_name*.  
  
 A cláusula DECRYPTION BY PASSWORD pode ser omitida se a senha no arquivo estiver protegida com uma senha nula.  
  
 Quando a chave privada de um certificado que já existe no banco de dados for importada a partir de um arquivo, a chave privada será protegida automaticamente pela chave mestra do banco de dados. Para proteger a chave privada com uma senha, use a frase ENCRYPTION BY PASSWORD.  
  
 A opção REMOVE PRIVATE KEY exclui a chave privada do certificado do banco de dados. Você pode fazer isso quando o certificado for usado para confirmar assinaturas ou em cenários do [!INCLUDE[ssSB](../../includes/sssb-md.md)] que não requerem uma chave privada. Não remova a chave privada de um certificado que protege uma chave simétrica.  
  
 Não é necessário especificar uma senha de descriptografia quando a chave privada for criptografada com a chave mestra do banco de dados.  
  
> [!IMPORTANT]  
>  Sempre faça uma cópia de arquivamento de uma chave privada antes de removê-la de um banco de dados. Para obter mais informações, veja [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md).  
  
 A opção WITH PRIVATE KEY não está disponível em um banco de dados independente.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER no certificado.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-changing-the-password-of-a-certificate"></a>A. Alterando a senha de um certificado  
  
```  
ALTER CERTIFICATE Shipping04   
    WITH PRIVATE KEY (DECRYPTION BY PASSWORD = 'pGF$5DGvbd2439587y',  
    ENCRYPTION BY PASSWORD = '4-329578thlkajdshglXCSgf');  
GO  
```  
  
### <a name="b-changing-the-password-that-is-used-to-encrypt-the-private-key"></a>B. Alterando a senha usada para criptografar a chave privada  
  
```  
ALTER CERTIFICATE Shipping11   
    WITH PRIVATE KEY (ENCRYPTION BY PASSWORD = '34958tosdgfkh##38',  
    DECRYPTION BY PASSWORD = '95hkjdskghFDGGG4%');  
GO  
```  
  
### <a name="c-importing-a-private-key-for-a-certificate-that-is-already-present-in-the-database"></a>C. Importando uma chave privada para um certificado que já está existe no banco de dados  
  
```  
ALTER CERTIFICATE Shipping13   
    WITH PRIVATE KEY (FILE = 'c:\\importedkeys\Shipping13',  
    DECRYPTION BY PASSWORD = 'GDFLKl8^^GGG4000%');  
GO  
```  
  
### <a name="d-changing-the-protection-of-the-private-key-from-a-password-to-the-database-master-key"></a>D. Alterando a proteção da chave privada de uma senha para a chave mestra de banco de dados  
  
```  
ALTER CERTIFICATE Shipping15   
    WITH PRIVATE KEY (DECRYPTION BY PASSWORD = '95hk000eEnvjkjy#F%');  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [Remover certificado &#40; Transact-SQL &#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

