---
title: Analysis Services com Grupos de Disponibilidade AlwaysOn | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 14d16bfd-228c-4870-b463-a283facda965
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 813740a542f06417156c746574dd0995e59aabd6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62791871"
---
# <a name="analysis-services-with-always-on-availability-groups"></a>Analysis Services com grupos de disponibilidade AlwaysOn
  Um grupo de disponibilidade AlwaysOn é uma coleção predefinida de bancos de dados relacionais do SQL Server que faz failover junto quando condições disparam um failover em qualquer um dos bancos de dados, redirecionando solicitações para um banco de dados espelhado em outra instância no mesmo grupo de disponibilidade. Se você estiver usando grupos de disponibilidade como sua solução de alta disponibilidade, poderá usar um banco de dados nesse grupo como uma fonte de dados em uma solução de tabela do Analysis Services ou multidimensional. Todas as operações do Analysis Services a seguir funcionam como esperado ao usar um banco de dados de disponibilidade: processando ou importando dados, consultando dados relacionais diretamente (usando o armazenamento de ROLAP ou o modo DirectQuery), e writeback.  
  
 O processamento e a consulta são cargas de trabalho somente leitura. Você pode melhorar o desempenho descarregando essas cargas de trabalho em uma réplica secundária legível. Este cenário exige configuração adicional. Use a lista de verificação neste tópico para garantir que você siga todas as etapas.  
  
  
##  <a name="bkmk_prereq"></a> Pré-requisitos  
 Você deve ter um logon do SQL Server em todas as réplicas. Você deve ser um **sysadmin** para configurar grupos de disponibilidade, ouvintes e bancos de dados, mas os usuários só precisam de permissões **db_datareader** para acessar o banco de dados de um cliente do Analysis Services.  
  
 Use um provedor de dados que oferece suporte ao protocolo TDS versão 7.4 ou mais recente, como o SQL Server Native Client 11.0 ou o Provedor de Dados para o SQL Server no .NET Framework 4.02.  
  
 **(Para cargas de trabalho somente leitura)**. A função de réplica secundária deve ser configurada para conexões somente leitura; o grupo de disponibilidade deve ter uma lista de roteamento e a conexão na fonte de dados do Analysis Services deve especificar o ouvinte de grupo de disponibilidade. As instruções são fornecidas neste tópico.  
  
##  <a name="bkmk_UseSecondary"></a> Lista de verificação: usar uma réplica secundária para operações somente leitura  
 A menos que a solução Analysis Services inclua writeback, você pode configurar uma conexão da fonte de dados para usar uma réplica secundária legível. Se você tiver uma conexão de rede rápida, a réplica secundária terá latência de dados muito baixa, fornecendo dados quase idênticos aos da réplica primária. Usando a réplica secundária em operações do Analysis Services, você pode reduzir a contenção de leitura/gravação na réplica primária e obter uma melhor utilização de réplicas secundárias em seu grupo de disponibilidade.  
  
 Por padrão, tanto o acesso de leitura-gravação quanto o acesso de intenção de leitura são permitidos para a réplica primária e nenhuma conexão é permitida para as réplicas secundárias. Uma configuração adicional é exigida para definir uma conexão de cliente somente leitura com uma réplica secundária. A configuração requer a definição de propriedades na réplica secundária e a execução de um script T-SQL que define uma lista de roteamento somente leitura. Use os procedimentos a seguir para garantir que você executou ambas as etapas.  
  
> [!NOTE]  
>  As etapas a seguir pressupõem a existência de um grupo de disponibilidade AlwaysOn e de bancos de dados. Se você estiver configurando um novo grupo, use o Assistente Novo Grupo de Disponibilidade para criar o grupo e unir os bancos de dados. O assistente verifica pré-requisitos, fornece orientação para cada etapa e executa a sincronização inicial. Para obter mais informações, consulte [Usar a caixa de diálogo Assistente de Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](use-the-availability-group-wizard-sql-server-management-studio.md).  
  
#### <a name="step-1-configure-access-on-an-availability-replica"></a>Etapa 1: Configurar o acesso em uma réplica de disponibilidade  
  
