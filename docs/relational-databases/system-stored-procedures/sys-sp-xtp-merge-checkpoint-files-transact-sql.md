---
title: sys. sp_xtp_merge_checkpoint_files (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/28/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_xtp_merge_checkpoint_files_TSQL
- sys.sp_xtp_merge_checkpoint_files
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_xtp_merge_checkpoint_files
ms.assetid: da04df2a-f7a1-41e7-a1ef-2d5d68919892
author: stevestein
ms.author: sstein
ms.openlocfilehash: 73638d41c7a24a37c068d365771b4d0469a174d5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68041017"
---
# <a name="syssp_xtp_merge_checkpoint_files-transact-sql"></a>sys.sp_xtp_merge_checkpoint_files (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  **Sys. sp_xtp_merge_checkpoint_files** mescla todos os arquivos de dados e Delta no intervalo de transações especificado.  
  
 Para obter mais informações, consulte [criando e gerenciando armazenamento para objetos com otimização de memória](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
||  
|-|  
|**Observação**: esse procedimento armazenado é preterido [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]no. Ele não é mais necessário e não pode ser usado, iniciando [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].|  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.sp_xtp_merge_checkpoint_files database_name, @transaction_lower_bound, @transaction_upper_bound  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 O nome do banco de dados no qual invocar a mesclagem. Se o banco de dados não tiver tabelas na memória, este procedimento retornará com erro do usuário. Se o banco de dados estiver offline, ele retornará um erro.  
  
 *lower_bound_Tid*  
 O limite inferior de transações para um arquivo de dados, conforme mostrado em [Sys. dm_db_xtp_checkpoint_files &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md) correspondente ao arquivo de ponto de verificação inicial da mesclagem. Um erro é gerado para o valor inválido de transactonId.  
  
 *upper_bound_Tid*  
 O (BIGINT) limite superior de transações para um arquivo de dados, conforme mostrado em [Sys. dm_db_xtp_checkpoint_files &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md). Um erro é gerado para o valor inválido de transactonId.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhum  
  
## <a name="cursors-returned"></a>Cursores retornados  
 Nenhum  
  
## <a name="permissions"></a>Permissões  
 Requer a função de servidor fixa sysadmin e a função de banco de dados fixa db_owner.  
  
## <a name="remarks"></a>Comentários  
 Mescla os dados e arquivos delta no intervalo válido para gerar um único arquivo de dados e delta. Esse procedimento não honra a política de mesclagem.  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
