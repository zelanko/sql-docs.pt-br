## <a name="prerequisites"></a>Pré-requisitos

Antes de criar o grupo de disponibilidade, você precisa:

- Defina o seu ambiente para que todos os servidores que hospedam réplicas de disponibilidade podem se comunicar.
- Instale o SQL Server.

>[!NOTE]
>No Linux, você deve criar um grupo de disponibilidade antes de adicioná-lo como um recurso de cluster para ser gerenciado pelo cluster. Este documento fornece um exemplo que cria o grupo de disponibilidade. Para obter instruções específicas de distribuição para criar o cluster e adicione o grupo de disponibilidade como um recurso de cluster, consulte os links em "Próximas etapas".

1. Atualize o nome do computador para cada host.

   Cada nome do SQL Server deve:
   
   - 15 caracteres ou menos.
   - Exclusivo dentro da rede.
   
   Para definir o nome do computador, edite `/etc/hostname`. O script a seguir permite que você edite `/etc/hostname` com `vi`:

   ```bash
   sudo vi /etc/hostname
   ```

2. Configure o arquivo de hosts.

    >[!NOTE]
    >Se os nomes de host são registrados com o IP no servidor DNS, você não precisa fazer as seguintes etapas. Valide que todos os nós devem ser parte da configuração do grupo de disponibilidade podem se comunicar uns com os outros. (Um ping para o nome do host deve responder com o endereço IP correspondente). Além disso, certifique-se de que o arquivo /etc/hosts não contém um registro que mapeia o endereço IP do host local 127.0.0.1 com o nome do host do nó.
    >

   O arquivo de hosts em cada servidor contém os endereços IP e nomes de todos os servidores que farão parte do grupo de disponibilidade. 

   O comando a seguir retorna o endereço IP do servidor atual:

   ```bash
   sudo ip addr show
   ```

   Atualize `/etc/hosts`. O script a seguir permite que você edite `/etc/hosts` com `vi`:

   ```bash
   sudo vi /etc/hosts
   ```

   A exemplo a seguir mostra `/etc/hosts` no **node1** com adições para **node1**, **node2** e **node3**. Neste documento, **node1** refere-se ao servidor que hospeda a réplica primária. E **node2** e **node3** se referir a servidores que hospedam as réplicas secundárias.

    ```
    127.0.0.1   localhost localhost4 localhost4.localdomain4
    ::1       localhost localhost6 localhost6.localdomain6
    10.128.18.12 node1
    10.128.16.77 node2
    10.128.15.33 node3
    ```

### <a name="install-sql-server"></a>Instalar o SQL Server

Instale o SQL Server. Os links a seguir apontem para instruções de instalação do SQL Server para diversas distribuições: 

- [Red Hat Enterprise Linux](../linux/quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md)
- [Ubuntu](../linux/quickstart-install-connect-ubuntu.md)

## <a name="enable-alwayson-availability-groups-and-restart-mssql-server"></a>Habilitar grupos de disponibilidade do AlwaysOn e reinicie o servidor mssql

Habilite grupos de disponibilidade AlwaysOn em cada nó que hospeda uma instância do SQL Server. Reinicie o `mssql-server`. Execute o seguinte script:

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

##  <a name="enable-an-alwaysonhealth-event-session"></a>Habilitar uma sessão de evento AlwaysOn_health 

Opcionalmente, você pode habilitar eventos estendidos do AlwaysOn disponibilidade grupos ajudar com o diagnóstico da causa raiz ao solucionar problemas de um grupo de disponibilidade. Execute o seguinte comando em cada instância do SQL Server: 

```SQL
ALTER EVENT SESSION  AlwaysOn_health ON SERVER WITH (STARTUP_STATE=ON);
GO
```

