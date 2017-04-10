---
title: "Criar um ponto de extremidade de espelhamento de banco de dados para grupos de disponibilidade AlwaysOn (SQL Server PowerShell) | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Grupos de Disponibilidade [SQL Server], instância de servidor"
  - "Grupos de disponibilidade [SQL Server], implantando"
  - "Grupos de disponibilidade [SQL Server], ponto de extremidade"
ms.assetid: 6197bbe7-67d4-446d-ba5f-cabfa5df77f1
caps.latest.revision: 9
ms.author: "mikeray"
manager: "jhubbard"
---
# Criar um ponto de extremidade de espelhamento de banco de dados para grupos de disponibilidade AlwaysOn (SQL Server PowerShell)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve como criar um ponto de extremidade de espelhamento de banco de dados para uso do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o PowerShell.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  [Segurança](#Security)  
  
-   **Para criar um ponto de extremidade de espelhamento de banco de dados usando:**  [PowerShell](#PowerShellProcedure)  
  
## Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
> [!IMPORTANT]  
>  O algoritmo RC4 é preterido. [!INCLUDE[ssNoteDepFutureDontUse](../../../includes/ssnotedepfuturedontuse-md.md)] Recomendamos usar AES.  
  
####  <a name="Permissions"></a> Permissões  
 Exige a permissão CREATE ENDPOINT ou a associação na função de servidor fixa sysadmin. Para obter mais informações, veja [Permissões GRANT do ponto de extremidade &#40;Transact-SQL&#41;](../../../t-sql/statements/grant-endpoint-permissions-transact-sql.md).  
  
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
  
    -   [Permitir que um ponto de extremidade de espelhamento de banco de dados use certificados para conexões de saída &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/database mirroring - use certificates for outbound connections.md)  
  
    -   [Permitir que um ponto de extremidade de espelhamento de banco de dados use certificados para conexões de entrada &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/database mirroring - use certificates for inbound connections.md)  
  
-   [Especificar um endereço de rede do servidor &#40;Espelhamento de banco de dados&#41;](../../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)  
  
-   [Especificar a URL do ponto de extremidade ao adicionar ou modificar uma réplica de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify endpoint url - adding or modifying availability replica.md)  
  
 **Para exibir informações sobre o ponto de extremidade de espelhamento de banco de dados**  
  
-   [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)  
  
## Consulte também  
 [Criar um grupo de disponibilidade &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)   
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  