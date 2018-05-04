---
title: sys.fn_hadr_backup_is_preferred_replica  (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.fn_hadr_backup_is_preferred_replica_TSQL
- sys.fn_hadr_backup_is_preferred_replica
- fn_hadr_backup_is_preferred_replica_TSQL
- fn_hadr_backup_is_preferred_replica
dev_langs:
- TSQL
helpviewer_keywords:
- backup on secondary replicas
- active secondary replicas [SQL Server], backup on secondary replicas
- sys.fn_hadr_backup_is_preferred_replica function
ms.assetid: 61b9be77-e2f6-4da1-b2ae-a62cbe226145
caps.latest.revision: 19
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3cf2513671262ec2a5e1d62755572e541f548a62
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sysfnhadrbackupispreferredreplica--transact-sql"></a>sys.fn_hadr_backup_is_preferred_replica  (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Usado para determinar se a réplica atual for a réplica de backup preferencial.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.fn_hadr_backup_is_preferred_replica ( 'dbname' )  
```  
  
## <a name="arguments"></a>Argumentos  
 '*dbname*'  
 É o nome do banco de dados do qual é feito o backup. *DBName* é do tipo sysname.  
  
## <a name="returns"></a>Retorna  
 Retornará 1 se o banco de dados da instância atual estiver na réplica preferencial. Caso contrário, retorna 0.  
  
## <a name="remarks"></a>Remarks  
 Use esta função em um script de backup para determinar se o banco de dados atual está na réplica preferencial para backups. Você pode executar um script em cada réplica de disponibilidade. Cada um desses trabalhos examina os mesmos dados para determinar qual trabalho deve ser executado, portanto, somente um dos trabalhos agendados realmente passa para o estágio de backup. O código de exemplo pode ser semelhante ao seguinte:  
  
```  
If sys.fn_hadr_backup_is_preferred_replica( @dbname ) <> 1   
BEGIN  
-- If this is not the preferred replica, exit (probably without error).  
END  
-- If this is the preferred replica, continue to do the backup.  
  
```  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-sysfnhadrbackupispreferredreplica"></a>A. Usando sys.fn_hadr_backup_is_preferred_replica  
 O exemplo a seguir retornará 1 se o banco de dados atual for a réplica de backup preferencial.  
  
```  
SELECT sys.fn_hadr_backup_is_preferred_replica ('TestDB');  
GO  
```  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Configurar Backup em réplicas de disponibilidade & #40; SQL Server & #41;](../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
## <a name="see-also"></a>Consulte também  
 [Funções de grupos de disponibilidade sempre &#40;Transact-SQL&#41;](../../relational-databases/system-functions/always-on-availability-groups-functions-transact-sql.md)   
 [Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [CRIAR GRUPO de DISPONIBILIDADE &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [Secundárias ativas: Backup em réplicas secundárias &#40;em grupos de disponibilidade AlwaysOn&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)[exibições do catálogo de grupos de disponibilidade AlwaysOn &#40;Transact-SQL    &#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)  
  
  
