---
title: "Alta disponibilidade e recuperação de desastres para Master Data Services | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: sabotta
ms.author: carlasab
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2afbf59101a0605dba2e79f09777160cb4de5cab
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---



# <a name="high-availability-and-disaster-recovery-for-master-data-services"></a>Alta disponibilidade e recuperação de desastres para Master Data Services

**Resumo:** este artigo descreve uma solução para Master Data Service (MDS) hospedado em uma configuração do grupo de disponibilidade AlwaysOn. Esse artigo descreve como instalar e configurar o SQL 2016 Master Data Services em um grupo de disponibilidade (AG) AlwaysOn do SQL 2016. O objetivo principal dessa solução é melhorar a alta disponibilidade e recuperação de desastres de dados de back-end do MDS hospedados em um banco de dados SQL Server.

## <a name="introduction"></a>Introdução


Este artigo descreve uma solução para Master Data Service (MDS) hospedado em uma configuração de grupo de disponibilidade do AlwaysOn. O artigo descreve como instalar e configurar o SQL 2016 MDS em um grupo de disponibilidade do AlwaysOn do SQL 2016 (AG). O objetivo principal dessa solução é melhorar a alta disponibilidade e recuperação de desastres de dados de back-end do MDS hospedados em um banco de dados SQL Server.

Para implementar a solução, você precisa concluir as seguintes tarefas abordadas neste artigo.

