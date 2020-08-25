---
title: Criar e configurar um grupo de disponibilidade para SQL Server em Linux
description: Este tutorial mostra como criar e configurar grupos de disponibilidade para o SQL Server em Linux e como criar certificados e pontos de extremidade de grupos de disponibilidade.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 06/28/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: c3b1bf11bfbc91fa2226bfc925e80288aaf9281d
ms.sourcegitcommit: 3ea082c778f6771b17d90fb597680ed334d3e0ec
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/11/2020
ms.locfileid: "88088949"
---
# <a name="create-and-configure-an-availability-group-for-sql-server-on-linux"></a>Criar e configurar um grupo de disponibilidade para SQL Server em Linux

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

Este tutorial aborda como criar e configurar um AG (grupo de disponibilidade) para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] no Linux. Ao contrário de [!INCLUDE[sssql15-md](../includes/sssql15-md.md)] e anteriores no Windows, você pode habilitar AGs com ou sem criar o cluster subjacente do Pacemaker primeiro. A integração com o cluster, se necessário, não é feita até mais tarde.

O tutorial inclui as seguintes tarefas:
 
> [!div class="checklist"]
> * Habilitar grupos de disponibilidade.
> * Criar pontos de extremidade do grupo de disponibilidade e certificados.
> * Use [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] (SSMS) ou Transact-SQL para criar um grupo de disponibilidade.
> * Crie o logon [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] e as permissões para o Pacemaker.
> * Criar recursos de grupo de disponibilidade em um cluster do Pacemaker (tipo externo somente).

## <a name="prerequisite"></a>Pré-requisito
- Implante o cluster de alta disponibilidade do Pacemaker conforme descrito em [Implantar um cluster do Pacemaker para SQL Server em Linux](sql-server-linux-deploy-pacemaker-cluster.md).


## <a name="enable-the-availability-groups-feature"></a>Habilitar o recurso grupos de disponibilidade

Ao contrário do Windows, você não pode usar o PowerShell nem o Configuration Manager [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] para habilitar o recurso de AG (grupos de disponibilidade). No Linux, você deve usar o `mssql-conf` para habilitar o recurso. Há duas maneiras de habilitar o recurso de grupos de disponibilidade: usar o utilitário `mssql-conf` ou editar o arquivo `mssql.conf` manualmente.

> [!IMPORTANT]
> O recurso AG deve ser habilitado para réplicas somente de configuração, mesmo em [!INCLUDE[ssexpress-md](../includes/ssexpress-md.md)].

### <a name="use-the-mssql-conf-utility"></a>Usar o utilitário mssql-conf

Em um prompt, emita o seguinte:

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled 1
```

### <a name="edit-the-mssqlconf-file"></a>Editar o arquivo mssql.conf

Você também pode modificar o arquivo `mssql.conf`, localizado sob a pasta `/var/opt/mssql`, para adicionar as seguintes linhas:

```
[hadr]

