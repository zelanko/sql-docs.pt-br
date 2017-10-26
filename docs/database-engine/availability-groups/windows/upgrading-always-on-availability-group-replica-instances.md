---
title: "Fazer upgrade das instâncias de réplica do Grupo de Disponibilidade AlwaysOn | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f670af56-dbcc-4309-9119-f919dcad8a65
caps.latest.revision: 14
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 1783e700e516978e4eded68fa675addd8d31a234
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="upgrading-always-on-availability-group-replica-instances"></a>Atualizar instâncias de réplica do Grupo de Disponibilidade AlwaysOn
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Ao atualizar um Grupo de Disponibilidade AlwaysOn do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para uma nova versão do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] , para um novo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]service pack ou atualização cumulativa do ou ao instalar um novo service pack ou atualização cumulativa do Windows, você pode reduzir o tempo de inatividade para a réplica primária para um único failover manual executando uma atualização sem interrupção (ou dois failovers manuais em caso de failback para a primária original). Durante o processo de atualização, uma réplica secundária não estará disponível para failover ou para operações somente leitura e, depois da atualização, poderá levar algum tempo para que a réplica secundária fique atualizada com o nó da réplica primária, dependendo do volume de atividade no nó da réplica primária (portanto, espere alto tráfego de rede).  
  
