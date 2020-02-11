---
title: Restaurar um banco de dados e associá-lo a um pool de recursos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 0d20a569-8a27-409c-bcab-0effefb48013
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: cac1e775d5cccaccca90b03104de4132e651284e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62467840"
---
# <a name="restore-a-database-and-bind-it-to-a-resource-pool"></a>Restaurar um banco de dados e associá-lo a um pool de recursos
  Embora você tenha memória suficiente para restaurar um banco de dados com tabelas com otimização memória, siga as práticas recomendadas e associe o banco de dados a um pool de recursos nomeado. Como o banco de dados deve existir antes de você poder associá-lo ao pool, restaurar seu banco de dados é um processo de várias etapas. Este tópico orienta ao longo desse processo.  
  
##  <a name="restore-with-norecovery"></a>Restaurar com NORECOVERY  
 Quando você restaurar um banco de dados, NORECOVERY faz com que o banco de dados seja criado e a imagem de disco seja restaurada sem consumir memória.  
  
```sql  
RESTORE DATABASE IMOLTP_DB   
   FROM DISK = 'C:\IMOLTP_test\IMOLTP_DB.bak'  
   WITH NORECOVERY  
```  
  
##  <a name="create-the-resource-pool"></a>Criar o pool de recursos  
 O [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir cria um pool de recursos chamado Pool_IMOLTP com 50% da memória disponível para seu uso.  Depois que o pool é criado, o Administrador de Recursos é reconfigurado para incluir o Pool_IMOLTP.  
  
```sql  
CREATE RESOURCE POOL Pool_IMOLTP WITH (MAX_MEMORY_PERCENT = 50);  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
##  <a name="bind-the-database-and-resource-pool"></a>Associar o banco de dados e o pool de recursos  
 Use a função do sistema `sp_xtp_bind_db_resource_pool` para associar o banco de dados ao pool de recursos. A função usa dois parâmetros: o nome do banco de dados seguido pelo nome do pool de recursos.  
  
 O [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir define uma associação do banco de dados IMOLTP_DB ao pool de recursos Pool_IMOLTP. A associação não entra em vigor até que você conclua a próxima etapa.  
  
```sql  
EXEC sp_xtp_bind_db_resource_pool 'IMOLTP_DB', 'Pool_IMOLTP'  
GO  
```  
  
##  <a name="restore-with-recovery"></a>Restaurar com RECOVERY  
 Quando você restaura o banco de dados com recuperação, o banco de dados é colocado online e todos os dados restaurados.  
  
```sql  
RESTORE DATABASE IMOLTP_DB   
   WITH RECOVERY  
```  
  
##  <a name="monitor-the-resource-pool-performance"></a>Monitorar o desempenho do pool de recursos  
 Quando o banco de dados for associado ao pool de recursos nomeado e restaurado com recuperação, monitore o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o objeto Resource Pool Stats. Para obter mais informações, consulte [Objeto SQLServer:Resource Pool Stats](../performance-monitor/sql-server-resource-pool-stats-object.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Associar um banco de dados com tabelas com otimização de memória a um pool de recursos](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [sys.sp_xtp_bind_db_resource_pool &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-bind-db-resource-pool-transact-sql)   
 [SQL Server, objeto de estatísticas do pool de recursos](../performance-monitor/sql-server-resource-pool-stats-object.md)   
 [sys.dm_resource_governor_resource_pools](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql)  
  
  
