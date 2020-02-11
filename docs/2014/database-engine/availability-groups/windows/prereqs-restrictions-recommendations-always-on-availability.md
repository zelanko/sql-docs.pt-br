---
title: Pré-requisitos, restrições e recomendações para Grupos de Disponibilidade AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: b12b9030d27e371e0299e06917464b1467b9b10e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72782959"
---
# <a name="prerequisites-restrictions-and-recommendations-for-alwayson-availability-groups-sql-server"></a>Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn (SQL Server)
  Este tópico descreve considerações sobre a implantação do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], inclusive pré-requisitos, restrições e recomendações para computadores host, clusters WSFC (Windows Server Failover Clustering), instâncias de servidor e grupos de disponibilidade. Para cada um desses componentes, são indicadas considerações sobre segurança e as permissões exigidas, se houver.  
  
> [!IMPORTANT]  
>  Antes de implantar o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], é altamente recomendável que você leia cada seção deste tópico.  
  
 
  
##  <a name="DotNetHotfixes"></a>Hotfixes do .NET que dão suporte ao Grupos de Disponibilidade AlwaysOn  
 Dependendo dos componentes e recursos do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usados com o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], você poderá precisar instalar hotfixes .Net adicionais identificados na tabela seguinte. Os hotfixes podem ser instalados em qualquer ordem.  
  
