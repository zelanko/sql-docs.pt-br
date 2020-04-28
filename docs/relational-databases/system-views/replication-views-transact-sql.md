---
title: Exibições de replicação (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- distribution databases [SQL Server replication], system views
- metadata [SQL Server], views
- views [SQL Server], replication
- replication views [SQL Server]
- publications [SQL Server replication], system views
- articles [SQL Server replication], system views
- replication metadata [SQL Server]
- subscriptions [SQL Server replication], system views
- system views [SQL Server], replication
ms.assetid: 93e5056d-0d93-4a48-ba33-72762eb995d8
author: stevestein
ms.author: sstein
ms.openlocfilehash: 51cc9434805fbd14204d74edae1594ae01c06bb2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68129574"
---
# <a name="replication-views-transact-sql"></a>Exibições de replicação (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Essas exibições contêm informações que são usadas pela replicação [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]no. As exibições permitem o acesso mais fácil aos dados nas [tabelas do sistema de replicação](../../relational-databases/system-tables/replication-tables-transact-sql.md). As exibições são criadas em um banco de dados de usuário quando esse banco de dados está habilitado como banco de dados de publicação ou assinatura. Todos os objetos de replicação são removidos dos bancos de dados do usuário quando o banco de dados é removido de uma topologia de replicação. O método preferencial para acessar metadados de replicação é usando [procedimentos armazenados de replicação](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).  
  
> [!IMPORTANT]  
>  Exibições de sistema não devem ser alteradas diretamente por nenhum usuário.  
  
## <a name="replication-views"></a>Exibições de replicação  
 A seguir, uma lista das exibições de sistema usadas pela replicação, agrupadas por banco de dados.  
  
### <a name="replication-views-in-the-msdb-database"></a>Exibições de replicação no banco de dados msdb  
  
|||  
|-|-|  
|[&#41;&#40;Transact-SQL de MSdatatype_mappings](../../relational-databases/system-views/msdatatype-mappings-transact-sql.md)|[&#41;sysdatatypemappings &#40;Transact-SQL](../../relational-databases/system-views/sysdatatypemappings-transact-sql.md)|  
  
### <a name="replication-views-in-the-distribution-database"></a>Exibições de replicação no banco de dados de distribuição  
  
|||  
|-|-|  
|[&#41;IHextendedArticleView &#40;Transact-SQL](../../relational-databases/system-views/ihextendedarticleview-transact-sql.md)|[sysarticles &#40;exibição do sistema&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)|  
|[&#41;IHextendedSubscriptionView &#40;Transact-SQL](../../relational-databases/system-views/ihextendedsubscriptionview-transact-sql.md)|[&#41;sysextendedarticlesview &#40;Transact-SQL](../../relational-databases/system-views/sysextendedarticlesview-transact-sql.md)|  
|[&#41;IHsyscolumns &#40;Transact-SQL](../../relational-databases/system-views/ihsyscolumns-transact-sql.md)|[syspublications &#40;Modo de Exibição do Sistema&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/syspublications-system-view-transact-sql.md)|  
|[&#41;&#40;Transact-SQL de MSdistribution_status](../../relational-databases/system-views/msdistribution-status-transact-sql.md)|[syssubscriptions &#40;Modo de Exibição do Sistema&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/syssubscriptions-system-view-transact-sql.md)|  
|[sysarticlecolumns &#40;exibição do sistema&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)||  
  
### <a name="replication-views-in-the-publication-database"></a>Exibições de replicação no banco de dados de publicação  
  
|||  
|-|-|  
|[&#41;sysmergeextendedarticlesview &#40;Transact-SQL](../../relational-databases/system-views/sysmergeextendedarticlesview-transact-sql.md)|[&#41;sysmergepartitioninfoview &#40;Transact-SQL](../../relational-databases/system-views/sysmergepartitioninfoview-transact-sql.md)|  
|[&#41;systranschemas &#40;Transact-SQL](../../relational-databases/system-views/systranschemas-transact-sql.md)||  
  
### <a name="replication-views-in-the-subscription-database"></a>Exibições de replicação no banco de dados de assinatura  
  
|||  
|-|-|  
|[&#41;sysmergeextendedarticlesview &#40;Transact-SQL](../../relational-databases/system-views/sysmergeextendedarticlesview-transact-sql.md)|[&#41;sysmergepartitioninfoview &#40;Transact-SQL](../../relational-databases/system-views/sysmergepartitioninfoview-transact-sql.md)|  
|[&#41;systranschemas &#40;Transact-SQL](../../relational-databases/system-views/systranschemas-transact-sql.md)||  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
