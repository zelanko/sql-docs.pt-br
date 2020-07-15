---
title: Definir configurações do SQL Server em Linux
description: Este artigo descreve como usar a ferramenta mssql-conf para definir configurações do SQL Server no Linux.
author: VanMSFT
ms.author: vanto
ms.date: 07/30/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 06798dff-65c7-43e0-9ab3-ffb23374b322
ms.openlocfilehash: 5d3ee42f28fed73a4dd513b10d01948552fdd6d5
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85901540"
---
# <a name="configure-sql-server-on-linux-with-the-mssql-conf-tool"></a>Configurar o SQL Server em Linux com a ferramenta mssql-conf

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

**mssql-conf** é um script de configuração que é instalado com o SQL Server 2017 para Red Hat Enterprise Linux, SUSE Linux Enterprise Server e Ubuntu. Ele modifica o [**mssql.conf file**](#mssql-conf-format) no qual os valores de configuração estão armazenados. Você pode usar o utilitário **mssql-conf** para definir os seguintes parâmetros:

|||
|---|---|
| [Agente](#agent) | Habilite o SQL Server Agent. |
| [Ordenação](#collation) | Definir uma nova ordenação para o SQL Server em Linux. |
| [Comentários do cliente](#customerfeedback) | Escolher se o SQL Server envia ou não comentários à Microsoft. |
| [Perfil do Database Mail](#dbmail) | Definir o perfil padrão do Database Mail para o SQL Server em Linux. |
| [Diretório de dados padrão](#datadir) | Alterar o diretório padrão para novos arquivos de dados de banco de dados do SQL Server (.mdf). |
| [Diretório de log padrão](#datadir) | Alterar o diretório padrão para novos arquivos de log de banco de dados do SQL Server (.ldf). |
| [Diretório padrão do banco de dados mestre](#masterdatabasedir) | Alterar o diretório padrão para o banco de dados mestre e os arquivos de log.|
| [Nome padrão do arquivo de banco de dados mestre](#masterdatabasename) | Alterar o nome de arquivos de banco de dados mestre. |
| [Diretório de despejo padrão](#dumpdir) | Alterar o diretório padrão para novos despejos de memória e outros arquivos de solução de problemas. |
| [Diretório de log de erros padrão](#errorlogdir) | Alterar o diretório padrão para novos arquivos de logs de erros do SQL Server, rastreamento do Profiler padrão, XE da sessão de integridade do sistema e XE da sessão do Hekaton. |
| [Diretório de backup padrão](#backupdir) | Alterar o diretório padrão para novos arquivos de backup. |
| [Tipo de despejo](#coredump) | Escolher o tipo de arquivo de despejo de memória de despejo a ser coletado. |
| [Alta disponibilidade](#hadr) | Habilitar grupos de disponibilidade. |
| [Diretório de auditoria local](#localaudit) | Definir um diretório para adicionar arquivos de auditoria local. |
| [Localidade](#lcid) | Definir a localidade a ser usada pelo SQL Server. |
| [Limite de memória](#memorylimit) | Definir o limite de memória para o SQL Server. |
| [Porta TCP](#tcpport) | Alterar a porta em que o SQL Server escuta conexões. |
| [TLS](#tls) | Configurar o protocolo TLS. |
| [Sinalizadores de rastreamento](#traceflags) | Definir os sinalizadores de rastreamento que o serviço vai usar. |

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

**mssql-conf** é um script de configuração que é instalado com o [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] para Red Hat Enterprise Linux, SUSE Linux Enterprise Server e Ubuntu. Você pode usar esse utilitário para definir os seguintes parâmetros:

|||
|---|---|
| [Agente](#agent) | Habilitar o SQL Server Agent |
| [Ordenação](#collation) | Definir uma nova ordenação para o SQL Server em Linux. |
| [Comentários do cliente](#customerfeedback) | Escolher se o SQL Server envia ou não comentários à Microsoft. |
| [Perfil do Database Mail](#dbmail) | Definir o perfil padrão do Database Mail para o SQL Server em Linux. |
| [Diretório de dados padrão](#datadir) | Alterar o diretório padrão para novos arquivos de dados de banco de dados do SQL Server (.mdf). |
| [Diretório de log padrão](#datadir) | Alterar o diretório padrão para novos arquivos de log de banco de dados do SQL Server (.ldf). |
| [Diretório padrão de arquivos de banco de dados mestre](#masterdatabasedir) | Alterar o diretório padrão para os arquivos do banco de dados mestre na instalação existente do SQL.|
| [Nome padrão do arquivo de banco de dados mestre](#masterdatabasename) | Alterar o nome de arquivos de banco de dados mestre. |
| [Diretório de despejo padrão](#dumpdir) | Alterar o diretório padrão para novos despejos de memória e outros arquivos de solução de problemas. |
| [Diretório de log de erros padrão](#errorlogdir) | Alterar o diretório padrão para novos arquivos de logs de erros do SQL Server, rastreamento do Profiler padrão, XE da sessão de integridade do sistema e XE da sessão do Hekaton. |
| [Diretório de backup padrão](#backupdir) | Alterar o diretório padrão para novos arquivos de backup. |
| [Tipo de despejo](#coredump) | Escolher o tipo de arquivo de despejo de memória de despejo a ser coletado. |
| [Alta disponibilidade](#hadr) | Habilitar grupos de disponibilidade. |
| [Diretório de auditoria local](#localaudit) | Definir um diretório para adicionar arquivos de auditoria local. |
| [Localidade](#lcid) | Definir a localidade a ser usada pelo SQL Server. |
| [Limite de memória](#memorylimit) | Definir o limite de memória para o SQL Server. |
| [Coordenador de Transações Distribuídas da Microsoft](#msdtc) | Configurar e solucionar problemas do MSDTC no Linux. |
| [EULAs para Serviços de Machine Learning](#mlservices-eula) | Aceitar os EULAs de R e Python para pacotes de Serviços de Machine Learning. Aplica-se somente ao SQL Server 2019.|
| [outboundnetworkaccess](#mlservices-outbound-access) |Habilitar o acesso à rede para extensões Java, R e Python dos [Serviços de Machine Learning](sql-server-linux-setup-machine-learning.md).|
| [Porta TCP](#tcpport) | Alterar a porta em que o SQL Server escuta conexões. |
| [TLS](#tls) | Configurar o protocolo TLS. |
| [Sinalizadores de rastreamento](#traceflags) | Definir os sinalizadores de rastreamento que o serviço vai usar. |

::: moniker-end

> [!TIP]
> Algumas dessas configurações também podem ser definidas com variáveis de ambiente. Para obter mais informações, confira [Definir configurações do SQL Server com variáveis de ambiente](sql-server-linux-configure-environment-variables.md).

## <a name="usage-tips"></a>Dicas de uso

* Para grupos de disponibilidade Always On e clusters de disco compartilhados, sempre faça as mesmas alterações de configuração em cada nó.

* Para o cenário de cluster de disco compartilhado, não tente reiniciar o serviço **mssql-server** para aplicar as alterações. O SQL Server está em execução como um aplicativo. Em vez disso, coloque o recurso offline e, em seguida, novamente online.

* Esses exemplos executam mssql-conf especificando o caminho completo: **/opt/mssql/bin/mssql-conf**. Se você optar por navegar até esse caminho, execute mssql-conf no contexto do diretório atual: **./mssql-conf**.

## <a name="enable-sql-server-agent"></a><a id="agent"></a> Habilitar o SQL Server Agent

A configuração **sqlagent.enabled** habilita o [SQL Server Agent](sql-server-linux-run-sql-server-agent-job.md). Por padrão, o SQL Server Agent está desabilitado. Se **sqlagent.enabled** não está presente no arquivo de configurações mssql.conf, o SQL Server pressupõe internamente que o SQL Server Agent está desabilitado.

Para alterar essa configuração, use as seguintes etapas:

1. Habilite o SQL Server Agent:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
   ```

2. Reinicie o serviço SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="change-the-sql-server-collation"></a><a id="collation"></a> Alterar a ordenação do SQL Server

A opção **set-collation** altera o valor da ordenação para qualquer um dos agrupamentos compatíveis.

1. Primeiro [faça backup de todos os bancos de dados de usuário](sql-server-linux-backup-and-restore-database.md) no servidor.

1. Use o procedimento armazenado [sp_detach_db](../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md) para desanexar os bancos de dados de usuário.

1. Execute a opção **set-collation** e siga os prompts:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set-collation
   ```

1. O utilitário mssql-conf tentará alterar para o valor de ordenação especificado e reiniciar o serviço. Se houver erros, ele reverterá a ordenação para o valor anterior.

1. Restaure os backups de banco de dados do usuário.

Para obter uma lista de agrupamentos compatíveis, execute a função [sys.fn_helpcollations](../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md): `SELECT Name from sys.fn_helpcollations()`.

## <a name="configure-customer-feedback"></a><a id="customerfeedback"></a> Configurar os comentários do cliente

A configuração **telemetry.customerfeedback** determina se o SQL Server envia comentários à Microsoft ou não. Por padrão, esse valor é definido como **true** para todas as edições. Para alterar o valor, execute os seguintes comandos:

> [!IMPORTANT]
> Você não pode desligar os comentários do cliente para edições gratuitas do SQL Server, Express e Developer.

1. Execute o script mssql-conf como raiz com o comando **set** para **telemetry.customerfeedback**. O exemplo a seguir desativa os comentários do cliente, especificando **false**.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false
   ```

1. Reinicie o serviço SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

Para obter mais informações, confira [Comentários do cliente para SQL Server em Linux](sql-server-linux-customer-feedback.md) e a [Política de Privacidade do SQL Server](https://go.microsoft.com/fwlink/?LinkID=868444).

## <a name="change-the-default-data-or-log-directory-location"></a><a id="datadir"></a> Alterar a localização padrão do diretório de dados ou de log

As configurações **filelocation.defaultdatadir** e **filelocation.defaultlogdir** alteram a localização em que o novo banco de dados e os arquivos de log são criados. Por padrão, essa localização é /var/opt/mssql/data. Para alterar essas configurações, use as seguintes etapas:

1. Crie o diretório de destino para novos arquivos de log e de dados de bancos de dados. O exemplo a seguir cria um diretório **/tmp/data**:

   ```bash
   sudo mkdir /tmp/data
   ```

1. Altere o proprietário e o grupo do diretório para o usuário **mssql**:

   ```bash
   sudo chown mssql /tmp/data
   sudo chgrp mssql /tmp/data
   ```

1. Use mssql-conf para alterar o diretório de dados padrão com o comando **set**:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultdatadir /tmp/data
   ```

1. Reinicie o serviço SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

1. Agora, todos os arquivos de banco de dados para os novos bancos de dados criados serão armazenados nessa nova localização. Se quiser alterar a localização dos arquivos de log (.ldf) dos novos bancos de dados, você poderá usar o seguinte comando "set":

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultlogdir /tmp/log
   ```

1. Esse comando também pressupõe que um diretório/tmp/log exista e que esteja sob o usuário e grupo **mssql**.


## <a name="change-the-default-master-database-file-directory-location"></a><a id="masterdatabasedir"></a> Alterar a localização do diretório padrão de arquivos de banco de dados mestre

A configuração **filelocation.masterdatafile** e **filelocation.masterlogfile** altera a localização em que o mecanismo de SQL Server procura os arquivos de banco de dados mestre. Por padrão, essa localização é /var/opt/mssql/data.

Para alterar essas configurações, use as seguintes etapas:

1. Crie o diretório de destino para novos arquivos de log de erros. O exemplo a seguir cria um novo diretório **/tmp/masterdatabasedir**:

   ```bash
   sudo mkdir /tmp/masterdatabasedir
   ```

1. Altere o proprietário e o grupo do diretório para o usuário **mssql**:

   ```bash
   sudo chown mssql /tmp/masterdatabasedir
   sudo chgrp mssql /tmp/masterdatabasedir
   ```

1. Use mssql-conf para alterar o diretório de banco de dados mestre padrão para os dados mestres e os arquivos de log com o comando **set**:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterdatafile /tmp/masterdatabasedir/master.mdf
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterlogfile /tmp/masterdatabasedir/mastlog.ldf
   ```

   > [!NOTE]
   > Além de mover os dados mestres e os arquivos de log, isso também move a localização padrão para todos os outros bancos de dados do sistema.

1. Interromper o serviço do SQL Server:

   ```bash
   sudo systemctl stop mssql-server
   ```

1. Mover o master.mdf e o masterlog.ldf:

   ```bash
   sudo mv /var/opt/mssql/data/master.mdf /tmp/masterdatabasedir/master.mdf 
   sudo mv /var/opt/mssql/data/mastlog.ldf /tmp/masterdatabasedir/mastlog.ldf
   ```

1. Iniciar o serviço do SQL Server:

   ```bash
   sudo systemctl start mssql-server
   ```

   > [!NOTE]
   > Se o SQL Server não puder localizar os arquivos master.mdf e mastlog.ldf no diretório especificado, uma cópia modelo dos bancos de dados do sistema será criada automaticamente no diretório especificado e SQL Server será inicializado com êxito. No entanto, metadados como bancos de dados de usuário, logons de servidor, certificados de servidor, chaves de criptografia, trabalhos do SQL Agent ou senha de logon de SA antiga não serão atualizados no novo banco de dados mestre. Para continuar usando os metadados existentes, você precisará interromper o SQL Server e mover o master.mdf e o mastlog.ldf antigos para a nova localização especificada e iniciar o SQL Server.
 
## <a name="change-the-name-of-master-database-files"></a><a id="masterdatabasename"></a> Alterar o nome de arquivos de banco de dados mestre

A configuração **filelocation.masterdatafile** e **filelocation.masterlogfile** altera a localização em que o mecanismo de SQL Server procura os arquivos de banco de dados mestre. Você também pode usar isso para alterar o nome dos arquivos de log e do banco de dados mestre. 

Para alterar essas configurações, use as seguintes etapas:

1. Interromper o serviço do SQL Server:

   ```bash
   sudo systemctl stop mssql-server
   ```

1. Use mssql-conf para alterar os nomes de banco de dados mestre esperados para os arquivos de log e os dados mestre com o comando **set**:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterdatafile /var/opt/mssql/data/masternew.mdf
   sudo /opt/mssql/bin/mssql-conf set filelocation.mastlogfile /var/opt/mssql/data/mastlognew.ldf
   ```

   > [!IMPORTANT]
   > Você só pode alterar o nome dos arquivos de log e do banco de dados mestre após o SQL Server ter sido iniciado com êxito. Antes da execução inicial, o SQL Server espera que os arquivos sejam nomeados master.mdf e mastlog.ldf.

1. Alterar o nome dos arquivos de log e dos dados de banco de dados mestre 

   ```bash
   sudo mv /var/opt/mssql/data/master.mdf /var/opt/mssql/data/masternew.mdf
   sudo mv /var/opt/mssql/data/mastlog.ldf /var/opt/mssql/data/mastlognew.ldf
   ```

1. Iniciar o serviço do SQL Server:

   ```bash
   sudo systemctl start mssql-server
   ```

## <a name="change-the-default-dump-directory-location"></a><a id="dumpdir"></a> Alterar a localização padrão de despejo do diretório

A configuração **filelocation.defaultdumpdir** altera a localização padrão em que a memória e os despejos SQL são gerados sempre que há uma falha. Por padrão, esses arquivos são gerados em /var/opt/mssql/log.

Para configurar essa nova localização, use os seguintes comandos:

1. Crie o diretório de destino para novos arquivos de despejo. O exemplo a seguir cria um diretório **/tmp/dump**:

   ```bash
   sudo mkdir /tmp/dump
   ```

1. Altere o proprietário e o grupo do diretório para o usuário **mssql**:

   ```bash
   sudo chown mssql /tmp/dump
   sudo chgrp mssql /tmp/dump
   ```

1. Use mssql-conf para alterar o diretório de dados padrão com o comando **set**:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultdumpdir /tmp/dump
   ```

1. Reinicie o serviço SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="change-the-default-error-log-file-directory-location"></a><a id="errorlogdir"></a> Alterar a localização padrão do diretório de arquivos de log de erros

A configuração **filelocation.errorlogfile** altera a localização em que o novo log de erros, o rastreamento padrão do Profiler, os arquivos XE da sessão de integridade do sistema e os arquivos XE da sessão do Hekaton são criados. Por padrão, essa localização é /var/opt/mssql/log. O diretório no qual o arquivo de log de erros do SQL é definido se torna o diretório de logs padrão para outros logs.

Para alterar essas configurações:

1. Crie o diretório de destino para novos arquivos de log de erros. O exemplo a seguir cria um diretório **/tmp/logs**:

   ```bash
   sudo mkdir /tmp/logs
   ```

1. Altere o proprietário e o grupo do diretório para o usuário **mssql**:

   ```bash
   sudo chown mssql /tmp/logs
   sudo chgrp mssql /tmp/logs
   ```

1. Use mssql-conf para alterar o nome do arquivo de log de erros padrão com o comando **set**:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.errorlogfile /tmp/logs/errorlog
   ```

1. Reinicie o serviço SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```


## <a name="change-the-default-backup-directory-location"></a><a id="backupdir"></a> Alterar a localização padrão de backup do diretório

A configuração **filelocation.defaultbackupdir** altera a localização padrão em que os arquivos de backup são gerados. Por padrão, esses arquivos são gerados em /var/opt/mssql/data.

Para configurar essa nova localização, use os seguintes comandos:

1. Crie o diretório de destino para novos arquivos de backup. O exemplo a seguir cria um diretório **/tmp/backup**:

   ```bash
   sudo mkdir /tmp/backup
   ```

1. Altere o proprietário e o grupo do diretório para o usuário **mssql**:

   ```bash
   sudo chown mssql /tmp/backup
   sudo chgrp mssql /tmp/backup
   ```

1. Use mssql-conf para alterar o diretório de backup padrão com o comando "set":

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultbackupdir /tmp/backup
   ```

1. Reinicie o serviço SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="specify-core-dump-settings"></a><a id="coredump"></a> Especificar configurações de despejo de núcleo

Se ocorrer uma exceção em um dos processos de SQL Server, o SQL Server criará um despejo de memória.

Há duas opções para controlar o tipo de despejo de memória que o SQL Server coleta: **coredump.coredumptype** e **coredump.captureminiandfull**. Eles estão relacionados às duas fases da captura de despejo principal. 

A primeira fase da captura é controlada pela configuração **coredump.coredumptype**, que determina o tipo de arquivo de despejo gerado durante uma exceção. A segunda fase é habilitada quando a configuração **coredump.captureminiandfull**. Se **coredump.captureminiandfull** for definido como true, o arquivo de despejo especificado por **coredump.coredumptype** e um segundo minidespejo serão gerados. Definir **coredump.captureminiandfull** como false desabilita a segunda tentativa de captura.

1. Decida se deseja capturar o minidespejo e o despejo completo com a configuração **coredump.captureminiandfull**.

    ```bash
    sudo /opt/mssql/bin/mssql-conf set coredump.captureminiandfull <true or false>
    ```

    Padrão: **false**

1. Especifique o tipo de arquivo de despejo com a configuração **coredump.coredumptype**.

    ```bash
    sudo /opt/mssql/bin/mssql-conf set coredump.coredumptype <dump_type>
    ```

    Padrão: **miniplus**

    A tabela a seguir lista os possíveis valores **coredump.coredumptype**.

    | Type | Descrição |
    |-----|-----|
    | **mini** | Mini é o menor tipo de arquivo de despejo. Ele usa as informações do sistema Linux para determinar threads e módulos no processo. O despejo contém apenas os módulos e pilhas de thread do ambiente de host. Ele não contém referências de memória indiretas nem globais. |
    | **miniplus** | O MiniPlus é semelhante ao mini, mas inclui memória adicional. Ele entende os mecanismos internos do SQLPAL e o ambiente de host, adicionando as seguintes regiões de memória ao despejo:</br></br> – Vários globais</br> – Toda a memória acima de 64 TB</br> – Todas as regiões nomeadas encontradas em **/proc/$pid/maps**</br> – Memória indireta de threads e pilhas</br> – Informações de threads</br> –Tebs e Pebs associados</br> – Informações do módulo</br> – Árvore de VMM e de VAD |
    | **filtrado** | Filtrado usa um design baseado em subtração em que toda a memória no processo é incluída, a menos que seja especificamente excluída. O design entende os mecanismos internos do SQLPAL e o ambiente de host, excluindo certas regiões do despejo.
    | **completo** | Completo é um despejo de processo completo que inclui todas as regiões localizadas em **/proc/$pid/maps**. Isso não é controlado pela configuração **coredump.captureminiandfull**. |

## <a name="set-the-default-database-mail-profile-for-sql-server-on-linux"></a><a id="dbmail"></a> Definir o perfil padrão do Database Mail para o SQL Server em Linux

O **sqlpagent.databasemailprofile** permite que você defina o perfil padrão do Database Mail para alertas de email.

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.databasemailprofile <profile_name>
```
## <a name="high-availability"></a><a id="hadr"></a> Alta disponibilidade

A opção **hadr.hadrenabled** habilita grupos de disponibilidade na instância do SQL Server. O comando a seguir habilita os grupos de disponibilidade definindo **hadr.hadrenabled** para 1. É preciso reiniciar o SQL Server para que essa configuração entre em vigor.

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

Para obter informações sobre como isso é usado com grupos de disponibilidade, confira os dois tópicos a seguir.

- [Configurar um grupo de disponibilidade Always On para o SQL Server em Linux](sql-server-linux-availability-group-configure-ha.md)
- [Configurar um grupo de disponibilidade de escala de leitura para o SQL Server em Linux](sql-server-linux-availability-group-configure-rs.md)


## <a name="set-local-audit-directory"></a><a id="localaudit"></a> Definir o diretório de auditoria local

A configuração **telemetry.userrequestedlocalauditdirectory** habilita a auditoria local e permite que você defina o diretório em que os logs de auditoria local são criados.

1. Crie um diretório de destino para novos logs de Auditoria Local. O exemplo a seguir cria um diretório **/tmp/audit**:

   ```bash
   sudo mkdir /tmp/audit
   ```

1. Altere o proprietário e o grupo do diretório para o usuário **mssql**:

   ```bash
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
   ```

1. Execute o script mssql-conf como raiz com o comando **set** para **telemetry.userrequestedlocalauditdirectory**:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
   ```

1. Reinicie o serviço SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

Para obter mais informações, confira [Comentários do cliente para SQL Server em Linux](sql-server-linux-customer-feedback.md).

## <a name="change-the-sql-server-locale"></a><a id="lcid"></a> Alterar a localidade do SQL Server

A configuração **language.lcid** altera a localidade do SQL Server para qualquer LCID (identificador de idioma) com suporte. 

1. O exemplo a seguir altera a localidade para francês (1036):

   ```bash
   sudo /opt/mssql/bin/mssql-conf set language.lcid 1036
   ```

1. Reinicie o serviço do SQL Server para aplicar as alterações:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="set-the-memory-limit"></a><a id="memorylimit"></a> Definir o limite de memória

A configuração **memory.memorylimitmb** controla a quantidade de memória física (em MB) disponível para o SQL Server. O padrão é 80% da memória física.

1. Execute o script mssql-conf como raiz com o comando **set** para **memory.memorylimitmb**. O exemplo a seguir altera a memória disponível para SQL Server para 3,25 GB (3.328 MB).

   ```bash
   sudo /opt/mssql/bin/mssql-conf set memory.memorylimitmb 3328
   ```

1. Reinicie o serviço do SQL Server para aplicar as alterações:

   ```bash
   sudo systemctl restart mssql-server
   ```

::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a name="configure-msdtc"></a><a id="msdtc"></a> Configurar MSDTC

As configurações **network.rpcport** e **distributedtransaction.servertcpport** são usadas para configurar o MSDTC (Coordenador de Transações Distribuídas da Microsoft). Para alterar essas configurações, execute os seguintes comandos:

1. Execute o script mssql-conf como raiz com o comando **set** para "network.rpcport":

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.rpcport <rcp_port>
   ```

2. Em seguida, defina a configuração "distributedtransaction.servertcpport":

   ```bash
   sudo /opt/mssql/bin/mssql-conf set distributedtransaction.servertcpport <servertcpport_port>
   ```

Além de definir esses valores, você também deve configurar o roteamento e atualizar o firewall para a porta 135. Para obter mais informações sobre como fazer isso, confira [Como configurar o MSDTC no Linux](sql-server-linux-configure-msdtc.md).

Há várias outras configurações de mssql-conf que você pode usar para monitorar e solucionar problemas do MSDTC. A tabela a seguir descreve resumidamente essas configurações. Para obter mais informações o uso delas, confira os detalhes no artigo de suporte do Windows, [Como habilitar o rastreamento de diagnóstico para o MS DTC](https://support.microsoft.com/help/926099/how-to-enable-diagnostic-tracing-for-ms-dtc-on-a-windows-based-compute).

| configuração mssql-conf | Descrição |
|---|---|
| distributedtransaction.allowonlysecurerpccalls | Configurar chamadas RPC somente seguras para transações distribuídas |
| distributedtransaction.fallbacktounsecurerpcifnecessary | Configurar chamadas RPC somente de segurança para transações distribuídas |
| distributedtransaction.maxlogsize | Tamanho do arquivo de log de transações do DTC em MB. O padrão é 64 MB |
| distributedtransaction.memorybuffersize | Tamanho do buffer circular no qual os rastreamentos são armazenados. Esse tamanho é em MB e o padrão é 10 MB |
| distributedtransaction.servertcpport | Porta do servidor RPC do MSDTC |
| distributedtransaction.trace_cm | Rastreamentos no gerenciador de conexões |
| distributedtransaction.trace_contact | Rastreia o pool de contatos e os contatos |
| distributedtransaction.trace_gateway | Rastreia a origem do gateway |
| distributedtransaction.trace_log | Rastreamento de log |
| distributedtransaction.trace_misc | Rastreamentos que não podem ser categorizados em outras categorias |
| distributedtransaction.trace_proxy | Rastreamentos gerados no proxy do MSDTC |
| distributedtransaction.trace_svc | Rastreia a inicialização do serviço e do arquivo .exe |
| distributedtransaction.trace_trace | A infraestrutura de rastreamento propriamente dita |
| distributedtransaction.trace_util | Rastreia rotinas do utilitário que são chamadas de vários locais |
| distributedtransaction.trace_xa | Origem de rastreamento do XATM (Gerenciador de Transação XA) |
| distributedtransaction.tracefilepath | Pasta na qual os arquivos de rastreamento devem ser armazenados |
| distributedtransaction.turnoffrpcsecurity | Habilitar ou desabilitar a segurança RPC para transações distribuídas |

::: moniker-end
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a name="accept-mlservices-eulas"></a><a id="mlservices-eula"></a> Aceitar EULAs para Serviços de Machine Learning

A adição de [pacotes R ou Python de aprendizado de máquina](sql-server-linux-setup-machine-learning.md) ao mecanismo de banco de dados requer que você aceite os termos de licenciamento para distribuições open-source de R e Python. A tabela a seguir enumera todas as opções ou comandos disponíveis relacionados a EULAs de Serviços de Machine Learning. O mesmo parâmetro de EULA é usado para R e Python, dependendo do que você instalou.

```bash
# For all packages: database engine and mlservices
# Setup prompts for mlservices EULAs, which you need to accept
sudo /opt/mssql/bin/mssql-conf setup

# Add R or Python to an existing installation
sudo /opt/mssql/bin/mssql-conf setup accept-eula-ml

# Alternative valid syntax
# Adds the EULA section to the INI and sets acceptulam to yes
sudo /opt/mssql/bin/mssql-conf set EULA accepteulaml Y

# Rescind EULA acceptance and removes the setting
sudo /opt/mssql/bin/mssql-conf unset EULA accepteulaml
```

Você também pode adicionar a aceitação de EULA diretamente ao [arquivo mssql.conf](#mssql-conf-format):

```ini
[EULA]
accepteula = Y
accepteulaml = Y
```
:::moniker-end
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a name="enable-outbound-network-access"></a><a id="mlservices-outbound-access"></a> Habilitar acesso à rede de saída

O acesso à rede de saída para extensões R, Python e Java no recurso de [Serviços de Machine Learning do SQL Server](sql-server-linux-setup-machine-learning.md) está desabilitado por padrão. Para habilitar as solicitações de saída, defina a propriedade booliana "outboundnetworkaccess" usando mssql-conf.

Depois de definir a propriedade, reinicie o serviço SQL Server Launchpad para ler os valores atualizados do arquivo INI. Uma mensagem de reinicialização lembrará você sempre que uma configuração relacionada à extensibilidade for modificada.

```bash
# Adds the extensibility section and property.
# Sets "outboundnetworkaccess" to true.
# This setting is required if you want to access data or operations off the server.
sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1

# Turns off network access but preserves the setting
sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 0

# Removes the setting and rescinds network access
sudo /opt/mssql/bin/mssql-conf unset extensibility.outboundnetworkaccess
```

Você também pode adicionar "outboundnetworkaccess" diretamente ao [arquivo mssql.conf](#mssql-conf-format):

```ini
[extensibility]
outboundnetworkaccess = 1
```
:::moniker-end

## <a name="change-the-tcp-port"></a><a id="tcpport"></a> Alterar a porta TCP

A configuração **network.tcpport** altera a porta TCP em que o SQL Server escuta conexões. Por padrão, essa porta é definida para 1433. Para alterar a porta, execute os seguintes comandos:

1. Execute o script mssql-conf como raiz com o comando "set" para "network.tcpport":

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.tcpport <new_tcp_port>
   ```

2. Reinicie o serviço SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

3. Ao se conectar ao SQL Server agora, você deve especificar a porta personalizada com uma vírgula (,) após o nome do host ou o endereço IP. Por exemplo, para se conectar com o SQLCMD, você usaria o seguinte comando:

   ```bash
   sqlcmd -S localhost,<new_tcp_port> -U test -P test
   ```

## <a name="specify-tls-settings"></a><a id="tls"></a> Especificar configurações de TLS

As opções a seguir configuram o TLS para uma instância do SQL Server em execução no Linux.

|Opção |Descrição |
|--- |--- |
|**network.forceencryption** |Se for 1, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] forçará a criptografia de todas as conexões. Por padrão, essa opção é 0. |
|**network.tlscert** |O caminho absoluto para o arquivo de certificado que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa para TLS. Exemplo:   `/etc/ssl/certs/mssql.pem` O arquivo de certificado deve ser acessível pela conta MSSQL. A Microsoft recomenda restringir o acesso ao arquivo usando o `chown mssql:mssql <file>; chmod 400 <file>`. |
|**network.tlskey** |O caminho absoluto para o arquivo de chave privada que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa para TLS. Exemplo:  `/etc/ssl/private/mssql.key` O arquivo de certificado deve ser acessível pela conta MSSQL. A Microsoft recomenda restringir o acesso ao arquivo usando o `chown mssql:mssql <file>; chmod 400 <file>`. |
|**network.tlsprotocols** |Uma lista separada por vírgula de quais protocolos TLS são permitidos pelo SQL Server. O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sempre tenta negociar o protocolo mais forte permitido. Se um cliente não der suporte a nenhum protocolo permitido, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] rejeitará a tentativa de conexão.  Para compatibilidade, todos os protocolos compatíveis são permitidos por padrão (1.2, 1.1 e 1.0).  Se os clientes dão suporte ao protocolo TLS 1.2, a Microsoft recomenda que ele seja o único permitido. |
|**network.tlsciphers** |Especifica quais codificações são permitidas pelo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para protocolo TLS. Essa cadeia de caracteres deve ser formatada segundo o [formato de lista de codificação do OpenSSL](https://www.openssl.org/docs/man1.0.2/apps/ciphers.html). Em geral, não é necessário alterar essa opção. <br /> Por padrão, são permitidas as seguintes codificações: <br /> `ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA` |
| **network.kerberoskeytabfile** |Caminho para o arquivo keytab do Kerberos |

Para obter um exemplo de como usar as configurações de protocolo TLS, confira [Criptografar conexões com o SQL Server em Linux](sql-server-linux-encrypted-connections.md).

## <a name="enabledisable-traceflags"></a><a id="traceflags"></a> Habilitar/desabilitar sinalizadores de rastreamento

Essa opção de **sinalizador de rastreamento** habilita ou desabilita o sinalizadores de rastreamento para a inicialização do serviço SQL Server. Para habilitar/desabilitar um sinalizador de rastreamento, use os seguintes comandos:

1. Para habilitar um sinalizador de rastreamento, use o comando a seguir. Por exemplo, para o sinalizador de rastreamento 1234:

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 1234 on
   ```

1. Você pode habilitar vários sinalizadores de rastreamento especificando-os separadamente:

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 2345 3456 on
   ```

1. De modo semelhante, você pode desabilitar um ou mais sinalizadores de rastreamento habilitados, especificando-os e adicionando o parâmetro **off**:

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 1234 2345 3456 off
   ```

1. Reinicie o serviço do SQL Server para aplicar as alterações:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="remove-a-setting"></a>Remover uma configuração

Para remover a definição de qualquer configuração feita com `mssql-conf set`, chame **mssql-conf** com a opção `unset` e o nome da configuração. Isso limpa a configuração, retornando-a efetivamente ao valor padrão.

1. O exemplo a seguir limpa a opção **network.tcpport**.

   ```bash
   sudo /opt/mssql/bin/mssql-conf unset network.tcpport
   ```

1. Reinicie o serviço SQL Server.

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="view-current-settings"></a>Exibir as configurações atuais

Para exibir as configurações definidas, execute o seguinte comando para gerar o conteúdo do arquivo **mssql.conf** como saída:

```bash
sudo cat /var/opt/mssql/mssql.conf
```

Observe que todas as configurações não mostradas neste arquivo estão usando os respectivos valores padrão. A próxima seção fornece um arquivo **mssql.conf** de exemplo.


## <a name="mssqlconf-format"></a><a id="mssql-conf-format"></a> Formato mssql.conf

O arquivo **/var/opt/mssql/mssql.conf** a seguir fornece um exemplo para cada configuração. Você pode usar esse formato para fazer alterações manualmente no arquivo **mssql.conf** conforme necessário. Se você alterar o arquivo manualmente, deverá reiniciar o SQL Server antes que as alterações sejam aplicadas. Para usar o arquivo **mssql.conf** com o Docker, você deverá fazer com que o Docker [persista seus dados](sql-server-linux-configure-docker.md). Primeiro, adicione um arquivo **mssql.conf** completo ao diretório de host e, em seguida, execute o contêiner. Há um exemplo disso nos [Comentários do cliente](sql-server-linux-customer-feedback.md).

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```ini
[EULA]
accepteula = Y

[coredump]
captureminiandfull = true
coredumptype = full

[filelocation]
defaultbackupdir = /var/opt/mssql/data/
defaultdatadir = /var/opt/mssql/data/
defaultdumpdir = /var/opt/mssql/data/
defaultlogdir = /var/opt/mssql/data/

[hadr]
hadrenabled = 0

[language]
lcid = 1033

[memory]
memorylimitmb = 4096

[network]
forceencryption = 0
ipaddress = 10.192.0.0
kerberoskeytabfile = /var/opt/mssql/secrets/mssql.keytab
tcpport = 1401
tlscert = /etc/ssl/certs/mssql.pem
tlsciphers = ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA
tlskey = /etc/ssl/private/mssql.key
tlsprotocols = 1.2,1.1,1.0

[sqlagent]
databasemailprofile = default
errorlogfile = /var/opt/mssql/log/sqlagentlog.log
errorlogginglevel = 7

[telemetry]
customerfeedback = true
userrequestedlocalauditdirectory = /tmp/audit

[traceflag]
traceflag0 = 1204
traceflag1 = 2345
traceflag = 3456
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```ini
[EULA]
accepteula = Y
accepteulaml = Y

[coredump]
captureminiandfull = true
coredumptype = full

[distributedtransaction]
servertcpport = 51999

[filelocation]
defaultbackupdir = /var/opt/mssql/data/
defaultdatadir = /var/opt/mssql/data/
defaultdumpdir = /var/opt/mssql/data/
defaultlogdir = /var/opt/mssql/data/

[hadr]
hadrenabled = 0

[language]
lcid = 1033

[memory]
memorylimitmb = 4096

[network]
forceencryption = 0
ipaddress = 10.192.0.0
kerberoskeytabfile = /var/opt/mssql/secrets/mssql.keytab
rpcport = 13500
tcpport = 1401
tlscert = /etc/ssl/certs/mssql.pem
tlsciphers = ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA
tlskey = /etc/ssl/private/mssql.key
tlsprotocols = 1.2,1.1,1.0

[sqlagent]
databasemailprofile = default
errorlogfile = /var/opt/mssql/log/sqlagentlog.log
errorlogginglevel = 7

[telemetry]
customerfeedback = true
userrequestedlocalauditdirectory = /tmp/audit

[traceflag]
traceflag0 = 1204
traceflag1 = 2345
traceflag = 3456
```

::: moniker-end

## <a name="next-steps"></a>Próximas etapas

Para, em vez disso, usar variáveis de ambiente para fazer algumas dessas alterações de configuração, confira [Definir configurações do SQL Server com variáveis de ambiente](sql-server-linux-configure-environment-variables.md).

Para outras ferramentas e cenários de gerenciamento, confira [Gerenciar o SQL Server em Linux](sql-server-linux-management-overview.md).