hadr.hadrenabled = 1
```

### <a name="restart-ssnoversion-md"></a>Reinicie o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
Depois de habilitar os grupos de disponibilidade, como no Windows, você deve reiniciar o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Isso pode ser feito pelo seguinte:

```bash
sudo systemctl restart mssql-server
```

## <a name="create-the-availability-group-endpoints-and-certificates"></a>Criar os pontos de extremidade do grupo de disponibilidade e certificados

Um grupo de disponibilidade usa pontos de extremidade TCP para comunicação. No Linux, os pontos de extremidade para um AG só terão suporte se os certificados forem usados para autenticação. Isso significa que o certificado de uma instância deve ser restaurado em todas as outras instâncias que serão réplicas que participam do mesmo AG. O processo de certificado é necessário até mesmo para uma réplica somente de configuração. 

A criação de pontos de extremidade e a restauração de certificados só podem ser feitas por meio do Transact-SQL. Você também pode usar certificados não gerados por [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Você também precisará de um processo para gerenciar e substituir todos os certificados que expiram.

> [!IMPORTANT]
> Se planejar usar o assistente [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] para criar o AG, ainda precisará criar e restaurar os certificados usando o Transact-SQL no Linux.

Para obter a sintaxe completa das opções disponíveis para os vários comandos (como segurança adicional), confira:

-   [BACKUP CERTIFICATE](../t-sql/statements/backup-certificate-transact-sql.md)
-   [CREATE CERTIFICATE](../t-sql/statements/create-certificate-transact-sql.md)
-   [CREATE ENDPOINT](../t-sql/statements/create-endpoint-transact-sql.md)

> [!NOTE]
> Embora você vá criar um grupo de disponibilidade, o tipo de ponto de extremidade usa *FOR DATABASE_MIRRORING*, pois alguns aspectos subjacentes foram compartilhados com esse recurso agora preterido.

Este exemplo criará certificados para uma configuração de três nós. Os nomes das instância são LinAGN1, LinAGN2 e LinAGN3.

1.  Execute o seguinte em LinAGN1 para criar a chave mestra, o certificado e o ponto de extremidade, bem como fazer backup do certificado. Para este exemplo, a porta TCP típica 5022 é usada para o ponto de extremidade.
    
    ```SQL
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<StrongPassword>';
    
    GO
    
    CREATE CERTIFICATE LinAGN1_Cert
    WITH SUBJECT = 'LinAGN1 AG Certificate';
    
    GO
    
    BACKUP CERTIFICATE LinAGN1_Cert
    TO FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE ENDPOINT AGEP
    STATE = STARTED
    AS TCP (
        LISTENER_PORT = 5022,
        LISTENER_IP = ALL)
    FOR DATABASE_MIRRORING (
        AUTHENTICATION = CERTIFICATE LinAGN1_Cert,
        ROLE = ALL);
    
    GO
    ```
    
2.  Faça o mesmo em LinAGN2:
    
    ```SQL
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<StrongPassword>';
    
    GO
    
    CREATE CERTIFICATE LinAGN2_Cert
    WITH SUBJECT = 'LinAGN2 AG Certificate';
    
    GO
    
    BACKUP CERTIFICATE LinAGN2_Cert
    TO FILE = '/var/opt/mssql/data/LinAGN2_Cert.cer';
    
    GO
    
    CREATE ENDPOINT AGEP
    STATE = STARTED
    AS TCP (
        LISTENER_PORT = 5022,
        LISTENER_IP = ALL)
    FOR DATABASE_MIRRORING (
        AUTHENTICATION = CERTIFICATE LinAGN2_Cert,
        ROLE = ALL);
    
    GO
    ```
    
3.  Por fim, execute a mesma sequência em LinAGN3:
    
    ```SQL
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<StrongPassword>';
    
    GO
    
    CREATE CERTIFICATE LinAGN3_Cert
    WITH SUBJECT = 'LinAGN3 AG Certificate';
    
    GO
    
    BACKUP CERTIFICATE LinAGN3_Cert
    TO FILE = '/var/opt/mssql/data/LinAGN3_Cert.cer';
    
    GO
    
    CREATE ENDPOINT AGEP
    STATE = STARTED
    AS TCP (
        LISTENER_PORT = 5022,
        LISTENER_IP = ALL)
    FOR DATABASE_MIRRORING (
        AUTHENTICATION = CERTIFICATE LinAGN3_Cert,
        ROLE = ALL);
    
    GO
    ```
    
4.  Usando `scp` o ou outro utilitário, copie os backups do certificado para cada nó que fará parte do AG.
    
    Para este exemplo:
    
    - Copie LinAGN1_Cert.cer para LinAGN2 e LinAGN3
    - Copie LinAGN2_Cert.cer para LinAGN1 e LinAGN3.
    - Copie LinAGN3_Cert.cer para LinAGN1 e LinAGN2.
    
5.  Altere a propriedade e o grupo associado aos arquivos de certificado copiados para o `mssql`.
    
    ```bash
    sudo chown mssql:mssql <CertFileName>
    ```
    
6.  Crie os logons e os usuário em nível de instância associados a LinAGN2 e LinAGN3 no LinAGN1.
    
    ```SQL
    CREATE LOGIN LinAGN2_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN2_User FOR LOGIN LinAGN2_Login;
    
    GO
    
    CREATE LOGIN LinAGN3_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN3_User FOR LOGIN LinAGN3_Login;
    
    GO
    ```
    
7.  Restaure LinAGN2_Cert e LinAGN3_Cert em LinAGN1. Ter os certificados de outras réplicas é um aspecto importante da comunicação e da segurança do AG.
    
    ```SQL
    CREATE CERTIFICATE LinAGN2_Cert
    AUTHORIZATION LinAGN2_User
    FROM FILE = '/var/opt/mssql/data/LinAGN2_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN3_Cert
    AUTHORIZATION LinAGN3_User
    FROM FILE = '/var/opt/mssql/data/LinAGN3_Cert.cer';
    
    GO
    
