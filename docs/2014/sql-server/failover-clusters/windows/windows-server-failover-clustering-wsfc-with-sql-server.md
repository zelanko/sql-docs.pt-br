---
title: WSFC (Clustering de Failover do Windows Server) com o SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], WSFC clusters
- Windows Server Failover Clustering (WSFC), with SQL Server
- WSFC, with SQL Server
- quorum [SQL Server]
- failover clustering [SQL Server], AlwaysOn Availability Groups
ms.assetid: 79d2ea5a-edd8-4b3b-9502-96202057b01a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f39911901b6ab729382c2e08b34c3452d4ec65cd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63246028"
---
# <a name="windows-server-failover-clustering-wsfc-with-sql-server"></a>WSFC (Windows Server Failover Clustering) com o SQL Server
  Um Cluster WSFC ( *Windows Server failover clustering* ) é um grupo de servidores independentes que funcionam em conjunto para aumentar a disponibilidade de aplicativos e serviços. 
  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] tira proveito dos serviços e recursos do WSFC para oferecer suporte às instâncias de cluster de failover do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] e do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 
  
##  <a name="TermsAndDefs"></a> Termos e definições  
 Cluster WSFC  
 Um cluster do WSFC (Windows Server Failover Clustering é um grupo de servidores independentes que funcionam em conjunto para aumentar a disponibilidade de aplicativos e serviços.  
  
 Instância de cluster de failover  
 Uma instância de um serviço do Windows que gerencia um recurso de endereço IP, um recurso de nome de rede e recursos adicionais que são necessários para executar um ou mais aplicativos ou serviços. Os clientes podem usar o nome de rede para acessar os recursos no grupo, semelhante ao uso de um nome de computador para acessar os serviços em um servidor físico. Porém, como uma instância de cluster de failover é um grupo, seu failover pode ser feito em outro nó sem afetar o nome ou o endereço subjacente.  
  
 Nó  
 Um sistema do Microsoft Windows Server que seja membro ativo ou inativo de um cluster de servidores.  
  
 Recurso de cluster  
 Uma entidade física ou lógica que pode ser de propriedade de um nó, colocada online e offline, movida entre nós e gerenciada como um objeto de cluster. Um recurso de cluster pode ser de propriedade de apenas um único nó em determinado momento.  
  
 Resource group  
 Uma coleção de recursos de cluster gerenciados como um único objeto de cluster. Normalmente, um grupo de recursos contém todos os recursos de cluster que são necessário para a execução de um aplicativo ou serviço específico. Failover e failback sempre agem em grupos de recursos.  
  
 Dependência de recurso  
 Um recurso do qual outro recurso depende. Se o recurso A depender do recurso B, B será uma dependência de A.  
  
 Recurso de nome de rede  
 Um nome de servidor lógico que é gerenciado como um recurso de cluster. Um recurso de nome de rede deve ser usado com um recurso de endereço IP.  
  
 Proprietário preferido  
 Um nó no qual um grupo de recursos prefere ser executado. Cada grupo de recursos é associado a uma lista de proprietários preferidos classificados em ordem de preferência. Durante o failover automático, o grupo de recursos é movido para o próximo nó preferido na lista de proprietários preferidos.  
  
 Proprietário possível  
 Um nó secundário no qual um recurso pode ser executado. Cada grupo de recursos é associado a uma lista de possíveis proprietários. Os grupos de recursos podem fazer failover apenas nos nós listados como possíveis proprietários.  
  
 Modo de quorum  
 A configuração de quorum em um cluster de failover que determina o número de falhas de nós que o cluster pode sustentar.  
  
 Quorum forçado  
 O processo para iniciar o cluster embora apenas uma minoria dos elementos que são necessários para o quorum esteja em comunicação.  
  
 Para obter mais informações, consulte: [Glossário de cluster de failover](/previous-versions/windows/desktop/MsCS/server-cluster-glossary)  
  
##  <a name="Overview"></a>Visão geral do Windows Server failover clustering  
 O Windows Server Failover Clustering fornece recursos de infraestrutura que dão suporte aos cenários de alta disponibilidade e recuperação de desastres dos aplicativos de servidor hospedados, como o Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e o Microsoft Exchange. Se houver falha em um nó de cluster ou serviço, os serviços que foram hospedados naquele nó poderão ser transferidos automática ou manualmente para outro nó disponível em um processo conhecido como *failover*.  
  
 Os nós do cluster do WSFC funcionam em conjunto para fornecer coletivamente estes tipos de recursos:  
  
-   **Metadados e notificações distribuídos.** O serviço WSFC e os metadados de aplicativos hospedados são mantidos em cada nó do cluster. Esses metadados incluem a configuração e o status do WSFC, além das configurações dos aplicativos hospedados. As alterações nos metadados ou no status de um nó são propagadas automaticamente para os outros nós do cluster.  
  
-   **Gerenciamento de recursos.** Os nós individuais do cluster podem fornecer recursos físicos, como armazenamento anexado diretamente, interfaces de rede e acesso a armazenamento em disco compartilhado. Os aplicativos hospedados se registram como um recurso de cluster e podem configurar dependências de inicialização e de integridade em outros recursos.  
  
-   **Monitoramento de integridade.** A detecção de integridade entre nós e de nó primário é realizada por meio de uma combinação de comunicações de rede de estilo de pulsação e de monitoramento de recursos. A integridade geral do cluster é determinada pelos votos de um quorum de nós no cluster.  
  
-   **Coordenação de failover.** Cada recurso é configurado para ser hospedado em um nó primário, e cada um deles pode ser transferido automática ou manualmente para um ou mais nós secundários. Uma política de failover baseado em integridade controla a transferência automática de propriedade de recurso entre nós. Os nós e os aplicativos hospedados são notificados quando ocorre um failover para que possam reagir de maneira apropriada.  
  
 Para obter mais informações, consulte: [Clusters de failover no Windows Server 2008 R2](https://technet.microsoft.com/library/ff182338\(WS.10\).aspx)  
  
##  <a name="AlwaysOnWsfcTech"></a>SQL Server tecnologias AlwaysOn e WSFC  
 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]O *AlwaysOn* é uma nova solução de alta disponibilidade e recuperação de desastres que aproveita o WSFC. AlwaysOn fornece uma solução integrada e flexível, que aumenta a disponibilidade do aplicativo, fornece melhor retorno em investimentos de hardware e simplifica a implantação e o gerenciamento de alta disponibilidade.  
  
 As Instâncias de Cluster de Failover [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] e AlwaysOn usam o WSFC como uma tecnologia de plataforma, registrando componentes como recursos de cluster WSFC.  Os recursos relacionados são combinados em um *grupo de recursos*, que podem ser tornados dependentes de outros recursos de cluster do WSFC. O serviço de cluster do WSFC pode detectar e sinalizar a necessidade de reiniciar a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou fazer failover automaticamente em um nó de servidor diferente no cluster do WSFC.  
  
> [!IMPORTANT]  
>  Para aproveitar ao máximo as tecnologias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] AlwaysOn, você deve aplicar vários pré-requisitos relacionados ao WSFC.  
>   
>  Para obter mais informações, veja: [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)  
  
