---
title: sp_setnetname (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_setnetname
- sp_setnetname_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_setnetname
ms.assetid: f416ba81-3835-4588-b0a3-2fe75589490e
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7e9f439854cc1d3af3ca5db09981f2eba2af7a4f
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="spsetnetname-transact-sql"></a>sp_setnetname (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Define os nomes de rede no **sys** para seus nomes de computador de rede reais para instâncias remotas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Este procedimento pode ser usado para habilitar a execução de chamadas de procedimento armazenado remoto para computadores com nomes de rede contendo identificadores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não são válidos.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_setnetname  
@server = 'server',   
     @netname = 'network_name'  
```  
  
## <a name="arguments"></a>Argumentos  
 **@server= '** *servidor* **'**  
 É o nome do servidor remoto conforme referenciado em sintaxe de chamada de procedimento armazenado remoto codificado pelo usuário. Exatamente uma linha em **sys** já deve existir para usar esse *server*. *server* é **sysname**, sem padrão.  
  
 **@netname='** *network_name* **'**  
 É o nome de rede do computador ao qual as chamadas de procedimento armazenado remoto são feitas. *network_name* é **sysname**, sem padrão.  
  
 Esse nome deve corresponder ao nome do computador de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, e o nome pode incluir caracteres que não são permitidos em identificadores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="remarks"></a>Comentários  
 Algumas chamadas de procedimento armazenado remoto a computadores com Windows podem encontrar problemas se o nome do computador tiver identificadores que não são válidos.  
  
 Como servidores vinculados e servidores remotos residem no mesmo namespace, eles não podem ter o mesmo nome. No entanto, você pode definir um servidor vinculado e um servidor remoto em um servidor especificado, atribuindo nomes diferentes e usando **sp_setnetname** para definir o nome de rede de um deles como o nome de rede do servidor subjacente.  
  
```  
--Assume sqlserv2 is actual name of SQL Server   
--database server  
EXEC sp_addlinkedserver 'sqlserv2';  
GO  
EXEC sp_addserver 'rpcserv2';  
GO  
EXEC sp_setnetname 'rpcserv2', 'sqlserv2';  
```  
  
> [!NOTE]  
>  Usando **sp_setnetname** apontar um servidor vinculado para o servidor local não tem suporte. Os servidores referenciados dessa maneira não podem participar de uma transação distribuída.  
  
## <a name="permissions"></a>Permissões  
 Requer a participação no **sysadmin** e **setupadmin** funções de servidor fixas.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra uma sequência administrativa típica usada no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para emitir a chamada de procedimento armazenado remoto.  
  
```  
USE master;  
GO  
EXEC sp_addserver 'Win_1';  
EXEC sp_setnetname 'Win_1','Win-1';  
EXEC Win_1.master.dbo.sp_who;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Mecanismo de banco de dados armazenados procedimentos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_addserver &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
