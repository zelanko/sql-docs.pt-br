---
title: "Instâncias do cluster de failover do AlwaysOn (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 01/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- clustering [SQL Server]
- high availability [SQL Server], failover clustering
- virtual servers [SQL Server], about virtual servers
- clusters [SQL Server]
- servers [SQL Server], failover clustering
- resource groups [SQL Server]
- availability [SQL Server]
- failover clustering [SQL Server]
- AlwaysOn [SQL Server], see failover clustering [SQL Server]
ms.assetid: 86a15b33-4d03-4549-8ea2-b45e4f1baad7
caps.latest.revision: 80
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a5de42512c1b7f5372e96f53b6332145fb99a3d8
ms.lasthandoff: 04/11/2017

---
# <a name="always-on-failover-cluster-instances-sql-server"></a>Instâncias do cluster de failover do AlwaysOn (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Como parte da oferta do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] AlwaysOn, as Instâncias de Cluster de Failover do AlwaysOn aproveitam a funcionalidade WSFC (Windows Server Failover Clustering) para fornecer alta disponibilidade local por meio de redundância na instância de nível de servidor, uma FCI ( *instância de cluster de failover* ). Uma FCI é uma instância única do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que é instalada em nós de WSFC (Windows Server Failover Clustering) e, possivelmente, em várias sub-redes. Na rede, uma FCI aparece ser uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sendo executada em um único computador, mas proporciona failover de um nó do WSFC para outro se o nó atual se tornar indisponível.  
  
 Uma FCI pode aproveitar os [Grupos de Disponibilidade](../../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md) para fornecer recuperação remota de desastres no nível do banco de dados. Para obter mais informações, consulte [Clustering de failover e Grupos de Disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md).  
 
 > [!NOTE]  
 > O Windows Server 2016 Datacenter Edition apresenta suporte para S2D (Espaços de Armazenamento Diretos). As instâncias de cluster de failover do SQL Server dão suporte ao S2D para recursos de armazenamento de cluster. Para obter mais informações, consulte [Espaços de Armazenamento Diretos no Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).
 > 
 >As instâncias de cluster de failover também dão suporte ao CSVs (Volumes Compartilhados de Cluster). Para obter mais informações, veja [Noções básicas sobre volumes compartilhados clusterizados em um cluster de failover](http://technet.microsoft.com/library/dd759255.aspx). 
   
 **Neste tópico:**  
  
-   [Benefícios](#Benefits)  
  
-   [Recomendações](#Recommendations)  
  
-   [Visão geral da instância de cluster de failover](#Overview)  
  
-   [Elementos de uma instância de cluster de failover](#FCIelements)  
  
-   [Conceitos e tarefas de failover do SQL Server](#ConceptsAndTasks)  
  
-   [Tópicos relacionados](#RelatedTopics)  
  
##  <a name="Benefits"></a> Benefícios de uma instância de cluster de failover  
 Quando há falha de hardware ou de software de um servidor, os aplicativos ou clientes que conectam ao servidor enfrentam um tempo de inatividade. Quando uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é configurada para ser uma FCI (em vez de uma instância autônoma), a alta disponibilidade dessa instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é protegida pela presença de nós redundantes na FCI. Somente um dos nós na FCI tem o grupo de recursos do WSFC de cada vez. No caso de uma falha (problemas de hardware, falhas de sistema operacional, aplicativo ou falhas de serviço) ou de uma atualização planejada, a propriedade do grupo de recursos é movida para outro nó do WSFC. Este processo é transparente ao cliente ou aplicativo que se conecta ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e isso minimiza o tempo de inatividade pelo qual passa o aplicativo ou os clientes durante uma falha. Alguns dos principais benefícios que instâncias de cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] oferecem:  
  
-   Proteção em nível de instância por redundância  
  
-   Failover automático no caso de uma falha (problemas de hardware, falhas de sistema operacional, aplicativo ou falhas de serviço)  
  
    > [!IMPORTANT]  
    >  Em um grupo de disponibilidade, não há suporte para o failover automático de uma FCI para outros nós dentro do grupo de disponibilidade. Isto significa que os nós das FCIs e autônomos não deverão ser acoplados dentro de um grupo de disponibilidade se o failover automático for um componente importante de sua solução de alta disponibilidade. Porém, este acoplamento pode ser feito para sua solução de *recuperação de desastres* .  
  
-   Suporte para uma matriz ampla de soluções de armazenamento, inclusive discos de cluster do WSFC (iSCSI, Fiber Channel e assim por diante) e compartilhamentos de arquivos de protocolo SMB.  
  
-   Solução de recuperação de desastres usando uma FCI de várias sub-redes ou executando um banco de dados hospedado por FCI dentro de um grupo de disponibilidade. Com o novo suporte a várias sub-redes no [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], uma FCI de várias sub-redes não mais exigirá uma LAN virtual, aumentando a capacidade de gerenciamento e a segurança de uma FCI de várias sub-redes.  
  
-   Zero reconfiguração de aplicativos e clientes durante failovers  
  
-   Política de failover flexível para eventos de gatilho granulares para failovers automáticos  
  
-   Failovers confiáveis por meio de detecção de integridade periódica e detalhada usando conexões dedicadas e persistidas  
  
-   Capacidade de configuração e previsibilidade em tempo de failover por meio de pontos de verificação indiretos em segundo plano  
  
-   Uso acelerado de recurso durante failovers  
  
##  <a name="Recommendations"></a> Recomendações  
 Em um ambiente de produção, é recomendável usar endereços IP estáticos juntamente com o endereço IP virtual de uma instância de cluster de failover.  Não é recomendável o uso do DHCP em um ambiente de produção. No caso de tempo de inatividade, se a concessão do IP DHCP expirar, será necessário tempo adicional para registrar novamente o endereço IP DHCP novo associado ao nome DNS.  
  
##  <a name="Overview"></a> Visão geral da instância de cluster de failover  
 Uma FCI é executada em um grupo de recursos do WSFC com um ou mais nós do WSFC. Quando a FCI é iniciada, um dos nós assume a propriedade do grupo de recursos e coloca sua instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] online. Os recursos de propriedade deste nó incluem:  
  
-   Nome da rede  
  
-   Endereço IP  
  
-   Discos compartilhados  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Serviço do Mecanismo de Banco de Dados  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Analysis Services, se estiver instalado  
  
-   Um recurso de compartilhamento de arquivos, se o recurso FILESTREAM estiver instalado  
  
 A qualquer momento, somente o proprietário do grupo de recursos (e nenhum outro nó na FCI) está executando os respectivos serviços do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no grupo de recursos. Quando um failover ocorrer, se é um failover automático ou um failover planejado, esta sequência de eventos acontece:  
  
1.  A menos que ocorra uma falha de hardware ou de sistema, todas as páginas sujas no cache do buffer serão gravadas no disco.  
  
2.  Todos os respectivos serviços do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no grupo de recursos são parados no nó ativo.  
  
3.  A propriedade de grupo de recursos é transferida para outro nó na FCI.  
  
4.  O novo proprietário do grupo de recursos inicia seus serviços do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
5.  As solicitações de conexão de aplicativo cliente são automaticamente direcionadas para o novo nó ativo usando o mesmo VNN (nome de rede virtual).  
  
 A FCI fica online contanto que seu cluster WSFC subjacente esteja com boa integridade de quorum (a maioria dos nós do quorum WSFC estão disponíveis como destinos de failover automáticos). Quando o cluster do WSFC perde seu quorum, devido a falha de hardware, software, rede ou configuração de quorum imprópria, o cluster do WSFC inteiro, junto com o FCI, é colocado offline. É necessário realizar uma intervenção manual neste cenário de failover não planejado para restabelecer o quorum nos nós disponíveis restantes para colocar o cluster do WSFC e da FCI online novamente. Para obter mais informações, veja [Configuração de modos de quorum WSFC e votação &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md).  
  
### <a name="predictable-failover-time"></a>Hora de failover previsível  
 Dependendo de quando sua instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] executou uma operação de ponto de verificação pela última vez, pode haver uma quantidade significativa de páginas sujas no cache do buffer. Por consequência, os failovers duram o suficiente para gravar as páginas sujas restantes no disco, o que pode levar a um tempo de failover longo e imprevisível. A partir do [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], a FCI pode usar pontos de verificação indiretos para limitar a quantidade de páginas sujas mantidas no cache do buffer. Embora consuma recursos adicionais sob carga de trabalho normal, isto torna o failover mais previsível e também mais configurável. Isto é muito útil quando o acordo do nível de serviço em sua organização especifica o RTO (objetivo de tempo de recuperação) para sua solução de alta disponibilidade. Para obter mais informações sobre pontos de verificação indiretos, consulte [Indirect Checkpoints](../../../relational-databases/logs/database-checkpoints-sql-server.md#IndirectChkpt).  
  
### <a name="reliable-health-monitoring-and-flexible-failover-policy"></a>Monitoramento de integridade confiável e política de failover flexível  
 Depois que a FCI é iniciada com sucesso, o serviço do WSFC monitora a integridade do cluster do WSFC subjacente e também a integridade da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . A partir do [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], o serviço do WSFC usa uma conexão dedicada para sondar a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ativa em busca de diagnóstico de componente detalhados por meio de um procedimento armazenado de sistema. São três implicações:  
  
-   A conexão dedicada para a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] possibilita sondar diagnóstico de componente com confiança o tempo todo, mesmo quando a FCI está sob carga pesada. Isto possibilita distinguir entre um sistema que está sob carga pesada e um sistema que de fato tem condições de falha, impedindo, portanto, problemas como falsos failovers.  
  
-   Os diagnóstico de componente detalhado possibilita configurar uma política de failover mais flexível, por meio da qual você pode escolher quais condições de falha acionam failovers e quais condições de falha não acionam.  
  
-   O diagnóstico de componente detalhado também permite uma melhor solução de problemas de failovers automáticos retroativamente. As informações de diagnóstico são armazenadas em arquivos de log que são colocados com os logs de erros do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Você pode carregá-los no Visualizador do Arquivo de Log para inspecionar os estados do componente que levam até a ocorrência de failover para determinar o que causa o failover.  
  
 Para obter mais informações, consulte [Failover Policy for Failover Cluster Instances](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md).  
  
##  <a name="FCIelements"></a> Elementos de uma instância de cluster de failover  
 Uma FCI consiste em um conjunto de servidores físicos (nós) que contêm configuração de hardware semelhante e também configuração de software idêntica, que inclui versão de sistema operacional e nível de patch e versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , nível de patch, componentes e nome de instância. A configuração de software idêntica é necessária para assegurar que a FCI possa ser completamente funcional porque ocorre o failover entre os nós.  
  
 Grupo de recursos do WSFC  
 Uma FCI do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é executada em um grupo de recursos do WSFC. Cada nó no grupo de recursos mantém uma cópia sincronizada dos parâmetros de configuração e chave do Registro como pontos de verificação para assegurar a funcionalidade completa da FCI depois de um failover e somente um dos nós no cluster possui o grupo de recursos de cada vez (o nó ativo). O serviço do WSFC gerencia o cluster de servidores, a configuração de quorum, a política de failover e as operações de failover, assim como os endereços de VNN e IP virtuais para a FCI. No caso de uma falha (problemas de hardware, falhas de sistema operacional, aplicativo ou falhas de serviço) ou de uma atualização planejada, a propriedade do grupo de recursos é movida para outro nó na FCI. O número de nós que têm suporte em um grupo de recursos do WSFC depende de sua edição do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Além disso, o mesmo cluster do WSFC pode executar várias FCIs (vários grupos de recursos), dependendo de sua capacidade de hardware, como CPUs, memória e número de discos.  
  
 Binários do SQL Server  
 Os binários de produto são instalados localmente em cada nó da FCI, um processo semelhante a instalações autônomas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Porém, durante a inicialização, os serviços não são iniciados automaticamente, mas são gerenciados pelo WSFC.  
  
 Armazenamento  
 Ao contrário do grupo de disponibilidade, uma FCI deve usar armazenamento compartilhado entre todos os nós da FCI para o armazenamento do banco de dados e do log. O armazenamento compartilhado pode ser na forma de discos de cluster do WSFC, discos em uma rede SAN, S2D (Espaços de Armazenamento Diretos) ou compartilhamentos de arquivos em um SMB. Deste modo, todos os nós na FCI têm a mesma exibição dos dados de instância sempre que um failover ocorre. No entanto, isto significa que o armazenamento compartilhado tem o potencial de ser o único ponto de falha, e a FCI depende da solução de armazenamento subjacente para assegurar a proteção de dados.  
  
 Nome da rede  
 O VNN para a FCI fornece um ponto de conexão unificado para a FCI. Isto permite que aplicativos conectem-se ao VNN sem a necessidade de conhecer o nó ativo atualmente. Quando um failover ocorre, o VNN é registrado para o novo nó ativo depois de iniciar. Este processo é transparente ao cliente ou aplicativo que se conecta ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e isso minimiza o tempo de inatividade pelo qual passa o aplicativo ou os clientes durante uma falha.  
  
 IP virtuais  
 No caso de uma FCI de várias sub-redes, um endereço IP virtual é atribuído a cada sub-rede na FCI. Durante um failover, o VNN no servidor DNS é atualizado para apontar para o endereço IP virtual para a respectiva sub-rede. Aplicativos e clientes podem então se conectar ao FCI usando o mesmo VNN depois de um failover de várias sub-redes.  
  
##  <a name="ConceptsAndTasks"></a> Conceitos e tarefas de failover do SQL Server  
  
|Conceitos e tarefas|Tópico|  
|------------------------|-----------|  
|Descreve o mecanismo de detecção de falha e a política de failover flexível.|[Failover Policy for Failover Cluster Instances](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)|  
|Descreve os conceitos na administração e na manutenção da FCI.|[Administração e manutenção da instância de cluster de failover](../../../sql-server/failover-clusters/windows/failover-cluster-instance-administration-and-maintenance.md)|  
|Descreve a configuração e os conceitos de várias sub-redes|[Clustering de várias sub-redes do SQL Server &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/sql-server-multi-subnet-clustering-sql-server.md)|  
  
##  <a name="RelatedTopics"></a> Tópicos relacionados  
  
|**Descrições do tópico**|**Tópico**|  
|----------------------------|---------------|  
|Descreve como instalar uma nova FCI do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|[Criar um novo cluster de failover do SQL Server &#40;Instalação&#41;](../../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)|  
|Descreve como atualizar para um cluster de failover do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] .|[Atualizar uma instância de cluster de failover do SQL Server](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md)|  
|Descreve conceitos de clustering de failover do Windows e fornece links para tarefas relativas ao clustering de failover do Windows.|[!INCLUDE[nextref_longhorn](../../../includes/nextref-longhorn-md.md)]: [Visão geral de clusters de failover](http://go.microsoft.com/fwlink/?LinkId=177878)<br /><br /> [!INCLUDE[nextref_longhorn](../../../includes/nextref-longhorn-md.md)] R2: [Visão geral de clusters de failover](http://go.microsoft.com/fwlink/?LinkId=177879)|  
|Descreve as distinções em conceitos entre nós em uma FCI e réplicas dentro de um grupo de disponibilidade e considerações para usar uma FCI para hospedar uma réplica para um grupo de disponibilidade.|[Clustering de failover e Grupos de Disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)|  
  
  