> [!NOTE]  
>  Este tópico limita a discussão à atualização do próprio SQL Server. Ele não aborda a atualização do sistema operacional que contém o Cluster de Failover do Windows Server (WSFC). Não há suporte para atualização do sistema operacional do Windows que hospeda o cluster de failover para sistemas operacionais anteriores ao Windows Server 2012 R2. Para atualizar um nó de cluster executado no Windows Server 2012 R2, veja [Atualização sem interrupção do sistema operacional do cluster](https://technet.microsoft.com/library/dn850430.aspx)  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Antes de começar, examine as seguintes informações importantes:  
  
-   [Supported Version and Edition Upgrades](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md): verifique se você pode atualizar para o SQL Server 2016 de sua versão do sistema operacional Windows e da versão do SQL Server. Por exemplo, não é possível atualizar diretamente de uma instância do SQL Server 2005 para o [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
-   [Choose a Database Engine Upgrade Method](../../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md): selecione o método e as etapas de atualização apropriados com base em sua análise de atualizações de versão e de edição com suporte e também com base em outros componentes instalados em seu ambiente a fim de atualizar os componentes na ordem correta.  
  
-   [Planejar e testar o plano de atualização do mecanismo de banco de dados](../../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md): examine as notas de versão e os problemas conhecidos da atualização, a lista de verificação pré-atualização, e desenvolva e teste o plano de atualização.  
  
-   [Requisitos de hardware e software para a instalação do SQL Server 2016](../../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md): examine os requisitos de software para a instalação do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Se for necessário um software adicional, instale-o em cada nó antes de começar o processo de atualização para minimizar qualquer tempo de inatividade.  
  
## <a name="rolling-upgrade-best-practices-for-always-on-availability-groups"></a>Práticas recomendadas de atualização sem interrupção de grupos de disponibilidade AlwaysOn  
 As práticas recomendadas a seguir devem ser observadas durante as atualizações de servidor para minimizar o tempo de inatividade e a perda de dados dos grupos de disponibilidade:  
  
-   Antes de iniciar a atualização sem interrupção,  
  
    -   Execute um failover manual em, pelo menos, uma das instâncias de réplica de confirmação síncrona  
  
    -   Proteja os dados executando um backup completo em cada banco de dados de disponibilidade  
  
    -   Execute o comando DBCC CHECKDB em cada banco de dados de disponibilidade  
  
-   Sempre execute a atualização das instâncias remotas da réplica secundária primeiro; depois, das instâncias locais da réplica secundária; por fim, da instância da réplica primária.  
  
-   Os backups não podem ocorrer em um banco de dados que está no processo de ser atualizado.  Antes de atualizar as réplicas secundárias, configure a preferência de backup automatizado para executar backups apenas na réplica primária.  Durante uma atualização de versão, nenhuma réplica será legível ou estará disponível para backups. Durante uma atualização sem versão, você pode configurar backups automatizados para serem executados em réplicas secundárias antes de atualizar a réplica primária.  
  
-   Durante uma atualização de versão, secundários legíveis não podem ser lidos após uma atualização do secundário legível e antes do failover de uma réplica primária para uma secundária atualizada ou a da atualização da réplica primária.  
  
-   Para proteger o grupo de disponibilidade contra failovers indesejados durante o processo de atualização, remova o failover de disponibilidade de todas as réplicas de confirmação síncrona antes de começar.  
  
-   Não atualize a instância da réplica primária antes de fazer failover do grupo de disponibilidade para a instância atualizada com uma réplica secundária primeiro. Do contrário, os aplicativos cliente poderão passar por um longo tempo de inatividade durante a atualização na instância da réplica primária.  
  
-   Sempre faça failover do grupo de disponibilidade em uma instância da réplica secundária de confirmação síncrona. Se você fizer failover para uma instância de réplica secundária de confirmação assíncrona, os bancos de dados sofrerão perda de dados, e a movimentação dos dados será automaticamente suspensa até que você a retome manualmente.  
  
-   Não atualize a instância da réplica primária antes de atualizar qualquer outra instância da réplica secundária. Uma réplica primária atualizada não pode mais enviar logs para nenhuma réplica secundária cuja instância do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] ainda não tenha sido atualizada para a mesma versão. Quando a movimentação dos dados para uma réplica secundária for suspensa, nenhum failover automático poderá ocorrer nessa réplica, e os bancos de dados de disponibilidade ficarão vulneráveis à perda de dados.  
  
-   Antes de fazer failover em um grupo de disponibilidade, verifique se o estado da sincronização do destino do failover é SINCRONIZADO.  
  
## <a name="rolling-upgrade-process"></a>Processo de atualização sem interrupção  
 Na prática, o processo exato dependerá de fatores como a topologia da implantação dos grupos de disponibilidade e o modo de confirmação de cada réplica. Mas, no cenário mais simples, a atualização sem interrupção é um processo de vários estágios que, na sua forma mais simples, envolve as seguintes etapas:  
  
 ![Upgrade de grupo de disponibilidade no cenário HADR](../../../database-engine/availability-groups/windows/media/alwaysonupgrade-ag-hadr.gif "Upgrade de grupo de disponibilidade no cenário HADR")  
  
1.  Remover o failover automático em todas as réplicas de confirmação síncrona  
  
2.  Atualizar todas as instâncias de réplica secundária que executam réplicas secundárias de confirmação assíncrona  
  
3.  Atualizar todas as instâncias de réplica secundária locais que não estão executando a réplica primária  
  
4.  Fazer o failover manual do grupo de disponibilidade em uma réplica secundária local de confirmação síncrona  
  
5.  Atualizar a instância da réplica local que hospedava a réplica primária  
  
6.  Configurar parceiros de failover automático conforme desejado  
  
 Se necessário, você pode executar um failover manual extra para retornar o grupo de disponibilidade à sua configuração original.  
  
## <a name="availability-group-with-one-remote-secondary-replica"></a>Grupo de disponibilidade com uma réplica secundária remota  
 Se você tiver implantado um grupo de disponibilidade somente para recuperação de desastre, talvez seja necessário fazer failover do grupo de disponibilidade para uma réplica secundária de confirmação assíncrona. Essa configuração é ilustrada na figura a seguir:  
  
 ![Upgrade de grupo de disponibilidade no cenário DR](../../../database-engine/availability-groups/windows/media/agupgrade-ag-dr.gif "Upgrade de grupo de disponibilidade no cenário DR")  
  
 Nesse caso, você deve fazer failover do grupo de disponibilidade para uma réplica secundária de confirmação assíncrona durante a atualização sem interrupção. Para evitar a perda de dados, altere o modo de confirmação para confirmação síncrona e aguarde a réplica secundária ser sincronizada para que você possa fazer o failover do grupo de disponibilidade. Portanto, o processo de atualização sem interrupção possivelmente será o seguinte:  
  
1.  Atualizar a instância de réplica secundária no local remoto  
  
2.  Alterar o modo de confirmação para confirmação síncrona  
  
3.  Aguardar até que o estado da sincronização seja SINCRONIZADO  
  
4.  Fazer failover do grupo de disponibilidade para a réplica secundária no local remoto  
  
5.  Atualizar a instância da réplica local (local primário)  
  
6.  Fazer failover do grupo de disponibilidade de volta para o local primário  
  
7.  Alterar o modo de confirmação para confirmação assíncrona  
  
 Como o modo de confirmação síncrona não é uma configuração recomendada para a sincronização de dados em um site remoto, os aplicativos cliente podem observar um aumento imediato na latência do banco de dados depois que a configuração é alterada. Além disso, a execução de um failover fará com que todas as mensagens de log não confirmadas sejam descartadas. A quantidade de mensagens de log descartadas pode ser muito grande devido à alta latência da rede entre os dois sites, fazendo com que os clientes experimentem um alto volume de falha transacional. Você pode minimizar o impacto nos aplicativos cliente fazendo o seguinte:  
  
-   Selecione cuidadosamente uma janela de manutenção durante o baixo tráfego do cliente  
  
-   Durante a atualização do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] no local primário, altere o modo de disponibilidade novamente para confirmação assíncrona e, em seguida, reverta para confirmação síncrona quando estiver pronto para fazer failover para o local primário novamente  
  
