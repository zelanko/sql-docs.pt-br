---
title: sys. sp_cdc_disable_table (Transact-SQL) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c3586c6a18d01dda7f1e462b8874cc9d9f36d2d5
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82832479"
---
# <a name="syssp_cdc_disable_table-transact-sql"></a>sys.sp_cdc_disable_table (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Desabilita a captura de dados de alteração para a tabela de origem especificada e a instância de captura no banco de dados atual. A captura de dados de alteração não está disponível em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.sp_cdc_disable_table   
  [ @source_schema = ] 'source_schema' ,   
  [ @source_name = ] 'source_name'  
  [ , [ @capture_instance = ] 'capture_instance' | 'all' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @source_schema = ] 'source\_schema'`É o nome do esquema no qual a tabela de origem está contida. *source_schema* é **sysname**, sem padrão, e não pode ser nulo.  
  
 *source_schema* deve existir no banco de dados atual.  
  
`[ @source_name = ] 'source\_name'`É o nome da tabela de origem da qual a captura de dados de alteração deve ser desabilitada. *source_name* é **sysname**, sem padrão, e não pode ser nulo.  
  
 *source_name* deve existir no banco de dados atual.  
  
`[ @capture_instance = ] 'capture\_instance' | 'all'`É o nome da instância de captura a ser desabilitada para a tabela de origem especificada. *capture_instance* é **sysname** e não pode ser nulo.  
  
 Quando ' all' é especificado, todas as instâncias de captura definidas para *source_name* são desabilitadas.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 **Sys. sp_cdc_disable_table** descarta a tabela de alteração da captura de dados de alterações e as funções do sistema associadas à tabela de origem e à instância de captura especificadas. Ele exclui todas as linhas associadas à instância de captura especificada das tabelas do sistema de captura de dados de alterações e define a coluna **is_tracked_by_cdc** para a entrada de tabela na exibição de catálogo [Sys. Tables](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md) como 0.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados fixa **db_owner** .  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [sys.sp_cdc_enable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)  
  
  
