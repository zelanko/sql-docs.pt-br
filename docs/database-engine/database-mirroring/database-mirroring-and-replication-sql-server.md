---
title: Espelhamento e replicação de banco de dados (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.component: database-mirroring
ms.reviewer: ''
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- replication [SQL Server], database mirroring and
ms.assetid: 82796217-02e2-4bc5-9ab5-218bae11a2d6
caps.latest.revision: 39
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9cc2c02b5d2f8f75607ed5afe555bbffc3b77c34
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="database-mirroring-and-replication-sql-server"></a>Espelhamento e replicação de banco de dados (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O espelhamento do banco de dados pode ser usado junto com a replicação para aprimorar a disponibilidade ao banco de dados de publicação. O espelhamento do banco de dados compreende duas cópias de um único banco de dados que geralmente reside em computadores diferentes. Em determinado momento, apenas uma cópia do banco de dados está atualmente disponível aos clientes. Essa cópia é conhecida como o banco de dados principal. As atualizações realizadas pelos clientes no banco de dados principal são aplicadas à outra cópia do banco de dados, conhecida como banco de dados espelho. O espelhamento envolve a aplicação do log de transações de cada inserção, atualização ou exclusão efetuada no banco de dados principal, para o banco de dados espelho.  
  
 O failover de replicação para um espelho tem o suporte total para os bancos de dados de publicação, com suporte limitado para bancos de dados de assinatura. O espelhamento de banco de dados não tem suporte para bancos de dados de distribuição. Para obter informações sobre como recuperar um banco de dados de distribuição ou banco de dados de assinatura sem precisar reconfigurar a replicação, veja [Fazer backup e restaurar bancos de dados replicados](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md).   
  
> [!NOTE]  
>  Após um failover, o espelho se torna o principal. Nesse tópico, "principal" e "espelho" sempre se referem ao principal original e ao espelho.  
  
## <a name="requirements-and-considerations-for-using-replication-with-database-mirroring"></a>Exigências e considerações no uso de replicação com espelhamento do banco de dados  
 Esteja atento quanto às exigências e às considerações a seguir, quando for usar a replicação com o espelhamento do banco de dados:  
  
-   O principal e o espelho devem compartilhar um Distribuidor. Recomendamos que esse seja um Distribuidor remoto que ofereça tolerância maior a falhas, caso o Publicador tenha um failover não programado.  
  
-   A replicação dá suporte ao espelhamento do banco de dados de publicação para a replicação de mesclagem e para a replicação transacional com Assinantes somente leitura ou Assinantes de atualização em fila. Não há suporte para Assinantes de atualização imediata, Publicadores Oracle, Publicadores em uma topologia ponto a ponto e republicação.  
  
-   Os metadados e os objetos que existem fora do banco de dados não são copiados para o espelho, inclusive logons, trabalhos, servidores vinculados, etc. Se precisar dos metadados e dos objetos no espelho, será preciso copiá-los manualmente. Para obter mais informações, veja [Administração de logons e trabalhos após a troca de funções &#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md).  
  
## <a name="configuring-replication-with-database-mirroring"></a>Configurando a replicação do espelhamento do banco de dados  
 A configuração da replicação e do espelhamento do banco de dados compreende cinco etapas. Cada etapa está descrita com mais detalhes na próxima seção.  
  
1.  Configurar o Publicador.  
  
2.  Configure o espelhamento do banco de dados  
  
3.  Configurar o espelho para usar o mesmo Distribuidor como principal.  
  
4.  Configurar os agentes de replicação para failover.  
  
5.  Adicione o principal e o espelho ao Replication Monitor.  
  
 As Etapas 1 e 2 podem ser realizadas também em ordem oposta.  
  
#### <a name="to-configure-database-mirroring-for-a-publication-database"></a>Para configurar o espelhamento de banco de dados para um banco de dados de publicação  
  
1.  Configure o Publicador:  
  
    1.  Recomendamos o uso de um Distribuidor remoto. Para obter mais informações sobre como configurar a distribuição, veja [Configurar a distribuição](../../relational-databases/replication/configure-distribution.md).  
  
    2.  Você pode habilitar um banco de dados para instantâneos e publicações transacionais e/ou publicações de mesclagem. Para bancos de dados espelhados com mais de um tipo de publicação, é necessário habilitar os dois tipos de banco de dados no mesmo nó, usando [sp_replicationdboption](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md). Por exemplo, você pode executar as chamadas do procedimento armazenado a seguir, no principal:  
  
        ```  
        exec sp_replicationdboption @dbname='<PublicationDatabase>', @optname='publish', @value=true;  
        exec sp_replicationdboption @dbname='<PublicationDatabase>', @optname='mergepublish', @value=true;  
        ```  
  
         Para obter mais informações sobre como criar publicações, veja [Publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md).  
  
2.  Configure o espelhamento do banco de dados Para obter mais informações, veja [Estabelecer uma sessão de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md) e [Configurando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md).  
  
3.  Configure a distribuição para o espelho. Especifique o nome do espelho como Publicador e especifique o mesmo Distribuidor e a pasta de instantâneos usada pelo principal. Por exemplo, caso esteja configurando a replicação com procedimentos armazenados, execute [sp_adddistpublisher](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md) no Distribuidor e execute [sp_adddistributor](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md) no espelho. Para **sp_adddistpublisher**:  
  
    -   Defina o valor do parâmetro **@publisher** para o nome de rede do espelho.  
  
    -   Defina o valor do parâmetro **@working_directory** para a pasta de instantâneos usada pelo principal.  
  
4.  Especifique o nome do espelho para o parâmetro do agente **– PublisherFailoverPartner** . Esse parâmetro de agente é exigido pelos seguintes agentes para identificar o espelho, após o failover:  
  
    -   Snapshot Agent (para todas as publicações)  
  
    -   Log Reader Agent (para todas as publicações transacionais)  
  
    -   Queue Reader Agent (para publicações transacionais que dão suporte às assinaturas de atualização em fila).  
  
    -   Merge Agent (para assinaturas de mesclagem)  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ouvinte de replicação (replisapi.dll: para assinaturas de mesclagem sincronizadas usando a sincronização da Web)  
  
    -   SQL Merge ActiveX Control (para assinaturas de mesclagem sincronizadas com o controle)  
  
     O Distribution Agent e o Distribution ActiveX Control não têm esse parâmetro porque não se conectam ao Publicador.  
  
     As alterações do parâmetro de agente entrarão em vigor na próxima vez o agente for iniciado. Se o agente ficar executando continuamente, será necessário parar e reiniciar o agente. Os parâmetros de agente podem ser especificados em perfis de agente e no prompt de comando. Para obter mais informações, consulte:  
  
    -   [Exibir e modificar parâmetros do prompt de comando de agentes de replicação &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Conceitos dos executáveis do Replication Agent](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
     Recomendamos adicionar o **–PublisherFailoverPartner** a um perfil de agente e especificar o nome do espelho no perfil. Por exemplo, se você estiver configurando uma replicação com procedimentos armazenados:  
  
    ```  
    -- Execute sp_help_agent_profile in the context of the distribution database to get the list of profiles.  
    -- Select the profile id of the profile that needs to be updated from the result set.  
    -- In the agent_type column returned by sp_help_agent_profile:   
    -- 1 = Snapshot Agent; 2 = Log Reader Agent; 3 = Distribution Agent; 4 = Merge Agent; 9 = Queue Reader Agent.  
  
    exec sp_help_agent_profile;  
  
    -- Setting the -PublisherFailoverPartner parameter in the default Snapshot Agent profile (profile 1).  
    -- Execute sp_add_agent_parameter in the context of the distribution database.  
    exec sp_add_agent_parameter @profile_id = 1, @parameter_name = N'-PublisherFailoverPartner', @parameter_value = N'<Failover Partner Name>';  
  
    -- Setting the -PublisherFailoverPartner parameter in the default Merge Agent profile (profile 6).  
    -- Execute sp_add_agent_parameter in the context of the distribution database.  
    exec sp_add_agent_parameter @profile_id = 6, @parameter_name = N'-PublisherFailoverPartner', @parameter_value = N'<Failover Partner Name>';  
    ```  
  
5.  Adicione o principal e o espelho ao Replication Monitor. Para obter mais informações, veja [Adicionar e remover Publicadores do Replication Monitor](../../relational-databases/replication/monitor/add-and-remove-publishers-from-replication-monitor.md).  
  
## <a name="maintaining-a-mirrored-publication-database"></a>Mantendo um banco de dados espelhado  
 Manter um banco de dados de publicação espelhado é praticamente o mesmo que manter um banco de dados não espelhado, com as considerações a seguir:  
  
-   A administração e o monitoramento devem ocorrer no servidor ativo. No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], as publicações aparecem sob a pasta **Publicações Locais** , somente para o servidor ativo. Por exemplo, se um failover for realizado no espelho, as publicações serão exibidas no espelho; mas não, no principal. Se ocorrer um failover de banco de dados no espelho, talvez seja necessário atualizar manualmente o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e o Replication Monitor, para que a alteração seja refletida.  
  
-   O Replication Monitor exibe os nós do Publicador na árvore de objetos para ambos, o principal e o espelho. Se o principal for o servidor ativo, as informações da publicação só serão exibidas sob o nó principal, no Replication Monitor.  
  
     Se o espelho for o servidor ativo:  
  
    -   Se ocorrer um erro em um agente, esse erro será indicado somente no nó principal, não no nó espelho.  
  
    -   Se o principal estiver indisponível, os nós principal e espelho exibem listas de publicações idênticas. O monitoramento deve ser realizado nas publicações sob o nó espelho.  
  
-   Ao usar os procedimentos armazenados ou RMO (Replication Management Objects) para gerenciar a replicação no espelho, nos casos em que você especifica o nome do Publicador, especifique o nome da instância na qual o banco de dados foi habilitado para a replicação. Para determinar o nome apropriado, use a função [publishingservername](../../t-sql/functions/replication-functions-publishingservername.md).  
  
     Quando um banco de dados de publicação é espelhado, os metadados de replicação armazenados no banco de dados espelhado são idênticos aos metadados armazenados no banco de dados principal. Portanto, para os bancos de dados de publicação habilitados para replicação no principal, o nome da instância do Publicador armazenado nas tabelas do sistema no espelho será o nome do principal, não do espelho. Isso afetará a configuração e a manutenção da replicação, em caso de failover do banco de dados de publicação no espelho. Por exemplo, se você configurar a replicação com procedimentos armazenados no espelho após o failover e desejar adicionar uma assinatura pull a um banco de dados de publicação habilitado no principal, será necessário especifique o nome do principal, em vez do nome do espelho para o parâmetro **@publisher** de **sp_addpullsubscription** ou **sp_addmergepullsubscription**.  
  
     Ao habilitar um banco de dados de publicação no espelho, após o failover para o espelho, o nome da instância do Publicador, armazenado nas tabelas do sistema, será o nome do espelho; neste caso, você usará o nome do espelho para o parâmetro **@publisher** .  
  
    > [!NOTE]  
    >  Em alguns casos, como **sp_addpublication**, o parâmetro **@publisher** tem suporte apenas nos Publicadores não[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ; nesses casos, ele não é relevante para o espelhamento do banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Para sincronizar uma assinatura no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] , após o failover: sincronize as assinaturas pull do Assinante e sincronize as assinaturas push do Publicador ativo.  
  
### <a name="replication-behavior-if-mirroring-is-removed"></a>Comportamento da replicação se o espelhamento for removido  
 Considere as questões a seguir, em caso de remoção do espelhamento do banco de dados de um banco de dados publicado:  
  
-   Se o banco de dados de publicação no principal não estiver mais espelhado, a replicação continuará a funcionar sem-alteração no principal original.  
  
-   Se ocorrer um failover de banco de dados de publicação do principal para o espelho, e a relação de espelhamento for subsequentemente desabilitada ou removida, os agentes de replicação não funcionarão com o espelho. Se o principal estiver permanentemente perdido, desabilite e, em seguida, reconfigure a replicação com o espelho especificado como Publicador.  
  
-   Se o espelhamento do banco de dados for completamente removido, o banco de dados espelho estará em um estado de recuperação e deverá ser restaurado para tornar-se funcional. O comportamento do banco de dados recuperado com relação à replicação depende da especificação da opção KEEP_REPLICATION. Essa opção força a operação de restauração para preservar as configurações da replicação, quando for restaurar um banco de dados publicado em um servidor que não seja naquele em que o backup foi criado. Use a opção KEEP_REPLICATION somente quando o outro banco de dados de publicação estiver indisponível. A opção não terá suporte se o outro banco de dados de publicação continuar intacto e replicando. Para obter mais informações sobre a opção KEEP_REPLICATION, veja [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md).  
  
## <a name="log-reader-agent-behavior"></a>Comportamento do Log Reader Agent  
 A tabela a seguir descreve o comportamento do Log Reader Agent nos vários modos operacionais do espelhamento do banco de dados.  
  
|Modo de operação|Comportamento do Log Reader Agent se o espelho estiver indisponível|  
|--------------------|------------------------------------------------------------|  
|Modo de segurança alta com failover automático|Se o espelho estiver indisponível, o Log Reader Agent propagará os comandos no banco de dados de distribuição. O principal não pode realizar o failover no espelho, até que este esteja on-line novamente e tenha todas as transações do principal.|  
|Modo de alto desempenho|Se o espelho estiver indisponível, o banco de dados principal estará em execução exposto (isto é, sem-espelho). Porém, o Log Reader Agent só replica as transações que estão intensificadas no espelho. Caso o serviço seja forçado e o servidor espelho assumir a função do principal, o Log Reader Agent funcionará no espelho e iniciará a seleção de novas transações.<br /><br /> Fique ciente de que a latência de replicação aumentará, se o espelho ficar atrás do principal.|  
|Modo de segurança alta sem failover automático|Todas as transações confirmadas têm a garantia de serem intensificadas em disco, no servidor espelho. O Log Reader Agent só replica as transações que estão intensificadas no espelho. Se o espelho estiver indisponível, o principal proíbe qualquer atividade adicional no banco de dados; portanto, o Log Reader Agent não terá nenhuma transação a ser replicada.|  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos e tarefas de replicação](../../relational-databases/replication/replication-features-and-tasks.md)   
 [Replicação e envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/log-shipping-and-replication-sql-server.md)  
  
  
