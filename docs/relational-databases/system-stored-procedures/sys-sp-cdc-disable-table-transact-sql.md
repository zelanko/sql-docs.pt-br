---
title: sys.sp_cdc_disable_table (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 0b1c2f30758987c902e5610ef3fa9f8b26809889
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58533738"
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
`[ @source_schema = ] 'source\_schema'` É o nome do esquema no qual a tabela de origem está contida. *source_schema* está **sysname**, sem padrão, e não pode ser NULL.  
  
 *source_schema* deve existir no banco de dados atual.  
  
`[ @source_name = ] 'source\_name'` É o nome da tabela de origem do qual alteração captura de dados deve ser desabilitada. *source_name* está **sysname**, sem padrão, e não pode ser NULL.  
  
 *source_name* deve existir no banco de dados atual.  
  
`[ @capture_instance = ] 'capture\_instance' | 'all'` É o nome da instância de captura para desabilitar para a tabela de origem especificado. *capture_instance* está **sysname** e não pode ser NULL.  
  
 Quando 'all'é especificado, todas as instâncias de captura definidas para *source_name* estão desabilitados.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentários  
 **sp_cdc_disable_table** descartes do change data capture alterar tabela e funções do sistema associadas com a instância de captura e a tabela de origem especificada. Exclui qualquer linha associada com a instância de captura especificada da tabelas de sistema do change data capture e define o **is_tracked_by_cdc** coluna para a entrada de tabela na [sys. Tables](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md) exibição do catálogo como 0.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na **db_owner** função fixa de banco de dados.  
  
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
 [sys.sp_cdc_enable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)  
  
  