1.  No Pesquisador de Objetos, conecte-se à instância de servidor que hospeda a réplica primária e expanda a árvore de servidores.  
  
    > [!NOTE]  
    >  Estas etapas são obtidas de [Configurar o acesso somente leitura em uma réplica de disponibilidade &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md), que fornece informações adicionais e instruções alternativas para executar esta tarefa.  
  
2.  Expanda os nós **Alta Disponibilidade AlwaysOn** e **Grupos de Disponibilidade** .  
  
3.  Clique no grupo de disponibilidade cuja réplica você deseja alterar. Expanda **Réplicas de Disponibilidade**.  
  
4.  Clique com o botão direito do mouse na réplica secundária e clique em **Propriedades**.  
  
5.  Na caixa de diálogo **Propriedades da Réplica de Disponibilidade** , altere o acesso de conexão para a função secundária, da seguinte forma:  
  
    -   Na lista suspensa **Secundária legível** , selecione **Somente intenção de leitura**.  
  
    -   Na lista suspensa **Conexões na função primária** , selecione **Permitir todas as conexões**. Esse é o padrão.  
  
    -   Opcionalmente, na lista suspensa **Modo de disponibilidade** , selecione **Confirmação síncrona**. Esta etapa não é necessária, mas sua definição garante que exista a paridade de dados entre as réplicas primária e secundária.  
  
         Esta propriedade também é um requisito para failover planejado. Se você desejar executar um failover manual planejado para fins de testes, defina **Modo de disponibilidade** como **Confirmação síncrona** para as réplicas primária e secundária.  
  
#### <a name="step-2-configure-read-only-routing"></a>Etapa 2: Configurar roteamento somente leitura  
  
1.  Conecte-se à réplica primária.  
  
    > [!NOTE]  
    >  Estas etapas são obtidas de [Configurar o roteamento somente leitura para um grupo de disponibilidade &#40;SQL Server&#41;](configure-read-only-routing-for-an-availability-group-sql-server.md), que contém informações adicionais e instruções alternativas para executar esta tarefa.  
  
2.  Abra uma janela de consulta e cole o script a seguir. Este script executa três ações: habilita conexões legíveis com uma réplica secundária (que está desabilitada por padrão), define a URL do roteamento somente leitura e cria a lista de roteamento que prioriza a forma de direcionamento de solicitações de conexão.  A primeira instrução, que permite conexões legíveis, será redundante se você já tiver definido as propriedades no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)], mas será incluída para manter a integridade.  
  
    ```  
    ALTER AVAILABILITY GROUP [AG1]  
     MODIFY REPLICA ON  
    N'COMPUTER01' WITH   
    (SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY));  
  
    ALTER AVAILABILITY GROUP [AG1]  
     MODIFY REPLICA ON  
    N'COMPUTER01' WITH   
    (SECONDARY_ROLE (READ_ONLY_ROUTING_URL = N'TCP://COMPUTER01.contoso.com:1433'));  
  
    ALTER AVAILABILITY GROUP [AG1]  
     MODIFY REPLICA ON  
    N'COMPUTER02' WITH   
    (SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY));  
  
    ALTER AVAILABILITY GROUP [AG1]  
     MODIFY REPLICA ON  
    N'COMPUTER02' WITH   
    (SECONDARY_ROLE (READ_ONLY_ROUTING_URL = N'TCP://COMPUTER02.contoso.com:1433'));  
  
    ALTER AVAILABILITY GROUP [AG1]   
    MODIFY REPLICA ON  
    N'COMPUTER01' WITH   
    (PRIMARY_ROLE (READ_ONLY_ROUTING_LIST=('COMPUTER02','COMPUTER01')));  
  
    ALTER AVAILABILITY GROUP [AG1]   
    MODIFY REPLICA ON  
    N'COMPUTER02' WITH   
    (PRIMARY_ROLE (READ_ONLY_ROUTING_LIST=('COMPUTER01','COMPUTER02')));  
    GO  
    ```  
  
3.  Modifique o script, substituindo espaços reservados por valores que são válidos para sua implantação:  
  
    -   Substitua 'Computer01' pelo nome da instância do servidor que hospeda a réplica primária.  
  
    -   Substitua 'Computer02' pelo nome da instância do servidor que hospeda a réplica secundária.  
  
    -   Substitua 'contoso.com' pelo nome de seu domínio ou omita-o do script se todos os computadores estiverem no mesmo domínio. Mantenha o número da porta se o ouvinte estiver usando a porta padrão. A porta que é usada de fato pelo ouvinte é listada na página de propriedades no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)].  
  
