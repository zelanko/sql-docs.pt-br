---
title: Configurar o cluster de disco compartilhado SLES para o SQL Server
description: Implemente a alta disponibilidade configurando o cluster de disco compartilhado do SLES (SUSE Linux Enterprise Server) para o SQL Server.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: e5ad1bdd-c054-4999-a5aa-00e74770b481
ms.openlocfilehash: 70701d5c0103da089444177db1143066d0c862cd
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68032227"
---
# <a name="configure-sles-shared-disk-cluster-for-sql-server"></a>Configurar o cluster de disco compartilhado SLES para o SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este guia fornece instruções sobre como criar um cluster de disco compartilhado de dois nós para o SQL Server no SLES (SUSE Linux Enterprise Server). A camada de clustering baseia-se no [HAE (Extensão de Alta Disponibilidade)](https://www.suse.com/products/highavailability) do SUSE criado com base no [Pacemaker](https://clusterlabs.org/). 

Para obter mais informações sobre configuração de cluster, opções do agente de recursos, gerenciamento, melhores práticas e recomendações, confira a [Extensão de Alta Disponibilidade do SUSE Linux Enterprise 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html).

## <a name="prerequisites"></a>Prerequisites

Para concluir o cenário de ponta a ponta a seguir, você precisará de dois computadores para implantar o cluster de dois nós e outro servidor para configurar o compartilhamento NFS. As etapas abaixo descrevem como esses servidores serão configurados.

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>Instalar e configurar o sistema operacional em cada nó de cluster

A primeira etapa é configurar o sistema operacional nos nós de cluster. Para esse passo a passo, use o SLES com uma assinatura válida para o complemento de HA.

## <a name="install-and-configure-sql-server-on-each-cluster-node"></a>Instalar e configurar o SQL Server em cada nó de cluster

