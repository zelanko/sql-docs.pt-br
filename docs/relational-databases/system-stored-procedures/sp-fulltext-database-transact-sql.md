---
title: sp_fulltext_database (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_fulltext_database_TSQL
- sp_fulltext_database
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_database
ms.assetid: eeb1e151-eb00-484c-8fd1-5641e621ffc6
caps.latest.revision: 45
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 5ee4cb63c476b898c286f6223e9e56d1778e6a47
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39563900"
---
# <a name="spfulltextdatabase-transact-sql"></a>sp_fulltext_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Não tem efeito nos catálogos de texto completo no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e em versões posteriores e tem suporte apenas para compatibilidade com versões anteriores. **sp_fulltext_database** não desabilita o mecanismo de texto completo para um determinado banco de dados. Todos os bancos de dados criados pelo usuário no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] sempre são habilitados para indexação de texto completo.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_fulltext_database [@action=] 'action'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@action=**] **'***ação***'**  
 É a ação a ser executada. **ação** está **varchar(20)**, e pode ser um destes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**enable**|Com suporte somente para compatibilidade com versões anteriores. Não tem nenhum efeito em catálogos de texto completo no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e em versões posteriores.|  
|**disable**|Com suporte somente para compatibilidade com versões anteriores. Não tem nenhum efeito em catálogos de texto completo no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e em versões posteriores.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Remarks  
 No [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e em versões posteriores, a indexação de texto completo não pode ser desativada. Desabilitar a indexação de texto completo não remove linhas da **sysfulltextcatalogs** e não indicar que tabelas habilitadas de texto completo não são mais marcadas para indexação de texto completo. Todas as definições de metadados de texto completo permanecem nas tabelas do sistema.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa e **db_owner** banco de dados fixa podem executar **sp_fulltext_database**.  
  
## <a name="see-also"></a>Consulte também  
 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [FULLTEXTSERVICEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
