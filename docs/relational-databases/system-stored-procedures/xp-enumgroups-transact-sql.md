---
title: xp_enumgroups (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_enumgroups_TSQL
- xp_enumgroups
dev_langs:
- TSQL
helpviewer_keywords:
- xp_enumgroups
ms.assetid: 0bd3ed36-e260-469c-a5ff-b033fb9ea59d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0e228f2a2363cab777c2b7ae44185e3c215e8f93
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85633693"
---
# <a name="xp_enumgroups-transact-sql"></a>xp_enumgroups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Fornece uma lista de grupos Microsoft Windows locais ou uma lista de grupos globais que estão definidos em um domínio do Windows especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
xp_enumgroups [ 'domain_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *domain_name* **'**  
 É o nome do domínio do Windows para o qual será enumerada uma lista de grupos globais. *domain_name* é **sysname**, com um padrão de NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**grupo**|**sysname**|Nome do grupo do Windows|  
|**mente**|**sysname**|Descrição do grupo do Windows fornecida pelo Windows|  
  
## <a name="remarks"></a>Comentários  
 Se *domain_name* for o nome do computador baseado no Windows em que uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executada ou nenhum nome de domínio for especificado, **xp_enumgroups** enumerará os grupos locais do computador que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **xp_enumgroups** não pode ser usado quando uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução no Windows 98.  
  
## <a name="permissions"></a>Permissões  
 Requer a associação na função de banco de dados fixa **db_owner** no banco de dados **mestre** ou a associação à função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir lista os grupos do domínio `sales`.  
  
```  
EXEC xp_enumgroups 'sales';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_grantlogin](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_revokelogin](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados estendidos gerais &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de xp_loginconfig](../../relational-databases/system-stored-procedures/xp-loginconfig-transact-sql.md)   
 [&#41;&#40;Transact-SQL de xp_logininfo](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  
