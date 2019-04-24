---
title: Pré-requisitos, restrições e recomendações para grupos de disponibilidade
description: Uma descrição de pré-requisitos, restrições e recomendações para implantação de um grupo de disponibilidade Always On.
ms.custom: seodec18
ms.date: 03/22/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], server instance
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], WSFC clusters
- Availability Groups [SQL Server], about
- Availability Groups [SQL Server], prerequisites and restrictions
- Availability Groups [SQL Server], Failover Cluster Instances
- Availability Groups [SQL Server], databases
- Availability Groups [SQL Server]
ms.assetid: edbab896-42bb-4d17-8d75-e92ca11f7abb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dec0b9aa3c92cdefa82e3031546ea8200f70bb6e
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59042435"
---
# <a name="prerequisites-restrictions-and-recommendations-for-always-on-availability-groups"></a>Pré-requisitos, restrições e recomendações para Grupos de Disponibilidade AlwaysOn
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este artigo descreve considerações sobre a implantação do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], incluindo pré-requisitos, restrições e recomendações para computadores host, clusters WSFC (Cluster de Failover do Windows Server), instâncias de servidor e grupos de disponibilidade. Para cada um desses componentes, são indicadas considerações sobre segurança e as permissões exigidas, se houver.  
  
> [!IMPORTANT]  
>  Antes de implantar o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], é altamente recomendável que você leia cada seção deste tópico.  
    
##  <a name="DotNetHotfixes"></a> Hotfixes do .NET que dão suporte a grupos de disponibilidade  
 Dependendo dos componentes e recursos do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usados com o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], você poderá precisar instalar hotfixes .Net adicionais identificados na tabela seguinte. Os hotfixes podem ser instalados em qualquer ordem.  
  
