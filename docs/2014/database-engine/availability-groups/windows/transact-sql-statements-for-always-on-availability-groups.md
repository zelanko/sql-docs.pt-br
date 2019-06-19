---
title: Visão geral de instruções Transact-SQL para grupos de disponibilidade AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], about
- Availability Groups [SQL Server], Transact-SQL statements
ms.assetid: 184d0a81-2259-4db9-9d0d-01aac0b502c8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f635faa05d7d77a50d31491b1bab9b16875e728c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62813806"
---
# <a name="overview-of-transact-sql-statements-for-alwayson-availability-groups-sql-server"></a>Visão geral de instruções Transact-SQL para Grupos de Disponibilidade AlwaysOn (SQL Server)
  Este tópico apresenta as instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)] que oferecem suporte à implantação do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] e à criação e ao gerenciamento de grupos de disponibilidade, réplicas de disponibilidade e bancos de dados de disponibilidade.  
  
  
##  <a name="CreateEndpoint"></a> CREATE ENDPOINT  
 [CREATE ENDPOINT... FOR DATABASE_MIRRORING](/sql/t-sql/statements/create-endpoint-transact-sql) cria um ponto de extremidade de espelhamento de banco de dados, caso não exista nenhum na instância de servidor. Cada instância de servidor na qual você pretende implantar o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] ou o espelhamento de banco de dados requer um ponto de extremidade de espelhamento de banco de dados.  
  
 Execute essa instrução na instância de servidor em que você está criando o ponto de extremidade. É possível criar somente um ponto de extremidade de espelhamento de banco de dados em uma instância. Para obter mais informações, consulte [O ponto de extremidade de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md).  
  
##  <a name="CreateAG"></a> CREATE AVAILABILITY GROUP  
 [CREATE AVAILABILITY GROUP](/sql/t-sql/statements/create-availability-group-transact-sql) cria um novo grupo de disponibilidade e opcionalmente um ouvinte de grupo de disponibilidade. No mínimo, você deve especificar sua instância de servidor local que se tornará a réplica primária inicial. Opcionalmente, você também pode especificar até quatro réplicas secundárias.  
  
 Execute CREATE AVAILABILITY GROUP na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em que você deseja hospedar a réplica primária inicial de seu novo grupo de disponibilidade. Essa instância de servidor deve residir em um nó de um Failover de Cluster WSFC (Windows Server) (para obter mais informações, consulte [pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md).  
  
##  <a name="AlterAG"></a> ALTER AVAILABILITY GROUP  
 [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) oferece suporte à alteração de um grupo de disponibilidade existente ou de ouvinte de grupo de disponibilidade e ao failover de um grupo de disponibilidade.  
  
 Execute ALTER AVAILABILITY GROUP na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospeda a réplica primária atual.  
  
##  <a name="AlterDb"></a> ALTER DATABASE... SET HADR...  
 As opções da cláusula [SET HADR](/sql/t-sql/statements/alter-database-transact-sql-set-hadr) da instrução ALTER DATABASE permitem unir um banco de dados secundário ao grupo de disponibilidade do banco de dados primário correspondente, removem um banco de dados unido e suspendem a sincronização de dados em um banco de dados unido e retomam a sincronização de dados.  
  
##  <a name="DropAG"></a> DROP AVAILABILITY GROUP  
 [DROP AVAILABILITY GROUP](/sql/t-sql/statements/drop-availability-group-transact-sql) remove um grupo de disponibilidade especificado e todas as suas réplicas. DROP AVAILABILITY GROUP pode ser executado em qualquer nó [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] no cluster de failover do WSFC.  
  
##  <a name="Restrictions"></a> Restrições nas instruções Transact-SQL AVAILABILITY GROUP  
 As instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)] CREATE AVAILABILITY GROUP, ALTER AVAILABILITY GROUP e DROP AVAILABILITY GROUP têm as seguintes limitações:  
  
-   Com exceção de DROP AVAILABILITY GROUP, a execução dessas instruções requer que o serviço HADR seja habilitado na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Habilitar e desabilitar Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md).  
  
-   Essas instruções não podem ser executadas dentro de transações ou lotes.  
  
-   Embora elas se empenhem ao máximo para fazer a limpeza após uma falha, elas não garantem a reversão de todas as alterações após a falha. No entanto, os sistemas devem ser capazes de tratar e, em seguida, ignorar as falhas parciais.  
  
-   Essas instruções não oferecem suporte a expressões ou variáveis.  
  
-   Se uma instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] for executada enquanto outra recuperação ou ação do grupo de disponibilidade estiver em andamento, a instrução retornará um erro. Espere a conclusão da ação ou da recuperação e repita a instrução, se necessário.  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
  
