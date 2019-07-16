---
title: Configurar configurações do SQL Server no Linux
description: Este artigo descreve como usar a ferramenta mssql-conf para definir configurações do SQL Server no Linux.
author: VanMSFT
ms.author: vanto
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 06798dff-65c7-43e0-9ab3-ffb23374b322
ms.openlocfilehash: ac1f88377b15bf8bd4a92a5dd705716db55deaaf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077598"
---
# <a name="configure-sql-server-on-linux-with-the-mssql-conf-tool"></a>Configurar o SQL Server no Linux com a ferramenta mssql-conf

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

**MSSQL-conf** é um script de configuração que é instalado com o SQL Server 2017 para Red Hat Enterprise Linux, SUSE Linux Enterprise Server e Ubuntu. Você pode usar esse utilitário para definir os seguintes parâmetros:

|||
|---|---|
| [Agente](#agent) | Habilite o SQL Server Agent. |
| [Ordenação](#collation) | Defina um novo agrupamento para o SQL Server no Linux. |
| [Comentários do cliente](#customerfeedback) | Escolha se o SQL Server envia comentários à Microsoft. |
| [Perfil do Database Mail](#dbmail) | Defina o perfil de email do banco de dados padrão para o SQL Server no Linux. |
| [Diretório de dados padrão](#datadir) | Altere o diretório padrão para novos arquivos de dados de banco de dados do SQL Server (. mdf). |
| [Diretório de log padrão](#datadir) | Altera o diretório padrão para novos arquivos de log (. ldf) de banco de dados do SQL Server. |
| [Diretório de banco de dados mestre padrão](#masterdatabasedir) | Altera o diretório padrão para os arquivos de log e banco de dados mestre.|
| [Nome do arquivo de banco de dados mestre padrão](#masterdatabasename) | Altera o nome dos arquivos de banco de dados mestre. |
| [Diretório de despejo padrão](#dumpdir) | Altere o diretório padrão para novos despejos de memória e outros arquivos de solução de problemas. |
| [Diretório de log de erro padrão](#errorlogdir) | Altera o diretório padrão para novos arquivos de log de erros do SQL Server, rastreamento do Profiler padrão, XE de sessão de integridade do sistema e Hekaton sessão XE. |
| [Diretório de backup padrão](#backupdir) | Altere o diretório padrão para novos arquivos de backup. |
| [Tipo de despejo](#coredump) | Escolha o tipo de arquivo de despejo de memória de despejo para coletar. |
| [Alta disponibilidade](#hadr) | Habilite grupos de disponibilidade. |
| [Diretório da auditoria local](#localaudit) | Defina um diretório para adicionar arquivos de auditoria Local. |
| [Localidade](#lcid) | Defina a localidade para o SQL Server usar. |
| [Limite de memória](#memorylimit) | Defina o limite de memória do SQL Server. |
| [Porta TCP](#tcpport) | Altere a porta em que o SQL Server escuta para conexões. |
| [TLS](#tls) | Configure a segurança em nível de transporte. |
| [Sinalizadores de rastreamento](#traceflags) | Defina os sinalizadores de rastreamento que o serviço usará. |

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

**MSSQL-conf** é um script de configuração que é instalado com [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] para Red Hat Enterprise Linux, SUSE Linux Enterprise Server e Ubuntu. Você pode usar esse utilitário para definir os seguintes parâmetros:

|||
|---|---|
| [Agente](#agent) | Habilitar o SQL Server Agent |
| [Ordenação](#collation) | Defina um novo agrupamento para o SQL Server no Linux. |
| [Comentários do cliente](#customerfeedback) | Escolha se o SQL Server envia comentários à Microsoft. |
| [Perfil do Database Mail](#dbmail) | Defina o perfil de email do banco de dados padrão para o SQL Server no Linux. |
| [Diretório de dados padrão](#datadir) | Altere o diretório padrão para novos arquivos de dados de banco de dados do SQL Server (. mdf). |
| [Diretório de log padrão](#datadir) | Altera o diretório padrão para novos arquivos de log (. ldf) de banco de dados do SQL Server. |
| [Diretório de arquivos de banco de dados mestre padrão](#masterdatabasedir) | Altera o diretório padrão para os arquivos de banco de dados mestre na instalação existente do SQL.|
| [Nome do arquivo de banco de dados mestre padrão](#masterdatabasename) | Altera o nome dos arquivos de banco de dados mestre. |
| [Diretório de despejo padrão](#dumpdir) | Altere o diretório padrão para novos despejos de memória e outros arquivos de solução de problemas. |
| [Diretório de log de erro padrão](#errorlogdir) | Altera o diretório padrão para novos arquivos de log de erros do SQL Server, rastreamento do Profiler padrão, XE de sessão de integridade do sistema e Hekaton sessão XE. |
| [Diretório de backup padrão](#backupdir) | Altere o diretório padrão para novos arquivos de backup. |
| [Tipo de despejo](#coredump) | Escolha o tipo de arquivo de despejo de memória de despejo para coletar. |
| [Alta disponibilidade](#hadr) | Habilite grupos de disponibilidade. |
| [Diretório da auditoria local](#localaudit) | Defina um diretório para adicionar arquivos de auditoria Local. |
| [Localidade](#lcid) | Defina a localidade para o SQL Server usar. |
| [Limite de memória](#memorylimit) | Defina o limite de memória do SQL Server. |
| [Coordenador de transações distribuídas da Microsoft](#msdtc) | Configurar e solucionar problemas de MSDTC no Linux. |
| [MLServices EULAs](#mlservices-eula) | Aceite o R e Python EULAs para mlservices pacotes. Aplica-se ao SQL Server de 2019 apenas.|
| [outboundnetworkaccess](#mlservices-outbound-access) |Habilitar o acesso de rede de saída para [mlservices](sql-server-linux-setup-machine-learning.md) extensões de R, Python e Java.|
| [Porta TCP](#tcpport) | Altere a porta em que o SQL Server escuta para conexões. |
| [TLS](#tls) | Configure a segurança em nível de transporte. |
| [Sinalizadores de rastreamento](#traceflags) | Defina os sinalizadores de rastreamento que o serviço usará. |

::: moniker-end

> [!TIP]
> Algumas dessas configurações também podem ser configuradas com variáveis de ambiente. Para obter mais informações, consulte [configurações de configurar o SQL Server com variáveis de ambiente](sql-server-linux-configure-environment-variables.md).

## <a name="usage-tips"></a>Dicas de uso

* Para grupos de disponibilidade AlwaysOn e clusters de discos compartilhados, sempre faça as mesmas alterações de configuração em cada nó.

* Para o cenário de cluster de disco compartilhado, não tente reiniciar o **mssql-server** serviço para aplicar as alterações. SQL Server está em execução como um aplicativo. Em vez disso, coloque o recurso offline e, em seguida, voltar a ficar online.

* Esses exemplos executam mssql-conf especificando o caminho completo: **/opt/mssql/bin/mssql-conf**. Se você optar por navegar para esse caminho, em vez disso, execute o mssql-conf no contexto do diretório atual: **. / mssql-conf**.

## <a id="agent"></a> Habilitar o SQL Server Agent

O **sqlagent.enabled** definindo habilita [SQL Server Agent](sql-server-linux-run-sql-server-agent-job.md). Por padrão, o SQL Server Agent está desabilitado. Se **sqlagent.enabled** não está presente no arquivo de configurações mssql.conf, em seguida, o SQL Server internamente pressupõe que o SQL Server Agent está desabilitado.

Para alterar essa configuração, use as seguintes etapas:

1. Habilite o SQL Server Agent:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
   ```

2. Reinicie o serviço do SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="collation"></a> Alterar o agrupamento do SQL Server

O **agrupamento de conjunto** opção altera o valor de agrupamento para qualquer um dos agrupamentos com suporte.

1. Primeira [fazer backup de bancos de dados de qualquer usuário](sql-server-linux-backup-and-restore-database.md) em seu servidor.

1. Em seguida, use o [sp_detach_db](../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md) procedimento armazenado para desanexar os bancos de dados do usuário.

1. Execute o **agrupamento de conjunto** opção e siga os prompts:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set-collation
   ```

1. O utilitário mssql-conf tentará alterar para o valor de agrupamento especificado e reinicie o serviço. Se houver erros, ele reverterá o agrupamento para o valor anterior.

1. Restaure os backups de banco de dados do usuário.

Para obter uma lista de agrupamentos com suporte, execute as [sys. fn_helpcollations](../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md) função: `SELECT Name from sys.fn_helpcollations()`.

## <a id="customerfeedback"></a> Configurar os comentários dos clientes

O **telemetry.customerfeedback** alterações de configuração, se o SQL Server envia comentários à Microsoft ou não. Por padrão, esse valor é definido como **verdadeira** para todas as edições. Para alterar o valor, execute os seguintes comandos:

> [!IMPORTANT]
> Você pode desligar os comentários dos clientes gratuitamente edições do SQL Server, Express e Developer.

1. Execute o script mssql-conf como raiz com o **definir** comando **telemetry.customerfeedback**. O exemplo a seguir desativa os comentários dos clientes, especificando **falsos**.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false
   ```

1. Reinicie o serviço do SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

Para obter mais informações, consulte [comentários do cliente para o SQL Server no Linux](sql-server-linux-customer-feedback.md) e o [SQL Server Privacy Statement](https://go.microsoft.com/fwlink/?LinkID=868444).

## <a id="datadir"></a> Alterar o local de diretório de dados ou de log padrão

O **filelocation.defaultdatadir** e **filelocation.defaultlogdir** configurações alterar o local onde os novo banco de dados e arquivos de log são criados. Por padrão, esse local é /var/opt/mssql/data. Para alterar essas configurações, use as seguintes etapas:

1. Crie arquivos de log e dados de diretório de destino para o novo banco de dados. O exemplo a seguir cria um novo **/tmp/dados** diretório:

   ```bash
   sudo mkdir /tmp/data
   ```

1. Alterar o proprietário e o grupo do diretório para o **mssql** usuário:

   ```bash
   sudo chown mssql /tmp/data
   sudo chgrp mssql /tmp/data
   ```

1. Use o mssql-conf para alterar o diretório de dados padrão com o **definir** comando:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultdatadir /tmp/data
   ```

1. Reinicie o serviço do SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

1. Agora todos os arquivos de banco de dados para novos bancos de dados criados serão armazenados neste local novo. Se você quiser alterar o local dos arquivos de log (. ldf) de novos bancos de dados, você pode usar o comando "set" seguintes:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultlogdir /tmp/log
   ```

1. Esse comando também pressupõe que um diretório de log/tmp/existe e que está sob o usuário e grupo **mssql**.


## <a id="masterdatabasedir"></a> Alterar o local de diretório do arquivo de banco de dados mestre padrão

O **filelocation.masterdatafile** e **filelocation.masterlogfile** alterações de configuração no local onde o mecanismo do SQL Server procura os arquivos de banco de dados mestre. Por padrão, esse local é /var/opt/mssql/data.

Para alterar essas configurações, use as seguintes etapas:

1. Crie o diretório de destino para novos arquivos de log de erros. O exemplo a seguir cria um novo **masterdatabasedir/tmp/** diretório:

   ```bash
   sudo mkdir /tmp/masterdatabasedir
   ```

1. Alterar o proprietário e o grupo do diretório para o **mssql** usuário:

   ```bash
   sudo chown mssql /tmp/masterdatabasedir
   sudo chgrp mssql /tmp/masterdatabasedir
   ```

1. Usar o mssql-conf para alterar o diretório de banco de dados mestre padrão para os arquivos de log e de dados mestre com o **definir** comando:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterdatafile /tmp/masterdatabasedir/master.mdf
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterlogfile /tmp/masterdatabasedir/mastlog.ldf
   ```

   > [!NOTE]
   > Além de mover os dados mestre e os arquivos de log, isso também move o local padrão para todos os outros bancos de dados do sistema.

1. Interrompa o serviço do SQL Server:

   ```bash
   sudo systemctl stop mssql-server
   ```

1. Mova o Master. mdf e masterlog.ldf:

   ```bash
   sudo mv /var/opt/mssql/data/master.mdf /tmp/masterdatabasedir/master.mdf 
   sudo mv /var/opt/mssql/data/mastlog.ldf /tmp/masterdatabasedir/mastlog.ldf
   ```

1. Inicie o serviço do SQL Server:

   ```bash
   sudo systemctl start mssql-server
   ```

   > [!NOTE]
   > Se o SQL Server não é possível localizar os arquivos mdf e Mastlog no diretório especificado, uma cópia do modelo dos bancos de dados do sistema será automaticamente criada no diretório especificado e do SQL Server será inicializado com êxito. No entanto, metadados, como bancos de dados do usuário, logons de servidor, certificados de servidor, chaves de criptografia, trabalhos do SQL agent ou senha de logon de SA antiga não serão atualizado no novo banco de dados mestre. Você precisará parar o SQL Server e mover seu antigo Master. mdf e Mastlog para o novo local especificado e iniciar o SQL Server para continuar usando os metadados existentes.
 
## <a id="masterdatabasename"></a> Alterar o nome dos arquivos de banco de dados mestre

O **filelocation.masterdatafile** e **filelocation.masterlogfile** alterações de configuração no local onde o mecanismo do SQL Server procura os arquivos de banco de dados mestre. Você também pode usar isso para alterar o nome dos arquivos de log e banco de dados mestres. 

Para alterar essas configurações, use as seguintes etapas:

1. Interrompa o serviço do SQL Server:

   ```bash
   sudo systemctl stop mssql-server
   ```

1. Use o mssql-conf para alterar os nomes de banco de dados mestre esperado para os arquivos de log e de dados mestre com o **definir** comando:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterdatafile /var/opt/mssql/data/masternew.mdf
   sudo /opt/mssql/bin/mssql-conf set filelocation.mastlogfile /var/opt/mssql/data/mastlognew.ldf
   ```

   > [!IMPORTANT]
   > Você só pode alterar o nome do banco de dados mestre e arquivos de log depois que o SQL Server foi iniciado com êxito. Antes da execução inicial, o SQL Server espera que os arquivos a ser denominado Master. mdf e Mastlog.

1. Alterar o nome dos arquivos de dados e de log de banco de dados mestre 

   ```bash
   sudo mv /var/opt/mssql/data/master.mdf /var/opt/mssql/data/masternew.mdf
   sudo mv /var/opt/mssql/data/mastlog.ldf /var/opt/mssql/data/mastlognew.ldf
   ```

1. Inicie o serviço do SQL Server:

   ```bash
   sudo systemctl start mssql-server
   ```

## <a id="dumpdir"></a> Alterar o local do diretório de despejo padrão

O **filelocation.defaultdumpdir** o local padrão onde a memória e despejos de memória do SQL são gerados sempre que houver uma falha de alterações de configuração. Por padrão, esses arquivos são gerados no /var/opt/mssql/log.

Para configurar esse novo local, use os seguintes comandos:

1. Crie o diretório de destino para novos arquivos de despejo. O exemplo a seguir cria um novo **/tmp/despejo** diretório:

   ```bash
   sudo mkdir /tmp/dump
   ```

1. Alterar o proprietário e o grupo do diretório para o **mssql** usuário:

   ```bash
   sudo chown mssql /tmp/dump
   sudo chgrp mssql /tmp/dump
   ```

1. Use o mssql-conf para alterar o diretório de dados padrão com o **definir** comando:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultdumpdir /tmp/dump
   ```

1. Reinicie o serviço do SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="errorlogdir"></a> Alterar o local de diretório de arquivo de log de erro padrão

O **filelocation.errorlogfile** o local onde o novo log de erros, o rastreamento do criador de perfil de padrão, a sessão XE de integridade do sistema e a arquivos de sessão XE Hekaton são criados de alterações de configuração. Por padrão, esse local é /var/opt/mssql/log. O diretório no qual o arquivo de log de erros do SQL será definido se torna o diretório de log padrão para outros logs.

Para alterar essas configurações:

1. Crie o diretório de destino para novos arquivos de log de erros. O exemplo a seguir cria um novo **/tmp/logs** diretório:

   ```bash
   sudo mkdir /tmp/logs
   ```

1. Alterar o proprietário e o grupo do diretório para o **mssql** usuário:

   ```bash
   sudo chown mssql /tmp/logs
   sudo chgrp mssql /tmp/logs
   ```

1. Use o mssql-conf para alterar o nome do arquivo de log de erros padrão com o **definir** comando:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.errorlogfile /tmp/logs/errorlog
   ```

1. Reinicie o serviço do SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```


## <a id="backupdir"></a> Alterar o local do diretório de backup padrão

O **filelocation.defaultbackupdir** o local padrão onde os arquivos de backup são gerados de alterações de configuração. Por padrão, esses arquivos são gerados no /var/opt/mssql/data.

Para configurar esse novo local, use os seguintes comandos:

1. Crie o diretório de destino para novos arquivos de backup. O exemplo a seguir cria um novo **/tmp/backup** diretório:

   ```bash
   sudo mkdir /tmp/backup
   ```

1. Alterar o proprietário e o grupo do diretório para o **mssql** usuário:

   ```bash
   sudo chown mssql /tmp/backup
   sudo chgrp mssql /tmp/backup
   ```

1. Use o mssql-conf para alterar o diretório de backup padrão com o comando "set":

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultbackupdir /tmp/backup
   ```

1. Reinicie o serviço do SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="coredump"></a> Especifique as configurações de despejo de núcleo

Se ocorrer uma exceção em um dos processos do SQL Server, SQL Server cria um despejo de memória.

Há duas opções para controlar o tipo de memória despejos de memória que o SQL Server coleta: **coredump.coredumptype** e **coredump.captureminiandfull**. Elas se relacionam com as duas fases da captura de despejo de núcleo. 

A primeira captura de fase é controlada pelo **coredump.coredumptype** configuração, que determina o tipo de arquivo de despejo gerado durante uma exceção. A segunda fase é habilitado quando o **coredump.captureminiandfull** configuração. Se **coredump.captureminiandfull** é definido como true, o despejo de arquivo especificado por **coredump.coredumptype** é gerado e um segundo minidespejo também é gerado. Definindo **coredump.captureminiandfull** como false desabilita a captura da segunda tentativa.

1. Decida se deseja capturar despejos minidespejos e completos com o **coredump.captureminiandfull** configuração.

    ```bash
    sudo /opt/mssql/bin/mssql-conf set coredump.captureminiandfull <true or false>
    ```

    Padrão: **false**

1. Especifique o tipo de arquivo de despejo com o **coredump.coredumptype** configuração.

    ```bash
    sudo /opt/mssql/bin/mssql-conf set coredump.coredumptype <dump_type>
    ```

    Padrão: **miniplus**

    A tabela a seguir lista os possíveis **coredump.coredumptype** valores.

    | type | Descrição |
    |-----|-----|
    | **mini** | Mini é o menor tipo de arquivo de despejo. Ele usa as informações do sistema Linux para determinar os threads e módulos no processo. O despejo contém somente os módulos e pilhas de threads do ambiente de host. Ele não contém referências à memória indireta ou globais. |
    | **miniplus** | MiniPlus é semelhante a mini, mas ele inclui a memória adicional. Ele compreende as partes internas de SQLPAL e o ambiente de host, adicionando as seguintes regiões de memória para o despejo:</br></br> -Várias referências de globais</br> -Toda a memória acima de 64TB</br> -All chamada regions encontrados no **/proc/.$ pid/mapas**</br> -Memória indireta de threads e pilhas</br> -Informações de thread</br> -Do Teb e do Peb associados</br> -Informações module</br> -Árvore VMM e VAD |
    | **filtered** | Design de filtrado usa uma subtração com base em onde toda a memória do processo está incluída, a menos que especificamente excluído. O design compreende as partes internas de SQLPAL e o ambiente de host, excluindo determinadas regiões de despejo.
    | **full** | Completo um despejo de processo completo que inclui todas as regiões está localizado em **/proc/.$ pid/maps**. Isso não é controlado pelas **coredump.captureminiandfull** configuração. |

## <a id="dbmail"></a> Defina o perfil de email do banco de dados padrão para o SQL Server no Linux

O **sqlpagent.databasemailprofile** permite que você defina o perfil de email de banco de dados padrão para alertas de email.

```bash
sudo /opt/mssq/bin/mssql-conf set sqlagent.databasemailprofile <profile_name>
```
## <a id="hadr"></a> Alta disponibilidade

O **hadr.hadrenabled** opção permite que grupos de disponibilidade na instância do SQL Server. O comando a seguir habilita os grupos de disponibilidade, definindo **hadr.hadrenabled** como 1. Você deve reiniciar o SQL Server para a configuração tenha efeito.

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

Para obter informações sobre como isso é usado com grupos de disponibilidade, consulte os tópicos a seguir.

- [Configurar sempre no grupo de disponibilidade para o SQL Server no Linux](sql-server-linux-availability-group-configure-ha.md)
- [Configurar o grupo de disponibilidade de escala de leitura para o SQL Server no Linux](sql-server-linux-availability-group-configure-rs.md)


## <a id="localaudit"></a> Diretório de conjunto de auditoria local

O **telemetry.userrequestedlocalauditdirectory** configuração habilita a auditoria Local e permite que você defina o diretório onde os logs de auditoria Local é criados.

1. Crie um diretório de destino para novos logs de auditoria Local. O exemplo a seguir cria um novo **auditoria/tmp/** diretório:

   ```bash
   sudo mkdir /tmp/audit
   ```

1. Alterar o proprietário e o grupo do diretório para o **mssql** usuário:

   ```bash
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
   ```

1. Execute o script mssql-conf como raiz com o **definir** comando **telemetry.userrequestedlocalauditdirectory**:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
   ```

1. Reinicie o serviço do SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

Para obter mais informações, consulte [comentários do cliente para o SQL Server no Linux](sql-server-linux-customer-feedback.md).

## <a id="lcid"></a> Alterar a localidade do SQL Server

O **language.lcid** alterações de configuração de localidade do SQL Server a qualquer identificador de idioma com suporte (LCID). 

1. O exemplo a seguir altera a localidade para francês (1036):

   ```bash
   sudo /opt/mssql/bin/mssql-conf set language.lcid 1036
   ```

1. Reinicie o serviço do SQL Server para aplicar as alterações:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="memorylimit"></a> Definir o limite de memória

O **memory.memorylimitmb** determina a quantidade memória física (em MB) disponível para o SQL Server. O padrão é 80% da memória física.

1. Execute o script mssql-conf como raiz com o **definir** comando **memory.memorylimitmb**. O exemplo a seguir altera a memória disponível para o SQL Server para 3,25 GB (3328 MB).

   ```bash
   sudo /opt/mssql/bin/mssql-conf set memory.memorylimitmb 3328
   ```

1. Reinicie o serviço do SQL Server para aplicar as alterações:

   ```bash
   sudo systemctl restart mssql-server
   ```

::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="msdtc"></a> Configurar o MSDTC

O **network.rpcport** e **distributedtransaction.servertcpport** configurações são usadas para configurar o Microsoft Distributed Transaction coordenador (MSDTC). Para alterar essas configurações, execute os seguintes comandos:

1. Execute o script mssql-conf como raiz com o **definir** comando para "network.rpcport":

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.rpcport <rcp_port>
   ```

2. Em seguida, defina a configuração de "distributedtransaction.servertcpport":

   ```bash
   sudo /opt/mssql/bin/mssql-conf set distributedtransaction.servertcpport <servertcpport_port>
   ```

Além de definir esses valores, você também deve configurar o roteamento e atualizar o firewall para a porta 135. Para obter mais informações sobre como fazer isso, consulte [como configurar o MSDTC no Linux](sql-server-linux-configure-msdtc.md).

Há várias outras configurações para o mssql-conf que você pode usar para monitorar e solucionar problemas de MSDTC. A tabela a seguir descreve resumidamente essas configurações. Para obter mais informações sobre seu uso, consulte os detalhes no artigo de suporte do Windows, [como habilitar o rastreamento de diagnóstico para o MS DTC](https://support.microsoft.com/help/926099/how-to-enable-diagnostic-tracing-for-ms-dtc-on-a-windows-based-compute).

| configuração de MSSQL-conf | Descrição |
|---|---|
| distributedtransaction.allowonlysecurerpccalls | Configurar segura somente chamadas RPC para transações distribuídas |
| distributedtransaction.fallbacktounsecurerpcifnecessary | Configurar segurança somente chamadas RPC para distribuído |transações
| distributedtransaction.maxlogsize | Tamanho do arquivo DTC transações log em MB. O padrão é 64MB |
| distributedtransaction.memorybuffersize | Tamanho do buffer circular na qual os rastreamentos são armazenados. Esse tamanho estará em MB e o padrão é 10MB |
| distributedtransaction.servertcpport | Porta do servidor de rpc MSDTC |
| distributedtransaction.trace_cm | Rastreamentos no Gerenciador de conexão |
| distributedtransaction.trace_contact | Rastreia o pool de contato e contatos |
| distributedtransaction.trace_gateway | Fonte de Gateway de rastreamentos |
| distributedtransaction.trace_log | Rastreamento de log |
| distributedtransaction.trace_misc | Rastreamentos que não podem ser categorizados em outras categorias |
| distributedtransaction.trace_proxy | Rastreamentos que são gerados no proxy do MSDTC |
| distributedtransaction.trace_svc | Rastreia a inicialização de arquivo de serviço e .exe |
| distributedtransaction.trace_trace | A própria infra-estrutura de rastreamento |
| distributedtransaction.trace_util | Rotinas de utilitário de rastreamentos que são chamadas de vários locais |
| distributedtransaction.trace_xa | Origem de rastreamento do Gerenciador de transações XA (XATM) |
| distributedtransaction.tracefilepath | Pasta arquivos de rastreamento que devem ser armazenados |
| distributedtransaction.turnoffrpcsecurity | Habilitar ou desabilitar a segurança RPC para transações distribuídas |

::: moniker-end
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="mlservices-eula"></a> Aceitar MLServices EULAs

Adicionando [pacotes de R ou Python de aprendizado de máquina](sql-server-linux-setup-machine-learning.md) ao banco de dados mecanismo requer que você aceite os termos de licenciamento para as distribuições de software livre de R e Python. A tabela a seguir enumera todos os comandos disponíveis ou opções relacionadas ao mlservices EULAs. O mesmo parâmetro de termos de licença é usado para R e Python, dependendo do que você instalou.

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

Você também pode adicionar aceitação do EULA diretamente para o [mssql.conf arquivo](#mssql-conf-format):

```ini
[EULA]
accepteula = Y
accepteulaml = Y
```
:::moniker-end
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="mlservices-outbound-access"></a> Habilitar o acesso de rede de saída

Acesso de rede de saída para as extensões de R, Python e Java na [serviços do SQL Server Machine Learning](sql-server-linux-setup-machine-learning.md) recurso está desabilitado por padrão. Para permitir solicitações de saída, defina "outboundnetworkaccess" propriedade booleana usando mssql-conf.

Depois de definir a propriedade, reinicie o serviço Launchpad do SQL Server para ler os valores atualizados no arquivo INI. Lembra você de uma mensagem de reinicialização sempre que uma configuração de extensibilidade é modificada.

```bash
# Adds the extensibility section and property.
# Sets "outboundnetworkaccess" to true.
# This setting is required if you want to access data or operations off the server.
sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1

# Turns off network access but preserves the setting
/opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 0

# Removes the setting and rescinds network access
sudo /opt/mssql/bin/mssql-conf unset extensibility.outboundnetworkaccess
```

Você também pode adicionar "outboundnetworkaccess" diretamente para o [mssql.conf arquivo](#mssql-conf-format):

```ini
[extensibility]
outboundnetworkaccess = 1
```
:::moniker-end

## <a id="tcpport"></a> Alterar a porta TCP

O **network.tcpport** a porta TCP em que o SQL Server escuta para conexões de alterações de configuração. Por padrão, essa porta é definida para 1433. Para alterar a porta, execute os seguintes comandos:

1. Execute o script mssql-conf como raiz com o comando "set" para "network.tcpport":

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.tcpport <new_tcp_port>
   ```

2. Reinicie o serviço do SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

3. Ao se conectar ao SQL Server agora, você deve especificar a porta personalizada com uma vírgula (,) após o nome do host ou endereço IP. Por exemplo, para se conectar com o SQLCMD, você usaria o seguinte comando:

   ```bash
   sqlcmd -S localhost,<new_tcp_port> -U test -P test
   ```

## <a id="tls"></a> Especifique as configurações de TLS

As opções a seguir configurar TLS para uma instância do SQL Server em execução no Linux.

|Opção |Descrição |
|--- |--- |
|**network.forceencryption** |Se for 1, em seguida, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] força todas as conexões sejam criptografadas. Por padrão, essa opção é 0. |
|**network.tlscert** |O caminho absoluto para o certificado do arquivo que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa para TLS. Exemplo:   `/etc/ssl/certs/mssql.pem`  O arquivo de certificado deve ser acessível pela conta mssql. A Microsoft recomenda restringir o acesso para o arquivo usando `chown mssql:mssql <file>; chmod 400 <file>`. |
|**network.tlskey** |O caminho absoluto para a chave privada do arquivo que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa para TLS. Exemplo:  `/etc/ssl/private/mssql.key`  O arquivo de certificado deve ser acessível pela conta mssql. A Microsoft recomenda restringir o acesso para o arquivo usando `chown mssql:mssql <file>; chmod 400 <file>`. |
|**network.tlsprotocols** |Uma lista separada por vírgulas de quais TLS protocolos são permitidos pelo SQL Server. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sempre tenta negociar o protocolo permitido mais forte. Se um cliente não oferece suporte a qualquer protocolo permitido, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] rejeita a tentativa de conexão.  Para compatibilidade, todos os protocolos com suporte são permitidos por padrão (1.2, 1.1, 1.0).  Se seus clientes de suportam a TLS 1.2, a Microsoft recomenda permitindo que apenas o TLS 1.2. |
|**network.tlsciphers** |Especifica quais codificações são permitidas por [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para TLS. Essa cadeia de caracteres deve ser formatada de acordo [formato de lista de criptografia do OpenSSL](https://www.openssl.org/docs/man1.0.2/apps/ciphers.html). Em geral, não será preciso alterar essa opção. <br /> Por padrão, as seguintes codificações são permitidas: <br /> `ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA` |
| **network.kerberoskeytabfile** |Caminho para o arquivo de keytab do Kerberos |

Para obter um exemplo de como usar as configurações de TLS, consulte [criptografando conexões com o SQL Server no Linux](sql-server-linux-encrypted-connections.md).

## <a id="traceflags"></a> Habilitar/desabilitar sinalizadores de rastreamento

Isso **traceflag** opção habilita ou desabilita os sinalizadores de rastreamento para a inicialização do serviço do SQL Server. Para habilitar/desabilitar um sinalizador de rastreamento use os seguintes comandos:

1. Habilite um sinalizador de rastreamento usando o comando a seguir. Por exemplo, para o sinalizador de rastreamento 1234:

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 1234 on
   ```

1. Você pode habilitar vários sinalizadores de rastreamento, especificando-as separadamente:

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 2345 3456 on
   ```

1. De maneira semelhante, você pode desabilitar uma ou mais sinalizadores de rastreamento habilitados especificando-os e adicionando as **desativar** parâmetro:

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 1234 2345 3456 off
   ```

1. Reinicie o serviço do SQL Server para aplicar as alterações:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="remove-a-setting"></a>Remover uma configuração

Para desativar todas as configurações feitas com `mssql-conf set`, chame **mssql-conf** com o `unset` opção e o nome da configuração. Isso limpa a configuração, efetivamente retorná-lo para seu valor padrão.

1. O exemplo a seguir limpa o **network.tcpport** opção.

   ```bash
   sudo /opt/mssql/bin/mssql-conf unset network.tcpport
   ```

1. Reinicie o serviço SQL Server.

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="view-current-settings"></a>Exibir configurações atuais

Para exibir qualquer configurado configurações, executadas o seguinte comando para exibir o conteúdo do **mssql.conf** arquivo:

```bash
sudo cat /var/opt/mssql/mssql.conf
```

Observe que quaisquer configurações não mostradas nesse arquivo usando seus valores padrão. A próxima seção fornece uma amostra **mssql.conf** arquivo.


## <a id="mssql-conf-format"></a> formato de MSSQL.conf

O seguinte **/var/opt/mssql/mssql.conf** arquivo fornece um exemplo para cada configuração. Você pode usar esse formato manualmente fazer alterações para o **mssql.conf** arquivo conforme necessário. Se você alterar manualmente o arquivo, você deve reiniciar o SQL Server antes que as alterações sejam aplicadas. Para usar o **mssql.conf** arquivo com o Docker, você deve ter o Docker [persistir seus dados](sql-server-linux-configure-docker.md). Primeiro, adicione uma completa **mssql.conf** arquivo ao seu diretório do host e, em seguida, execute o contêiner. Há um exemplo na [comentários dos clientes](sql-server-linux-customer-feedback.md).

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

Em vez de usar variáveis de ambiente para fazer algumas dessas alterações de configuração, consulte [configurações de configurar o SQL Server com variáveis de ambiente](sql-server-linux-configure-environment-variables.md).

Para outros cenários e ferramentas de gerenciamento, consulte [gerenciar o SQL Server no Linux](sql-server-linux-management-overview.md).
