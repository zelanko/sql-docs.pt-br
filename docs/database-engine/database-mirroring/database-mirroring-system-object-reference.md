---
title: Referência de objeto do sistema de espelhamento de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.openlocfilehash: 6f43477ebb45812fb4e71ca501296518ed3950c9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66795510"
---
# <a name="database-mirroring-system-object-reference"></a>Referência de objeto do sistema de espelhamento de banco de dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="system-catalog-views"></a>Exibições de catálogo do sistema

| Exibição de catálogo do sistema | Descrição|
| :------ | :----------------------------- |
| [sys.database_mirroring_witnesses](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   | Contém uma linha para cada função testemunha desempenhada por um servidor em uma parceria de espelhamento de banco de dados. |
| &nbsp; | &nbsp; |

## <a name="system-dynamic-management-views"></a>Exibições de gerenciamento dinâmico do sistema

| Exibição de gerenciamento dinâmico do sistema | Descrição|
| :------ | :----------------------------- |
| [sys.dm_db_mirroring_auto_page_repair](../../relational-databases/system-dynamic-management-views/database-mirroring-sys-dm-db-mirroring-auto-page-repair.md)   | Retorna uma linha para cada tentativa de reparo automático de página em qualquer banco de dados espelho na instância de servidor.  |
| [sys.dm_db_mirroring_connections](../../relational-databases/system-dynamic-management-views/database-mirroring-sys-dm-db-mirroring-connections.md)    | Retorna uma linha para cada conexão estabelecida para espelhamento de banco de dados. |
| &nbsp; | &nbsp; |

## <a name="system-tables"></a>Tabelas do sistema

| Tabela do sistema | Descrição|
| :------ | :----------------------------- |
| [sysdbmaintplan_databases](../../relational-databases/system-tables/sysdbmaintplan-databases-transact-sql.md)   | Retorna informações sobre planos de manutenção de espelhamento de banco de dados. |
| [sysdbmaintplan_history](../../relational-databases/system-tables/sysdbmaintplan-history-transact-sql.md)    | Retorna informações sobre o histórico dos planos de manutenção de espelhamento de banco de dados. |
| [sysdbmaintplan_jobs](../../relational-databases/system-tables/sysdbmaintplan-jobs-transact-sql.md)    |Retorna informações sobre os trabalhos dos planos de manutenção de espelhamento de banco de dados.  |
| [sysdbmaintplans](../../relational-databases/system-tables/sysdbmaintplans-transact-sql.md)    | Retorna informações sobre planos de espelhamento de banco de dados.  |
| &nbsp; | &nbsp; |


## <a name="see-also"></a>Consulte Também  
 [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   

  
  
