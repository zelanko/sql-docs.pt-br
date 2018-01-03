---
title: Atualizado - SQL Server no Linux documentos | Microsoft Docs
description: "Trechos de código de exibição de conteúdo atualizado para alterados recentemente na documentação, para o Microsoft SQL Server no Linux."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: rothja
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: linux-sql
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 12/02/2017
ms.author: genemi
ms.openlocfilehash: 030f30580b0ddb02da2a67990d0c58acf15236c9
ms.sourcegitcommit: 73043fe1ac5d60b67e33b44053c0a7733b98bc3d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/23/2017
---
# <a name="new-and-recently-updated-sql-server-on-linux-docs"></a>Novos e recentemente atualizado: SQL Server no Linux docs



Quase todos os dias a Microsoft atualiza alguns de seus artigos existentes no site de documentação [Docs.Microsoft.com](http://docs.microsoft.com/). Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é reexecutado periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita ou como markdown do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de datas e o assunto a seguir:



- *Intervalo de datas das atualizações:* &nbsp; **28-09-2017** &nbsp; a &nbsp; **02-12-2017**
- *Área de assunto:* &nbsp; **Microsoft SQL Server no Linux**.




&nbsp;

## <a name="new-articles-created-recently"></a>Novos artigos criados recentemente

Os links a seguir direcionam para novos artigos que foram adicionados recentemente.


1. [Executar o SQL Server 2017 na nuvem](quickstart-install-connect-clouds.md)
2. [Repositórios de alteração do repositório de visualização no repositório de GA](sql-server-linux-change-repo.md)
3. [Práticas recomendadas e diretrizes de configuração para 2017 do SQL Server no Linux](sql-server-linux-performance-best-practices.md)
4. [Instâncias de Cluster de failover - SQL Server no Linux](sql-server-linux-shared-disk-cluster-concepts.md)
5. [Configurar a instância de cluster de failover - iSCSI – SQL Server no Linux](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
6. [Configurar a instância de cluster de failover - NFS - SQL Server no Linux](sql-server-linux-shared-disk-cluster-configure-nfs.md)
7. [Configurar a instância de cluster de failover - SMB - SQL Server no Linux](sql-server-linux-shared-disk-cluster-configure-smb.md)
8. [Operar a instância de cluster de failover - SQL Server no Linux](sql-server-linux-shared-disk-cluster-operate.md)
9. [Limitações e problemas conhecidos do SSIS no Linux](sql-server-linux-ssis-known-issues.md)
10. [Restaurar um banco de dados do SQL Server em um contêiner do Docker do Linux](tutorial-restore-backup-in-sql-server-container.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados de artigos que passaram por uma atualização extensa recentemente.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes um trecho é separado da sintaxe de markdown importante que circunda no artigo real. Portanto, esses trechos servem apenas como orientações gerais. Os trechos só mostram a você se vale a pena clicar e visitar o artigo real conforme seus interesses.

Por essas e outras razões, não copie o código desses trechos, nem considere-os como verdade exata. Em vez disso, visite o artigo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compacta fornece links para todos os artigos atualizados listados na seção Trechos.

1. [Executar a imagem de contêiner de 2017 do SQL Server com o Docker](#TitleNum_1)
2. [Configurar o grupo de disponibilidade do AlwaysOn para SQL Server no Linux](#TitleNum_2)
3. [Alta disponibilidade e proteção de dados para as configurações de grupo de disponibilidade](#TitleNum_3)
4. [Configurar imagens de contêiner de 2017 do SQL Server no Docker](#TitleNum_4)
5. [Criptografar conexões ao SQL Server no Linux](#TitleNum_5)
6. [Criar e executar trabalhos do SQL Server Agent no Linux](#TitleNum_6)
7. [Orientação de instalação do SQL Server no Linux](#TitleNum_7)
8. [Configurar a instância de cluster de failover - SQL Server no Linux (RHEL)](#TitleNum_8)
9. [Solucionar problemas do SQL Server no Linux](#TitleNum_9)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-run-the-sql-server-2017-container-image-with-dockerquickstart-install-connect-dockermd"></a>1. &nbsp;[Executar a imagem de contêiner de 2017 do SQL Server com o Docker](quickstart-install-connect-docker.md)

*Atualizado: 30-11-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Próximo](#TitleNum_2))

<!-- Source markdown line 261.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 2aaf953c2f1fb675b1304186108fbef1eebf6f8f f7cd42bb320a8892a5ec63ce999186438097636a  (PR=4150  ,  Filename=quickstart-install-connect-docker.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



**Remover o contêiner**


Se você quiser remover o contêiner do SQL Server usado neste tutorial, execute os seguintes comandos:

```
sudo docker stop sql1
sudo docker rm sql1
```

```
docker stop sql1
docker rm sql1
```

> [!WARNING]
> Parando e removendo um contêiner permanentemente exclui todos os dados do SQL Server no contêiner. Se você precisar preservar os dados, [criar e copiar um arquivo de backup fora do container--tutorial-restore-backup-in-sql-server-container.md) ou use uma [contêiner persistência de dados technique--sql-server-linux-configure-docker.md#persist).




&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-configure-always-on-availability-group-for-sql-server-on-linuxsql-server-linux-availability-group-configure-hamd"></a>2. &nbsp;[Configurar sempre no grupo de disponibilidade para o SQL Server no Linux](sql-server-linux-availability-group-configure-ha.md)

*Atualizado em: 2017-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_1) | [próxima](#TitleNum_3))

<!-- Source markdown line 129.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 3c7e6bc862e5b062a855918efbeee5fe748b7236 6900c9a30ce04ce54e7aaa270ef7d276c18f9afd  (PR=4150  ,  Filename=sql-server-linux-availability-group-configure-ha.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



- Crie grupo de disponibilidade com duas réplicas síncronas e uma réplica de configuração:

   >[!IMPORTANT]
   >Essa arquitetura permite que qualquer edição do SQL Server para hospedar a réplica de terceira. Por exemplo, a terceira réplica pode ser hospedada no SQL Server Enterprise Edition. Na Enterprise Edition, é o tipo de ponto de extremidade válido apenas `WITNESS`.

```sql
   CREATE AVAILABILITY GROUP [ag1]
      WITH (CLUSTER_TYPE = EXTERNAL)
      FOR REPLICA ON
       N'**<node1>**' WITH (
          ENDPOINT_URL = N'tcp://**<node1>**:**<5022>**',
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
          FAILOVER_MODE = EXTERNAL,
          SEEDING_MODE = AUTOMATIC
          ),
       N'**<node2>**' WITH (
          ENDPOINT_URL = N'tcp://**<node2>**:**<5022>**',
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
          FAILOVER_MODE = EXTERNAL,
          SEEDING_MODE = AUTOMATIC
          ),
       N'**<node3>**' WITH (
          ENDPOINT_URL = N'tcp://**<node3>**:**<5022>**',
          AVAILABILITY_MODE = CONFIGURATION_ONLY
          );
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-high-availability-and-data-protection-for-availability-group-configurationssql-server-linux-availability-group-hamd"></a>3. &nbsp;[Alta disponibilidade e proteção de dados para as configurações de grupo de disponibilidade](sql-server-linux-availability-group-ha.md)

*Atualizado em: 2017-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_2) | [próxima](#TitleNum_4))

<!-- Source markdown line 106.  ms.author= "mikeray".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 e6bee794ce19f1ed62298b4a0cce7207550f1595 b64726cd6e91721850721786d26c170d59fc320a  (PR=4150  ,  Filename=sql-server-linux-availability-group-ha.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



O valor padrão para `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` é 0. A tabela a seguir descreve o comportamento de disponibilidade.

| |Alta disponibilidade & </br> Proteção de dados | Proteção de dados
|:---|---|---
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>*</sup>|1
|Interrupção principal | Failover automático. Novo primário é R / w. | Failover automático. Novo primário não está disponível para transações de usuário.
|Interrupção de réplica secundária | Primário está R/W, em execução exposto a perda de dados (se o principal falha e não pode ser recuperado). Nenhum failover automático se primário falha também. | Primário não está disponível para transações de usuário. Nenhuma réplica façam failover para se primário falha também.
|Interrupção de réplica apenas de configuração | É primário R / w. Nenhum failover automático se primário falha também. | É primário R / w. Nenhum failover automático se primário falha também.
|Secundário síncrono + configuração somente paralisação de réplica| Primário não está disponível para transações de usuário. Nenhum failover automático. | Primário não está disponível para transações de usuário. Nenhuma réplica para failover para se primário falha também.
<sup>*</sup>Padrão

>[!NOTE]
>A instância do SQL Server que hospeda a réplica apenas de configuração também pode hospedar outros bancos de dados. Ele também pode participar como um banco de dados somente de configuração para mais de um grupo de disponibilidade.

**Requisitos**


* Todas as réplicas de um grupo de disponibilidade com uma única réplica de configuração devem ser SQL Server 2017 atualização Cumulativa 1 ou posterior.
* Qualquer edição do SQL Server pode hospedar uma réplica apenas de configuração, incluindo o SQL Server Express.
* O grupo de disponibilidade precisa de pelo menos uma réplica secundária - além da réplica primária.
* Réplicas somente de configuração não são considerados o número máximo de réplicas por instância do SQL Server. SQL Server standard edition permite até três réplicas, SQL Server Enterprise Edition permite até 9.



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-configure-sql-server-2017-container-images-on-dockersql-server-linux-configure-dockermd"></a>4. &nbsp;[Imagens de contêiner de configurar o SQL Server 2017 no Docker](sql-server-linux-configure-docker.md)

*Atualizado em: 2017-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_3) | [próxima](#TitleNum_5))

<!-- Source markdown line 34.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c759fb88ae8d654414202f28c5fc58dfd02581bf fd270118f2f4608fceaf563fc143951b41097bdb  (PR=4150  ,  Filename=sql-server-linux-configure-docker.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



Este tópico de configuração fornece cenários de uso adicionais nas seções a seguir.

**<a id="production"></a>Executar produção imagens de contêiner**


Início rápido na seção anterior é executada a edição gratuita do desenvolvedor do SQL Server do Hub do Docker. A maioria das informações ainda se aplica se você deseja executar imagens de contêiner, como as edições Enterprise, Standard ou Web de produção. No entanto, há algumas diferenças são descritas aqui.

- Você só pode usar SQL Server em um ambiente de produção se você tiver uma licença válida. Você pode obter uma licença de produção do SQL Server Express gratuita [aqui](https://go.microsoft.com/fwlink/?linkid=857693). SQL Server Standard e Enterprise Edition licenças estão disponíveis por meio de [Microsoft Volume Licensing](https://www.microsoft.com/Licensing/licensing-programs/licensing-programs.aspx).

- Imagens de contêiner do SQL Server de produção devem ser extraídas de [Docker repositório](https://store.docker.com). Se você ainda não tiver um, crie uma conta no repositório do Docker.

- A imagem de contêiner de desenvolvedor no repositório do Docker pode ser configurada para executar edições produção. Use as etapas a seguir para executar edições de produção:

   1. Primeiro, faça logon sua id de docker da linha de comando.

```
      docker login
```

   1. Em seguida, você precisa obter o desenvolvedor livre imagem de contêiner no armazenamento do Docker. Vá para [https://store.docker.com/images/mssql-server-linux](https://store.docker.com/images/mssql-server-linux), clique em **prosseguir para a conclusão**e siga as instruções.

   1. Examine os requisitos e executar procedimentos em [início rápido – guia de início rápido-install-conectar-se-docker.md). Mas há duas diferenças. Você deve receber a imagem **repositório/microsoft/mssql-server-linux:\<nome da marca\>**  de armazenamento do Docker. E você deve especificar a edição de produção com o **MSSQL_PID** variável de ambiente. O exemplo a seguir mostra como executar a imagem de contêiner de 2017 do SQL Server mais recente para o Enterprise Edition:



&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-encrypting-connections-to-sql-server-on-linuxsql-server-linux-encrypted-connectionsmd"></a>5. &nbsp;[Criptografar conexões ao SQL Server no Linux](sql-server-linux-encrypted-connections.md)

*Atualizado em: 2017-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_4) | [próxima](#TitleNum_6))

<!-- Source markdown line 45.  ms.author= meetb;rickbyh.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 7e3187866df060903e30000d60d673edad46d210 bcb1f2771e6c29b535a30b9f23ac296954509187  (PR=4150  ,  Filename=sql-server-linux-encrypted-connections.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



        sudo chown mssql:mssql mssql.pem mssql.key
        sudo chmod 600 mssql.pem mssql.key
        sudo mv mssql.pem /etc/ssl/certs/
        sudo mv mssql.key /etc/ssl/private/

- **Configurar o SQL Server**

        systemctl stop mssql-server
        cat /var/opt/mssql/mssql.conf
        sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssqlfqdn.pem
        sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssqlfqdn.key
        sudo /opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2
        sudo /opt/mssql/bin/mssql-conf set network.forceencryption 0

- **Registrar o certificado do computador cliente (Windows, Linux ou macOS)**

    -   Se você estiver usando o certificado de autoridade de certificação assinado, você precisa copiar o certificado de autoridade de certificação (CA) em vez do certificado de usuário no computador cliente.
    -   Se você estiver usando o certificado autoassinado apenas copiar o arquivo. PEM para as seguintes pastas do respectivas para distribuição e executar os comandos para habilitá-las

        - **Windows**: importar o arquivo. PEM como um certificado de usuário atual -> confiável autoridades de certificação raiz -> certificados
        - **macOS**:

-   **Cadeias de conexão de exemplo**

    - **..! NCLUIR-NotShown - ssmanstudiofull-md-... /Includes/ssManStudioFull-MD.MD)]** ! [ SSMS conexão dialog--media/sql-server-linux-encrypted-connections/ssms-encrypt-connection.png "SSMS conexão caixa de diálogo")



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-create-and-run-sql-server-agent-jobs-on-linuxsql-server-linux-run-sql-server-agent-jobmd"></a>6. &nbsp;[Criar e executados trabalhos do SQL Server Agent no Linux](sql-server-linux-run-sql-server-agent-job.md)

*Atualizado em: 2017-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_5) | [próxima](#TitleNum_7))

<!-- Source markdown line 35.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1598129bb5f98434435d8ad02336a9adf76c7870 6fe3fe7df3a60dbac31f1df59aac9860d293421a  (PR=4150  ,  Filename=sql-server-linux-run-sql-server-agent-job.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



Os seguintes pré-requisitos são necessários para concluir este tutorial:

* Computador Linux com os seguintes pré-requisitos:
  * SQL Server 2017 ([RHEL--quickstart-install-connect-red-hat.md), [SLES - quickstart-install-conectar-se-suse.md), ou [Ubuntu - quickstart-install-conectar-se-ubuntu.md)) com as ferramentas de linha de comando.

Os seguintes pré-requisitos são opcionais:

* Computador Windows com o SSMS:
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) para etapas opcionais de SSMS.

**Instalar o SQL Server Agent**


Para usar o SQL Server Agent no Linux, você deve primeiro instalar o **mssql-server-agente** pacote em um computador que já tenha instalado de 2017 do SQL Server.

1. Instalar **mssql-server-agente** com o comando apropriado para seu sistema operacional Linux.

   | Plataforma | Comando de instalação |
   |-----|-----|
   | RHEL | `sudo yum install mssql-server-agent` |
   | SLES | `sudo zypper refresh`<br/>`sudo zypper update mssql-server-agent` |
   | Ubuntu | `sudo apt-get update`<br/>`sudo apt-get install mssql-server-agent` |

1. Reinicie o SQL Server com o seguinte comando:

```
   sudo systemctl restart mssql-server
```

**Criar um banco de dados de exemplo**


Use as seguintes etapas para criar um banco de dados de exemplo chamado **SampleDB**. Este banco de dados é usado para o trabalho de backup diário.

1. No computador Linux, abra uma sessão de terminal bash.



&nbsp;

&nbsp;

---

<a name="TitleNum_7"/>

### <a name="7-nbsp-installation-guidance-for-sql-server-on-linuxsql-server-linux-setupmd"></a>7. &nbsp;[Orientação de instalação do SQL Server no Linux](sql-server-linux-setup.md)

*Atualizado em: 2017-12-01* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_6) | [próxima](#TitleNum_8))

<!-- Source markdown line 125.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 8ba2bf6f9cf4b5f54a6ee0f4d16d4437d5724880 eedddcfb64c6432215f56b74dc91700d9804fce8  (PR=4160  ,  Filename=sql-server-linux-setup.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=085dd05d56afecbb454206ed8402cfbaa597cfbe) -->



**<a id="repositories"></a>Configurar repositórios de origem**


Quando você instala ou atualiza o SQL Server, você obter a versão mais recente do SQL Server do seu repositório Microsoft configurado.

**Opções do repositório**


Há dois tipos principais de repositórios para cada distribuição:

- **Atualizações cumulativas (CU)**: repositório de atualização a cumulativa (CU) contém os pacotes para a versão do SQL Server base e correções de bugs ou melhorias desde a versão. Atualizações cumulativas são específicas para uma versão de lançamento, como SQL Server 2017. Elas são lançadas em um ritmo regular.

- **GDR**: repositório o GDR contém os pacotes para a versão de base do SQL Server e somente correções críticas e atualizações de segurança desde a versão. Essas atualizações também são adicionadas para a próxima versão de atualizações Cumulativas.

Cada versão de atualização Cumulativa e GDR contém o pacote completo do SQL Server e todas as atualizações anteriores para esse repositório. Há suporte à atualização de uma versão GDR para uma versão CU alterando seu repositório configurado para o SQL Server. Você também pode [downgrade – #rollback) para qualquer versão dentro de sua versão principal (ex: 2017). Atualizando uma atualização cumulativa versão para uma versão GDR não tem suporte.

**Verifique seu repositório configurado**


Se você quiser verificar o repositório está configurado, use as seguintes técnicas dependente de plataforma.

| Plataforma | Procedimento |
|-----|-----|
| RHEL | 1. Exibir os arquivos de **/etc/yum.repos.d** diretório:`sudo ls /etc/yum.repos.d`<br/>2. Procure um arquivo que define o diretório do SQL Server, como **server.repo mssql**.<br/>3. Imprima o conteúdo do arquivo:`sudo cat /etc/yum.repos.d/mssql-server.repo`<br/>4. O **nome** propriedade é o repositório configurado.|
| SLES | 1. Execute o seguinte comando:`sudo zypper info mssql-server`<br/>2. O **repositório** propriedade é o repositório configurado. |
| Ubuntu | 1. Execute o seguinte comando:`sudo cat /etc/apt/sources.list`<br/>2. Examine a URL do pacote para o servidor mssql. |



&nbsp;

&nbsp;

---

<a name="TitleNum_8"/>

### <a name="8-nbsp-configure-failover-cluster-instance---sql-server-on-linux-rhelsql-server-linux-shared-disk-cluster-configuremd"></a>8. &nbsp;[Configurar instância de cluster de failover - SQL Server no Linux (RHEL)](sql-server-linux-shared-disk-cluster-configure.md)

*Atualizado em: 2017-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_7) | [próxima](#TitleNum_9))

<!-- Source markdown line 25.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 308fa1809c80a009f7f15b5ca6917f6b76588c3e 71f18baa320041ff10c94e8c7668e40dff45cac3  (PR=4150  ,  Filename=sql-server-linux-shared-disk-cluster-configure.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



> [!div class="checklist"]
> * Instalar e configurar o Linux
> * Instalar e configurar o SQL Server
> * Configurar o arquivo de hosts
> * Configurar o armazenamento compartilhado e mover os arquivos de banco de dados
> * Instalar e configurar Pacemaker em cada nó de cluster
> * Configurar a instância de cluster de failover

Este artigo explica como criar uma instância de cluster de failover do disco compartilhado de dois nós (FCI) do SQL Server. O artigo inclui instruções e exemplos de script para o Red Hat Enterprise Linux (RHEL). Ubuntu distribuições são semelhantes às RHEL para os exemplos de script serão normalmente também funcionam no Ubuntu.

Para obter informações conceituais, consulte [SQL Server Failover Cluster FCI (instância) em Linux--sql-server-linux-shared-disk-cluster-concepts.md).

**Pré-requisitos**


Para concluir o cenário de ponta a ponta abaixo, você precisa duas máquinas para implantar o cluster de dois nós e outro servidor para o armazenamento. Etapas a seguir descrevem como esses servidores serão configurados.

**Instalar e configurar o Linux**


A primeira etapa é configurar o sistema operacional em nós de cluster. Em cada nó no cluster, configure uma distribuição de linux. Use a distribuição e a versão mesmo em ambos os nós. Use um ou outro as distribuições a seguir:

* RHEL com uma assinatura válida para o complemento HA

**Instalar e configurar o SQL Server**


1. Instalar e configurar o SQL Server em ambos os nós.  Para obter instruções detalhadas, consulte [instalar o SQL Server no Linux – sql server-linux setup.md).
1. Designe um nó como primário e o outro como secundário, para fins de configuração. Usar essas condições para o seguinte neste guia.
1. No nó secundário, interromper e desabilitar o SQL Server.
    O exemplo a seguir para e desabilita o SQL Server:
```
    sudo systemctl stop mssql-server
    sudo systemctl disable mssql-server
```

    > [!NOTE]
    > At set up time, a Server Master Key is generated for the SQL Server instance and placed at `var/opt/mssql/secrets/machine-key`. On Linux, SQL Server always runs as a local account called mssql. Because it's a local account, its identity isn't shared across nodes. Therefore, you need to copy the encryption key from primary node to each secondary node so each local mssql account can access it to decrypt the Server Master Key.



&nbsp;

&nbsp;

---

<a name="TitleNum_9"/>

### <a name="9-nbsp-troubleshoot-sql-server-on-linuxsql-server-linux-troubleshooting-guidemd"></a>9. &nbsp;[Solucionar problemas do SQL Server no Linux](sql-server-linux-troubleshooting-guide.md)

*Atualizado: 30-11-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_8))

<!-- Source markdown line 125.  ms.author= anshrest.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5f8557a34b38e028ff6e5ac370b6d2d6bf315091 196e56187b57bdd79cc5cdc5e6fce3d41e82af0c  (PR=4150  ,  Filename=sql-server-linux-troubleshooting-guide.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



**Inicie o SQL Server em uma configuração mínima ou em modo de usuário único**


**Inicie o SQL Server no modo de configuração mínima**

Isso será útil se a definição de um valor de configuração (por exemplo, sobrecarga de confirmação de memória) impediu o servidor de ser iniciado.

```
   sudo -u mssql /opt/mssql/bin/sqlservr -f
```

**Inicie o SQL Server no modo de usuário único**

Em determinadas circunstâncias, pode ser necessário iniciar uma instância do SQL Server no modo de usuário único usando o opção de inicialização -m. Por exemplo, você pode querer mudar as opções de configuração de servidor ou recuperar um banco de dados mestre danificado ou outro banco de dados do sistema. Por exemplo, você talvez queira alterar as opções de configuração de servidor ou recuperar um banco de dados mestre danificado ou outro banco de dados do sistema

Inicie o SQL Server no modo de usuário único
```
   sudo -u mssql /opt/mssql/bin/sqlservr -m
```

Inicie o SQL Server no modo de usuário único com SQLCMD
```
   sudo -u mssql /opt/mssql/bin/sqlservr -m SQLCMD
```

> [!WARNING]
>  Inicie o SQL Server no Linux com o usuário “mssql” para evitar problemas futuros de inicialização. Exemplo: “sudo -u mssql /opt/mssql/bin/sqlservr [STARTUP OPTIONS]”

Se você acidentalmente iniciou do SQL Server com outro usuário, você precisará alterar a propriedade de arquivos de banco de dados do SQL Server para o usuário 'mssql' antes de iniciar o SQL Server com systemd. Por exemplo, para alterar a propriedade de todos os arquivos de banco de dados em /var/opt/mssql para o usuário 'mssql', execute o seguinte comando

```
   chown -R mssql:mssql /var/opt/mssql/
```







## <a name="similar-articles"></a>Artigos Semelhantes

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
    2017-12-02  23:00pm
-->

Esta seção lista artigos muito semelhantes a artigos atualizados recentemente em outras áreas de assunto, em nosso repositório público GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Áreas de assunto que têm artigos novos ou atualizados recentemente

- [Novo + Atualizado (3 + 14): documentos sobre **Análise Avançada para SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [Novo + atualizado (1 + 0): documentos do **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Novo + Atualizado (87 + 0): documentos sobre **Sistema de Plataforma Analítica para SQL**](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Novo + Atualizado (5 + 4): documentos sobre **Conexão ao SQL**](../connect/new-updated-connect.md)
- [Novo + Atualizado (0 + 1): documentos sobre o **Mecanismo de Banco de Dados para SQL**](../database-engine/new-updated-database-engine.md)
- [Novo + Atualizado (2 + 2): documentos sobre **Integration Services para SQL**](../integration-services/new-updated-integration-services.md)
- [Novo + Atualizado (10 + 9): documentos sobre **Linux para SQL**](../linux/new-updated-linux.md)
- [Novo + Atualizado (2 + 4): documentos sobre **Bancos de Dados Relacionais para SQL**](../relational-databases/new-updated-relational-databases.md)
- [Novo + Atualizado (4 + 2): documentos sobre o **Reporting Services para SQL**](../reporting-services/new-updated-reporting-services.md)
- [Novo + Atualizado (0 + 1): documentos de **Exemplos para SQL**](../sample/new-updated-sample.md)
- [Novo + Atualizado (21 + 0): documentos sobre o **SQL Operations Studio**](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Novo + Atualizado (5 + 1): documentos do **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [Novo + atualizado (0 + 1): documentos do **SSDT (SQL Server Data Tools)**](../ssdt/new-updated-ssdt.md)
- [Novo + Atualizado (1 + 0): documentos sobre o **SSMA (SQL Server Migration Assistant)**](../ssma/new-updated-ssma.md)
- [Novo + atualizado (0 + 1): documentos do **SSMS (SQL Server Management Studio)**](../ssms/new-updated-ssms.md)
- [Novo + Atualizado (0 + 2): documentos sobre o **Transact-SQL**](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Áreas de assunto que não têm nenhum artigo novo ou atualizado recentemente

- [Novo + Atualizado (0 + 0): documentos sobre **DMA (Assistente de Migração de Dados) para o SQL**](../dma/new-updated-dma.md)
- [Novo + atualizado (0 + 0): documentos do **ADO (ActiveX Data Objects) para SQL**](../ado/new-updated-ado.md)
- [Novo + atualizado (0 + 0): documentos do **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Novo + atualizado (0 + 0): documentos de **Extensões DMX (Data Mining) para SQL**](../dmx/new-updated-dmx.md)
- [Novo + Atualizado (0+0): documentos sobre o **MDS (Master Data Services) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Novo + atualizado (0 + 0): documentos de **Expressão MDX para SQL**](../mdx/new-updated-mdx.md)
- [Novo + atualizado (0 + 0): documentos do **ODBC (Open Database Connectivity) para SQL**](../odbc/new-updated-odbc.md)
- [Novo + atualizado (0 + 0): documentos do **PowerShell para SQL**](../powershell/new-updated-powershell.md)
- [Novo + Atualizado (0 + 0): documentos de **Ferramentas para SQL**](../tools/new-updated-tools.md)
- [Novo + atualizado (0 + 0): documentos do **XQuery para SQL**](../xquery/new-updated-xquery.md)


