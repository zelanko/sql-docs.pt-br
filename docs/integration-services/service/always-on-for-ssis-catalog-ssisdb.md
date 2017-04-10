---
title: "Always On for SSIS Catalog (SSISDB) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.ssms.alwayson.f1"
ms.assetid: 7f089455-35ee-4c13-884e-9254b685d07d
caps.latest.revision: 17
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 16
---
# Always On for SSIS Catalog (SSISDB)
  O recurso Grupos de Disponibilidade AlwaysOn é uma solução de alta disponibilidade e recuperação de desastres que fornece uma alternativa de nível corporativo para espelhamento de banco de dados. Um grupo de disponibilidade permite um ambiente de failover para um conjunto discreto de bancos de dados de usuário, conhecidos como bancos de dados de disponibilidade, que fazem failover juntos. Para obter mais informações, confira [Grupos de Disponibilidade AlwaysOn](https://msdn.microsoft.com/library/hh510230.aspx).  
  
 Para fornecer a alta disponibilidade ao catálogo do SSIS (SSISDB) e seu conteúdo (projetos, pacotes, logs de execução, etc.), você pode adicionar o banco de dados do SSISDB (da mesma forma que qualquer outro banco de dados de usuário) a um Grupo de Disponibilidade AlwaysOn. Quando ocorre um failover, um dos nós secundários automaticamente se torna o novo nó primário.  
 
 > [!IMPORTANT]  Quando ocorre um failover, os pacotes que estavam em execução não reiniciam ou retomam. 
 
 **Neste tópico:**  
  
1.  [Pré-requisitos](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#prereq)  
  
2.  [Configurar o suporte do SSIS para Always On](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Firsttime)  
  
3.  [Atualizando o SSISDB em um grupo de disponibilidade](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Upgrade)  
  
##  <a name="a-nameprereqa-prerequisites"></a><a name="prereq"></a> Pré-requisitos  
 Você deve executar as seguintes etapas de pré-requisito antes de habilitar o suporte do Always On para o banco de dados do SSISDB.  
  
1.  Configurar um cluster de failover do Windows. Confira a postagem do blog [Installing the Failover Cluster Feature and Tools for Windows Server 2012](http://blogs.msdn.com/b/clustering/archive/2012/04/06/10291601.aspx) (Instalando o recurso Cluster de Failover e as Ferramentas para o Windows Server 2012) para obter instruções. Você deve instalar o recurso e as ferramentas em todos os nós de cluster.  
  
2.  Instalar o recurso SSIS (SQL Server 2016 com Integration Services) em cada nó do cluster.  
  
3.  Habilitar o recurso Always On para cada instância do SQL Server. Confira [Habilitar Grupos de Disponibilidade Always On](https://msdn.microsoft.com/library/ff878259.aspx) para obter detalhes.  
  
##  <a name="a-namefirsttimea-configure-ssis-support-for-always-on"></a><a name="Firsttime"></a> Configurar o suporte do SSIS para Always On  
  
-   [Etapa 1: Criar o catálogo do Integration Services](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Step1)  
  
-   [Etapa 2: Adicionar o SSISDB a um Grupo de Disponibilidade Always On](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Step2)  
  
-   [Etapa 3: Habilitar o suporte do SSIS para o Always On](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Step3)  
  
> [!IMPORTANT]  
>  -   Você deve executar estas etapas no **nó primário** do grupo de disponibilidade.  
> -   Você deve habilitar o **Suporte do SSIS para Always On** após adicionar o SSISDB a um grupo Always On.  
  
###  <a name="a-namestep1a-step-1-create-integration-services-catalog"></a><a name="Step1"></a> Etapa 1: Criar o catálogo do Integration Services  
  
1.  Inicie o **SQL Server Management Studio** e o conecte a uma instância do SQL Server no cluster que você deseja definir como o **nó primário** do grupo de alta disponibilidade do Always On para SSISDB.  
  
2.  No Pesquisador de Objetos, expanda o nó de servidor, clique com o botão direito do mouse no nó **Catálogos do Integration Services** e clique em **Criar Catálogo**.  
  
3.  Clique em **Habilitar Integração CLR**. Esse catálogo usa procedimentos armazenados CLR.  
  
4.  Clique em **Habilitar a execução automática de procedimento armazenado do Integration Services na inicialização do SQL Server** para habilitar o procedimento armazenado [catalog.startup](https://msdn.microsoft.com/library/hh230984.aspx) a ser executado toda vez que a instância do servidor SSIS for reiniciada. O procedimento armazenado executa a manutenção do estado das operações para o catálogo SSISDB. Ele corrigirá o status de todos os pacotes que estavam sendo executados se e quando a instância do servidor SSIS ficar inoperante.  
  
5.  Digite uma **senha**e clique em **OK**. A senha protege a chave mestra do banco de dados que é usada para criptografar os dados do catálogo. Salve a senha em um local seguro. É recomendado que você também faça backup da chave mestra do banco de dados. Para obter mais informações, consulte [Back Up a Database Master Key](https://msdn.microsoft.com/library/aa337546.aspx).  
  
###  <a name="a-namestep2a-step-2-add-ssisdb-to-an-always-on-availability-group"></a><a name="Step2"></a> Etapa 2: Adicionar o SSISDB a um Grupo de Disponibilidade Always On  
 Adicionar o banco de dados do SSISDB a um Grupo de Disponibilidade Always On é quase igual a adicionar qualquer outro banco de dados de usuário em um grupo de disponibilidade. Confira [Use the Availability Group Wizard](https://msdn.microsoft.com/library/hh403415.aspx)(Usar o assistente do Grupo de Disponibilidade).  
  
 Você precisa fornecer a senha que especificou ao criar o Catálogo do SSIS na página **Selecionar Bancos de Dados** do assistente **Novo Grupo de Disponibilidade** .  
  
 ![New Availability Group](../../integration-services/service/media/ssis-newavailabilitygroup.png "New Availability Group")  
  
###  <a name="a-namestep3a-step-3-enable-ssis-support-for-always-on"></a><a name="Step3"></a> Etapa 3: Habilitar o suporte do SSIS para o Always On  
 Depois de criar o Catálogo do Integration Services, clique com o botão direito do mouse no nó **Catálogos do Integration Services** e clique em **Habilitar Suporte do Always On...**. Você deve ver a seguinte caixa de diálogo **Habilitar Suporte para Always On** . Se esse item de menu estiver desabilitado, verifique se você tem todos os pré-requisitos instalados e clique em **Atualizar**.  
  
 ![Enable Support for AlwaysOn](../../integration-services/service/media/ssis-enablesupportforalwayson.png "Enable Support for AlwaysOn")  
  
> [!WARNING]  
>  O failover automático do banco de dados do SSISDB só será permitido quando você habilitar o Suporte do SSIS para o Always On.  
  
 As réplicas secundárias recentemente adicionadas do grupo de disponibilidade AlwaysOn serão mostradas na tabela. Clique em **Conectar …** de cada réplica na lista e digite as credenciais de autenticação para se conectar à réplica. A conta de usuário deve ser membro do grupo sysadmin em cada réplica para habilitar o suporte do SSIS para Always On. Depois de se conectar com êxito a cada réplica, clique em **OK** para habilitar o suporte do SSIS para Always On.  
  
##  <a name="a-nameupgradea-upgrading-ssisdb-in-an-availability-group"></a><a name="Upgrade"></a> Atualizando o SSISDB em um grupo de disponibilidade  
 Se estiver atualizando o SQL Server de uma versão anterior, e o SSISDB estiver em um grupo de disponibilidade Always On, sua atualização poderá ser bloqueada pela regra "Verificação do SSISDB no Grupo de Disponibilidade Always On". Esse bloqueio ocorre porque a atualização é executada no modo de usuário único, enquanto um banco de dados de disponibilidade deve ser um banco de dados de multiusuário. Portanto, durante a atualização ou a aplicação de patch, todos os bancos de dados de disponibilidade, incluindo o SSISDB, são colocados no modo offline e não são atualizados nem corrigidos. Para que a atualização continue, você precisa remover o SSISDB do grupo de disponibilidade, atualizar ou corrigir cada nó e adicionar o SSISDB de volta ao grupo de disponibilidade.  
  
 Se você estiver bloqueado pela regra "Verificação do SSISDB no Grupo de Disponibilidade Always On", será preciso seguir estas etapas para atualizar o SQL Server.  
  
1.  Remova o banco de dados do SSISDB do grupo de disponibilidade. Para obter mais informações, veja [Remover um banco de dados secundário de um grupo de disponibilidade &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/remove-a-secondary-database-from-an-availability-group-sql-server.md) e [Remover um banco de dados primário de um grupo de disponibilidade &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md).  
  
2.  Clique em **Executar novamente** no assistente de atualização. A regra "Verificação do SSISDB no Grupo de Disponibilidade Always On" passará.  
  
3.  Clique em **Avançar** para continuar a atualização.  
  
4.  Depois de atualizar todos os nós, adicione o banco de dados do SSISDB de volta ao grupo de disponibilidade Always On. Para obter mais informações, consulte [Adicionar um banco de dados a um grupo de disponibilidade &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/add-a-database-to-an-availability-group-sql-server.md).  
  
 Se você não estiver bloqueado ao fazer a atualização do SQL Server, e o SSISDB estiver em um grupo de disponibilidade Always On, será preciso fazer a atualização do SSISDB separadamente depois de fazer a atualização do mecanismo de banco de dados do SQL Server. Use o Assistente de Atualização do SSIS para atualizar o SSISDB, conforme descrito no procedimento a seguir.  
  
1.  Mova o banco de dados do SSISDB para fora do grupo de disponibilidade ou exclua o grupo de disponibilidade se o SSISDB for o único banco de dados no grupo de disponibilidade. Você precisa iniciar o **SQL Server Management Studio** no **nó primário** do grupo de disponibilidade para executar essa tarefa.  
  
2.  Remova o banco de dados do SSISDB de todos os **nós de réplica**.  
  
3.  Atualize o banco de dados do SSISDB no **nó primário**. No**Pesquisador de Objetos** do SQL Server Management Studio, expanda **Catálogos do Integration Services**, clique com o botão direito do mouse em **SSISDB**e selecione **Atualização do Banco de Dados**. Siga as instruções do **Assistente de Atualização do SSISDB** para atualizar o banco de dados. Você precisa iniciar o **Assistente de Atualização do SSISDB** localmente no **nó primário**.  
  
4.  Siga as instruções em [Etapa 2: Adicionar o SSISDB a um Grupo de Disponibilidade Always On](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Step2) para adicionar o SSISDB a um grupo de disponibilidade.  
  
5.  Siga as instruções em [Etapa 3: Habilitar o suporte do SSIS para o Always On](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Step3).  
  
  