8.  Grant the logins associated with LinAG2 and LinAGN3 permission to connect to the endpoint on LinAGN1.
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN2_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN3_Login;
    
    GO
    ```
    
9.  Crie os logons e os usuário em nível de instância associados a LinAGN1 e LinAGN3 no LinAGN2.
    
    ```SQL
    CREATE LOGIN LinAGN1_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN1_User FOR LOGIN LinAGN1_Login;
    
    GO
    
    CREATE LOGIN LinAGN3_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN3_User FOR LOGIN LinAGN3_Login;
    
    GO
    ```
    
10. Restaure LinAGN1_Cert e LinAGN3_Cert em LinAGN2.
    
    ```SQL
    CREATE CERTIFICATE LinAGN1_Cert
    AUTHORIZATION LinAGN1_User
    FROM FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN3_Cert
    AUTHORIZATION LinAGN3_User
    FROM FILE = '/var/opt/mssql/data/LinAGN3_Cert.cer';
    
    GO
    ```
    
11. Conceda aos logons associados a permissão LinAG1 e LinAGN3 para conectarem-se ao ponto de extremidade em LinAGN2.
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN1_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN3_Login;
    
    GO
    ```
    
12. Crie os logons e os usuário em nível de instância associados a LinAGN1 e LinAGN2 no LinAGN3.
    
    ```SQL
    CREATE LOGIN LinAGN1_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN1_User FOR LOGIN LinAGN1_Login;
    
    GO
    
    CREATE LOGIN LinAGN2_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN2_User FOR LOGIN LinAGN2_Login;
    
    GO
    ```
    
13. Restaure LinAGN1_Cert e LinAGN2_Cert em LinAGN3. 
    
    ```SQL
    CREATE CERTIFICATE LinAGN1_Cert
    AUTHORIZATION LinAGN1_User
    FROM FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN2_Cert
    AUTHORIZATION LinAGN2_User
    FROM FILE = '/var/opt/mssql/data/LinAGN2_Cert.cer';
    
    GO
    ```
    
