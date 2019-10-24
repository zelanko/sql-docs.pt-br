---
title: Alterar o período de tempo limite da sessão de uma réplica de disponibilidade (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], session timeout
- session timeout [SQL Server]
ms.assetid: e23c6e06-1cd1-4d4a-9bc2-e3e06ab2933d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1408d970093fde0e2efea9662b56b9f099d6b0b4
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2019
ms.locfileid: "72783027"
---
# <a name="change-the-session-timeout-period-for-an-availability-replica-sql-server"></a>Alterar o período de tempo limite da sessão de uma réplica de disponibilidade (SQL Server)
  Este tópico descreve como configurar o período de tempo limite da sessão de uma réplica de disponibilidade AlwaysOn usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../../includes/tsql-md.md)]ou o PowerShell no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. O período de tempo limite da sessão é uma propriedade de réplica que controla quantos segundos uma réplica de disponibilidade espera por uma resposta de ping de uma réplica conectada antes de considerar que ocorreu uma falha na conexão. Por padrão, uma réplica espera 10 segundos por uma resposta de ping. Esta propriedade de réplica aplica-se apenas à conexão entre uma determinada réplica secundária e a réplica primária do grupo de disponibilidade. Para obter mais informações o período de tempo limite da sessão, confira [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md).  
  
-   **Antes de começar:**  
  
     [Pré-requisitos](#Prerequisites)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para alterar o período do tempo limite de sessão usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Prerequisites  
  
-   Você deve estar conectado à instância do servidor que hospeda a réplica primária.  
  
###  <a name="Recommendations"></a> Recomendações  
 Recomendamos que você mantenha o tempo limite em 10 segundos ou mais. Definir o valor como menos de 10 segundos cria a possibilidade de um sistema extremamente carregado perdendo PINGs e declarando uma falsa falha.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para alterar o período do tempo limite de sessão de uma réplica de disponibilidade**  
  
1.  No Pesquisador de Objetos, conecte-se à instância de servidor que hospeda a réplica primária e expanda a árvore de servidores.  
  
2.  Expanda os nós **Alta Disponibilidade AlwaysOn** e **Grupos de Disponibilidade** .  
  
3.  Clique no grupo de disponibilidade cuja réplica de disponibilidade você deseja configurar.  
  
4.  Clique com o botão direito do mouse na réplica a ser configurada e clique em **Propriedades**.  
  
5.  Na caixa de diálogo **Propriedades da Réplica de Disponibilidade** , use o campo **Tempo limite da sessão (segundos)** para alterar o número de segundos do período do tempo limite da sessão nesta réplica.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 **Para alterar o período do tempo limite de sessão de uma réplica de disponibilidade**  
  
1.  Conecte-se à instância de servidor que hospeda a réplica primária.  
  
2.  Use a instrução [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) , da seguinte maneira:  
  
     ALTER AVAILABILITY GROUP *group_name*  
  
     MODIFY REPLICA ON '*instance_name*' WITH ( SESSION_TIMEOUT =*seconds* )  
  
     em que *group_name* é o nome do grupo de disponibilidade, *instance_name* é o nome da instância de servidor que hospeda a réplica de disponibilidade a ser modificada e *seconds* especifica o número mínimo de segundos que a réplica deve esperar antes de aplicar o log aos bancos de dados ao funcionar como uma réplica secundária. O valor padrão é 0 segundos, o que indica que não há nenhum atraso de aplicação.  
  
     O exemplo a seguir, inserido na réplica primária do grupo de disponibilidade `AccountsAG` , altera o valor do tempo limite da sessão para `15` segundos para a réplica localizada na instância de servidor `INSTANCE09` .  
  
    ```  
    ALTER AVAILABILITY GROUP AccountsAG   
       MODIFY REPLICA ON 'INSTANCE09' WITH (SESSION_TIMEOUT = 15);  
    ```  
  
##  <a name="PowerShellProcedure"></a> Usando o PowerShell  

### <a name="to-change-the-session-timeout-period-for-an-availability-replica"></a>Para alterar o período do tempo limite de sessão de uma réplica de disponibilidade
  
1.  Altere o diretório (`cd`) para a instância do servidor que hospeda a réplica primária.  
  
2.  Use o cmdlet `Set-SqlAvailabilityReplica` com o parâmetro `SessionTimeout` para alterar o número de segundos do período de tempo limite da sessão em uma réplica de disponibilidade especificada.  
  
     Por exemplo, o seguinte comando define o período de tempo limite de sessão para 15 segundos.  
  
    ```powershell
    Set-SqlAvailabilityReplica -SessionTimeout 15 -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AvailabilityReplicas\MyReplica  
    ```  
  
    > [!NOTE]  
    >  Para exibir a sintaxe de um cmdlet, use o cmdlet `Get-Help` no ambiente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
Para configurar e usar o provedor de SQL Server PowerShell, consulte [provedor de SQL Server PowerShell](../../../powershell/sql-server-powershell-provider.md).
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do &#40;grupos de disponibilidade AlwaysOn SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)  
