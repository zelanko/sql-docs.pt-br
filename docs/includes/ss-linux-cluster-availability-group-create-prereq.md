## <a name="prerequisites"></a>Pré-requisitos

Antes de criar o grupo de disponibilidade, você precisa:

- Definir o seu ambiente para que todos os servidores que hospedam réplicas de disponibilidade possam se comunicar
- Instalar o SQL Server

>[!NOTE]
>No Linux, você deve criar um grupo de disponibilidade antes de adicioná-lo como um recurso de cluster para ser gerenciado pelo cluster. Este documento fornece um exemplo que cria o grupo de disponibilidade. Para ver instruções específicas à distribuição para criar o cluster e adicionar o grupo de disponibilidade como um recurso de cluster, consulte os links em [Próximas etapas](#next-steps).

1. **Atualizar o nome do computador para cada host**

   Cada nome do SQL Server deve:
   
   - Ter 15 caracteres ou menos
   - Ser exclusivo dentro da rede
   
   Para definir o nome do computador, edite `/etc/hostname`. O script a seguir permite que você edite `/etc/hostname` com `vi`.

   ```bash
   sudo vi /etc/hostname
   ```

1. **Configurar o arquivo dos hosts**

>[!NOTE]
>Se os nomes de host estiverem registrados com o IP no servidor DNS, não será necessário executar as etapas abaixo. Valide se todos os nós que fazem parte da configuração do grupo de disponibilidade podem se comunicar entre si (ping no nome do host deverá responder com o endereço IP correspondente). Além disso, verifique se o arquivo /etc/hosts não contém um registro que mapeia o endereço IP do localhost, 127.0.0.1 com o nome do host do nó.


   O arquivo de hosts em cada servidor contém os endereços IP e nomes de todos os servidores que farão parte do grupo de disponibilidade. 

   O comando a seguir retorna o endereço IP do servidor atual:

   ```bash
   sudo ip addr show
   ```

   Atualize `/etc/hosts`. O script a seguir permite que você edite `/etc/hosts` com `vi`.

   ```bash
   sudo vi /etc/hosts
   ```

   A exemplo a seguir mostra `/etc/hosts` no **node1** com adições para **node1**, **node2** e **node3**. Neste documento, **node1** se refere ao servidor que hospeda a réplica primária. **node2** e **node3** se referem a servidores que hospedam réplicas secundárias.


   ```
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1       localhost localhost6 localhost6.localdomain6
   10.128.18.12 node1
   10.128.16.77 node2
   10.128.15.33 node3
   ```

### <a name="install-sql-server"></a>Instalar o SQL Server

Instale o SQL Server. Os links a seguir apontam para instruções de instalação do SQL Server para diversas distribuições. 

- [Red Hat Enterprise Linux](../linux/quickstart-install-connect-red-hat.md)

- [SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md)

- [Ubuntu](../linux/quickstart-install-connect-ubuntu.md)

## <a name="enable-always-on-availability-groups-and-restart-sqlserver"></a>Habilitar grupos de disponibilidade Always On e reiniciar o SQL Server

Habilite grupos de disponibilidade AlwaysOn em cada nó que hospeda uma instância do SQL Server e, em seguida, reinicie o `mssql-server`.  Execute o seguinte script:

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

##  <a name="enable-alwaysonhealth-event-session"></a>Habilitar a sessão de evento AlwaysOn_health 

Como opção, é possível habilitar eventos estendidos de grupos de disponibilidade Always On para ajudar com o diagnóstico da causa raiz ao solucionar problemas de um grupo de disponibilidade. Execute o comando a seguir em cada instância do SQL Server. 

```Transact-SQL
ALTER EVENT SESSION  AlwaysOn_health ON SERVER WITH (STARTUP_STATE=ON);
GO
```

Para obter mais informações sobre essa sessão XE, consulte [Eventos de extensão Always On](http://msdn.microsoft.com/library/dn135324.aspx).

## <a name="create-db-mirroring-endpoint-user"></a>Criar usuário do ponto de extremidade de espelhamento de bd

O script de Transact-SQL a seguir cria um logon denominado `dbm_login` e um usuário chamado `dbm_user`. Atualize o script com uma senha forte. Execute o seguinte comando em todos as instâncias do SQL Server para criar o usuário de ponto de extremidade de espelhamento de banco de dados.

```Transact-SQL
CREATE LOGIN dbm_login WITH PASSWORD = '**<1Sample_Strong_Password!@#>**';
CREATE USER dbm_user FOR LOGIN dbm_login;
```

## <a name="create-a-certificate"></a>Criar um certificado

O serviço do SQL Server no Linux usa certificados para autenticar a comunicação entre os pontos de extremidade de espelhamento. 

O script de Transact-SQL a seguir cria uma chave mestra e um certificado. Em seguida, ele faz backup do certificado e protege o arquivo com uma chave privada. Atualize o script com senhas fortes. Conecte-se à instância primária do SQL Server e execute a seguinte Transact-SQL para criar o certificado:

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

Neste ponto, a réplica primária do SQL Server tem um certificado em `/var/opt/mssql/data/dbm_certificate.cer` e uma chave privada em `var/opt/mssql/data/dbm_certificate.pvk`. Copie esses dois arquivos no mesmo local em todos os servidores que hospedarão as réplicas de disponibilidade. Use o usuário mssql ou conceda permissão ao usuário mssql para acessar esses arquivos. 

Por exemplo, no servidor de origem, o comando a seguir copia os arquivos para o computador de destino. Substitua os valores **<node2>** pelos nomes das instâncias do SQL Server que hospedarão as réplicas. 

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

O script do Transact-SQL a seguir cria uma chave mestra e um certificado com base no backup que você criou na réplica primária do SQL Server. O comando também autoriza o usuário a acessar o certificado. Atualize o script com senhas fortes. A senha de descriptografia é a mesma senha que você usou para criar o arquivo. pvk em uma etapa anterior. Execute o script a seguir em todos os servidores secundários para criar o certificado.

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

## <a name="create-the-database-mirroring-endpoints-on-all-replicas"></a>Crie os pontos de extremidade de espelhamento de banco de dados em todas as réplicas

Os pontos de espelhamento de banco de dados usam o Protocolo de Controle de Transmissão (TCP) para enviar e receber mensagens entre as instâncias de servidor que participam das sessões do espelhamento de banco de dados ou hospedam réplicas de disponibilidade. O ponto de extremidade de espelhamento de banco de dados escuta em um exclusivo número de porta TCP. 

O Transact-SQL a seguir cria um ponto de extremidade de escuta chamado `Hadr_endpoint` para o grupo de disponibilidade. Ele começa no ponto de extremidade e concede a permissão de conexão para o usuário que você criou. Antes de executar o script, substitua os valores entre `**< ... >**`.

>[!NOTE]
>Para esta versão, não use um endereço IP diferente para o IP do ouvinte. Estamos trabalhando para corrigir esse problema, mas o único valor aceitável por hora é “0.0.0.0”.

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

>[!IMPORTANT]
>Para a versão do SQL Server 2017, o único método de autenticação com suporte para o ponto de extremidade com espelhamento de banco de dados é o `CERTIFICATE`. A opção `WINDOWS` será habilitada em uma versão futura.

Para obter mais informações, consulte [O Ponto de Extremidade de Espelhamento de Banco de Dados (SQL Server)](http://msdn.microsoft.com/library/ms179511.aspx).
