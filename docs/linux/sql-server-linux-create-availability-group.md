---
title: Criar e configurar um grupo de disponibilidade para o SQL Server no Linux | Microsoft Docs
description: Este tutorial mostra como criar e configurar grupos de disponibilidade para o SQL Server no Linux.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 06/28/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: 69b3e30c39d8b9947cf4c2f7d675920f0c2a2094
ms.sourcegitcommit: 3e5f1545e5c6c92fa32e116ee3bff1018ca946a2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37107224"
---
# <a name="create-and-configure-an-availability-group-for-sql-server-on-linux"></a>Criar e configurar um grupo de disponibilidade para o SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este tutorial aborda como criar e configurar um grupo de disponibilidade (AG) para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] no Linux. Ao contrário de [!INCLUDE[sssql15-md](../includes/sssql15-md.md)] e anteriormente no Windows, você pode habilitar grupos de disponibilidade com ou sem criar o cluster subjacente do Pacemaker pela primeira vez. Integração com o cluster, se necessário, não é feita até mais tarde.

Este tutorial inclui as seguintes tarefas:
 
> [!div class="checklist"]
> * Habilite grupos de disponibilidade.
> * Crie certificados e pontos de extremidade de grupo de disponibilidade.
> * Use [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] (SSMS) ou o Transact-SQL para criar um grupo de disponibilidade.
> * Criar o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] logon e permissões do Pacemaker.
> * Crie recursos do grupo de disponibilidade em um cluster Pacemaker (apenas tipo externo).

## <a name="prerequisite"></a>Pré-requisito
- Implantar o cluster de alta disponibilidade do Pacemaker, conforme descrito em [implantar um cluster Pacemaker para o SQL Server no Linux](sql-server-linux-deploy-pacemaker-cluster.md).


## <a name="enable-the-availability-groups-feature"></a>Habilite o recurso de grupos de disponibilidade

