---
title: Fazer upgrade e atualização de servidores do grupo de disponibilidade com tempo mínimo de inatividade e perda de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: f670af56-dbcc-4309-9119-f919dcad8a65
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8e9be78ff13d39b4cdcaf60516ac20b9a85648d6
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53357071"
---
# <a name="upgrade-and-update-of-availability-group-servers-with-minimal-downtime-and-data-loss"></a>Fazer upgrade e atualização dos servidores de grupo de disponibilidade com tempo de inatividade e perda de dados mínimos
  Ao atualizar ou fazer upgrade de instâncias de servidor do SQL Server 2012 para um service pack ou uma versão mais recente, você pode reduzir o tempo de inatividade de um grupo de disponibilidade para apenas um único failover manual executando uma atualização ou um upgrade sequencial. Para fazer upgrade de versões do SQL Server, essa ação é conhecida como upgrade sem interrupção; para atualizar a versão atual do SQL Server com hotfixes ou service packs, essa ação é conhecida como atualização sem interrupção.  
  
 Este tópico limita a discussão somente a upgrades/atualizações do SQL Server. Para sistema operacional-upgrades/atualizações executados em instâncias do SQL Server altamente disponível, consulte [entre clusters migração de grupos de disponibilidade AlwaysOn para atualizações do sistema operacional](https://msdn.microsoft.com/library/jj873730.aspx)  
  
## <a name="rolling-upgradeupdate-best-practices-for-alwayson-availability-groups"></a>Práticas recomendadas de upgrade/atualização sem interrupção de grupos de disponibilidade AlwaysOn  
 As práticas recomendadas a seguir devem ser observadas durante os upgrades/atualizações de servidor para minimizar o tempo de inatividade e a perda de dados dos grupos de disponibilidade:  
  
-   Antes de iniciar o upgrade/atualização sem interrupção,  
  
    -   Execute um failover manual em, pelo menos, uma das réplicas de confirmação síncrona  
  
    -   Proteja os dados executando um backup completo em cada banco de dados de disponibilidade  
  
    -   Execute o comando DBCC CHECKDB em cada banco de dados de disponibilidade  
  
-   Sempre execute o upgrade/atualização dos nós remotos da réplica secundária primeiro; depois, dos nós locais da réplica secundária; por fim, do nó da réplica primária.  
  
-   Os backups não podem ocorrer em um banco de dados que está no processo de ser atualizado.  Antes de atualizar as réplicas secundárias, configure a preferência de backup automatizado para executar backups apenas na réplica primária.  Antes de atualizar a réplica primária, modifique essa configuração para executar backups apenas nas réplicas secundárias.  
  
-   Para proteger o grupo de disponibilidade contra failovers indesejados durante o processo de upgrade/atualização, remova o failover de disponibilidade de todas as réplicas de confirmação síncrona antes de começar.  
  
-   Não faça upgrade do nó da réplica primária antes de fazer failover do grupo de disponibilidade para um nó submetido a upgrade com uma réplica secundária primeiro. Do contrário, os aplicativos cliente poderão passar por um longo tempo de inatividade durante o upgrade/atualização na réplica primária.  
  
-   Sempre faça failover do grupo de disponibilidade em um nó da réplica secundária de confirmação síncrona. Se você fizer failover para uma réplica secundária de confirmação assíncrona, os bancos de dados sofrerão perda de dados, e a movimentação dos dados será automaticamente suspensa até que você a retome manualmente.  
  
-   Não faça upgrade/atualização do nó da réplica primária antes de fazer upgrade/atualização de qualquer outro nó da réplica secundária. Uma réplica primária submetida a upgrade não pode mais enviar logs para nenhuma réplica secundária que ainda não tenha sido submetida a upgrade para a mesma versão. Quando a movimentação dos dados para uma réplica secundária for suspensa, nenhum failover automático poderá ocorrer nessa réplica, e os bancos de dados de disponibilidade ficarão vulneráveis à perda de dados.  
  
-   Antes de fazer failover em um grupo de disponibilidade, verifique se o estado da sincronização do destino do failover é SINCRONIZADO.  
  
## <a name="rolling-upgradeupdate-process"></a>Processo de upgrade/atualização sem interrupção  
 Na prática, o processo exato dependerá de fatores como a topologia da implantação dos grupos de disponibilidade e o modo de confirmação de cada réplica. Mas, no cenário mais simples, o upgrade/atualização sem interrupção é um processo de vários estágios que, na sua forma mais simples, envolve as seguintes etapas:  
  
 ![Upgrade de grupo de disponibilidade no cenário HADR](../../media/alwaysonupgrade-ag-hadr.gif "Upgrade de grupo de disponibilidade no cenário HADR")  
  
1.  Remover o failover automático em todas as réplicas de confirmação síncrona  
  
2.  Fazer upgrade/atualização de todas as instâncias de servidor remotas que executam réplicas secundárias de confirmação assíncrona  
  
3.  Fazer upgrade/atualização de todas as instâncias de servidor locais que não estão executando a réplica primária  
  
4.  Fazer o failover manual do grupo de disponibilidade em uma réplica secundária de confirmação síncrona  
  
5.  Fazer upgrade/atualização da instância de servidor que hospedava a réplica primária  
  
6.  Configurar parceiros de failover automático conforme desejado  
  
 Se necessário, você pode executar um failover manual extra para retornar o grupo de disponibilidade à sua configuração original.  
  
## <a name="availability-group-with-one-remote-secondary-replica"></a>Grupo de disponibilidade com uma réplica secundária remota  
 Se você tiver implantado um grupo de disponibilidade somente para recuperação de desastre, talvez seja necessário fazer failover do grupo de disponibilidade para uma réplica secundária de confirmação assíncrona. Essa configuração é ilustrada na figura a seguir:  
  
 ![Upgrade de grupo de disponibilidade no cenário DR](../../media/agupgrade-ag-dr.gif "Upgrade de grupo de disponibilidade no cenário DR")  
  
 Nesse caso, você deve fazer failover do grupo de disponibilidade para uma réplica secundária de confirmação assíncrona durante o upgrade/atualização sem interrupção. Para evitar a perda de dados, altere o modo de confirmação para confirmação síncrona e aguarde a réplica secundária ser sincronizada para que você possa fazer o failover do grupo de disponibilidade. Portanto, o processo de upgrade/atualização sem interrupção possivelmente será o seguinte:  
  
1.  Fazer o upgrade/atualização do servidor remoto  
  
2.  Alterar o modo de confirmação para confirmação síncrona  
  
3.  Aguardar até que o estado da sincronização seja SINCRONIZADO  
  
4.  Fazer failover do grupo de disponibilidade para o site remoto  
  
5.  Fazer o upgrade/atualização do servidor local (site primário)  
  
6.  Fazer failover do grupo de disponibilidade para o site primário  
  
7.  Alterar o modo de confirmação para confirmação assíncrona  
  
 Como o modo de confirmação síncrona não é uma configuração recomendada para a sincronização de dados em um site remoto, os aplicativos cliente podem observar um aumento imediato na latência do banco de dados depois que a configuração é alterada. Além disso, a execução de um failover fará com que todas as mensagens de log não confirmadas sejam descartadas. A quantidade de mensagens de log descartadas pode ser muito grande devido à alta latência da rede entre os dois sites, fazendo com que os clientes experimentem um alto volume de falha transacional. Você pode minimizar o impacto nos aplicativos cliente fazendo o seguinte:  
  
-   Selecione cuidadosamente uma janela de manutenção durante o baixo tráfego do cliente  
  
-   Durante o upgrade/atualização do SQL Server no site primário, altere o modo de disponibilidade novamente para confirmação assíncrona e, em seguida, reverta para confirmação síncrona quando estiver pronto para fazer failover para o site primário novamente  
  
## <a name="availability-group-with-failover-cluster-instance-nodes"></a>Grupo de disponibilidade com nós de instância de cluster de failover  
 Se um grupo de disponibilidade contiver nós de FCI (instância de cluster de failover), você deverá fazer upgrade/atualização dos nós inativos antes de fazer upgrade/atualização dos nós ativos. A figura a seguir ilustra um cenário de grupo de disponibilidade comum com FCIs para alta disponibilidade local e confirmação assíncrona entre as FCIs de recuperação de desastre remota, e a sequência de upgrade.  
  
 ![Upgrade de grupo de disponibilidade com FCIs](../../media/agupgrade-ag-fci-dr.gif "Upgrade de grupo de disponibilidade com FCIs")  
  
1.  Fazer upgrade/atualização de REMOTE2  
  
2.  Fazer failover de FCI2 para REMOTE2  
  
3.  Fazer upgrade/atualização de REMOTE1  
  
4.  Fazer upgrade/atualização de PRIMARY2  
  
5.  Fazer failover de FCI1 para PRIMARY2  
  
6.  Fazer upgrade/atualização de PRIMARY1  
  
## <a name="upgradeupdate-sql-server-instances-with-multiple-availability-groups"></a>Fazer upgrade/atualização de instâncias do SQL Server com vários grupos de disponibilidade  
 Se você estiver executando vários grupos de disponibilidade com réplicas primárias em nós de servidor separados (uma configuração Ativo/Ativo), o caminho do upgrade/atualização envolverá mais etapas de failover para preservar a alta disponibilidade no processo. Suponhamos que você esteja executando três grupos de disponibilidade nos três nós de servidor, conforme mostrado na tabela a seguir, e que todas as réplicas secundárias estejam em execução no modo de confirmação síncrona.  
  
|Grupo de disponibilidade|Node1|Node2|Node3|  
|------------------------|-----------|-----------|-----------|  
|AG1|Primária|||  
|AG2||Primária||  
|AG3|||Primária|  
  
 Talvez seja apropriado na sua situação executar um upgrade/atualização sem interrupção com balanceamento de carga na sequência a seguir:  
  
1.  Fazer failover de AG2 para Node3 (para liberar Node2)  
  
2.  Fazer upgrade/atualização de Node2  
  
3.  Fazer failover de AG1 para Node2 (para liberar Node1)  
  
4.  Fazer upgrade/atualização de Node1  
  
5.  Fazer failover de AG2 e AG3 para Node1 (para liberar Node3)  
  
6.  Fazer upgrade/atualização de Node3  
  
7.  Fazer failover de AG3 para Node3  
  
 Essa sequência de upgrade/atualização tem um tempo de inatividade médio inferior a dois failovers por grupo de disponibilidade. A configuração resultante é mostrada na tabela a seguir.  
  
|Grupo de disponibilidade|Node1|Node2|Node3|  
|------------------------|-----------|-----------|-----------|  
|AG1||Primária||  
|AG2|Primária|||  
|AG3|||Primária|  
  
 Com base na sua implementação, o caminho do upgrade/atualização pode variar, bem como o tempo de inatividade experimentado pelos aplicativos cliente.  
  
  
