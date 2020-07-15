## <a name="prerequisites"></a>Pré-requisitos

Antes de criar o grupo de disponibilidade, você precisa:

- Definir seu ambiente para que todos os servidores que hospedam réplicas de disponibilidade possam se comunicar.
- Instale o SQL Server.

>[!NOTE]
>No Linux, você deve criar um grupo de disponibilidade antes de adicioná-lo como um recurso de cluster para ser gerenciado pelo cluster. Este documento fornece um exemplo que cria o grupo de disponibilidade. Para ver instruções específicas à distribuição para criar o cluster e adicionar o grupo de disponibilidade como um recurso de cluster, confira os links em "Próximas etapas".

1. Atualize o nome do computador para cada host.

   Cada nome do SQL Server deve:
   
   - Ter 15 caracteres ou menos.
   - Ser exclusivo dentro da rede.
   
   Para definir o nome do computador, edite `/etc/hostname`. O script a seguir permite que você edite `/etc/hostname` com `vi`:

   ```bash
   sudo vi /etc/hostname
   ```

2. Configurar o arquivo dos hosts.

    >[!NOTE]
    >Se os nomes de host estiverem registrados com o IP no servidor DNS, não será necessário executar as etapas abaixo. Valide que todos os nós que farão parte da configuração do grupo de disponibilidade possam se comunicar uns com os outros. (Um ping para o nome do host deve fornecer o endereço IP correspondente.) Além disso, verifique se o arquivo /etc/hosts não contém um registro que mapeia o endereço IP do localhost, 127.0.0.1 com o nome do host do nó.
    >

   O arquivo de hosts em cada servidor contém os endereços IP e nomes de todos os servidores que farão parte do grupo de disponibilidade. 

   O comando a seguir retorna o endereço IP do servidor atual:

   ```bash
   sudo ip addr show
   ```

   Atualizar `/etc/hosts`. O script a seguir permite que você edite `/etc/hosts` com `vi`:

   ```bash
   sudo vi /etc/hosts
   ```

   A exemplo a seguir mostra `/etc/hosts` no **node1** com adições para **node1**, **node2** e **node3**. Neste documento, **node1** se refere ao servidor que hospeda a réplica primária. E **node2** e **node3** se referem a servidores que hospedam réplicas secundárias.

    ```
    127.0.0.1   localhost localhost4 localhost4.localdomain4
    ::1       localhost localhost6 localhost6.localdomain6
    10.128.18.12 node1
    10.128.16.77 node2
    10.128.15.33 node3
    ```

### <a name="install-sql-server"></a>Instale o SQL Server

Instale o SQL Server. Os links a seguir apontam para instruções de instalação do SQL Server para diversas distribuições: 

- [Red Hat Enterprise Linux](../linux/quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md)
- [Ubuntu](../linux/quickstart-install-connect-ubuntu.md)

## <a name="enable-alwayson-availability-groups-and-restart-mssql-server"></a>Habilitar grupos de disponibilidade Always On e reiniciar o mssql-server

Habilite grupos de disponibilidade AlwaysOn em cada nó que hospeda uma instância do SQL Server. Em seguida, reinicie `mssql-server`. Execute o seguinte script:

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

##  <a name="enable-an-alwayson_health-event-session"></a>Habilitar uma sessão de evento AlwaysOn_health 

Como opção, é possível habilitar eventos estendidos de grupos de disponibilidade AlwaysOn para ajudar com o diagnóstico da causa raiz ao solucionar problemas de um grupo de disponibilidade. Execute o seguinte comando em cada instância do SQL Server: 

```SQL
ALTER EVENT SESSION  AlwaysOn_health ON SERVER WITH (STARTUP_STATE=ON);
GO
```

Para obter mais informações sobre essa sessão XE, confira [Eventos estendidos sempre ativados](../database-engine/availability-groups/windows/always-on-extended-events.md).

## <a name="create-a-certificate"></a>Criar um certificado

O serviço do SQL Server no Linux usa certificados para autenticar a comunicação entre os pontos de extremidade de espelhamento. 

