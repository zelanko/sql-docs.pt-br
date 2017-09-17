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
ms.date: 09/11/2017
ms.author: genemi
ms.translationtype: MT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: 9e6b139e45ccb5184255eabedfb0f809ff64fd2b
ms.contentlocale: pt-br
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-sql-server-on-linux-docs"></a>Novos e recentemente atualizado: SQL Server no Linux docs



A Microsoft atualiza alguns de seus artigos existentes no site de documentação [Docs.Microsoft.com](http://docs.microsoft.com/) todos os dias. Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é reexecutado periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita ou como markdown do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de datas e o assunto a seguir:



- *Intervalo de datas das atualizações:* &nbsp; **2017-07-18** &nbsp; - para - &nbsp; **2017-09-11**
- *Área de assunto:* &nbsp; **Microsoft SQL Server no Linux**.




&nbsp;

## <a name="new-articles-created-recently"></a>Novos artigos criados recentemente

Os links a seguir saltar para novos artigos que foram adicionados recentemente.


1. [Email de banco de dados e alertas de Email com o SQL Agent no Linux](sql-server-linux-db-mail-sql-agent.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados a partir de artigos que encontraram recentemente uma atualização grande.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes um trecho é separado da sintaxe de markdown importante que circunda no artigo real. Portanto, esses trechos servem apenas como orientações gerais. Os trechos só mostram a você se vale a pena clicar e visitar o artigo real conforme seus interesses.

Por essas e outras razões, não copie o código desses trechos, nem considere-os como verdade exata. Em vez disso, visite o artigo real.





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compact fornece links para todos os artigos atualizados que estão listados na seção foram extraídas.

1. [Operar o grupo de disponibilidade de alta disponibilidade para o SQL Server no Linux](#TitleNum_1)
2. [Configurar imagens de contêiner de 2017 do SQL Server no Docker](#TitleNum_2)
3. [Configurar o SQL Server no Linux com a ferramenta mssql conf](#TitleNum_3)
4. [Comentários do cliente para o SQL Server no Linux](#TitleNum_4)
5. [Migrar um banco de dados do SQL Server do Windows para Linux usando backup e restauração](#TitleNum_5)
6. [Notas de versão do SQL Server 2017 no Linux](#TitleNum_6)
7. [Orientação de instalação do SQL Server no Linux](#TitleNum_7)
8. [Instalar o SQL Server Integration Services (SSIS) no Linux](#TitleNum_8)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-operate-ha-availability-group-for-sql-server-on-linuxsql-server-linux-availability-group-failover-hamd"></a>1. &nbsp;[Operar HA do grupo de disponibilidade para o SQL Server no Linux](sql-server-linux-availability-group-failover-ha.md)

*Atualizado em: 24-08-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([próxima](#TitleNum_2))

<!-- Source markdown line 167.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1bef3ece125721b041aa2b9d836329736377df8d 669d2b9a614d680b98280d5b522ba82cf466536c  (PR=2948  ,  Filename=sql-server-linux-availability-group-failover-ha.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=7b8c23474aee48e6d34ba268bc8942bc1c0263d3) -->



**Atualizar o grupo de disponibilidade**


Antes de atualizar um grupo de disponibilidade, examine as práticas recomendadas em [atualização disponibilidade grupo réplica instâncias-... / database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md).

As seções a seguir explicam como executar uma atualização sem interrupção com instâncias do SQL Server no Linux com grupos de disponibilidade.

**Etapas de atualização no Linux**


Quando as réplicas de grupo de disponibilidade em instâncias do SQL Server no Linux, o tipo de cluster do grupo de disponibilidade é `EXTERNAL` ou `NONE`. Um grupo de disponibilidade que é gerenciado por um Gerenciador de cluster, além de Failover de Cluster WSFC (Windows Server) é `EXTERNAL`. Pacemaker com Corosync é um exemplo de um Gerenciador de cluster externo. Um grupo de disponibilidade com o Gerenciador de cluster não tem o tipo de cluster `NONE` as etapas de atualização descritas aqui são específicas para grupos de disponibilidade do tipo de cluster `EXTERNAL` ou `NONE`.

1. Antes de começar, fazer backup de cada banco de dados.
2. Atualize instâncias do SQL Server que hospedam réplicas de secundário.

    a. Atualize primeiro réplicas secundárias assíncronas.

    b. Atualize as réplicas secundárias síncronas.

   >[!NOTE]
   >Se um grupo de disponibilidade tiver apenas assíncrona réplicas - para evitar a perda de dados altere uma réplica de síncrona e aguarde até que ele é sincronizado. Em seguida, atualize esta réplica.

   b. 1. Parar o recurso no nó que hospeda a réplica secundária de destino para atualização

   Antes de executar o comando Atualizar, pare o recurso para que o cluster não monitorá-lo e fazer failover desnecessariamente. O exemplo a seguir adiciona uma restrição de local no nó que resultará no recurso deve ser interrompida. Atualização `ag_cluster-master` com o nome do recurso e `nodeName1` com o nó que hospeda a réplica de destino para atualização.

```
   pcs constraint location ag_cluster-master avoids nodeName1
```



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-configure-sql-server-2017-container-images-on-dockersql-server-linux-configure-dockermd"></a>2. &nbsp;[Imagens de contêiner de configurar o SQL Server 2017 no Docker](sql-server-linux-configure-docker.md)

*Atualizado em: 05-09-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_1) | [próxima](#TitleNum_3))

<!-- Source markdown line 257.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0239ed55a23721eedcc0407a0886d08da47c975b 108fe230151cff7dc91fcdc22218f232394746ec  (PR=3050  ,  Filename=sql-server-linux-configure-docker.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=60272ce672c0a32738b0084ea86f8907ec7fc0a5) -->



1. Identificar o Docker **marca** para a versão que você deseja usar. Para exibir as marcas disponíveis, consulte [a página de hub do Docker mssql-server-linux](https://hub.docker.com/r/microsoft/mssql-server-linux/tags/).

1. Baixe a imagem de contêiner de SQL Server com a marca. Por exemplo, para receber a imagem do RC1, substitua `<image_tag>` no comando a seguir com `rc1`.

```
   docker pull microsoft/mssql-server-linux:<image_tag>
```

1. Para executar um novo contêiner com essa imagem, especifique o nome da marca das `docker run` comando. No comando a seguir, substitua `<image_tag>` com a versão que você deseja executar.

```
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d microsoft/mssql-server-linux:<image_tag>
```

```
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d microsoft/mssql-server-linux:<image_tag>
```

Essas etapas também podem ser usadas para fazer o downgrade de um contêiner existente. Por exemplo, você pode deseja reverter ou fazer o downgrade de um contêiner em execução para solução de problemas ou teste. Para fazer o downgrade de um contêiner em execução, você deve estar usando uma técnica de persistência para a pasta de dados. Siga as mesmas etapas descritas a [atualizar seção – #upgrade), mas especificar o nome da marca da versão anterior, quando você executar o novo contêiner.

> [!IMPORTANT]



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-configure-sql-server-on-linux-with-the-mssql-conf-toolsql-server-linux-configure-mssql-confmd"></a>3. &nbsp;[Configurar o SQL Server no Linux com a ferramenta mssql conf](sql-server-linux-configure-mssql-conf.md)

*Atualizado em: 05-09-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_2) | [próxima](#TitleNum_4))

<!-- Source markdown line 233.  ms.author= lbosq.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 6117f03e9617b70077488d86f94b32537c4cb9e8 4247a749c056037dd71a27121525be04be6a4f21  (PR=3042  ,  Filename=sql-server-linux-configure-mssql-conf.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=46b16dcf147dbd863eec0330e87511b4ced6c4ce) -->



**<a id="localaudit"></a>Diretório de conjunto de auditoria local**


O **telemetry.userrequestedlocalauditdirectory** configuração habilita a auditoria Local e permite que você defina o diretório onde os logs de auditoria Local é criados.

1. Crie um diretório de destino para novos logs de auditoria Local. O exemplo a seguir cria um novo **/tmp/auditoria** diretório:

```
   sudo mkdir /tmp/audit
```

1. Alterar o proprietário e o grupo do diretório para o **mssql** usuário:

```
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
```

1. Execute o script mssql conf como raiz com o **definir** comando **telemetry.userrequestedlocalauditdirectory**:

```
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
```

1. Reinicie o serviço do SQL Server:

```
   sudo systemctl restart mssql-server
```

Para obter mais informações, consulte [comentários do cliente para o SQL Server em Linux--sql-server-linux-customer-feedback.md).

**<a id="lcid"></a>Alterar a localidade do SQL Server**


O **language.lcid** alterações de configuração de localidade do SQL Server a qualquer identificador de idioma com suporte (LCID).

1. O exemplo a seguir altera a localidade para o francês (1036):

```
   sudo /opt/mssql/bin/mssql-conf set language.lcid 1036
```

1. Reinicie o serviço do SQL Server para aplicar as alterações:

```
   sudo systemctl restart mssql-server
```

**<a id="memorylimit"></a>Definir o limite de memória**


O **memory.memorylimitmb** determina a quantidade memória física (em MB) disponível para o SQL Server. O padrão é 80% da memória física.

1. Execute o script mssql conf como raiz com o **definir** comando **memory.memorylimitmb**. O exemplo a seguir altera a memória disponível para o SQL Server para 3,25 GB (3328 MB).

```
   sudo /opt/mssql/bin/mssql-conf set memory.memorylimitmb 3328
```

1. Reinicie o serviço do SQL Server para aplicar as alterações:



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-customer-feedback-for-sql-server-on-linuxsql-server-linux-customer-feedbackmd"></a>4. &nbsp;[Comentários do cliente para o SQL Server no Linux](sql-server-linux-customer-feedback.md)

*Atualizado em: 24-08-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_3) | [próxima](#TitleNum_5))

<!-- Source markdown line 104.  ms.author= anshrest.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 9d8122e864804004d91f6b7c5c3d24c4a4114d34 7316ef831c390a854c324f23a02c3fb6005e2fea  (PR=2948  ,  Filename=sql-server-linux-customer-feedback.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=7b8c23474aee48e6d34ba268bc8942bc1c0263d3) -->




**No Docker**

Para habilitar a auditoria Local no docker, você deve ter Docker [manter seu data--sql-server-linux-configure-docker.md).

1. O diretório de destino para novos logs de auditoria Local será no contêiner. Crie um diretório de destino para novos logs de auditoria Local no diretório de host no seu computador. O exemplo a seguir cria um novo **/auditoria** diretório:

```
   sudo mkdir <host directory>/audit
```


1. Adicionar uma `mssql.conf` arquivo com as linhas `[telemetry]` e `userrequestedlocalauditdirectory = <host directory>/audit` no diretório do host:

```
   echo '[telemetry]' >> <host directory>/mssql.conf
```

```
   echo 'userrequestedlocalauditdirectory = <host directory>/audit' >> <host directory>/mssql.conf
```
2. Executar a imagem de contêiner
```
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' --cap-add SYS_PTRACE -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux
```

```
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" --cap-add SYS_PTRACE -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux
```

**Próximas etapas**





&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-migrate-a-sql-server-database-from-windows-to-linux-using-backup-and-restoresql-server-linux-migrate-restore-databasemd"></a>5. &nbsp;[Migrar um banco de dados do SQL Server do Windows para Linux usando backup e restauração](sql-server-linux-migrate-restore-database.md)

*Atualizado em: 24-08-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_4) | [próxima](#TitleNum_6))

<!-- Source markdown line 30.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 e78f5516a46eab834f644979d3e1c0ca415fabcd 6b03a01385078290b9f451ac013b628f53e0e8b4  (PR=2948  ,  Filename=sql-server-linux-migrate-restore-database.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=7b8c23474aee48e6d34ba268bc8942bc1c0263d3) -->



* Computador Windows com o seguinte:
  * [SQL Server](https://www.microsoft.com/sql-server/sql-server-2016-editions) instalado.
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) instalado.
  * Banco de dados de destino para migrar.

* Computador Linux com os seguintes itens instalados:
  * SQL Server 2017 RC2. Consulte os tutoriais de instalação para [RHEL--quickstart-install-connect-red-hat.md) [SLES - quickstart-install-conectar-se-suse.md), ou [Ubuntu - quickstart-install-conectar-se-ubuntu.md).
  * SQL Server 2017 RC2 [tools--sql-server-linux-setup-tools.md de linha de comando).

**Criar um backup no Windows**


Há várias maneiras de criar um arquivo de backup de um banco de dados no Windows. As etapas a seguir usam o SQL Server Management Studio (SSMS).

1. Iniciar **SQL Server Management Studio** em seu computador Windows.

1. Na caixa de diálogo de conexão, digite **localhost**.

1. No Pesquisador de objetos, expanda **bancos de dados**.



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-release-notes-for-sql-server-2017-on-linuxsql-server-linux-release-notesmd"></a>6. &nbsp;[Notas de versão do SQL Server 2017 no Linux](sql-server-linux-release-notes.md)

*Atualizado em: 2017-08-23* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_5) | [próxima](#TitleNum_7))

<!-- Source markdown line 31.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 4c8b9876f4792782314ba2f9b246405fb8036f84 acb97cf0a2e0bdd039575eaab9c41003316cbb02  (PR=2939  ,  Filename=sql-server-linux-release-notes.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=91098c850b0f6affb8e4831325d0f18fd163d71a) -->



**<a id="RC2"></a>RC2 (agosto de 2017)**


A versão do mecanismo do SQL Server para esta versão é 14.0.900.75.

**Plataformas com suporte**


| Plataforma | Sistema de Arquivos | Guia de Instalação |
|-----|-----|-----|
| Área de trabalho, servidor e estação de trabalho do Red Hat Enterprise Linux 7.3 | XFS ou EXT4 | [Instalação guide--quickstart-install-connect-red-hat.md) |
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [Guia de instalação - quickstart-install-conectar-se-suse.md) |
| Ubuntu 16.04LTS | EXT4 | [Guia de instalação - quickstart-install-conectar-se-ubuntu.md) |
| Mecanismo do docker 1.8 + no Windows, Mac ou Linux | N/A | [Guia de instalação - quickstart-install-conectar-se-docker.md) |

> [!NOTE]
> É necessário pelo menos 3,25 GB de memória para executar o SQL Server no Linux.
> Mecanismo do SQL Server foi testado até 1,5 TB de memória no momento.

**Detalhes do pacote**


Detalhes do pacote e locais de download para os pacotes RPM e Debian são listados na tabela a seguir. Observe que você não precisa baixar esses pacotes diretamente se você usar as etapas nos guias de instalação a seguir:

- [Instalação do pacote do SQL Server – sql server-linux setup.md)
- [Instalação package--sql-server-linux-setup-full-text-search.md de pesquisa de texto completo)
- [Instalação do SQL Server Agent package--sql-server-linux-setup-sql-agent.md)

| Pacote | versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.900.75-1 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.900.75-1.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.900.75-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.900.75-1.x86_64.rpm)</br>[Pacote RPM do SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.900.75-1.x86_64.rpm) |



&nbsp;

&nbsp;

---

<a name="TitleNum_7"/>

### <a name="7-nbsp-installation-guidance-for-sql-server-on-linuxsql-server-linux-setupmd"></a>7. &nbsp;[Orientação de instalação do SQL Server no Linux](sql-server-linux-setup.md)

*Atualizado em: 2017-08-28* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_6) | [próxima](#TitleNum_8))

<!-- Source markdown line 70.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 00394e1733568a55243788d828968ff9b58a3c99 8ba2bf6f9cf4b5f54a6ee0f4d16d4437d5724880  (PR=2971  ,  Filename=sql-server-linux-setup.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=303d3b74da3fe370d19b7602c0e11e67b63191e7) -->



**<a id="rollback"></a>Reversão SQL Server**


A reversão ou fazer downgrade do SQL Server para uma versão anterior, use as seguintes etapas:

1. Identifique o número de versão para o pacote do SQL Server que você deseja fazer o downgrade. Para obter uma lista de números de pacote, consulte [versão notes--sql-server-linux-release-notes.md).

1. Fazer o downgrade para uma versão anterior do SQL Server. Nos comandos a seguir, substitua `<version_number>` com o número de versão do SQL Server identificado na etapa um.

   | Plataforma | Comando de atualização de pacote |
   |-----|-----|
   | RHEL | `sudo yum downgrade mssql-server-<version_number>.x86_64` |
   | SLES | `sudo zypper install --oldpackage mssql-server=<version_number>` |
   | Ubuntu | `sudo apt-get install mssql-server=<version_number>`<br/>`sudo systemctl start mssql-server` |

> [!NOTE]
> Somente há suporte para fazer o downgrade para uma versão dentro da mesma versão principal, como SQL Server 2017.

> [!IMPORTANT]
> Somente há suporte para downgrade entre RC2 e RC1 neste momento.




&nbsp;

&nbsp;

---

<a name="TitleNum_8"/>

### <a name="8-nbsp-install-sql-server-integration-services-ssis-on-linuxsql-server-linux-setup-ssismd"></a>8. &nbsp;[Instalar o SQL Server Integration Services (SSIS) no Linux](sql-server-linux-setup-ssis.md)

*Atualizado em: 24-08-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_7))

<!-- Source markdown line 66.  ms.author= lle.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 a3fecd2553d1b25406445b8a26b22c9015dd98fe f836d560513fef1217e7dbce0ab85f78eec6f937  (PR=2948  ,  Filename=sql-server-linux-setup-ssis.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=7b8c23474aee48e6d34ba268bc8942bc1c0263d3) -->



Se você já tiver `mssql-server-is` instalado, você pode atualizar a versão mais recente com o seguinte comando:

```
sudo apt-get install mssql-server-is
```


Para remover `mssql-server-is`, você pode executar o seguinte comando:
```
sudo apt-get remove msssql-server-is
```



**<a name="RHEL"></a>Instalar o SSIS em RHEL**

Para instalar o `mssql-server-is` o pacote em RHEL, siga estas etapas:


1.  Entre no modo de superusuário.

```
    sudo su
```


2.  Baixe o arquivo de configuração de repositório do Microsoft SQL Server Red Hat.

```
    curl https://packages.microsoft.com/config/rhel/7/mssql-server.repo > /etc/yum.repos.d/mssql-server.repo
```


3.  Sair do modo de superusuário.

```
    exit
```


4.  Execute os comandos a seguir para instalar o SQL Server Integration Services.

```
    sudo yum install -y mssql-server-is
```


5.  Após a instalação, execute `ssis-conf`.







## <a name="similar-articles"></a>Artigos Semelhantes

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

Esta seção lista os artigos muito semelhantes para artigos atualizados recentemente em outras áreas de assunto, em nosso repositório público de GitHub.com: [sql/MicrosoftDocs-documentos](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Áreas de assunto que têm artigos novos ou atualizados recentemente

- [Novo + atualizado (3 + 12): **Advanced Analytics para o SQL** documentos](../advanced-analytics/new-updated-advanced-analytics.md)
- [Novo + atualizado (5 + 0): **conectar-se ao SQL** documentos](../connect/new-updated-connect.md)
- [Novo + atualizado (5 + 1): **mecanismo de banco de dados do SQL** documentos](../database-engine/new-updated-database-engine.md)
- [Novo + atualizado (19 + 82): **Integration Services para SQL** documentos](../integration-services/new-updated-integration-services.md)
- [Novo + atualizado (1 + 8): **Linux para o SQL** documentos](../linux/new-updated-linux.md)
- [Novo + atualizado (12 + 1): **bancos de dados relacionais do SQL** documentos](../relational-databases/new-updated-relational-databases.md)
- [Novo + atualizado (0 + 1): **Reporting Services para SQL** documentos](../reporting-services/new-updated-reporting-services.md)
- [Novo + atualizado (7 + 1): **Microsoft SQL Server** documentos](../sql-server/new-updated-sql-server.md)
- [Novo + atualizado (1 + 1): **SQL Server Data Tools (SSDT)** documentos](../ssdt/new-updated-ssdt.md)
- [Novo + atualizado (0 + 2): **Migration Assistant SSMA (SQL Server)** documentos](../ssma/new-updated-ssma.md)
- [Novo + atualizado (1 + 4): **SQL Server Management Studio (SSMS)** documentos](../ssms/new-updated-ssms.md)
- [Novo + atualizados (4 + 1): **Transact-SQL** documentos](../t-sql/new-updated-t-sql.md)
- [Novo + atualizado (0 + 1): **Tools para SQL** documentos](../tools/new-updated-tools.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Áreas de assunto que não têm nenhum artigo novo ou atualizado recentemente

- [Novo + atualizado (0 + 0): documentos do **ADO (ActiveX Data Objects) para SQL**](../ado/new-updated-ado.md)
- [Novo + atualizado (0 + 0): **Analysis Services para SQL** documentos](../analysis-services/new-updated-analysis-services.md)
- [Novo + atualizado (0 + 0): documentos do **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Novo + atualizado (0 + 0): documentos de **Extensões DMX (Data Mining) para SQL**](../dmx/new-updated-dmx.md)
- [Novo + atualizado (0 + 0): **Master Data Services (MDS) para SQL** documentos](../master-data-services/new-updated-master-data-services.md)
- [Novo + atualizado (0 + 0): documentos de **Expressão MDX para SQL**](../mdx/new-updated-mdx.md)
- [Novo + atualizado (0 + 0): documentos do **ODBC (Open Database Connectivity) para SQL**](../odbc/new-updated-odbc.md)
- [Novo + atualizado (0 + 0): documentos do **PowerShell para SQL**](../powershell/new-updated-powershell.md)
- [Novo + atualizado (0 + 0): documentos de **Exemplos para SQL**](../sample/new-updated-sample.md)
- [Novo + atualizado (0 + 0): documentos do **XQuery para SQL**](../xquery/new-updated-xquery.md)



