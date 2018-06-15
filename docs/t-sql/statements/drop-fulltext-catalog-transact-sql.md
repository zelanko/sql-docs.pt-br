---
title: DROP FULLTEXT CATALOG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DROP_FULLTEXT_CATALOG_TSQL
- DROP FULLTEXT CATALOG
dev_langs:
- TSQL
helpviewer_keywords:
- dropping full-text catalogs
- removing full-text catalogs
- full-text catalogs [SQL Server], removing
- deleting full-text catalogs
- DROP FULLTEXT CATALOG statement
ms.assetid: b54efb0b-400b-49ce-923b-ce20a2a12255
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 6e379e8c123712be849e64e05d0b91030de073eb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33069443"
---
# <a name="drop-fulltext-catalog-transact-sql"></a>DROP FULLTEXT CATALOG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Remove um catálogo de texto completo de um banco de dados. Remova todos os índices de texto completo associados ao catálogo antes de remover o catálogo.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DROP FULLTEXT CATALOG catalog_name  
```  
  
## <a name="arguments"></a>Argumentos  
 *catalog_name*  
 É o nome do catálogo a ser removido. Se *catalog_name* não existir, o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará um erro e não executará a operação DROP. O grupo de arquivos do catálogo de texto completo não deve ser marcado como OFFLINE ou READONLY para que o comando tenha êxito.  
  
## <a name="permissions"></a>Permissões  
 O usuário deve ter a permissão DROP no catálogo de texto completo ou ser um membro das funções de banco de dados fixas **db_owner** ou **db_ddladmin**.  
  
## <a name="see-also"></a>Consulte Também  
 [sys.fulltext_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)   
 [ALTER FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)   
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [Pesquisa de Texto Completo](../../relational-databases/search/full-text-search.md)  
  
  
