---
title: Tabelas do sistema (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- status information [SQL Server]
- tables [SQL Server], system tables
- information retrieval [SQL Server]
- status information [SQL Server], system tables
- system information [SQL Server]
- system tables [SQL Server]
- system tables [SQL Server], about system tables
- system tables [SQL Server], retrieving information from
- retrieving system table information
ms.assetid: 56b8ad51-930c-4e5c-8d99-8c939d5b70ac
author: stevestein
ms.author: sstein
ms.openlocfilehash: 292b6cdce6b2f13445e50f79c956f07eb8d33de7
ms.sourcegitcommit: 676458a9535198bff4c483d67c7995d727ca4a55
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69903602"
---
# <a name="system-tables-transact-sql"></a>Tabelas do sistema (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Os tópicos desta seção descrevem as tabelas do sistema no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 As tabelas do sistema não devem ser alteradas diretamente por nenhum usuário. Por exemplo, não tente modificar tabelas do sistema com instruções DELETE, UPDATE ou INSERT ou com disparadores definidos pelo usuário.  
  
 É permitido fazer referência a colunas documentadas nas tabelas do sistema. Entretanto, muitas das colunas nas tabelas do sistema não são documentadas. Não devem ser escritos aplicativos que consultem diretamente colunas não documentadas. Em vez disso, para recuperar informações armazenadas nas tabelas do sistema, os aplicativos devem usar qualquer um dos seguintes componentes:  
  
-   Procedimentos armazenados do sistema  
  
-   Instruções e funções [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SMO (Management Objects)  
  
-   RMO (Replication Management Objects)  
  
-   Funções de catálogo da API do banco de dados  
  
 Estes componentes compõem uma API publicada obtendo informações do sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O [!INCLUDE[msCoName](../../includes/msconame-md.md)] mantém a compatibilidade desses componentes de uma versão para outra. O formato das tabelas do sistema depende da arquitetura interna do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e pode ser diferente entre versões. Portanto, os aplicativos que acessem diretamente as colunas não documentadas das tabelas do sistema podem precisar ser alterados antes de acessar uma versão mais recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>Nesta seção  
 Os tópicos da tabela do sistema são organizados pelas seguintes áreas de recurso:  
  
|||  
|-|-|  
|[Fazer backup e restaurar &#40;tabelas TRANSACT-SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)|[Tabelas de envio de logs &#40;Transact-SQL&#41;](../../relational-databases/system-tables/log-shipping-tables-transact-sql.md)|  
|[Transact-SQL de &#40;tabelas de captura de dados de alterações&#41;](../../relational-databases/system-tables/change-data-capture-tables-transact-sql.md)|[Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)|  
|[Transact-SQL de &#40;tabelas do plano de manutenção de banco de dados&#41;](../../relational-databases/system-tables/database-maintenance-plan-tables-transact-sql.md)|[Transact- &#40;SQL de tabelas de SQL Server Agent&#41;](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)|  
|[SQL Server tabelas &#40;de eventos estendidos TRANSACT-SQL&#41;](../../relational-databases/extended-events/xevents-references-system-objects.md#system-tables)|[o Transact- &#40;SQL sys. sysoledbusers&#41;](../../relational-databases/system-compatibility-views/sys-sysoledbusers-transact-sql.md)|  
|[Transact- &#40;SQL de tabelas de Integration Services&#41;](../../relational-databases/system-tables/integration-services-tables-transact-sql.md)|[systranschemas &#40;Transact-SQL&#41;](../../relational-databases/system-views/systranschemas-transact-sql.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Exibições &#40;de compatibilidade TRANSACT-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