### <a name="instance-level-high-availability-with-alwayson-failover-cluster-instances"></a>Alta disponibilidade em nível de instância com instâncias de cluster de failover AlwaysOn  
 Uma *FCI (Instância de Cluster de Failover)* AlwaysOn é uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instalada em nós em um cluster WSFC. Esse tipo de instância tem dependências de recursos no armazenamento de disco compartilhado (via Fibre Channel ou SAN iSCSI) e em um nome de rede virtual. O nome de rede virtual tem uma dependência de recurso em um ou mais endereços IP virtuais, cada um em uma sub-rede diferente. O serviço do SQL Server e o serviço SQL Server Agent são registrados como recursos; ambos se tornam dependentes do recurso de nome de rede virtual.  
  
 No caso de um failover, o serviço WSFC transfere a propriedade dos recursos da instância para um nó de failover designado. A instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é então reiniciada no nó de failover e os bancos de dados são recuperados da maneira usual. Em qualquer momento determinado, apenas um único nó do cluster pode hospedar a FCI e os recursos subjacentes.  
  
> [!NOTE]  
>  Uma Instância de Cluster de Failover AlwaysOn exige armazenamento em disco compartilhado simétrico, como uma SAN (rede de área de armazenamento) ou um compartilhamento de arquivos SMB.  Os volumes de armazenamento de disco compartilhados devem estar disponíveis a todos os nós de failover potenciais no cluster do WSFC.  
  
 Para obter mais informações, consulte: [instâncias de cluster de failover do AlwaysOn](always-on-failover-cluster-instances-sql-server.md)  
  
