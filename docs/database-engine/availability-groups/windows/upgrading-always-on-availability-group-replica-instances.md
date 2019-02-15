---
title: Fazer upgrade das instâncias de réplica do Grupo de Disponibilidade AlwaysOn | Microsoft Docs
ms.custom: ''
ms.date: 01/10/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: f670af56-dbcc-4309-9119-f919dcad8a65
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 27e2a4939ebe376408aad64414503a8c9edd46ce
ms.sourcegitcommit: 1510d9fce125e5b13e181f8e32d6f6fbe6e7c7fe
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2019
ms.locfileid: "55771342"
---
# <a name="upgrading-always-on-availability-group-replica-instances"></a>Atualizar instâncias de réplica do Grupo de Disponibilidade AlwaysOn
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Ao atualizar uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospeda um AG (Grupo de Disponibilidade) do AlwaysOn para uma nova versão do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], para um novo service pack ou atualização cumulativa do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], ou ao instalar um novo service pack ou atualização cumulativa do Windows, você poderá reduzir o tempo de inatividade para a réplica primária para um único failover manual executando uma atualização sem interrupção (ou dois failovers manuais em caso de failback para a primária original). Durante o processo de atualização, uma réplica secundária não estará disponível para failover ou para operações somente leitura e, depois da atualização, poderá levar algum tempo para que a réplica secundária fique atualizada com o nó da réplica primária, dependendo do volume de atividade no nó da réplica primária (portanto, espere alto tráfego de rede). Além disso, lembre-se de que depois do failover inicial para uma réplica secundária executando uma versão mais recente do SQL Server, os bancos de dados nesse Grupo de Disponibilidade passarão por um processo de atualização para colocá-los na versão mais recente. Durante esse tempo, não haverá nenhuma réplica legível para nenhum desses bancos de dados. O tempo de inatividade depois do failover inicial dependerá do número de bancos de dados no Grupo de Disponibilidade. Se você planeja realizar o failback no primário original, essa etapa não será repetida ao realizar o failback.
  
