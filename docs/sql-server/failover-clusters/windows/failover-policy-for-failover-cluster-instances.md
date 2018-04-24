---
title: Política de failover para instâncias de cluster de failover | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: failover-clusters
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- flexible failover policy
ms.assetid: 39ceaac5-42fa-4b5d-bfb6-54403d7f0dc9
caps.latest.revision: 45
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 91a6c3525ed89624bca7289bd76963cd932b9623
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="failover-policy-for-failover-cluster-instances"></a>Política de failover para instâncias de cluster de failover
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Em uma FCI (instância de cluster de failover) do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , somente um nó pode ter o grupo de recursos de cluster do WSFC (Windows Server Failover Cluster) em um determinado momento. As solicitações do cliente são atendidas por esse nó na FCI. Em caso de falha e uma reinicialização malsucedida, a propriedade de grupo é movida para outro nó do WSFC na FCI. Esse processo é chamado de failover. [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] aumenta a confiabilidade de detecção de falha e fornece uma política de failover flexível.  
  
 Uma FCI do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] depende do serviço do WSFC subjacente para detecção de failover. Assim, dois mecanismos determinam o comportamento de failover para FCI: a primeira é a funcionalidade nativa do WSFC e a última é a funcionalidade adicionada pela instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   O cluster do WSFC mantém a configuração de quorum que assegura um destino de failover exclusivo em um failover automático. O serviço do WSFC determina se o cluster está na integridade de quorum ideal o tempo todo e coloca o grupo de recursos online e offline devidamente.  
  
-   A instância ativa do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] relata periodicamente um conjunto de diagnóstico de componente para o grupo de recursos do WSFC sobre uma conexão dedicada. O grupo de recursos do WSFC mantém a política de failover, que define as condições de falha que acionam reinicializações e failovers.  
  
 Este tópico discute o segundo mecanismo acima. Para obter mais informações sobre o comportamento do WSFC para configuração de quorum e detecção de integridade, consulte [Configuração de modos de quorum e votação do WSFC &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md).  
  
> [!IMPORTANT]  
>  Failovers automáticos de e para uma FCI não são permitidos em um grupo de disponibilidade AlwaysOn. No entanto, failovers manuais de e para uma FCI são permitidos em um grupo de disponibilidade AlwaysOn.  
  
##  <a name="Concepts"></a> Visão geral da política de failover  
 O processo de failover pode ser dividido nas etapas seguintes:  
  
