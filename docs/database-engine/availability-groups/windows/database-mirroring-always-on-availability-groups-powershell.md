---
title: 'Powershell: Ponto de extremidade de espelhamento de banco de dados do grupo de disponibilidade'
description: Descreve como criar um ponto de extremidade de espelhamento de banco de dados para um Grupo de Disponibilidade AlwaysOn usando o PowerShell.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], server instance
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], endpoint
ms.assetid: 6197bbe7-67d4-446d-ba5f-cabfa5df77f1
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d8cc91d628c365d4f9092ca24a8b4df06f17adf2
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75252903"
---
# <a name="create-a-database-mirroring-endpoint-for-an-availability-group-using-powershell"></a>Criar um ponto de extremidade de espelhamento de banco de dados para um grupo de disponibilidade usando o PowerShell
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve como criar um ponto de extremidade de espelhamento de banco de dados para uso do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o PowerShell.  
  

  
##  <a name="Permissions"></a> Permissões  
 Exige a permissão CREATE ENDPOINT ou a associação na função de servidor fixa sysadmin. Para obter mais informações, consulte [Permissões GRANT do ponto de extremidade &#40;Transact-SQL&#41;](../../../t-sql/statements/grant-endpoint-permissions-transact-sql.md).  

> [!IMPORTANT]  
>  O algoritmo RC4 é preterido. [!INCLUDE[ssNoteDepFutureDontUse](../../../includes/ssnotedepfuturedontuse-md.md)] Recomendamos usar AES.  
  
##  <a name="PowerShellProcedure"></a> Usando o PowerShell  
 **Para criar um ponto de extremidade de espelhamento de banco de dados**  
  
1.  Altere o diretório (**cd**) para a instância de servidor para a qual você deseja criar o ponto de extremidade de espelhamento de banco de dados.  
  
2.  Use o cmdlet **New-SqlHadrEndpoint** para criar o ponto de extremidade e use o **Set-SqlHadrEndpoint** para iniciar o ponto de extremidade.  
  
###  <a name="PShellExample"></a> Exemplo (PowerShell)  
 Os comandos do PowerShell a seguir criam um ponto de extremidade de espelhamento de banco de dados em uma instância do SQL Server (*Machine*\\*Instance*). O ponto de extremidade usa a porta 5022.  
  
> [!IMPORTANT]  
>  Este exemplo só funciona em uma instância de servidor que atualmente não tem um ponto de extremidade de espelhamento de banco de dados.  
  
```  
# Create the endpoint.  
$endpoint = New-SqlHadrEndpoint MyMirroringEndpoint -Port 5022 -Path SQLSERVER:\SQL\Machine\Instance  
  
# Start the endpoint  
Set-SqlHadrEndpoint -InputObject $endpoint -State "Started"  
  
```  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para configurar um ponto de extremidade de espelhamento de banco de dados**  
  
-   [Criar um ponto de extremidade de espelhamento de banco de dados para a Autenticação do Windows &#40;SQL Server&#41;](../../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Usar certificados para um ponto de extremidade de espelhamento de banco de dados &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
    -   [Permitir que um ponto de extremidade de espelhamento de banco de dados use certificados para conexões de saída &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
    -   [Permitir que um ponto de extremidade de espelhamento de banco de dados use certificados para conexões de entrada &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/database-mirroring-use-certificates-for-inbound-connections.md)  
  
-   [Especificar um endereço de rede do servidor &#40;Espelhamento de banco de dados&#41;](../../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)  
  
-   [Especificar a URL do ponto de extremidade ao adicionar ou modificar uma réplica de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
 **Para exibir informações sobre o ponto de extremidade de espelhamento de banco de dados**  
  
-   [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Criar um grupo de disponibilidade &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)   
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
