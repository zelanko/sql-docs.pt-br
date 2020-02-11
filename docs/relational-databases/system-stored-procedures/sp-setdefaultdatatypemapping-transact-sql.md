---
title: sp_setdefaultdatatypemapping (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_setdefaultdatatypemapping
- sp_setdefaultdatatypemapping_TSQL
helpviewer_keywords:
- sp_setdefaultdatatypemapping
ms.assetid: 7394e8ca-4ce1-4e99-a784-205007c2c248
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9f0dfadc3b2b990d999df1d66069c4b68df9e6cf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68104412"
---
# <a name="sp_setdefaultdatatypemapping-transact-sql"></a>sp_setdefaultdatatypemapping (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Marca um mapeamento de tipo de dados [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] existente entre o e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] um sistema de gerenciamento que não seja de banco de dados (DBMS) como o padrão. Esse procedimento armazenado é executado no Distribuidor em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_setdefaultdatatypemapping [ [ @mapping_id = ] mapping_id ]  
    [ , [ @source_dbms = ] 'source_dbms' ]  
    [ , [ @source_version = ] 'source_version' ]  
    [ , [ @source_type = ] 'source_type' ]   
    [ , [ @source_length_min = ] source_length_min ]  
    [ , [ @source_length_max = ] source_length_max ]  
    [ , [ @source_precision_min = ] source_precision_min ]  
    [ , [ @source_precision_max = ] source_precision_max ]  
    [ , [ @source_scale_min = ] source_scale_min ]  
    [ , [ @source_scale_max = ] source_scale_max ]  
    [ , [ @source_nullable = ] source_nullable ]  
    [ , [ @destination_dbms = ] 'destination_dbms' ]  
    [ , [ @destination_version = ] 'destination_version' ]  
    [ , [ @destination_type = ] 'destination_type' ]  
    [ , [ @destination_length = ] destination_length ]  
    [ , [ @destination_precision = ] destination_precision ]  
    [ , [ @destination_scale = ] destination_scale ]  
    [ , [ @destination_nullable = ] source_nullable ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @mapping_id = ] mapping_id`Identifica um mapeamento de tipo de dados existente.  *mapping_id* é **int**, com o valor padrão de NULL. Se você especificar *mapping_id*, os parâmetros restantes não serão necessários.  
  
`[ @source_dbms = ] 'source_dbms'`É o nome do DBMS do qual os tipos de dados são mapeados. *source_dbms* é **sysname**e pode ser um dos valores a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**MSSQLSERVER**|A origem é um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ORACLE**|A origem é um banco de dados Oracle.|  
|NULL (padrão)||  
  
 Você deve especificar esse parâmetro se *mapping_id* for NULL.  
  
`[ @source_version = ] 'source_version'`É o número de versão do DBMS de origem. *source_version* é **varchar (10)**, com um valor padrão de NULL.  
  
`[ @source_type = ] 'source_type'`É o tipo de dados no DBMS de origem. *source_type* é **sysname**. Você deve especificar esse parâmetro se *mapping_id* for NULL.  
  
`[ @source_length_min = ] source_length_min`É o comprimento mínimo do tipo de dados no DBMS de origem. *source_length_min* é **bigint**, com um valor padrão de NULL.  
  
`[ @source_length_max = ] source_length_max`É o comprimento máximo do tipo de dados no DBMS de origem. *source_length_max* é **bigint**, com um valor padrão de NULL.  
  
`[ @source_precision_min = ] source_precision_min`É a precisão mínima do tipo de dados no DBMS de origem. *source_precision_min* é **bigint**, com um valor padrão de NULL.  
  
`[ @source_precision_max = ] source_precision_max`É a precisão máxima do tipo de dados no DBMS de origem. *source_precision_max* é **bigint**, com um valor padrão de NULL.  
  
`[ @source_scale_min = ] source_scale_min`É a escala mínima do tipo de dados no DBMS de origem. *source_scale_min* é **int**, com um valor padrão de NULL.  
  
`[ @source_scale_max = ] source_scale_max`É a escala máxima do tipo de dados no DBMS de origem. *source_scale_max* é **int**, com um valor padrão de NULL.  
  
`[ @source_nullable = ] source_nullable`É se o tipo de dados no DBMS de origem der suporte a um valor NULL. *source_nullable* é **bit**, com um valor padrão de NULL. **1** significa que há suporte para valores nulos.  
  
`[ @destination_dbms = ] 'destination_dbms'`É o nome do DBMS de destino. *destination_dbms* é **sysname**e pode ser um dos valores a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**MSSQLSERVER**|O destino é um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ORACLE**|O destino é um banco de dados Oracle.|  
|**DB2**|O destino é um banco de dados IBM DB2.|  
|**SYBASE**|O destino é um banco de dados Sybase.|  
|NULL (padrão)||  
  
`[ @destination_version = ] 'destination_version'`É a versão do produto do DBMS de destino. *destination_version* é **varchar (10)**, com um valor padrão de NULL.  
  
`[ @destination_type = ] 'destination_type'`É o tipo de dados listado no DBMS de destino. *destination_type* é **sysname**, com um valor padrão de NULL.  
  
`[ @destination_length = ] destination_length`É o comprimento do tipo de dados no DBMS de destino. *destination_length* é **bigint**, com um valor padrão de NULL.  
  
`[ @destination_precision = ] destination_precision`É a precisão do tipo de dados no DBMS de destino. *destination_precision* é **bigint**, com um valor padrão de NULL.  
  
`[ @destination_scale = ] destination_scale`É a escala do tipo de dados no DBMS de destino. *destination_scale* é **int**, com um valor padrão de NULL.  
  
`[ @destination_nullable = ] destination_nullable`É se o tipo de dados no DBMS de destino der suporte a um valor NULL. *destination_nullable* é **bit**, com um valor padrão de NULL. **1** significa que há suporte para valores nulos.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_setdefaultdatatypemapping** é usado em todos os tipos de replicação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entre o e um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não DBMS.  
  
 Os mapeamentos de tipo de dados padrão se aplicam a todas as topologias de replicação que incluem o DBMS especificado.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_setdefaultdatatypemapping**.  
  
## <a name="see-also"></a>Consulte Também  
 [Especificar mapeamentos de tipo de dados para um Publicador Oracle](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [&#41;&#40;Transact-SQL de sp_getdefaultdatatypemapping](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpdatatypemap](../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)  
  
  