4.  Execute o script.  
  
     Em seguida, crie uma fonte de dados em um modelo do Analysis Services que usa um banco de dados do grupo recém-configurado.  
  
##  <a name="bkmk_ssasAODB"></a> Criar uma fonte de dados do Analysis Services usando um banco de dados de disponibilidade do AlwaysOn  
 Esta seção explica como criar uma fonte de dados do Analysis Services que conecta a um banco de dados em um grupo de disponibilidade. Você pode usar estas instruções para configurar uma conexão a uma réplica primária (padrão) ou a uma réplica secundária legível configurada com base em etapas de uma seção anterior. Parâmetros de configuração de AlwaysOn, mais as propriedades de conexão definidas no cliente, determinarão se uma réplica primária ou secundária é usada.  
  
1.  No [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)], em um projeto de Modelo de mineração de dados e multidimensional do Analysis Services, clique com o botão direito do mouse em **Fontes de Dados** e selecione **Nova Fonte de Dados**. Clique em **Novo** para criar uma nova fonte de dados.  
  
     Outra alternativa para um projeto de modelo de tabela é clicar no menu Modelo e em **Importar de Fonte de Dados**.  
  
2.  Em Gerenciador de Conexões, em Provedor, escolha um provedor que ofereça suporte ao protocolo TDS. O SQL Server Native Client 11.0 oferece suporte a esse protocolo.  
  
3.  Em Gerenciador de Conexões, em Nome do Servidor, insira o nome do *ouvinte de grupo de disponibilidade*e escolha um banco de dados que esteja disponível no grupo.  
  
     O ouvinte de grupo de disponibilidade redireciona uma conexão de cliente a uma réplica primária para solicitações de leitura/gravação ou para uma réplica secundária quando você especifica a intenção de leitura na cadeia de conexão. Como funções de réplica serão alteradas durante um failover (em que a primária se torna a secundária e uma secundária se torna primária), você sempre deve especificar o ouvinte de forma que a conexão de cliente seja redirecionada conformemente.  
  
     Para determinar o nome do ouvinte do grupo de disponibilidade, você pode solicitar a um administrador de banco de dados ou se conectar a uma instância no grupo de disponibilidade e exibir sua configuração de disponibilidade de AlwaysOn. Na captura de tela a seguir, o ouvinte do grupo de disponibilidade é o **AdventureWorks2**.  
  
     ![Pasta AlwaysOn Availability no Management Studio](../../media/ssas-alwaysoninfoinssms.png "pasta AlwaysOn Availability no Management Studio")  
  
4.  Ainda no Gerenciador de Conexões, clique em **Tudo** no painel de navegação esquerdo para exibir a grade de propriedades do provedor de dados.  
  
     Defina **Intenção de Aplicativo** como **READONLY** se você estiver configurando uma conexão de cliente somente leitura para uma réplica secundária. Caso contrário, mantenha o **READWRITE** padrão para redirecionar a conexão para a réplica primária.  
  
5.  Em Informações da Representação, selecione **Usar um nome de usuário e uma senha específicos do Windows**e insira uma conta de usuário de domínio do Windows que tenha um mínimo de permissões **db_datareader** no banco de dados.  
  
     Não escolha **Usar as credenciais do usuário atual** ou **Herdar**. Você pode escolher **Usar a conta de serviço**, mas apenas se essa conta tiver permissões de leitura no banco de dados.  
  
     Conclua a fonte de dados e feche o Assistente de Fonte de Dados.  
  
6.  Adicione **MultiSubnetFailover=Yes** à cadeia de conexão para fornecer detecção mais rápida e conexão ao servidor ativo. Para obter mais informações sobre essa propriedade, consulte [Suporte do SQL Server Native Client à alta disponibilidade e recuperação de desastre](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).  
  
     Esta propriedade não está visível na grade de propriedades. Para adicionar a propriedade, clique com o botão direito do mouse na fonte de dados e escolha **Exibir Código**. Adicione `MultiSubnetFailover=Yes` à cadeia de conexão.  
  
 A fonte de dados é definida agora. Você pode continuar a criar um modelo, começando pela exibição da fonte de dados ou, no caso de modelos de tabela, criando relações. Quando você chega a tal ponto em que dados precisam ser recuperados do banco de dados de disponibilidade (por exemplo, quando você está pronto para processar ou implantar a solução), pode testar a configuração para verificar se dados são acessados da réplica secundária.  
  
