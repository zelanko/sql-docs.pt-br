---
title: ALTER CRYPTOGRAPHIC PROVIDER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/20/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 20
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 6d97094cb11eff7586883bc71c94220dbec05041
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37974907"
---
# <a name="alter-cryptographic-provider-transact-sql"></a>ALTER CRYPTOGRAPHIC PROVIDER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera um provedor criptográfico no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a partir de um provedor EKM (Gerenciamento Extensível de Chaves).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
ALTER CRYPTOGRAPHIC PROVIDER provider_name   
    [ FROM FILE = path_of_DLL ]  
    ENABLE | DISABLE  
```  
  
## <a name="arguments"></a>Argumentos  
 *provider_name*  
 Nome do provedor de Gerenciamento de Chaves Extensível.  
  
 *Path_of_DLL*  
 Caminho do arquivo .dll que implementa a interface de Gerenciamento Extensível de Chaves do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ENABLE | DISABLE  
 Habilita ou desabilita um provedor.  
  
## <a name="remarks"></a>Remarks  
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
```  
ALTER CRYPTOGRAPHIC PROVIDER SecurityProvider   
DISABLE;  
GO  
```  

2. Faça upgrade do arquivo. dll do provedor. O GUID deve ser o mesmo que a versão anterior, mas a versão pode ser diferente.  
```  
ALTER CRYPTOGRAPHIC PROVIDER SecurityProvider  
FROM FILE = 'c:\SecurityProvider\SecurityProvider_v2.dll';  
GO  
```  

3. Habilite o provedor atualizado.   
```  
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
  
  
