## <a name="prerequisites"></a>Pré-requisitos

Antes de criar o grupo de disponibilidade, você precisa:

- Definir o seu ambiente para que todos os servidores que hospedam réplicas de disponibilidade podem se comunicar
- Instalar o SQL Server

>[!NOTE]
>No Linux, você deve criar um grupo de disponibilidade antes de adicioná-lo como um recurso de cluster para ser gerenciado pelo cluster. Este documento fornece um exemplo que cria o grupo de disponibilidade. Distribuição de instruções específicas para criar o cluster e adicione o grupo de disponibilidade como um recurso de cluster, consulte os links em [próximas etapas](#next-steps).

1. **Atualizar o nome do computador para cada host**

   Cada nome de SQL Server deve ser:
   
   - 15 caracteres ou menos
   - Exclusivo dentro da rede
   
   Para definir o nome do computador, editar `/etc/hostname`. O script a seguir permite que você edite `/etc/hostname` com `vi`.

   ```bash
   sudo vi /etc/hostname
   ```

1. **Configurar o arquivo de hosts**

>[!NOTE]
>Se os nomes de host são registrados com o IP no servidor DNS, não é necessário executar as etapas abaixo. Valide que todos os nós que serão parte da configuração do grupo de disponibilidade podem se comunicar entre si (ping o nome do host deve responder com o endereço IP correspondente). Além disso, certifique-se de que o arquivo /etc/hosts não contém um registro que mapeia o endereço IP de localhost, 127.0.0.1 com o nome do host do nó.


   O arquivo de hosts em cada servidor contém os endereços IP e nomes de todos os servidores que farão parte do grupo de disponibilidade. 

   O comando a seguir retorna o endereço IP do servidor atual:

   ```bash
   sudo ip addr show
   ```

   Atualização `/etc/hosts`. O script a seguir permite que você edite `/etc/hosts` com `vi`.

   ```bash
   sudo vi /etc/hosts
   ```

   A exemplo a seguir mostra `/etc/hosts` na **node1** com adições para **node1** e **node2**. Neste documento **node1** refere-se à réplica primária do SQL Server. **Node2** refere-se ao SQL Server secundário.;


   ```
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1       localhost localhost6 localhost6.localdomain6
   10.128.18.128 node1
   10.128.16.77 node2
   ```

### <a name="install-sql-server"></a>Instalar o SQL Server

Instale o SQL Server. Os links a seguir apontam para instruções de instalação do SQL Server para diversas distribuições. 

- [Red Hat Enterprise Linux](..\linux\sql-server-linux-setup-red-hat.md)

- [SUSE Linux Enterprise Server](..\linux\sql-server-linux-setup-suse-linux-enterprise-server.md)

- [Ubuntu](..\linux\sql-server-linux-setup-ubuntu.md)

## <a name="enable-always-on-availability-groups-and-restart-sqlserver"></a>Habilitar grupos de disponibilidade AlwaysOn e reinicie o SQL Server

Habilitar grupos de disponibilidade AlwaysOn em cada nó que hospeda o serviço do SQL Server e reinicie o `mssql-server`.  Execute o seguinte script:

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

##    <a name="enable-alwaysonhealth-event-session"></a>Habilitar a sessão de evento AlwaysOn_health 

Você pode habilitar optionaly grupos de disponibilidade AlwaysOn específico eventos estendidos para ajudar com o diagnóstico da causa raiz ao solucionar problemas de um grupo de disponibilidade.

```Transact-SQL
ALTER EVENT SESSION  AlwaysOn_health ON SERVER WITH (STARTUP_STATE=ON);
GO
```

Para obter mais informações sobre essa sessão XE, consulte [sempre em eventos estendidos](http://msdn.microsoft.com/library/dn135324.aspx).

## <a name="create-db-mirroring-endpoint-user"></a>Criar usuário do ponto de extremidade de espelhamento de banco de dados

Script Transact-SQL a seguir cria um logon denominado `dbm_login`e um usuário chamado `dbm_user`. Atualize o script com uma senha forte. Execute o seguinte comando em todos os servidores do SQL para criar o usuário de ponto de extremidade de espelhamento de banco de dados.

```Transact-SQL
CREATE LOGIN dbm_login WITH PASSWORD = '**<1Sample_Strong_Password!@#>**';
CREATE USER dbm_user FOR LOGIN dbm_login;
```

## <a name="create-a-certificate"></a>Criar um certificado

O serviço do SQL Server no Linux usa certificados para autenticar a comunicação entre os pontos de extremidade de espelhamento. 

Script Transact-SQL a seguir cria uma chave mestra e o certificado. Em seguida, faz o certificado de backup e protege o arquivo com uma chave privada. Atualize o script com senhas fortes. Conecte-se ao servidor SQL primário e execute a seguinte Transact-SQL para criar o certificado:

```Transact-SQL
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate WITH SUBJECT = 'dbm';
BACKUP CERTIFICATE dbm_certificate
   TO FILE = '/var/opt/mssql/data/dbm_certificate.cer'
   WITH PRIVATE KEY (
           FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
           ENCRYPTION BY PASSWORD = '**<Private_Key_Password>**'
       );
```

Neste ponto, a réplica primária do SQL Server tem um certificado em `/var/opt/mssql/data/dbm_certificate.cer` e um at chave privada `var/opt/mssql/data/dbm_certificate.pvk`. Copie esses dois arquivos no mesmo local em todos os servidores que hospedam réplicas de disponibilidade. Use o usuário mssql ou conceder permissão ao usuário mssql para acessar esses arquivos. 

Por exemplo no servidor de origem, o comando a seguir copia os arquivos para o computador de destino. Substitua o  **<node2>**  valores com os nomes das instâncias do SQL Server que hospedam as réplicas. 

```bash
cd /var/opt/mssql/data
scp dbm_certificate.* root@**<node2>**:/var/opt/mssql/data/
```

No servidor de destino, dê permissão ao usuário mssql para acessar o certificado.

```bash
cd /var/opt/mssql/data
chown mssql:mssql dbm_certificate.*
```

## <a name="create-the-certificate-on-secondary-servers"></a>Criar o certificado em servidores secundários

Script Transact-SQL a seguir cria uma chave mestra e o certificado do backup que você criou na réplica primária do SQL Server. O comando também autoriza o usuário a acessar o certificado. Atualize o script com senhas fortes. A senha de descriptografia é a mesma senha que você usou para criar o arquivo. pvk em uma etapa anterior. Execute o seguinte script em todos os servidores secundários para criar o certificado.

```Transact-SQL
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate   
    AUTHORIZATION dbm_user
    FROM FILE = '/var/opt/mssql/data/dbm_certificate.cer'
    WITH PRIVATE KEY (
    FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
    DECRYPTION BY PASSWORD = '**<Private_Key_Password>**'
            );
```

## <a name="create-the-database-mirroring-endpoints-on-all-replicas"></a>Criar o pontos de extremidade em todas as réplicas de espelhamento de banco de dados

Os pontos de espelhamento de banco de dados usam o Protocolo de Controle de Transmissão (TCP) para enviar e receber mensagens entre as instâncias de servidor que participam das sessões do espelhamento de banco de dados ou hospedam réplicas de disponibilidade. O ponto de extremidade de espelhamento de banco de dados escuta em um exclusivo número de porta TCP. 

O Transact-SQL a seguir cria um ponto de extremidade de escutando chamado `Hadr_endpoint` para o grupo de disponibilidade. Iniciar o ponto de extremidade e concede a permissão de conexão para o usuário que você criou. Antes de executar o script, substitua os valores entre `**< ... >**`.


>[!NOTE]
>Para esta versão, não use um endereço IP diferente para o IP do ouvinte. Estamos trabalhando para corrigir esse problema, mas o único valor aceitável para agora é '0.0.0.0'.

Atualizar o Transact-SQL a seguir para o seu ambiente em todas as instâncias do SQL Server: 

```Transact-SQL
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

>[!IMPORTANT]
>A porta TCP no firewall precisa ser aberta para a porta do ouvinte.

Para obter mais informações, consulte [o banco de dados do ponto de extremidade espelhamento (SQL Server)](http://msdn.microsoft.com/library/ms179511.aspx).
