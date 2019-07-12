---
title: Configurar o cluster de disco compartilhado de SLES para SQL Server
description: Implementar a alta disponibilidade por meio da configuração de cluster de disco compartilhado do SUSE Linux Enterprise Server (SLES) para o SQL Server.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
manager: jroth
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: e5ad1bdd-c054-4999-a5aa-00e74770b481
ms.openlocfilehash: 0b65c2cca781dc077e72ff06fb7de5ae8ee2e8c5
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834651"
---
# <a name="configure-sles-shared-disk-cluster-for-sql-server"></a>Configurar o cluster de disco compartilhado de SLES para SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este guia fornece instruções para criar um cluster de disco compartilhado de dois nós para o SQL Server no SUSE Linux Enterprise Server (SLES). A camada de clustering é baseada no SUSE [alta disponibilidade de extensão (HAE)](https://www.suse.com/products/highavailability) criado na parte superior da [Pacemaker](https://clusterlabs.org/). 

Para obter mais informações sobre a configuração de cluster, opções de recurso do agente, gerenciamento, as práticas recomendadas e recomendações, consulte [SUSE Linux Enterprise alta disponibilidade extensão 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html).

## <a name="prerequisites"></a>Pré-requisitos

Para concluir o seguinte cenário de ponta a ponta, você precisa de duas máquinas para implantar o cluster de dois nós e outro servidor para configurar o compartilhamento NFS. As etapas a seguir descrevem como esses servidores serão configurados.

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>Instalar e configurar o sistema operacional em cada nó de cluster

A primeira etapa é configurar o sistema operacional em nós de cluster. Para este passo a passo, use SLES com uma assinatura válida para o complemento de alta disponibilidade.

## <a name="install-and-configure-sql-server-on-each-cluster-node"></a>Instalar e configurar o SQL Server em cada nó de cluster

