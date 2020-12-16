## <a name="prerequisites"></a>Prerequisites

Antes de criar o grupo de disponibilidade, você precisa:

- Definir seu ambiente para que todos os servidores que hospedam réplicas de disponibilidade possam se comunicar.
- Instale o SQL Server. Consulte [Instalar o SQL Server](../database-engine/install-windows/install-sql-server.md) para obter detalhes.

## <a name="enable-always-on-availability-groups-and-restart-mssql-server"></a>Habilitar grupos de disponibilidade Always On e reiniciar o mssql-server

>[!NOTE]
>O comando a seguir utiliza cmdlets do módulo sqlserver publicado na Galeria do PowerShell. É possível instalar esse módulo usando o comando Install-Module.

Habilite grupos de disponibilidade Always On em cada réplica que hospeda uma instância do SQL Server. Em seguida, reinicie o serviço do SQL Server. Execute o seguinte comando para habilitar e reiniciar os serviços do SQL Server:

```powershell
Enable-SqlAlwaysOn -ServerInstance <server\instance> -Force
```

## <a name="enable-an-alwayson_health-event-session"></a>Habilitar uma sessão de evento AlwaysOn_health

 Para ajudar com o diagnóstico da causa raiz ao solucionar problemas de um grupo de disponibilidade, é possível opcionalmente habilitar uma sessão de eventos estendidos (XEvents) de grupos de disponibilidade Always On. Para fazê-lo, execute o seguinte comando em cada instância do SQL Server:

```sql
ALTER EVENT SESSION  AlwaysOn_health ON SERVER WITH (STARTUP_STATE=ON);
GO
```

Para obter mais informações sobre essa sessão de XEvents, consulte [Eventos estendidos de grupos de disponibilidade Always On](../database-engine/availability-groups/windows/always-on-extended-events.md).

## <a name="database-mirroring-endpoint-authentication"></a>Autenticação do ponto de extremidade de espelhamento de banco de dados

Para a sincronização funcionar corretamente, as réplicas envolvidas no grupo de disponibilidade de escala de leitura precisarão autenticar pelo ponto de extremidade. Os dois cenários principais que você pode usar para essa autenticação são abordados nas próximas seções.

### <a name="service-account"></a>Conta de serviço

Em um ambiente do Active Directory em que todas as réplicas secundárias são ingressadas no mesmo domínio, o SQL Server pode autenticar usando a conta de serviço. Você precisa criar explicitamente um logon para a conta de serviço em cada instância do SQL Server:

```sql
CREATE LOGIN [<domain>\service account] FROM WINDOWS;
```

### <a name="sql-login-authentication"></a>Autenticação de logon do SQL

Em ambientes em que as réplicas secundárias podem não ser ingressadas em um Domínio do Active Directory, é necessário utilizar a autenticação do SQL. O script Transact-SQL a seguir cria um logon denominado `dbm_login` e um usuário chamado `dbm_user`. Atualize o script com uma senha forte. Para criar o usuário de ponto de extremidade de espelhamento de banco de dados, execute o seguinte comando em todas as instâncias do SQL Server:

```sql
CREATE LOGIN dbm_login WITH PASSWORD = '**<1Sample_Strong_Password!@#>**';
CREATE USER dbm_user FOR LOGIN dbm_login;
```

#### <a name="certificate-authentication"></a>Autenticação de certificado

Se você utiliza uma réplica secundária que requer autenticação com a autenticação do SQL, use um certificado para autenticar entre os pontos de extremidade de espelhamento.

O script Transact-SQL a seguir cria uma chave mestra e um certificado. Em seguida, ele faz backup do certificado e protege o arquivo com uma chave privada. Atualize o script com senhas fortes. Execute o script na instância primária do SQL Server para criar o certificado:

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate WITH SUBJECT = 'dbm';
BACKUP CERTIFICATE dbm_certificate
   TO FILE = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.cer'
   WITH PRIVATE KEY (
           FILE = 'c:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.pvk',
           ENCRYPTION BY PASSWORD = '**<Private_Key_Password>**'
       );
```

Nesse momento, sua réplica primária do SQL Server tem um certificado em `c:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.cer` e uma chave privada em `c:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.pvk`. Copie esses dois arquivos no mesmo local em todos os servidores que hospedarão as réplicas de disponibilidade.

Em cada réplica secundária, verifique se a conta de serviço da instância do SQL Server tem permissões para acessar o certificado.

#### <a name="create-the-certificate-on-secondary-servers"></a>Criar o certificado em servidores secundários

O script Transact-SQL a seguir cria uma chave mestra e um certificado com base no backup que você criou na réplica primária do SQL Server. O comando também autoriza usuários a acessarem o certificado. Atualize o script com senhas fortes. A senha de descriptografia é a mesma senha que você usou para criar o arquivo *.pvk* em uma etapa anterior. Para criar o certificado, execute o seguinte script em todas as réplicas secundárias:

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate
    AUTHORIZATION dbm_user
    FROM FILE = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.cer'
    WITH PRIVATE KEY (
    FILE = 'c:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.pvk',
    DECRYPTION BY PASSWORD = '**<Private_Key_Password>**'
            );
```

## <a name="create-database-mirroring-endpoints-on-all-replicas"></a>Criar pontos de extremidade de espelhamento de banco de dados em todas as réplicas

Os pontos de espelhamento de banco de dados usam o protocolo TCP para enviar e receber mensagens entre as instâncias de servidor que participam das sessões de espelhamento de banco de dados ou hospedam réplicas de disponibilidade. O ponto de extremidade de espelhamento de banco de dados escuta em um número da porta TCP exclusivo.

O script Transact-SQL a seguir cria um ponto de extremidade de escuta chamado `Hadr_endpoint` para o grupo de disponibilidade. Ele inicia o ponto de extremidade e concede permissão de conexão à conta de serviço ou ao logon do SQL criado em uma etapa anterior. Antes de executar o script, substitua os valores entre `**< ... >**`. Opcionalmente, é possível incluir um endereço IP, `LISTENER_IP = (0.0.0.0)`. O endereço IP do ouvinte deve ser um endereço IPv4. Também é possível usar `0.0.0.0`.

Atualize o script Transact-SQL a seguir para seu ambiente em todas as instâncias do SQL Server:

```SQL
CREATE ENDPOINT [Hadr_endpoint]
    AS TCP (LISTENER_PORT = **<5022>**)
    FOR DATA_MIRRORING (
        ROLE = ALL,
        AUTHENTICATION = CERTIFICATE dbm_certificate,
        ENCRYPTION = REQUIRED ALGORITHM AES
        );
ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
GRANT CONNECT ON ENDPOINT::[Hadr_endpoint] TO [<service account or user>];
```

A porta TCP no firewall deve estar aberta para a porta do ouvinte.

Para obter mais informações, consulte [O ponto de extremidade de espelhamento de banco de dados (SQL Server)](../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md).