O script Transact-SQL a seguir cria uma chave mestra e um certificado. Em seguida, ele faz backup do certificado e protege o arquivo com uma chave privada. Atualize o script com senhas fortes. Conecte-se à instância primária do SQL Server. Para criar o certificado, execute o seguinte script Transact-SQL:

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

Nesse momento, sua réplica primária do SQL Server tem um certificado em `/var/opt/mssql/data/dbm_certificate.cer` e uma chave privada em `var/opt/mssql/data/dbm_certificate.pvk`. Copie esses dois arquivos no mesmo local em todos os servidores que hospedarão as réplicas de disponibilidade. Use o usuário mssql ou conceda permissão ao usuário mssql para acessar esses arquivos. 

Por exemplo, no servidor de origem, o comando a seguir copia os arquivos para o computador de destino. Substitua os valores `**<node2>**` pelos nomes das instâncias do SQL Server que hospedarão as réplicas. 

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

O script Transact-SQL a seguir cria uma chave mestra e um certificado com base no backup que você criou na réplica primária do SQL Server. Atualize o script com senhas fortes. A senha de descriptografia é a mesma senha que você usou para criar o arquivo. pvk em uma etapa anterior. Para criar o certificado, execute o script a seguir em todos os servidores secundários:

```SQL
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate
    FROM FILE = '/var/opt/mssql/data/dbm_certificate.cer'
    WITH PRIVATE KEY (
    FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
    DECRYPTION BY PASSWORD = '**<Private_Key_Password>**'
            );
```

## <a name="create-the-database-mirroring-endpoints-on-all-replicas"></a>Criar os pontos de extremidade de espelhamento de banco de dados em todas as réplicas

Os pontos de espelhamento de banco de dados usam o TCP (Protocolo de Controle de Transmissão) para enviar e receber mensagens entre as instâncias de servidor que participam das sessões de espelhamento de banco de dados ou hospedam réplicas de disponibilidade. O ponto de extremidade de espelhamento de banco de dados escuta em um exclusivo número de porta TCP. 

O script Transact-SQL a seguir cria um ponto de extremidade de escuta chamado `Hadr_endpoint` para o grupo de disponibilidade. Ele começa no ponto de extremidade e concede a permissão de conexão para o certificado que você criou. Antes de executar o script, substitua os valores entre `**< ... >**`. Ou é possível incluir um endereço IP `LISTENER_IP = (0.0.0.0)`. O endereço IP do ouvinte deve ser um endereço IPv4. Também é possível usar `0.0.0.0`. 

Atualize o script Transact-SQL a seguir para seu ambiente em todas as instâncias do SQL Server: 

```SQL
CREATE ENDPOINT [Hadr_endpoint]
    AS TCP (LISTENER_PORT = **<5022>**)
    FOR DATABASE_MIRRORING (
        ROLE = ALL,
        AUTHENTICATION = CERTIFICATE dbm_certificate,
        ENCRYPTION = REQUIRED ALGORITHM AES
        );
ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
```

>[!NOTE]
>Se você usar o SQL Server Express Edition em um nó para hospedar uma réplica somente de configuração, o único valor válido para `ROLE` será `WITNESS`. Execute o seguinte script no SQL Server Express Edition:

```SQL
CREATE ENDPOINT [Hadr_endpoint]
    AS TCP (LISTENER_PORT = **<5022>**)
    FOR DATABASE_MIRRORING (
        ROLE = WITNESS,
        AUTHENTICATION = CERTIFICATE dbm_certificate,
        ENCRYPTION = REQUIRED ALGORITHM AES
        );
ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
```

A porta TCP no firewall deve estar aberta para a porta do ouvinte.



>[!IMPORTANT]
>Para a versão do SQL Server 2017, o único método de autenticação com suporte para o ponto de extremidade com espelhamento de banco de dados é o `CERTIFICATE`. A opção `WINDOWS` será habilitada em uma versão futura.

Para obter mais informações, consulte [O ponto de extremidade de espelhamento de banco de dados (SQL Server)](https://msdn.microsoft.com/library/ms179511.aspx).


