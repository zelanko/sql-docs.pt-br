---
title: SETUSER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SETUSER_TSQL
- SETUSER
dev_langs:
- TSQL
helpviewer_keywords:
- delegation [SQL Server]
- impersonation [SQL Server]
- SETUSER statement
- user impersonation [SQL Server]
ms.assetid: 7acfac5c-9ad6-4226-b874-7add36c4ea43
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: a592e2a335e8ce04341dba4a7bbc160f84b4b68a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="setuser-transact-sql"></a>SETUSER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Permite que um membro da função de servidor fixa **sysadmin** ou o proprietário do banco de dados represente outro usuário.  
  
> [!IMPORTANT]  
>  SETUSER é incluído somente para compatibilidade com versões anteriores. SETUSER pode não ter suporte em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Recomendamos o uso de [EXECUTE AS](../../t-sql/statements/execute-as-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SETUSER [ 'username' [ WITH NORESET ] ]   
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *username* **'**  
 É o nome de um usuário do Windows ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no banco de dados atual que é representado. Quando *username* não é especificado, a identidade original do administrador do sistema ou do proprietário do banco de dados que representa o usuário é redefinida.  
  
 WITH NORESET  
 Especifica que as instruções SETUSER seguintes (sem nenhum *username* especificado) não devem redefinir a identidade do usuário como administrador do sistema ou proprietário do banco de dados.  
  
## <a name="remarks"></a>Remarks  
 SETUSER pode ser usado por um membro da função de servidor fixa **sysadmin** ou o proprietário de um banco de dados para adotar a identidade de outro usuário e testar suas permissões. A associação à função de banco de dados fixa db_owner não é suficiente.  
  
 Use SETUSER somente com usuários do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. SETUSER não tem suporte com usuários de Windows. Quando SETUSER é usado para assumir a identidade de outro usuário, todo objeto que o usuário da representação cria é de propriedade do usuário representado. Por exemplo, se o proprietário do banco de dados assumir a identidade do usuário **Marina** e criar uma tabela chamada **orders**, a tabela **orders** será de propriedade de **Marina**, e não do administrador do sistema.  
  
 SETUSER permanece em vigor até que outra instrução SETUSER seja emitida ou até que o banco de dados atual seja alterado com a instrução USE.  
  
> [!NOTE]  
>  Se SETUSER WITH NORESET for usado, o proprietário do banco de dados ou administrador do sistema deverá fazer logoff e logon novamente para restabelecer seus próprios direitos.  
  
## <a name="permissions"></a>Permissões  
 Exige associação à função de servidor fixa **sysadmin** ou deve ser o proprietário do banco de dados. A associação à função de banco de dados fixa **db_owner** não é suficiente  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra como o proprietário do banco de dados pode adotar a identidade de outro usuário. O usuário `mary` criou uma tabela chamada `computer_types`. Usando SETUSER, o proprietário do banco de dados representa `mary` para conceder ao usuário `joe` acesso à tabela `computer_types` e, em seguida, redefine sua própria identidade.  
  
```  
SETUSER 'mary';  
GO  
GRANT SELECT ON computer_types TO joe;  
GO  
--To revert to the original user  
SETUSER;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [USE &#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md)  
  
  