||Recurso dependente|Hotfix|Link|  
|------|-----------------------|------------|----------|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]|O hotfix para o .NET 3.5 SP1 adiciona suporte a recursos do Cliente SQL para AlwaysOn de intenção de Leitura, somente leitura e multisubnetfailover. O hotfix precisa ser instalado em cada servidor de relatório do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] .|KB 2654347: [Hotfix para .NET 3.5 SP1 para adição de suporte aos recursos Always On](https://go.microsoft.com/fwlink/?LinkId=242896)|  
  

###  <a name="SystemRequirements"></a> Lista de verificação: requisitos (sistema Windows)  
 Para oferecer suporte ao recurso [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] , verifique se cada computador que participará de um ou mais grupos de disponibilidade atende aos seguintes requisitos básicos:  
  
||Requisito|Link|  
|------|-----------------|----------|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Verifique se o sistema não é um controlador de domínio.|Os grupos de disponibilidade não têm suporte em controladores de domínio.|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Verifique se cada computador está executando o Windows Server 2012 ou versões posteriores.|[Requisitos de hardware e software para a instalação do SQL Server 2016](../../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Verifique se cada computador é um nó em um WSFC.|[WSFC &#40;Windows Server Failover Clustering&#41; com o SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Verifique se o WSFC contém nós suficientes para dar suporte às configurações de grupo de disponibilidade.|Um nó de cluster pode hospedar uma réplica de um grupo de disponibilidade. O mesmo nó não pode hospedar duas réplicas do mesmo grupo de disponibilidade. O nó de cluster pode participar de vários grupos de disponibilidade, com uma réplica de cada grupo. <br /><br /> Pergunte aos administradores de banco de dados quantos nós de cluster são necessários para dar suporte às réplicas de disponibilidade dos grupos de disponibilidade planejados.<br /><br /> [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).|  

  
> [!IMPORTANT]  
>  Verifique também se seu ambiente está corretamente configurado para a conexão a um grupo de disponibilidade. Para obter mais informações, veja [Conectividade de cliente AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md).  
  
###  <a name="ComputerRecommendations"></a> Recomendações para computadores que hospedam réplicas de disponibilidade (sistema Windows)  
  
-   **Sistemas comparáveis:**  Para um grupo de disponibilidade especificado, todas as réplicas de disponibilidade devem ser executadas em sistemas comparáveis que possam manipular cargas de trabalho idênticas.  
  
-   **Adaptadores de rede dedicados:**  Para obter um melhor desempenho, use um adaptador de rede dedicado (placa de interface de rede) para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)].  
  
-   **Espaço em disco suficiente:**  Cada computador no qual uma instância de servidor hospeda uma réplica de disponibilidade precisa ter espaço em disco suficiente para todos os bancos de dados do grupo de disponibilidade. Lembre-se de que à medida que os bancos de dados primários crescem, seus bancos de dados secundários correspondentes crescem na mesma proporção.  
  
###  <a name="PermissionsWindows"></a> Permissões (sistema Windows)  
 Para administrar um WSFC, o usuário deve ser um administrador do sistema em cada nó de cluster.  
  
 Para obter mais informações sobre a conta usada para administrar o cluster, confira [Apêndice A: Requisitos do cluster de failover](https://technet.microsoft.com/library/dd197454.aspx).  
  
###  <a name="RelatedTasksWindows"></a> Tarefas relacionadas (sistema Windows)  
  
|Tarefa|Link|  
|----------|----------|  
|Defina o valor de HostRecordTTL.|[Alterar o HostRecordTTL (usando o Windows PowerShell)](#ChangeHostRecordTTLps)|  
  
####  <a name="ChangeHostRecordTTLps"></a> Alterar o HostRecordTTL (usando o Windows PowerShell)  
  
1.  Abra a janela do PowerShell por meio da opção **Executar como Administrador**.  
  
2.  Importe o módulo FailoverClusters.  
  
3.  Use o cmdlet **Get-ClusterResource** para encontrar o recurso de Nome de Rede, depois use o cmlet **Set-ClusterParameter** para definir o valor de **HostRecordTTL** , da seguinte maneira:  
  
     Get-ClusterResource "*\<NetworkResourceName>*" | Set-ClusterParameter HostRecordTTL *\<TimeInSeconds>*  
  
     O exemplo do PowerShell a seguir define o HostRecordTTL como 300 segundos para um recurso de nome de rede chamado `SQL Network Name (SQL35)`.  
  
    ```  
    Import-Module FailoverClusters  
  
    $nameResource = "SQL Network Name (SQL35)"  
    Get-ClusterResource $nameResource | Set-ClusterParameter ClusterParameter HostRecordTTL 300  
    ```  
  
    > [!TIP]  
    >  Sempre que você abrir uma nova janela do PowerShell, deverá importar o módulo **FailoverClusters** .  
  
##### <a name="related-content-powershell"></a>Conteúdo relacionado (PowerShell)  
  
-   [Clustering e alta disponibilidade](https://blogs.msdn.com/b/clustering/archive/2009/05/23/9636665.aspx) (Blog da equipe de Clustering de Failover e Balanceamento de Carga de Rede)  
  
-   [Guia de Introdução ao Windows PowerShell em um cluster de failover](https://technet.microsoft.com/library/ee619762\(WS.10\).aspx)  
  
-   [Comandos de recursos de cluster e cmdlets equivalentes no Windows PowerShell](https://msdn.microsoft.com/library/ee619744.aspx#BKMK_resource)  
  
###  <a name="RelatedContentWS"></a> Conteúdo relacionado (Windows System)  
  
-   [Definir configurações DNS em um cluster de failover multissite](https://technet.microsoft.com/library/dd197562\(WS.10\).aspx)  
  
-   [Registro de DNS com recurso de nome de rede](https://blogs.msdn.com/b/clustering/archive/2009/07/17/9836756.aspx)  
  

##  <a name="ServerInstance"></a> Pré-requisitos e restrições da instância de SQL Server  
 Cada grupo de disponibilidade requer um conjunto de parceiros de failover, conhecidos como *réplicas de disponibilidade*, que são hospedados por instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Uma instância específica pode ser uma *instância autônomo* ou uma FCI (*instância de cluster de failover*) do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 **Nesta seção:**  
  
-   [Lista de verificação: Pré-requisitos](#PrerequisitesSI)  
  
-   [Uso de thread por grupos de disponibilidade](#ThreadUsage)  
  
-   [Permissões](#PermissionsSI)  
  
-   [Tarefas relacionadas](#RelatedTasksSI)  
  
-   [Conteúdo relacionado](#RelatedContentSI)  
  
###  <a name="PrerequisitesSI"></a> Lista de verificação: pré-requisitos (instância de servidor)  
  
||Pré-requisito|Links|  
|-|------------------|-----------|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|O computador host deve ser um nó WSFC. As instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospedam as réplicas de disponibilidade de determinado grupo de disponibilidade residem em nós separados do cluster. Um grupo de disponibilidade pode temporariamente abranger dois clusters, enquanto está migrando para outro cluster. O SQL Server 2016 introduz grupos de disponibilidade distribuídos. Em um grupo de disponibilidade distribuído, dois grupos de disponibilidade residem em clusters diferentes.|[WSFC &#40;Windows Server Failover Clustering&#41; com o SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)<br /><br /> [Clustering de failover e Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)<br/> <br/> [Grupos de Disponibilidade Distribuída (Grupos de Disponibilidade AlwaysOn)](../../../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md)|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Se você desejar um grupo de disponibilidade para funcionar com o Kerberos:<br /><br /> Todas as instâncias de servidor que hospedam uma réplica de disponibilidade para o grupo de disponibilidade deve usar a mesma conta de serviço do SQL Server.<br /><br /> O administrador de domínio precisa registrar um Nome de entidade de serviço (SPN) manualmente com Active Directory na conta de serviço do SQL Server para o nome de rede virtual (VNN) do ouvinte de grupo de disponibilidade. Se o SPN for registrado em uma conta diferente da conta de serviço do SQL Server, a autenticação falhará.<br /><br /> <br /><br /> <b>\*\* Importante \*\*</b> Se você alterar a conta de serviço do SQL Server, o administrador de domínio precisará registrar de novo o SPN manualmente.|[Registrar um nome de entidade de serviço para conexões de Kerberos](../../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)<br /><br /> **Breve explicação:**<br /><br /> O Kerberos e os SPNs impõem a autenticação mútua. O SPN é mapeado para a conta do Windows que inicia os serviços do SQL Server. Se o SPN não estiver registrado corretamente ou se ele falhar, a camada de segurança do Windows não poderá determinar a conta associada ao SPN e a autenticação Kerberos não será utilizada.<br /><br /> <br /><br /> Observação: O NTLM não tem este requisito.|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Se você pretende usar uma instância de cluster de failover (FCI) do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para hospedar uma réplica de disponibilidade, verifique se compreende as restrições de FCI e se os requisitos de FCI são atendidos.|[Pré-requisitos e requisitos para usar uma FCI (Instância de Cluster de Failover) do SQL Server para hospedar uma réplica de disponibilidade](#FciArLimitations) (mais adiante neste artigo)|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Cada instância de servidor deve estar executando a mesma versão do SQL Server para participar de um Grupo de Disponibilidade Always On.|Edições e recursos compatíveis do [SQL 2014](https://docs.microsoft.com/sql/getting-started/features-supported-by-the-editions-of-sql-server-2014?view=sql-server-2014), [SQL 2016](https://docs.microsoft.com/sql/sql-server/editions-and-components-of-sql-server-2016?view=sql-server-2016), [SQL 2017](https://docs.microsoft.com/sql/sql-server/editions-and-components-of-sql-server-2017?view=sql-server-2017).|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Todas as instâncias de servidor que hospedam réplicas de disponibilidade para um grupo de disponibilidade devem usar a mesma ordenação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|[Definir ou alterar a ordenação do servidor](../../../relational-databases/collations/set-or-change-the-server-collation.md)|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Habilite o recurso [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] em cada instância de servidor que hospedará uma réplica de disponibilidade para qualquer grupo de disponibilidade. Em determinado computador, você pode habilitar quantas instâncias de servidor desejar para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] , desde que tenham suporte da instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|[Habilitar e desabilitar Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)<br /><br /> <br /><br /> <b>\*\* Importante \*\*</b> Se você destruir e recriar um WSFC, deverá desabilitar e reabilitar o recurso [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] em cada instância de servidor habilitada para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] no cluster original.|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Cada instância de servidor exige um ponto de extremidade de espelhamento de banco de dados. Note que esse ponto de extremidade é compartilhado por todas as réplicas de disponibilidade e parceiros de espelhamento de banco de dados e testemunhas na instância de servidor.<br /><br /> Se uma instância de servidor selecionada para hospedar uma réplica de disponibilidade estiver sendo executada em uma conta de usuário de domínio e ainda não tiver um ponto de extremidade de espelhamento de banco de dados, o [Assistente de Novo Grupo de Disponibilidade](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md) (ou o [Assistente para Adicionar Réplica ao Grupo de Disponibilidade](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)) poderá criar o ponto de extremidade e conceder a permissão CONNECT à conta de serviço da instância de servidor. No entanto, se o serviço [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] estiver sendo executado como uma conta interna, como Sistema Local, Serviço Local ou Serviço de Rede, ou como uma conta que não pertença a um domínio, você deverá usar certificados para autenticação de ponto de extremidade, e o assistente não poderá criar um ponto de extremidade de espelhamento de banco de dados na instância de servidor. Nesse caso, é recomendável criar manualmente os pontos de extremidade de espelhamento de banco de dados antes de iniciar o assistente.<br /><br /> <br /><br /> <b>\*\* Observação de Segurança \*\*</b> A segurança de transporte para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] é a mesma do espelhamento de banco de dados.|[O ponto de extremidade de espelhamento de banco de dados &#40;SQL Server&#41;](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)<br /><br /> [Segurança de transporte para espelhamento de banco de dados e grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Se algum banco de dados que utilize o FILESTREAM for adicionado a um grupo de disponibilidade, verifique se o FILESTREAM está habilitado em cada instância de servidor que hospedará uma réplica de disponibilidade do grupo de disponibilidade.|[Habilitar e configurar o FILESTREAM](../../../relational-databases/blob/enable-and-configure-filestream.md)|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Se algum banco de dados independente for adicionado a um grupo de disponibilidade, verifique se a opção de servidor **contained database authentication** está definida como **1** em cada instância de servidor que hospedará uma réplica de disponibilidade do grupo de disponibilidade.|[Opção de configuração do servidor contained database authentication](../../../database-engine/configure-windows/contained-database-authentication-server-configuration-option.md)<br /><br /> [Opções de configuração do servidor &#40;SQL Server&#41;](../../../database-engine/configure-windows/server-configuration-options-sql-server.md)|  
  
###  <a name="ThreadUsage"></a> Uso de thread por grupos de disponibilidade  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] tem os seguintes requisitos para threads de trabalho:  
  
-   Em uma instância ociosa do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] não usa nenhum thread.  
  
-   O número máximo de threads usados por grupos de disponibilidade é a configuração definida para o número máximo de threads de servidor ('**máximo de threads de trabalho**') menos 40.  
  
-   As réplicas de disponibilidade hospedadas em uma instância de servidor específica compartilham um único pool de threads.  
  
     Os threads são compartilhados sob demanda, da seguinte maneira:  
  
    -   Normalmente, há 3 a 10 threads compartilhados, mas esse número pode aumentar dependendo da carga de trabalho da réplica primária.  
  
    -   Se um determinado thread ficar ocioso por um tempo, ele será liberado novamente no pool de threads geral do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Normalmente, um thread inativa é liberado após ~15 segundos de inatividade. No entanto, dependendo da última atividade, um thread ocioso pode ser retido por mais tempo.  

    -   Uma instância do SQL Server usa até 100 threads de restauração paralela para réplicas secundárias. Cada banco de dados usa até metade do número total de núcleos de CPU, mas não mais de 16 threads por banco de dados. Se o número total de threads necessários para uma única instância exceder 100, o SQL Server usará um único thread de restauração para cada banco de dados restante. Os threads de restauração serial são liberados após aproximadamente 15 segundos de inatividade. 
    
    > [!NOTE]
    > Os bancos de dados são escolhidos para seguir em thread único com base na ID de banco de dados em ordem crescente. Como tal, a ordem de criação do banco de dados deve ser considerada para instâncias do SQL Server que hospedam mais bancos de dados de grupo de disponibilidade do que threads de trabalho disponíveis. Por exemplo, em um sistema com 32 ou mais núcleos de CPU, os seis primeiros bancos de dados (ordenados por ID de banco de dados) em um grupo ou grupos de disponibilidade usarão o modo de restauração paralela e todos os bancos de dados subsequentes usarão o modo de restauração individual.
  
-   Além disso, os grupos de disponibilidade usam threads não compartilhados, da seguinte maneira:  
  
    -   Cada réplica primária usa 1 thread de captura de log para cada banco de dados primário. Além de isso, ela usa 1 thread de envio de log para cada banco de dados secundário. Os threads de envio de log são liberados após ~15 segundos de inatividade.    
  
    -   Um backup em uma réplica secundária mantém um thread na réplica primária durante a operação de backup.  
  
 Para obter mais informações, confira [Always On – HADRON Learning Series: Worker Pool Usage for HADRON Enabled Databases](https://blogs.msdn.com/b/psssql/archive/2012/05/17/Always%20On-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx) (AlwaysOn – Série de Aprendizado do HADRON: Uso do pool de trabalho para bancos de dados habilitados para HADRON) (blog dos Engenheiros do CSS [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]).  
  
###  <a name="PermissionsSI"></a> Permissões (instância de servidor)  
  
|Tarefa|Permissões necessárias|  
|----------|--------------------------|  
|Criando o ponto de extremidade de espelhamento de banco de dados|Requer permissão CREATE ENDPOINT ou associação na função de servidor fixa **sysadmin** .  Também requer a permissão CONTROL ON ENDPOINT. Para obter mais informações, consulte [Permissões GRANT do ponto de extremidade &#40;Transact-SQL&#41;](../../../t-sql/statements/grant-endpoint-permissions-transact-sql.md).|  
|Habilitando o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]|Exige a associação ao grupo **Administrador** no computador local e o controle total no WSFC.|  
  
###  <a name="RelatedTasksSI"></a> Tarefas relacionadas (instância de servidor)  
  
|Tarefa|Artigo|  
|----------|-----------|  
|Determinando se existe um ponto de extremidade de espelhamento de banco de dados|[sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)|  
|Criando o ponto de extremidade de espelhamento de banco de dados (caso ainda não exista)|[Criar um ponto de extremidade de espelhamento de banco de dados para a Autenticação do Windows &#40;SQL Server&#41;](../../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)<br /><br /> [Usar certificados para um ponto de extremidade de espelhamento de banco de dados &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)<br /><br /> [Criar um ponto de extremidade de espelhamento de banco de dados para grupos de disponibilidade AlwaysOn &#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell.md)|  
|Habilitando grupos de disponibilidade|[Habilitar e desabilitar Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)|  
  
###  <a name="RelatedContentSI"></a> Conteúdo relacionado (instância de servidor)  
  
-   [Always On – HADRON Learning Series: Worker Pool Usage for HADRON Enabled Databases](https://blogs.msdn.com/b/psssql/archive/2012/05/17/Always%20On-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx) (Always On – série de aprendizagem do HADRON: uso do pool de trabalho para bancos de dados habilitados para HADRON)  
  
##  <a name="NetworkConnect"></a> Recomendações de conectividade de rede  
 É altamente recomendável usar os mesmos links de rede para a comunicação entre nós do WSFC e a comunicação entre réplicas de disponibilidade.  Usar links de rede separados pode causar comportamentos inesperados se algum dos links falhar (até mesmo com intermitência).  
  
 Por exemplo, para que um grupo de disponibilidade dê suporte a failover automático, a réplica secundária que é o parceiro de failover automático deverá estar no estado SYNCHRONIZED. Se o link de rede para esta réplica secundária falhar (até mesmo com intermitência), a réplica entrará no estado UNSYNCHRONIZED e não poderá começar a ressincronizar até que o link seja restaurado. Se o WSFC solicitar um failover automático enquanto a réplica secundária estiver não sincronizada, o failover automático não ocorrerá.  
  
##  <a name="ClientConnSupport"></a> Suporte à conectividade de cliente  
 Para obter informações sobre o suporte do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] para a conectividade de cliente, veja [Conectividade de cliente AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md).  
  
##  <a name="FciArLimitations"></a> Pré-requisitos e restrições para usar uma FCI (instância de cluster de failover) do SQL Server para hospedar uma réplica de disponibilidade  
 **Nesta seção:**  
  
-   [Restrições](#RestrictionsFCI)  
  
-   [Lista de verificação: Pré-requisitos](#PrerequisitesFCI)  
  
-   [Tarefas relacionadas](#RelatedTasksFCIs)  
  
-   [Conteúdo relacionado](#RelatedContentFCIs)  
  
###  <a name="RestrictionsFCI"></a> Restrições (FCIs)  
  
> [!NOTE]  
> As Instâncias de Cluster de Failover dão suporte a CSVs (Volumes Compartilhados Clusterizados). Para obter mais informações sobre CSV, consulte [Noções básicas sobre volumes compartilhados clusterizados em um cluster de failover](https://technet.microsoft.com/library/dd759255.aspx).  
  
-   **Os nós de cluster de uma FCI podem hospedar somente uma réplica para um grupo de disponibilidade especificado:**  Se você adicionar uma réplica de disponibilidade a uma FCI, os nós do WSFC que são possíveis proprietários da FCI não poderão hospedar outra réplica para o mesmo grupo de disponibilidade.  Para evitar possíveis conflitos, é recomendável configurar os possíveis proprietários para a instância do cluster de failover. Isso evitará a possibilidade de que um único WSFC tente hospedar duas réplicas de disponibilidade para o mesmo grupo de disponibilidade.
  
     Além disso, cada uma das outras réplicas deve ser hospedada por uma instância do SQL Server 2016 que reside em um nó de cluster diferente no mesmo cluster de failover do Windows Server. A única exceção é que, embora tenha sido migrado para outro cluster, um grupo de disponibilidade pode temporariamente abranger dois clusters. 

  >[!WARNING]
  > Usando o Gerenciador de Cluster de Failover para mover uma *instância de cluster de failover* que hospeda um grupo de disponibilidade para um nó que *já* está hospedando uma réplica do mesmo grupo de disponibilidade pode resultar na perda da réplica do grupo de disponibilidade, impedindo que ele seja colocado online no nó de destino. Um único nó de um cluster de failover não pode hospedar mais de uma réplica do mesmo grupo de disponibilidade. Para obter mais informações sobre como isso ocorre e como recuperar, consulte o blog [Replica unexpectedly dropped in availability group](https://blogs.msdn.microsoft.com/alwaysonpro/2014/02/03/issue-replica-unexpectedly-dropped-in-availability-group/) (Réplica removida inesperadamente no grupo de disponibilidade). 

  
-   **As FCIs não dão suporte ao failover automático por grupos de disponibilidade:**  As FCIs não dão suporte ao failover automático por grupos de disponibilidade e, portanto, qualquer réplica de disponibilidade hospedada por uma FCI pode ser configurada somente para failover manual.  
  
-   **Alterando o nome da rede da FCI:**  Caso você precise alterar o nome da rede de uma FCI que hospeda uma réplica de disponibilidade, precisará remover a réplica do grupo de disponibilidade e, em seguida, adicionar a réplica novamente ao grupo de disponibilidade. Você não pode remover a réplica primária; então, se você estiver renomeando um FCI que está hospedando a réplica primária, realize failover em uma réplica secundária e, depois, remova a réplica primária anterior e adicione-a novamente. Note que a renomeação de um FCI pode alterar a URL de seu ponto de extremidade de espelhamento de banco de dados. Ao adicionar a réplica, especifique a URL do ponto de extremidade atual.  
  
###  <a name="PrerequisitesFCI"></a> Lista de verificação: pré-requisitos (FCIs)  
  
||Pré-requisito|Link|  
|-|------------------|----------|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Verifique se cada instância de cluster de failover do SQL Server (FCI) possui o armazenamento compartilhado exigido pela instalação de instância de cluster de failover do SQL Server padrão.||  
  
###  <a name="RelatedTasksFCIs"></a> Tarefas relacionadas (FCIs)  
  
|Tarefa|Artigo|  
|----------|-----------|  
|Instalando um cluster de failover do SQL Server|[Criar um novo cluster de failover do SQL Server &#40;Instalação&#41;](../../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)|  
|Atualização in-loco de seu cluster de failover do SQL Server existente|[Atualizar uma instância de cluster de failover do SQL Server &#40;instalação&#41;](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md)|  
|Manutenção do seu cluster de failover existente do SQL Server|[Adicionar ou remover nós em um cluster de failover do SQL Server &#40;Instalação&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)|  
  
###  <a name="RelatedContentFCIs"></a> Conteúdo relacionado (FCIs)  
  
-   [Clustering de failover e Grupos de Disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)  
  
-   [Always On Architecture Guide: Building a High Availability and Disaster Recovery Solution by Using Failover Cluster Instances and Availability Groups](https://technet.microsoft.com/library/jj215886.aspx) (Guia de arquitetura do Always On: criando uma solução de alta disponibilidade e de recuperação de desastre usando instâncias de cluster de failover e grupos de disponibilidade)  
  
##  <a name="PrerequisitesForAGs"></a> Pré-requisitos e restrições do grupo de disponibilidade  
 **Nesta seção:**  
  
-   [Restrições](#RestrictionsAG)  
  
-   [Requisitos](#RequirementsAG)  
  
-   [Segurança](#SecurityAG)  
  
-   [Tarefas relacionadas](#RelatedTasksAGs)  
  
###  <a name="RestrictionsAG"></a> Restrições (grupos de disponibilidade)  
  
-   **As réplicas de disponibilidade precisam ser hospedadas por nós diferentes de um WSFC:**  Para um grupo de disponibilidade especificado, as réplicas de disponibilidade precisam ser hospedadas por instâncias de servidor executadas em nós diferentes do mesmo WSFC. A única exceção é que, embora tenha sido migrado para outro cluster, um grupo de disponibilidade pode temporariamente abranger dois clusters.  
  
    > [!NOTE]  
    >  Cada uma das máquinas virtuais no mesmo computador físico pode hospedar uma réplica de disponibilidade para o mesmo grupo de disponibilidade, pois cada uma delas funciona como um computador separado.  
  
-   **Nome exclusivo do grupo de disponibilidade:**  Cada nome de grupo de disponibilidade precisa ser exclusivo no WSFC. O tamanho máximo de um nome de grupo de disponibilidade é 128 caracteres.  
  
-   **Réplicas de disponibilidade:**  Cada grupo de disponibilidade suporta uma réplica primária e até oito réplicas secundárias. Todas as réplicas podem ser executadas no modo de confirmação assíncrona ou até três delas podem ser executadas no modo de confirmação síncrona (uma réplica primária com duas réplicas secundárias síncronas).  
  
-   **Número máximo de grupos de disponibilidade e bancos de dados de disponibilidade por computador:** o número real de bancos de dados e grupos de disponibilidade que você pode colocar em um computador (VM ou físico) depende do hardware e da carga de trabalho, mas nenhum limite é imposto. A Microsoft testou até 10 grupos de disponibilidade e 100 bancos de dados por computador físico, mas isso não é um limite de associação. Dependendo da especificação de hardware no servidor e da carga de trabalho, é possível colocar um número maior de bancos de dados e grupos de disponibilidade em uma instância do SQL Server. Os sinais de sistemas sobrecarregados podem incluir, entre outros, esgotamento de thread de trabalho, tempos de resposta lentos para exibições de sistema dos grupos de disponibilidade AlwaysOn e DMVs e/ou despejos de sistema do dispatcher parados. Não se esqueça de testar completamente seu ambiente com uma carga de trabalho semelhante à de produção para assegurar que ele possa manipular a capacidade da carga de trabalho de pico nos SLAs do seu aplicativo. Ao considerar SLAs, não se esqueça de considerar a carga sob condições de falha, bem como os tempos de resposta esperados.  
  
-   **Não use o Gerenciador de Cluster de Failover para manipular grupos de disponibilidade:**  
  
     Por exemplo:  
  
    -   Não altere nenhuma propriedade de grupo de disponibilidade, como os proprietários possíveis.  
  
    -   Não use o Gerenciador de Cluster de Failover para executar failover de grupos de disponibilidade. Você deve usar [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
###  <a name="RequirementsAG"></a> Pré-requisitos (grupos de disponibilidade)  
 Ao criar ou reconfigurar uma configuração de grupo de disponibilidade, cumpra os requisitos a seguir.  
  
||Pré-requisito|Descrição|  
|-|------------------|-----------------|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Se você pretende usar uma instância de cluster de failover (FCI) do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para hospedar uma réplica de disponibilidade, verifique se compreende as restrições de FCI e se os requisitos de FCI são atendidos.|[Pré-requisitos e restrições do uso de uma FCI (instância de cluster de failover) do SQL Server para hospedar uma réplica de disponibilidade](#FciArLimitations) (anteriormente neste artigo)|  
  
###  <a name="SecurityAG"></a> Segurança (grupos de disponibilidade)  
  
-   A segurança é herdada do WSFC. O clustering de failover do Windows Server fornece dois níveis de segurança do usuário na granularidade de todo o cluster:  
  
    -   Acesso somente leitura  
  
    -   Controle total  
  
         O [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] precisa de controle total; a habilitação do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] em uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] concede a ela controle total do cluster (por meio do SID de Serviço).  
  
         Não é possível adicionar nem remover diretamente a segurança de uma instância de servidor no Gerenciador de Cluster. Para gerenciar sessões de segurança de cluster, use o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager ou o WMI equivalente no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Cada instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve ter permissões para acessar o Registro, o cluster e assim sucessivamente.  
  
-   É recomendável que você use a criptografia para conexões entre instâncias de servidor que hospedam réplicas de disponibilidade do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] .  
  
#### <a name="permissions-availability-groups"></a>Permissões (grupos de disponibilidade)  
  
|Tarefa|Permissões necessárias|  
|----------|--------------------------|  
|Criando um grupo de disponibilidade|Requer a associação na função de servidor fixa **sysadmin** e a permissão de servidor CREATE AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.|  
|Alterando um grupo de disponibilidade|Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.<br /><br /> Além disso, unir um banco de dados a um grupo de disponibilidade exige a associação na função de banco de dados fixa **db_owner** .|  
|Descartando/excluindo um grupo de disponibilidade|Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER. Para descartar um grupo de disponibilidade não hospedado na localização de réplica local, você precisará da permissão CONTROL SERVER ou CONTROL nesse grupo de disponibilidade.|  
  
###  <a name="RelatedTasksAGs"></a> Tarefas relacionadas (grupos de disponibilidade)  
  
|Tarefa|Artigo|  
|----------|-----------|  
|Criando um grupo de disponibilidade|[Usar o grupo de disponibilidade (Novo assistente de grupo de disponibilidade)](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)<br /><br /> [Criar um grupo de disponibilidade (Transact-SQL)](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)<br /><br /> [Criar um Grupo de disponibilidade (SQL Server PowerShell)](../../../database-engine/availability-groups/windows/create-an-availability-group-sql-server-powershell.md)<br /><br /> [Especificar a URL do ponto de extremidade ao adicionar ou modificar uma réplica de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)|  
|Modificando o número de réplicas de disponibilidade|[Adicionar uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)<br /><br /> [Unir uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)<br /><br /> [Remover uma réplica secundária de um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server.md)|  
|Criando um ouvinte de grupo de disponibilidade|[Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)|  
|Descartando um grupo de disponibilidade|[Remover um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md)|  
  
##  <a name="PrerequisitesForDbs"></a> Pré-requisitos e restrições do banco de dados de disponibilidade  
 Para ser qualificado para ser adicionado a um grupo de disponibilidade, um banco de dados precisa atender aos pré-requisitos e restrições a seguir.  
  
 **Nesta seção:**  
  
-   [Requisitos](#RequirementsDb)  
  
-   [Restrições](#RestrictionsDb)  
  
-   [Recomendações para computadores que hospedam réplicas de disponibilidade (sistema Windows)](#TDEdbs)  
  
-   [Permissões](#PermissionsDbs)  
  
-   [Tarefas relacionadas](#RelatedTasksADb)  
  
###  <a name="RequirementsDb"></a> Lista de verificação: requisitos (bancos de dados de disponibilidade)  
 Para estar qualificado para ser adicionado a um grupo de disponibilidade, um banco de dados deve ter as seguintes condições:  
  
||Requisitos|Link|  
|-|------------------|----------|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Ser um banco de dados de usuário. Os bancos de dados do sistema não podem pertencer a um grupo de disponibilidade.||  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Residir na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em que você cria o grupo de disponibilidade e ser acessível à instância de servidor.||  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Ser um banco de dados de leitura/gravação. Os bancos de dados somente leitura não podem ser adicionados a um grupo de disponibilidade.|[sys.databases](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) (**is_read_only** = 0)|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Ser um banco de dados de vários usuários.|[sys.databases](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) (**user_access** = 0)|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Não usar AUTO_CLOSE.|[sys.databases](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) (**is_auto_close_on** = 0)|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Use o modelo de recuperação completa (também conhecido como modo de recuperação completa).|[sys.databases](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) (**recovery_model** = 1)|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Ter pelo menos um backup de banco de dados completo.<br /><br /> Observação: Após a definição de uma banco de dados para um modo de recuperação completa, um backup completo será necessário para iniciar a cadeia de log de recuperação completa.|[Criar um backup completo de banco de dados &#40;SQL Server&#41;](../../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Não pertencer a um grupo de disponibilidade existente.|[sys.databases](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) (**group_database_id** = NULL)|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Não ser configurado para espelhamento de banco de dados.|[sys.database_mirroring](../../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md) (Se o banco de dados não participar do espelhamento, todas as colunas prefixadas com “mirroring_” serão NULL.)|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Antes de adicionar um banco de dados que usa o FILESTREAM a um grupo de disponibilidade, verifique se o FILESTREAM está habilitado em cada instância de servidor que hospeda ou hospedará uma réplica de disponibilidade do grupo de disponibilidade.|[Habilitar e configurar o FILESTREAM](../../../relational-databases/blob/enable-and-configure-filestream.md)|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Antes de adicionar um banco de dados independente a um grupo de disponibilidade, verifique se a opção de servidor **contained database authentication** está definida como **1** em cada instância de servidor que hospeda ou hospedará uma réplica de disponibilidade do grupo de disponibilidade.|[Opção de configuração de servidor contained database authentication](../../../database-engine/configure-windows/contained-database-authentication-server-configuration-option.md)<br /><br /> [Opções de configuração do servidor &#40;SQL Server&#41;](../../../database-engine/configure-windows/server-configuration-options-sql-server.md)|  
  
> [!NOTE]  
>  O [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] funciona com qualquer nível de compatibilidade de banco de dados com suporte.  
  
###  <a name="RestrictionsDb"></a> Restrições (bancos de dados de disponibilidade)  
  
-   Se o caminho do arquivo (incluindo a letra da unidade) de um banco de dados secundário diferir do caminho do banco de dados primário correspondente, as seguintes restrições se aplicarão:  
  
    -   **[!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)]/[!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)]:**  Não há suporte para a opção **Completa** (na página [Selecionar Página Inicial de Sincronização de Dados](../../../database-engine/availability-groups/windows/select-initial-data-synchronization-page-always-on-availability-group-wizards.md)),  
  
    -   **RESTORE WITH MOVE:**  Para criar os bancos de dados secundários, os arquivos de banco de dados precisam ser executados com RESTORE WITH MOVE em cada instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospeda uma réplica secundária.  
  
    -   **Impacto em operações de adição de arquivo:**  Uma operação posterior de adição de arquivo na réplica primária poderá falhar nos bancos de dados secundários. Esta falha pode levar à suspensão de bancos de dados secundários. Isso, por sua vez, leva as réplicas secundárias a entrarem no estado NOT SYNCHRONIZING.  
  
        > [!NOTE]  
        >  Para obter informações sobre como responder a uma operação de adicionar arquivo com falha, veja [Solução de problemas de uma operação de adição de arquivos com falha &#40;Grupos de disponibilidade de AlwaysOn&#41;](../../../database-engine/availability-groups/windows/troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md).  
  
-   Você não pode remover um banco de dados que pertence atualmente a um grupo de disponibilidade.  
  
###  <a name="TDEdbs"></a> Acompanhamento para bancos de dados TDE protegidos  
 Se você usar criptografia de dados transparente (TDE), o certificado ou a chave assimétrica para criação e descriptografia de outras chaves deverá ser igual em todas as instância de servidor que hospedam uma réplica de disponibilidade para o grupo de disponibilidade. Para obter mais informações, veja [Mover um banco de dados protegido por TDE para outro SQL Server](../../../relational-databases/security/encryption/move-a-tde-protected-database-to-another-sql-server.md).  
  
###  <a name="PermissionsDbs"></a> Permissões (bancos de dados de disponibilidade)  
 Requer a permissão ALTER no banco de dados.  
  
###  <a name="RelatedTasksADb"></a> Tarefas relacionadas (bancos de dados de disponibilidade)  
  
|Tarefa|Artigo|  
|----------|-----------|  
|Preparando um banco de dados secundário (manualmente)|[Preparar um banco de dados secundário manualmente para um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)|  
|Unindo um banco de dados secundário ao grupo de disponibilidade (manualmente)|[Unir um banco de dados secundário a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)|  
|Modificando o número de bancos de dados de disponibilidade|[Adicionar um banco de dados a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/availability-group-add-a-database.md)<br /><br /> [Remover um banco de dados secundário de um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-database-from-an-availability-group-sql-server.md)<br /><br /> [Remover um banco de dados primário de um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md)|  
  
##  <a name="RelatedContent"></a> Conteúdo relacionado  
  
-   [Guia de soluções AlwaysOn do Microsoft SQL Server para alta disponibilidade e recuperação de desastre](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   [Blog da equipe do Always On do SQL Server: o blog oficial da equipe do Always On do SQL Server](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
-   [Always On – HADRON Learning Series: Worker Pool Usage for HADRON Enabled Databases](https://blogs.msdn.com/b/psssql/archive/2012/05/17/Always%20On-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx) (Always On – série de aprendizagem do HADRON: uso do pool de trabalho para bancos de dados habilitados para HADRON)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Clustering de failover e Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [Conectividade de cliente AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md)  
  
    
  
--------------------------------------------------  

