---
title: sp_addextendedproc (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_addextendedproc_TSQL
- sp_addextendedproc
dev_langs: TSQL
helpviewer_keywords: sp_addextendedproc
ms.assetid: c0d4b47b-a855-451e-90e5-5fb2d836ebfa
caps.latest.revision: "33"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bf0fa69b0704ba7ad3a4f433415298e3706d98bf
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spaddextendedproc-transact-sql"></a>sp_addextendedproc (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Registra o nome de um novo procedimento armazenado estendido à [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Em vez disso, use a [Integração CLR](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) .  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addextendedproc [ @functname = ] 'procedure' ,   
     [ @dllname = ] 'dll'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@functname =** ] **'***procedimento***'**  
 É o nome da função a ser chamada dentro da DLL (biblioteca de vínculo dinâmico). *procedimento* é **nvarchar (517)**, sem padrão. *procedimento* opcionalmente pode incluir o nome do proprietário na forma *owner.function*.  
  
 [  **@dllname =** ] **'***dll***'**  
 É o nome da DLL que contém a função. *dll* é **varchar (255)**, sem padrão. É recomendável especificar o caminho completo da DLL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="remarks"></a>Comentários  
 Depois que um procedimento armazenado estendido é criado, ele deve ser adicionado ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando **sp_addextendedproc**. Para obter mais informações, consulte [adicionando um procedimento armazenado estendido para o SQL Server](../../relational-databases/extended-stored-procedures-programming/adding-an-extended-stored-procedure-to-sql-server.md).  
  
 Esse procedimento pode ser executado somente no **mestre** banco de dados. Para executar um procedimento armazenado estendido de um banco de dados diferente de **mestre**, qualifique o nome do procedimento armazenado estendido com **mestre**.  
  
 **sp_addextendedproc** adiciona entradas para o [sys. Objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) exibição de catálogo, registrar o nome do novo procedimento armazenado estendido com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ele também adiciona uma entrada de [extended_procedures](../../relational-databases/system-catalog-views/sys-extended-procedures-transact-sql.md) exibição do catálogo.  
  
> [!IMPORTANT]  
>  DLLs existentes que não são registradas com um caminho completo não funcionarão depois da atualização do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para corrigir o problema, use **sp_dropextendedproc** para cancelar o registro de DLL e, em seguida, registrá-la novamente com **sp_addextendedproc**, especificando o caminho completo.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** pode executar a função de servidor fixa **sp_addextendedproc**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir adiciona o **xp_hello** o procedimento armazenado estendido.  
  
```  
USE master;  
GO  
EXEC sp_addextendedproc xp_hello, 'c:\xp_hello.dll';  
```  
  
## <a name="see-also"></a>Consulte também  
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [sp_dropextendedproc &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)   
 [sp_helpextendedproc &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