### <a name="database-level-high-availability-with-includesshadrincludessshadr-mdmd"></a>Alta disponibilidade no nível do banco de dados com o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]  
 Um *grupo de disponibilidade* é um conjunto de bancos de dados de usuário que fazem failover juntos. Um grupo de disponibilidade consiste em uma *réplica de disponibilidade* primária e em uma a quatro réplicas secundárias que são mantidas pelo movimento de dados baseado em log do SQL Server para proteção de dados, dispensando o armazenamento compartilhado. Cada réplica é hospedada por uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em um nó diferente do cluster do WSFC. O grupo de disponibilidade e um nome de rede virtual correspondente são registrados como recursos no cluster do WSFC.  
  
 Um *ouvinte de grupo de disponibilidade* no nó de réplica primária responde às solicitações de cliente de entrada para conectar-se ao nome de rede virtual e, com base nos atributos da cadeia de conexão, redireciona cada solicitação à instância apropriada do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 No caso de um failover, em vez de transferir a propriedade de recursos físicos compartilhados para outro nó, o WSFC é utilizado para reconfigurar uma réplica secundária em outra instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para se tornar a réplica primária do grupo de disponibilidade. O recurso de nome de rede virtual do grupo de disponibilidade é transferido para aquela instância.  
  
 A qualquer determinado momento, apenas uma única instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pode hospedar a réplica primária dos bancos de dados de um grupo de disponibilidade. Cada réplica secundária associada deve residir em uma instância separada, e cada instância deve residir em nós físicos separados.  
  
> [!NOTE]  
>  O [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] não exige a implantação de uma Instância de Cluster de Failover ou o uso de armazenamento compartilhado simétrico (SAN ou SMB).  
>   
>  Uma FCI (Instância de Cluster de Failover) pode ser usada junto com um grupo de disponibilidade para aprimorar a disponibilidade de uma réplica de disponibilidade. Entretanto, para impedir situações de competição potenciais no cluster do WSFC, o failover automático do grupo de disponibilidade não tem suporte de e para uma réplica de disponibilidade que está hospedada em uma FCI ou vice-versa.  
  
 Para obter mais informações, confira: [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
##  <a name="AlwaysOnWsfcHealth"></a>Failover e monitoramento de integridade do WSFC  
 A alta disponibilidade de uma solução de AlwaysOn é realizada por meio do monitoramento proativo da integridade dos recursos físicos e lógicos do cluster do WSFC, junto com failover automático sobre e reconfiguração de hardware redundante.  Um administrador do sistema também pode iniciar um *failover manual* de um grupo de disponibilidade ou instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de um nó para outro.  
  
### <a name="failover-policies-for-nodes-failover-cluster-instances-and-availability-groups"></a>Políticas de failover para nós, instâncias de cluster de failover e grupos de disponibilidade  
 Uma *política de failover* é configurada no nó de cluster WSFC, na FCI (Instância de Cluster de failover) do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e nos níveis de grupos de disponibilidade.  Essas políticas, baseadas na severidade, duração e frequência do status do recurso do cluster não íntegro e na capacidade de resposta do nó, podem disparar uma reinicialização do serviço ou um *failover automático* de recursos do cluster de um nó para outro ou disparar a movimentação de uma réplica primária de grupo de disponibilidade de uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para outra.  
  
 O failover de uma réplica de grupo de disponibilidade não afeta a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] subjacente.  O failover de uma FCI move as réplicas do grupo de disponibilidade hospedado com a instância.  
  
 Para obter mais informações, consulte: [política de failover para instâncias de cluster de failover](failover-policy-for-failover-cluster-instances.md)  
  
