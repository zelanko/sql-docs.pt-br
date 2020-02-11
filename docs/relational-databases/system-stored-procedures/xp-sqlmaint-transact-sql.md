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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68091915"
---
# <a name="xp_sqlmaint-transact-sql"></a>xp_sqlmaint (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Chama o utilitário **sqlmaint** com uma cadeia de caracteres que contém os comutadores **sqlmaint**. O utilitário **sqlmaint** executa um conjunto de operações de manutenção em um ou mais bancos de dados.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
xp_sqlmaint 'switch_string'     
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *switch_string* **'**  
 É uma cadeia de caracteres que contém as opções do utilitário **sqlmaint** . As opções e seus valores devem ser separados por um espaço.  
  
 O **-?** a opção não é válida para **xp_sqlmaint**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhum. Retornará um erro se o utilitário **sqlmaint** falhar.  
  
## <a name="remarks"></a>Comentários  
 Se esse procedimento for chamado por um usuário conectado com SQL Server autenticação, as opções **-U "***login_id***"** e **-P "***senha***"** serão precedidas para *switch_string* antes da execução. Se o usuário estiver conectado com a autenticação do Windows, *switch_string* será passado sem alterar para **sqlmaint**.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Utilitário sqlmaint](../../tools/sqlmaint-utility.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