## <a name="availability-group-with-failover-cluster-instance-nodes"></a>Grupo de disponibilidade com nós de instância de cluster de failover  
 Se um grupo de disponibilidade contiver nós de FCI (instância de cluster de failover), você deverá atualizar os nós inativos antes de atualizar os nós ativos. A figura a seguir ilustra um cenário de grupo de disponibilidade comum com FCIs para alta disponibilidade local e confirmação assíncrona entre as FCIs de recuperação de desastre remota, e a sequência de upgrade.  
  
 ![Upgrade de grupo de disponibilidade com FCIs](../../../database-engine/availability-groups/windows/media/agupgrade-ag-fci-dr.gif "Upgrade de grupo de disponibilidade com FCIs")  
  
1.  Atualizar REMOTE2  
  
2.  Fazer failover de FCI2 para REMOTE2  
  
3.  Atualizar REMOTE1  
  
4.  Atualizar PRIMARY2  
  
5.  Fazer failover de FCI1 para PRIMARY2  
  
6.  Atualizar PRIMARY1  
  
## <a name="upgrade-update-sql-server-instances-with-multiple-availability-groups"></a>Atualizar instâncias do SQL Server com vários grupos de disponibilidade  
 Se você estiver executando vários grupos de disponibilidade com réplicas primárias em nós de servidor separados (uma configuração Ativo/Ativo), o caminho da atualização envolverá mais etapas de failover para preservar a alta disponibilidade no processo. Suponhamos que você esteja executando três grupos de disponibilidade nos três nós de servidor, conforme mostrado na tabela a seguir, e que todas as réplicas secundárias estejam em execução no modo de confirmação síncrona.  
  
|Grupo de disponibilidade|Node1|Node2|Node3|  
|------------------------|-----------|-----------|-----------|  
|AG1|Primária|||  
|AG2||Primária||  
|AG3|||Primária|  
  
 Talvez seja apropriado na sua situação executar uma atualização sem interrupção com balanceamento de carga na sequência a seguir:  
  
1.  Fazer failover de AG2 para Node3 (para liberar Node2)  
  
2.  Atualizar Node2  
  
3.  Fazer failover de AG1 para Node2 (para liberar Node1)  
  
4.  Atualizar Node1  
  
5.  Fazer failover de AG2 e AG3 para Node1 (para liberar Node3)  
  
6.  Atualizar Node3  
  
7.  Fazer failover de AG3 para Node3  
  
 Essa sequência de atualização tem um tempo de inatividade médio inferior a dois failovers por grupo de disponibilidade. A configuração resultante é mostrada na tabela a seguir.  
  
|Grupo de disponibilidade|Node1|Node2|Node3|  
|------------------------|-----------|-----------|-----------|  
|AG1||Primária||  
|AG2|Primária|||  
|AG3|||Primária|  
  
 Com base na sua implementação, o caminho da atualização pode variar, bem como o tempo de inatividade experimentado pelos aplicativos cliente.  
  
> [!NOTE]  
>  Em muitos casos, após a atualização sem interrupção, você executará failback para a réplica primária original.  
  
## <a name="see-also"></a>Consulte também  
 [Atualizar para o SQL Server 2016 usando o Assistente de Instalação &#40;Instalação&#41;](../../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)   
 [Instalar o SQL Server 2016 do prompt de comando](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)  
  
  

