---
description: CREATE CRYPTOGRAPHIC PROVIDER (Transact-SQL)
title: CREATE CRYPTOGRAPHIC PROVIDER (Transact-SQL) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE_CRYPTOGRAPHIC_TSQL
- CRYPTOGRAPHIC PROVIDER
- PROVIDER_TSQL
- CREATE CRYPTOGRAPHIC
- CREATE CRYPTOGRAPHIC PROVIDER
- CRYPTOGRAPHIC_PROVIDER_TSQL
- CREATE_CRYPTOGRAPHIC_PROVIDER_TSQL
- PROVIDER
dev_langs:
- TSQL
helpviewer_keywords:
- 33085 (Database Engine error)
- CREATE CRYPTOGRAPHIC PROVIDER statement
- 33032 (Database Engine error)
ms.assetid: 059a39a6-9d32-4d3f-965b-0a1ce75229c7
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: b1a12f2c53409148854b806f1141bf46acad8a4e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88467242"
---
# <a name="create-cryptographic-provider-transact-sql"></a>CREATE CRYPTOGRAPHIC PROVIDER (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Cria um provedor criptográfico no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a partir de um provedor EKM (Gerenciamento Extensível de Chaves).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CREATE CRYPTOGRAPHIC PROVIDER provider_name   
    FROM FILE = path_of_DLL  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *provider_name*  
 É o nome do provedor de Gerenciamento Extensível de Chaves.  
  
 *path_of_DLL*  
 É o caminho do arquivo .dll que implementa o Gerenciamento Extensível de Chaves do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ao usar o **Conector do SQL Server para Microsoft Azure Key Vault**, a localização padrão é **'C:\Program Files\Microsoft SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll'**.  
  
## <a name="remarks"></a>Comentários  
 Todas as chaves criadas por um provedor farão referência ao provedor por meio de seu GUID. O GUID é retido em todas as versões da DLL.  
  
 A DLL que implementa a interface SQLEKM deve ser assinada digitalmente usando qualquer certificado. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verificará a assinatura. Isso inclui sua cadeia de certificados, que deve ter sua raiz instalada no local **Autoridades de Certificação Raiz Confiáveis** em um sistema Windows. Se a assinatura não for verificada corretamente, a instrução CREATE CRYPTOGRAPHIC PROVIDER falhará. Para obter mais informações sobre certificados e cadeias de certificados, consulte [Certificados e chaves assimétricas do SQL Server](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  
  
 Quando uma dll de provedor EKM não implementar todos os métodos necessários, CREATE CRYPTOGRAPHIC PROVIDER poderá retornar o erro 33085:  
  
 `One or more methods cannot be found in cryptographic provider library '%.*ls'.`  
  
 Quando o arquivo de cabeçalho usado para criar a dll de provedor EKM estiver desatualizado, CREATE CRYPTOGRAPHIC PROVIDER poderá retornar o erro 33032:  
  
 `SQL Crypto API version '%02d.%02d' implemented by provider is not supported. Supported version is '%02d.%02d'.`  
  
## <a name="permissions"></a>Permissões  
 Exige a permissão CONTROL SERVER ou a associação à função de servidor fixa **sysadmin**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria um provedor criptográfico chamado `SecurityProvider` no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com base em um arquivo .dll. O arquivo .dll é nomeado `c:\SecurityProvider\SecurityProvider_v1.dll` e instalado no servidor. O certificado do provedor deve ser instalado primeiro no servidor.  
  
```  
-- Install the provider  
CREATE CRYPTOGRAPHIC PROVIDER SecurityProvider  
    FROM FILE = 'C:\SecurityProvider\SecurityProvider_v1.dll';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciamento Extensível de Chaves &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [ALTER CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-cryptographic-provider-transact-sql.md)   
 [DROP CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-cryptographic-provider-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [Gerenciamento extensível de chaves usando o Cofre de Chaves do Azure &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
  
