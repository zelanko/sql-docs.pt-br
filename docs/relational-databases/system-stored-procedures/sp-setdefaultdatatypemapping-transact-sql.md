---
title: sp_setdefaultdatatypemapping (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_setdefaultdatatypemapping
- sp_setdefaultdatatypemapping_TSQL
helpviewer_keywords:
- sp_setdefaultdatatypemapping
ms.assetid: 7394e8ca-4ce1-4e99-a784-205007c2c248
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 6b8d3751448d553666f7b7301c42329f32a7713a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="spsetdefaultdatatypemapping-transact-sql"></a>sp_setdefaultdatatypemapping (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Marca um mapeamento de tipo de dados existente entre [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e não[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados (DBMS) do sistema de gerenciamento como o padrão. Esse procedimento armazenado é executado no Distribuidor em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [  **@mapping_id=** ] *mapping_id*  
 Identifica um mapeamento de tipo de dados existente.  *mapping_id* é **int**, com o valor padrão de NULL. Se você especificar *mapping_id*, em seguida, os parâmetros restantes não são necessários.  
  
 [ **@source_dbms**=] **'***source_dbms***'**  
 É o nome do DBMS no qual os tipos de dados são mapeados. *source_dbms* é **sysname**, e pode ser um dos valores a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|A origem é um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ORACLE**|A origem é um banco de dados Oracle.|  
|NULL (padrão)||  
  
 Você deve especificar esse parâmetro se *mapping_id* é NULL.  
  
 [  **@source_version=** ] **'***source_version***'**  
 É o número da versão do DBMS de origem. *source_version* é **varchar (10)**, com um valor padrão de NULL.  
  
 [ **@source_type**=] **'***source_type***'**  
 É o tipo de dados no DBMS de origem. *source_type* é **sysname**. Você deve especificar esse parâmetro se *mapping_id* é NULL.  
  
 [  **@source_length_min=** ] *source_length_min*  
 É o comprimento mínimo do tipo de dados no DBMS de origem. *source_length_min* é **bigint**, com um valor padrão de NULL.  
  
 [  **@source_length_max=** ] *source_length_max*  
 É o comprimento máximo do tipo de dados no DBMS de origem. *source_length_max* é **bigint**, com um valor padrão de NULL.  
  
 [  **@source_precision_min=** ] *source_precision_min*  
 É a precisão mínima do tipo de dados no DBMS de origem. *source_precision_min* é **bigint**, com um valor padrão de NULL.  
  
 [  **@source_precision_max=** ] *source_precision_max*  
 É a precisão máxima do tipo de dados no DBMS de origem. *source_precision_max* é **bigint**, com um valor padrão de NULL.  
  
 [  **@source_scale_min=** ] *source_scale_min*  
 É a escala mínima do tipo de dados no DBMS de origem. *source_scale_min* é **int**, com um valor padrão de NULL.  
  
 [  **@source_scale_max=** ] *source_scale_max*  
 É a escala máxima do tipo de dados no DBMS de origem. *source_scale_max* é **int**, com um valor padrão de NULL.  
  
 [  **@source_nullable=** ] *source_nullable*  
 Especifica se o tipo de dados no DBMS de origem dá suporte a um valor de NULL. *source_nullable* é **bit**, com um valor padrão de NULL. **1** significa que valores NULL têm suporte.  
  
 [ **@destination_dbms** =] **'***destination_dbms***'**  
 O nome do DBMS de destino. *destination_dbms* é **sysname**, e pode ser um dos valores a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|O destino é um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ORACLE**|O destino é um banco de dados Oracle.|  
|**DB2**|O destino é um banco de dados IBM DB2.|  
|**SYBASE**|O destino é um banco de dados Sybase.|  
|NULL (padrão)||  
  
 [ **@destination_version**=] **'***destination_version***'**  
 É a versão de produto do DBMS de destino. *destination_version* é **varchar (10)**, com um valor padrão de NULL.  
  
 [ **@destination_type**=] **'***destination_type***'**  
 É o tipo de dados listado no DBMS de destino. *destination_type* é **sysname**, com um valor padrão de NULL.  
  
 [  **@destination_length=** ] *destination_length*  
 É o comprimento do tipo de dados no DBMS de destino. *destination_length* é **bigint**, com um valor padrão de NULL.  
  
 [  **@destination_precision=** ] *destination_precision*  
 É a precisão do tipo de dados no DBMS de destino. *destination_precision* é **bigint**, com um valor padrão de NULL.  
  
 [  **@destination_scale=** ] *destination_scale*  
 É a escala do tipo de dados no DBMS de destino. *destination_scale* é **int**, com um valor padrão de NULL.  
  
 [  **@destination_nullable=** ] *destination_nullable*  
 Especifica se o tipo de dados no DBMS de destino dá suporte a um valor de NULL. *destination_nullable* é **bit**, com um valor padrão de NULL. **1** significa que valores NULL têm suporte.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_setdefaultdatatypemapping** é usado em todos os tipos de replicação entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e não[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBMS.  
  
 Os mapeamentos de tipo de dados padrão se aplicam a todas as topologias de replicação que incluem o DBMS especificado.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** pode executar a função de servidor fixa **sp_setdefaultdatatypemapping**.  
  
## <a name="see-also"></a>Consulte também  
 [Especificar mapeamentos de tipo de dados para um publicador Oracle](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [sp_getdefaultdatatypemapping &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)   
 [sp_helpdatatypemap &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)  
  
  
