---
title: "Alta disponibilidade e recuperação de desastres para Master Data Services | Microsoft Docs"
ms.custom: 
ms.date: 07/28/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: installing-mds-in-an-alwayson-group-environment
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: f5cebe2ba32765cc5f4bddc974ee62b3ed3b8915
ms.contentlocale: pt-br
ms.lasthandoff: 09/07/2017

---



# <a name="high-availability-and-disaster-recovery-for-master-data-services"></a>Alta disponibilidade e recuperação de desastres para Master Data Services

**Resumo:** este artigo descreve uma solução para Master Data Service (MDS) hospedado em uma configuração do grupo de disponibilidade AlwaysOn. Esse artigo descreve como instalar e configurar o SQL 2016 Master Data Services em um grupo de disponibilidade (AG) AlwaysOn do SQL 2016. O objetivo principal dessa solução é melhorar a alta disponibilidade e recuperação de desastres de dados de back-end do MDS hospedados em um banco de dados SQL Server.

## <a name="introduction"></a>Introdução


Este artigo descreve uma solução para MDS (Master Data Service) hospedado em uma configuração do grupo de disponibilidade AlwaysOn. Esse artigo descreve como instalar e configurar o SQL 2016 MDS em um AG (grupo de disponibilidade) AlwaysOn do SQL 2016. O objetivo principal dessa solução é melhorar a alta disponibilidade e recuperação de desastres de dados de back-end do MDS hospedados em um banco de dados SQL Server.

Para implementar a solução, você precisa concluir as seguintes tarefas abordadas neste artigo.