14. Conceda aos logons associados a permissão LinAG1 e LinAGN2 para conectarem-se ao ponto de extremidade em LinAGN3.
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN1_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN2_Login;
    
    GO
    ```

## <a name="create-the-availability-group"></a>Crie o grupo de disponibilidade

Esta seção aborda como usar o [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] SSMS (ou o Transact-SQL) para criar o grupo de disponibilidade para o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)].

### <a name="use-ssmanstudiofull-md"></a>Use [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)].

Esta seção mostra como criar um AG com um tipo de cluster Externo usando o SSMS com o Assistente de Novo Grupo de Disponibilidade.

1.  No SSMS, expanda **Alta Disponibilidade Always On**, clique com o botão direito do mouse em **Grupos de Disponibilidade** e selecione **Assistente de Novo Grupo de Disponibilidade**.

2.  Na caixa de diálogo Introdução, clique em **Avançar**.

3.  Na caixa de diálogo Especificar Opções do Grupo de Disponibilidade, insira um nome para o grupo de disponibilidade e selecione um tipo de cluster EXTERNO ou NENHUM no menu suspenso. Externo deve ser usado quando o Pacemaker for ser implantado. Nenhum é para cenários especializados, como expansão de leitura. Selecionar a opção de detecção de integridade no nível do banco de dados é opcional. Para obter mais informações sobre essa opção, confira [Opção de failover de detecção de integridade no nível do banco de dados do grupo de disponibilidade](../database-engine/availability-groups/windows/sql-server-always-on-database-health-detection-failover-option.md). Clique em **Próximo**.

    ![Criar grupo de disponibilidade 03](./media/sql-server-linux-create-availability-group/image3.png)

4.  Na caixa de diálogo Selecionar Bancos de Dados, selecione os bancos de dados que participarão do AG. Cada banco de dados deve ter um backup completo antes que possa ser adicionado a um AG. Clique em **Próximo**.

5.  Na caixa de diálogo Especificar Réplicas, clique em **Adicionar Réplica**.

6.  Na caixa de diálogo Conectar-se ao Servidor, digite o nome da instância do Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] que será a réplica secundária e as credenciais para conectar-se. Clique em **Conectar**.

7.  Repita as duas etapas anteriores para a instância que conterá uma réplica somente de configuração ou outra réplica secundária.

8.  Agora, todas as três instâncias devem ser listadas na caixa de diálogo Especificar Réplicas. Se estiver usando um tipo de cluster Externo, para a réplica secundária que será verdadeiramente secundária, verifique se o Modo de Disponibilidade corresponde ao da réplica primária e o modo de failover está definido como Externo. Para a réplica somente de configuração, selecione um modo de disponibilidade somente de Configuração.

    O exemplo a seguir mostra um AG com duas réplicas, um tipo de cluster Externo e uma réplica somente de configuração.

    ![Criar grupo de disponibilidade 04](./media/sql-server-linux-create-availability-group/image4.png)

    O exemplo a seguir mostra um AG com duas réplicas, um tipo de cluster Nenhum e uma réplica somente de configuração.

    ![Criar grupo de disponibilidade 05](./media/sql-server-linux-create-availability-group/image5.png)

9.  Se você quiser alterar as preferências de backup, clique na guia Preferências de Backup. Para obter mais informações sobre as preferências de backup com o AGs, confira [Configurar o backup em réplicas de disponibilidade](../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md).

10. Se estiver usando secundários legíveis ou criando um AG com um tipo de cluster de Nenhum para escala de leitura, você poderá criar um ouvinte selecionando a guia Ouvinte. Um ouvinte também pode ser adicionado posteriormente. Para criar um ouvinte, escolha a opção **Criar um ouvinte de grupo de disponibilidade** e insira um nome, uma porta TCP/IP e se deseja usar um endereço IP DHCP atribuído automaticamente ou estático. Lembre-se de que, para um AG com um tipo de cluster de Nenhum, o IP deve ser estático e definido como o endereço IP do primário.

    ![Criar grupo de disponibilidade 06](./media/sql-server-linux-create-availability-group/image6.png)

11. Se um ouvinte for criado para cenários legíveis, o SSMS 17.3 ou posterior permitirá a criação do roteamento somente leitura no assistente. Ele também pode ser adicionado posteriormente por meio de SSMS ou Transact-SQL. Para adicionar o roteamento somente leitura agora:

    a.  Selecione a guia Roteamento Somente Leitura.

    b.  Insira as URLs para as réplicas somente leitura. Essas URLs são semelhantes aos pontos de extremidade, exceto pelo fato de usarem a porta da instância, e não o ponto de extremidade.

    c.  Selecione cada URL e, na parte inferior, selecione as réplicas legíveis. Para seleção múltipla, mantenha pressionada a tecla SHIFT ou clique e arraste.

12. Clique em **Próximo**.

13. Escolha como as réplicas secundárias serão inicializadas. O padrão é usar a [propagação automática](../database-engine/availability-groups/windows/automatically-initialize-always-on-availability-group.md), que requer o mesmo caminho em todos os servidores que participam do AG. Você também pode fazer com que o assistente faça a ação de backup, cópia e restauração (a segunda opção); fazer com que ele ingresse se você tiver feito a ação de backup, cópia e restauração manualmente do banco de dados nas réplicas (terceira opção); ou adicionar o banco de dados mais tarde (última opção). Assim como ocorre com os certificados, se você estiver fazendo backups e copiando-os manualmente, as permissões nos arquivos de backup precisarão ser definidas em outras réplicas. Clique em **Próximo**.

14. Na caixa de diálogo Validação, se tudo não voltar como Sucesso, investigue. Alguns avisos são aceitáveis e não fatais, como se você não criar um ouvinte. Clique em **Próximo**.

15. Na caixa de diálogo Resumo, clique em **Concluir**. O processo para criar o AG será iniciado agora.

16. Quando a criação do AG for concluída, clique em **Fechar** nos Resultados. Agora você pode ver o AG nas réplicas nas exibições de gerenciamento dinâmico, bem como na pasta Alta Disponibilidade Always On no SSMS.

### <a name="use-transact-sql"></a>Usar o Transact-SQL

Esta seção mostra exemplos de como criar um AG usando o Transact-SQL. O ouvinte e o roteamento somente leitura podem ser configurados após a criação do AG. O AG pode ser modificado com `ALTER AVAILABILITY GROUP`, mas a alteração do tipo de cluster não pode ser feita no [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. Se você não deseja criar um AG com um tipo de cluster Externo, deve excluí-lo e recriá-lo com um tipo de cluster Nenhum. Mais informações e outras opções podem ser encontradas nos seguintes links:

-   [CREATE AVAILABILITY GROUP (Transact-SQL)](../t-sql/statements/create-availability-group-transact-sql.md)
-   [ALTER AVAILABILITY GROUP (Transact-SQL)](../t-sql/statements/alter-availability-group-transact-sql.md)
-   [Configurar o roteamento somente leitura para um grupo de disponibilidade (SQL Server)](../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)
-   [Criar ou configurar um ouvinte de grupo de disponibilidade (SQL Server)](../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)

#### <a name="example-one---two-replicas-with-a-configuration-only-replica-external-cluster-type"></a>Exemplo Um: duas réplicas com uma réplica somente de configuração (tipo de cluster Externo)

Esse exemplo mostra como criar um AG de duas réplicas que usa uma réplica somente de configuração.

1.  Execute no nó que será a réplica primária que contém a cópia de leitura/gravação completa dos bancos de dados. Este exemplo usa propagação automática.

    ```SQL
    CREATE AVAILABILITY GROUP [<AGName>]
    WITH (CLUSTER_TYPE = EXTERNAL)
    FOR DATABASE <DBName>
    REPLICA ON N'LinAGN1' WITH (
       ENDPOINT_URL = N' TCP://LinAGN1.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT),
    N'LinAGN2' WITH (
       ENDPOINT_URL = N'TCP://LinAGN2.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
       SEEDING_MODE = AUTOMATIC),
    N'LinAGN3' WITH (
       ENDPOINT_URL = N'TCP://LinAGN3.FullyQualified.Name:5022',
       AVAILABILITY_MODE = CONFIGURATION_ONLY);
       
    GO
    ```
    
2.  Em uma janela de consulta conectada à outra réplica, execute o seguinte para unir a réplica ao AG e iniciar o processo de propagação da réplica primária para a secundária.
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```
    
3. Em uma janela de consulta conectada à réplica somente de configuração, ingresse-a no AG.
    
   ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
   ```

#### <a name="example-two---three-replicas-with-read-only-routing-external-cluster-type"></a>Exemplo Dois: três réplicas com roteamento somente leitura (tipo de cluster Externo)

Este exemplo mostra três réplicas completas e como o roteamento somente leitura pode ser configurado como parte da criação inicial do AG.

1.  Execute no nó que será a réplica primária que contém a cópia de leitura/gravação completa dos bancos de dados. Este exemplo usa propagação automática.

    ```SQL
    CREATE AVAILABILITY GROUP [<AGName>]
    WITH (CLUSTER_TYPE = EXTERNAL)
    FOR DATABASE <DBName>
    REPLICA ON N'LinAGN1'
    WITH (
       ENDPOINT_URL = N'TCP://LinAGN1.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN2.FullyQualified.Name', 'LinAGN3.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL = N'TCP://LinAGN1.FullyQualified.Name:1433')),
    N'LinAGN2' WITH (
       ENDPOINT_URL = N'TCP://LinAGN2.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       SEEDING_MODE = AUTOMATIC,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN1.FullyQualified.Name', 'LinAGN3.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL = N'TCP://LinAGN2.FullyQualified.Name:1433')),
    N'LinAGN3' WITH (
       ENDPOINT_URL = N'TCP://LinAGN3.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       SEEDING_MODE = AUTOMATIC,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN1.FullyQualified.Name', 'LinAGN2.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL = N'TCP://LinAGN3.FullyQualified.Name:1433'))
    LISTENER '<ListenerName>' (WITH IP = ('<IPAddress>', '<SubnetMask>'), Port = 1433);
    
    GO
    ```
    
    Alguns pontos a serem observados sobre essa configuração:
    
    - *AGName* é o nome do grupo de disponibilidade.
    - *DBName* é o nome do banco de dados que será usado com o grupo de disponibilidade. Também pode ser uma lista de nomes separados por vírgulas.
    - *ListenerName* é um nome diferente de qualquer um dos servidores/nós subjacentes. Ele será registrado em DNS junto com o *IPAddress*.
    - *IPAddress* é um endereço IP associado a *ListenerName*. Também é exclusivo e não é igual ao de nenhum dos servidores/nós. Aplicativos e usuários finais usarão *ListenerName* ou *IPAddress* para conectarem-se ao AG.
    - *SubnetMask* é a máscara de sub-rede do *IPAddress*, por exemplo, 255.255.255.0.

2.  Em uma janela de consulta conectada à outra réplica, execute o seguinte para unir a réplica ao AG e iniciar o processo de propagação da réplica primária para a secundária.
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```
    
3.  Repita a Etapa 2 para a terceira réplica.

#### <a name="example-three---two-replicas-with-read-only-routing-none-cluster-type"></a>Exemplo Três: duas réplicas com roteamento somente leitura (tipo de cluster de Nenhum)

Este exemplo mostra a criação de uma configuração de duas réplicas usando um tipo de cluster Nenhum. Ele é usado para o cenário de escala de leitura em que nenhum failover é esperado. Isso cria o ouvinte que é, na verdade, a réplica primária, bem como o roteamento somente leitura, usando a funcionalidade round robin.

1.  Execute no nó que será a réplica primária que contém a cópia de leitura/gravação completa dos bancos de dados. Este exemplo usa propagação automática.

    ```SQL
    CREATE AVAILABILITY GROUP [<AGName>]
    WITH (CLUSTER_TYPE = NONE)
    FOR DATABASE <DBName>
    REPLICA ON N'LinAGN1'
    WITH (
       ENDPOINT_URL = N'TCP://LinAGN1.FullyQualified.Name: <PortOfEndpoint>',
       FAILOVER_MODE = MANUAL,
       AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN1.FullyQualified.Name'.'LinAGN2.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL = N'TCP://LinAGN1.FullyQualified.Name:<PortOfInstance>'));
    N'LinAGN2' WITH (
       ENDPOINT_URL = N'TCP://LinAGN2.FullyQualified.Name:<PortOfEndpoint>',
       FAILOVER_MODE = MANUAL,
       SEEDING_MODE = AUTOMATIC,
       AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN1.FullyQualified.Name', 'LinAGN2.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL =N'TCP://LinAGN2.FullyQualified.Name:<PortOfInstance>'));
    LISTENER '<ListenerName>' (WITH IP = ('<PrimaryReplicaIPAddress>', '<SubnetMask>'), Port = <PortOfListener>);
    
    GO
    ```
    
    Where
    - *AGName* é o nome do grupo de disponibilidade.
    - *DBName* é o nome do banco de dados que será usado com o grupo de disponibilidade. Também pode ser uma lista de nomes separados por vírgulas.
    - *PortOfEndpoint* é o número da porta usada pelo ponto de extremidade criado.
    - *PortOfInstance* é o número da porta usada pela instância do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)].
    - *ListenerName* é um nome diferente de qualquer uma das réplicas subjacentes, mas não será realmente usado.
    - *PrimaryReplicaIPAddress* é o endereço IP da réplica primária.
    - *SubnetMask* é a máscara de sub-rede do *IPAddress*. Por exemplo, 255.255.255.0.
    
2.  Ingresse a réplica secundária no AG e inicie a propagação automática.
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = NONE);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```

## <a name="create-the-ssnoversion-md-login-and-permissions-for-pacemaker"></a>Criar o logon [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] e as permissões para o Pacemaker

Um cluster de alta disponibilidade do Pacemaker subjacente a [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] no Linux precisa de acesso à instância do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], bem como permissões no grupo de disponibilidade em si. Essas etapas criam o logon e as permissões associadas, juntamente com um arquivo que informa ao Pacemaker como fazer logon no [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)].

1.  Em uma janela de consulta conectada à primeira réplica, execute o seguinte:

    ```SQL
    CREATE LOGIN PMLogin WITH PASSWORD ='<StrongPassword>';
    
    GO
    
    GRANT VIEW SERVER STATE TO PMLogin;
    
    GO
    
    GRANT ALTER, CONTROL, VIEW DEFINITION ON AVAILABILITY GROUP::<AGThatWasCreated> TO PMLogin;
    
    GO
    ```
    
2.  No Nó 1, insira o comando 
    ```bash
    sudo emacs /var/opt/mssql/secrets/passwd
    ```
    
    Isso abrirá o editor Emacs.
    
3.  Insira as duas linhas a seguir no editor:

    ```
    PMLogin
    <StrongPassword>
    ```
    
4.  Mantenha pressionada a tecla CTRL e, em seguida, pressione X e então C para sair e salvar o arquivo.

5.  Execute (executar) 
    ```bash
    sudo chmod 400 /var/opt/mssql/secrets/passwd
    ```
    
    para bloquear o arquivo.

6.  Repita as Etapas 1-5 nos outros servidores que funcionarão como réplicas.

## <a name="create-the-availability-group-resources-in-the-pacemaker-cluster-external-only"></a>Crie os recursos do grupo de disponibilidade em um cluster do Pacemaker (somente tipo Externo)

Depois que um grupo de disponibilidade foi criado no [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], os recursos correspondentes devem ser criados no Pacemaker quando um tipo de cluster Externo é especificado. Há dois recursos associados a um AG: o AG em si e um endereço IP. Configurar o recurso de endereço IP é opcional se você não está usando a funcionalidade do ouvinte, mas é recomendado.

O recurso AG criado é um tipo especial de recurso chamado de clone. Basicamente, o recurso AG tem cópias em cada nó e há um recurso de controle chamado mestre. O mestre está associado ao servidor que hospeda a réplica primária. Os outros recursos hospedam réplicas secundárias (regulares ou somente de configuração) e podem ser promovidos para mestre em um failover.

[!INCLUDE [bias-sensitive-term-t](../includes/bias-sensitive-term-t.md)]

1.  Crie o recurso do AG com a seguinte sintaxe:

    **RHEL (Red Hat Enterprise Linux) e Ubuntu**
    
    ```bash
    sudo pcs resource create <NameForAGResource> ocf:mssql:ag ag_name=<AGName> meta failure-timeout=30s --master meta notify=true
    ```

    >[!NOTE]
    >No RHEL 7,4, você pode encontrar um aviso com o uso de --master. Para evitar isso, use `sudo pcs resource create <NameForAGResource> ocf:mssql:ag ag_name=<AGName> meta failover-timeout=30s master notify=true`
   
    **SUSE Linux Enterprise Server (SLES)**
    
    ```bash
    primitive <NameForAGResource> \
    ocf:mssql:ag \
    params ag_name="<AGName>" \
    meta failure-timeout=60s \
    op start timeout=60s \
    op stop timeout=60s \
    op promote timeout=60s \
    op demote timeout=10s \
    op monitor timeout=60s interval=10s \
    op monitor timeout=60s interval=11s role="Master" \
    op monitor timeout=60s interval=12s role="Slave" \
    op notify timeout=60s
    ms ms-ag_cluster <NameForAGResource> \
    meta master-max="1" master-node-max="1" clone-max="3" \
    clone-node-max="1" notify="true" \
    commit
    ```
    
    em que *NameForAGResource* é o nome exclusivo fornecido a esse recurso de cluster para o AG e *AGName* é o nome do AG que foi criado.
 
2.  Crie o recurso de endereço IP para o AG que será associado à funcionalidade do ouvinte.

    **RHEL e Ubuntu**
    
    ```bash
    sudo pcs resource create <NameForIPResource> ocf:heartbeat:IPaddr2 ip=<IPAddress> cidr_netmask=<Netmask>
    ```

    **SLES**
    
    ```bash
    crm configure \
    primitive <NameForIPResource> \
       ocf:heartbeat:IPaddr2 \
       params ip=<IPAddress> \
          cidr_netmask=<Netmask>
    ```
    
    em que *NameForIPResource* é o nome exclusivo do recurso IP e *IPAddress* é o endereço IP estático atribuído ao recurso. No SLES, você também precisa fornecer a máscara de rede. Por exemplo, 255.255.255.0 teria um valor de 24 para *Netmask.*
    
3.  Para garantir que o endereço IP e o recurso do AG estejam em execução no mesmo nó, uma restrição de colocalização deve ser configurada.

    **RHEL e Ubuntu**
    
    ```bash
    sudo pcs constraint colocation add <NameForIPResource> <NameForAGResource>-master INFINITY with-rsc-role=Master
    ```

    **SLES**
    
    ```bash
    crm configure <NameForConstraint> inf: \
    <NameForIPResource> <NameForAGResource>:Master 
    commit
    ```
    
    em que *NameForIPResource* é o nome do recurso de IP, *NameForAGResource* é o nome do recurso AG e, no SLES, *NameForConstraint* é o nome para a restrição.

4.  Crie uma restrição de ordenação para garantir que o recurso AG esteja em funcionamento antes do endereço IP. Enquanto a restrição de colocalização implica uma restrição de ordenação, isso a impõe.

    **RHEL e Ubuntu**
    
    ```bash
    sudo pcs constraint order promote <NameForAGResource>-master then start <NameForIPResource>
    ```
    
    **SLES**
    
    ```bash
    crm configure \
    order <NameForConstraint> inf: <NameForAGResource>:promote <NameForIPResource>:start
    commit
    ```
    
    em que *NameForIPResource* é o nome do recurso de IP, *NameForAGResource* é o nome do recurso AG e, no SLES, *NameForConstraint* é o nome para a restrição.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu a criar e configurar um grupo de disponibilidade para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] no Linux. Você aprendeu a:
> [!div class="checklist"]
> * Habilitar grupos de disponibilidade.
> * Crie pontos de extremidade do AG e certificados.
> * Use o [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] (SSMS) ou o Transact-SQL para criar um AG.
> * Crie o logon [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] e as permissões para o Pacemaker.
> * Crie recursos do AG em um cluster do Pacemaker.

Para a maioria das tarefas de administração do AG, incluindo atualizações e failover, confira:

> [!div class="nextstepaction"]
> [Operar um grupo de HA para o SQL Server em Linux](sql-server-linux-availability-group-failover-ha.md)

