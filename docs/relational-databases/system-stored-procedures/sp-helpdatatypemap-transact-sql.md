---
title: sp_helpdatatypemap (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpdatatypemap
- sp_helpdatatypemap_TSQL
helpviewer_keywords:
- sp_helpdatatypemap
ms.assetid: 800c9c65-723e-4961-a63d-327987f129f0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0b9666c13a2e4d8183d19fade64bf49b13377b9a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68771056"
---
# <a name="sp_helpdatatypemap-transact-sql"></a>sp_helpdatatypemap (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Retorna informações sobre os mapeamentos de tipo de dados [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definidos entre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o DBMS (sistemas de gerenciamento não-de bits). Esse procedimento armazenado é executado no Distribuidor em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @source_dbms = ] 'source_dbms'`É o nome do DBMS do qual os tipos de dados são mapeados. *source_dbms* é **sysname**e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**MSSQLSERVER**|A origem é um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ORACLE**|A origem é um banco de dados Oracle.|  
  
`[ @source_version = ] 'source_version'`É a versão do produto do DBMS de origem. *source_version*é **varchar (10)** e, se não for especificado, os mapeamentos de tipo de dados para todas as versões do DBMS de origem serão retornados. Habilita o conjunto de resultados a ser filtrado pela versão de fonte do DBMS.  
  
`[ @source_type = ] 'source_type'`É o tipo de dados listado no DBMS de origem. *source_type* é **sysname**e, se não for especificado, os mapeamentos para todos os tipos de dados no DBMS de origem serão retornados. Habilita o conjunto de resultados a ser filtrado pelo tipo de dados no DBMS de origem.  
  
`[ @destination_dbms = ] 'destination_dbms'`É o nome do DBMS de destino. *destination_dbms* é **sysname**e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**MSSQLSERVER**|O destino é um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ORACLE**|O destino é um banco de dados Oracle.|  
|**DB2**|O destino é um banco de dados IBM DB2.|  
|**SYBASE**|O destino é um banco de dados Sybase.|  
  
`[ @destination_version = ] 'destination_version'`É a versão do produto do DBMS de destino. *destination_version*é **varchar (10)** e, se não for especificado, os mapeamentos para todas as versões do DBMS de destino serão retornados. Habilita o conjunto de resultados a ser filtrado pela versão de destino do DBMS.  
  
`[ @destination_type = ] 'destination_type'`É o tipo de dados listado no DBMS de destino. *destination_type*é **sysname**e, se não for especificado, os mapeamentos para todos os tipos de dados no DBMS de destino serão retornados. Habilita o conjunto de resultados a ser filtrado pelo tipo de dados no DBMS de destino.  
  
`[ @defaults_only = ] defaults_only`É se apenas os mapeamentos de tipo de dados padrão forem retornados. *defaults_only* é **bit**, com um padrão de **0**. **1** significa que somente os mapeamentos de tipo de dados padrão são retornados. **0** significa que o padrão e os mapeamentos de tipo de dados definidos pelo usuário são retornados.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Descrição|  
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
 **sp_helpdatatypemap** define mapeamentos de tipo de dados de Publicadores não SQL Server e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de Publicadores para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes não.  
  
 Quando a combinação especificada de DBMS de origem e de destino não é suportada, **sp_helpdatatypemap** retorna um conjunto de resultados vazio.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** no distribuidor ou membros da função de banco de dados fixa **db_owner** no banco de dados de distribuição podem executar **sp_helpdatatypemap**.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_getdefaultdatatypemapping](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_setdefaultdatatypemapping](../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md)  
  
  