1.  [Monitorar o status de integridade](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md#monitor)  
  
2.  [Determinando falhas](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md#determine)  
  
3.  [Respondendo a falhas](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md#respond)  
  
###  <a name="monitor"></a> Monitorar o status de integridade  
 Há três tipos de status de integridade que são monitorados para a FCI:  
  
-   [Estado do serviço SQL Server](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md#service)  
  
-   [Capacidade de resposta da instância do SQL Server](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md#instance)  
  
-   [Diagnóstico de componente do SQL Server](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md#component)  
  
####  <a name="service"></a> Estado do serviço SQL Server  
 O serviço do WSFC monitora o estado inicial do serviço SQL Server no nó de FCI ativo para detectar quando o serviço SQL Server é interrompido.  
  
####  <a name="instance"></a> Capacidade de resposta da instância do SQL Server  
 Durante a inicialização do SQL Server, o serviço do WSFC usa a DLL do recurso de Mecanismo de Banco de Dados do SQL Server para criar uma nova conexão com um thread separado que é usado exclusivamente para monitorar o status de integridade. Isso assegura que a instância do SQL tenha os recursos necessários para relatar seu status de integridade durante o carregamento. Com o uso dessa conexão dedicada, o SQL Server executa o procedimento armazenado de sistema [sp_server_diagnostics &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) no modo de repetição para relatar periodicamente o status de integridade dos componentes do SQL Server para a DLL de recurso.  
  
 A DLL do recurso determina a capacidade de resposta da instância do SQL que usa um tempo limite de verificação de integridade. A propriedade HealthCheckTimeout define por quanto tempo a DLL do recurso deve esperar o procedimento armazenado sp_server_diagnostics antes de relatar a instância do SQL como sem resposta para o serviço do WSFC. Essa propriedade pode ser configurada com o uso de T-SQL, bem como no snap-in Gerenciador de Cluster de Failover. Para obter mais informações, consulte [Configure HealthCheckTimeout Property Settings](../../../sql-server/failover-clusters/windows/configure-healthchecktimeout-property-settings.md). Os itens a seguir descrevem como essa propriedade afeta as configurações de tempo limite e intervalo de repetição:  
  
-   A DLL de recurso chama o procedimento armazenado sp_server_diagnostics e define o intervalo de repetição para um terço da configuração de HealthCheckTimeout.  
  
-   Se o procedimento armazenado sp_server_diagnostics estiver lento ou não estiver retornando informações, a DLL do recurso esperará o intervalo especificado por HealthCheckTimeout antes de relatar para o serviço do WSFC que a instância do SQL não está respondendo.  
  
-   Se a conexão dedicada for perdida, a DLL do recurso tentará estabelecer novamente a conexão com a instância SQL do intervalo especificado por HealthCheckTimeout antes de relatar para o serviço do WSFC que a instância do SQL não está respondendo.  
  
####  <a name="component"></a> Diagnóstico de componente do SQL Server  
 O procedimento armazenado de sistema sp_server_diagnostics coleta periodicamente o diagnóstico de componente na instância do SQL. As informações de diagnóstico coletadas são apresentadas como uma linha para cada um dos seguintes componentes e passados para o thread de chamada.  
  
1.  sistema  
  
2.  recurso  
  
3.  processo de consulta  
  
4.  io_subsystem  
  
5.  eventos  
  
 O sistema, o recurso e os componentes do processo de consulta são usados para detecção de falha. O io_subsytem e os componentes de eventos são usados apenas para fins de diagnóstico.  
  
 Cada conjunto de linhas de informações também é gravado no log de diagnósticos do cluster do SQL Server. Para obter mais informações, consulte [Exibir e ler o log de diagnóstico da instância do cluster de failover](../../../sql-server/failover-clusters/windows/view-and-read-failover-cluster-instance-diagnostics-log.md).  
  
> [!TIP]  
>  Embora o procedimento armazenado sp_server_diagnostic seja usado pela tecnologia SQL Server AlwaysOn, ele está disponível para utilização em qualquer instância do SQL Server para ajudar a detectar e solucionar problemas.  
  
####  <a name="determine"></a> Determinando falhas  
 A DLL do recurso do Mecanismo de Banco de Dados do SQL Server determina se o status de integridade detectado é uma condição para falha usando a propriedade FailureConditionLevel. A propriedade FailureConditionLevel define quais status de integridade detectados causam reinicializações ou failovers. Há vários níveis de opções disponíveis, variando desde nenhuma reinicialização automática ou failover a todas as condições de falha possíveis resultantes em uma reinicialização automática ou failover. Para obter mais informações sobre como configurar essa propriedade, consulte [Configure FailureConditionLevel Property Settings](../../../sql-server/failover-clusters/windows/configure-failureconditionlevel-property-settings.md).  
  
 As condições de falha são definidas em uma escala crescente. Para os níveis 1-5, cada um deles deve incluir todas as condições dos níveis anteriores, além de suas próprias condições. Isso significa que, a cada nível, há uma probabilidade crescente de failover ou reinicialização. Os níveis de condição de falha são descritos na tabela a seguir.  
  
 Examine [sp_server_diagnostics &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md), pois esse procedimento armazenado de sistema desempenha uma função importante nos níveis de condição de falha.  
  
|Nível|Condição|Description|  
|-----------|---------------|-----------------|  
|0|Nenhum failover ou reinicialização automática|Indica que nenhum failover ou reinicialização será disparado automaticamente em nenhuma condição de falha. Esse nível destina-se apenas a fins de manutenção do sistema.|  
|1|Failover ou reinicialização quando o servidor estiver inativo|Indica que uma reinicialização ou failover de servidor será disparado se a seguinte condição for gerada:<br /><br /> O serviço SQL Server está inativo.|  
|2|Failover ou reinicialização em caso de servidor sem resposta|Indica que uma reinicialização ou failover de servidor será disparado uma destas condições for gerada:<br /><br /> O serviço SQL Server está inativo.<br /><br /> A instância do SQL Server não está respondendo (a DLL do Recurso não pode receber dados de sp_server_diagnostics nas configurações de HealthCheckTimeout).|  
|3*|Failover ou reinicialização em caso de erros críticos de servidor|Indica que uma reinicialização ou failover de servidor será disparado uma destas condições for gerada:<br /><br /> O serviço SQL Server está inativo.<br /><br /> A instância do SQL Server não está respondendo (a DLL do Recurso não pode receber dados de sp_server_diagnostics nas configurações de HealthCheckTimeout).<br /><br /> O procedimento armazenado de sistema sp_server_diagnostics retorna ‘erro de sistema’.|  
|4|Failover ou reinicialização em caso de erros moderados de servidor|Indica que uma reinicialização ou failover de servidor será disparado uma destas condições for gerada:<br /><br /> O serviço SQL Server está inativo.<br /><br /> A instância do SQL Server não está respondendo (a DLL do Recurso não pode receber dados de sp_server_diagnostics nas configurações de HealthCheckTimeout).<br /><br /> O procedimento armazenado de sistema sp_server_diagnostics retorna ‘erro de sistema’.<br /><br /> O procedimento armazenado de sistema sp_server_diagnostics retorna ‘erro de recurso’.|  
|5|Failover ou reinicialização em qualquer condição de falha qualificada|Indica que uma reinicialização ou failover de servidor será disparado uma destas condições for gerada:<br /><br /> O serviço SQL Server está inativo.<br /><br /> A instância do SQL Server não está respondendo (a DLL do Recurso não pode receber dados de sp_server_diagnostics nas configurações de HealthCheckTimeout).<br /><br /> O procedimento armazenado de sistema sp_server_diagnostics retorna ‘erro de sistema’.<br /><br /> O procedimento armazenado de sistema sp_server_diagnostics retorna ‘erro de recurso’.<br /><br /> O procedimento armazenado de sistema sp_server_diagnostics retorna ‘erro de processamento de consulta’.|  
  
 *Valor padrão  
  
####  <a name="respond"></a> Respondendo a falhas  
 Após a detecção de uma ou mais condições de falha, como o serviço do WSFC responderá às falhas dependerá do estado do quorum do WSFC e das configurações de reinicialização e failover do grupo de recursos de FCI. Se a FCI tiver perdido seu quorum do WSFC, toda a FCI é colocada offline e a FCI perdeu sua alta disponibilidade. Se a FCI ainda tiver seu quorum do WSFC, o serviço do WSFC poderá responder primeiro tentando reiniciar o nó com falha e depois executando failover se as tentativas de reinicialização não forem bem-sucedidas. As configurações de reinicialização e failover são definidas no snap-in Gerenciador de Cluster de Failover. Para obter mais informações sobre essas configurações, consulte [\<Recursos> Propriedades: guia Políticas](http://technet.microsoft.com/library/cc725685.aspx).  
  
 Para obter mais informações sobre como manter a integridade do quórum, veja [Configuração de modos de quorum e votação do WSFC &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md).  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-server-configuration-transact-sql.md)  
  
  
