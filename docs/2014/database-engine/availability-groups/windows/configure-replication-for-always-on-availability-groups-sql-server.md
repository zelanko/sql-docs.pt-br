---
title: Configurar a replicação para Grupos de Disponibilidade AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], interoperability
- replication [SQL Server], AlwaysOn Availability Groups
ms.assetid: 4e001426-5ae0-4876-85ef-088d6e3fb61c
caps.latest.revision: 14
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a57ba4393c23920b98a407176de51034715a54c6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37229596"
---
# <a name="configure-replication-for-always-on-availability-groups-sql-server"></a>Configurar a replicação para Grupos de Disponibilidade AlwaysOn (SQL Server)
  A configuração dos grupos de disponibilidade AlwaysOn e da replicação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] envolve sete etapas. Cada etapa está descrita com mais detalhes nas seções a seguir.  
  

  
##  <a name="step1"></a> 1. Configurar as publicações de banco de dados e assinaturas  
 **Configurar o distribuidor**  
  
 O distribuidor não deve ser um host para as réplicas atuais (ou planejadas) do grupo de disponibilidade do qual o banco de dados de publicação é (ou se tornará) membro.  
  
1.  Configurar a distribuição no distribuidor. Se estiverem sendo usados procedimentos armazenados para a configuração, execute `sp_adddistributor`. Use o parâmetro *@password* para identificar a senha que será usada quando um publicador remoto se conectar ao distribuidor. A senha também será necessária em cada publicador remoto quando o distribuidor remoto for instalado.  
  
    ```  
    USE master;  
    GO  
    EXEC sys.sp_adddistributor  
        @distributor = 'MyDistributor',  
        @password = '**Strong password for distributor**';  
    ```  
  
2.  Criar o banco de dados de distribuição no distribuidor. Se estiverem sendo usados procedimentos armazenados para a configuração, execute `sp_adddistributiondb`.  
  
    ```  
    USE master;  
    GO  
    EXEC sys.sp_adddistributiondb  
        @database = 'distribution',  
        @security_mode = 1;  
    ```  
  
3.  Configurar o publicador remoto. Se estiverem sendo usados procedimentos armazenados para configurar o distribuidor, execute `sp_adddistpublisher`. O parâmetro *@security_mode* é usado para determinar como o procedimento armazenado de validação de publicador, que é executado dos agentes de replicação, se conecta à réplica primária atual. Se a autenticação do Windows definida como 1 for usada na conexão à primária atual. Se estiver definida como 0, a autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] será usada com os valores *@login* e *@password* especificados. O logon e a senha especificada devem ser válidos em cada réplica secundária para o procedimento armazenado de validação se conectar com êxito a essa réplica.  
  
    > [!NOTE]  
    >  Se qualquer agente de replicação modificado for executado em um computador que não seja o distribuidor, o uso da autenticação do Windows para a conexão à réplica primária exigirá a configuração da autenticação Kerberos para a comunicação entre os computadores host da réplica. O uso de um logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para a conexão à réplica primária atual não requer a autenticação Kerberos.  
  
    ```  
    USE master;  
    GO  
    EXEC sys.sp_adddistpublisher  
        @publisher = 'AGPrimaryReplicaHost',  
        @distribution_db = 'distribution',  
        @working_directory = '\\MyReplShare\WorkingDir',  
        @login = 'MyPubLogin',  
        @password = '**Strong password for publisher**';  
    ```  
  
 Para obter mais informações, consulte [sp_adddistpublisher &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql).  
  
 **Configurar o publicador no publicador original**  
  
1.  Configurar um distribuidor remoto. Se procedimentos armazenados estiverem sendo usados para configurar o publicador, execute `sp_adddistributor`. Especifique o mesmo valor para *@password* que o usado quando `sp_adddistrbutor` foi executado no distribuidor para configurar a distribuição.  
  
    ```  
    exec sys.sp_adddistributor  
        @distributor = 'MyDistributor',  
        @password = 'MyDistPass'  
    ```  
  
2.  Habilitar o banco de dados para replicação. Se procedimentos armazenados estiverem sendo usados para configurar o publicador, execute `sp_replicationdboption`. Se as replicações transacional e de mesclagem forem configurada para o banco de dados, cada uma deverá ser habilitada.  
  
    ```  
    USE master;  
    GO  
    EXEC sys.sp_replicationdboption  
        @dbname = 'MyDBName',  
        @optname = 'publish',  
        @value = 'true';  
  
    EXEC sys.sp_replicationdboption  
        @dbname = 'MyDBName',  
        @optname = 'merge publish',  
        @value = 'true';  
    ```  
  
