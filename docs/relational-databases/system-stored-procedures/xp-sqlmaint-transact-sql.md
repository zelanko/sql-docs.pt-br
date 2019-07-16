---
title: xp_sqlmaint (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_sqlmaint
- xp_sqlmaint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_sqlmaint
ms.assetid: bda66e1b-6bbd-49be-b86e-37efc920e912
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9948767ca0eca5721207079f978987142653e9c2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091915"
---
# <a name="xpsqlmaint-transact-sql"></a>xp_sqlmaint (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Chamadas a **sqlmaint** utility com uma cadeia de caracteres que contém **sqlmaint**comutadores. O **sqlmaint** utilitário executa um conjunto de operações de manutenção em um ou mais bancos de dados.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
xp_sqlmaint 'switch_string'     
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *switch_string* **'**  
 É uma cadeia de caracteres que contém o **sqlmaint** opções do utilitário. As opções e seus valores devem ser separados por um espaço.  
  
 O **-?** switch não é válido para **xp_sqlmaint**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 nenhuma. Retorna um erro se o **sqlmaint** utilitário falhar.  
  
## <a name="remarks"></a>Comentários  
 Se esse procedimento for chamado por um usuário feito logon com a autenticação do SQL Server, o **- U "***login_id***"** e **-P "***senha***"** switches são pré-anexados *switch_string* antes da execução. Se o usuário fizer logon com a autenticação do Windows, *switch_string* é passado sem alteração **sqlmaint**.  
  
## <a name="permissions"></a>Permissões  
 Exige associação à função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 No exemplo a seguir, `xp_sqlmaint` chama `sqlmaint` para executar verificações de integridade, criar um arquivo de relatório e atualizar `msdb.dbo.sysdbmaintplan_history`.  
  
```  
EXEC xp_sqlmaint '-D AdventureWorks2012 -PlanID 02A52657-D546-11D1-9D8A-00A0C9054212   
   -Rpt "C:\Program Files\Microsoft SQL Server\MSSQL\LOG\DBMaintPlan2.txt" -WriteHistory  -CkDB -CkAl';   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
The command(s) executed successfully.  
```  
  
## <a name="see-also"></a>Consulte também  
 [Utilitário Sqlmaint](../../tools/sqlmaint-utility.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
