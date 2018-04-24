---
title: Restaurar um banco de dados e associá-lo a um pool de recursos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0d20a569-8a27-409c-bcab-0effefb48013
caps.latest.revision: 15
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 51889249cacb9367d7e6b90184c07277fa61290a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="restore-a-database-and-bind-it-to-a-resource-pool"></a>Restaurar um banco de dados e associá-lo a um pool de recursos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Embora você tenha memória suficiente para restaurar um banco de dados com tabelas com otimização memória, siga as práticas recomendadas e associe o banco de dados a um pool de recursos nomeado. Como o banco de dados deve existir antes de você poder associá-lo ao pool, restaurar seu banco de dados é um processo de várias etapas. Este tópico orienta ao longo desse processo.  
  
## <a name="restoring-a-database-with-memory-optimized-tables"></a>Restaurando um banco de dados com tabelas com otimização de memória  
 As etapas a seguir restauram completamente o banco de dados IMOLTP_DB e o associam ao Pool_IMOLTP.  
  
1.  [Restaurar com NORECOVERY](../../relational-databases/in-memory-oltp/restore-a-database-and-bind-it-to-a-resource-pool.md#bkmk_NORECOVERY)  
  
2.  [Criar o pool de recursos](../../relational-databases/in-memory-oltp/restore-a-database-and-bind-it-to-a-resource-pool.md#bkmk_createPool)  
  
3.  [Associar o banco de dados e o pool de recursos](../../relational-databases/in-memory-oltp/restore-a-database-and-bind-it-to-a-resource-pool.md#bkmk_bind)  
  
4.  [Restaurar com RECOVERY](../../relational-databases/in-memory-oltp/restore-a-database-and-bind-it-to-a-resource-pool.md#bkmk_RECOVERY)  
  
5.  [Monitorar o desempenho do pool de recursos](../../relational-databases/in-memory-oltp/restore-a-database-and-bind-it-to-a-resource-pool.md#bkmk_Monitor)  
  
###  <a name="bkmk_NORECOVERY"></a> Restaurar com NORECOVERY  
 Quando você restaurar um banco de dados, NORECOVERY faz com que o banco de dados seja criado e a imagem de disco seja restaurada sem consumir memória.  
  
```sql  
RESTORE DATABASE IMOLTP_DB   
   FROM DISK = 'C:\IMOLTP_test\IMOLTP_DB.bak'  
   WITH NORECOVERY  
```  
  
###  <a name="bkmk_createPool"></a> Criar o pool de recursos  
 O [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir cria um pool de recursos chamado Pool_IMOLTP com 50% da memória disponível para seu uso.  Depois que o pool é criado, o Administrador de Recursos é reconfigurado para incluir o Pool_IMOLTP.  
  
```sql  
CREATE RESOURCE POOL Pool_IMOLTP WITH (MAX_MEMORY_PERCENT = 50);  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
###  <a name="bkmk_bind"></a> Associar o banco de dados e o pool de recursos  
 Use a função do sistema `sp_xtp_bind_db_resource_pool` para associar o banco de dados ao pool de recursos. A função usa dois parâmetros: o nome do banco de dados seguido pelo nome do pool de recursos.  
  
 O [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir define uma associação do banco de dados IMOLTP_DB ao pool de recursos Pool_IMOLTP. A associação não entra em vigor até que você conclua a próxima etapa.  
  
```sql  
EXEC sp_xtp_bind_db_resource_pool 'IMOLTP_DB', 'Pool_IMOLTP'  
GO  
```  
  
###  <a name="bkmk_RECOVERY"></a> Restaurar com RECOVERY  
 Quando você restaura o banco de dados com recuperação, o banco de dados é colocado online e todos os dados restaurados.  
  
```sql  
RESTORE DATABASE IMOLTP_DB   
   WITH RECOVERY  
```  
  
###  <a name="bkmk_Monitor"></a> Monitorar o desempenho do pool de recursos  
 Quando o banco de dados for associado ao pool de recursos nomeado e restaurado com recuperação, monitore o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o objeto Resource Pool Stats. Para obter mais informações, consulte [Objeto SQLServer:Resource Pool Stats](../../relational-databases/performance-monitor/sql-server-resource-pool-stats-object.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Associar um banco de dados com tabelas com otimização de memória a um pool de recursos](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [sys.sp_xtp_bind_db_resource_pool &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-bind-db-resource-pool-transact-sql.md)   
 [Objeto SQLServer:Resource Pool Stats](../../relational-databases/performance-monitor/sql-server-resource-pool-stats-object.md)   
 [sys.dm_resource_governor_resource_pools](../../relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql.md)  
  
  
