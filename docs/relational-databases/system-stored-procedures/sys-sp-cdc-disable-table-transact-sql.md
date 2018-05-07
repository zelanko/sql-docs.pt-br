---
title: sp_cdc_disable_table (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sp_cdc_disable_table
- sp_cdc_disable_table
- sys.sp_cdc_disable_table_TSQL
- sp_cdc_disable_table_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_disable_table
- sys.sp_cdc_disable_table
- change data capture [SQL Server], disabling tables
ms.assetid: da2156c0-504e-4d76-b9a0-4448becf9bda
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 16356cc8a5d427a9432ac8c753b1e51d915337d4
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="sysspcdcdisabletable-transact-sql"></a>sys.sp_cdc_disable_table (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Desabilita a captura de dados de alteração para a tabela de origem especificada e a instância de captura no banco de dados atual. A captura de dados de alteração não está disponível em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.sp_cdc_disable_table   
  [ @source_schema = ] 'source_schema' ,   
  [ @source_name = ] 'source_name'  
  [ , [ @capture_instance = ] 'capture_instance' | 'all' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@source_schema=** ] **'***source_schema***'**  
 É o nome do esquema no qual a tabela de origem está contida. *source_schema* é **sysname**, sem padrão, e não pode ser NULL.  
  
 *source_schema* deve existir no banco de dados atual.  
  
 [  **@source_name=** ] **'***source_name***'**  
 É o nome da tabela de origem da qual desabilitar a captura de dados de alteração. *source_name* é **sysname**, sem padrão, e não pode ser NULL.  
  
 *source_name* deve existir no banco de dados atual.  
  
 [  **@capture_instance=** ] **'***capture_instance***'** | **'** todas as **'**  
 É o nome da instância de captura a ser desabilitada na tabela de origem especificada. *capture_instance* é **sysname** e não pode ser NULL.  
  
 Quando 'all' for especificada, todas as instâncias de captura definidas para *source_name* estão desabilitados.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="remarks"></a>Remarks  
 **sp_cdc_disable_table** descarta a captura de dados de alteração alterar tabela e funções do sistema associadas à instância de captura e a tabela de origem especificada. Exclui qualquer linha associada à instância de captura especificada do tabelas de sistema do change data capture e define o **is_tracked_by_cdc** coluna para a entrada da tabela no [sys. Tables](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md) exibição do catálogo como 0.  
  
## <a name="permissions"></a>Permissões  
 Requer a participação no **db_owner** função fixa de banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir desabilita a captura de dados de alteração na tabela `HumanResources.Employee`.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_disable_table   
    @source_schema = N'HumanResources',   
    @source_name = N'Employee',  
    @capture_instance = N'HumanResources_Employee';  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_cdc_enable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)  
  
  
