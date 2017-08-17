---
title: Usar o Assistente de Grupo de Disponibilidade (SQL Server Management Studio) | Microsoft Docs
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.newagwizard.f1
- sql13.swb.newavgroupwiz.f1
helpviewer_keywords:
- New Availability Group Wizard, availability replicas
- Availability Groups [SQL Server], wizards
- Availability Groups [SQL Server], creating
ms.assetid: e1f1dccc-9e65-471d-8fd1-b45085c9484a
caps.latest.revision: 46
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: f4a3c46eaad9fcdb330210d18ed8b2a56e178043
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="use-the-availability-group-wizard-sql-server-management-studio"></a>Usar a caixa de diálogo Assistente de Grupo de Disponibilidade (SQL Server Management Studio)
  Este tópico descreve como usar o **Assistente de Novo Grupo de Disponibilidade** no [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] para criar e configurar um grupo de disponibilidade AlwaysOn no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Um *grupo de disponibilidade* define um conjunto de bancos de dados de usuários que realizará o failover como uma única unidade e um conjunto de parceiros de failover, conhecido como *réplicas de disponibilidade*, que oferece suporte a failover.  
  
> [!NOTE]  
>  Para obter uma introdução aos grupos de disponibilidade, confira [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).  
    
##  <a name="BeforeYouBegin"></a> Antes de começar  
 É recomendável que você leia esta seção antes de tentar criar seu primeiro grupo de disponibilidade.  
  
###  <a name="Prerequisites"></a> Pré-requisitos, restrições e recomendações  

Na maioria dos casos, você pode usar o Assistente de Novo Grupo de Disponibilidade para concluir todas as tarefas necessárias para criar e configurar um grupo de disponibilidade. No entanto, talvez seja necessário concluir algumas das tarefas manualmente.  
  