3.  Criar publicações, artigos e assinaturas da replicação. Para obter mais informações sobre como configurar a replicação consulte os objetos Publishing Data e Database.  
  
##  <a name="step2"></a> 2. Configurar o grupo de disponibilidade AlwaysOn  
 Na réplica primária pretendida, crie o grupo de disponibilidade com o banco de dados publicado (ou a ser publicado) como um banco de dados membro. Se estiver usando o Assistente de Grupo de Disponibilidade, você poderá permitir que o assistente sincronize os bancos de dados de réplica secundária inicialmente ou poderá executar a inicialização manualmente usando backup e restauração.  
  
 Crie um ouvinte de DNS para o grupo de disponibilidade que será usado pelos agentes de replicação para conectar à replicação primária atual. O nome de ouvinte que é especificado será usado como o destino de redirecionamento para o par publicador original/banco de dados publicado. Por exemplo, se você estiver usando o DDL para configurar o grupo de disponibilidade, o seguinte exemplo de código poderá ser usado para especificar um ouvinte de grupo de disponibilidade para um grupo de disponibilidade existente chamado `MyAG`:  
  
```  
ALTER AVAILABILITY GROUP 'MyAG'   
    ADD LISTENER 'MyAGListenerName' (WITH IP (('10.120.19.155', '255.255.254.0')));  
```  
  
 Para obter mais informações, consulte [Criação e configuração de Grupos de Disponibilidade &#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md).  
  
##  <a name="step3"></a> 3. Verifique se todos os hosts de réplica secundária estão configurados para replicação.  
 Em cada host de réplica secundária, verifique se o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] foi configurado para oferecer suporte à replicação. A seguinte consulta pode ser executada em cada host de réplica secundária para determinar se a replicação é instalada:  
  
```  
USE master;  
GO  
DECLARE @installed int;  
EXEC @installed = sys.sp_MS_replication_installed;  
SELECT @installed;  
```  
  
 Se *@installed* for 0, a replicação deverá ser adicionada à instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
##  <a name="step4"></a> 4. Configurar os hosts de réplica secundária como publicadores de replicação  
 Uma réplica secundária não pode agir como um publicador de replicação ou republicador, mas a replicação deve ser configurada de forma que a secundária possa assumir o comando depois de um failover. No distribuidor, configure a distribuição para cada host de réplica secundária. Especifique o mesmo banco de dados de distribuição e diretório de trabalho que foram especificados quando o publicador original foi adicionado ao distribuidor. Se você estiver usando procedimentos armazenados para configurar a distribuição, use `sp_adddistpublisher` para associar os publicadores remotos ao distribuidor. Se *@login* e *@password* para o publicador original, especifique os mesmos valores para cada um quando adicionar os hosts de réplica secundária como publicadores.  
  
```  
EXEC sys.sp_adddistpublisher  
    @publisher = 'AGSecondaryReplicaHost',  
    @distribution_db = 'distribution',  
    @working_directory = '\\MyReplShare\WorkingDir',  
    @login = 'MyPubLogin',  
    @password = '**Strong password for publisher**';  
```  
  
 Em cada host de réplica secundária, configure a distribuição. Identifique o distribuidor do publicador original como o distribuidor remoto. Use a mesma senha que o usado quando `sp_adddistributor` foi executado originalmente no distribuidor. Se procedimentos armazenados estiverem sendo usados para configurar a distribuição, o *@password* parâmetro do `sp_adddistributor` é usado para especificar a senha.  
  
```  
EXEC sp_adddistributor   
    @distributor = 'MyDistributor',  
    @password = '**Strong password for distributor**';  
```  
  
 Em cada host de réplica secundária, verifique se os assinantes push das publicações de banco de dados aparecem como servidores vinculados. Se procedimentos armazenados estiverem sendo usados para configurar os publicadores remotos, use `sp_addlinkedserver` para adicionar os assinantes (caso ainda não estejam presentes) como servidores vinculados aos Publicadores.  
  
```  
EXEC sys.sp_addlinkedserver   
    @server = 'MySubscriber';  
```  
  
##  <a name="step5"></a> 5. Redirecionar o publicador original para o nome do ouvinte do AG  
 No distribuidor, no banco de dados de distribuição, execute o procedimento armazenado `sp_redirect_publisher` para associar o publicador original e o banco de dados publicado com o nome do ouvinte de grupo de disponibilidade do grupo de disponibilidade.  
  
