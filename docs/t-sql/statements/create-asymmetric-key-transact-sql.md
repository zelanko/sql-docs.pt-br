---
title: CREATE ASYMMETRIC KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ASYMMETRIC_KEY_TSQL
- CREATE ASYMMETRIC KEY
- CREATE_ASYMMETRIC_KEY_TSQL
- ASYMMETRIC KEY
dev_langs:
- TSQL
helpviewer_keywords:
- asymmetric keys [SQL Server], creating
- encryption [SQL Server], asymmetric keys
- CREATE ASYMMETRIC KEY statement
- asymmetric keys [SQL Server]
- cryptography [SQL Server], asymmetric keys
ms.assetid: 141bc976-7631-49f6-82bd-a235028645b1
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 009029f16d85fa82867f37e075066701dacfc375
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "73064687"
---
# <a name="create-asymmetric-key-transact-sql"></a>CREATE ASYMMETRIC KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Cria uma chave assimétrica no banco de dados.  
  
 Este recurso é incompatível com a exportação de banco de dados usando a DACFx (estrutura de aplicativo da camada de dados). Você deve remover todas as chaves assimétricas antes de exportar.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
CREATE ASYMMETRIC KEY asym_key_name   
   [ AUTHORIZATION database_principal_name ]  
   [ FROM <asym_key_source> ]  
   [ WITH <key_option> ] 
   [ ENCRYPTION BY <encrypting_mechanism> ] 
   [ ; ]
  
<asym_key_source>::=  
     FILE = 'path_to_strong-name_file'  
   | EXECUTABLE FILE = 'path_to_executable_file'  
   | ASSEMBLY assembly_name  
   | PROVIDER provider_name  
  
<key_option> ::=  
   ALGORITHM = <algorithm>  
      |  
   PROVIDER_KEY_NAME = 'key_name_in_provider'  
      |  
      CREATION_DISPOSITION = { CREATE_NEW | OPEN_EXISTING }  
  
<algorithm> ::=  
      { RSA_4096 | RSA_3072 | RSA_2048 | RSA_1024 | RSA_512 }   
  
<encrypting_mechanism> ::=  
    PASSWORD = 'password'   
