---
description: sp_fulltext_database (Transact-SQL)
title: sp_fulltext_database (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_database_TSQL
- sp_fulltext_database
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_database
ms.assetid: eeb1e151-eb00-484c-8fd1-5641e621ffc6
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 27e239838e8112b30ef5ba7bbb54082050b220a5
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549764"
---
# <a name="sp_fulltext_database-transact-sql"></a>sp_fulltext_database (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Não tem efeito nos catálogos de texto completo no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e em versões posteriores e tem suporte apenas para compatibilidade com versões anteriores. **sp_fulltext_database** não desabilita o mecanismo de texto completo para um determinado banco de dados. Todos os bancos de dados criados pelo usuário no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] sempre são habilitados para indexação de texto completo.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_fulltext_database [@action=] 'action'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @action = ] 'action'` É a ação a ser executada. a **ação** é **varchar (20)** e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**enable**|Com suporte somente para compatibilidade com versões anteriores. Não tem nenhum efeito em catálogos de texto completo no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e em versões posteriores.|  
|**disable**|Com suporte somente para compatibilidade com versões anteriores. Não tem nenhum efeito em catálogos de texto completo no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e em versões posteriores.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 No [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e em versões posteriores, a indexação de texto completo não pode ser desativada. Desabilitar a indexação de texto completo não remove linhas de **sysfulltextcatalogs** e não indica que as tabelas habilitadas para texto completo não estão mais marcadas para indexação de texto completo. Todas as definições de metadados de texto completo permanecem nas tabelas do sistema.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** e **db_owner** função de banco de dados fixa podem ser executados **sp_fulltext_database**.  
  
## <a name="see-also"></a>Consulte Também  
 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [FULLTEXTSERVICEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