1. Instalar e configurar o SQL Server em ambos os nós. Para obter instruções detalhadas, consulte [instalar o SQL Server no Linux](sql-server-linux-setup.md).
2. Designe um nó como primário e o outro como secundário, para fins de configuração. Usar esses termos para os seguintes itens neste guia. 
3. No nó secundário, interrompa e desabilite o SQL Server. O exemplo a seguir interrompe e desabilita o SQL Server:

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl disable mssql-server
    ```

    > [!NOTE]
    > No momento da instalação, uma chave mestra do servidor é gerado para a instância do SQL Server e colocado no `/var/opt/mssql/secrets/machine-key`. No Linux, SQL Server sempre é executado como uma conta local chamada mssql. Porque é uma conta local, sua identidade não é compartilhada entre os nós. Portanto, você precisará copiar a chave de criptografia do nó principal para cada nó secundário, portanto, cada conta mssql local pode acessá-lo para descriptografar a chave mestra do servidor.
4. No nó primário, crie um logon do SQL server para Pacemaker e conceder a permissão de logon para executar `sp_server_diagnostics`. O pacemaker usa essa conta para verificar qual nó está executando o SQL Server.

    ```bash
    sudo systemctl start mssql-server
    ```
    Conectar-se para o banco de dados mestre do SQL Server com a conta 'sa' e execute o seguinte:

    ```sql
    USE [master]
    GO
    CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'
    GRANT VIEW SERVER STATE TO <loginName>
    ```
5. No nó primário, interrompa e desabilite o SQL Server.
6. Siga as instruções [na documentação do SUSE](https://www.suse.com/documentation/sles11/book_sle_admin/data/sec_basicnet_yast.html) para configurar e atualizar o arquivo de hosts para cada nó do cluster. O arquivo de 'host' deve incluir o endereço IP e o nome de cada nó do cluster.

    Para verificar o endereço IP do nó atual executar:

    ```bash
    sudo ip addr show
    ```

    Defina o nome do computador em cada nó. Dê a cada nó de um nome exclusivo que é de 15 caracteres ou menos. Definir o nome do computador, adicionando-o para `/etc/hostname` usando [yast](https://www.suse.com/documentation/sles11/book_sle_admin/data/sec_basicnet_yast.html) ou [manualmente](https://www.suse.com/documentation/sled11/book_sle_admin/data/sec_basicnet_manconf.html).

    A exemplo a seguir mostra `/etc/hosts` com adições para dois nós denominados `SLES1` e `SLES2`.

    ```
    127.0.0.1   localhost
    10.128.18.128 SLES1
    10.128.16.77 SLES2
    ```

    > [!NOTE]
    > Todos os nós de cluster devem ser capazes de acessar um ao outro via SSH. Ferramentas como hb_report ou crm_report (para solução de problemas) e Gerenciador de histórico do Hawk exigem acesso SSH sem senha entre os nós, caso contrário, eles podem apenas coletar dados do nó atual. No caso de você usar uma porta SSH não padrão, use a opção -X ([consulte a página do manual](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_requirements_other.html)). Por exemplo, se a porta SSH é 3479, invoque um crm_report com:
    >
    >```bash
    >crm_report -X "-p 3479" [...]
    >```
    >Para obter mais informações, consulte o [guia de administração]. (https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.misc)

Na próxima seção, você irá configurar o armazenamento compartilhado e mover os arquivos de banco de dados para que o armazenamento.  

## <a name="configure-shared-storage-and-move-database-files"></a>Configurar o armazenamento compartilhado e mover arquivos de banco de dados

Há uma variedade de soluções que fornecem armazenamento compartilhado. Este passo a passo demonstra como configurar o armazenamento compartilhado com NFS. É recomendável seguir as práticas recomendadas e usar o Kerberos para proteger o NFS: 

- [Compartilhamento de sistemas de arquivos com o NFS](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#cha.nfs)

Se você não seguir essas diretrizes, qualquer pessoa que possa acessar sua rede e falsificar o endereço IP de um nó do SQL será capaz de acessar seus arquivos de dados. Como sempre, certifique-se de modelo de risco você em seu sistema antes de usá-lo em produção. 

Outra opção de armazenamento é usar o compartilhamento de arquivos SMB:

- [Seção do Samba da documentação do SUSE](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#cha.samba)

### <a name="configure-an-nfs-server"></a>Configurar um servidor NFS

Para configurar um servidor NFS, consulte as etapas a seguir na documentação do SUSE: [Configurando o servidor NFS](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#sec.nfs.configuring-nfs-server).

### <a name="configure-all-cluster-nodes-to-connect-to-the-nfs-shared-storage"></a>Configurar todos os nós de cluster para se conectar ao armazenamento compartilhado NFS

Antes de configurar o cliente NFS para montar o caminho de arquivos de banco de dados do SQL Server para apontar para o local de armazenamento compartilhado, certifique-se de que salvar os arquivos de banco de dados para um local temporário para poder copiá-los posteriormente o compartilhamento:

1. **No nó primário**, salvar os arquivos de banco de dados em um local temporário. O script a seguir cria um novo diretório temporário, copia os arquivos de banco de dados para o novo diretório e remove os arquivos antigos do banco de dados. Como o SQL Server é executado como usuário local mssql, você precisa certificar-se de que, após a transferência de dados para o compartilhamento montado, usuário local tem acesso de leitura / gravação ao compartilhamento. 

    ```bash
    su mssql
    mkdir /var/opt/mssql/tmp
    cp /var/opt/mssql/data/* /var/opt/mssql/tmp
    rm /var/opt/mssql/data/*
    exit
    ```

    Configure o cliente NFS em todos os nós de cluster:

    - [Configuração de clientes](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#sec.nfs.configuring-nfs-clients)

    > [!NOTE]
    > É recomendável seguir as práticas recomendadas e recomendações sobre armazenamento altamente disponível NFS do SUSE: [Armazenamento NFS altamente disponível com DRBD e Pacemaker](https://www.suse.com/documentation/sle-ha-12/book_sleha_techguides/data/art_ha_quick_nfs.html).

2. Valide que SQL Server é iniciado com êxito com o novo caminho de arquivo. Faça isso em cada nó. No momento apenas um nó deve executar o SQL Server por vez. Eles não podem ambos executados ao mesmo tempo porque eles ambos tentará acessar os arquivos de dados simultaneamente (para evitar acidentalmente iniciando o SQL Server em ambos os nós, use um recurso de cluster do sistema de arquivos para garantir que o compartilhamento não está montado duas vezes por nós diferentes). Os comandos a seguir iniciar o SQL Server, verificam o status e, em seguida, interrompa o SQL Server.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    sudo systemctl stop mssql-server
    ```

Neste ponto, ambas as instâncias do SQL Server são configuradas para executar com os arquivos de banco de dados no armazenamento compartilhado. A próxima etapa é configurar o SQL Server para Pacemaker. 

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

- **Nome de recurso do SQL Server**: Um nome para o recurso clusterizado do SQL Server. 
- **Valor de tempo limite**: O valor de tempo limite é a quantidade de tempo que o cluster espera enquanto um recurso é colocado online. Para o SQL Server, isso é a hora em que você espera que o SQL Server para trazer o `master` banco de dados online. 

Atualize os valores do script a seguir para o seu ambiente. Execute em um nó para configurar e iniciar o serviço clusterizado.

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

Depois que a configuração for confirmada, o SQL Server for iniciado no mesmo nó que o recurso IP virtual. 

Para obter mais informações, consulte [Configurando e gerenciando recursos de Cluster (linha de comando)](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.manual_config). 

### <a name="verify-that-sql-server-is-started"></a>Verifique se o SQL Server é iniciado. 

Para verificar se o SQL Server foi iniciado, execute as **crm status** comando:

```bash
crm status
```

Os exemplos a seguir mostra os resultados quando o Pacemaker foi iniciado com êxito como recurso de cluster. 
```
2 nodes configured
2 resources configured

Online: [ SLES1 SLES2 ]

Full list of resources:

 admin_addr     (ocf::heartbeat:IPaddr2):       Started SLES1
 mssqlha        (ocf::mssql:fci):       Started SLES1
```

## <a name="managing-cluster-resources"></a>Gerenciar recursos de cluster

Para gerenciar os recursos de cluster, consulte o tópico SUSE a seguir: [Gerenciar recursos de Cluster](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.config.crm )

### <a name="manual-failover"></a>failover manual

Embora os recursos são configurados para failover automaticamente (ou migrar) para outros nós do cluster em caso de falha de hardware ou software, você pode mover um recurso manualmente para outro nó no cluster usando a GUI do Pacemaker ou a linha de comando . 

Use o comando de migração para esta tarefa. Por exemplo, para migrar do recurso SQL em nomes de nó de cluster SLES2 executar: 

```bash
crm resource
migrate mssqlha SLES2
```

## <a name="additional-resources"></a>Recursos adicionais

[Extensão de alta disponibilidade do SUSE Linux Enterprise - guia de administração](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html) 