```  
  
## <a name="arguments"></a>Argumentos  
 *asym_key_name*  
 É o nome de uma chave assimétrica no banco de dados. Os nomes de chave assimétrica devem estar de acordo com as regras para [identificadores](../../relational-databases/databases/database-identifiers.md) e ser exclusivos no banco de dados.  

 AUTHORIZATION *database_principal_name*  
 Especifica o proprietário da chave assimétrica. O proprietário não pode ser uma função ou um grupo. Se esta opção for omitida, o proprietário será o usuário atual.  
  
 FROM *asym_key_source*  
 Especifica a fonte da qual carregar o par de chaves assimétricas.  
  
 FILE = '*path_to_strong-name_file*'  
 Especifica o caminho de um arquivo com nome forte a partir do qual o par de chaves deve ser carregado. Limitado a 260 caracteres por MAX_PATH da API do Windows.  
  
> [!NOTE]  
>  Essa opção não está disponível em um banco de dados independente.  
  
 EXECUTABLE FILE = '*path_to_executable_file*'  
 Especifica o caminho de um arquivo do assembly do qual a chave pública deve ser carregada. Limitado a 260 caracteres por MAX_PATH da API do Windows.  
  
> [!NOTE]  
>  Essa opção não está disponível em um banco de dados independente.  
  
 ASSEMBLY *assembly_name*  
 Especifica o nome de um assembly assinado que já foi carregado no banco de dados do qual a chave pública deve ser carregada.  
  
 PROVIDER *provider_name*  
 Especifica um nome de um provedor de EKM (gerenciamento extensível de chaves). O provedor deve ser definido primeiro com o uso da instrução CREATE PROVIDER. Para obter mais informações sobre o gerenciamento de chave externa, veja [EKM &#40;Gerenciamento extensível de chaves&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
 ALGORITHM = \<algorithm>  
 Cinco algoritmos podem ser fornecidos: RSA_4096, RSA_3072, RSA_2048, RSA_1024 e RSA_512.  
  
 RSA_1024 e RSA_512 são preteridos. Para usar RSA_1024 ou RSA_512 (não recomendado) você deve definir o nível de compatibilidade do banco de dados para 120 ou inferior.  
  
 PROVIDER_KEY_NAME = '*key_name_in_provider*'  
 Especifica o nome da chave do provedor externo.  
  
 CREATION_DISPOSITION = CREATE_NEW  
 Cria uma chave nova no dispositivo de Gerenciamento Extensível de Chaves. PROVIDER_KEY_NAME deve ser usado para especificar o nome da chave no dispositivo. Se já existir uma chave no dispositivo, a instrução falhará e será apresentado um erro.  
  
 CREATION_DISPOSITION = OPEN_EXISTING  
 Mapeia uma chave assimétrica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para uma chave de Gerenciamento Extensível de Chaves existente. PROVIDER_KEY_NAME deve ser usado para especificar o nome da chave no dispositivo. Se CREATION_DISPOSITION = OPEN_EXISTING não for fornecido, o padrão será CREATE_NEW.  
  
 ENCRYPTION BY PASSWORD = '*password*'  
 Especifica a senha com a qual a chave privada deve ser criptografada. Se essa cláusula não estiver presente, a chave privada será criptografada com a chave mestra do banco de dados. *password* tem um máximo de 128 caracteres. A *password* deve atender aos requisitos da política de senha do Windows do computador que executa a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="remarks"></a>Comentários  
 Uma *chave assimétrica* é uma entidade protegível no nível do banco de dados. Em sua forma padrão, esta entidade contém uma chave pública e uma chave privada. Quando executado sem a cláusula FROM, CREATE ASYMMETRIC KEY gera um par de chaves novo. Quando executado com a cláusula FROM, CREATE ASYMMETRIC KEY importa um par de chaves de um arquivo ou uma chave pública de um assembly ou arquivo DLL.  
  
 Por padrão, a chave privada é protegida pela chave-mestre de banco de dados. Se nenhuma chave-mestre de banco de dados tiver sido criada, será exigida uma senha para proteger a chave privada.  
  
 A chave privada pode ter 512, 1024 ou 2048 bits.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CREATE ASYMMETRIC KEY no banco de dados. Se a cláusula AUTHORIZATION estiver especificada, exigirá a permissão IMPERSONATE na entidade de segurança do banco de dados ou a permissão ALTER na função de aplicativo. Somente logons do Windows, logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e funções de aplicativo podem ter chaves assimétricas. Grupos e funções não podem possuir chaves assimétricas.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-an-asymmetric-key"></a>a. Criando uma chave assimétrica  
 O exemplo a seguir cria uma chave assimétrica denominada `PacificSales09` usando o algoritmo `RSA_2048` e protege a chave privada com uma senha.  
  
```sql  
CREATE ASYMMETRIC KEY PacificSales09   
    WITH ALGORITHM = RSA_2048   
    ENCRYPTION BY PASSWORD = '<enterStrongPasswordHere>';   
GO  
```  
  
### <a name="b-creating-an-asymmetric-key-from-a-file-giving-authorization-to-a-user"></a>B. Criando uma chave assimétrica de um arquivo, dando autorização a um usuário  
 O exemplo seguinte cria a chave assimétrica `PacificSales19` com base em um par de chaves armazenado em um arquivo e atribui propriedade da chave assimétrica ao usuário `Christina`. A chave privada é protegida pela chave mestra do banco de dados, que precisa ser criada antes da criação da chave assimétrica.  
  
```sql  
CREATE ASYMMETRIC KEY PacificSales19  
    AUTHORIZATION Christina  
    FROM FILE = 'c:\PacSales\Managers\ChristinaCerts.tmp';  
GO  
```  
  
### <a name="c-creating-an-asymmetric-key-from-an-ekm-provider"></a>C. Criando uma chave assimétrica de um provedor de EKM  
 O exemplo a seguir cria a chave assimétrica `EKM_askey1` de um par de chaves armazenado em um provedor de Gerenciamento Extensível de Chaves chamado `EKM_Provider1` e uma chave nesse provedor chamada `key10_user1`.  
  
```sql  
CREATE ASYMMETRIC KEY EKM_askey1   
    FROM PROVIDER EKM_Provider1  
    WITH   
        ALGORITHM = RSA_2048,   
        CREATION_DISPOSITION = CREATE_NEW  
        , PROVIDER_KEY_NAME  = 'key10_user1' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)  
 [DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)  
 [ASYMKEYPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/asymkeyproperty-transact-sql.md)  
 [ASYMKEY_ID &#40;Transact-SQL&#41;](../../t-sql/functions/asymkey-id-transact-sql.md)  
 [Escolher um algoritmo de criptografia](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
 [Gerenciamento extensível de chaves usando o Cofre de Chaves do Azure &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
  
