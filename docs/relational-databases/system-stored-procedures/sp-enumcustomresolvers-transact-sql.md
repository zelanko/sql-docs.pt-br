---
title: sp_enumcustomresolvers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_enumcustomresolvers
- sp_enumcustomresolvers_TSQL
helpviewer_keywords:
- sp_enumcustomresolvers
ms.assetid: 81bd0d3a-48dc-42b1-b662-c630f61fc630
author: stevestein
ms.author: sstein
ms.openlocfilehash: 361a0d8e47372612eddf40cdf1663df2e70da0a6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68124625"
---
# <a name="sp_enumcustomresolvers-transact-sql"></a>sp_enumcustomresolvers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma lista de todos os manipuladores de lógica de negócios disponíveis e resolvedores personalizados registrados no Distribuidor. Esse procedimento armazenado é executado no Publicador, em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_enumcustomresolvers [ [ @distributor =] 'distributor']  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @distributor = ] 'distributor'`É o nome do distribuidor no qual o resolvedor personalizado está localizado. o *distribuidor* é **sysname**, com um padrão de NULL. *Esse parâmetro é preterido e será removido em uma versão futura.*  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**article_resolver**|**nvarchar (255)**|Nome amigável para o manipulador de lógica de negócios ou resolvedor de conflito.|  
|**resolver_clsid**|**nvarchar(50)**|CLSID (ID de classe) do resolvedor com base em COM. Para um manipulador de lógica de negócios, essa coluna retorna um valor zero de CLSID.|  
|**is_dotnet_assembly**|**bit**|Indica se o registro é para um manipulador de lógica de negócios.<br /><br /> **0** = resolvedor de conflitos com base em com<br /><br /> **1** = manipulador de lógica de negócios|  
|**dotnet_assembly_name**|**nvarchar (255)**|O nome do assembly do [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework que implementa o manipulador de lógica de negócios.|  
|**dotnet_class_name**|**nvarchar (255)**|É o nome da classe que substitui <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> para implementar o manipulador de lógica de negócios.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_enumcustomresolvers** é usado na replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** e a função de banco de dados fixa **db_owner** podem executar **sp_enumcustomresolvers**.  
  
## <a name="see-also"></a>Consulte Também  
 [Implementar um manipulador de lógica de negócios para um artigo de mesclagem](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)   
 [Implementar um resolvedor de conflitos personalizado para um artigo de mesclagem](../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)   
 [&#41;&#40;Transact-SQL de sp_lookupcustomresolver](../../relational-databases/system-stored-procedures/sp-lookupcustomresolver-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_unregistercustomresolver](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