Ao contrário no Windows, você não pode usar o PowerShell ou [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Configuration Manager para habilitar a disponibilidade de grupos de recurso (AG). No Linux, você deve usar `mssql-conf` para habilitar o recurso. Há duas maneiras para habilitar o recurso de grupos de disponibilidade: usar o `mssql-conf` utilitário ou editar o `mssql.conf` arquivo manualmente.

> [!IMPORTANT]
> O recurso de grupo de disponibilidade deve ser habilitado para réplicas somente de configuração, mesmo em [!INCLUDE[ssexpress-md](../includes/ssexpress-md.md)].

### <a name="use-the-mssql-conf-utility"></a>Use o utilitário mssql-conf

Em um prompt, execute o seguinte:

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled 1
```

### <a name="edit-the-mssqlconf-file"></a>Edite o arquivo mssql.conf

Você também pode modificar o `mssql.conf` arquivo, localizado sob o `/var/opt/mssql` pasta, para adicionar as seguintes linhas:

```
[hadr]

hadr.hadrenabled = 1
```

### <a name="restart-includessnoversion-mdincludesssnoversion-mdmd"></a>Reiniciar [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
Depois de habilitar grupos de disponibilidade, como no Windows, você deve reiniciar [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Isso pode ser feito pelo seguinte:

```bash
sudo systemctl restart mssql-server
```

## <a name="create-the-availability-group-endpoints-and-certificates"></a>Criar os pontos de extremidade de grupo de disponibilidade e certificados

Um grupo de disponibilidade usa pontos de extremidade TCP para comunicação. No Linux, só há suporte para pontos de extremidade para um grupo de disponibilidade se forem usados certificados para autenticação. Isso significa que o certificado de uma instância deve ser restaurado em todas as outras instâncias que serão réplicas que participam no mesmo AG. O processo de certificado é necessário até mesmo para uma réplica somente de configuração. 

Criando pontos de extremidade e restaurar certificados só podem ser feitos por meio do Transact-SQL. Você pode usar não -[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]-gerado também certificados. Você também precisará de um processo para gerenciar e substituir todos os certificados que expiram.

> [!IMPORTANT]
> Se você planeja usar o [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] Assistente para criar o grupo de disponibilidade, você ainda precisará criar e restaurar os certificados usando o Transact-SQL no Linux.

Para obter a sintaxe completa sobre as opções disponíveis para os vários comandos (como segurança adicional), consulte:

-   [BACKUP CERTIFICATE](../t-sql/statements/backup-certificate-transact-sql.md)
-   [CRIAR CERTIFICADO](../t-sql/statements/create-certificate-transact-sql.md)
-   [CREATE ENDPOINT](../t-sql/statements/create-endpoint-transact-sql.md)

> [!NOTE]
> Embora você estará criando um grupo de disponibilidade, o tipo de ponto de extremidade usa *FOR DATABASE_MIRRORING*, porque alguns aspectos subjacentes uma vez foram compartilhados com esse recurso agora foi preterida.

Este exemplo criará certificados para uma configuração de três nós. Os nomes de instância são LinAGN1, LinAGN2 e LinAGN3.

1.  Execute o seguinte no LinAGN1 para criar a chave mestra, o certificado e o ponto de extremidade, bem como fazer backup do certificado. Neste exemplo, a porta TCP típica 5022 é usada para o ponto de extremidade.
    
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
    
2.  Fazer o mesmo em LinAGN2:
    
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
    
4.  Usando `scp` ou outro utilitário, copie os backups do certificado para cada nó que fará parte do AG.
    
    Para este exemplo:
    
    - Copiar LinAGN1_Cert.cer LinAGN2 e LinAGN3
    - Copie LinAGN2_Cert.cer LinAGN1 e LinAGN3.
    - Copie LinAGN3_Cert.cer LinAGN1 e LinAGN2.
    
5.  Alterar a propriedade e o grupo associado com os arquivos do certificado copiado para `mssql`.
    
    ```bash
    sudo chown mssql:mssql <CertFileName>
    ```
    
6.  Crie logons de nível de instância e usuários associados LinAGN2 e LinAGN3 em LinAGN1.
    
    ```SQL
    CREATE LOGIN LinAGN2_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN2_User FOR LOGIN LinAGN2_Login;
    
    GO
    
    CREATE LOGIN LinAGN3_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN3_User FOR LOGIN LinAGN3_Login;
    
    GO
    ```
    
7.  Restaure LinAGN2_Cert e LinAGN3_Cert em LinAGN1. Ter certificados a outras réplicas é um aspecto importante de comunicação do grupo de disponibilidade e segurança.
    
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
    
9.  Crie logons de nível de instância e usuários associados LinAGN1 e LinAGN3 em LinAGN2.
    
    ```SQL
    CREATE LOGIN LinAGN1_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN1_User FOR LOGIN LinAGN1_Login;
    
    GO
    
    CREATE LOGIN LinAGN3_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN3_User FOR LOGIN LinAGN3_Login;
    
    GO
    ```
    
10.  Restaure LinAGN1_Cert e LinAGN3_Cert em LinAGN2. 
    
    ```SQL
    CREATE CERTIFICATE LinAGN1_Cert
    AUTHORIZATION LinAGN1_User
    FROM FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN3_Cert
    AUTHORIZATION LinAGN3_User
    FROM FILE = '/var/opt/mssql/data/LinAGN3_Cert.cer';
    
    GO
    
11.  Grant the logins associated with LinAG1 and LinAGN3 permission to connect to the endpoint on LinAGN2.
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN1_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN3_Login;
    
    GO
    ```
    
12.  Crie logons de nível de instância e usuários associados LinAGN1 e LinAGN2 em LinAGN3.
    
    ```SQL
    CREATE LOGIN LinAGN1_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN1_User FOR LOGIN LinAGN1_Login;
    
    GO
    
    CREATE LOGIN LinAGN2_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN2_User FOR LOGIN LinAGN2_Login;
    
    GO
    ```
    
13.  Restaure LinAGN1_Cert e LinAGN2_Cert em LinAGN3. 
    
    ```SQL
    CREATE CERTIFICATE LinAGN1_Cert
    AUTHORIZATION LinAGN1_User
    FROM FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN2_Cert
    AUTHORIZATION LinAGN2_User
    FROM FILE = '/var/opt/mssql/data/LinAGN2_Cert.cer';
    
    GO
    
14.  Grant the logins associated with LinAG1 and LinAGN2 permission to connect to the endpoint on LinAGN3.
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN1_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN2_Login;
    
    GO
    ```

## <a name="create-the-availability-group"></a>Criar o grupo de disponibilidade

Esta seção aborda como usar [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] (SSMS) ou o Transact-SQL para criar o grupo de disponibilidade para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)].

### <a name="use-includessmanstudiofull-mdincludesssmanstudiofull-mdmd"></a>Use [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)]

Esta seção mostra como criar um grupo de disponibilidade com um tipo de cluster externo usando o SSMS com o Assistente de novo grupo de disponibilidade.

1.  No SSMS, expanda **alta disponibilidade Always On**, clique com botão direito **grupos de disponibilidade**e selecione **Assistente de novo grupo de disponibilidade**.

2.  Na caixa de diálogo Introdução, clique em **próxima**.

3.  Na caixa de diálogo especificar opções de grupo de disponibilidade, insira um nome para o grupo de disponibilidade e selecione um tipo de cluster de EXTERNAL ou NONE na lista suspensa. Externo deve ser usado quando o Pacemaker será implantado. Nenhum é para cenários especializados, como leitura de expansão. Selecionando a opção de detecção de integridade no nível do banco de dados é opcional. Para obter mais informações sobre essa opção, consulte [opção de failover de detecção de integridade no nível de banco de dados de grupo de disponibilidade](../database-engine/availability-groups/windows/sql-server-always-on-database-health-detection-failover-option.md). Clique em **Avançar**.

    ![](./media/sql-server-linux-create-availability-group/image3.png)

4.  Na caixa de diálogo Selecionar bancos de dados, selecione os bancos de dados que farão parte do grupo de disponibilidade. Cada banco de dados deve ter um backup completo antes que ele pode ser adicionado a um AG. Clique em **Avançar**.

5.  Na caixa de diálogo especificar réplicas, clique em **para adicionar réplica**.

6.  Em conectar-se a caixa de diálogo do servidor, insira o nome da instância do Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] que será a réplica secundária e as credenciais para se conectar. Clique em **Conectar**.

7.  Repita as duas etapas anteriores para a instância que contém uma réplica somente configuração ou outra réplica secundária.

8.  Todas as três instâncias devem agora estar listadas na caixa de diálogo especificar réplicas. Se usar um tipo de cluster externo, para a réplica secundária que será um verdadeiro secundário, verifique se o modo de disponibilidade corresponde da réplica primária e o modo de failover é definido como externo. Para a réplica somente de configuração, selecione um modo de disponibilidade da configuração somente.

    O exemplo a seguir mostra um grupo de disponibilidade com duas réplicas, um tipo de cluster externo e uma réplica somente de configuração.

    ![](./media/sql-server-linux-create-availability-group/image4.png)

    O exemplo a seguir mostra um grupo de disponibilidade com duas réplicas, um tipo de cluster de nenhum e uma réplica somente de configuração.

    ![](./media/sql-server-linux-create-availability-group/image5.png)

9.  Se você quiser alterar as preferências de backup, clique na guia Preferências de Backup. Para obter mais informações sobre as preferências de backup com grupos de disponibilidade, consulte [configurar o backup em réplicas de disponibilidade](../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md).

10. Se usar secundários legíveis ou criar um grupo de disponibilidade com um cluster do tipo de nenhum para escala de leitura, você pode criar um ouvinte, selecionando a guia ouvinte. Um ouvinte também pode ser adicionado posteriormente. Para criar um ouvinte, escolha a opção **criar um ouvinte de grupo de disponibilidade** e insira um nome, uma porta TCP/IP e se é necessário usar um endereço IP de DHCP estático ou atribuído automaticamente. Lembre-se de que, para um grupo de disponibilidade com um tipo de cluster nenhum, o IP deve ser estático e definido para o endereço IP do primário.

    ![](./media/sql-server-linux-create-availability-group/image6.png)

11. Se um ouvinte é criado para cenários legíveis, o SSMS 17.3 ou posterior permite a criação do roteamento somente leitura no assistente. Ele também pode ser adicionado posteriormente por meio do SSMS ou Transact-SQL. Para adicionar o roteamento somente leitura agora:

    A.  Selecione a guia roteamento somente leitura.

    B.  Insira as URLs para as réplicas somente leitura. Essas URLs são semelhantes aos pontos de extremidade, exceto que eles usam a porta da instância, não o ponto de extremidade.

    c.  Selecione cada URL e na parte inferior, selecione as réplicas legíveis. Para selecionar vários, mantenha pressionada a tecla SHIFT ou clique e arraste.

12. Clique em **Avançar**.

13. Escolha como as réplicas secundárias serão inicializadas. O padrão é usar [a propagação automática](../database-engine/availability-groups/windows/automatically-initialize-always-on-availability-group.md), que requer o mesmo caminho em todos os servidores que participam do AG. Você também pode ter o Assistente para fazer uma cópia de backup e restaurar (a segunda opção); ele tem a junção se você tiver manualmente o backup, copiou e restaurou o banco de dados nas réplicas (terceira opção); ou adicione o banco de dados mais tarde (última opção). Assim como acontece com certificados, se você estiver fazendo backups e copiá-los manualmente, as permissões nos arquivos de backup precisa ser definido nas outras réplicas. Clique em **Avançar**.

14. Na caixa de diálogo validação, se tudo o que não voltar como êxito, investigue. Alguns avisos são aceitáveis e não é fatal, por exemplo, se você não criar um ouvinte. Clique em **Avançar**.

15. Na caixa de diálogo resumida, clique em **concluir**. O processo para criar o grupo de disponibilidade agora será iniciado.

16. Quando a criação do grupo de disponibilidade estiver concluída, clique em **fechar** nos resultados. Agora você pode ver o grupo de disponibilidade nas réplicas nas exibições de gerenciamento dinâmico, bem como sob a pasta de alta disponibilidade AlwaysOn no SSMS.

### <a name="use-transact-sql"></a>Usar o Transact-SQL

Esta seção mostra exemplos de criação de um grupo de disponibilidade usando o Transact-SQL. O ouvinte e o roteamento somente leitura podem ser configurados depois que o grupo de disponibilidade é criado. O grupo de disponibilidade em si pode ser modificado com `ALTER AVAILABILITY GROUP`, mas a alteração do tipo de cluster não pode ser feita [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. Se você não pretendia criar um grupo de disponibilidade com um tipo de cluster externo, você deve excluí-la e recriá-la com um tipo de cluster nenhum. Obter mais informações e outras opções podem ser encontradas nos seguintes links:

-   [CREATE AVAILABILITY GROUP (Transact-SQL)](../t-sql/statements/create-availability-group-transact-sql.md)
-   [ALTER AVAILABILITY GROUP (Transact-SQL)](../t-sql/statements/alter-availability-group-transact-sql.md)
-   [Configurar o roteamento somente leitura para um grupo de disponibilidade (SQL Server)](../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)
-   [Criar ou configurar um ouvinte de grupo de disponibilidade (SQL Server)](../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)

#### <a name="example-one--two-replicas-with-a-configuration-only-replica-external-cluster-type"></a>Réplicas de exemplo 1 – 2 com uma réplica somente de configuração (tipo de cluster externo)

Este exemplo mostra como criar um grupo de disponibilidade de duas réplicas que usa uma réplica somente de configuração.

1.  Execute no nó que será a réplica primária que contém a cópia de leitura/gravação total dos bancos de dados. Este exemplo usa a propagação automática.

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
    
2.  Em uma janela de consulta conectada a outra réplica, execute o seguinte para unir a réplica no AG e iniciar o processo de propagação do primário para a réplica secundária.
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```
    
3.  Em uma janela de consulta conectada à réplica somente configuração, associe-o para o grupo de disponibilidade.
    
   ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
   ```

#### <a name="example-two--three-replicas-with-read-only-routing-external-cluster-type"></a>Réplicas de duas a três de exemplo com o roteamento de somente leitura (tipo de cluster externo)

Este exemplo mostra três completo réplicas e o roteamento como somente leitura podem ser configurados como parte da criação inicial do grupo de disponibilidade.

1.  Execute no nó que será a réplica primária que contém a cópia de leitura/gravação total dos bancos de dados. Este exemplo usa a propagação automática.

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
    
    Algumas coisas a observar sobre essa configuração:
    
    - *AGName* é o nome do grupo de disponibilidade.
    - *DBName* é o nome do banco de dados que será usado com o grupo de disponibilidade. Ele também pode ser uma lista de nomes separados por vírgulas.
    - *ListenerName* é um nome que é diferente de qualquer um dos servidores/nós subjacentes. Ele será registrado no DNS junto com *IPAddress*.
    - *IPAddress* é um endereço IP que está associado com *ListenerName*. Também é exclusiva e não o mesmo que qualquer um dos servidores/nós. Aplicativos e usuários finais será usar *ListenerName* ou *IPAddress* para conectar-se para o grupo de disponibilidade.
    - *Máscara de sub-rede* é a máscara de sub-rede *IPAddress*; por exemplo, 255.255.255.0.

2.  Em uma janela de consulta conectada a outra réplica, execute o seguinte para unir a réplica no AG e iniciar o processo de propagação do primário para a réplica secundária.
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```
    
3.  Repita a etapa 2 para a terceira réplica.

#### <a name="example-three--two-replicas-with-read-only-routing-none-cluster-type"></a>Réplicas de exemplo – dois a três com roteamento somente leitura (nenhum tipo de cluster)

Este exemplo mostra a criação de uma configuração de duas réplicas usando um tipo de cluster nenhum. Ele é usado para o cenário de escala de leitura em que nenhum failover é esperada. Isso cria o ouvinte que está, na verdade, a réplica primária, bem como o roteamento somente leitura, usando a funcionalidade de round robin.

1.  Execute no nó que será a réplica primária que contém a cópia de leitura/gravação total dos bancos de dados. Este exemplo usa a propagação automática.

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
    - *DBName* é o nome do banco de dados que será usado com o grupo de disponibilidade. Ele também pode ser uma lista de nomes separados por vírgulas.
    - *PortOfEndpoint* é o número da porta usado pelo ponto de extremidade criado.
    - *PortOfInstance* é o número da porta usado pela instância do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)].
    - *ListenerName* é um nome que é diferente de qualquer uma das réplicas subjacentes, mas realmente não será usado.
    - *PrimaryReplicaIPAddress* é o endereço IP da réplica primária.
    - *Máscara de sub-rede* é a máscara de sub-rede *IPAddress*. Por exemplo, 255.255.255.0.
    