- Se você estiver usando um tipo de cluster WSFC (Cluster de Failover do Windows Server) para hospedar o grupo de disponibilidade, verifique se as instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospedam as réplicas de disponibilidade residem em servidores (ou nós) de cluster diferentes no mesmo WSFC. Também verifique se cada uma das instâncias de servidor atende a todos os outros pré-requisitos do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Para obter mais informações, é altamente recomendável que você leia [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
-   Se uma instância de servidor selecionada para hospedar uma réplica de disponibilidade estiver sendo executada em uma conta de usuário de domínio e ainda não tiver um ponto de extremidade de espelhamento de banco de dados, o assistente poderá criar o ponto de extremidade e conceder a permissão CONNECT à conta de serviço da instância de servidor. No entanto, se o serviço [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] estiver sendo executado como uma conta interna, como Sistema Local, Serviço Local ou Serviço de Rede, ou como uma conta que não pertença a um domínio, você deverá usar certificados para autenticação de ponto de extremidade, e o assistente não poderá criar um ponto de extremidade de espelhamento de banco de dados na instância de servidor. Nesse caso, é recomendável criar manualmente os pontos de extremidade de espelhamento de banco de dados antes de iniciar o Assistente de Novo Grupo de Disponibilidade.  
  
     **Para usar certificados para um ponto de extremidade de espelhamento de banco de dados:**  
  
     [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../../t-sql/statements/create-endpoint-transact-sql.md)  
  
     [Usar certificados para um ponto de extremidade de espelhamento de banco de dados &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
-   As FCIs (Instâncias de cluster de failover) do SQL Server não dão suporte ao failover automático por grupos de disponibilidade, de modo que qualquer réplica de disponibilidade que esteja hospedado por um FCI só pode ser configurada para failover manual.  
  
-   **Pré-requisitos para o assistente realizar sincronização de dados inicial total**  
  
    -   Todos os caminhos de arquivos do banco de dados devem ser idênticos em cada instância de servidor que hospede uma réplica para o grupo de disponibilidade.  
  
    -   Não pode haver nome de banco de dados em nenhuma instância de servidor que hospeda uma réplica secundária. Isto significa que nenhum dos novos bancos de dados secundários pode existir ainda.  
  
    -   Você precisará especificar um compartilhamento de rede para que o assistente crie e acesse backups. Para a réplica primária, a conta usada para iniciar o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] deve ter permissões de leitura e gravação no sistema de arquivos em um compartilhamento de rede. Para réplicas secundárias, a conta deve ter permissão de leitura no compartilhamento de rede.  
  
        > [!IMPORTANT]  
        >  Os backups de log farão parte de sua cadeia de backup de log. Armazene os arquivos de backup de log adequadamente.  
  
     Se você não puder usar o assistente para executar a sincronização de dados inicial completa, precisará preparar seus bancos de dados secundários manualmente. Você pode fazer isto antes de ou depois de executar o assistente. Para obter mais informações, veja [Preparar um banco de dados secundário manualmente para um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer associação na função de servidor fixa **sysadmin** e a permissão de servidor CREATE AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou CONTROL SERVER.  
  
 Também exige permissão CONTROL ON ENDPOINT se você desejar permitir que o Assistente de grupo de disponibilidade gerencie o ponto de extremidade de espelhamento de banco de dados.  
  
##  <a name="RunAGwiz"></a> Usando o Assistente de Novo Grupo de Disponibilidade  
  
1.  No Pesquisador de Objetos, conecte-se à instância do servidor que hospeda a réplica de disponibilidade primária.  
  
2.  Expanda os nós **Alta Disponibilidade AlwaysOn** e **Grupos de Disponibilidade** .  
  
3.  Para iniciar o Assistente de Novo Grupo de Disponibilidade, selecione o comando **Assistente de Novo Grupo de Disponibilidade** .  
  
4.  Na primeira vez você executa este assistente, uma página de **Introdução** é exibida. Para ignorar essa página no futuro, clique em **Não mostrar esta página novamente**. Depois de ler esta página, clique em **Avançar**.  
  
5.  Na página **Especificar Opções do Grupo de Disponibilidade**, insira o nome do novo grupo de disponibilidade no campo **Nome do grupo de disponibilidade**. Esse nome deve ser um identificador válido do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] exclusivo no cluster e no domínio como um todo. O tamanho máximo de um nome de grupo de disponibilidade é 128 caracteres. e

6. Em seguida, especifique o tipo de cluster. Os tipos de cluster possíveis dependem da versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e do sistema operacional. Escolha **WSFC**, **EXTERNAL** ou **NONE**. Para obter detalhes, consulte [Página Especificar Nome do Grupo de Disponibilidade](specify-availability-group-name-page.md)
 
6.  Na página **Selecionar Bancos de Dados** , a grade lista bancos de dados de usuário na instância do servidor conectada que estão qualificados para se tornarem os *bancos de dados de disponibilidade*. Selecione um ou mais dos bancos de dados listados para participarem do novo grupo de disponibilidade. Inicialmente, esses bancos de dados serão os *bancos de dados primários*iniciais.  
  
     Para cada banco de dados listado, a coluna **Tamanho** exibe o tamanho do banco de dados, se conhecido. A coluna **Status** indica se determinado banco de dados atende aos [pré-requisitos](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)de bancos de dados de disponibilidade. Se os pré-requisitos não forem atendidos, uma descrição breve do status indicará o motivo pelo qual o banco de dados não se qualifica, por exemplo, se ele não usar o modelo de recuperação completa. Para obter mais informações, clique na descrição do status.  
  
     Se você alterar um banco de dados para torná-lo qualificado, clique em **Atualizar** para atualizar a grade de bancos de dados.  
  
     Se o banco de dados contiver uma chave mestra de banco de dados, insira a senha para a chave mestra de banco de dados na coluna **Senha** .  
  
7.  Na página **Especificar Réplicas** , especifique e configure uma ou mais réplicas para o novo grupo de disponibilidade. Essa página contém quatro guias: A tabela a seguir apresenta essas guias. Para obter mais informações, confira o tópico [Página Especificar Réplicas &#40;Assistente de Novo Grupo de Disponibilidade: Assistente para Adicionar Réplica&#41;](../../../database-engine/availability-groups/windows/specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md).  
  
    |Tab|Descrição breve|  
    |---------|-----------------------|  
    |**Réplicas**|Use esta guia para especificar cada instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospedará uma réplica secundária. Observe que a instância de servidor à qual você está conectado no momento deve hospedar a réplica primária.|  
    |**Pontos de extremidade**|Use esta guia para verificar quaisquer pontos de extremidade de espelhamento de banco de dados existentes e também, se esse ponto de extremidade estiver ausente em uma instância de servidor cujas contas de serviço usam a Autenticação do Windows para criar o ponto de extremidade automaticamente.<br /><br /> Observação: se alguma instância de servidor estiver sendo executada em uma conta de usuário que não pertença a um domínio, você precisará fazer uma alteração manual na instância de servidor para que possa continuar as etapas do assistente. Para obter mais informações, consulte [Pré-requisitos](#Prerequisites)anteriormente neste tópico.|  
    |**Preferências de backup**|Use esta guia para especificar sua preferência de backup para o grupo de disponibilidade como um todo e suas prioridades de backup para as réplicas de disponibilidade individuais.|  
    |**Ouvinte**|Use esta guia para criar um ouvinte de grupo de disponibilidade. Por padrão, o assistente não cria um ouvinte.|  
  
8.  Na página **Selecionar Sincronização de Dados Inicial** , escolha como você deseja que seus novos bancos de dados secundários sejam criados e unidos ao grupo de disponibilidade. Escolha uma das seguintes opções:  
  
    -   **Propagação automática**  
  
         O SQL Server cria automaticamente as réplicas secundárias para cada banco de dados no grupo. A propagação automática exige que os caminhos do arquivo de dados e de log sejam os mesmos em cada instância do SQL Server que faz parte do grupo. Disponível no [!INCLUDE[sssql15-md.md](../../../includes/sssql15-md.md)] e posterior. Consulte [Inicializar automaticamente o grupo de disponibilidade AlwaysOn](automatically-initialize-always-on-availability-group.md).
    
    -   **Backup completo de log e de banco de dados**  
  
         Selecione esta opção se seu ambiente atender aos requisitos para iniciar automaticamente a sincronização de dados inicial (para obter mais informações, veja [Pré-requisitos, restrições e recomendações](#Prerequisites), anteriormente neste tópico).  
  
         Se você selecionar **Total**, depois de criar o grupo de disponibilidade, o assistente fará backup de todos os bancos de dados primários e de seu log de transações em um compartilhamento de rede e restaurará os backups em todas as instâncias de servidor que hospedam uma réplica secundária. Em seguida, o assistente unirá cada banco de dados secundário ao grupo de disponibilidade.  
  
         No campo **Especificar um local de rede compartilhado acessível por todas as réplicas:** , especifique um compartilhamento de backup ao qual todas as instâncias do servidor que hospedam réplicas de host têm acesso de leitura/gravação. Para obter mais informações, consulte [Pré-requisitos](#Prerequisites)anteriormente neste tópico.  
  
    -   **Somente junção**  
  
         Se preparou bancos de dados secundários manualmente nas instâncias do servidor que hospedam réplicas secundárias, você poderá selecionar essa opção. O assistente unirá os bancos de dados secundários existentes ao grupo de disponibilidade.  
  
    -   **Ignorar sincronização de dados inicial**  
  
         Selecione esta opção se desejar usar seus próprios backups de banco de dados e de log de seus bancos de dados primários. Para obter mais informações, veja [Iniciar movimentação de dados em um banco de dados secundário AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md).  
  
9. A página **Validação** verifica se os valores especificados neste Assistente atendem aos requisitos do Assistente de Novo Grupo de Disponibilidade. Para fazer uma alteração, clique em **Anterior** para retornar a uma página anterior do assistente para alterar um ou mais valores. Clique em **Avançar** para retornar à página **Validação** e clique em **Executar Novamente a Validação**.  
  
10. Na página **Resumo** , revise as opções escolhidas para o novo grupo de disponibilidade. Para fazer uma alteração, clique em **Anterior** para retornar à página relevante. Após fazer a alteração, clique em **Avançar** para retornar à página **Resumo** .  
  
    > [!IMPORTANT]  
    >  Quando a conta de serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de uma instância de servidor que hospedará uma nova réplica de disponibilidade ainda não existir como um logon, o Assistente para Novo Grupo de Disponibilidade precisará criar o logon. Na página **Resumo** , o assistente exibe as informações para o logon que deve ser criado. Se você clicar em **Concluir**, o assistente criará esse logon para a conta de serviço do SQL Server e concederá a permissão CONNECT a ele.  
  
     Se estiver satisfeito com a seleções, opcionalmente, clique em **Script** para criar um script das etapas que o assistente executará. Em seguida, para criar e configurar o novo grupo de disponibilidade, clique em **Concluir**.  
  
11. A página **Progresso** exibe o progresso das etapas de criação do grupo de disponibilidade (configuração de pontos de extremidade, criação do grupo de disponibilidade e ingresso da réplica secundária no grupo).  
  
12. Quando essas etapas forem concluídas, a página **Resultados** exibirá o resultado de cada etapa. Se todas essas etapas tiverem êxito, o novo grupo de disponibilidade será configurado completamente. Se quaisquer das etapas resultar em um erro, você poderá precisar concluir a configuração manualmente ou use um assistente para a etapa com falha. Para obter informações sobre a causa de um determinado erro, clique no link de "Erro" associado na coluna **Resultado** .  
  
     Quando o assistente for concluído, clique em **Fechar** para sair.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para concluir a configuração do grupo de disponibilidade**  
  
-   [Unir uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Preparar um banco de dados secundário manualmente para um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [Unir um banco de dados secundário a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
 **Maneiras alternativas de criar um grupo de disponibilidade**  
  
-   [Usar a caixa de diálogo Novo Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Criar um grupo de disponibilidade &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)  
  
-   [Criar um grupo de disponibilidade &#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-sql-server-powershell.md)  
  
 **Para habilitar os Grupos de Disponibilidade AlwaysOn**  
  
-   [Habilitar e desabilitar Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)  
  
 **Para configurar um ponto de extremidade de espelhamento de banco de dados**  
  
-   [Criar um ponto de extremidade de espelhamento de banco de dados para grupos de disponibilidade AlwaysOn &#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Criar um ponto de extremidade de espelhamento de banco de dados para a Autenticação do Windows &#40;SQL Server&#41;](../../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Usar certificados para um ponto de extremidade de espelhamento de banco de dados &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
-   [Especificar a URL do ponto de extremidade ao adicionar ou modificar uma réplica de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
 **Para solucionar problemas de configuração dos grupos de disponibilidade AlwaysOn**  
  
-   [Solucionar problemas de configuração de grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
-   [Solução de problemas de uma operação de adição de arquivos com falha &#40;Grupos de disponibilidade de AlwaysOn&#41;](../../../database-engine/availability-groups/windows/troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="RelatedContent"></a> Conteúdo relacionado  
  
-   **Blogs:**  
  
     [Série de aprendizado do AlwaysOn – HADRON: uso do pool de trabalho para bancos de dados habilitados para HADRON](http://blogs.msdn.com/b/psssql/archive/2012/05/17/Always%20On-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
     [Blogs da equipe do AlwaysOn do SQL Server: o blog oficial da equipe do AlwaysOn do SQL Server](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
     [Blogs dos engenheiros do CSS SQL Server](http://blogs.msdn.com/b/psssql/)  
  
-   **Vídeos:**  
  
     [Microsoft SQL Server codinome “Denali” Série AlwaysOn, Parte 1: Introduzindo a próxima geração de solução de alta disponibilidade](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server codinome “Denali” Série AlwaysOn, Parte 2: Criando uma solução de alta disponibilidade de missão crítica usando AlwaysOn](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **Whitepapers:**  
  
     [Guia de soluções AlwaysOn do Microsoft SQL Server para alta disponibilidade e recuperação de desastre](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [White papers da Microsoft para SQL Server 2012](http://msdn.microsoft.com/library/hh403491.aspx)  
  
     [White papers da equipe de consultoria do cliente do SQL Server](http://sqlcat.com/)  
  
## <a name="alternate-ways-to-create-availability-groups"></a>Formas alternativas de criar grupos de disponibilidade

Como alternativa ao uso do Assistente de Novo Grupo de Disponibilidade, você pode usar os cmdlets PowerShell [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para obter mais informações, veja [Criar um grupo de disponibilidade &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md) ou [Criar um grupo de disponibilidade &#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-sql-server-powershell.md).  


## <a name="see-also"></a>Consulte também  
 [O ponto de extremidade de espelhamento de banco de dados &#40;SQL Server&#41;](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)  
  

