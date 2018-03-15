---
title: DBCC dllname (FREE) (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbcc_dllname_(FREE)_TSQL
- dllname
- dbcc dllname (FREE)
- FREE
- dbcc_dllname(FREE)_TSQL
- FREE_TSQL
- dllname_TSQL
- dbcc dllname(FREE)
dev_langs:
- TSQL
helpviewer_keywords:
- DLL unloading [SQL Server]
- DBCC dllname (FREE)
- freeing DLLs
- unloading DLLs
ms.assetid: 1eb71c17-fe15-430b-8916-e4e312dcf9c0
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0ad6b900d45ef1c87c0aca0d961685c68a72a33d
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-dllname-free-transact-sql"></a>DBCC dllname (FREE) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] Descarrega da memória a DLL de procedimento armazenado estendido especificada.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
```sql
DBCC <dllname> ( FREE ) [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumentos  
 \<*dllname*>  
 É o nome do DLL para libertar da memória.  
  
 WITH NO_INFOMSGS  
 Suprime todas as mensagens informativas.  
  
## <a name="remarks"></a>Remarks
Quando um procedimento armazenado estendido é executado, o DLL permanece carregado pela instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] até que o servidor seja desativado. Esta instrução permite a um DLL ser descarregado da memória sem desativar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para exibir os arquivos DLL carregados no momento pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], execute **sp_helpextendedproc**
  
## <a name="result-sets"></a>Conjuntos de resultados  
Quando uma DLL válida é especificada, o DBCC *nomedadll* (FREE) retorna:
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissões  
Exige associação à função de servidor fixa **sysadmin** ou à função de banco de dados fixa **db_owner** .
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir considera que `xp_sample` esteja implementado como xp_sample.dll e tenha sido executado. DBCC \<*dllname*> (FREE) descarrega o arquivo xp_sample.dll associado ao procedimento estendido `xp_sample`.
  
```sql  
DBCC xp_sample (FREE);  
```  
  
## <a name="see-also"></a>Consulte Também  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[Características de execução de procedimentos armazenados estendidos](../../relational-databases/extended-stored-procedures-programming/execution-characteristics-of-extended-stored-procedures.md)  
[sp_addextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)  
[sp_dropextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
[sp_helpextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)  
[Descarregamento de uma DLL de procedimento armazenado estendido](../../relational-databases/extended-stored-procedures-programming/unloading-an-extended-stored-procedure-dll.md)
  
  
