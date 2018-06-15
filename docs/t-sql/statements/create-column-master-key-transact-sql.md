---
title: CREATE COLUMN MASTER KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: e5dafed981c030b5f06e41610fd3add6c4af0238
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33071213"
---
# <a name="create-column-master-key-transact-sql"></a>CREATE COLUMN MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Cria um objeto de metadados de chave mestra de coluna em um banco de dados. Uma entrada de metadados de chave mestra de coluna que representa uma chave, armazenada em um repositório de chaves externas, que é usada para proteger (criptografar) as chaves de criptografia de coluna ao usar o recursos [Always Encrypted &#40;Mecanismo de Banco de Dados&#41; ](../../relational-databases/security/encryption/always-encrypted-database-engine.md). Múltiplas chaves mestras de coluna permitem a rotação de chaves; altere periodicamente a chave para aumentar a segurança. Você pode criar uma chave mestra de coluna em um repositório de chaves e seu objeto de metadados correspondente no banco de dados usando o Pesquisador de Objetos no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou no PowerShell. Para obter detalhes, veja [Visão geral do gerenciamento de chaves para Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
CREATE COLUMN MASTER KEY key_name   
    WITH (  
        KEY_STORE_PROVIDER_NAME = 'key_store_provider_name',  
        KEY_PATH = 'key_path'   
         )   
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *key_name*  
 É o nome pelo qual a chave mestra de coluna será conhecida no banco de dados.  
  
 *key_store_provider_name*  
 Especifica o nome de um provedor de repositório de chaves, que é um componente de software do cliente que encapsula um repositório de chaves que contém a chave mestra de coluna. Um driver cliente habilitado para Always Encrypted usa um nome de provedor de repositório de chaves para pesquisar um provedor de repositório de chaves no registro do driver de provedores de repositório de chaves. O driver usa o provedor para descriptografar chaves de criptografia de coluna, protegidas pela chave mestra da coluna, armazenadas no repositório de chaves subjacente. Um valor de texto não criptografado da chave de criptografia de coluna então é usado para criptografar parâmetros de consulta, correspondentes às colunas de banco de dados criptografadas, ou para descriptografar os resultados da consulta de colunas criptografadas.  
  
 Bibliotecas de drivers de cliente habilitadas para Always Encrypted incluem provedores de repositório de chaves para repositórios de chaves populares.   
  
Um conjunto de provedores disponíveis depende do tipo e da versão do driver do cliente. veja a documentação do Always Encrypted para drivers específicos:

[Desenvolver aplicativos usando o Always Encrypted com o Provedor do .NET Framework para SQL Server](../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)


As tabelas abaixo capturam os nomes de provedores do sistema:  
  
|Nome do Provedor do repositório de chaves|Repositório de chaves subjacente|  
    |-----------------------------|--------------------------|
    |'MSSQL_CERTIFICATE_STORE'|Repositório de Certificados do Windows| 
    |'MSSQL_CSP_PROVIDER'|Um repositório, como um HSM (módulo de segurança de hardware) compatível com o Microsoft CryptoAPI.|
    |'MSSQL_CNG_STORE'|Um repositório, como um HSM (módulo de segurança de hardware) (HSM) compatível com a Cryptography API Next Generation.|  
    |'Azure_Key_Vault'|Veja [Introdução ao Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)|  
  

 Você pode implementar um provedor de repositório de chaves personalizado para armazenar chaves mestras de coluna em um repositório para o qual não há nenhum provedor de repositório de chave mestra interno em seu driver de cliente habilitado para Always Encrypted.  Observe que os nomes de provedores de repositório de chaves personalizado não podem começar com 'MSSQL _', que é um prefixo reservado para provedores de repositório de chaves [!INCLUDE[msCoName](../../includes/msconame-md.md)]. 

  
 key_path  
 O caminho da chave no repositório de chave mestra de coluna. O caminho da chave deve ser válido no contexto de cada aplicativo cliente que deve criptografar ou descriptografar dados armazenados em uma coluna (indiretamente) protegida pela chave mestra de coluna referenciada, e o aplicativo cliente precisa ter permissão para acessar a chave. O formato do caminho da chave é específico do provedor do repositório de chaves. A lista a seguir descreve o formato de caminhos de chave para provedores de repositório de chaves do sistema Microsoft específicos.  
  