Para obter mais informações sobre essa sessão XE, consulte [AlwaysOn eventos estendidos](http://msdn.microsoft.com/library/dn135324.aspx).

## <a name="create-a-database-mirroring-endpoint-user"></a>Criar um usuário de ponto de extremidade de espelhamento de banco de dados

Script Transact-SQL a seguir cria um logon denominado `dbm_login` e um usuário chamado `dbm_user`. Atualize o script com uma senha forte. Para criar o usuário de ponto de extremidade de espelhamento de banco de dados, execute o seguinte comando em todas as instâncias do SQL Server:

```SQL
CREATE LOGIN dbm_login WITH PASSWORD = '**<1Sample_Strong_Password!@#>**';
CREATE USER dbm_user FOR LOGIN dbm_login;
```

## <a name="create-a-certificate"></a>Criar um certificado

O serviço do SQL Server no Linux usa certificados para autenticar a comunicação entre os pontos de extremidade de espelhamento. 

Script Transact-SQL a seguir cria uma chave mestra e um certificado. Em seguida, ele faz o backup do certificado e protege o arquivo com uma chave privada. Atualize o script com senhas fortes. Conecte-se à instância do SQL Server primária. Para criar o certificado, execute o seguinte script do Transact-SQL:

```SQL
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate WITH SUBJECT = 'dbm';
BACKUP CERTIFICATE dbm_certificate
   TO FILE = '/var/opt/mssql/data/dbm_certificate.cer'
   WITH PRIVATE KEY (
           FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
           ENCRYPTION BY PASSWORD = '**<Private_Key_Password>**'
       );
```

Neste ponto, a réplica primária do SQL Server tem um certificado em `/var/opt/mssql/data/dbm_certificate.cer` e um at chave privada `var/opt/mssql/data/dbm_certificate.pvk`. Copie esses dois arquivos no mesmo local em todos os servidores que hospedarão as réplicas de disponibilidade. Use o usuário mssql ou conceder permissão ao usuário mssql para acessar esses arquivos. 

Por exemplo, no servidor de origem, o comando a seguir copia os arquivos para o computador de destino. Substitua o `**<node2>**` valores com os nomes das instâncias do SQL Server que hospedam as réplicas. 

```bash
cd /var/opt/mssql/data
scp dbm_certificate.* root@**<node2>**:/var/opt/mssql/data/
```

Em cada servidor de destino, dê permissão ao usuário mssql para acessar o certificado.

```bash
cd /var/opt/mssql/data
chown mssql:mssql dbm_certificate.*
```

## <a name="create-the-certificate-on-secondary-servers"></a>Criar o certificado em servidores secundários

Script Transact-SQL a seguir cria uma chave mestra e um certificado de backup que você criou na réplica primária do SQL Server. O comando também autoriza o usuário a acessar o certificado. Atualize o script com senhas fortes. A senha de descriptografia é a mesma senha que você usou para criar o arquivo. pvk em uma etapa anterior. Para criar o certificado, execute o seguinte script em todos os servidores secundários:

```SQL
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate   
    AUTHORIZATION dbm_user
    FROM FILE = '/var/opt/mssql/data/dbm_certificate.cer'
    WITH PRIVATE KEY (
    FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
    DECRYPTION BY PASSWORD = '**<Private_Key_Password>**'
            );
```

## <a name="create-the-database-mirroring-endpoints-on-all-replicas"></a>Criar os pontos de extremidade de espelhamento de banco de dados em todas as réplicas

Pontos de extremidade de espelhamento do banco de dados usam o protocolo de controle de transmissão (TCP) para enviar e receber mensagens entre instâncias do servidor que participam de sessões de espelhamento de banco de dados ou hospedam réplicas de disponibilidade. O ponto de extremidade de espelhamento de banco de dados escuta em um exclusivo número de porta TCP. O ouvinte TCP requer um endereço IP do ouvinte. O endereço IP do ouvinte deve ser um endereço IPv4. Você também pode usar `0.0.0.0`. 

Script Transact-SQL a seguir cria um ponto de extremidade de escutando chamado `Hadr_endpoint` para o grupo de disponibilidade. Ele inicia o ponto de extremidade e concede permissão de conexão para o usuário que você criou. Antes de executar o script, substitua os valores entre `**< ... >**`.

Atualize o script Transact-SQL a seguir para o seu ambiente em todas as instâncias do SQL Server: 

```SQL
CREATE ENDPOINT [Hadr_endpoint]
    AS TCP (LISTENER_IP = (0.0.0.0), LISTENER_PORT = **<5022>**)
    FOR DATA_MIRRORING (
        ROLE = ALL,
        AUTHENTICATION = CERTIFICATE dbm_certificate,
        ENCRYPTION = REQUIRED ALGORITHM AES
        );
ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
GRANT CONNECT ON ENDPOINT::[Hadr_endpoint] TO [dbm_login];
```

>[!NOTE]
>Se você usar o SQL Server Express Edition em um nó para hospedar uma réplica somente para configuração, o único valor válido para `ROLE` é `WITNESS`. Execute o seguinte script no SQL Server Express Edition:

```SQL
CREATE ENDPOINT [Hadr_endpoint]
    AS TCP (LISTENER_IP = (0.0.0.0), LISTENER_PORT = **<5022>**)
    FOR DATA_MIRRORING (
        ROLE = WITNESS,
        AUTHENTICATION = CERTIFICATE dbm_certificate,
        ENCRYPTION = REQUIRED ALGORITHM AES
        );
ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
GRANT CONNECT ON ENDPOINT::[Hadr_endpoint] TO [dbm_login];
```

A porta TCP no firewall deve estar aberta para a porta do ouvinte.



>[!IMPORTANT]
>Para a versão do SQL Server 2017, o único método de autenticação com suporte para o ponto de extremidade de espelhamento de banco de dados é `CERTIFICATE`. O `WINDOWS` opção será habilitada em uma versão futura.

Para obter mais informações, consulte [o banco de dados (SQL Server) do ponto de extremidade de espelhamento](http://msdn.microsoft.com/library/ms179511.aspx).


