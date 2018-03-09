---
title: sp_helpdatatypemap (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helpdatatypemap
- sp_helpdatatypemap_TSQL
helpviewer_keywords:
- sp_helpdatatypemap
ms.assetid: 800c9c65-723e-4961-a63d-327987f129f0
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d22a2c19f5824ef0a1cb5e0a145afd72492289df
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpdatatypemap-transact-sql"></a>sp_helpdatatypemap (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre os mapeamentos de tipo de dados definido entre [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e não-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (DBMS) de sistemas de gerenciamento de banco de dados. Esse procedimento armazenado é executado no Distribuidor em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpdatatypemap [ @source_dbms = ] 'source_dbms'   
    [ , [ @source_version = ] 'source_version' ]  
    [ , [ @source_type = ] 'source_type' ]   
    [ , [ @destination_dbms = ] 'destination_dbms' ]  
    [ , [ @destination_version = ] 'destination_version' ]  
    [ , [ @destination_type = ] 'destination_type' ]  
    [ , [ @defaults_only = ] defaults_only ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@source_dbms** =] **'***source_dbms***'**  
 É o nome do DBMS no qual os tipos de dados são mapeados. *source_dbms* é **sysname**, e pode ser um dos valores a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|A origem é um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ORACLE**|A origem é um banco de dados Oracle.|  
  
 [  **@source_version** =] **'***source_version***'**  
 É a versão de produto do DBMS de origem. *source_version*é **varchar (10)**, e se não for especificado, o tipo de dados mapeamentos para todas as versões da fonte de DBMS são retornados. Habilita o conjunto de resultados a ser filtrado pela versão de fonte do DBMS.  
  
 [  **@source_type** =] **'***source_type***'**  
 É o tipo de dados listado no DBMS de origem. *source_type* é **sysname**, e se não for especificado, mapeamentos de todos os tipos de dados no DBMS de origem serão retornados. Habilita o conjunto de resultados a ser filtrado pelo tipo de dados no DBMS de origem.  
  
 [  **@destination_dbms**  =] **'***destination_dbms***'**  
 O nome do DBMS de destino. *destination_dbms* é **sysname**, e pode ser um dos valores a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|O destino é um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ORACLE**|O destino é um banco de dados Oracle.|  
|**DB2**|O destino é um banco de dados IBM DB2.|  
|**SYBASE**|O destino é um banco de dados Sybase.|  
  
 [  **@destination_version** =] **'***destination_version***'**  
 É a versão de produto do DBMS de destino. *destination_version*é **varchar (10)**, e se não for especificado, mapeamentos de todas as versões do DBMS de destino serão retornados. Habilita o conjunto de resultados a ser filtrado pela versão de destino do DBMS.  
  
 [  **@destination_type** =] **'***destination_type***'**  
 É o tipo de dados listado no DBMS de destino. *destination_type*é **sysname**, e se não for especificado, mapeamentos de todos os tipos de dados no DBMS de destino serão retornados. Habilita o conjunto de resultados a ser filtrado pelo tipo de dados no DBMS de destino.  
  
 [  **@defaults_only** =] *defaults_only*  
 Especifica se os mapeamentos de tipos de dados padrão são retornados. *defaults_only* é **bit**, com um padrão de **0**. **1** significa que somente os dados padrão mapeamentos de tipo são retornados. **0** significa que o padrão e quaisquer dados definidos pelo usuário mapeamentos de tipo são retornados.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Description|  
|-----------------|-----------------|  
|**mapping_id**|Identifica um mapeamento de tipo de dados.|  
|**source_dbms**|É o nome e número da versão do DBMS de origem.|  
|**source_type**|É o tipo de dados no DBMS de origem.|  
|**destination_dbms**|O nome do DBMS de destino.|  
|**destination_type**|É o tipo de dados no DBMS de destino.|  
|**is_default**|Se o mapeamento for um padrão ou um mapeamento alternativo. Um valor de **0** indica que esse mapeamento é definido pelo usuário.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpdatatypemap** define mapeamentos de tipo de dados de editores não SQL Server e do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicadores não[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes.  
  
 Quando não há suporte para a combinação especificada de origem e destino DBMS, **sp_helpdatatypemap** retorna um conjunto de resultados vazio.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** a função de servidor fixa no distribuidor ou membros do **db_owner** função de banco de dados fixa no banco de dados de distribuição pode executar **sp_helpdatatypemap**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_getdefaultdatatypemapping &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)   
 [sp_setdefaultdatatypemapping &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md)  
  
  
