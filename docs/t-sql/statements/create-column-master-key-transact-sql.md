---
description: CREATE COLUMN MASTER KEY (Transact-SQL)
title: CREATE COLUMN MASTER KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SQL13.SWB.NEWCOLUMNMASTERKEYDEF.GENERAL.F1
- SQL13.SWB.COLUMNMASTERKEYDEF.GENERAL.F1
- CREATE COLUMN MASTER KEY
- COLUMN MASTER KEY
- CREATE_COLUMN_MASTER_KEY_TSQL
- COLUMN_MASTER_KEY_TSQL
- SQL13.SWB.NEWCOLUMNMASTERKEY.GENERAL.F1
- SQL13.SWB.COLUMNMASTERKEY.GENERAL.F1
dev_langs:
- TSQL
helpviewer_keywords:
- column master key definition
- column master key, create
- CREATE COLUMN MASTER KEY statement
- Always Encrypted, create column master key
ms.assetid: f8926b95-e146-4e3f-b56b-add0c0d0a30e
author: jaszymas
ms.author: jaszymas
ms.openlocfilehash: a92d256d376b9931924a7bf6672769bcd19917f4
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88645946"
---
# <a name="create-column-master-key-transact-sql"></a>CREATE COLUMN MASTER KEY (Transact-SQL)
[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]


Cria um objeto de metadados de chave mestra de coluna em um banco de dados. Uma entrada de metadados de chave mestra de coluna representa uma chave, armazenada em um repositório de chave externa. A chave protege (criptografa) chaves de criptografia de coluna quando você está usando [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md) ou [Always Encrypted com enclaves seguros](../../relational-databases/security/encryption/always-encrypted-enclaves.md). Múltiplas chaves mestras de coluna permitem a rotação periódica de chaves para aumentar a segurança. Crie uma chave mestra de coluna em um repositório de chaves e seu objeto de metadados relacionado no banco de dados usando o Pesquisador de Objetos no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou no PowerShell. Para obter detalhes, veja [Visão geral do gerenciamento de chaves para Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md).  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
 

> [!IMPORTANT]
> A criação de chaves habilitadas para enclave (com ENCLAVE_COMPUTATIONS) requer o [Always Encrypted com enclaves seguros](../../relational-databases/security/encryption/always-encrypted-enclaves.md).

## <a name="syntax"></a>Sintaxe  

```syntaxsql
CREATE COLUMN MASTER KEY key_name   
    WITH (  
        KEY_STORE_PROVIDER_NAME = 'key_store_provider_name',  
        KEY_PATH = 'key_path'   
        [,ENCLAVE_COMPUTATIONS (SIGNATURE = signature)]
         )   
[;]  
```  

## <a name="arguments"></a>Argumentos
*key_name*  
O nome da chave mestra de coluna no banco de dados.  
  
*key_store_provider_name*  
Especifica o nome de um provedor de repositório de chaves. Um provedor de repositório de chaves é um componente de software do lado do cliente com um repositório de chaves que contém a chave mestra de coluna. 

Um driver cliente, habilitado com o Always Encrypted:

- Usa o nome do provedor do repositório de chaves 
- Pesquisa o provedor do repositório de chaves no Registro do driver dos provedores do repositório de chaves 

Em seguida, o driver usa o provedor para descriptografar chaves de criptografia de coluna. As chaves de criptografia de coluna são protegidas pela chave mestra da coluna. A chave mestra da coluna é armazenada no repositório de chaves subjacente. Um valor de texto não criptografado da chave de criptografia de coluna então é usado para criptografar parâmetros de consulta, correspondentes às colunas de banco de dados criptografadas. Ou a chave de criptografia da coluna descriptografa os resultados da consulta de colunas criptografadas.  
  
Bibliotecas de drivers de cliente habilitadas para Always Encrypted incluem provedores de repositório de chaves para repositórios de chaves populares.   
  
Um conjunto de provedores disponíveis depende do tipo e da versão do driver do cliente. Veja a documentação do Always Encrypted para drivers específicos: [Desenvolver aplicativos usando o Always Encrypted](../../relational-databases/security/encryption/always-encrypted-client-development.md).


A tabela a seguir mostra os nomes de provedores de sistema:  
  
