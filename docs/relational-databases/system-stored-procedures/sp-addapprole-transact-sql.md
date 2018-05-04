---
title: sp_addapprole (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_addapprole_TSQL
- sp_addapprole
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addapprole
ms.assetid: 24200295-9a54-4cab-9922-fb2e88632721
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 44958d1c576cee4346a28b9e0b3dcdf04386d646
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="spaddapprole-transact-sql"></a>sp_addapprole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Adiciona uma função de aplicativo ao banco de dados atual.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [CREATE APPLICATION ROLE](../../t-sql/statements/create-application-role-transact-sql.md) em vez disso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addapprole [ @rolename = ] 'role' , [ @password = ] 'password'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@rolename =** ] **'***função***'**  
 É o nome da nova função de aplicativo. *Função* é **sysname**, sem padrão. *função* deve ser um identificador válido e não pode existir no banco de dados atual.  
  
 Os nomes de função de aplicativo podem conter de 1 até 128 caracteres, inclusive cartas, símbolos e números. Os nomes de função não podem conter uma barra invertida (\\) nem ser nulo ou uma cadeia de caracteres vazia (").  
  
 [  **@password =** ] **'***senha***'**  
 É a senha necessária para ativar a função de aplicativo. *senha* é **sysname**, sem padrão. *senha* não pode ser NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Remarks  
 Em versões anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], os usuários (e as funções) não são completamente distintos de esquemas. Começando com [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], os esquemas são completamente distintos de funções. Esta nova arquitetura é refletida no comportamento de CREATE APPLICATION ROLE. Esta instrução substitui **sp_addapprole**.  
  
 Para manter a compatibilidade com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], **sp_addapprole** fará o seguinte:  
  
-   Se um esquema de nome igual ao da função de aplicativo ainda não existir, tal esquema será criado. O novo esquema será de propriedade da função de aplicativo e será o esquema padrão da função de aplicativo.  
  
-   Se um esquema de nome igual ao da função de aplicativo já existir, o procedimento falhará.  
  
-   Complexidade de senha não é verificada por **sp_addapprole**. Mas a complexidade da senha é verificada por CREATE APPLICATION ROLE.  
  
 O parâmetro *senha* é armazenado como um hash unidirecional.  
  
 O **sp_addapprole** procedimento armazenado não pode ser executado de dentro de uma transação definida pelo usuário.  
  
> [!IMPORTANT]  
>  O Microsoft ODBC **criptografar** opção não é suportada por **SqlClient**. Quando possível, solicite que os usuários insiram as credenciais de função de aplicativo no momento da execução. Evite armazenar as credenciais em um arquivo. Se precisar manter as credenciais, criptografe-as usando as funções CryptoAPI.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER ANY APPLICATION ROLE no banco de dados. Se um esquema com nome e proprietário iguais aos da nova função ainda não existir, isso também exigirá a permissão CREATE SCHEMA no banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir adiciona a nova função de aplicativo `SalesApp` com a senha `x97898jLJfcooFUYLKm387gf3` no banco de dados atual.  
  
```  
EXEC sp_addapprole 'SalesApp', 'x97898jLJfcooFUYLKm387gf3' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)  
  
  
