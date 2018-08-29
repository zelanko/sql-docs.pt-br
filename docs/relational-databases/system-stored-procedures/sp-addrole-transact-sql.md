---
title: sp_addrole (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_addrole
- sp_addrole_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addrole
ms.assetid: e8a21642-8440-419a-8585-93d3d9d44f00
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: cde14d46a81f26d7d41cc83bdca15b668622c8bf
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43038819"
---
# <a name="spaddrole-transact-sql"></a>sp_addrole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria uma nova função de banco de dados no banco de dados atual.  
  
> [!IMPORTANT]  
>  **sp_addrole** é incluído para compatibilidade com versões anteriores do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e podem não ter suporte em uma versão futura. Use [CREATE ROLE](../../t-sql/statements/create-role-transact-sql.md) em vez disso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addrole [ @rolename = ] 'role' [ , [ @ownername = ] 'owner' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@rolename =** ] **'***função***'**  
 É o nome da nova função de banco de dados. *função* é um **sysname**, sem padrão. *função* deve ser um identificador válido (ID) e ainda não deve existir no banco de dados atual.  
  
 [  **@ownername =**] **'***proprietário***'**  
 É o proprietário da nova função de banco de dados. *proprietário* é um **sysname**, com um padrão de usuário de execução atual. *proprietário* deve ser um usuário de banco de dados ou função de banco de dados no banco de dados atual.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Remarks  
 Os nomes de funções de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem ter de 1 a 128 caracteres, incluindo letras, símbolos e números. Os nomes de funções de banco de dados não podem: conter um caractere de barra invertida (\\), ser NULL, ou uma cadeia de caracteres vazia (**'**).  
  
 Depois de adicionar uma função de banco de dados, use [sp_addrolemember &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) para adicionar entidades à função. Quando as instruções GRANT, DENY ou REVOKE são usadas para aplicar permissões na função de banco de dados, os membros da função de banco de dados herdam essas permissões como se elas fossem aplicadas diretamente em suas contas.  
  
> [!NOTE]  
>  Novas funções de servidor não podem ser criadas. As funções podem ser criadas somente no nível do banco de dados.  
  
 **sp_addrole** não pode ser usado dentro de uma transação definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CREATE ROLE no banco de dados. Se estiver criando um esquema, requer CREATE SCHEMA no banco de dados. Se *proprietário* é especificado como um usuário ou grupo, requer IMPERSONATE nesse usuário ou grupo. Se *proprietário* é especificado como uma função, requer a permissão ALTER nessa função ou um membro dessa função. Se o proprietário for especificado como uma função de aplicativo, requer a permissão ALTER nessa função de aplicativo.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir adiciona uma nova função chamada `Managers` ao banco de dados atual.  
  
```  
EXEC sp_addrole 'Managers';  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos de segurança armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)  
  
  
