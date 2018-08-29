---
title: sp_cdc_get_captured_columns (Transact-SQL) | Microsoft Docs
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
- sp_cdc_get_captured_columns
- sys.sp_cdc_get_captured_columns
- sys.sp_cdc_get_captured_columns_TSQL
- sp_cdc_get_captured_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_cdc_get_captured_columns
- sp_cdc_get_captured_columns
- change data capture [SQL Server], querying metadata
ms.assetid: d9e680be-ab9b-4e0c-b63a-90658f241df8
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a53411c8be883f65f511473415dfc0226b21dcf2
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43024141"
---
# <a name="sysspcdcgetcapturedcolumns-transact-sql"></a>sys.sp_cdc_get_captured_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações de metadados de captura de dados de alteração das colunas de origem capturadas, localizadas pela instância de captura especificada. A captura de dados de alteração não está disponível em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.sp_cdc_get_captured_columns   
    [ @capture_instance = ] 'capture_instance'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @capture_instance =] '*capture_instance*'  
 É o nome da instância de captura associada à tabela de origem. *capture_instance* está **sysname** e não pode ser NULL.  
  
 Para gerar relatórios sobre as instâncias de captura para a tabela, execute as [sp_cdc_help_change_data_capture](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md) procedimento armazenado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|source_schema|**sysname**|Nome do esquema de tabela de origem.|  
|source_table|**sysname**|Nome da tabela de origem.|  
|capture_instance|**sysname**|Nome da instância de captura.|  
|column_name|**sysname**|Nome da coluna de origem capturada.|  
|column_id|**int**|ID da coluna na tabela de origem.|  
|column_ordinal|**int**|Posição da coluna na tabela de origem.|  
|data_type|**sysname**|Tipo de dados da coluna.|  
|character_maximum_length|**int**|Comprimento de máximo de caractere da coluna com base em caractere, caso contrário é NULL.|  
|NUMERIC_PRECISION|**tinyint**|Precisão da coluna com base numérica, caso contrário é NULL.|  
|numeric_precision_radix|**smallint**|Precisão base da coluna com base numérica, caso contrário é NULL.|  
|numeric_scale|**int**|Escala coluna com base numérica, caso contrário é NULL.|  
|datetime_precision|**smallint**|Precisão da coluna com base em data e hora, caso contrário é NULL.|  
  
## <a name="remarks"></a>Remarks  
 Use sys. sp_cdc_get_captured_columns para obter informações de coluna sobre as colunas capturadas retornadas ao consultar as funções de consulta de instância de captura [CDC. fn_cdc_get_all_changes < capture_instance >](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md) ou [CDC. fn_cdc_get_net_changes < capture_instance >](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md). Os nomes de coluna, ID e posição permanecem constantes durante a duração da instância de captura. Somente o tipo de dados de coluna é alterado quando o tipo de dados da coluna de origem subjacente na tabela controlada é alterado. As colunas que são adicionadas ou descartadas de uma tabela de origem não têm impacto sobre as colunas capturadas de instâncias de captura existente.  
  
 Use [sp_cdc_get_ddl_history](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-ddl-history-transact-sql.md) para obter informações sobre a definição de dados instruções DDL (linguagem) aplicadas a uma tabela de origem. Qualquer mudança de DDL que modificou a estrutura de uma coluna de origem localizada é retornada no conjunto de resultados.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados fixa db_owner. Para todos os outros usuários, requer a permissão SELECT em todas as colunas capturadas na tabela de origem e, se uma função associada para a instância de captura tiver sido definida, faça associação nessa função de banco de dados. Quando o chamador não tiver permissão para exibir os dados de origem, a função retornará o erro 22981 (O objeto não existe ou o acesso a ele é negado).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna informações sobre as colunas capturadas na instância de captura `HumanResources_Employee`.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_get_captured_columns   
    @capture_instance = N'HumanResources_Employee';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_cdc_help_change_data_capture &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)  
  
  
