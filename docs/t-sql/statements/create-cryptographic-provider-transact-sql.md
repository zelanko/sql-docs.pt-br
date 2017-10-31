---
title: "CRIAR um provedor CRIPTOGRÁFICO (Transact-SQL) | Microsoft Docs"
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
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9a7252786522ef4e0b4206db06d7dc8aa76cf308
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="create-cryptographic-provider-transact-sql"></a>CREATE CRYPTOGRAPHIC PROVIDER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria um provedor criptográfico no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a partir de um provedor EKM (Gerenciamento Extensível de Chaves).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CREATE CRYPTOGRAPHIC PROVIDER provider_name   
    FROM FILE = path_of_DLL  
```  
  
## <a name="arguments"></a>Argumentos  
 *provider_name*  
 É o nome do provedor de Gerenciamento Extensível de Chaves.  
  
 *path_of_DLL*  
 É o caminho do arquivo .dll que implementa o Gerenciamento Extensível de Chaves do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ao usar o **SQL Server Connector para Cofre de chaves do Microsoft Azure** o local padrão é **' C:\Program Files\Microsoft SQL Server Connector para Microsoft Azure chave Vault\Microsoft.AzureKeyVaultService.EKM.dll '**.  
  
## <a name="remarks"></a>Comentários  
 Todas as chaves criadas por um provedor farão referência ao provedor por meio de seu GUID. O GUID é retido em todas as versões da DLL.  
  
 A DLL que implementa a interface SQLEKM deve ser assinada digitalmente usando qualquer certificado. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verificará a assinatura. Isso inclui sua cadeia de certificado, que deve ter sua raiz instalada no **autoridades de certificação raiz confiáveis** local em um sistema Windows. Se a assinatura não for verificada corretamente, a instrução CREATE CRYPTOGRAPHIC PROVIDER falhará. Para obter mais informações sobre certificados e cadeias de certificados, consulte [SQL Server certificados e chaves assimétricas](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  
  
 Quando uma dll de provedor EKM não implementar todos os métodos necessários, CREATE CRYPTOGRAPHIC PROVIDER poderá retornar o erro 33085:  
  
 `One or more methods cannot be found in cryptographic provider library '%.*ls'.`  
  
 Quando o arquivo de cabeçalho usado para criar a dll de provedor EKM estiver desatualizado, CREATE CRYPTOGRAPHIC PROVIDER poderá retornar o erro 33032:  
  
 `SQL Crypto API version '%02d.%02d' implemented by provider is not supported. Supported version is '%02d.%02d'.`  
  
## <a name="permissions"></a>Permissões  
 Requer permissão CONTROL SERVER ou associação no **sysadmin** função de servidor fixa.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria um provedor criptográfico chamado `SecurityProvider` na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um arquivo. dll. O arquivo. dll é nomeado `c:\SecurityProvider\SecurityProvider_v1.dll` e é instalado no servidor. O certificado do provedor deve ser instalado primeiro no servidor.  
  
```  
-- Install the provider  
CREATE CRYPTOGRAPHIC PROVIDER SecurityProvider  
    FROM FILE = 'C:\SecurityProvider\SecurityProvider_v1.dll';  
```  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciamento Extensível de Chaves &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [ALTER CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-cryptographic-provider-transact-sql.md)   
 [DROP CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-cryptographic-provider-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [Gerenciamento extensível de chaves usando o Cofre de Chaves do Azure &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
  