##  <a name="bkmk_test"></a> Testar a configuração  
 Depois que você configurar a réplica secundária e criar uma conexão da fonte de dados no Analysis Services, poderá confirmar esse processamento e comandos de consulta serão redirecionados para a réplica secundária. Você também pode executar um failover manual planejado para verificar seu plano de recuperação para este cenário.  
  
#### <a name="step-1-confirm-the-data-source-connection-is-redirected-to-the-secondary-replica"></a>Etapa 1: Confirmar se a conexão da fonte de dados é redirecionada para a réplica secundária  
  
1.  Inicie o SQL Server Profiler e conecte à instância do SQL Server que hospeda a réplica secundária.  
  
     Quando o rastreamento for executado, os eventos `SQL:BatchStarting` e `SQL:BatchCompleting` mostrarão as consultas emitidas do Analysis Services que são executadas na instância do mecanismo de banco de dados. Estes eventos são selecionados por padrão; portanto, você só precisa iniciar o rastreamento.  
  
2.  No [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)], abra o projeto ou a solução do Analysis Services que contém uma conexão da fonte de dados a ser testada. Verifique se a fonte de dados especificou o ouvinte de grupo de disponibilidade e não uma instância no grupo.  
  
     Esta etapa é importante. O roteando para a réplica secundária não ocorrerá se você especificar um nome de instância de servidor.  
  
3.  Organize as janelas de aplicativo de forma que possa exibir o SQL Server Profiler e o [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)] lado a lado.  
  
4.  Implante a solução e quando concluir, pare o rastreamento.  
  
     Na janela de rastreamento, você deve consultar eventos do aplicativo **Microsoft SQL Server Analysis Services**. Você deve consultar instruções `SELECT` que recuperam dados de um banco de dados na instância do servidor que hospeda a réplica secundária, provando que a conexão foi feita através do ouvinte para a réplica secundária.  
  
#### <a name="step-2-perform-a-planned-failover-to-test-the-configuration"></a>Etapa 2: Executar um failover planejado para testar a configuração  
  
1.  No [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] , verifique as réplicas primária e secundária para garantir que ambas estão configuradas para o modo de confirmação síncrona e estão sincronizadas no momento.  
  
     As etapas a seguir assumem que uma réplica secundária é configurada para a confirmação síncrona.  
  
     Para verificar a sincronização, abra uma conexão com cada instância que hospeda as réplicas primária e secundária, expanda a pasta Bancos de Dados e verifique se o banco de dados tem **(Sincronizado)** e **(Sincronizando)** anexados a seu nome em cada réplica.  
  
    > [!NOTE]  
    >  Estas etapas são obtidas de [Executar um failover manual planejado de um grupo de disponibilidade&#40;SQL Server&#41;](perform-a-planned-manual-failover-of-an-availability-group-sql-server.md), que contém informações adicionais e instruções alternativas para executar esta tarefa.  
  
2.  No SQL Server Profiler, inicie os rastreamentos para cada réplica e exiba os rastreamentos lado a lado. Nas etapas a seguir, você comparará rastreamentos, confirmando que as consultas SQL usadas para processar ou consultar do Analysis Services alternam de uma réplica para a outra.  
  
3.  Execute um comando de processamento ou de consulta do Analysis Services. Como você configurou a fonte de dados para uma conexão somente leitura, deve ver a execução do comando na réplica secundária.  
  
4.  No [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)], conecte-se à réplica secundária.  
  
5.  Expanda os nós **Alta Disponibilidade AlwaysOn** e **Grupos de Disponibilidade** .  
  
6.  Clique com o botão direito do mouse no grupo de disponibilidade do qual fazer failover e selecione o comando **Failover** . Isso inicia o Assistente de Grupo de Disponibilidade de Failover. Use o assistente para escolher a réplica da qual será criada a nova réplica primária.  
  