1.  [Instalar e configurar o WSFC (Cluster de Failover do Windows Server)](#windows-server-failover-cluster-wsfc).

2.  [Configurar o AG AlwaysOn](#sql-server-alwayson-availability-group).

3.  [Configurar o MDS para ser executado em um nó WSFC](#configure-mds-to-run-on-an-wsfc-node).

As seções acima apresentarão brevemente as tecnologias, seguidas por instruções. Para obter informações detalhadas sobre as tecnologias, examine os documentos vinculados em cada seção.

Essa solução descrita neste artigo é criada sobre o AG AlwaysOn do SQL Server, no qual cada banco de dados tem várias réplicas síncronas ou assíncronas. Apenas uma réplica aceita a transação (aceita solicitações de usuário). Esta é a réplica primária.

Cada réplica tem seu próprio armazenamento, portanto, não há nenhum armazenamento compartilhado centralizado nesta solução. Quando há uma falha de software ou uma falha de hardware que afeta a réplica primária, a réplica primária pode fazer o failover para uma réplica de síncrona ou assíncrona manualmente ou automaticamente com base na configuração e na situação. Isso garante a alta disponibilidade do banco de dados com interrupção mínima para os usuários.

Réplicas assíncronas normalmente são hospedadas em um data center remota em relação ao centro de dados da réplica primária. No caso de cenários de desastre, a réplica primária pode realizar o failover para outro data center. Isso garante a recuperação de desastres do banco de dados.

Para fins de demonstração, a solução descrita neste artigo usa as seguintes versões do software. Versões mais antigas devem funcionar da mesma forma com potencialmente pequenas diferenças.

-   Windows Server 2012R2 com clister de failover do servidor

-   SQL Server 2016 com o recurso Master Data Service

Além disso, a solução usa duas VMs, **MDS-HA1** e **MDS-HA2**, para hospedar duas réplicas. Desde que ele tenha suporte pelo AG AlwaysOn do SQL Server, o MDS não limita quantas réplicas podem ser usadas.

Este artigo pressupõe que você tenha um conhecimento básico sobre o Windows Server, o Cluster de Failover do Windows Server, o AlwaysOn do SQL Server e o MDS do SQL Server.

## <a name="what-is-not-covered"></a>O que não é abordado

Este documento não aborda o seguinte:

-   Como fazer o IIS, o servidor Web que hospeda a interface do usuário do serviço de dados mestre, altamente disponível e recuperável após um desastre. O MDS não impõe nenhum requisito específico no IIS, para que as técnicas padrão para tornar o IIS altamente disponível e o balanceamento de carga pode funcionar aqui também.

-   Como usar o cluster de failover (FCI) do AlwaysOn do SQL Server para dar suporte à HA (alta disponibilidade) no back-end do MDS. O clustering de failover do SQL Server é uma solução de HA diferente e oficialmente tem suporte pelo SQL Server e ele funciona com o MDS.

-   Como usar uma solução híbrida de cluster de failover do SQL Server (FCI) e o AG do AlwaysOn para dar suporte à HA no back-end do MDS. A solução híbrida funciona com o MDS.

## <a name="design-consideration"></a>Considerações de design

A Figura 1 mostra uma configuração típica usada principalmente no AG do AlwaysOn. No data center primário, há duas réplicas com uma relação de confirmação síncrona e ambas as réplicas têm o privilégio VOTE. Isso é usado principalmente para melhorar a HA no caso de a réplica primária falhar.

No Data Center de Recuperação de Desastres, há uma réplica secundária com uma relação de confirmação assíncrona com a primária. Esse data center geralmente está em uma região geográfica diferente do data center primário. A réplica secundária não tem o privilégio VOTE.

Essa configuração é usada para atingir a recuperação no caso de o data center primário estar em um desastre, como um incêndio, terremoto etc. A configuração atinge a HA e a recuperação de desastres com um custo relativamente baixo.

![Configuração típica para o Grupo de Disponibilidade AlwaysOn](media/Fig1_TypicalConfig.png)

Figura 1. Uma configuração típica de Grupo de Disponibilidade AlwaysOn

Se você não precisar considerar a recuperação desastre, não será necessário ter uma réplica em um data center secundário. Se você precisar aumentar a HA, poderá ter mais réplicas síncronas no mesmo data center primário.

Portanto, é importante considerar seus cenários e requisitos e escolher quantas réplicas síncronas e assíncronas são necessárias e em quais data centers você deve colocá-las.

## <a name="windows-server-failover-cluster-wsfc"></a>WSFC (Cluster de Failover do Windows Server)

Esta seção aborda as seguintes tarefas.

1.  [Instalar o recurso de Failover do Windows](#install-failover-cluster-feature).

2.  [Criar um Cluster de Failover do Windows Server](#create-a-windows-server-failover-cluster).

Conforme mostrado na Figura 1 na seção anterior, a solução descrita neste artigo inclui o WSFC (Cluster de Failover do Windows Server). É preciso configurar o WSFC porque o SQL AlwaysOn depende do WFSC para failover e detecção de falha.

O WSFC é um recurso para melhorar a alta disponibilidade de aplicativos e serviços. Ele consiste em um grupo de instâncias do Windows Server independentes com o 	Serviço de Cluster de Failover da Microsoft em execução nessas instâncias. As instâncias do Windows Server (ou nós como são chamadas às vezes) estão conectadas de forma que possam se comunicar entre si e a detecção de falha seja possível. O WSFC fornece as funcionalidades de detecção de falha e failover. Se um nó ou um serviço falhar no cluster, a falha será detectada e outro nó automaticamente ou manualmente começará a fornecer os serviços hospedados no nó com falha. Dessa forma, os usuários sofrem interrupções mínimas nos serviços e a disponibilidade do serviço é melhorada.  

### <a name="prerequisites"></a>Pré-requisitos

O sistema operacional Windows Server é instalado em todas as instâncias e todas as atualizações são corrigidas.

>[!NOTE] 
>É **altamente recomendável** que você instale a mesma versão do Windows e o mesmo conjunto de recursos em todas as instâncias para evitar quaisquer possíveis problemas de compatibilidade.

### <a name="install-failover-cluster-feature"></a>Instalar o recurso de Cluster de Failover

Conclua as seguintes etapas para cada instância do Windows Server para instalar o recurso WSFC em cada instância. Você precisa de permissões de administrador.

1.  Abra o **Gerenciador do Servidor** no Windows Server e clique em **Adicionar Funções e Recursos** no painel direito. Isso iniciará o **Assistente para Adicionar Funções e Recursos**.

2.  Clique em **Avançar** até chegar à página **Recursos**.

3.  Selecione a caixa de seleção **Clustering de Failover** e clique em **Avançar** para concluir a instalação. Consulte a Figura 2.

    Se for solicitada a confirmação para **Adicionar recursos que são necessários para o Clustering de failover**, clique em **Adicionar Recursos**. Consulte a Figura 3.

    ![Assistente para Adicionar Funções e Recursos, Clustering de Failover](media/Fig2_SelectFeatures.png)

    Figura 2

    ![Assistente para Adicionar Funções e Recursos, necessário para o cluster de failover](media/Fig3_RequiredFeaturesFailover.png)

    Figura 3

4.  Na página **Confirmação**, clique em **Instalar** para instalar o recurso de clustering de failover.

5.  Na página **Resultado**, certifique-se de que tudo foi instalado com êxito sem erros e avisos.

### <a name="create-a-windows-server-failover-cluster"></a>Criar um novo cluster de failover do Windows Server

Depois que o recurso de WSFC é instalado em todas as instâncias, você pode configurar o WSFC. Será necessário fazer isso em apenas um nó.

1.  Abra o **Gerenciador do Servidor** no Windows Server e clique em **Gerenciador de Cluster de Failover** no menu **Ferramenta** no canto superior direito para iniciar o gerenciador.

2.  Em **Gerenciador de Cluster de Failover**, clique em **Validar Configuração** no painel direito. Consulte a Figura 4.

    ![Gerenciador de Cluster de Failover, Validar Configuração](media/Fig4_ValidateConfig.png)

    Figura 4

3.  No **Assistente para** **Validar uma Configuração**, clique em **Avançar**.

4.  Na caixa de diálogo **Selecionar Servidores ou um Cluster**, adicione os nomes de servidor que hospedarão o SQL Server e clique em **Avançar**. Consulte a Figura 5.

    Neste exemplo, adicionamos duas instâncias, MDS-HA1 e MDS-HA2.

    ![Assistente para Validar uma Configuração, página Selecionar Servidores ou um Cluster](media/Fig5_AddServer.png)

    Figura 5

5.  Na página **Opções de Teste**, clique em **Executar todos os testes** e clique em **Avançar**.

6.  Clique em **Avançar** para concluir a validação.

    A página **Validando** mostra o progresso e a página **Resumo** mostra o resumo da validação. Consulte as Figuras 6 e 7.

7.  Na página **Resumo**, verifique se há alguma mensagem de erro ou aviso.

    Os erros devem ser corrigidos. No entanto, os avisos não podem ser um problema. Uma mensagem de aviso significa que "o item testado pode atender ao requisito, mas há algo que você deve verificar". Por exemplo, a Figura 7 mostra um aviso “validar latência de acesso ao disco”, que pode ser devido ao disco estar ocupado com outras tarefas temporariamente e você pode ignorá-lo. Você deve verificar o documento online para cada um dos avisos e mensagens de erro para obter mais detalhes. Consulte a Figura 7.
 
    ![Assistente para Validar a Configuração, página Validando](media/Fig6_ValidationTests.png)

    Figura 6

    ![Assistente para Validar a Configuração, página Resumo](media/Fig7_ValidationSummary.png)

    Figura 7

8.  Na página **Resumo**, confirme se a caixa de seleção **Criar o cluster agora usando os nós de validação** está marcada e clique em **Concluir** para iniciar o **Assistente para** **Criar Cluster**.

9.  No **Assistente para** **Criar Cluster**, clique em **Avançar**.

10. Na página **Ponto de Acesso para Administrar o Cluster**, insira o nome do cluster WSFC e clique em **Avançar**. Neste exemplo, usamos "MDS-HA" como o nome do cluster. Consulte a Figura 8.

    ![Insira o nome do cluster](media/Fig8_EnterClusterName.png)

    Figura 8

11. Continue clicando em **Avançar** para concluir a criação do cluster. A seção do **Resumo do Cluster MDS-HA** exibe as informações do cluster. Consulte a Figura 9.

    ![Exibir informações de resumo para o Cluster](media/Fig9_ClusterSummary.png)

    Figura 9

    Se você precisar adicionar um nó posteriormente, clique na ação **Adicionar Nó** no painel direito no **Gerenciador de Cluster de Failover**.

Observações:

-   O recurso WSFC pode não estar disponível em todas as edições do Windows Server. Certifique-se de que sua edição tenha esse recurso.

-   Certifique-se de que você tenha as permissões adequadas para configurar o WSFC no active directory. Se houver qualquer problema, consulte [Failover Cluster Step-by-Step Guide: Configure Accounts in Active Directory](https://technet.microsoft.com/library/cc731002(v=ws.10).aspx) (Guia passo a passo do cluster de failover: configurar contas no Active Directory).

Para obter mais informações sobre o WSFC, consulte [Clusters de failover](https://technet.microsoft.com/library/cc732488(v=ws.10).aspx).

## <a name="sql-server-alwayson-availability-group"></a>Grupo de Disponibilidade AlwaysOn do SQL Server

Esta seção aborda as seguintes tarefas.

1.  [Habilitar o Grupo de Disponibilidade AlwaysOn do SQL Server](#enable-sql-server-alwayson-availability-group-on-every-sql-server-instance).

2.  [Criar um Grupo de Disponibilidade](#create-an-availability-group).

3.  [Validar e Testar o Grupo de Disponibilidade](#validation-and-test-the-availability-group).

As soluções AlwaysOn do SQLServer fornecem a recuperação de desastres e a alta disponibilidade para os bancos de dados SQLServer. O AlwaysOn tem duas soluções possíveis.
Ambas desenvolvidas com base no WSFC.

-   AG (Grupos de Disponibilidade) AlwaysOn

-   FCI (Instâncias do Cluster de Failover) do AlwaysOn.

O AG melhora a alta disponibilidade do nível do banco de dados. O AG (um conjunto de bancos de dados de usuário) e o nome de sua rede virtual são registrados como recursos no WSFC.

A FCI melhora a alta disponibilidade no nível da instância. O serviço do SQL Server e os serviços relacionados são registrados como recursos no WSFC. Além disso, a solução FCI exige o armazenamento em disco compartilhado simétrico, como compartilhamentos de arquivo SMB ou SAN, que devem estar disponíveis para todos os nós no cluster WFC.


### <a name="prerequisites"></a>Pré-requisitos

-   Instalar o SQL Server em todos os nós. Para obter mais informações, veja [Instalar o SQL Server 2016](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server).

-   (Recomendado) Instalar exatamente a mesma versão e conjunto de recursos do SQL Server em todos os nós. Em particular, o MDS deve ser instalado.

-   (Recomendado) Usar a mesma configuração em cada instância do SQL Server. Em particular, o mesmo agrupamento do servidor deve ser configurado em todas as instâncias do SQL Server.

-   (Recomendado) Usar a mesma conta de serviço para executar cada instância do SQL Server. Caso contrário, você terá que conceder permissão em cada instância do SQL Server para se certificar de que todas as instâncias do SQL Server podem se comunicar entre si.

-   Confirme se a configuração de firewall do Windows permite que as instâncias do SQL Server se comuniquem entre si.

### <a name="enable-sql-server-alwayson-availability-group-on-every-sql-server-instance"></a>Habilitar o Grupo de Disponibilidade AlwaysOn do SQL Server em todas as instâncias do SQL Server

1.  No **SQL Server Configuration Manager**, clique **Serviço do SQL Server** no painel esquerdo, clique com botão direito do mouse em **SQL Server** no painel direito e, em seguida, clique em **Propriedades**. Consulte a Figura 10.

    ![Janela Propriedades do SQL Server](media/Fig10_SQLServerProperties.png)

    Figura 10

2.  Na caixa de diálogo **Propriedades do** **SQL Server (MSSQLSERVER)**, clique na guia **Alta Disponibilidade AlwaysOn** e marque a caixa de seleção **Habilitar Grupos de Disponibilidade AlwaysOn**. Quando um valor for exibido na caixa de texto **Nome do cluster de failover do Windows**, clique em **OK** para continuar. Consulte a Figura 11.

    ![Opção Habilitar Grupos de Disponibilidade AlwaysOn](media/Fig11_EnableAlwaysOn.png)

    Figura 11

3.  Quando uma página de aviso for exibida, clique em **OK** para continuar. Consulte a Figura 12.

    ![Confirmar a parada e o reinício do serviço](media/Fig12_WarningServiceStopStart.png)

    Figura 12

4.  Clique em **Reiniciar** para reiniciar o serviço **SQL Server** e efetive essa alteração. Consulte a Figura 10.

>[!NOTE] 
>Você pode alterar a conta de serviço que executa o serviço SQL Server usando o **SQL Server Configuration Manager**. Clique na guia **Logon** na caixa de diálogo **Propriedades do** **SQL Server (MSSQLSERVER)**. Consulte a Figura 11.

### <a name="create-an-availability-group"></a>Criar um Grupo de Disponibilidade

Depois que o recurso AlwaysOn estiver habilitado em todas as instâncias do SQL Server, você poderá criar um novo AG que contém o banco de dados do MDS em um nó.

O AG pode ser criado apenas em bancos de dados existentes. Portanto, você cria um banco de dados do MDS em um nó ou cria um banco de dados temporário e, em seguida, remove o banco de dados temporário. Neste exemplo, criamos um banco de dados do MDS vazio e criamos um AG nesse banco de dados do MDS.

1.  Inicie o **SSMS** (**SQL Server Management Studio**) em um nó e conecte-se à instância local do SQL Server com as credenciais apropriadas.

2.  No SSMS, abra uma janela de **nova consulta** e execute o script a seguir para criar um banco de dados vazio. Substitua o C:\\temp pelo local que você deseja usar para executar um backup completo.

    ```
    CREATE DATABASE MDS\_Sample
    GO
    BACKUP DATABASE MDS\_Sample TO DISK='C:\\temp'
    GO
    ```

    >[!NOTE] 
    >Um backup de banco de dados completo é necessário para criar o AG nesse banco de dados.

3.  No **Pesquisador de objetos**, expanda a pasta **Alta Disponibilidade AlwaysOn** e clique em **Assistente de Novo Grupo de Disponibilidade** para iniciar o **Assistente de Novo Grupo de Disponibilidade**. Consulte a Figura 13.

    ![Iniciar o Assistente de Novo Grupo de Disponibilidade](media/Fig13_AvailabilityGroupsFolder.png)

    Figura 13

4.  No assistente de **Novo Grupo de Disponibilidade**, clique em **Avançar** para exibir a página **Especificar Nome**. Digite um nome para o AG e clique em **Avançar**. Consulte a Figura 14.

    ![Inserir o nome do Grupo de Disponibilidade](media/Fig14_AvailabilityGroupName.png)

    Figura 14

5.  Clique o banco de dados que você acabou de criar na página **Selecionar Banco de Dados** e clique em **Avançar**. Consulte a Figura 15.

    ![Selecionar o banco de dados](media/Fig15_AvailabilityGroupSelectDatabase.png)

    Figura 15

6.  Na página **Especificar Réplicas**, adicione outra réplica clicando em **Adicionar Réplica**. Esta página já lista as instâncias do SQL Server atuais locais como uma réplica. Consulte a Figura 16.

7.  Na caixa de diálogo **Conectar ao Servidor**, adicione as credenciais apropriadas e clique em **Conectar**.

    ![Conectar a uma instância do SQL Server](media/Fig16_AddReplicaConnectServer.png)

    Figura 16

    Agora você deve ver duas réplicas na lista. Repita essa etapa para adicionar outros nós como réplicas. Consulte a Figura 17.

    ![Exibir a lista de réplicas](media/Fig17_AvailabilityGroupSQLReplicas.png)

    Figura 17

    Para cada réplica, defina as seguintes configurações **Confirmação Síncrona**, **Failover Automático** e **Secundária Legível**. Consulte a Figura
17.

    **Confirmação Síncrona**: isso garante que se uma transação for confirmada na réplica primária de um banco de dados, a transação também será confirmada em todas as outras réplicas síncronas. A confirmação assíncrona não garante isso e pode atrasar a réplica primária.

    Normalmente, você deve habilitar confirmação síncrona apenas quando os dois nós estão no mesmo data center. Se eles estiverem em data centers diferentes, a confirmação síncrona poderá prejudicar o desempenho de banco de dados.

    Se essa caixa de seleção não estiver marcada, a confirmação assíncrona será usada.

    **Failover Automático:** quando a réplica primária estiver inativa, o AG realizará o failover automaticamente para sua réplica secundária quando o failover automático for selecionado. Isso só pode ser habilitado nas réplicas com confirmação síncrona.

    **Secundária Legível:** por padrão, os usuários não podem se conectar a nenhuma réplica secundária. Isso permitirá que os usuários se conectem à réplica secundária com acesso somente leitura.

8.  Na página **Especificar Réplicas**, clique na guia **Ouvinte** e faça o seguinte. Consulte a Figura 18.

    a.  Clique em **Criar um ouvinte de grupo de disponibilidade** para configurar um ouvinte de grupo de disponibilidade para a conexão de banco de dados MDS.

    b.  Insira um **Nome DNS do ouvinte**, como MDSSQLServer.

    c.  Insira a porta SQL padrão, 1433, na caixa de texto **Porta**.

    d.  Insira o DHCP na caixa de texto **Modo de Rede** e clique em **Avançar** para continuar.

    >[!NOTE] 
    >Opcionalmente, você pode escolher "IP Estático" como o **Modo de Rede** e inserir um IP estático. Você também pode inserir uma porta diferente de 1433. 

    ![Configurar o Ouvinte](media/Fig18_AvailabilityGroupCreateListener.png)

    Figura 18

9.  Na página **Selecionar Sincronização de Dados**, clique em **Completa** e especifique um compartilhamento de rede que todos os nós podem acessar. Clique em **Avançar** para continuar. Consulte a Figura 19.

    Esse compartilhamento de rede será usado para armazenar o backup do banco de dados para criar réplicas secundárias. Se isso não estiver disponível para sua organização, escolha outra preferência de sincronização de dados. Consulte [Grupo de Disponibilidade AlwaysOn do SQL Server 2016](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/always-on-availability-groups-sql-server) sobre como usar outras opções para criar réplicas secundárias. A Figura 17 também lista outras opções.

    ![Configurar a sincronização de dados](media/Fig19_AvailabilityGroupDataSync.png)

    Figura 19 

10. Na página **Validação**, certifique-se de que todas as validações sejam aprovadas com êxito e corrija os erros. Clique em **Avançar** para continuar.

11. Na página **Resumo**, examine todas as configurações e clique em **Concluir**. Isso criará o grupo de disponibilidade e o configurará.

12. Na página **Resultado**, confirme se todas as etapas necessárias foram concluídas.

### <a name="validation-and-test-the-availability-group"></a>Validação e teste do Grupo de Disponibilidade

1.  Abra o SSMS e conecte-se ao nome DNS do ouvinte que acabou de ser criado na seção [Criar um Grupo de Disponibilidade](#create-an-availability-group). Neste exemplo, é MDSSQLServer.

2.  No **Pesquisador de Objetos**, expanda a pasta **Alta Disponibilidade AlwaysOn**, clique com o botão direito do mouse no AG que acabou de criar na seção [Criar um Grupo de Disponibilidade](#create-an-availability-group) e clique em **Mostrar Painel**. Consulte a Figura 20. É exibido o status do novo AG e suas réplicas.

    ![Exibir o painel](media/Fig20_ShowDashboard.png)

    Figura 20 

3.  Clique em **Failover** para realizar um failover para uma réplica síncrona e uma réplica assíncrona. Isso é para verificar se o failover ocorre corretamente sem problemas.

 A configuração do AlwaysOn está concluída.

Para obter mais informações sobre o Grupo de Disponibilidade AlwaysOn, consulte [Grupo de Disponibilidade AlwaysOn do SQL Server 2016](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/always-on-availability-groups-sql-server).

## <a name="configure-mds-to-run-on-an-wsfc-node"></a>Configurar o MDS para ser executado em um nó WSFC

Essa solução apresentada neste artigo requer somente o banco de dados de back-end do MDS em execução no WSFC. Outras partes do MDS, como aplicativos Web e o Gerenciador de Configuração do MDS, podem ser executadas no nó no WSFC ou fora do WSFC, contanto que o MDS possa se conectar ao AG.

1.  Abra **Master Data Service Configuration Manager** em um nó, clique em **Configuração de Banco de Dados** e, em seguida, clique em **Criar Banco de Dados** para iniciar o **Assistente para Criar Banco de Dados**.

2.  Na página **Servidor de Banco de Dados**, digite o nome DNS do ouvinte do AG na caixa de texto **Instância do SQL Server**, clique em **Testar Conexão** e clique em **Avançar**. Consulte a Figura 21.

    ![Configurar o servidor de banco de dados com o ouvinte do AG](media/Fig21_MDSDatabaseServerListener.png)

    Figura 21

3.  Na página **Banco de Dados**, digite o nome do banco de dados que você criou na seção [Criar um Grupo de Disponibilidade](#create-an-availability-group) e clique em **Avançar**. Consulte a Figura 22.

    ![Criar e configurar o banco de dados](media/Fig22_MDSCreateDatabase.png)

    Figura 22

4.  Conclua o **Assistente para** **Criar Banco de Dados**. Para obter mais informações, consulte [Instalação e configuração do Master Data Services](https://docs.microsoft.com/sql/master-data-services/master-data-services-installation-and-configuration).

5.  Clique em **Aplicativos Web** em **Master Data Service Configuration Manager** para configurar o aplicativo Web e, em seguida, clique em **Aplicar** para aplicar as configurações ao MDS. Consulte a Figura 23. Para obter mais informações, consulte [Instalação e configuração do Master Data Services](https://docs.microsoft.com/sql/master-data-services/master-data-services-installation-and-configuration).

    ![Configurar o aplicativo Web](media/Fig23_MDSWebApplication.png)

    Figura 23

    A configuração do MDS foi concluída. Você pode repetir as etapas acima para configurar o MDS para ser executado em todos os nós. O banco de dados de back-end é o mesmo no mesmo AG.

6.  Se você criou um banco de dados temporário anteriormente (consulte a seção [Criar um Grupo de Disponibilidade](#create-an-availability-group)) para criar o AG AlwaysOn, deve remover o banco de dados temporário

    Para obter mais informações sobre o Master Data Service, consulte [Master Data Services](https://docs.microsoft.com/sql/master-data-services/master-data-services-overview-mds).

## <a name="conclusion"></a>Conclusão

Neste white paper, vimos como definir e configurar o banco de dados de back-end do Master Data Services sobre o Grupo de Disponibilidade AlwaysOn do SQL Server. Essa configuração fornece alta disponibilidade e recuperação de desastres no banco de dados de back-end do Master Data Services. Para implementar essa configuração, você precisa instalar e configurar o Cluster de Failover do Windows Server, o Grupo de Disponibilidade AlwaysOn do SQL Server e o Master Data Services.

## <a name="feedback"></a>Comentários

Este white paper foi útil? Envie seus comentários clicando **Comentários** na parte superior do artigo. 

Seus comentários nos ajudarão a melhorar a qualidade dos white papers que lançamos. 