|Nome do Provedor do repositório de chaves|Repositório de chaves subjacente|  
    |-----------------------------|--------------------------|
    |'MSSQL_CERTIFICATE_STORE'|Repositório de Certificados do Windows| 
    |'MSSQL_CSP_PROVIDER'|Um repositório, como um HSM (módulo de segurança de hardware) compatível com o Microsoft CryptoAPI.|
    |'MSSQL_CNG_STORE'|Um repositório, como um HSM (módulo de segurança de hardware) (HSM) compatível com a Cryptography API Next Generation.|  
    |'AZURE_KEY_VAULT'|Veja [Introdução ao Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)|  
    |'MSSQL_JAVA_KEYSTORE'| Repositório de chaves Java.}
  

No seu driver cliente habilitado para Always Encrypted, é possível configurar um provedor de repositório de chaves personalizado para armazenar chaves mestras de coluna para as quais não há nenhum provedor de repositório de chaves interno. Os nomes de provedores de repositório de chaves personalizado não podem começar com 'MSSQL_', que é um prefixo reservado para provedores de repositório de chaves [!INCLUDE[msCoName](../../includes/msconame-md.md)]. 

  
key_path  
O caminho da chave no repositório de chave mestra de coluna. O caminho da chave deve ser válido para cada aplicativo cliente que deve criptografar ou descriptografar dados. Os dados são armazenados em uma coluna (indiretamente) protegida pela chave mestra de coluna referenciada. O aplicativo cliente deve ter acesso à chave. O formato do caminho da chave é específico do provedor do repositório de chaves. A lista a seguir descreve o formato de caminhos de chave para provedores de repositório de chaves do sistema Microsoft específicos.  
  