7.  Confirme que o failover teve êxito:  
  
    -   No [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)], expanda os grupos de disponibilidade para exibir as designações (primária) e (secundária). A instância que antes era uma réplica primária agora deve ser uma réplica secundária.  
  
    -   Exiba o painel para determinar se foram detectados problemas de integridade. Clique com o botão direito do mouse no grupo de disponibilidade e selecione **Mostrar Painel**.  
  
8.  Espere um ou dois minutos pela conclusão do failover no backend.  
  
9. Repita o comando de processamento ou de consulta na solução do Analysis Services e observe os rastreamentos lado a lado no SQL Server Profiler. Você deve encontrar evidência de processamento na outra instância, que agora é a nova réplica secundária.  
  
##  <a name="bkmk_whathappens"></a> O que acontece depois que um failover ocorre  
 Durante um failover, uma réplica secundária faz a transição para a função primária e a réplica primária antiga faz a transição para a réplica secundária. Todas as conexões de cliente são finalizadas, a propriedade do ouvinte de grupo de disponibilidade é movida com a função de réplica primária para uma nova instância do SQL Server e o ponto de extremidade do ouvinte é associado aos endereços IP virtuais da nova instância e a portas TCP. Para obter mais informações, consulte [Sobre Acesso de conexão de cliente a réplicas de disponibilidade &#40;SQL Server&#41;](about-client-connection-access-to-availability-replicas-sql-server.md).  
  
 Se ocorrer um failover durante o processamento, o seguinte erro ocorrerá no Analysis Services na janela de Saída ou no arquivo de log: "Erro de OLE DB: Erro de OLE DB ou ODBC: falha no link de comunicação; 08S01; provedor TPC: uma conexão existente foi fechada forçadamente pelo host remoto. ; 08S01."  
  
 Este erro deverá ser resolvido se você aguardar um minuto e tentar novamente. Se o grupo de disponibilidade for configurado corretamente para a réplica secundária legível, o processando será retomado na nova réplica secundária quando você tentar novamente processar.  
  
 A causa mais provável de erros persistentes é um problema de configuração. Você pode tentar reexecutar o script T-SQL para resolver problemas na lista de roteamento, em URLs de roteamento somente leitura e a intenção de leitura na réplica secundária. Você também deve verificar se a réplica primária permite todas as conexões.  
  
##  <a name="bkmk_writeback"></a> Write-back ao usar um banco de dados de disponibilidade do AlwaysOn  
 Writeback é um recurso do Analysis Services que oferece suporte à análise E-Se no Excel. Ele também costuma ser usado para orçar e prever tarefas em aplicativos personalizados.  
  
 O suporte ao writeback exige uma conexão de cliente READWRITE. No Excel, se você tentar fazer write-back em uma conexão somente leitura, o seguinte erro ocorrerá: "Não foi possível recuperar dados da fonte de dados externa." "Não foi possível recuperar dados da fonte de dados externa."  
  
 Se você configurou uma conexão para sempre acessar uma réplica secundária legível, configure uma nova conexão que usa uma conexão READWRITE para a réplica primária.  
  
 Para fazer isso, crie uma fonte de dados adicional em um modelo do Analysis Services para oferece suporte à conexão de leitura/gravação. Ao criar a fonte de dados adicional, use o mesmo nome de ouvinte e banco de dados especificados na conexão somente leitura, mas, em vez de modificar a **Intenção de Aplicativo**, mantenha o padrão que dá suporte a conexões READWRITE. Você pode adicionar um novo fato ou tabelas de dimensão à sua exibição de fonte de dados com base na fonte de dados de leitura/gravação e, depois, habilitar o write-back nas novas tabelas.  
  
## <a name="see-also"></a>Consulte também  
 [Ouvintes do grupo de disponibilidade, conectividade de cliente e failover de aplicativo &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [Secundárias ativas: Réplicas secundárias legíveis &#40;grupos de disponibilidade AlwaysOn&#41;](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [Políticas AlwaysOn para problemas operacionais com grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](always-on-policies-for-operational-issues-always-on-availability.md)   
 [Criar uma fonte de dados &#40;SSAS multidimensional&#41;](../../../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)   
 [Habilitar o write-back de dimensão](../../../analysis-services/multidimensional-models/bi-wizard-enable-dimension-writeback.md)  
  
  
