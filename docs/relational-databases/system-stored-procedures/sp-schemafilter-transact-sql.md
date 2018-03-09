---
title: sp_schemafilter (Transact-SQL) | Microsoft Docs
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
- sp_schemafilter_TSQL
- sp_schemafilter
helpviewer_keywords:
- sp_schemafilter
ms.assetid: 199e869b-2cd2-44ee-b2ee-69edb06a1bc4
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 635a9d8fc39ea3621c4ba9b11f54300c19ec1011
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spschemafilter-transact-sql"></a>sp_schemafilter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica e exibe informações sobre o esquema que é excluído ao listar tabelas Oracle qualificadas para publicação.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_schemafilter [ @publisher = ] 'publisher'   
   [ , [ @schema = ] 'schema' ]   
   [ , [ @operation = ] 'operation' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@publisher**  =] **'***publicador***'**  
 É o nome do não[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador. *publicador* é **sysname**, sem padrão.  
  
 [ **@schema**  =] **'***esquema***'**  
 É o nome do esquema. *esquema* é **sysname**, com um valor padrão de NULL.  
  
 [ **@operation**  =] **'***operação***'**  
 É a ação a ser executada neste esquema. *operação* é **nvarchar (4)**, e pode ser um dos valores a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|**Adicionar**|Adiciona o esquema especificado à lista de esquemas não qualificados para publicação.|  
|**drop**|Descarta o esquema especificado na lista de esquemas não qualificados para publicação.|  
|**Ajuda**|Retorna a lista de esquemas não qualificados para publicação.|  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**SchemaName**|**sysname**|É o nome do esquema não qualificado para publicação.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_schemafilter** só deve ser usado para Publicadores heterogêneos.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** pode executar a função de servidor fixa no distribuidor **sp_schemafilter**.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
