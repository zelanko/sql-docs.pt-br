---
description: MSpublication_access (Transact-SQL)
title: MSpublication_access (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpublication_access_TSQL
- MSpublication_access
dev_langs:
- TSQL
helpviewer_keywords:
- MSpublication_access system table
ms.assetid: 7bebe47e-3153-4579-8092-5723667a24c6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f8a6e52f94bae4214c1a40e1f180c73b0193c5ff
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89524533"
---
# <a name="mspublication_access-transact-sql"></a>MSpublication_access (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSpublication_access** contém uma linha para cada [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon que tem acesso à publicação ou ao Publicador específico. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**publication_id**|**int**|A ID da publicação.|  
|**entrar**|**sysname**|Contas do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows que existem no lado do Publicador e do Distribuidor.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