2.  Una a réplica secundária para o grupo de disponibilidade e iniciar a propagação automática.
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = NONE);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```

## <a name="create-the-includessnoversion-mdincludesssnoversion-mdmd-login-and-permissions-for-pacemaker"></a>Criar o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] logon e permissões do Pacemaker

Um cluster de alta disponibilidade Pacemaker subjacente [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] no Linux precisa de acesso para o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] instância, bem como permissões no grupo de disponibilidade em si. Estas etapas criam o logon e as permissões associadas, junto com um arquivo que informa ao Pacemaker como fazer logon no [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)].

1.  Em uma janela de consulta conectada à primeira réplica, execute o seguinte:

    ```SQL
    CREATE LOGIN PMLogin WITH PASSWORD '<StrongPassword>';
    
    GO
    
    GRANT VIEW SERVER STATE TO PMLogin;
    
    GO
    
    GRANT ALTER, CONTROL, VIEW DEFINITION ON AVAILABILITY GROUP::<AGThatWasCreated> TO PMLogin;
    
    GO
    ```
    
2.  No nó 1, digite o comando 
    ```bash
    sudo emacs /var/opt/mssql/secrets/passwd
    ```
    
    Isso abrirá o editor Emacs.
    
3.  Insira duas linhas a seguir no editor:

    ```
    PMLogin
    <StrongPassword>
    ```
    
4.  Mantenha pressionada a tecla CTRL e, em seguida, pressione X, em seguida, C, para sair e salvar o arquivo.

5.  Execute (executar) 
    ```bash
    sudo chmod 400 /var/opt/mssql/secrets/passwd
    ```
    
    para bloquear o arquivo.

6.  Repita as etapas 1 a 5 nos outros servidores que servirão como réplicas.

## <a name="create-the-availability-group-resources-in-the-pacemaker-cluster-external-only"></a>Criar a disponibilidade do grupo de recursos do cluster do Pacemaker (externo)

Após um disponibilidade grupo é criado na [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], os recursos correspondentes devem ser criados no Pacemaker, quando um tipo de cluster externo é especificado. Há dois recursos associados a um grupo de disponibilidade: o grupo de disponibilidade em si e um endereço IP. Configurar o recurso de endereço IP é opcional, se você não estiver usando a funcionalidade de ouvinte, mas é recomendado.

O recurso de grupo de disponibilidade que é criado é um tipo especial de recurso chamado um clone. O recurso de grupo de disponibilidade tem, essencialmente, cópias em cada nó e há um recurso de controle chamado mestre. O mestre está associado com o servidor que hospeda a réplica primária. As réplicas secundárias (regulares ou somente de configuração) são consideradas servidores subordinados e pode ser promovidas a mestre em um failover.

1.  Crie o recurso de grupo de disponibilidade com a seguinte sintaxe:

    **Red Hat Enterprise Linux (RHEL) e Ubuntu**
    
    ```bash
    sudo pcs resource create <NameForAGResource> ocf:mssql:ag ag_name=<AGName> meta failure-timeout=30s --master meta notify=true
    ```

    >[!NOTE]
    >No RHEL 7.4, você poderá encontrar um aviso com o uso de - master. Para evitar isso, use `sudo pcs resource create <NameForAGResource> ocf:mssql:ag ag_name=<AGName> meta failover-timeout=30s master notify=true`
   
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
    
    em que *NameForAGResource* é o nome exclusivo dado a esse recurso de cluster para o grupo de disponibilidade, e *AGName* é o nome do grupo de disponibilidade que foi criado.
 
2.  Crie o recurso de endereço IP para o grupo de disponibilidade que será associado com a funcionalidade de ouvinte.

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
    
    em que *NameForIPResource* é o nome exclusivo para o recurso IP, e *IPAddress* é o endereço IP estático atribuído ao recurso. Em SLES, você também precisará fornecer a máscara de rede. Por exemplo, 255.255.255.0 teria um valor igual a 24 para *máscara de rede.*
    
3.  Para garantir que o endereço IP e o recurso de grupo de disponibilidade estão em execução no mesmo nó, uma restrição de colocação deve ser configurada.

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
    
    em que *NameForIPResource* é o nome para o recurso IP *NameForAGResource* é o nome do recurso de grupo de disponibilidade e em SLES, *NameForConstraint* é o nome para o restrição.

4.  Crie um restrição para garantir que o recurso de grupo de disponibilidade está ativo e em execução antes do endereço IP. Embora a restrição de colocação implica uma restrição de ordenação, isso aplicá-la.

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
    
    em que *NameForIPResource* é o nome para o recurso IP *NameForAGResource* é o nome do recurso de grupo de disponibilidade e em SLES, *NameForConstraint* é o nome para o restrição.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu a criar e configurar um grupo de disponibilidade para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] no Linux. Você aprendeu como para:
> [!div class="checklist"]
> * Habilite grupos de disponibilidade.
> * Pontos de extremidade de criar grupo de disponibilidade e certificados.
> * Use [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] (SSMS) ou o Transact-SQL para criar um grupo de disponibilidade.
> * Criar o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] logon e permissões do Pacemaker.
> * Crie recursos de grupo de disponibilidade em um cluster do Pacemaker.

Para a maioria das tarefas de administração de grupo de disponibilidade, incluindo atualizações e fazer failover, consulte:

> [!div class="nextstepaction"]
> [Operar o grupo de disponibilidade de alta disponibilidade para o SQL Server no Linux](sql-server-linux-availability-group-failover-ha.md)