-   **Nome do provedor:** MSSQL_CERTIFICATE_STORE  
  
     **Formato do caminho da chave:** *CertificateStoreName*/*CertificateStoreLocation*/*CertificateThumbprint*  
  
     Onde:  
  
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
  
     Onde:  
  
     *ProviderName*  
     O nome de um CSP (Provedor de Serviço de Criptografia), que implementa a CAPI, para o repositório de chave mestra de coluna. Se você usar um HSM como um repositório de chaves, esse deverá ser o nome do CSP dado pelo seu fornecedor HSM. O provedor deve ser instalado em um computador cliente.  
  
     *KeyIdentifier*  
     Identificador da chave, usado como uma chave mestra de coluna, no repositório de chaves.  
  
     **Exemplos:**  
  
    ```  
    N'My HSM CSP Provider/AlwaysEncryptedKey1'  
    ```  
  
-   **Nome do provedor:** MSSQL_CNG_STORE  
  
     **Formato do caminho da chave:** *ProviderName*/*KeyIdentifier*  
  
     Onde:  
  
     *ProviderName*  
     Nome do KSP (provedor de armazenamento de chaves), que implementa a API Cryptography: Next Generation (CNG) API para o repositório de chaves mestras de coluna. Se você usar um HSM como um repositório de chaves, esse deverá ser o nome do KSP dado pelo seu fornecedor HSM. O provedor precisa ser instalado em um computador cliente.  
  
     *KeyIdentifier*  
     Identificador da chave, usado como uma chave mestra de coluna, no repositório de chaves.  
  
     **Exemplos:**  
  
    ```  
    N'My HSM CNG Provider/AlwaysEncryptedKey1'  
    ```  

-   **Nome do provedor:** AZURE_KEY_STORE  
  
     **Formato do caminho da chave:** *KeyUrl*  
  
     Onde:  
  
     *KeyUrl*  
     A URL da chave no Azure Key Vault


Exemplo:
 
`N'https://myvault.vault.azure.net:443/keys/MyCMK/4c05f1a41b12488f9cba2ea964b6a700'`  
  
## <a name="remarks"></a>Remarks  

É necessário criar uma entrada de metadados de chave mestra de coluna antes de uma entrada de metadados de chave de criptografia de coluna poder ser criada no banco de dados e antes de qualquer coluna no banco de dados poder ser criptografada usando Always Encrypted. Observe que uma entrada de chave mestra de coluna nos metadados não contém a chave mestra de coluna real, que deve ser armazenada em um repositório de chaves de coluna externa (fora do SQL Server). O nome do provedor de repositório de chaves e o caminho da chave mestra de coluna nos metadados devem ser válidos para um aplicativo cliente poder usar a chave mestra de coluna para descriptografar uma chave de criptografia de coluna criptografada com a chave mestra de coluna e consultar colunas criptografadas.


  
## <a name="permissions"></a>Permissões  
 Requer a permissão **ALTER ANY COLUMN MASTER KEY**.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-column-master-key"></a>A. Criando uma chave mestra de coluna  
 Criando uma entrada de metadados de chave mestra de coluna para uma chave mestra de coluna armazenada no repositório de certificados para aplicativos cliente que usam o provedor MSSQL_CERTIFICATE_STORE para acessar a chave mestra de coluna:  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
     KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',   
     KEY_PATH = 'Current User/Personal/f2260f28d909d21c642a3d8e0b45a830e79a1420'  
   );  
```  
  
 Criando uma entrada de metadados de chave mestra de coluna para uma chave mestra de coluna que é acessada por aplicativos cliente que usam o provedor MSSQL_CNG_STORE:  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'MSSQL_CNG_STORE',    
    KEY_PATH = N'My HSM CNG Provider/AlwaysEncryptedKey'  
);  
```  
  
 Criando uma chave mestra de coluna armazenada no Azure Key Vault, para aplicativos cliente que usam o provedor AZURE_KEY_VAULT, para acessar a chave mestra de coluna.  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'AZURE_KEY_VAULT',  
    KEY_PATH = N'https://myvault.vault.azure.net:443/keys/  
        MyCMK/4c05f1a41b12488f9cba2ea964b6a700');  
```  
  
 Criando uma CMK armazenada em um repositório de chave mestra de coluna personalizada:  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = 'CUSTOM_KEY_STORE',    
    KEY_PATH = 'https://contoso.vault/sales_db_tce_key'  
);  
```  
  
## <a name="see-also"></a>Consulte Também
 
* [DROP COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-column-master-key-transact-sql.md)   
* [CREATE COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)
* [sys.column_master_keys (Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
* [Always Encrypted &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
* [Visão geral do gerenciamento de chaves do Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
  