||Recurso dependente|Hotfix|Link|  
|------|-----------------------|------------|----------|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]|O hotfix para .Net 3.5 SP1 adiciona suporte a recursos do Cliente SQL para AlwaysOn de intenção de Leitura, somente leitura e multisubnetfailover. O hotfix precisa ser instalado em cada servidor de relatório do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] .|KB 2654347: [Hotfix para .Net 3.5 SP1 para adicionar suporte para recursos AlwaysOn](https://go.microsoft.com/fwlink/?LinkId=242896)|  
  
##  <a name="SystemReqsForAOAG"></a>Recomendações e requisitos de sistema do Windows  
  
  
###  <a name="SystemRequirements"></a> Lista de verificação: requisitos (sistema Windows)  
 Para oferecer suporte ao recurso [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] , verifique se cada computador que participará de um ou mais grupos de disponibilidade atende aos seguintes requisitos básicos:  
  
||Requisito|Link|  
|------|-----------------|----------|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Verifique se o sistema não é um controlador de domínio.|Os grupos de disponibilidade não têm suporte em controladores de domínio.|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Verifique se cada computador está executando o Windows Server 2008 (não WOW64) na versão x86, x64 ou posterior.|O WOW64 (Windows de 32 bits no Windows de 64 bits) não oferece suporte ao [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)].|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Verifique se cada computador é um nó em um cluster WSFC (Windows Server Failover Clustering).|[WSFC &#40;Windows Server Failover Clustering&#41; com o SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Verifique se o cluster WSFC contém nós suficientes para oferecer suporte às suas configurações de grupo de disponibilidade.|Um nó WSFC pode hospedar apenas uma réplica de disponibilidade para determinado grupo de disponibilidade. Em um nó WSFC específico, uma ou mais instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] podem hospedar réplicas de disponibilidade para muitos grupos de disponibilidade.<br /><br /> Pergunte aos administradores do banco de dados quantos nós WSFC são necessários para oferecer suporte às réplicas de disponibilidade dos grupos de disponibilidade planejados.<br /><br /> [Visão geral do Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md).|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Verifique se todos os hotfixes do Windows aplicáveis foram instalados em todos os nós do cluster WSFC.|** \* Importante \* \* ** Vários hotfixes são necessários ou recomendados para os nós de um Cluster WSFC no qual [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] o está sendo implantado. Para obter mais informações, consulte [Hotfixes do Windows que dão suporte a grupos de disponibilidade AlwaysOn (Sistema do Windows)](#WinHotfixes), posteriormente nesta seção.|  
  
> [!IMPORTANT]  
>  Verifique também se seu ambiente está corretamente configurado para a conexão a um grupo de disponibilidade. Para obter mais informações, consulte [conectividade de cliente AlwaysOn (SQL Server)](always-on-client-connectivity-sql-server.md).  
  
####  <a name="WinHotfixes"></a>Hotfixes do Windows que dão suporte a Grupos de Disponibilidade AlwaysOn (sistema Windows)  
 Dependendo da sua topologia de cluster, diversos hotfixes adicionais do Windows Server 2008 Service Pack (SP2) ou Windows Server 2008 R2 podem ser aplicáveis para dar suporte ao [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. A tabela a seguir identifica esses hotfixes. Esses hotfixes podem ser instalados em qualquer ordem.  
  
||Aplica-se ao Windows 2008 SP2|Aplica-se ao Windows 2008 R2 SP1|Incluído no Windows 2012|Para dar suporte a...|Hotfix|Link|  
|------|---------------------------------|------------------------------------|------------------------------|-----------------|------------|----------|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Sim|Sim|Sim|**Configurando o quorum ideal de WSFC**|Em cada nó WSFC, verifique se o hotfix descrito no artigo 2494036 da Base de Dados de Conhecimento foi instalado.<br /><br /> Este hotfix oferece suporte à configuração de quorum ideal com destinos de failover não automático. Essa funcionalidade aprimora os clusters multissite, permitindo que você selecione os nós que votam.|KB 2494036:  [Um hotfix está disponível para permitir que você configure um nó de cluster que não tenha votos de quorum no Windows Server 2008 e no Windows Server 2008 R2](https://support.microsoft.com/kb/2494036)<br /><br /> Para obter informações sobre votação de quorum, consulte [Configuração de modos de quorum WSFC e votação &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md)|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Sim|Sim|Sim|**Uso mais eficiente da largura de banda de rede**|Em cada nó WSFC, verifique se o hotfix descrito no artigo 2616514 da Base de Dados de Conhecimento foi instalado.<br /><br /> Sem este hotfix, o serviço de Cluster envia notificações do Registro desnecessárias entre nós de cluster. Este comportamento limite a largura de banda de rede, que é um problema sério para [!INCLUDE[ssHADRc](../../../includes/sshadrc-md.md)].|KB 2616514:  [O serviço de cluster envia notificações de alteração da chave do Registro desnecessárias entre nós de cluster no Windows Server 2008 ou no Windows Server 2008 R2](https://support.microsoft.com/kb/2616514)|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")||Sim|Não aplicável|**O teste de armazenamento de VPD em discos que não estão disponíveis a todos os nós WSFC**|Se um nó WSFC estiver executando o Windows Server 2008 R2 Service Pack 1 (SP1) e o teste de armazenamento Validar VPD (Vital Product Data) do dispositivo SCSI falhar depois de execução incorreta em discos online e não disponíveis a todos os nós no cluster WSFC, instale o hotfix descrito no artigo 2531907 da Base de Dados de Conhecimento.<br /><br /> Este hotfix elimina avisos incorretos ou erros no relatório de validação quando há discos online.|KB 2531907: [Validar VPD (Vital Product Data) do dispositivo SCSI falha depois que você instala o Windows Server 2008 R2 SP1](https://support.microsoft.com/kb/2531907)|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")||Sim|Sim|**Failover mais rápido para réplicas locais**|Se um nó WSFC estiver sendo executado no Windows Server 2008 R2 Service Pack 1 (SP1), verifique se o hotfix descrito no artigo 2687741 da Base de Dados de Conhecimento foi instalado.<br /><br /> Este hotfix melhora o desempenho do failover do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] para réplicas locais.|KB 2687741:  [Um hotfix que melhora o desempenho do recurso "Grupo de disponibilidade AlwaysOn" no SQL Server 2012 está disponível para o Windows Server 2008 R2](https://support.microsoft.com/KB/2687741)|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Sim|Sim|Sim|**Armazenamento assimétrico-para FCIs (instâncias de cluster de failover)**|Se alguma FCI (Instância de Cluster de Failover) estiver habilitada para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], instale o hotfix 976097 do Windows Server 2008.<br /><br /> Esse hotfix habilita o snap-in MMC (console de gerenciamento Microsoft) de gerenciamento de cluster de failover para dar suporte a discos compartilhados de armazenamento assimétrico que estão disponíveis somente em alguns dos nós WSFC.|KB 976097: [hotfix para adicionar suporte para armazenamentos assimétricos no snap-in MMC de Gerenciamento de Cluster de Failover para um cluster de failover que está executando o Windows Server 2008 ou o Windows Server 2008 R2](https://support.microsoft.com/kb/976097)<br /><br /> [Guia da arquitetura do AlwaysOn: Criando uma solução de alta disponibilidade e recuperação de desastres usando instâncias de cluster de failover e grupos de disponibilidade](https://technet.microsoft.com/library/jj215886.aspx)|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Sim|Sim|Não aplicável|**IPsec (Internet Protocol Security)**|Se seu ambiente usar conexões IPsec, você poderá experimentar um longo atraso (cerca de dois ou três minutos) quando o computador cliente restabelece a conexão IPsec com um nome de rede virtual (e, neste contexto, para conectar-se ao ouvinte do grupo de disponibilidade). Se você utilizar conexões IPsec, será recomendável rever os cenários específicos detalhados no seguinte artigo da Base de Dados de Conhecimento (KB 980915).|KB 980915:  [Ocorre um atraso muito longo ao reconectar uma conexão IPSec de um computador que está executando o Windows Server 2003, o Windows Vista, o Windows Server 2008, o Windows 7 ou o Windows Server 2008 R2](https://support.microsoft.com/kb/980915)|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Sim|Sim|Sim|**Protocolo**|Se você utilizar conexões IPv6, será recomendável rever os cenários específicos detalhados no artigo 2578103 ou 2578113 da Base de Dados de Conhecimento, dependendo do sistema operacional do seu Windows Server.<br /><br /> Se sua topologia do Windows Server usar o IP versão 6 (IPv6), o serviço de Cluster WSFC precisará de cerca de 30 segundos para realizar o failover do endereço IP IPv6. Isso faz com que os clientes esperem cerca de 30 segundos para reconectar-se com o endereço IP IPv6.|KB 2578103 (Windows Server 2008): [o serviço de cluster leva aproximadamente 30 segundos para fazer failover de endereços IP IPv6 no Windows Server 2008](https://support.microsoft.com/kb/2578103)<br /><br /> KB 2578113 (Windows Server 2008 R2): **Windows Server 2008 R2:** [O serviço de cluster leva aproximadamente 30 segundos para fazer failover de endereços IP IPv6 no Windows Server 2008 R2](https://support.microsoft.com/kb/2578113)|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Sim|Sim|Sim|**Nenhum roteador entre o cluster e o servidor de aplicativo**|Se não existir nenhum roteador entre o cluster de failover e o servidor de aplicativos, o serviço de cluster lentamente fará o failover dos recursos relacionados à rede. Isso atrasa as reconexões do cliente depois que um grupo de disponibilidade faz failover. Na ausência de um roteador, será recomendável rever os cenários específicos detalhados no seguinte artigo da Base de Dados de Conhecimento 2582281 e instalar o hotfix, se isso for aplicável a seu ambiente:|KB 2582281:  [Operação de failover lenta se não existir nenhum roteador entre o cluster e um servidor de aplicativos](https://support.microsoft.com/kb/2582281)|  
  
###  <a name="ComputerRecommendations"></a> Recomendações para computadores que hospedam réplicas de disponibilidade (sistema Windows)  
  
-   **Sistemas comparáveis:**  Para um grupo de disponibilidade especificado, todas as réplicas de disponibilidade devem ser executadas em sistemas comparáveis que possam manipular cargas de trabalho idênticas.  
  
-   **Adaptadores de rede dedicados:**  Para obter um melhor desempenho, use um adaptador de rede dedicado (placa de interface de rede) para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)].  
  
-   **Espaço em disco suficiente:**  Cada computador no qual uma instância de servidor hospeda uma réplica de disponibilidade precisa ter espaço em disco suficiente para todos os bancos de dados do grupo de disponibilidade. Lembre-se de que à medida que os bancos de dados primários crescem, seus bancos de dados secundários correspondentes crescem na mesma proporção.  
  
###  <a name="PermissionsWindows"></a> Permissões (sistema Windows)  
 Para administrar um cluster WSFC, o usuário deve ser um administrador do sistema em todo nó de cluster.  
  
 Para obter mais informações sobre a conta usada para administrar o cluster, confira [Apêndice A: Requisitos do cluster de failover](https://technet.microsoft.com/library/dd197454\(WS.10\).aspx).  
  
###  <a name="RelatedTasksWindows"></a> Tarefas relacionadas (sistema Windows)  
  
|Tarefa|Link|  
|----------|----------|  
|Defina o valor de HostRecordTTL.|[Alterar o HostRecordTTL (usando o Windows PowerShell)](#ChangeHostRecordTTLps)|  
  
####  <a name="ChangeHostRecordTTLps"></a> Alterar o HostRecordTTL (usando o Windows PowerShell)  
  
1.  Abra a janela do PowerShell por meio da opção **Executar como Administrador**.  
  
2.  Importe o módulo FailoverClusters.  
  
3.  Use o cmdlet `Get-ClusterResource` para localizar o recurso Nome da Rede e use o cmdlet `Set-ClusterParameter` para definir o valor de `HostRecordTTL`, como segue:  
  
     Get-ClusterResource " *\<NetworkResourceName>* " | Set-ClusterParameter HostRecordTTL *\<TimeInSeconds>*  
  
     O exemplo do PowerShell a seguir define o HostRecordTTL como 300 segundos para um recurso Nome da Rede nomeado “`SQL Network Name (SQL35)`”.  
  
    ```powershell
    Import-Module FailoverClusters  
  
    $nameResource = "SQL Network Name (SQL35)"  
    Get-ClusterResource $nameResource | Set-ClusterParameter ClusterParameter HostRecordTTL 300  
    ```  
  
    > [!TIP]  
    >  Sempre que você abrir uma nova janela do PowerShell, deverá importar o módulo `FailoverClusters`.  
  
##### <a name="related-content-powershell"></a>Conteúdo relacionado (PowerShell)  
  
-   [Clustering e alta disponibilidade](https://blogs.msdn.com/b/clustering/archive/2009/05/23/9636665.aspx) (Blog da equipe de Clustering de Failover e Balanceamento de Carga de Rede)  
  
-   [Guia de Introdução ao Windows PowerShell em um cluster de failover](https://technet.microsoft.com/library/ee619762\(WS.10\).aspx)  
  
-   [Comandos de recursos de cluster e cmdlets equivalentes no Windows PowerShell](https://msdn.microsoft.com/library/ee619744.aspx#BKMK_resource)  
  
###  <a name="RelatedContentWS"></a> Conteúdo relacionado (Windows System)  
  
-   [Definir configurações DNS em um cluster de failover multissite](https://technet.microsoft.com/library/dd197562\(WS.10\).aspx)  
  
-   [Registro de DNS com recurso de nome de rede](https://blogs.msdn.com/b/clustering/archive/2009/07/17/9836756.aspx)  
  
-   [Clustering de failover de vários locais do Windows 2008 R2](https://kiruba4u.blogspot.com/2012/03/failover-clustering-in-windows-server.html)  
  
##  <a name="ServerInstance"></a> Pré-requisitos e restrições da instância de SQL Server  
 Cada grupo de disponibilidade requer um conjunto de parceiros de failover, conhecidos como *réplicas de disponibilidade*, que são hospedados por instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Uma instância específica pode ser uma *instância autônomo* ou uma FCI (*instância de cluster de failover*) do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 
  
###  <a name="PrerequisitesSI"></a> Lista de verificação: pré-requisitos (instância de servidor)  
  
||Pré-requisito|Links|  
|-|------------------|-----------|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|O computador host deve ser um nó WSFC (Windows Server Failover Clustering). As instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospedam as réplicas de disponibilidade para um determinado grupo de disponibilidade residem em nós separados de um único cluster do WSFC. A única exceção é que, embora tenha sido migrado para outro cluster WSFC, um grupo de disponibilidade pode temporariamente abranger dois clusters.|[WSFC &#40;Windows Server Failover Clustering&#41; com o SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)<br /><br /> [Clustering de failover e Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](failover-clustering-and-always-on-availability-groups-sql-server.md)|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Se você desejar um grupo de disponibilidade para funcionar com o Kerberos:<br /><br /> Todas as instâncias de servidor que hospedam uma réplica de disponibilidade para o grupo de disponibilidade deve usar a mesma conta de serviço do SQL Server.<br /><br /> O administrador de domínio precisa registrar um Nome de entidade de serviço (SPN) manualmente com Active Directory na conta de serviço do SQL Server para o nome de rede virtual (VNN) do ouvinte de grupo de disponibilidade. Se o SPN for registrado em uma conta diferente da conta de serviço do SQL Server, a autenticação falhará.<br /><br /> **\*\* Importante \*\*** Se você alterar a conta de serviço do SQL Server, o administrador de domínio precisará registrar de novo o SPN manualmente.|[Registrar um nome de entidade de serviço para conexões de Kerberos](../../configure-windows/register-a-service-principal-name-for-kerberos-connections.md)<br /><br /> **Breve explicação:**<br /><br /> O Kerberos e os SPNs impõem a autenticação mútua. O SPN é mapeado para a conta do Windows que inicia os serviços do SQL Server. Se o SPN não estiver registrado corretamente ou se ele falhar, a camada de segurança do Windows não poderá determinar a conta associada ao SPN e a autenticação Kerberos não será utilizada.<br /><br /> Observação: O NTLM não tem este requisito.|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Se você pretende usar uma instância de cluster de failover (FCI) do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para hospedar uma réplica de disponibilidade, verifique se compreende as restrições de FCI e se os requisitos de FCI são atendidos.|[Pré-requisitos e requisitos sobre o uso de uma SQL Server FCI (instância de cluster de failover) para hospedar uma réplica de disponibilidade](#FciArLimitations) (mais adiante neste tópico)|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Cada instância de servidor deve estar executando a Enterprise Edition do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].|[Recursos compatíveis com as edições do SQL Server 2014](../../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Todas as instâncias de servidor que hospedam réplicas de disponibilidade para um grupo de disponibilidade devem usar a mesma ordenação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|[Definir ou alterar a ordenação do servidor](../../../relational-databases/collations/set-or-change-the-server-collation.md)|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Habilite o recurso [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] em cada instância de servidor que hospedará uma réplica de disponibilidade para qualquer grupo de disponibilidade. Em determinado computador, você pode habilitar quantas instâncias de servidor desejar para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] , desde que tenham suporte da instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|[Habilitar e desabilitar grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)<br /><br /> ** \* Importante \* \* ** Se você excluir e recriar um Cluster WSFC, será necessário desabilitar e reabilitar o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] recurso em cada instância de servidor habilitada para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] o no Cluster WSFC original.|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Cada instância de servidor exige um ponto de extremidade de espelhamento de banco de dados. Note que esse ponto de extremidade é compartilhado por todas as réplicas de disponibilidade e parceiros de espelhamento de banco de dados e testemunhas na instância de servidor.<br /><br /> Se uma instância de servidor selecionada para hospedar uma réplica de disponibilidade estiver sendo executada em uma conta de usuário de domínio e ainda não tiver um ponto de extremidade de espelhamento de banco de dados, o [Assistente de Novo Grupo de Disponibilidade](use-the-availability-group-wizard-sql-server-management-studio.md) (ou o [Assistente para Adicionar Réplica ao Grupo de Disponibilidade](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)) poderá criar o ponto de extremidade e conceder a permissão CONNECT à conta de serviço da instância de servidor. No entanto, se o serviço [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] estiver sendo executado como uma conta interna, como Sistema Local, Serviço Local ou Serviço de Rede, ou como uma conta que não pertença a um domínio, você deverá usar certificados para autenticação de ponto de extremidade, e o assistente não poderá criar um ponto de extremidade de espelhamento de banco de dados na instância de servidor. Nesse caso, é recomendável criar manualmente os pontos de extremidade de espelhamento de banco de dados antes de iniciar o assistente.<br /><br /> **\*\* Observação de Segurança \*\*** A segurança de transporte para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] é a mesma do espelhamento de banco de dados.|[O ponto de extremidade de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md)<br /><br /> [Segurança de transporte para espelhamento de banco de dados e Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-mirroring/transport-security-database-mirroring-always-on-availability.md)|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Se algum banco de dados que utilize o FILESTREAM for adicionado a um grupo de disponibilidade, verifique se o FILESTREAM está habilitado em cada instância de servidor que hospedará uma réplica de disponibilidade do grupo de disponibilidade.|[Habilitar e configurar o FILESTREAM](../../../relational-databases/blob/enable-and-configure-filestream.md)|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Se algum banco de dados independente for adicionado a um grupo de disponibilidade, verifique se a opção de servidor `contained database authentication` está definida como `1` em cada instância de servidor que hospedará uma réplica de disponibilidade do grupo de disponibilidade.|[Opção de configuração do servidor contained database authentication](../../configure-windows/contained-database-authentication-server-configuration-option.md)<br /><br /> [Opções de configuração do servidor &#40;SQL Server&#41;](../../configure-windows/server-configuration-options-sql-server.md)|  
  
###  <a name="ThreadUsage"></a> Uso de thread por grupos de disponibilidade  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] tem os seguintes requisitos para threads de trabalho:  
  
-   Em uma instância ociosa do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] não usa nenhum thread.  
  
-   O número máximo de threads usados por grupos de disponibilidade é a configuração definida para o número máximo de threads de servidor ('`max worker threads`') menos 40.  
  
-   As réplicas de disponibilidade hospedadas em uma instância de servidor específica compartilham um único pool de threads.  
  
     Os threads são compartilhados sob demanda, da seguinte maneira:  
  
    -   Normalmente, há 3 a 10 threads compartilhados, mas esse número pode aumentar dependendo da carga de trabalho da réplica primária.  
  
    -   Se um determinado thread ficar ocioso por um tempo, ele será liberado novamente no pool de threads geral do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Normalmente, um thread inativa é liberado após ~15 segundos de inatividade. No entanto, dependendo da última atividade, um thread ocioso pode ser retido por mais tempo.  
  
-   Além disso, os grupos de disponibilidade usam threads não compartilhados, da seguinte maneira:  
  
    -   Cada réplica primária usa 1 thread de captura de log para cada banco de dados primário. Além de isso, ela usa 1 thread de envio de log para cada banco de dados secundário. Os threads de envio de log são liberados após ~15 segundos de inatividade.  
  
    -   Cada réplica secundária usa 1 thread de restauração para cada banco de dados secundário. Os threads de restauração são liberados após ~15 segundos de inatividade.  
  
    -   Um backup em uma réplica secundária mantém um thread na réplica primária durante a operação de backup.  
  
 Para obter mais informações, consulte [AlwaysON - HADRON Learning Series: Worker Pool Usage for HADRON Enabled Databases](https://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx) (Série de aprendizado do AlwaysON – HADRON: uso do pool de trabalho para bancos de dados habilitados para HADRON) (um blog dos engenheiros do CSS [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]).  
  
###  <a name="PermissionsSI"></a> Permissões (instância de servidor)  
  
|Tarefa|Permissões necessárias|  
|----------|--------------------------|  
|Criando o ponto de extremidade de espelhamento de banco de dados|Requer permissão CREATE ENDPOINT ou associação na função de servidor fixa **sysadmin** .  Também requer a permissão CONTROL ON ENDPOINT. Para obter mais informações, consulte [Permissões GRANT do ponto de extremidade &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-endpoint-permissions-transact-sql).|  
|Habilitando o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]|Requer a associação ao grupo **Administrador** no computador local e o controle total no cluster WSFC.|  
  
###  <a name="RelatedTasksSI"></a> Tarefas relacionadas (instância de servidor)  
  
|Tarefa|Tópico|  
|----------|-----------|  
|Determinando se existe um ponto de extremidade de espelhamento de banco de dados|[sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)|  
|Criando o ponto de extremidade de espelhamento de banco de dados (caso ainda não exista)|[Criar um ponto de extremidade de espelhamento de banco de dados para a Autenticação do Windows &#40;SQL Server&#41;](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)<br /><br /> [Usar certificados para um ponto de extremidade de espelhamento de banco de dados &#40;Transact-SQL&#41;](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)<br /><br /> [Criar um ponto de extremidade de espelhamento de banco de dados para Grupos de Disponibilidade AlwaysOn &#40;SQL Server PowerShell&#41;](database-mirroring-always-on-availability-groups-powershell.md)|  
|Habilitando grupos de disponibilidade AlwaysOn|[Habilitar e desabilitar grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)|  
  
###  <a name="RelatedContentSI"></a> Conteúdo relacionado (instância de servidor)  
  
-   [Série de aprendizado do AlwaysON - HADRON: uso de trabalho do pool para bancos de dados habilitados do HADRON](https://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
##  <a name="NetworkConnect"></a> Recomendações de conectividade de rede  
 Nós recomendamos fortemente que você use os mesmos links de rede para comunicações entre os membros de cluster do WSFC e as comunicações entre réplicas de disponibilidade.  Usar links de rede separados pode causar comportamentos inesperados se algum dos links falhar (até mesmo com intermitência).  
  
 Por exemplo, para que um grupo de disponibilidade dê suporte a failover automático, a réplica secundária que é o parceiro de failover automático deverá estar no estado SYNCHRONIZED. Se o link de rede para esta réplica secundária falhar (até mesmo com intermitência), a réplica entrará no estado UNSYNCHRONIZED e não poderá começar a ressincronizar até que o link seja restaurado. Se o cluster do WSFC solicitar um failover automático enquanto a réplica secundária estiver não sincronizada, o failover automático não ocorrerá.  
  
##  <a name="ClientConnSupport"></a> Suporte à conectividade de cliente  
 Para obter informações [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] sobre o suporte para conectividade de cliente, consulte [conectividade de cliente AlwaysOn (SQL Server)](always-on-client-connectivity-sql-server.md).  
  
##  <a name="FciArLimitations"></a> Pré-requisitos e restrições para usar uma FCI (instância de cluster de failover) do SQL Server para hospedar uma réplica de disponibilidade  
 
  
###  <a name="RestrictionsFCI"></a> Restrições (FCIs)  
  
> [!NOTE]  
>  No [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)], as instâncias de cluster de failover do AlwaysOn dão suporte a CSV (volumes compartilhados clusterizados) no [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] e no [!INCLUDE[win8srv](../../../includes/win8srv-md.md)]. Para obter mais informações sobre CSV, consulte [Noções básicas sobre volumes compartilhados clusterizados em um cluster de failover](https://technet.microsoft.com/library/dd759255.aspx).  
  
-   **Os nós de cluster de um FCI podem hospedar apenas uma réplica para um determinado grupo de disponibilidade:**  Se você adicionar uma réplica de disponibilidade em um FCI, os nós de Cluster WSFC que são possíveis proprietários de FCI não poderão hospedar outra réplica para o mesmo grupo de disponibilidade.  
  
     Além disso, cada uma das outras réplicas deve ser hospedada por uma instância do SQL Server 2012 que reside em um nó diferente do WSFC no mesmo cluster do WSFC. A única exceção é que, embora tenha sido migrado para outro cluster WSFC, um grupo de disponibilidade pode temporariamente abranger dois clusters.  
  
-   **As FCIs não dão suporte ao failover automático por grupos de disponibilidade:**  As FCIs não dão suporte ao failover automático por grupos de disponibilidade e, portanto, qualquer réplica de disponibilidade hospedada por uma FCI pode ser configurada somente para failover manual.  
  
-   **Alterando o nome da rede da FCI:**  Caso você precise alterar o nome da rede de uma FCI que hospeda uma réplica de disponibilidade, precisará remover a réplica do grupo de disponibilidade e, em seguida, adicionar a réplica novamente ao grupo de disponibilidade. Você não pode remover a réplica primária; então, se você estiver renomeando um FCI que está hospedando a réplica primária, realize failover em uma réplica secundária e, depois, remova a réplica primária anterior e adicione-a novamente. Note que a renomeação de um FCI pode alterar a URL de seu ponto de extremidade de espelhamento de banco de dados. Ao adicionar a réplica, especifique a URL do ponto de extremidade atual.  
  
###  <a name="PrerequisitesFCI"></a> Lista de verificação: pré-requisitos (FCIs)  
  
||Pré-requisito|Link|  
|-|------------------|----------|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Antes de usar um FCI para hospedar uma réplica de disponibilidade, verifique se o administrador do sistema instalou o hotfix do Windows Server 2008 descrito no artigo KB 976097 da Base de Dados de Conhecimento. Esse hotfix habilita o snap-in MMC (console de gerenciamento Microsoft) de gerenciamento de cluster de failover para dar suporte a discos compartilhados de armazenamento assimétrico que estão disponíveis somente em alguns dos nós WSFC.|KB 976097: [hotfix para adicionar suporte para armazenamentos assimétricos no snap-in MMC de Gerenciamento de Cluster de Failover para um cluster de failover que está executando o Windows Server 2008 ou o Windows Server 2008 R2](https://support.microsoft.com/kb/976097)|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Verifique se cada instância de cluster de failover do SQL Server (FCI) possui o armazenamento compartilhado exigido pela instalação de instância de cluster de failover do SQL Server padrão.||  
  
###  <a name="RelatedTasksFCIs"></a> Tarefas relacionadas (FCIs)  
  
|Tarefa|Tópico|  
|----------|-----------|  
|Instalando um cluster de failover do SQL Server|[Criar um novo cluster de failover do SQL Server &#40;Instalação&#41;](../../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)|  
|Atualização in-loco de seu cluster de failover do SQL Server existente|[Atualizar uma instância de cluster de failover do SQL Server &#40;instalação&#41;](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md)|  
|Manutenção do seu cluster de failover existente do SQL Server|[Adicionar ou remover nós em um cluster de failover do SQL Server &#40;Instalação&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)|  
  
###  <a name="RelatedContentFCIs"></a> Conteúdo relacionado (FCIs)  
  
-   [Clustering de failover e Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](failover-clustering-and-always-on-availability-groups-sql-server.md)  
  
-   [Guia da arquitetura do AlwaysOn: Criando uma solução de alta disponibilidade e recuperação de desastres usando instâncias de cluster de failover e grupos de disponibilidade](https://technet.microsoft.com/library/jj215886.aspx)  
  
##  <a name="PrerequisitesForAGs"></a> Pré-requisitos e restrições do grupo de disponibilidade  

  
###  <a name="RestrictionsAG"></a> Restrições (grupos de disponibilidade)  
  
-   As **réplicas de disponibilidade devem ser hospedadas por diferentes nós de um Cluster WSFC:**  Para um determinado grupo de disponibilidade, as réplicas de disponibilidade devem ser hospedadas por instâncias de servidor em execução em nós diferentes do mesmo Cluster WSFC. A única exceção é que, embora tenha sido migrado para outro cluster WSFC, um grupo de disponibilidade pode temporariamente abranger dois clusters.  
  
    > [!NOTE]  
    >  Cada uma das máquinas virtuais no mesmo computador físico pode hospedar uma réplica de disponibilidade para o mesmo grupo de disponibilidade, pois cada uma delas funciona como um computador separado.  
  
-   **Nome do grupo de disponibilidade exclusivo:**  Cada nome de grupo de disponibilidade deve ser exclusivo no Cluster WSFC. O tamanho máximo de um nome de grupo de disponibilidade é 128 caracteres.  
  
-   **Réplicas de disponibilidade:**  Cada grupo de disponibilidade suporta uma réplica primária e até oito réplicas secundárias. Todas as réplicas podem ser executadas no modo de confirmação assíncrona ou até três delas podem ser executadas no modo de confirmação síncrona (uma réplica primária com duas réplicas secundárias síncronas).  
  
-   **Número máximo de grupos de disponibilidade e bancos de dados de disponibilidade por computador:** o número real de bancos de dados e grupos de disponibilidade que você pode colocar em um computador (VM ou físico) depende do hardware e da carga de trabalho, mas nenhum limite é imposto. A Microsoft testou amplamente 10 grupos de disponibilidade e 100 bancos de dados por computador físico. Os sinais de sistemas sobrecarregados podem incluir, sem limitação, esgotamento de thread de trabalho, tempos de resposta lentos para exibições de sistema AlwaysOn e DMVs e/ou despejos de sistema do dispatcher parados. Não se esqueça de testar completamente seu ambiente com uma carga de trabalho semelhante à de produção para assegurar que ele possa manipular a capacidade da carga de trabalho de pico nos SLAs do seu aplicativo. Ao considerar SLAs, não se esqueça de considerar a carga sob condições de falha, bem como os tempos de resposta esperados.  
  
-   **Não use o Gerenciador de Cluster de Failover para manipular grupos de disponibilidade:**  
  
     Por exemplo:  
  
    -   Não altere nenhuma propriedade de grupo de disponibilidade, como os proprietários possíveis.  
  
    -   Não use o Gerenciador de Cluster de Failover para executar failover de grupos de disponibilidade. Você deve usar [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
###  <a name="RequirementsAG"></a> Pré-requisitos (grupos de disponibilidade)  
 Ao criar ou reconfigurar uma configuração de grupo de disponibilidade, cumpra os requisitos a seguir.  
  
||Pré-requisito|DESCRIÇÃO|  
|-|------------------|-----------------|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Se você pretende usar uma instância de cluster de failover (FCI) do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para hospedar uma réplica de disponibilidade, verifique se compreende as restrições de FCI e se os requisitos de FCI são atendidos.|[Pré-requisitos e restrições para usar uma SQL Server FCI (instância de cluster de failover) para hospedar uma réplica de disponibilidade](#FciArLimitations) (anteriormente neste tópico)|  
  
###  <a name="SecurityAG"></a> Segurança (grupos de disponibilidade)  
  
-   A segurança é herdada do cluster WSFC (Windows Server Failover Clustering). O WSFC fornece dois níveis de segurança de usuário na granularidade de APIs inteiras de cluster WSFC:  
  
    -   Acesso somente leitura  
  
    -   Controle total  
  
         
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] precisa de controle total; a habilitação do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] em uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] concede controle total do cluster WSFC (por SID de serviço).  
  
         Você não pode adicionar ou remover diretamente a segurança de uma instância de servidor no Gerenciador de Cluster de Failover WSFC. Para gerenciar sessões de segurança WSFC, use o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Gerenciador de Configuração ou o equivalente WMI do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Cada instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve ter permissões para acessar o Registro, o cluster e assim por diante.  
  
-   É recomendável que você use a criptografia para conexões entre instâncias de servidor que hospedam réplicas de disponibilidade do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] .  
  
#### <a name="permissions-availability-groups"></a>Permissões (grupos de disponibilidade)  
  
|Tarefa|Permissões necessárias|  
|----------|--------------------------|  
|Criando um grupo de disponibilidade|Requer a associação na função de servidor fixa **sysadmin** e a permissão de servidor CREATE AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.|  
|Alterando um grupo de disponibilidade|Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.<br /><br /> Além disso, unir um banco de dados a um grupo de disponibilidade exige a associação na função de banco de dados fixa **db_owner** .|  
|Descartando/excluindo um grupo de disponibilidade|Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER. Para descartar um grupo de disponibilidade não hospedado na localização de réplica local, você precisará da permissão CONTROL SERVER ou CONTROL nesse grupo de disponibilidade.|  
  
###  <a name="RelatedTasksAGs"></a> Tarefas relacionadas (grupos de disponibilidade)  
  
|Tarefa|Tópico|  
|----------|-----------|  
|Criando um grupo de disponibilidade|[Usar o grupo de disponibilidade (Novo assistente de grupo de disponibilidade)](use-the-availability-group-wizard-sql-server-management-studio.md)<br /><br /> [Criar um grupo de disponibilidade (Transact-SQL)](create-an-availability-group-transact-sql.md)<br /><br /> [Criar um Grupo de disponibilidade (SQL Server PowerShell)](../../../powershell/sql-server-powershell.md)<br /><br /> [Especificar a URL do ponto de extremidade ao adicionar ou modificar uma réplica de disponibilidade &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)|  
|Modificando o número de réplicas de disponibilidade|[Adicionar uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)<br /><br /> [Unir uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)<br /><br /> [Remover uma réplica secundária de um grupo de disponibilidade &#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md)|  
|Criando um ouvinte de grupo de disponibilidade|[Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)|  
|Descartando um grupo de disponibilidade|[Remover um grupo de disponibilidade &#40;SQL Server&#41;](remove-an-availability-group-sql-server.md)|  
  
##  <a name="PrerequisitesForDbs"></a> Pré-requisitos e restrições do banco de dados de disponibilidade  
 Para ser qualificado para ser adicionado a um grupo de disponibilidade, um banco de dados precisa atender aos pré-requisitos e restrições a seguir.  
  
 
  
###  <a name="RequirementsDb"></a> Lista de verificação: requisitos (bancos de dados de disponibilidade)  
 Para estar qualificado para ser adicionado a um grupo de disponibilidade, um banco de dados deve ter as seguintes condições:  
  
||Requisitos|Link|  
|-|------------------|----------|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Ser um banco de dados de usuário. Os bancos de dados do sistema não podem pertencer a um grupo de disponibilidade.||  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Residir na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em que você cria o grupo de disponibilidade e ser acessível à instância de servidor.||  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Ser um banco de dados de leitura/gravação. Os bancos de dados somente leitura não podem ser adicionados a um grupo de disponibilidade.|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**is_read_only** = 0)|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Ser um banco de dados de vários usuários.|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**user_access** = 0)|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Não usar AUTO_CLOSE.|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**is_auto_close_on** = 0)|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Use o modelo de recuperação completa (também conhecido como modo de recuperação completa).|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**recovery_model** = 1)|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Ter pelo menos um backup de banco de dados completo.<br /><br /> Observação: Após a definição de uma banco de dados para um modo de recuperação completa, um backup completo será necessário para iniciar a cadeia de log de recuperação completa.|[Criar um backup completo de banco de dados &#40;SQL Server&#41;](../../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Não pertencer a um grupo de disponibilidade existente.|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**group_database_id** = NULL)|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Não ser configurado para espelhamento de banco de dados.|[sys.database_mirroring](/sql/relational-databases/system-catalog-views/sys-database-mirroring-transact-sql) (Se o banco de dados não participar do espelhamento, todas as colunas prefixadas com “mirroring_” serão NULL.)|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Antes de adicionar um banco de dados que usa o FILESTREAM a um grupo de disponibilidade, verifique se o FILESTREAM está habilitado em cada instância de servidor que hospeda ou hospedará uma réplica de disponibilidade do grupo de disponibilidade.|[Habilitar e configurar o FILESTREAM](../../../relational-databases/blob/enable-and-configure-filestream.md)|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Caixa de seleção")|Antes de adicionar um banco de dados independente a um grupo de disponibilidade, verifique se a opção de servidor `contained database authentication` está definida como `1` em cada instância de servidor que hospeda ou hospedará uma réplica de disponibilidade do grupo de disponibilidade.|[Opção de configuração do servidor contained database authentication](../../configure-windows/contained-database-authentication-server-configuration-option.md)<br /><br /> [Opções de configuração do servidor &#40;SQL Server&#41;](../../configure-windows/server-configuration-options-sql-server.md)|  
  
> [!NOTE]  
>  O [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] funciona com qualquer nível de compatibilidade de banco de dados com suporte.  
  
###  <a name="RestrictionsDb"></a> Restrições (bancos de dados de disponibilidade)  
  
-   Se o caminho do arquivo (incluindo a letra da unidade) de um banco de dados secundário diferir do caminho do banco de dados primário correspondente, as seguintes restrições se aplicarão:  
  
    -   **[!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)]/[!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)]:**  Não há suporte para a opção **Completa** (na página [Selecionar Página Inicial de Sincronização de Dados](select-initial-data-synchronization-page-always-on-availability-group-wizards.md)),  
  
    -   **RESTORE WITH MOVE:**  Para criar os bancos de dados secundários, os arquivos de banco de dados precisam ser executados com RESTORE WITH MOVE em cada instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospeda uma réplica secundária.  
  
    -   **Impacto em operações de adição de arquivo:**  Uma operação posterior de adição de arquivo na réplica primária poderá falhar nos bancos de dados secundários. Esta falha pode levar à suspensão de bancos de dados secundários. Isso, por sua vez, leva as réplicas secundárias a entrarem no estado NOT SYNCHRONIZING.  
  
        > [!NOTE]  
        >  Para obter informações sobre como responder a uma operação de adicionar arquivo com falha, consulte [Solução de problemas de uma operação de adição de arquivos com falha &#40;Grupos de disponibilidade AlwaysOn&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md).  
  
-   Você não pode remover um banco de dados que pertence atualmente a um grupo de disponibilidade.  
  
###  <a name="TDEdbs"></a> Acompanhamento para bancos de dados TDE protegidos  
 Se você usar criptografia de dados transparente (TDE), o certificado ou a chave assimétrica para criação e descriptografia de outras chaves deverá ser igual em todas as instância de servidor que hospedam uma réplica de disponibilidade para o grupo de disponibilidade. Para obter mais informações, veja [Mover um banco de dados protegido por TDE para outro SQL Server](../../../relational-databases/security/encryption/move-a-tde-protected-database-to-another-sql-server.md).  
  
###  <a name="PermissionsDbs"></a> Permissões (bancos de dados de disponibilidade)  
 Requer a permissão ALTER no banco de dados.  
  
###  <a name="RelatedTasksADb"></a> Tarefas relacionadas (bancos de dados de disponibilidade)  
  
|Tarefa|Tópico|  
|----------|-----------|  
|Preparando um banco de dados secundário (manualmente)|[Preparar um banco de dados secundário manualmente para um grupo de disponibilidade &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)|  
|Unindo um banco de dados secundário ao grupo de disponibilidade (manualmente)|[Unir um banco de dados secundário a um grupo de disponibilidade &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)|  
|Modificando o número de bancos de dados de disponibilidade|[Adicionar um banco de dados a um grupo de disponibilidade &#40;SQL Server&#41;](availability-group-add-a-database.md)<br /><br /> [Remover um banco de dados secundário de um grupo de disponibilidade &#40;SQL Server&#41;](remove-a-secondary-database-from-an-availability-group-sql-server.md)<br /><br /> [Remover um banco de dados primário de um grupo de disponibilidade &#40;SQL Server&#41;](remove-a-primary-database-from-an-availability-group-sql-server.md)|  
  
##  <a name="RelatedContent"></a> Conteúdo relacionado  
  
-   [Guia de soluções AlwaysOn do Microsoft SQL Server para alta disponibilidade e recuperação de desastre](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   [Blog da equipe do AlwaysOn do SQL Server: blog oficial da equipe do SQL Server AlwaysOn](https://blogs.msdn.com/b/sqlalwayson/)  
  
-   [Série de aprendizado do AlwaysON - HADRON: uso de trabalho do pool para bancos de dados habilitados do HADRON](https://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Clustering de failover e Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [Conectividade de Cliente AlwaysOn (SQL Server)](always-on-client-connectivity-sql-server.md)  
  
  
