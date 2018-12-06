---
title: Instruções Transact-SQL para Grupos de Disponibilidade AlwaysOn | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
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
ms.openlocfilehash: 730ce9da4a2e44dec103b6c0620acae176f969d1
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52506551"
---
# <a name="transact-sql-statements-for-always-on-availability-groups"></a>Instruções Transact-SQL para Grupos de Disponibilidade AlwaysOn
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico apresenta as instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)] que oferecem suporte à implantação do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] e à criação e ao gerenciamento de grupos de disponibilidade, réplicas de disponibilidade e bancos de dados de disponibilidade.  
  
 **Neste tópico:**  
  
-   [CREATE ENDPOINT](#CreateEndpoint)  
  
-   [CREATE AVAILABILITY GROUP](#CreateAG)  
  
-   [ALTER AVAILABILITY GROUP](#AlterAG)  
  
-   [Opções ALTER DATABASE SET HADR](#AlterDb)  
  
-   [DROP AVAILABILITY GROUP](#DropAG)  
  
-   [Restrições nas instruções Transact-SQL AVAILABILITY GROUP](#Restrictions)  
  
##  <a name="CreateEndpoint"></a> CREATE ENDPOINT  
 [CREATE ENDPOINT... FOR DATABASE_MIRRORING](../../../t-sql/statements/create-endpoint-transact-sql.md) cria um ponto de extremidade de espelhamento de banco de dados, caso não exista nenhum na instância de servidor. Cada instância de servidor na qual você pretende implantar o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] ou o espelhamento de banco de dados requer um ponto de extremidade de espelhamento de banco de dados.  
  
 Execute essa instrução na instância de servidor em que você está criando o ponto de extremidade. É possível criar somente um ponto de extremidade de espelhamento de banco de dados em uma instância. Para obter mais informações, consulte [O ponto de extremidade de espelhamento de banco de dados &#40;SQL Server&#41;](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md).  
  
##  <a name="CreateAG"></a> CREATE AVAILABILITY GROUP  
 [CREATE AVAILABILITY GROUP](../../../t-sql/statements/create-availability-group-transact-sql.md) cria um novo grupo de disponibilidade e opcionalmente um ouvinte de grupo de disponibilidade. No mínimo, você deve especificar sua instância de servidor local que se tornará a réplica primária inicial. Opcionalmente, você também pode especificar até quatro réplicas secundárias.  
  
 Execute CREATE AVAILABILITY GROUP na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em que você deseja hospedar a réplica primária inicial de seu novo grupo de disponibilidade. Essa instância de servidor deve residir em um nó de um WSFC (Windows Server Failover Cluster) (para obter mais informações, consulte [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
##  <a name="AlterAG"></a> ALTER AVAILABILITY GROUP  
 [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) oferece suporte à alteração de um grupo de disponibilidade existente ou de ouvinte de grupo de disponibilidade e ao failover de um grupo de disponibilidade.  
  
 Execute ALTER AVAILABILITY GROUP na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospeda a réplica primária atual.  
  
##  <a name="AlterDb"></a> ALTER DATABASE... SET HADR...  
 As opções da cláusula [SET HADR](../../../t-sql/statements/alter-database-transact-sql-set-hadr.md) da instrução ALTER DATABASE permitem unir um banco de dados secundário ao grupo de disponibilidade do banco de dados primário correspondente, removem um banco de dados unido e suspendem a sincronização de dados em um banco de dados unido e retomam a sincronização de dados.  
  
##  <a name="DropAG"></a> DROP AVAILABILITY GROUP  
 [DROP AVAILABILITY GROUP](../../../t-sql/statements/drop-availability-group-transact-sql.md) remove um grupo de disponibilidade especificado e todas as suas réplicas. DROP AVAILABILITY GROUP pode ser executado em qualquer nó [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] no cluster de failover do WSFC.  
  
##  <a name="Restrictions"></a> Restrições nas instruções Transact-SQL AVAILABILITY GROUP  
 As instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)] CREATE AVAILABILITY GROUP, ALTER AVAILABILITY GROUP e DROP AVAILABILITY GROUP têm as seguintes limitações:  
  
-   Com exceção de DROP AVAILABILITY GROUP, a execução dessas instruções requer que o serviço HADR seja habilitado na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Habilitar e desabilitar Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md).  
  
-   Essas instruções não podem ser executadas dentro de transações ou lotes.  
  
-   Embora elas se empenhem ao máximo para fazer a limpeza após uma falha, elas não garantem a reversão de todas as alterações após a falha. No entanto, os sistemas devem ser capazes de tratar e, em seguida, ignorar as falhas parciais.  
  
-   Essas instruções não oferecem suporte a expressões ou variáveis.  
  
-   Se uma instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] for executada enquanto outra recuperação ou ação do grupo de disponibilidade estiver em andamento, a instrução retornará um erro. Espere a conclusão da ação ou da recuperação e repita a instrução, se necessário.  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
