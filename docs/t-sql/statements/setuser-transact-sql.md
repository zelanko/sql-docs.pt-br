---
title: SETUSER (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ab9805dda5f5b2b4199cb40ef3c28af1d5b4379f
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="setuser-transact-sql"></a>SETUSER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Permite que um membro do **sysadmin** fixo de função de servidor ou o proprietário do banco de dados para representar outro usuário.  
  
> [!IMPORTANT]  
>  SETUSER é incluído somente para compatibilidade com versões anteriores. SETUSER pode não ter suporte em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Recomendamos que você use [EXECUTE AS](../../t-sql/statements/execute-as-transact-sql.md) em vez disso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SETUSER [ 'username' [ WITH NORESET ] ]   
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *username* **'**  
 É o nome de um usuário do Windows ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no banco de dados atual que é representado. Quando *nome de usuário* não for especificado, a identidade original do administrador do sistema ou proprietário de banco de dados representando o usuário será redefinida.  
  
 WITH NORESET  
 Especifica que subsequentes instruções SETUSER (sem especificado *username*) não deve ser redefinida a identidade do usuário para o administrador do sistema ou proprietário do banco de dados.  
  
## <a name="remarks"></a>Comentários  
 SETUSER pode ser usado por um membro de **sysadmin** fixo de função de servidor ou o proprietário do banco de dados para adotar a identidade de outro usuário para testar as permissões do outro usuário. Associação na função de banco de dados fixa do db_owner não é suficiente.  
  
 Use SETUSER somente com usuários do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. SETUSER não tem suporte com usuários de Windows. Quando SETUSER é usado para assumir a identidade de outro usuário, todo objeto que o usuário da representação cria é de propriedade do usuário representado. Por exemplo, se o proprietário do banco de dados assume a identidade de usuário **Margaret** e cria uma tabela chamada **pedidos**, o **pedidos** tabela é de propriedade **Margaret** , não o administrador do sistema.  
  
 SETUSER permanece em vigor até que outra instrução SETUSER seja emitida ou até que o banco de dados atual seja alterado com a instrução USE.  
  
> [!NOTE]  
>  Se SETUSER WITH NORESET for usado, o proprietário do banco de dados ou administrador do sistema deverá fazer logoff e logon novamente para restabelecer seus próprios direitos.  
  
## <a name="permissions"></a>Permissões  
 Requer a participação no **sysadmin** função de servidor fixa ou deve ser o proprietário do banco de dados. Associação de **db_owner** função fixa de banco de dados não é suficiente  
  
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
  
## <a name="see-also"></a>Consulte também  
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [USE &#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md)  
  
  

