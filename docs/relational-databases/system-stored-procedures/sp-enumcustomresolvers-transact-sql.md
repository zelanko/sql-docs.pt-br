---
title: sp_enumcustomresolvers (Transact-SQL) | Microsoft Docs
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
- sp_enumcustomresolvers
- sp_enumcustomresolvers_TSQL
helpviewer_keywords:
- sp_enumcustomresolvers
ms.assetid: 81bd0d3a-48dc-42b1-b662-c630f61fc630
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: eb49ae55f4bde2304713f4fd336076585a987904
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32993153"
---
# <a name="spenumcustomresolvers-transact-sql"></a>sp_enumcustomresolvers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma lista de todos os manipuladores de lógica de negócios disponíveis e resolvedores personalizados registrados no Distribuidor. Esse procedimento armazenado é executado no Publicador, em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_enumcustomresolvers [ [ @distributor =] 'distributor']  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@distributor =**] **'***distribuidor***'**  
 É o nome do Distribuidor em que o resolvedor personalizado está localizado. *distribuidor* é **sysname**, com um padrão NULL. *Esse parâmetro é preterido e será removido em uma versão futura.*  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**article_resolver**|**nvarchar(255)**|Nome amigável para o manipulador de lógica de negócios ou resolvedor de conflito.|  
|**resolver_clsid**|**nvarchar(50)**|CLSID (ID de classe) do resolvedor com base em COM. Para um manipulador de lógica de negócios, essa coluna retorna um valor zero de CLSID.|  
|**is_dotnet_assembly**|**bit**|Indica se o registro é para um manipulador de lógica de negócios.<br /><br /> **0** = resolvedor de conflitos baseado em COM<br /><br /> **1** = manipulador de lógica de negócios|  
|**dotnet_assembly_name**|**nvarchar(255)**|O nome do assembly do [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework que implementa o manipulador de lógica de negócios.|  
|**dotnet_class_name**|**nvarchar(255)**|É o nome da classe que substitui <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> para implementar o manipulador de lógica de negócios.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_enumcustomresolvers** é usado em replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função fixa de servidor e o **db_owner** pode executar a função de banco de dados fixa **sp_enumcustomresolvers**.  
  
## <a name="see-also"></a>Consulte também  
 [Implementar um manipulador de lógica de negócios para um artigo de mesclagem](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)   
 [Implementar um resolvedor de conflitos personalizado para um artigo de mesclagem](../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)   
 [sp_lookupcustomresolver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lookupcustomresolver-transact-sql.md)   
 [sp_unregistercustomresolver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