>[!NOTE]  
>Este artigo limita a discussão à atualização do próprio SQL Server. Ele não aborda a atualização do sistema operacional que contém o Cluster de Failover do Windows Server (WSFC). Não há suporte para atualização do sistema operacional do Windows que hospeda o cluster de failover para sistemas operacionais anteriores ao Windows Server 2012 R2. Para atualizar um nó de cluster em execução no Windows Server 2012 R2, confira o artigo [Atualização sem interrupção do Sistema Operacional do Cluster](https://docs.microsoft.com/windows-server/failover-clustering/cluster-operating-system-rolling-upgrade).  
  
## <a name="prerequisites"></a>Prerequisites  
Antes de começar, examine as seguintes informações importantes:  
  
- [Atualizações compatíveis de versão e edição](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md): Verifique se você pode atualizar para o SQL Server 2016 de sua versão do sistema operacional Windows e da versão do SQL Server. Por exemplo, não é possível atualizar diretamente de uma instância do SQL Server 2005 para o [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
- [Escolher um método de atualização do mecanismo de banco de dados](../../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md): Para atualizar na ordem correta, selecione o método e as etapas de atualização apropriados com base em sua análise de atualizações de versão e de edição compatíveis e também com base em outros componentes instalados em seu ambiente.  
  
- [Planejar e testar o plano de atualização do mecanismo de banco de dados](../../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md): Analise as notas de versão e os problemas conhecidos da atualização, a lista de verificação pré-atualização, e desenvolva e teste o plano de atualização.  
  
- [Requisitos de hardware e software para a instalação do SQL Server](../../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md):  Analise os requisitos de software para a instalação do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Se for necessário um software adicional, instale-o em cada nó antes de começar o processo de atualização para minimizar qualquer tempo de inatividade.  

- [Verifique se a replicação ou captura de dados de alterações é usada para qualquer banco de dados do grupo de disponibilidade](#special-steps-for-change-data-capture-or-replication): Se qualquer banco de dados de disponibilidade estiver habilitado para CDA (captura de dados de alterações), conclua estas [instruções](#special-steps-for-change-data-capture-or-replication).

>[!NOTE]  
>Não há suporte para a combinação de versões das instâncias do SQL Server no mesmo AG fora de uma atualização sem interrupção, que atualiza as réplicas adequadamente. Uma versão posterior de uma instância do SQL Server não pode ser adicionada como uma nova réplica a um AG existente. Por exemplo, uma réplica do SQL Server 2017 não pode ser adicionada a um AG existente do SQL Server 2016. Para migrar para uma nova versão da instância do SQL Server usando AGs, o único método com suporte é um AG distribuído, que está no SQL Server 2016 Enterprise Edition ou posterior.

## <a name="rolling-upgrade-basics-for-always-on-ags"></a>Noções básicas de atualização sem interrupção para AGs do AlwaysOn  
Observe as diretrizes a seguir ao realizar atualizações de servidor para minimizar o tempo de inatividade e a perda de dados dos seus AGs:  
  
- Antes de iniciar a atualização sem interrupção,  
  
    - Execute um failover manual em, pelo menos, uma das instâncias de réplica de confirmação síncrona  
  
    - Proteja os dados executando um backup completo em cada banco de dados de disponibilidade  
  
    - Execute o comando DBCC CHECKDB em cada banco de dados de disponibilidade  
  
-   Sempre execute a atualização das instâncias remotas da réplica secundária primeiro; depois, das instâncias locais da réplica secundária; por fim, da instância da réplica primária.  
  
-   Os backups não podem ocorrer em um banco de dados que está no processo de ser atualizado.  Antes de atualizar as réplicas secundárias, configure a preferência de backup automatizado para executar backups apenas na réplica primária.  Durante uma atualização de versão, nenhuma réplica será legível ou estará disponível para backups. Durante uma atualização sem versão, você pode configurar backups automatizados para serem executados em réplicas secundárias antes de atualizar a réplica primária.  
  
-   Durante uma atualização de versão, secundários legíveis não podem ser lidos após uma atualização do secundário legível e antes do failover de uma réplica primária para uma secundária atualizada ou a da atualização da réplica primária.  
  
-   Para proteger o AG contra failovers indesejados durante o processo de atualização, remova o failover de disponibilidade de todas as réplicas de confirmação síncrona antes de começar.  
  
-   Não atualize a instância da réplica primária antes de fazer failover do AG para a instância atualizada com uma réplica secundária primeiro. Do contrário, os aplicativos cliente poderão passar por um longo tempo de inatividade durante a atualização na instância da réplica primária.  
  
-   Sempre faça failover do AG em uma instância da réplica secundária de confirmação síncrona. Se você fizer failover para uma instância de réplica secundária de confirmação assíncrona, os bancos de dados estarão vulneráveis a perda de dados e a movimentação de dados será automaticamente suspensa até que você a retome manualmente.  
  
-   Não atualize a instância da réplica primária antes de atualizar qualquer outra instância da réplica secundária. Uma réplica primária atualizada não pode mais enviar logs para nenhuma réplica secundária cuja instância do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] ainda não tenha sido atualizada para a mesma versão. Quando a movimentação dos dados para uma réplica secundária for suspensa, nenhum failover automático poderá ocorrer nessa réplica, e os bancos de dados de disponibilidade ficarão vulneráveis à perda de dados.  
  
-   Antes de fazer failover em um GA, verifique se o estado da sincronização do destino do failover é SINCRONIZADO.  

  > [!WARNING]
  > Instalar uma nova instância ou nova versão do SQL Server para um servidor que tem uma versão mais antiga do SQL Server instalado pode inadvertidamente **causar uma interrupção de qualquer grupo de disponibilidade que esteja hospedado pela versão mais antiga do SQL Server.** Isso ocorre porque durante a instalação da instância ou versão do SQL Server, o módulo de alta disponibilidade do SQL Server (RHS.EXE) é atualizado. Isso resulta em uma interrupção temporária de seus grupos de disponibilidade existentes na função primária no servidor. Portanto, é altamente recomendável que você execute uma das opções a seguir ao instalar uma versão mais recente do SQL Server para um sistema que já está hospedando uma versão mais antiga do SQL Server com um grupo de disponibilidade:
  > - Instalar a nova versão do SQL Server durante uma janela de manutenção. 
  > - Fazer failover do grupo de disponibilidade na réplica secundária, de modo que não seja a primária durante a instalação da nova instância do SQL Server. 
  
## <a name="rolling-upgrade-process"></a>Processo de atualização sem interrupção  
 Na prática, o processo exato depende de fatores como a topologia da implantação dos AGs e o modo de confirmação de cada réplica. Mas, no cenário mais simples, a atualização sem interrupção é um processo de vários estágios que, na sua forma mais simples, envolve as seguintes etapas:  
  
 ![Atualização do AG no cenário HADR](../../../database-engine/availability-groups/windows/media/alwaysonupgrade-ag-hadr.gif "Atualização do AG no cenário HADR")  
  
1.  Remover o failover automático em todas as réplicas de confirmação síncrona  
  
2.  Atualizar todas as instâncias de réplica secundária que executam réplicas secundárias de confirmação assíncrona  
  
3.  Atualizar todas as instâncias de réplica secundária locais que não estão executando a réplica primária  
  
4.  Fazer o failover manual do AG em uma réplica secundária local de confirmação síncrona  
  
5.  Atualizar a instância da réplica local que hospedava a réplica primária  
  
6.  Configurar parceiros de failover automático conforme desejado  
  
 Se necessário, você pode executar um failover manual extra para retornar o AG à sua configuração original.  
  
## <a name="ag-with-one-remote-secondary-replica"></a>AG com uma réplica secundária remota  
 Se você tiver implantado um AG somente para recuperação de desastre, talvez seja necessário fazer failover do AG para uma réplica secundária de confirmação assíncrona. Essa configuração é ilustrada na figura a seguir:  
  
 ![Atualização do AG no cenário DR](../../../database-engine/availability-groups/windows/media/agupgrade-ag-dr.gif "Atualização do AG no cenário DR")  
  
 Nesse caso, você deve fazer failover do AG para uma réplica secundária de confirmação assíncrona durante a atualização sem interrupção. Para evitar a perda de dados, altere o modo de confirmação para confirmação síncrona e aguarde a réplica secundária ser sincronizada para que você possa fazer o failover do AG. Portanto, o processo de atualização sem interrupção possivelmente será o seguinte:  
  
1.  Atualizar a instância de réplica secundária no local remoto  
  
2.  Alterar o modo de confirmação para confirmação síncrona  
  
3.  Aguardar até que o estado da sincronização seja SINCRONIZADO  
  
4.  Fazer failover do AG para a réplica secundária no site remoto  
  
5.  Atualizar a instância da réplica local (local primário)  
  
6.  Fazer failover do AG de volta para o local primário  
  
7.  Alterar o modo de confirmação para confirmação assíncrona  
  
 Como o modo de confirmação síncrona não é uma configuração recomendada para a sincronização de dados em um site remoto, os aplicativos cliente podem observar um aumento imediato na latência do banco de dados depois que a configuração é alterada. Além disso, a execução de um failover fará com que todas as mensagens de log não confirmadas sejam descartadas. O número de mensagens de log descartadas pode ser significante devido à alta latência da rede entre os dois locais, fazendo com que os clientes experimentem um alto volume de falha transacional. Você pode minimizar o impacto nos aplicativos cliente ao executar as seguintes ações:  
  
-   Selecione cuidadosamente uma janela de manutenção durante o baixo tráfego do cliente  
  
-   Durante a atualização do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] no local primário, altere o modo de disponibilidade novamente para confirmação assíncrona e, em seguida, reverta para confirmação síncrona quando estiver pronto para fazer failover para o local primário novamente  
  
## <a name="ag-with-failover-cluster-instance-nodes"></a>AG com nós da instância de cluster de failover  
 Se um AG contiver nós de FCI (instância de cluster de failover), você deverá atualizar os nós inativos antes de atualizar os nós ativos. A figura a seguir ilustra um cenário de AG comum com FCIs para alta disponibilidade local e confirmação assíncrona entre as FCIs de recuperação de desastre remota e a sequência de upgrade.  
  
 ![Atualização do AG com FCIs](../../../database-engine/availability-groups/windows/media/agupgrade-ag-fci-dr.gif "Atualização do AG com FCIs")  
  
1.  Atualizar REMOTE2  
  
2.  Fazer failover de FCI2 para REMOTE2  
  
3.  Atualizar REMOTE1  
  
4.  Atualizar PRIMARY2  
  
5.  Fazer failover de FCI1 para PRIMARY2  
  
6.  Atualizar PRIMARY1  
  
## <a name="upgrade-or-update-sql-server-instances-with-multiple-ags"></a>Atualizar instâncias do SQL Server com vários AGs  
 Se você estiver executando vários AGs com réplicas primárias em nós de servidor separados (uma configuração Ativo/Ativo), o caminho da atualização envolverá mais etapas de failover para preservar a alta disponibilidade no processo. Suponhamos que você esteja executando três AGs nos três nós de servidor, com todas as réplicas no modo de confirmação síncrona na tabela a seguir:  
  
|AG|Node1|Node2|Node3|  
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
  
 Essa sequência de atualização tem um tempo de inatividade médio inferior a dois failovers por AG. A configuração resultante é mostrada na tabela a seguir.  
  
|AG|Node1|Node2|Node3|  
|------------------------|-----------|-----------|-----------|  
|AG1||Primária||  
|AG2|Primária|||  
|AG3|||Primária|  
  
 Com base na sua implementação, o caminho da atualização pode variar, bem como o tempo de inatividade experimentado pelos aplicativos cliente.  
  
> [!NOTE]  
>  Em muitos casos, após a atualização sem interrupção, você executará o failback para a réplica primária original. 

## <a name="rolling-upgrade-of-a-distributed-availability-group"></a>Atualização sem interrupção de um grupo de disponibilidade distribuído
Para executar uma atualização sem interrupção de um grupo de disponibilidade distribuído, atualize primeiro todas as réplicas secundárias. Em seguida, faça failover do encaminhador e atualize a última instância restante do segundo grupo de disponibilidade. Depois que todas as réplicas tiverem sido atualizadas, faça failover do primário global e atualize a última instância restante do primeiro grupo de disponibilidade. É fornecido abaixo um diagrama detalhado com etapas. 

 Com base na sua implementação, o caminho da atualização pode variar, bem como o tempo de inatividade experimentado pelos aplicativos cliente.  
  
> [!NOTE]  
>  Em muitos casos, após a atualização sem interrupção, você executará o failback para as réplicas primárias originais. 

### <a name="general-steps-to-upgrade-a-distributed-availability-group"></a>Etapas gerais para atualizar um grupo de disponibilidade distribuído
1. Faça backup de todos os bancos de dados, incluindo os bancos de dados do sistema e os que participam do grupo de disponibilidade. 
2. Atualize e reinicie todas as réplicas secundárias do segundo grupo de disponibilidade (o downstream). 
3. Atualize e reinicie todas as réplicas secundárias do primeiro grupo de disponibilidade (o upstream). 
4. Faça failover do encaminhador primário para uma réplica secundária atualizada do grupo de disponibilidade secundário.
5. Aguarde a sincronização de dados. Os bancos de dados devem ser mostrados como sincronizados em todas as réplicas de confirmação síncrona, e o primário global deve ser sincronizado com o encaminhador.  
6. Atualize e reinicie a última instância restante do grupo de disponibilidade secundário. 
7. Faça failover do primário global para um secundário atualizado do primeiro grupo de disponibilidade.  
8. Atualize a última instância restante do grupo de disponibilidade primário.
9. Reinicie o servidor recém-atualizado. 
10. (opcional) Execute failback de ambos os grupos de disponibilidade para suas réplicas primárias originais.  

>[!IMPORTANT]
>- Verifique a sincronização entre cada etapa. Antes de passar para a próxima etapa, confirme que suas réplicas de confirmação síncrona estão sincronizadas dentro do grupo de disponibilidade e que seu primário global está sincronizado com o encaminhador no grupo de disponibilidade distribuído. 
>- **Recomendação**: Sempre que você verificar a sincronização, atualize o nó do banco de dados e o nó do grupo de disponibilidade distribuído no SQL Server Management Studio. Depois de tudo for sincronizado, salve uma captura de tela dos estados de cada réplica. Isso ajudará você a manter o controle de qual etapa você está, a fornecer provas de que tudo estava funcionando corretamente antes da próxima etapa e a auxiliar na solução de problemas se algo der errado. 


### <a name="diagram-example-for-a-rolling-upgrade-of-a-distributed-availability-group"></a>Diagrama de exemplo de uma atualização sem interrupção de um grupo de disponibilidade distribuído

| grupo de disponibilidade | Réplica primária | Réplica secundária|
| :------ | :----------------------------- |  :------ |
| AG1 | NODE1\SQLAG | NODE2\SQLAG|
| AG2 | NODE3\SQLAG | NODE4\SQLAG|
| Distributedag| AG1 (global) | AG2 (encaminhador) |
| &nbsp; | &nbsp; | &nbsp; |

![Exemplo de diagrama para o grupo de disponibilidade distribuído](media/upgrading-always-on-availability-group-replica-instances/rolling-upgrade-dag-diagram.png)


As etapas para atualizar as instâncias neste diagrama: 

1. Faça backup de todos os bancos de dados, incluindo os bancos de dados do sistema e os que participam do grupo de disponibilidade. 
2. Atualize NODE4\SQLAG (secundário do AG2) e reinicie o servidor. 
3. Atualize NODE2\SQLAG (secundário do AG1) e reinicie o servidor. 
4. Faça failover do AG2 do NODE3\SQLAG ao NODE4\SQLAG. 
5. Atualize o NODE3\SQLAG e reinicie o servidor. 
6. Faça failover do AG1 do NODE1\SQLAG ao NODE2\SQLAG. 
7. Atualize o NODE1\SQLAG e reinicie o servidor. 
8. (opcional) Execute failback para as réplicas primárias originais.
    1. Faça failover do AG2 do NODE4\SQLAG de volta para o NODE3\SQLAG.  
    2. Faça failover do AG1 do NODE2\SQLAG de volta para o NODE1\SQLAG. 

Se uma terceira réplica existisse em cada grupo de disponibilidade, ela seria atualizada antes de NODE3\SQLAG e de NODE1\SQLAG. 

>[!IMPORTANT]
>- Verifique a sincronização entre cada etapa. Antes de passar para a próxima etapa, confirme que suas réplicas de confirmação síncrona estão sincronizadas dentro do grupo de disponibilidade e que seu primário global está sincronizado com o encaminhador no grupo de disponibilidade distribuído. 
>- Recomendação: Sempre que você verificar a sincronização, atualize o nó do banco de dados e o nó do grupo de disponibilidade distribuído no SQL Server Management Studio. Após tudo ser sincronizado, tire uma captura de tela e salve-a. Isso ajudará você a manter o controle de qual etapa você está, a fornecer provas de que tudo estava funcionando corretamente antes da próxima etapa e a auxiliar na solução de problemas se algo der errado. 


## <a name="special-steps-for-change-data-capture-or-replication"></a>Etapas especiais para replicação ou captura de dados de alteração

Dependendo da atualização aplicada, outras etapas podem ser necessárias para bancos de dados de réplica de AG que são habilitados para a replicação ou captura de dados de alteração. Consulte as notas de versão da atualização para determinar se as etapas a seguir são necessárias:

1. Atualize todas as réplicas secundárias.

1. Depois de atualizar todas as réplicas secundárias, faça o failover no AG para a instância atualizada. 

1. Execute o seguinte Transact-SQL na instância que hospeda a réplica primária:

   ```sql
   EXECUTE [master].[sys].[sp_vupgrade_replication];
   ```

   >[!NOTE]
   >Este comando pode levar vários minutos para ser executado. 

1. Atualize a instância que foi originalmente a réplica primária.

Para obter mais informações, consulte [Funcionalidade de CDC pode falhar após a atualização para a atualização cumulativa mais recente](https://blogs.msdn.microsoft.com/sql_server_team/cdc-functionality-may-break-after-upgrading-to-the-latest-cu-for-sql-server-2012-2014-and-2016/).

  
## <a name="see-also"></a>Consulte Também  
 [Atualizar para o SQL Server 2016 usando o Assistente de Instalação &#40;Instalação&#41;](../../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)   

 [Instalar o SQL Server 2016 do prompt de comando](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)  
  
  