```  
USE distribution;  
GO  
EXEC sys.sp_redirect_publisher   
@original_publisher = 'MyPublisher',  
    @publisher_db = 'MyPublishedDB',  
    @redirected_publisher = 'MyAGListenerName';  
```  
  
##  <a name="step6"></a> 6. Executar o procedimento armazenado de validação de replicação para verificar a configuração  
 No distribuidor, no banco de dados de distribuição, execute o `sp_validate_replica_hosts_as_publishers` de procedimento armazenado para verificar se todos os hosts de réplica estão configurados para servir como publicadores para o banco de dados publicado.  
  
```  
USE distribution;  
GO  
DECLARE @redirected_publisher sysname;  
EXEC sys.sp_validate_replica_hosts_as_publishers  
    @original_publisher = 'MyPublisher',  
    @publisher_db = 'MyPublishedDB',  
    @redirected_publisher = @redirected_publisher output;  
```  
  
 O `sp_validate_replica_hosts_as_publishers` de procedimento armazenado deve ser executado de um logon com autorização suficiente em cada host de réplica de grupo de disponibilidade para consultar informações sobre o grupo de disponibilidade. Ao contrário de `sp_validate_redirected_publisher`, ele usa as credenciais do chamador e não usa o logon retido em msdistpublishers para se conectar a réplicas de grupo de disponibilidade.  
  
> [!NOTE]  
>  `sp_validate_replica_hosts_as_publishers` falhará com o seguinte erro ao validar hosts de réplica secundária que não permitir o acesso de leitura ou exigirem a especificação da intenção de leitura.  
>   
>  Mensagem 21899, Nível 11, Estado 1, Procedimento `sp_hadr_verify_subscribers_at_publisher`, Linha 109  
>   
>  A consulta ao publicador redirecionado 'MyReplicaHostName' para determinar se havia entradas de sysserver para os assinantes do publicador original 'MyOriginalPublisher' falhou com erro '976', mensagem de erro 'Erro 976, Nível 14, Estado 1, Mensagem: O banco de dados de destino, 'MyPublishedDB', está participando de um grupo de disponibilidade e no momento não está acessível para consultas. Qualquer movimento de dados é suspenso ou a réplica de disponibilidade não é habilitada para acesso de leitura. Para permitir o acesso somente leitura a esse banco de dados e a outros no grupo de disponibilidade, habilite o acesso de leitura para uma ou mais réplicas de disponibilidade secundárias no grupo.  Para obter mais informações, consulte o `ALTER AVAILABILITY GROUP` instrução no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Manuais Online.'.  
>   
>  Foram encontrados um ou mais erros de validação de publicador para o host de réplica 'MyReplicaHostName'.  
  
 Esse comportamento é esperado. Você deve verificar a presença das entradas de servidor de assinante nesses hosts de réplica secundária, consultando as entradas de sysserver diretamente no host.  
  
##  <a name="step7"></a> 7. Adicionar o publicador original ao Replication Monitor  
 Em cada réplica de grupo de disponibilidade, adicione o publicador original ao Replication Monitor.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Replicação**  
  
-   [Mantendo um banco de dados de publicação AlwaysOn &#40;SQL Server&#41;](maintaining-an-always-on-publication-database-sql-server.md)  
  
-   [A replicação, controle de alterações, Change Data Capture e grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](replicate-track-change-data-capture-always-on-availability.md)  
  
-   [Administração &#40;Replicação&#41;](../../../relational-databases/replication/administration/administration-replication.md)  
  
 **Para criar e configurar um grupo de disponibilidade**  
  
-   [Usar o Assistente de Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usar a caixa de diálogo Novo Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Criar um grupo de disponibilidade &#40;Transact-SQL&#41;](create-an-availability-group-transact-sql.md)  
  
-   [Criar um grupo de disponibilidade &#40;SQL Server PowerShell&#41;](../../../powershell/sql-server-powershell.md)  
  
-   [Especificar a URL do ponto de extremidade ao adicionar ou modificar uma réplica de disponibilidade &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
-   [Criar um ponto de extremidade de espelhamento para grupos de disponibilidade AlwaysOn do banco de dados &#40;SQL Server PowerShell&#41;](database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Unir uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Preparar um banco de dados secundário manualmente para um grupo de disponibilidade &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [Unir um banco de dados secundário a um grupo de disponibilidade &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
## <a name="see-also"></a>Consulte também  
 [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Grupos de disponibilidade do AlwaysOn: Interoperabilidade (SQL Server)](always-on-availability-groups-interoperability-sql-server.md)   
 [Replicação do SQL Server](../../../relational-databases/replication/sql-server-replication.md)  
  
  