1. Instalar e configurar o SQL Server em ambos os nós. Para obter instruções detalhadas, confira [Instalar o SQL Server em Linux](sql-server-linux-setup.md).
2. Designe um nó como primário e o outro como secundário para fins de configuração. Use esses termos para seguir este guia. 
3. No nó secundário, interrompa e desabilite o SQL Server. O seguinte exemplo interrompe e desabilita o SQL Server:

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl disable mssql-server
    ```

    > [!NOTE]
    > No momento da instalação, uma Chave Mestra do Servidor é gerada para a Instância do SQL Server e colocada em `/var/opt/mssql/secrets/machine-key`. No Linux, o SQL Server sempre é executado como uma conta local chamada mssql. Como é uma conta local, a identidade dela não é compartilhada entre os nós. Portanto, você precisa copiar a chave de criptografia do nó primário para cada nó secundário, de modo que cada conta mssql local possa acessá-la para descriptografar a Chave Mestra do Servidor.
4. No nó primário, crie um logon do SQL Server para o Pacemaker e conceda a permissão de logon para executar `sp_server_diagnostics`. O Pacemaker usa essa conta para verificar qual nó está executando o SQL Server.

    ```bash
    sudo systemctl start mssql-server
    ```
    Conecte-se ao banco de dados mestre do SQL Server com a conta 'SA' e execute o seguinte:

    ```sql
    USE [master]
    GO
    CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'
    GRANT VIEW SERVER STATE TO <loginName>
    ```
5. No nó primário, interrompa e desabilite o SQL Server.
6. Siga as instruções descritas [na documentação do SUSE](https://www.suse.com/documentation/sles11/book_sle_admin/data/sec_basicnet_yast.html) para configurar e atualizar o arquivo de hosts para cada nó de cluster. O arquivo 'hosts' precisa incluir o endereço IP e o nome de cada nó de cluster.

    Para verificar o endereço IP da execução do nó atual:

    ```bash
    sudo ip addr show
    ```

    Defina o nome do computador em cada nó. Dê a cada nó um nome exclusivo que tenha 15 caracteres ou menos. Defina o nome do computador adicionando-o `/etc/hostname` usando o [YaST](https://www.suse.com/documentation/sles11/book_sle_admin/data/sec_basicnet_yast.html) ou [manualmente](https://www.suse.com/documentation/sled11/book_sle_admin/data/sec_basicnet_manconf.html).

    O exemplo a seguir mostra `/etc/hosts` com adições para dois nós chamados `SLES1` e `SLES2`.

    ```
    127.0.0.1   localhost
    10.128.18.128 SLES1
    10.128.16.77 SLES2
    ```

    > [!NOTE]
    > Todos os nós de cluster precisam conseguir acessar um ao outro via SSH. Ferramentas como hb_report ou crm_report (para solução de problemas) e Gerenciador de histórico do Hawk exigem acesso SSH sem senha entre os nós, caso contrário, eles podem apenas coletar dados do nó atual. Caso você use uma porta SSH não padrão, use a opção -X ([confira a página de manual](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_requirements_other.html)). Por exemplo, se a porta SSH é 3479, invoque um crm_report com:
    >
    >```bash
    >crm_report -X "-p 3479" [...]
    >```
    >Para obter mais informações, confira [o Guia de Administração].(https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.misc)

Na próxima seção, você configurará o armazenamento compartilhado e moverá os arquivos de banco de dados para esse armazenamento.  

## <a name="configure-shared-storage-and-move-database-files"></a>Configurar o armazenamento compartilhado e mover arquivos de banco de dados

Há uma variedade de soluções para fornecer armazenamento compartilhado. Este passo a passo demonstra como configurar o armazenamento compartilhado com o NFS. Recomendamos seguir as melhores práticas e usar o Kerberos para proteger o NFS: 

- [Como compartilhar sistemas de arquivos com o NFS](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#cha.nfs)

Se você não seguir essas diretrizes, qualquer pessoa que possa acessar sua rede e falsificar o endereço IP de um nó SQL poderá acessar seus arquivos de dados. Como sempre, verifique se você tem o modelo de risco do sistema antes de usá-lo em produção. 

Outra opção de armazenamento é usar o compartilhamento de arquivo SMB:

- [Seção sobre o Samba da documentação do SUSE](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#cha.samba)

### <a name="configure-an-nfs-server"></a>Configurar um servidor NFS

Para configurar um servidor NFS, confira as seguintes etapas na documentação do SUSE: [Como configurar o servidor NFS](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#sec.nfs.configuring-nfs-server).

### <a name="configure-all-cluster-nodes-to-connect-to-the-nfs-shared-storage"></a>Configurar todos os nós de cluster para se conectar ao armazenamento compartilhado do NFS

Antes de configurar o NFS do cliente para montar o caminho de arquivos de banco de dados do SQL Server para que ele aponte para a localização de armazenamento compartilhado, salve os arquivos de banco de dados em uma localização temporária para poder copiá-los posteriormente no compartilhamento:

1. **Somente no nó primário**, salve os arquivos de banco de dados em uma localização temporária. O script a seguir, cria um diretório temporário, copia os arquivos de banco de dados para o novo diretório e remove os arquivos de banco de dados antigos. Enquanto o SQL Server é executado como o usuário local mssql, você precisa verificar se, após a transferência de dados para o compartilhamento montado, o usuário local tem acesso de leitura/gravação ao compartilhamento. 

    ```bash
    su mssql
    mkdir /var/opt/mssql/tmp
    cp /var/opt/mssql/data/* /var/opt/mssql/tmp
    rm /var/opt/mssql/data/*
    exit
    ```

    Configure o cliente NFS em todos os nós de cluster:

    - [Como configurar clientes](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#sec.nfs.configuring-nfs-clients)

    > [!NOTE]
    > É recomendável seguir as melhores práticas e as recomendações do SUSE referentes ao armazenamento NFS altamente disponível: [Armazenamento NFS altamente disponível com o DRBD e o Pacemaker](https://www.suse.com/documentation/sle-ha-12/book_sleha_techguides/data/art_ha_quick_nfs.html).

2. Verifique se o SQL Server é iniciado com êxito com o novo caminho de arquivo. Faça isso em cada nó. Neste ponto, apenas um nó deve executar o SQL Server por vez. Eles não podem ser executados ao mesmo tempo, porque tentarão acessar os arquivos de dados simultaneamente (para evitar a inicialização acidental do SQL Server em ambos os nós, use um recurso de cluster do sistema de arquivos para garantir que o compartilhamento não seja montado duas vezes por nós diferentes). Os comandos a seguir iniciam o SQL Server, verificam o status e, em seguida, interrompem o SQL Server.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    sudo systemctl stop mssql-server
    ```

Neste ponto, ambas as instâncias do SQL Server são configuradas para serem executadas com os arquivos de banco de dados no armazenamento compartilhado. A próxima etapa é configurar o SQL Server para o Pacemaker. 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>Instalar e configurar o Pacemaker em cada nó de cluster

1. **Em ambos os nós de cluster, crie um arquivo para armazenar o nome de usuário do SQL Server e a senha para o logon do Pacemaker**. O comando a seguir cria e popula este arquivo:

    ```bash
    sudo touch /var/opt/mssql/secrets/passwd
    sudo echo '<loginName>' >> /var/opt/mssql/secrets/passwd
    sudo echo '<loginPassword>' >> /var/opt/mssql/secrets/passwd
    sudo chown root:root /var/opt/mssql/secrets/passwd 
    sudo chmod 600 /var/opt/mssql/secrets/passwd
    ```
2. **Todos os nós de cluster devem ser capazes de acessar um ao outro via SSH**. Ferramentas como hb_report ou crm_report (para solução de problemas) e Gerenciador de histórico do Hawk exigem acesso SSH sem senha entre os nós, caso contrário, eles podem apenas coletar dados do nó atual. No caso de você usar uma porta SSH não padrão, use a opção -X (consulte a página do manual). Por exemplo, se a porta SSH é 3479, invoque um hb_report com:

    ```bash
    crm_report -X "-p 3479" [...]
    ```

    Para obter mais informações, consulte [Requisitos de sistema e as recomendações na documentação do SUSE](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_requirements_other.html).

3. **Instalar a extensão de Alta Disponibilidade**. Para instalar a extensão, siga as etapas no tópico SUSE a seguir:
    
    [Início rápido de instalação e configuração](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html)

4. **Instalar o agente do recurso FCI para SQL Server**. Execute os seguintes comandos em ambos os nós:

    ```bash
    sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo
    sudo zypper --gpg-auto-import-keys refresh
    sudo zypper install mssql-server-ha
    ```

5. **Configure automaticamente o primeiro nó**. A próxima etapa é configurar um cluster de um nó em execução por meio da configuração do primeiro nó, SLES1. Siga as instruções no tópico SUSE, [Configurando o primeiro nó](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.1st-node).

    Quando terminar, verifique o status do cluster com `crm status`:
    ```bash
    crm status
    ```

    Ele deve mostrar que esse único nó, SLES1, está configurado.

6. **Adicionar nós a um cluster existente**. Em seguida, adicione o nó SLES2 ao cluster. Siga as instruções no tópico SUSE, [Adicionar o segundo nó](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.2nd-node).
    
    Quando terminar, verifique o status do cluster com **crm status**. Se você tiver adicionado um segundo nó, a saída será semelhante ao seguinte:
        
    ```
    2 nodes configured
    1 resource configured
    Online: [ SLES1 SLES2 ]
    Full list of resources:
    admin_addr     (ocf::heartbeat:IPaddr2):       Started SLES1
    ```

    > [!NOTE]
    > **admin_addr** é o recurso de cluster de IP virtual que é configurado durante a configuração do cluster inicial de um nó.

7.  **Procedimentos de remoção**. Se você precisar remover um nó do cluster, use o script de inicialização **ha-cluster-remove**. Para obter mais informações, consulte [visão geral dos Scripts de inicialização](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.bootstrap).  

## <a name="configure-the-cluster-resources-for-sql-server"></a>Configurar os recursos de cluster para o SQL Server

As etapas a seguir explicam como configurar o recurso de cluster para o SQL Server. Há duas configurações que você precisa personalizar.

- **Nome do Recurso do SQL Server**: Um nome para o recurso clusterizado do SQL Server. 
- **Valor de Tempo Limite**: O valor de tempo limite é o tempo que o cluster aguarda enquanto um recurso é colocado online. Para o SQL Server, esse é o tempo durante o qual você espera que o SQL Server coloque o banco de dados `master` online. 

Atualize os valores com base no script a seguir para o seu ambiente. Faça a execução em um nó para configurar e iniciar o serviço clusterizado.

```bash
sudo crm configure
primitive <sqlServerResourceName> ocf:mssql:fci op start timeout=<timeout_in_seconds>
colocation <constraintName> inf: <virtualIPResourceName> <sqlServerResourceName>
show
commit
exit
```

Por exemplo, o script a seguir cria um recurso clusterizado do SQL Server chamado mssqlha. 

```bash
sudo crm configure
primitive mssqlha ocf:mssql:fci op start timeout=60s
colocation admin_addr_mssqlha inf: admin_addr mssqlha
show
commit
exit
```

Depois que a configuração for confirmada, o SQL Server será iniciado no mesmo nó do recurso de IP virtual. 

Para obter mais informações, confira [Como configurar e gerenciar recursos de cluster (linha de comando)](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.manual_config). 

### <a name="verify-that-sql-server-is-started"></a>Verifique se o SQL Server foi iniciado. 

Para verificar se o SQL Server foi iniciado, execute o comando **crm status**:

```bash
crm status
```

Os exemplos a seguir mostram os resultados de quando o Pacemaker iniciou com êxito um recurso clusterizado. 
```
2 nodes configured
2 resources configured

Online: [ SLES1 SLES2 ]

Full list of resources:

 admin_addr     (ocf::heartbeat:IPaddr2):       Started SLES1
 mssqlha        (ocf::mssql:fci):       Started SLES1
```

## <a name="managing-cluster-resources"></a>Como gerenciar recursos de cluster

Para gerenciar os recursos de cluster, confira o seguinte tópico sobre o SUSE: [Como gerenciar recursos de cluster](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.config.crm )

### <a name="manual-failover"></a>Failover manual

Embora os recursos sejam configurados para fazer failover (ou migrar) automaticamente para outros nós do cluster no caso de uma falha de hardware ou de software, você também poderá mover manualmente um recurso para outro nó no cluster usando a GUI do Pacemaker ou a linha de comando. 

Use o comando migrate para essa tarefa. Por exemplo, para migrar o recurso SQL para um nó de cluster chamado SLES2, execute: 

```bash
crm resource
migrate mssqlha SLES2
```

## <a name="additional-resources"></a>Recursos adicionais

[Extensão de Alta Disponibilidade do SUSE Linux Enterprise – Guia de Administração](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html) 
