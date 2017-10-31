---
title: Configurar o SQL Server no Linux | Microsoft Docs
description: "Este tópico descreve como usar a ferramenta mssql conf para definir configurações de 2017 do SQL Server no Linux."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 09/20/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 06798dff-65c7-43e0-9ab3-ffb23374b322
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: 14a7f9cb0f9888339140a226d31368deaf7b32f5
ms.contentlocale: pt-br
ms.lasthandoff: 10/02/2017

---
# <a name="configure-sql-server-on-linux-with-the-mssql-conf-tool"></a>Configurar o SQL Server no Linux com a ferramenta mssql conf

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

**MSSQL conf** é um script de configuração que é instalado com o SQL Server 2017 para Red Hat Enterprise Linux, SUSE Linux Enterprise Server e Ubuntu. Você pode usar esse utilitário para definir os seguintes parâmetros:

|||
|---|---|
| [Agrupamento](#collation) | Defina um novo agrupamento do SQL Server no Linux. |
| [Comentários do cliente](#customerfeedback) | Escolha se ou não o SQL Server envia comentários à Microsoft. |
| [Perfil do Database Mail](#dbmail) | Definir o perfil de email do banco de dados padrão do SQL Server no Linux |
| [Diretório de dados padrão](#datadir) | Altere o diretório padrão para novos arquivos de dados de banco de dados do SQL Server (. mdf). |
| [Diretório de log padrão](#datadir) | Altera o diretório padrão para novos arquivos de log (. ldf) de banco de dados do SQL Server. |
| [Diretório de despejo padrão](#dumpdir) | Altere o diretório padrão para novos despejos de memória e outros arquivos de solução de problemas. |
| [Diretório de backup padrão](#backupdir) | Altere o diretório padrão para novos arquivos de backup. |
| [Tipo de despejo](#coredump) | Escolha o tipo de arquivo de despejo de memória de despejo para coletar. |
| [Alta disponibilidade](#hadr) | Habilite grupos de disponibilidade. |
| [Diretório de auditoria local](#localaudit) | Definir um um diretório para adicionar arquivos de auditoria Local. |
| [Localidade](#lcid) | Defina a localidade para o SQL Server usar. |
| [Limite de memória](#memorylimit) | Defina o limite de memória para o SQL Server. |
| [Porta TCP](#tcpport) | Altere a porta em que o SQL Server escuta para conexões. |
| [TLS](#tls) | Configure a segurança em nível de transporte. |
| [Sinalizadores de rastreamento](#traceflags) | Defina os sinalizadores de rastreamento que o serviço irá usar. |

> [!TIP]
> Algumas dessas configurações também podem ser configuradas com variáveis de ambiente. Para obter mais informações, consulte [as configurações de configurar o SQL Server com variáveis de ambiente](sql-server-linux-configure-environment-variables.md).

## <a name="usage-tips"></a>Dicas de uso

* Para grupos de disponibilidade AlwaysOn e clusters de discos compartilhados, sempre fazer as mesmas alterações de configuração em cada nó.

* Para o cenário de cluster de disco compartilhado, tente reiniciar o **mssql server** serviço para aplicar as alterações. SQL Server está em execução como um aplicativo. Em vez disso, coloque o recurso offline e, em seguida, novamente online.

* Esses exemplos executados mssql-conf por especificam o caminho completo: **/opt/mssql/bin/mssql-conf**. Se você escolher navegar para o caminho em vez disso, execute mssql conf no contexto do diretório atual: **. / conf mssql**.

## <a id="collation"></a>Alterar o agrupamento do SQL Server

O **definir agrupamento** opção altera o valor de agrupamento para qualquer um dos agrupamentos com suporte.

1. Primeiro [qualquer banco de dados de usuário de backup](sql-server-linux-backup-and-restore-database.md) no seu servidor.

1. Em seguida, use o [sp_detach_db](../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md) procedimento armazenado para desanexar os bancos de dados do usuário.

1. Execute o **definir agrupamento** opção e siga as instruções:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set-collation
   ```

1. O utilitário mssql conf tentará alterar para o valor de agrupamento especificado e reinicie o serviço. Se houver erros, ele reverterá o agrupamento para o valor anterior.

1. Restaurar os backups de banco de dados do usuário.

Para obter uma lista de agrupamentos com suporte, execute o [sys. fn_helpcollations](../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md) função: `SELECT Name from sys.fn_helpcollations()`.

## <a id="customerfeedback"></a>Configurar comentários do cliente

O **telemetry.customerfeedback** alterações de configuração, se o SQL Server envia comentários à Microsoft ou não. Por padrão, esse valor é definido como **true**. Para alterar o valor, execute os seguintes comandos:

1. Execute o script mssql conf como raiz com o **definir** comando **telemetry.customerfeedback**. O exemplo a seguir desativa os comentários dos clientes, especificando **false**.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false
   ```

1. Reinicie o serviço do SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

Para obter mais informações, consulte [comentários do cliente para o SQL Server no Linux](sql-server-linux-customer-feedback.md).

## <a id="datadir"></a>Alterar o local padrão de diretório de dados ou de log

O **filelocation.defaultdatadir** e **filelocation.defaultlogdir** configurações alterar o local onde os novo banco de dados e arquivos de log são criados. Por padrão, esse local é /var/opt/mssql/data. Para alterar essas configurações, use as seguintes etapas:

1. Crie o diretório de destino para o novo banco de dados em arquivos de log e dados. O exemplo a seguir cria um novo **/tmp/dados** diretório:

   ```bash
   sudo mkdir /tmp/data
   ```

1. Alterar o proprietário e o grupo do diretório para o **mssql** usuário:

   ```bash
   sudo chown mssql /tmp/data
   sudo chgrp mssql /tmp/data
   ```

1. Use mssql conf para alterar o diretório de dados padrão com o **definir** comando:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultdatadir /tmp/data
   ```

1. Reinicie o serviço do SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

1. Agora, todos os arquivos de banco de dados para novos bancos de dados criados serão armazenados nesse novo local. Se você quiser alterar o local dos arquivos de log (. ldf) de novos bancos de dados, você pode usar o comando "set" seguintes:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultlogdir /tmp/log
   ```

1. Esse comando também presume que existe um diretório de log/tmp, e que está sob o usuário e grupo **mssql**.

## <a id="dumpdir"></a>Alterar o local do diretório de despejo padrão

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

1. Use mssql conf para alterar o diretório de dados padrão com o **definir** comando:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultdumpdir /tmp/dump
   ```

1. Reinicie o serviço do SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="backupdir"></a>Alterar o local do diretório de backup padrão

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

1. Use mssql conf para alterar o diretório de backup padrão com o comando "set":

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultbackupdir /tmp/backup
   ```

1. Reinicie o serviço do SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="coredump"></a>Especifique as configurações de despejo de núcleo

Se ocorrer uma exceção em um dos processos do SQL Server, SQL Server cria um despejo de memória.

Há duas opções para controlar o tipo de memória despejos de memória que o SQL Server coleta: **coredump.coredumptype** e **coredump.captureminiandfull**. Eles se relacionam com as duas fases de captura dump principal. 

A primeira captura fase é controlada pelo **coredump.coredumptype** configuração, que determina o tipo de arquivo de despejo gerado durante uma exceção. A segunda fase é habilitada quando o **coredump.captureminiandfull** configuração. Se **coredump.captureminiandfull** é definido como true, o despejo de arquivo especificado por **coredump.coredumptype** é gerado e um segundo minidespejo também é gerado. Configuração **coredump.captureminiandfull** como false desabilita a captura a segunda tentativa.

1. Decida se deseja capturar completos e minidespejos despejos de memória com o **coredump.captureminiandfull** configuração.

    ```bash
    sudo /opt/mssql/bin/mssql-conf set coredump.captureminiandfull <true or false>
    ```

    Padrão: **false**

1. Especifique o tipo de arquivo de despejo de memória com o **coredump.coredumptype** configuração.

    ```bash
    sudo /opt/mssql/bin/mssql-conf set coredump.coredumptype <dump_type>
    ```

    Padrão: **miniplus**

    A tabela a seguir lista os possíveis **coredump.coredumptype** valores.

    | Tipo | Description |
    |-----|-----|
    | **mini** | Mini é o menor tipo de arquivo de despejo de memória. Ele usa as informações do sistema Linux para determinar os threads e módulos no processo. O despejo contém apenas as pilhas de thread do ambiente de host e os módulos. Ele não contém referências à memória indireta ou globais. |
    | **miniplus** | MiniPlus é semelhante a mini, mas ele inclui memória adicional. Entenda os componentes internos do SQLPAL e do ambiente de host, adicionando as seguintes regiões de memória para o despejo de memória:</br></br> -Várias globais</br> -Toda a memória acima de 64TB</br> -Todas nomeadas regiões encontrados no **/proc/.$ pid/mapas**</br> -Memória indireta de threads e pilhas</br> -Informações do thread</br> -Do Teb e do Peb associados</br> -Informações module</br> -Árvore VMM e VAD |
    | **filtrado** | Design filtrado usa uma subtração com base em onde toda a memória do processo é incluída, a menos que especificamente excluído. O design compreende dos recursos internos do SQLPAL e o ambiente de host, exceto determinadas regiões do despejo de memória.
    | **completo** | Completo é um despejo de processo completo que inclui todas as regiões localizado em **/proc/.$ pid/mapas**. Isso não é controlado pelo **coredump.captureminiandfull** configuração. |

## <a id="dbmail"></a>Definir o perfil de email do banco de dados padrão do SQL Server no Linux

O **sqlpagent.databasemailprofile** permite que você defina o perfil de email de banco de dados padrão para alertas de email.

```bash
sudo /opt/mssq/bin/mssql-conf set sqlagent.databasemailprofile <profile_name>
```
## <a id="hadr"></a>Alta disponibilidade

O **hadr.hadrenabled** opção habilita os grupos de disponibilidade na instância do SQL Server. O comando a seguir habilita os grupos de disponibilidade, definindo **hadr.hadrenabled** como 1. Você deve reiniciar o SQL Server para a configuração entre em vigor.

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

Para informações sobre como isso é usado com grupos de disponibilidade, consulte os tópicos a seguir.

- [Configurar sempre no grupo de disponibilidade para o SQL Server no Linux](sql-server-linux-availability-group-configure-ha.md)
- [Configurar o grupo de disponibilidade de escala de leitura para o SQL Server no Linux](sql-server-linux-availability-group-configure-rs.md)

## <a id="localaudit"></a>Diretório de conjunto de auditoria local

O **telemetry.userrequestedlocalauditdirectory** configuração habilita a auditoria Local e permite que você defina o diretório onde os logs de auditoria Local é criados.

1. Crie um diretório de destino para novos logs de auditoria Local. O exemplo a seguir cria um novo **/tmp/auditoria** diretório:

   ```bash
   sudo mkdir /tmp/audit
   ```

1. Alterar o proprietário e o grupo do diretório para o **mssql** usuário:

   ```bash
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
   ```

1. Execute o script mssql conf como raiz com o **definir** comando **telemetry.userrequestedlocalauditdirectory**:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
   ```

1. Reinicie o serviço do SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

Para obter mais informações, consulte [comentários do cliente para o SQL Server no Linux](sql-server-linux-customer-feedback.md).

## <a id="lcid"></a>Alterar a localidade do SQL Server

O **language.lcid** alterações de configuração de localidade do SQL Server a qualquer identificador de idioma com suporte (LCID). 

1. O exemplo a seguir altera a localidade para o francês (1036):

   ```bash
   sudo /opt/mssql/bin/mssql-conf set language.lcid 1036
   ```

1. Reinicie o serviço do SQL Server para aplicar as alterações:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="memorylimit"></a>Definir o limite de memória

O **memory.memorylimitmb** determina a quantidade memória física (em MB) disponível para o SQL Server. O padrão é 80% da memória física.

1. Execute o script mssql conf como raiz com o **definir** comando **memory.memorylimitmb**. O exemplo a seguir altera a memória disponível para o SQL Server para 3,25 GB (3328 MB).

   ```bash
   sudo /opt/mssql/bin/mssql-conf set memory.memorylimitmb 3328
   ```

1. Reinicie o serviço do SQL Server para aplicar as alterações:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="tcpport"></a>Alterar a porta TCP

O **network.tcpport** a porta TCP em que o SQL Server escuta para conexões de alterações de configuração. Por padrão, essa porta é definida como 1433. Para alterar a porta, execute os seguintes comandos:

1. Execute o script de conferência mssql como raiz com o comando "set" para "network.tcpport":

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.tcpport <new_tcp_port>
   ```

1. Reinicie o serviço do SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

1. Ao conectar ao SQL Server, você deve especificar a porta personalizada com uma vírgula (,) após o nome do host ou endereço IP. Por exemplo, para conectar-se com o SQLCMD, você usaria o seguinte comando:

   ```bash
   sqlcmd -S localhost,<new_tcp_port> -U test -P test
   ```

## <a id="tls"></a>Especificar configurações de TLS

As opções a seguir configurar TLS para uma instância do SQL Server em execução no Linux.

|Opção |Description |
|--- |--- |
|**Network.forceencryption** |Se for 1, em seguida, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] força todas as conexões sejam criptografados. Por padrão, essa opção é 0. |
|**Network.tlscert** |O caminho absoluto para o certificado do arquivo que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa para TLS. Exemplo: `/etc/ssl/certs/mssql.pem` o arquivo de certificado deve ser acessível pela conta mssql. A Microsoft recomenda restringir o acesso ao arquivo usando `chown mssql:mssql <file>; chmod 400 <file>`. |
|**Network.tlskey** |O caminho absoluto para a chave privada do arquivo que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa para TLS. Exemplo: `/etc/ssl/private/mssql.key` o arquivo de certificado deve ser acessível pela conta mssql. A Microsoft recomenda restringir o acesso ao arquivo usando `chown mssql:mssql <file>; chmod 400 <file>`. |
|**Network.tlsprotocols** |Uma lista separada por vírgulas de quais TLS protocolos são permitidos pelo SQL Server. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]sempre tenta negociar o protocolo permitido mais forte. Se um cliente não oferece suporte a qualquer protocolo permitido, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] rejeitará a tentativa de conexão.  Para compatibilidade, todos os protocolos com suporte são permitidos por padrão (1.2, 1.1 e 1.0).  Se os clientes oferecem suporte a TLS 1.2, a Microsoft recomenda permitindo que apenas o protocolo TLS 1.2. |
|**Network.tlsciphers** |Especifica quais codificações são permitidas por [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para TLS. Essa cadeia de caracteres deve ser formatada por [formato de lista de codificação do OpenSSL](https://www.openssl.org/docs/man1.0.2/apps/ciphers.html). Em geral, você não precisará alterar essa opção. <br /> Por padrão, as seguintes codificações são permitidas: <br /> `ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA` |
| **Network.kerberoskeytabfile** |Caminho para o arquivo keytab Kerberos |

Para obter um exemplo de como usar as configurações de TLS, consulte [criptografando conexões com o SQL Server no Linux](sql-server-linux-encrypted-connections.md).

## <a id="traceflags"></a>Habilitar/desabilitar sinalizadores de rastreamento

Isso **traceflag** opção habilita ou desabilita os sinalizadores de rastreamento para a inicialização do serviço do SQL Server. Para ativar/desativar um sinalizador de rastreamento use os seguintes comandos:

1. Habilite um sinalizador de rastreamento usando o comando a seguir. Por exemplo, para o sinalizador de rastreamento 1234:

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 1234 on
   ```

1. Você pode habilitar vários sinalizadores de rastreamento especificando-os separadamente:

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 2345 3456 on
   ```

1. De maneira semelhante, você pode desabilitar um ou mais sinalizadores de rastreamento habilitados especificando-os e adicionando o **off** parâmetro:

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 1234 2345 3456 off
   ```

1. Reinicie o serviço do SQL Server para aplicar as alterações:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="remove-a-setting"></a>Remover uma configuração

Para desativar todas as configurações feitas com `mssql-conf set`, chame **mssql conf** com o `unset` opção e o nome da configuração. Isso limpa a configuração, efetivamente retorná-lo ao seu valor padrão.

1. O exemplo a seguir limpa o **network.tcpport** opção.

   ```bash
   sudo /opt/mssql/bin/mssql-conf unset network.tcpport
   ```

1. Reinicie o serviço do SQL Server.

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="view-current-settings"></a>Exibir configurações atuais

Para exibir qualquer configurado configurações, executadas o seguinte comando para gerar o conteúdo do **mssql.conf** arquivo:

```bash
sudo cat /var/opt/mssql/mssql.conf
```

Observe que as configurações não são mostradas neste arquivo estão usando seus valores padrão. A próxima seção fornece um exemplo de **mssql.conf** arquivo.

## <a name="mssqlconf-format"></a>formato de MSSQL.conf

O seguinte **/var/opt/mssql/mssql.conf** arquivo fornece um exemplo para cada configuração. Você pode usar esse formato para alterar manualmente para o **mssql.conf** arquivo conforme necessário. Se você alterar manualmente o arquivo, você deve reiniciar o SQL Server antes que as alterações sejam aplicadas. Para usar o **mssql.conf** arquivo com o Docker, você deve ter Docker [persistir os dados](sql-server-linux-configure-docker.md). Primeiro, adicione uma completa **mssql.conf** de arquivo para o diretório de host e, em seguida, executar o contêiner. Um exemplo no [comentários dos clientes](sql-server-linux-customer-feedback.md).

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

## <a name="next-steps"></a>Próximas etapas

Em vez de usar variáveis de ambiente para fazer algumas dessas alterações de configuração, consulte [as configurações de configurar o SQL Server com variáveis de ambiente](sql-server-linux-configure-environment-variables.md).

Para outros cenários e ferramentas de gerenciamento, consulte [gerenciar o SQL Server no Linux](sql-server-linux-management-overview.md).

