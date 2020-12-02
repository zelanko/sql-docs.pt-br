---
description: ALTER CRYPTOGRAPHIC PROVIDER (Transact-SQL)
title: ALTER CRYPTOGRAPHIC PROVIDER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/20/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_CRYPTOGRAPHIC_PROVIDER_TSQL
- ALTER CRYPTOGRAPHIC PROVIDER
- ALTER_CRYPTOGRAPHIC_TSQL
- ALTER CRYPTOGRAPHIC
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER CRYPTOGRAPHIC PROVIDER
ms.assetid: 876b6348-fb29-49e1-befc-4217979f6416
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 95c7f778abe9417a108e4df6982b73d3037f5ae9
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96124285"
---
# <a name="alter-cryptographic-provider-transact-sql"></a>ALTER CRYPTOGRAPHIC PROVIDER (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Altera um provedor criptográfico no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a partir de um provedor EKM (Gerenciamento Extensível de Chaves).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql  
ALTER CRYPTOGRAPHIC PROVIDER provider_name   
    [ FROM FILE = path_of_DLL ]  
    ENABLE | DISABLE  
```  
  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *provider_name*  
 Nome do provedor de Gerenciamento de Chaves Extensível.  
  
 *Path_of_DLL*  
 Caminho do arquivo .dll que implementa a interface de Gerenciamento Extensível de Chaves do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ENABLE | DISABLE  
 Habilita ou desabilita um provedor.  
  
## <a name="remarks"></a>Comentários  
 Se o provedor alterar o arquivo .dll usado para implementar o Gerenciamento de Chaves Extensível [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], será necessário usar a instrução ALTER CRYPTOGRAPHIC PROVIDER.  
  
 Quando o caminho do arquivo .dll é atualizado usando a instrução ALTER CRYPTOGRAPHIC PROVIDER, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa as seguintes ações:  
-   Desabilita o provedor.  
-   Verifica a assinatura DLL e assegura que o arquivo .dll tenha o mesmo GUID que foi registrado no catálogo.  
-   Atualiza a versão DLL no catálogo.  
  

Quando um provedor EKM estiver definido como DISABLE, quaisquer tentativas de usar o provedor com instruções de criptografia em novas conexões falharão.  
  
Para desabilitar um provedor, todas as sessões que o usam devem ser terminadas.  
  
Quando uma dll de provedor EKM não implementar todos os métodos necessários, ALTER CRYPTOGRAPHIC PROVIDER poderá retornar o erro 33085:  
  
 `One or more methods cannot be found in cryptographic provider library '%.*ls'.`  
  
Quando o arquivo de cabeçalho usado para criar a dll de provedor EKM provedor estiver desatualizado, ALTER CRYPTOGRAPHIC PROVIDER poderá retornar o erro 33032:  
  
 `SQL Crypto API version '%02d.%02d' implemented by provider is not supported. Supported version is '%02d.%02d'.`  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL no provedor criptográfico.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir altera um provedor criptográfico, chamado `SecurityProvider` no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], para uma versão mais nova de um arquivo .dll. Essa nova versão é chamada `c:\SecurityProvider\SecurityProvider_v2.dll` e é instalada no servidor. O certificado do provedor deve ser instalado no servidor.  
  
1. Desabilite o provedor para executar o upgrade. Isso encerrará todas as sessões de criptografia abertas.  
```sql  
ALTER CRYPTOGRAPHIC PROVIDER SecurityProvider   
DISABLE;  
GO  
```  

2. Faça upgrade do arquivo. dll do provedor. O GUID deve ser o mesmo que a versão anterior, mas a versão pode ser diferente.  
```sql  
ALTER CRYPTOGRAPHIC PROVIDER SecurityProvider  
FROM FILE = 'c:\SecurityProvider\SecurityProvider_v2.dll';  
GO  
```  

3. Habilite o provedor atualizado.   
```sql  
ALTER CRYPTOGRAPHIC PROVIDER SecurityProvider   
ENABLE;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciamento Extensível de Chaves &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/create-cryptographic-provider-transact-sql.md)   
 [DROP CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-cryptographic-provider-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [Gerenciamento extensível de chaves usando o Cofre de Chaves do Azure &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
  