1.  [Instalar e configurar o backup do Windows Server Failover cluster (WSFC)](#windows-server-failover-cluster-wsfc).

2.  [Configurar o grupo de disponibilidade do AlwaysOn](#sql-server-alwayson-availability-group).

3.  [Configure o MDS para ser executado em um nó WSFC](#configure-mds-to-run-on-an-wsfc-node).

As seções acima brevemente apresentará as tecnologias, seguidas por instruções. Para obter informações detalhadas sobre as tecnologias, examine os documentos vinculados a cada seção.

Essa solução descrita neste artigo é criada sobre o SQL Server AlwaysOn AG, no qual cada banco de dados tem várias réplicas síncronas ou assíncronas. Apenas uma réplica aceita a transação (aceita solicitações de usuário). Esta é a réplica primária.

Cada réplica tem seu próprio armazenamento, portanto, não há nenhum armazenamento compartilhado centralizado nesta solução. Quando há uma falha de software ou uma falha de hardware que afetam a réplica primária, a réplica primária pode fazer failover para uma réplica de síncrona ou assíncrona manualmente ou automaticamente com base na configuração e situações. Isso garante a alta disponibilidade do banco de dados com interrupção mínima para os usuários.

Réplicas assíncronas são hospedadas em um data center remoto do Centro de dados da réplica primária. No caso de cenários de desastre, a réplica primária pode fazer failover para outro data center. Isso garante a recuperação de desastres do banco de dados.

Para fins de demonstração, a solução descrita neste artigo usa as seguintes versões do software. Versões mais antigas devem funcionar mesmo com potencialmente pequenas diferenças.

-   Windows Server 2012R2 com o cluster de Failover do servidor

-   Com o recurso serviço de dados mestre do SQL Server 2016

Além disso, a solução usa duas VMs, **MDS HA1** e **MDS HA2**, hospedar duas réplicas. Desde que ele é suportado pelo SQL Server AlwaysOn AG, o MDS não limita quantas réplicas que você pode usar.

Este artigo pressupõe que você tenha um conhecimento básico sobre Cluster de Failover do Windows Server, Windows Server, SQL Server AlwaysOn e MDS do SQL Server.

## <a name="what-is-not-covered"></a>O que não é coberto

Este documento não aborda o seguinte:

-   Como fazer o IIS, o servidor web que hospeda o mestre de serviço de dados da interface do usuário, altamente disponível e recuperável após um desastre. MDS não impõe nenhum requisito específico no IIS, para que as técnicas padrão para tornar o IIS altamente disponível e o balanceamento de carga podem trabalhar aqui também.

-   Como usar o cluster de failover (FCI) do SQL Server AlwaysOn para oferecer suporte a alta disponibilidade (HA) no back-end de MDS. Clustering de failover do SQL Server é uma solução de alta disponibilidade diferente e é oficialmente suportado pelo SQL Server, e ele funciona com o MDS.

-   Como usar uma solução de cluster de failover do SQL Server (FCI) e o grupo de disponibilidade do AlwaysOn para oferecer suporte a alta disponibilidade no MDS back-end. A solução híbrida funciona com o MDS.

## <a name="design-consideration"></a>Considerações de design

A Figura 1 mostra uma configuração típica usada principalmente em grupo de disponibilidade do AlwaysOn. No data center primário, há duas réplicas com uma relação de confirmação síncrona e ambas as réplicas têm o privilégio de VOTO. Isso é usado principalmente para melhorar a alta disponibilidade no caso da réplica primária falhar.

O Data Center de recuperação de desastres, há uma réplica secundária com uma relação de confirmação assíncrona com o primário. Essa data center geralmente está em uma região geográfica diferente do data center principal. A réplica secundária não tem o privilégio de VOTO.

Essa configuração é usada para atingir a recuperação no caso de data center primário está em um desastre, como um incêndio, terremoto, etc. A configuração atinge dois alta disponibilidade e recuperação de desastres com custo relativamente baixo.

![Configuração típica para o grupo de disponibilidade do AlwaysOn](media/Fig1_TypicalConfig.png)

Figura 1. Uma configuração típica grupo de disponibilidade do AlwaysOn

Se você não precisa considerar a recuperação de desastres, você não precisa ter uma réplica em um segundo data center. Se você precisar aumentar a alta disponibilidade, você pode ter mais de réplicas síncronas no mesmo data center primário com.

Assim é importante considerar suas necessidades e os cenários e escolha quantas réplicas síncronas e assíncronas, você precisará e quais dados center, você deve colocá-los em.

## <a name="windows-server-failover-cluster-wsfc"></a>Cluster de Failover do Windows Server (WSFC)

Esta seção aborda as seguintes tarefas.

1.  [Instalar o recurso de Cluster de Failover do Windows](#install-failover-cluster-feature).

2.  [Criar um Cluster de Failover do Windows Server](#create-a-windows-server-failover-cluster).

Conforme mostrado na Figura 1 na seção anterior, a solução descrita neste artigo inclui o Windows Server Failover Cluster (WSFC). É preciso configurar WSFC porque o SQL AlwaysOn depende WFSC para failover e detecção de falha.

WSFC é um recurso para melhorar a alta disponibilidade de aplicativos e serviços. Ele consiste em um grupo de instâncias de servidor independente do windows com o serviço de Cluster de Failover do Microsoft em execução nessas instâncias. As instâncias de servidor do windows (ou nós conforme eles são chamados às vezes) estão conectados para que elas possam se comunicar entre si, e a detecção de falha possíveis. WSFC fornecem as funcionalidades de detecção e failover de falha. Se um nó ou um serviço falhar no cluster, em seguida, a falha é detectada e outro nó automaticamente ou manualmente começa a fornecer os serviços hospedados no nó com falha. Como tal, usuários apenas sofrer interrupções mínimo nos serviços e disponibilidade do serviço é aprimorada.  

### <a name="prerequisites"></a>Pré-requisitos

O sistema operacional Windows Server é instalado em todas as instâncias e todas as atualizações sejam corrigidas.

>[!NOTE] 
>É **altamente recomendável** que você instale a mesma versão do Windows e o mesmo recurso definidas em todas as instâncias para evitar possíveis problemas de compatibilidade.

### <a name="install-failover-cluster-feature"></a>Instalar o recurso Cluster de Failover

Conclua as seguintes etapas para cada instância do servidor do Windows instalar o recurso do WSFC em cada instância. Você precisa de permissões de administrador.

1.  Abra **Gerenciador do servidor** no Windows Server e clique em **adicionar funções e recursos** no painel direito. Isso iniciará o **assistente Adicionar funções e recursos**.

2.  Clique em **próximo** até chegar a **recursos** página.

3.  Selecione o **Clustering de Failover** caixa de seleção e, em seguida, clique em **próximo** para concluir a instalação. Consulte a Figura 2.

    Se você for solicitado a confirmar a **adicionar recursos que são necessários para o cluster de Failover**, clique em **adicionar recursos**. Consulte a Figura 3.

    ![Adicionar Assistente de funções e recursos de Clustering de Failover](media/Fig2_SelectFeatures.png)

    Figura 2

    ![Adicionar Assistente de funções e recursos necessários para o cluster de failover](media/Fig3_RequiredFeaturesFailover.png)

    Figura 3

4.  Sobre o **confirmação** , clique em **instalar** para instalar o recurso cluster de failover.

5.  Sobre o **resultados** página, verifique se tudo foi instalado com êxito sem erros e avisos.

### <a name="create-a-windows-server-failover-cluster"></a>Criar um novo cluster de failover do Windows Server

Depois que o recurso WSFC é instalado em todas as instâncias, você pode configurar o WSFC. Só será necessário fazer isso em um nó.

1.  Abra **Gerenciador do servidor** no Windows Server e clique em **Gerenciador de Cluster de Failover** no **ferramenta** menu no canto superior direito para iniciar o Gerenciador.

2.  Em **Gerenciador de Cluster de Failover**, clique em **validar configuração** no painel direito. Consulte a Figura 4.

    ![Gerenciador de Cluster de failover, validar configuração](media/Fig4_ValidateConfig.png)

    Figura 4

3.  No **validar uma configuração** **assistente**, clique em **próximo**.

4.  No **selecionar servidores ou um Cluster** caixa de diálogo caixa, adicione os nomes dos servidores que hospedam o SQL Server e, em seguida, clique em **próximo**. Consulte a Figura 5.

    Neste exemplo, adicionamos duas instâncias, MDS HA1 e HA2 do MDS.

    ![Validar um Assistente de configuração, selecionar servidores ou uma página de Cluster](media/Fig5_AddServer.png)

    Figura 5

5.  Sobre o **opções de teste** , clique em **executar todos os testes**e, em seguida, clique em **próximo**.

6.  Clique em **próximo** para concluir a validação.

    O **Validando** página mostra o progresso e o **resumo** página mostra o resumo de validação. Consulte figuras 6 e 7.

7.  Sobre o **resumo** página, verifique as mensagens de aviso ou erro.

    Erros devem ser corrigidos. No entanto, os avisos não podem ser um problema. Uma mensagem de aviso significa que "o item testado pode atender ao requisito, mas há algo que você deve verificar". Por exemplo, a Figura 7 mostra um "validar latência de acesso" aviso, que pode ser devido a disco sendo temporariamente ocupado em outras tarefas, e você pode ignorá-lo. Você deve verificar o documento online para cada um dos avisos e mensagens de erro para obter mais detalhes. Consulte a Figura 7.
 
    ![Validar o Assistente de configuração, página Validando](media/Fig6_ValidationTests.png)

    Figura 6

    ![Validar um Assistente de configuração, a página de resumo](media/Fig7_ValidationSummary.png)

    Figura 7

8.  No **resumo** , confirme que o **criar o cluster agora usando os nós validados** caixa de seleção está selecionada e, em seguida, clique em **concluir** para iniciar o **criar Cluster** **assistente**.

9.  No **criar Cluster** **assistente**, clique em **próximo**.

10. Sobre o **ponto de acesso para administrar o Cluster** página, insira o nome do cluster WSFC e, em seguida, clique em **próximo**. Neste exemplo, usamos "MDS HA" como o nome do cluster. Consulte a Figura 8.

    ![Insira o nome do Cluster](media/Fig8_EnterClusterName.png)

    Figura 8

11. Continue clicando em **próximo** para concluir a criação do cluster. O **resumo do Cluster MDS HA** seção exibe as informações de cluster. Consulte a Figura 9.

    ![Exibir informações de resumo para o Cluster](media/Fig9_ClusterSummary.png)

    Figura 9

    Se você precisar adicionar um nó posteriormente, clique em **adicionar nó** ação no painel à direita no **Gerenciador de Cluster de Failover**.

Observações:

-   O recurso do WSFC pode não estar disponível em todas as edições do Windows Server. Certifique-se de que sua edição tem esse recurso.

-   Verifique se que você tem as permissões adequadas para configurar WSFC no active directory. Se houver qualquer problema, consulte [guia do passo a passo de Cluster de Failover: configurar contas no Active Directory](https://technet.microsoft.com/library/cc731002(v=ws.10).aspx).

Para obter mais informações sobre WSFC, consulte [Clusters de Failover](https://technet.microsoft.com/library/cc732488(v=ws.10).aspx).

## <a name="sql-server-alwayson-availability-group"></a>Grupo de Disponibilidade AlwaysOn do SQL Server

Esta seção aborda as seguintes tarefas.

1.  [O grupo de disponibilidade do Enable SQL Server AlwaysOn](#enable-sql-server-alwayson-availability-group-on-every-sql-server-instance).

2.  [Criar um grupo de disponibilidade](#create-an-availability-group).

3.  [Validar e testar o grupo de disponibilidade](#validation-and-test-the-availability-group).

Soluções do SQLServer AlwaysOn fornecem alta disponibilidade e recuperação de desastres para bancos de dados do SQL Server. AlwaysOn tem duas soluções possíveis.
São desenvolvidos com base no WSFC.

-   Grupos de disponibilidade do AlwaysOn (AG)

-   As instâncias de Cluster de Failover do AlwaysOn (FCI).

AG aprimora a disponibilidade de alto nível do banco de dados. O grupo de disponibilidade (um conjunto de bancos de dados do usuário) e seu nome de rede virtual são registrados como recursos no WSFC.

FCI aprimora a disponibilidade de alto nível de instância. Serviço do SQL Server e os serviços relacionados são registrados como recursos no WSFC. Além disso, a solução FCI exige armazenamento em disco compartilhado simétrico, como compartilhamentos de arquivos de SAN ou SMB, que deve estar disponível para todos os nós no cluster WFC.


### <a name="prerequisites"></a>Pré-requisitos

-   Instale o SQL Server em todos os nós. Para obter mais informações, veja [Instalar o SQL Server 2016](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server).

-   (Recomendado) Instale o conjunto exato de recurso do mesmo SQL Server e a versão em cada nó. Em particular, o MDS deve ser instalado.

-   (Recomendado) Use a mesma configuração em cada instância do SQL Server. Em particular, o mesmo agrupamento do servidor deve ser configurado em todas as instâncias do SQL Server.

-   (Recomendado) Use a mesma conta de serviço para executar cada instância do SQL Server. Caso contrário, você terá que conceder permissão em cada instância do SQL Server para certificar-se de que as instâncias do SQL Server podem se comunicar entre si.

-   Confirme que a configuração de firewall do Windows permite que as instâncias do SQL Server para se comunicar entre si.

### <a name="enable-sql-server-alwayson-availability-group-on-every-sql-server-instance"></a>Grupo de disponibilidade do AlwaysOn do Enable SQL Server em cada instância do SQL Server

1.  No **SQL Server Configuration Manager** clique **serviço do SQL Server** no painel esquerdo, clique com botão direito **do SQL Server** no painel direito e, em seguida, clique **propriedades**. Consulte a Figura 10.

    ![Janela de propriedades do SQL Server](media/Fig10_SQLServerProperties.png)

    Figura 10

2.  No **SQL Server (MSSQLSERVER)** **propriedades** caixa de diálogo, clique o **alta disponibilidade AlwaysOn** guia e, em seguida, selecione o **habilitar grupos de disponibilidade do AlwaysOn** caixa de seleção. Quando um valor não exibirá o **nome de cluster de failover do Windows** caixa de texto, clique em **Okey** para continuar. Consulte a Figura 11.

    ![Habilitar a opção de grupos de disponibilidade AlwaysOn](media/Fig11_EnableAlwaysOn.png)

    Figura 11

3.  Quando uma página de aviso será exibida, clique em **Okey** para continuar. Consulte a Figura 12.

    ![Confirmar para parar e reiniciar o serviço](media/Fig12_WarningServiceStopStart.png)

    Figura 12

4.  Clique em **reiniciar**, reinicie o **do SQL Server** de serviço e para efetivar a alteração. Consulte a Figura 10.

>[!NOTE] 
>Você pode alterar a conta de serviço que executa o serviço do SQL Server usando o **SQL Server Configuration Manager**. Clique o **logon** guia o **SQL Server (MSSQLSERVER)** **propriedades** caixa de diálogo. Consulte a Figura 11.

### <a name="create-an-availability-group"></a>Criar um grupo de disponibilidade

Depois que o recurso AlwaysOn está habilitado em todas as instâncias do SQL Server, você pode criar um novo grupo de disponibilidade que contém o banco de dados do MDS em um nó.

AG só pode ser criado em bancos de dados existentes. Portanto a você criar um banco de dados do MDS em um nó, ou criar um banco de dados temporário e, em seguida, solte o banco de dados temporário. Neste exemplo, vamos criar um banco de dados emptyMDS e criar um grupo de disponibilidade neste banco de dados do MDS.

1.  Iniciar **SQL Server Management Studio** (**SSMS**) em um nó e conecte-se à instância local do SQL Server com as credenciais apropriadas.

2.  No SSMS, abra um **nova consulta** janela e execute o script a seguir para criar um banco de dados vazio. Substitua o c:\\temp com o local que você deseja usar para executar um backup completo.

    ```
    CREATE DATABASE MDS\_Sample
    GO
    BACKUP DATABASE MDS\_Sample TO DISK='C:\\temp'
    GO
    ```

    >[!NOTE] 
    >Um backup de banco de dados completo é necessário para criar o grupo de disponibilidade neste banco de dados.

3.  No **Pesquisador de objetos**, expanda o **alta disponibilidade AlwaysOn** pasta e clique em **Assistente de novo grupo de disponibilidade** para iniciar o **Assistente de novo grupo de disponibilidade**. Consulte a Figura 13.

    ![Assistente para iniciar o novo grupo de disponibilidade](media/Fig13_AvailabilityGroupsFolder.png)

    Figura 13

4.  No **novo grupo de disponibilidade** assistente, clique em **próximo** para exibir o **especificar nome** página. Digite um nome para o grupo de disponibilidade e, em seguida, clique em **próximo**. Consulte a Figura 14.

    ![Digite o nome do grupo de disponibilidade](media/Fig14_AvailabilityGroupName.png)

    Figura 14

5.  Clique o banco de dados que você acabou de criar no **Selecionar banco de dados** página e, em seguida, clique em **próximo**. Consulte a Figura 15.

    ![Selecione o banco de dados](media/Fig15_AvailabilityGroupSelectDatabase.png)

    Figura 15

6.  Sobre o **especificar réplicas** página, adicione outra réplica clicando **adicionar réplica**. Esta página lista já instâncias do SQL Server atuais, locais como uma réplica. Consulte a Figura 16.

7.  No **conectar ao servidor** caixa de diálogo caixa, adicione as credenciais apropriadas e clique em **conectar**.

    ![Conectar a uma instância do SQL Server](media/Fig16_AddReplicaConnectServer.png)

    Figura 16

    Agora você deve ver duas réplicas da lista. Repita essa etapa para adicionar outros nós como réplicas. Consulte a Figura 17.

    ![Exiba a lista de réplicas](media/Fig17_AvailabilityGroupSQLReplicas.png)

    Figura 17

    Para cada réplica, configure o seguinte **confirmação síncrona**, **Failover automático**, e **secundária legível** configurações. Consulte a Figura
17.

    **Confirmação síncrona**: Isso garante que se uma transação é confirmada na réplica primária de um banco de dados, em seguida, a transação é também confirmada em todas as outras réplicas síncronas. Confirmação assíncrona não garante que isso, e ele pode atrasar a réplica primária.

    Normalmente, você deve habilitar confirmação síncrona apenas quando os dois nós estão no mesmo data center. Se eles estiverem em data centers diferentes, confirmação síncrona pode prejudicar o desempenho de banco de dados.

    Se essa caixa de seleção não estiver selecionada, a confirmação assíncrona é usada.

    **Failover automático:** quando a réplica primária está inativo, o grupo de disponibilidade fará o failover automaticamente à réplica secundária quando o failover automático é selecionado. Isso só pode ser habilitado nas réplicas com confirmação síncrona.

    **Secundária legível:** por padrão, os usuários não podem se conectar a qualquer réplica secundária. Isso permitirá que os usuários conectem-se à réplica secundária com acesso somente leitura.

8.  Sobre o **especificar réplicas** , clique no **ouvinte** guia e faça o seguinte. Consulte a Figura 18.

    A.  Clique em **criar um ouvinte de grupo de disponibilidade** para configurar um ouvinte de grupo de disponibilidade para a conexão de banco de dados do MDS.

    B.  Insira um **nome DNS do ouvinte**, como MDSSQLServer.

    c.  Insira a porta SQL padrão, 1433, no **porta** caixa de texto.

    d.  Insira o DHCP no **modo de rede** caixa de texto e clique **próximo** para continuar.

    >[!NOTE] 
    >Opcionalmente, você pode escolher "IP estático" como o **modo de rede** e insira um endereço IP estático. Você também pode inserir uma porta diferente de 1433. 

    ![Configurar o ouvinte](media/Fig18_AvailabilityGroupCreateListener.png)

    Figura 18

9.  Sobre o **selecionar sincronização de dados** , clique em **completo**e especifique um compartilhamento de rede que podem acessar todos os nós. Clique em **Avançar** para continuar. Consulte a Figura 19.

    Esse compartilhamento de rede será usado para armazenar o backup do banco de dados para criar réplicas secundárias. Se isso não está disponível para sua organização, escolha outro preferência de sincronização de dados. Consulte [grupo de disponibilidade do AlwaysOn do SQL Server 2016](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/always-on-availability-groups-sql-server) sobre como usar outras opções para criar réplicas secundárias. A Figura 17 também lista outras opções.

    ![Configurar a sincronização de dados](media/Fig19_AvailabilityGroupDataSync.png)

    Figura 19 

10. Sobre o **validação** página, verifique se todas as validações transcorrem com êxito e corrigir os erros. Clique em **Avançar** para continuar.

11. Sobre o **resumo** página, examine todas as configurações e clique em **concluir**. Isso criará o grupo de disponibilidade e configurá-lo.

12. Sobre o **resultados** , confirme se todas as etapas necessárias foram concluídas.

### <a name="validation-and-test-the-availability-group"></a>O grupo de disponibilidade de teste e validação

1.  Abra o SSMS e conecte-se para o nome DNS do ouvinte acabou de criar no [criar um grupo de disponibilidade](#create-an-availability-group) seção. Neste exemplo, é MDSSQLServer.

2.  Em **Pesquisador de objetos**, expanda o **alta disponibilidade AlwaysOn** pasta, o grupo de disponibilidade que você acabou criado no botão direito do mouse o [criar um grupo de disponibilidade](#create-an-availability-group) seção e, em seguida, clique em **Mostrar painel**. Consulte a Figura 20. É exibido o status do novo grupo de disponibilidade e suas réplicas.

    ![Exibir o painel](media/Fig20_ShowDashboard.png)

    Figura 20 

3.  Clique em **Failover** fazer um failover para uma réplica de síncrona e uma réplica assíncrona. Isso é verificar que se o failover corretamente ocorra sem problemas.

 A configuração de AlwaysOn é concluída.

Para obter mais informações sobre o grupo de disponibilidade AlwaysOn, consulte [grupo de disponibilidade do AlwaysOn do SQL Server 2016](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/always-on-availability-groups-sql-server).

## <a name="configure-mds-to-run-on-an-wsfc-node"></a>Configure o MDS para ser executado em um nó do WSFC

Essa solução apresentada neste artigo requer somente o banco de dados de back-end do MDS em execução no WSFC. Outras partes do MDS, como aplicativos web e o MDS configuration manager, podem ser executados no nó no WSFC ou fora de WSFC, desde que o MDS pode conectar-se para o grupo de disponibilidade.

1.  Abra **Gerenciador de configuração do Master Data Service** em um nó, clique em **configuração de banco de dados**e, em seguida, clique em **criar banco de dados** para iniciar o **criar Assistente de banco de dados**.

2.  No **o servidor de banco de dados** página, digite o nome DNS do ouvinte AG no **instância do SQL Server** caixa de texto, clique em **Conexão de teste**e, em seguida, clique em **próximo**. Consulte a Figura 21.

    ![Configurar o servidor de banco de dados com o ouvinte do AG](media/Fig21_MDSDatabaseServerListener.png)

    Figura 21

3.  No **banco de dados** página, digite o nome do banco de dados que você criou no [criar um grupo de disponibilidade](#create-an-availability-group) seção e, em seguida, clique em **próximo**. Consulte a Figura 22.

    ![Criar e configurar o banco de dados](media/Fig22_MDSCreateDatabase.png)

    A Figura 22

4.  Concluir o **criar banco de dados** **assistente**. Para obter mais informações, consulte [configuração e instalação do Master Data Services](https://docs.microsoft.com/sql/master-data-services/master-data-services-installation-and-configuration).

5.  Clique em **aplicativos Web** na **Gerenciador de configuração do Master Data Service** para configurar o aplicativo Web e, em seguida, clique em **aplicar** para aplicar as configurações no MDS. Consulte a Figura 23. Para obter mais informações, consulte [configuração e instalação do Master Data Services](https://docs.microsoft.com/sql/master-data-services/master-data-services-installation-and-configuration).

    ![Configurar o aplicativo Web](media/Fig23_MDSWebApplication.png)

    Figura 23

    A instalação do MDS é concluída. Você pode repetir as etapas acima para configurar o MDS para ser executado em todos os nós. O banco de dados de back-end é o mesmo na mesma AG.

6.  Se você criou um banco de dados temporário (consulte [criar um grupo de disponibilidade](#create-an-availability-group) seção) para criar o grupo de disponibilidade do AlwaysOn, em seguida, você deve descartar o banco de dados temporário

    Para obter mais informações sobre o serviço de dados mestre, consulte [Master Data Services](https://docs.microsoft.com/sql/master-data-services/master-data-services-overview-mds).

## <a name="conclusion"></a>Conclusão

Este white paper, vimos como instalar e configurar o banco de dados de back-end do Master Data Services na parte superior do grupo de disponibilidade do AlwaysOn do SQL Server. Essa configuração fornece alta disponibilidade e recuperação de desastres do banco de dados de back-end do Master Data Services. Para implementar essa configuração, você precisa instalar e configurar o Windows Server Failover Cluster, SQL Server AlwaysOn grupo de disponibilidade e o Master Data Services.

## <a name="feedback"></a>Comentários

Este white paper foi útil? Envie seus comentários clicando **comentários** na parte superior do artigo. 

Seus comentários nos ajudarão a melhorar a qualidade dos white papers que lançamos. 