-   **Nome do provedor:** MSSQL_CERTIFICATE_STORE  
  
    **Formato do caminho da chave:** *CertificateStoreName*/*CertificateStoreLocation*/*CertificateThumbprint*  
  
     Em que:  
  
    *CertificateStoreLocation*  
    Local do repositório de certificados, que deve ser o Usuário Atual ou o Computador Local. Para obter mais informações, veja [Computador local e repositórios de certificados do usuário atual](https://msdn.microsoft.com/library/windows/hardware/ff548653.aspx).  
  
    *CertificateStore*  
    Nome do repositório de certificados, por exemplo 'Meu'.  
  
    *CertificateThumbprint*  
    Impressão digital do certificado.  
  
    **Exemplos:**  
  
    ```  
    N'CurrentUser/My/BBF037EC4A133ADCA89FFAEC16CA5BFA8878FB94'  
  
    N'LocalMachine/My/CA5BFA8878FB94BBF037EC4A133ADCA89FFAEC16'  
    ```  
  
-   **Nome do provedor:** MSSQL_CSP_PROVIDER  
  
    **Formato do caminho da chave:** *ProviderName*/*KeyIdentifier*  
  
    Em que:  
  
    *ProviderName*  
    O nome de um CSP (Provedor de Serviço de Criptografia), que implementa a CAPI, para o repositório de chave mestra de coluna. Se você usar um HSM como um repositório de chaves, o nome do provedor deverá ser o nome do CSP dado pelo seu fornecedor HSM. O provedor deve ser instalado em um computador cliente.  
  
    *KeyIdentifier*  
    Identificador da chave, usado como uma chave mestra de coluna, no repositório de chaves.  
  
    **Exemplos:**  
  
    ```  
    N'My HSM CSP Provider/AlwaysEncryptedKey1'  
    ```  
  
-   **Nome do provedor:** MSSQL_CNG_STORE  
  
    **Formato do caminho da chave:** *ProviderName*/*KeyIdentifier*  
  
    Em que:  
  
    *ProviderName*  
    Nome do KSP (provedor de armazenamento de chaves), que implementa a API Cryptography: Next Generation (CNG) API para o repositório de chaves mestras de coluna. Se você usar um HSM como um repositório de chaves, o nome do provedor deverá ser o nome do KSP dado pelo seu fornecedor HSM. O provedor deve ser instalado em um computador cliente.  
  
    *KeyIdentifier*  
    Identificador da chave, usado como uma chave mestra de coluna, no repositório de chaves.  
  
    **Exemplos:**  
  
    ```  
    N'My HSM CNG Provider/AlwaysEncryptedKey1'  
    ```  

-   **Nome do provedor:** AZURE_KEY_STORE  
  
    **Formato do caminho da chave:** *KeyUrl*  
  
    Em que:  
  
    *KeyUrl*  
    A URL da chave no Azure Key Vault

ENCLAVE_COMPUTATIONS  
Especifica se a chave mestra da coluna está habilitada para enclave. Você pode compartilhar todas as chaves de criptografia de coluna, criptografadas com a chave mestra de coluna, com um enclave seguro no servidor e usá-las para cálculos dentro do enclave. Para obter mais informações, consulte [Always Encrypted com enclaves seguros](../../relational-databases/security/encryption/always-encrypted-enclaves.md).

*assinatura*  
Um literal binário que é um resultado de assinar digitalmente o *caminho da chave* e a configuração ENCLAVE_COMPUTATIONS com a chave mestra de coluna. A assinatura reflete se ENCLAVE_COMPUTATIONS for especificado ou não. A assinatura protege os valores assinados de serem alterados por usuários não autorizados. Um driver de cliente habilitado para Always Encrypted verificará a assinatura e retornará um erro para o aplicativo se a assinatura for inválida. A assinatura deve ser gerada usando ferramentas do lado do cliente. Para obter mais informações, consulte [Always Encrypted com enclaves seguros](../../relational-databases/security/encryption/always-encrypted-enclaves.md).

## <a name="remarks"></a>Comentários

Crie uma entrada de metadados de chave mestra de coluna antes de uma entrada de metadados de chave de criptografia de coluna ser criada no banco de dados e antes de qualquer coluna no banco de dados poder ser criptografada usando Always Encrypted. Uma entrada de chave mestra de coluna nos metadados não contém a chave mestra de coluna real. A chave mestra de coluna deve ser armazenada em um repositório de chaves de coluna externo (fora do SQL Server). O nome do provedor de repositório de chaves e o caminho da chave mestra de coluna nos metadados devem ser válidos para um aplicativo cliente. O aplicativo cliente precisa usar a chave mestra de coluna para descriptografar uma chave de criptografia de coluna. A chave de criptografia de coluna é criptografada com a chave mestra de coluna. O aplicativo cliente também precisa consultar colunas criptografadas.

É recomendável usar ferramentas, como o SSMS (SQL Server Management Studio) ou o PowerShell para gerenciar chaves mestras de coluna. Essas ferramentas geram assinaturas (se você estiver usando Always Encrypted com enclaves seguros) e emitem automaticamente instruções `CREATE COLUMN MASTER KEY` para criar objetos de metadados de chave de criptografia de coluna. Confira [Provisionar chaves Always Encrypted usando o SQL Server Management Studio](../../relational-databases/security/encryption/configure-always-encrypted-keys-using-ssms.md) e [Provisionar chaves Always Encrypted usando o PowerShell](../../relational-databases/security/encryption/configure-always-encrypted-keys-using-powershell.md). 

  
## <a name="permissions"></a>Permissões  
Requer a permissão **ALTER ANY COLUMN MASTER KEY**.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-column-master-key"></a>a. Criando uma chave mestra de coluna  
O exemplo a seguir cria uma entrada de metadados de chave mestra de coluna para uma chave mestra de coluna. A chave mestra de coluna é armazenada no Repositório de Certificados para aplicativos cliente que usam o provedor MSSQL_CERTIFICATE_STORE para acessar a chave mestra de coluna:  
  
```sql  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
     KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',   
     KEY_PATH = 'Current User/Personal/f2260f28d909d21c642a3d8e0b45a830e79a1420'  
   );  
```  
  
Criar uma entrada de metadados de chave mestra de coluna para uma chave mestra de coluna. Aplicativos cliente, que usam o provedor MSSQL_CNG_STORE, acessam a chave mestra de coluna:  
  
```sql  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'MSSQL_CNG_STORE',    
    KEY_PATH = N'My HSM CNG Provider/AlwaysEncryptedKey'  
);  
```  
  
Criar uma entrada de metadados de chave mestra de coluna para uma chave mestra de coluna. A chave mestra de coluna é armazenada no Azure Key Vault, para aplicativos cliente que usam o provedor AZURE_KEY_VAULT, para acessar a chave mestra de coluna.  
  
```sql  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'AZURE_KEY_VAULT',  
    KEY_PATH = N'https://myvault.vault.azure.net:443/keys/  
        MyCMK/4c05f1a41b12488f9cba2ea964b6a700');  
```  
  
Criar uma entrada de metadados de chave mestra de coluna para uma chave mestra de coluna. A chave mestra de coluna é armazenada em um repositório de chave mestra de coluna personalizada:  
  
```sql  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = 'CUSTOM_KEY_STORE',    
    KEY_PATH = 'https://contoso.vault/sales_db_tce_key'  
);  
```  
### <a name="b-creating-an-enclave-enabled-column-master-key"></a>B. Criando uma chave mestra da coluna habilitada para enclave  
O exemplo a seguir cria uma entrada de metadados de chave mestra de coluna para uma chave mestra de coluna habilitada para enclave. A chave mestra de coluna habilitada para enclave é armazenada em um Repositório de Certificados, para aplicativos cliente que usam o provedor MSSQL_CERTIFICATE_STORE, para acessar a chave mestra de coluna:  
  
```sql  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
     KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',   
     KEY_PATH = 'Current User/Personal/f2260f28d909d21c642a3d8e0b45a830e79a1420'  
     ENCLAVE_COMPUTATIONS (SIGNATURE = 0xA80F5B123F5E092FFBD6014FC2226D792746468C901D9404938E9F5A0972F38DADBC9FCBA94D9E740F3339754991B6CE26543DEB0D094D8A2FFE8B43F0C7061A1FFF65E30FDDF39A1B954F5BA206AAC3260B0657232020542419990261D878318CC38EF4E853970ED69A8D4A306693B8659AAC1C4E4109DE5EB148FD0E1FDBBC32F002C1D8199D313227AD689279D8DEEF91064DF122C19C3767C463723AB663A6F8412AE17E745922C0E3A257EAEF215532588ACCBD440A03C7BC100A38BD0609A119E1EF7C5C6F1B086C68AB8873DBC6487B270340E868F9203661AFF0492CEC436ABF7C4713CE64E38CF66C794B55636BFA55E5B6554AF570CF73F1BE1DBD)
  );  
```  
  
Criar uma entrada de metadados de chave mestra de coluna para uma chave mestra de coluna habilitada para enclave. A chave mestra de coluna habilitada para enclave é armazenada no Azure Key Vault, para aplicativos cliente que usam o provedor AZURE_KEY_VAULT, para acessar a chave mestra de coluna.  
  
```sql  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'AZURE_KEY_VAULT',  
    KEY_PATH = N'https://myvault.vault.azure.net:443/keys/MyCMK/4c05f1a41b12488f9cba2ea964b6a700');
    ENCLAVE_COMPUTATIONS (SIGNATURE = 0xA80F5B123F5E092FFBD6014FC2226D792746468C901D9404938E9F5A0972F38DADBC9FCBA94D9E740F3339754991B6CE26543DEB0D094D8A2FFE8B43F0C7061A1FFF65E30FDDF39A1B954F5BA206AAC3260B0657232020582413990261D878318CC38EF4E853970ED69A8D4A306693B8659AAC1C4E4109DE5EB148FD0E1FDBBC32F002C1D8199D313227AD689279D8DEEF91064DF122C19C3767C463723AB663A6F8412AE17E745922C0E3A257EAEF215532588ACCBD440A03C7BC100A38BD0609A119E1EF7C5C6F1B086C68AB8873DBC6487B270340E868F9203661AFF0492CEC436ABF7C4713CE64E38CF66C794B55636BFA55E5B6554AF570CF73F1BE1DBD)
  );
```  
  
## <a name="see-also"></a>Consulte Também
 
* [DROP COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-column-master-key-transact-sql.md)   
* [CREATE COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)
* [sys.column_master_keys (Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
* [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
* [Always Encrypted com enclaves seguros](../../relational-databases/security/encryption/always-encrypted-enclaves.md)   
* [Visão geral do gerenciamento de chaves do Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)   
* [Gerenciar chaves para Always Encrypted com enclaves seguros](../../relational-databases/security/encryption/always-encrypted-enclaves-manage-keys.md)   
  