### <a name="wsfc-resource-health-detection"></a>Detecção de integridade de recursos do WSFC  
 Cada recurso em um nó de cluster do WSFC pode relatar seu status e integridade, periodicamente ou sob demanda. Várias circunstâncias podem indicar falha no recurso; por exemplo, deficiência de energia, erros de disco ou de memória, erros de comunicação de rede ou serviços sem resposta.  
  
 Recursos de cluster WSFC como redes, armazenamento ou serviços podem se tornar dependentes uns dos outros. A integridade cumulativa de um recurso é determinada pela acúmulo bem-sucedido de sua integridade com a integridade de cada uma de suas dependências de recurso.  
  
### <a name="wsfc-inter-node-health-detection-and-quorum-voting"></a>Detecção de integridade entre nós do WSFC e votação de quorum  
 Cada nó em um cluster do WSFC participa da comunicação de pulsação periódica para compartilhar o status de integridade do nó com os outros nós. Nós sem resposta são considerados como em estado com falha.  
  
 Um conjunto de nós de *quorum* é uma maioria dos nós de votação e testemunhas no cluster WSFC. A integridade geral e o status de um cluster WSFC são determinados por um *voto de quorum*periódico. A presença de um quorum significa que o cluster está íntegro e é capaz de fornecer tolerância a falhas no nível de nó.  
  
 Um *modo de quorum* é configurado no nível de cluster do WSFC que determina a metodologia usada na votação do quorum e quando executar um failover automático ou colocar o cluster offline.  
  
> [!TIP]  
>  É prática recomendada sempre ter um número ímpar de votos de quorum em um cluster do WSFC.  Para a finalidade da votação de quorum, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não precisa ser instalado em todos os nós do cluster. Um servidor adicional pode agir como um membro do quorum, ou o modelo de quorum do WSFC pode ser configurado para usar um compartilhamento de arquivo remoto como um desempatador.  
>   
>  Para obter mais informações, consulte: [configuração de modos de quorum do WSFC e votação &#40;SQL Server&#41;](wsfc-quorum-modes-and-voting-configuration-sql-server.md)  
  
### <a name="disaster-recovery-through-forced-quorum"></a>Recuperação de desastres por meio de quorum forçado  
 Dependendo das práticas operacionais e da configuração do cluster do WSFC, você pode incorrer em failovers automáticos e manuais e ainda manter uma solução do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] AlwaysOn robusta e tolerante a falhas. No entanto, se um quorum dos nós de votação elegíveis no cluster do WSFC não puder se comunicar um com o outro, ou se houver falha na validação de integridade do cluster do WSFC, o cluster do WSFC poderá ser colocado offline.  
  
 Se o cluster do WSFC for colocado offline por causa de um desastre não planejado ou devido a um hardware persistente ou falha de comunicação, será necessária intervenção administrativa manual para *forçar um quorum* e colocar os nós de cluster sobreviventes online em uma configuração não tolerante a falhas.  
  
 Subsequentemente, uma série de etapas também deve ser utilizada para reconfigurar o cluster do WSFC, recuperar as réplicas de banco de dados afetadas e restabelecer um novo quorum.  
  
 Para obter mais informações, consulte: [recuperação de desastre do WSFC por meio de quorum forçado &#40;SQL Server&#41;](wsfc-disaster-recovery-through-forced-quorum-sql-server.md)  
  
##  <a name="AlwaysOnWsfcRelationship"></a>Relação dos componentes do SQL Server AlwaysOn com o WSFC  
 Existem várias camadas de relações entre o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] AlwaysOn e os recursos e componentes do WSFC.  
  
 Os grupos de disponibilidade do AlwaysOn são hospedados nas instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
 Uma solicitação de cliente que especifica um nome de rede do ouvinte de grupo de disponibilidade lógico para se conectar a um banco de dados primário ou secundário é redirecionada para o nome de rede de instância apropriado da instância subjacente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou da Instância de Cluster de Failover (FCI) do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 As instâncias do SQL Server estão hospedadas ativamente em um único nó.  
 Quando presente, uma instância autônoma do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sempre reside em um único nó com um nome de rede de instância estático.  Quando presente, uma FCI do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] estará ativa em um entre dois ou mais nós de failover possíveis com um único nome de rede de instância virtual.  
  
 Nós são membros de um cluster do WSFC.  
 Os metadados e o status de configuração do WSFC de todos os nós são armazenados em cada nó. Cada servidor pode oferecer volumes de armazenamento assimétrico ou de armazenamento compartilhado (SAN) para bancos de dados do usuário ou do sistema. Cada servidor tem pelo menos uma interface de rede física em uma ou mais sub-redes IP.  
  
 O serviço WSFC monitora a integridade e gerencia a configuração de um grupo de servidores.  
 O serviço WSFC (Windows Server Failover Cluster) propaga alterações nos metadados e no status da Configuração do WSFC para todos os nós do cluster. Os metadados parciais e o status podem ser armazenados em um compartilhamento de arquivos remoto com testemunha de quorum do WSFC. Dois ou mais nós ou testemunhas ativos constituem um quorum para votar na integridade do cluster WSFC.  
  
 
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] são subchaves do cluster WSFC.  
 Se você excluir e recriar um cluster WSFC, precisará desabilitar e reabilitar o recurso [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] em cada instância de servidor habilitada para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] no cluster WSFC original. Para obter mais informações, veja [Habilitar e desabilitar Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md).  
  
 ![Diagrama de contexto de componente do SQL Server AlwaysOn](../../../database-engine/media/alwaysoncomponentcontextdiagram.gif "Diagrama de contexto de componente do SQL Server AlwaysOn")  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Exibir configurações de NodeWeight de quorum do cluster](view-cluster-quorum-nodeweight-settings.md)  
  
-   [Definir configurações de NodeWeight de quorum do cluster](configure-cluster-quorum-nodeweight-settings.md)  
  
-   [Forçar um cluster WSFC para iniciar sem um quorum](force-a-wsfc-cluster-to-start-without-a-quorum.md)  
  
##  <a name="RelatedContent"></a> Conteúdo relacionado  
  
-   [Tecnologias do Windows Server: clusters de failover](https://technet.microsoft.com/library/cc732488\(v=WS.10\).aspx)  
  
-   [Clusters de failover no Windows Server 2008 R2](https://technet.microsoft.com/library/ff182338\(WS.10\).aspx)  
  
-   [Exibir eventos e logs de um cluster de failover](https://technet.microsoft.com/library/cc772342\(WS.10\).aspx)  
  
-   [Cluster de failover Get-ClusterLog do cmdlet](https://technet.microsoft.com/library/ee461045.aspx)  
  
## <a name="see-also"></a>Consulte Também  
 [Instâncias de cluster de failover do AlwaysOn (SQL Server)](always-on-failover-cluster-instances-sql-server.md)   
 [Visão geral do Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Os modos de quorum WSFC e a configuração de votação &#40;SQL Server&#41;](wsfc-quorum-modes-and-voting-configuration-sql-server.md)   
 [Política de failover para instâncias de cluster de failover](failover-policy-for-failover-cluster-instances.md)   
 [Recuperação de desastres do WSFC por meio de quorum forçado &#40;SQL Server&#41;](wsfc-disaster-recovery-through-forced-quorum-sql-server.md)  
  
  
