---
title: Solucionar problemas do SQL Server no Linux | Microsoft Docs
description: Fornece dicas de solução de problemas para usar o SQL Server no Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/01/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 99636ee8-2ba6-4316-88e0-121988eebcf9S
ms.openlocfilehash: 6ff0e1eb50f7e7af831ed58b4de05b520fd3f06a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66712859"
---
# <a name="troubleshoot-sql-server-on-linux"></a>Solucionar problemas do SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este documento descreve como solucionar problemas de Microsoft SQL Server em execução no Linux ou em um contêiner do Docker. Ao solucionar problemas do SQL Server no Linux, lembre-se de examinar os recursos com suporte e limitações conhecidas do comando de [SQL Server nas notas de versão do Linux](sql-server-linux-release-notes.md).

> [!TIP]
> Para obter respostas para perguntas frequentes, consulte o [SQL Server nas perguntas frequentes sobre o Linux](sql-server-linux-faq.md).

## <a id="connection"></a> Solucionar problemas de falhas de conexão
Se você estiver tendo dificuldade para se conectar ao SQL Server Linux, há alguns itens a serem verificados.

- Se você não conseguir se conectar localmente usando **localhost**, tente usar o endereço IP 127.0.0.1 em vez disso. É possível que **localhost** não está mapeada corretamente para esse endereço.

- Verifique se o nome do servidor ou endereço IP é acessível em seu computador cliente.

   > [!TIP]
   > Para localizar o endereço IP do seu computador Ubuntu, você pode executar o comando ifconfig como no exemplo a seguir:
   >
   >   ```bash
   >   sudo ifconfig eth0 | grep 'inet addr'
   >   ```
   > Para Red Hat, você pode usar o endereço ip, como no exemplo a seguir:
   >
   >   ```bash
   >   sudo ip addr show eth0 | grep "inet"
   >   ```
   > Uma exceção a essa técnica se relaciona às VMs do Azure. Para VMs do Azure, [localizar o IP público para a VM no portal do Azure](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine#connect).

- Se aplicável, verifique que você abriu a porta do SQL Server (padrão 1433) no firewall.

- Para VMs do Azure, verifique se você tem um [regra de grupo de segurança de rede para a porta do SQL Server padrão](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine#remote).

- Verifique se que o nome de usuário e a senha não contêm erros de digitação ou espaços extras ou incorreta maiusculas e minúsculas.

- Tente definir explicitamente o número de porta e protocolo com o nome do servidor, como o exemplo a seguir: **tcp:servername, 1433**.

- Problemas de conectividade de rede também podem causar tempos limite e erros de conexão. Depois de verificar suas informações de conexão e a conectividade de rede, tente novamente a conexão.

## <a name="manage-the-sql-server-service"></a>Gerenciar o serviço SQL Server

As seções a seguir mostram como iniciar, parar, reiniciar e verificar o status do serviço do SQL Server. 

### <a name="manage-the-mssql-server-service-in-red-hat-enterprise-linux-rhel-and-ubuntu"></a>Gerenciar o serviço mssql-server no Red Hat Enterprise Linux (RHEL) e no Ubuntu 

Verificar o status do serviço do SQL Server usando este comando:

   ```bash
   sudo systemctl status mssql-server
   ```

Você pode parar, iniciar ou reiniciar o serviço SQL Server, conforme necessário usando os seguintes comandos:

   ```bash
   sudo systemctl stop mssql-server
   sudo systemctl start mssql-server
   sudo systemctl restart mssql-server
   ```

### <a name="manage-the-execution-of-the-mssql-docker-container"></a>Gerenciar a execução de contêiner do Docker mssql

Você pode obter a ID de status e o contêiner do contêiner de Docker do SQL Server mais recente criada executando o comando a seguir (a ID está sob o **ID do CONTÊINER** coluna):

   ```bash
   sudo docker ps -l
   ```
   
Você pode parar ou reiniciar o serviço SQL Server, conforme necessário usando os seguintes comandos:
   
   ```bash
   sudo docker stop <container ID>
   sudo docker restart <container ID>
   ```

> [!TIP]
> Para obter mais dicas de solução de problemas para o Docker, consulte [contêineres do Docker do SQL Server de solução de problemas](sql-server-linux-configure-docker.md#troubleshooting).

## <a name="access-the-log-files"></a>Acessar os arquivos de log
   
Os logs do mecanismo do SQL Server para o arquivo /var/opt/mssql/log/errorlog nas instalações do Linux e Docker. Você precisa estar no modo de "superusuário" para procurar esse diretório.

O instalador registra em log aqui: / var/opt/mssql/instalação-< carimbo de hora que representa a hora de instalação > você pode procurar os arquivos de log de erros com qualquer ferramenta compatível de UTF-16 como 'vim' ou 'cat', desta forma: 

   ```bash
   sudo cat errorlog
   ```

Se você preferir, você também pode converter os arquivos em UTF-8 para lê-los com 'mais' ou 'menos' com o seguinte comando:
   
   ```bash
   sudo iconv -f UTF-16LE -t UTF-8 <errorlog> -o <output errorlog file>
   ```
## <a name="extended-events"></a>Eventos estendidos

Eventos estendidos podem ser consultados por meio de um comando SQL.  Para obter mais informações sobre eventos estendidos podem ser encontradas [aqui](https://technet.microsoft.com/library/bb630282.aspx):

## <a name="crash-dumps"></a>Os despejos de memória 

Procure os despejos de memória no diretório de log no Linux. Verifique se há sob o diretório /var/opt/mssql/log despejos de núcleo do Linux (. tar.gz2 extensão) ou SQL minidespejos (extensão. mdmp)

Para despejos de núcleo 
   ```bash
   sudo ls /var/opt/mssql/log | grep .tar.gz2 
   ```

Para despejos de memória do SQL 
   ```bash
   sudo ls /var/opt/mssql/log | grep .mdmp 
   ```
   
## <a name="start-sql-server-in-minimal-configuration-or-in-single-user-mode"></a>Inicie o SQL Server na configuração mínima ou no modo de usuário único

### <a name="start-sql-server-in-minimal-configuration-mode"></a>Inicie o SQL Server no modo de configuração mínima
Isso será útil se a definição de um valor de configuração (por exemplo, sobrecarga de confirmação de memória) impediu o servidor de ser iniciado.
  
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -f
   ```

### <a name="start-sql-server-in-single-user-mode"></a>Inicie o SQL Server no modo de usuário único
Em determinadas circunstâncias, talvez você precise iniciar uma instância do SQL Server no modo de usuário único usando o opção de inicialização -m. Por exemplo, você pode querer mudar as opções de configuração de servidor ou recuperar um banco de dados mestre danificado ou outro banco de dados do sistema. Por exemplo, você talvez queira alterar as opções de configuração de servidor ou recuperar um banco de dados mestre danificado ou outro banco de dados do sistema   

Inicie o SQL Server no modo de usuário único
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -m
   ```

Inicie o SQL Server no modo de usuário único com o SQLCMD
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -m SQLCMD
   ```
  
> [!WARNING]  
>  Inicie o SQL Server no Linux com o usuário “mssql” para evitar problemas futuros de inicialização. Exemplo: “sudo -u mssql /opt/mssql/bin/sqlservr [STARTUP OPTIONS]” 

Se você acidentalmente tiver iniciado o SQL Server com outro usuário, você deve alterar a propriedade dos arquivos de banco de dados do SQL Server para o usuário 'mssql' antes de iniciar o SQL Server com systemd. Por exemplo, para alterar a propriedade de todos os arquivos de banco de dados em /var/opt/mssql para o usuário 'mssql', execute o seguinte comando

   ```bash
   chown -R mssql:mssql /var/opt/mssql/
   ```

## <a name="rebuild-system-databases"></a>Recriar bancos de dados do sistema
Como último recurso, você pode escolher recriar o mestre e bancos de dados modelo de volta para versões padrão.

> [!WARNING]
> Essas etapas serão **excluir todos os dados de sistema do SQL Server** que você tenha configurado! Isso inclui informações sobre seus bancos de dados do usuário (mas não os usuário próprios bancos de dados). Isso também excluirá outras informações armazenadas nos bancos de dados system, incluindo o seguinte: informações de chave mestra, quaisquer certificados carregados no mestre, a senha de logon de SA, as informações relacionadas ao trabalho do msdb, informações sobre o DB Mail do msdb e opções de sp_configure. Use apenas se você compreender as implicações!

1. Pare o SQL Server.

   ```bash
   sudo systemctl stop mssql-server
   ```

1. Execute **sqlservr** com o **Forçar instalação** parâmetro. 

   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr --force-setup
   ```
   
   > [!WARNING]
   > Veja o aviso anterior! Além disso, você deve executá-lo como o **mssql** usuário conforme mostrado aqui.

1. Depois de ver a mensagem "A recuperação foi concluída", pressione CTRL + C. Esse procedimento desligará o SQL Server

1. Reconfigure a senha SA.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set-sa-password
   ```
   
1. Inicie o SQL Server e reconfigurar o servidor. Isso inclui restaurar ou anexar novamente a qualquer banco de dados do usuário.

   ```bash
   sudo systemctl start mssql-server
   ```

## <a name="improve-performance"></a>Melhorar o desempenho

Há muitos fatores que afetam o desempenho, incluindo design de banco de dados, hardware e demandas de carga de trabalho. Se você estiver procurando para melhorar o desempenho, comece revisando as práticas recomendadas neste artigo, [práticas recomendadas de desempenho e diretrizes de configuração do SQL Server no Linux](sql-server-linux-performance-best-practices.md). Em seguida, explore algumas das ferramentas disponíveis para solucionar problemas de desempenho.

- [Repositório de Consultas](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)
- [Exibições de gerenciamento dinâmico (DMVs) do sistema](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
- [Painel de desempenho no SQL Server Management Studio](https://blogs.msdn.microsoft.com/sql_server_team/new-in-ssms-performance-dashboard-built-in/)

## <a name="common-issues"></a>Problemas comuns

1. Você não pode se conectar à instância do SQL Server remota.

   Consulte a seção solução de problemas do artigo [conectar-se ao SQL Server no Linux](#connection).

2. ERRO: Nome do host deve ter 15 caracteres ou menos.

   Isso é um problema conhecido que ocorre sempre que o nome do computador que está tentando instalar o pacote Debian do SQL Server é mais de 15 caracteres. Atualmente, não há nenhuma solução alternativa diferente de alterar o nome da máquina. É uma maneira de fazer isso editando o arquivo de nome de host e reiniciar a máquina. O seguinte [guia de site](https://www.cyberciti.biz/faq/ubuntu-change-hostname-command/) explica isso em detalhes.

3. Redefinindo a senha de administração (SA) do sistema.

   Se você tiver esquecido a senha de SA (administrador) do sistema ou precisa redefini-la por algum outro motivo, siga estas etapas.

   > [!NOTE]
   > As etapas a seguir interromper temporariamente o serviço do SQL Server.

   Faça logon no terminal de host, execute os seguintes comandos e siga os prompts para redefinir a senha SA:

   ```bash
   sudo systemctl stop mssql-server
   sudo /opt/mssql/bin/mssql-conf setup
   ```

4. Usando caracteres especiais na senha.

   Se você usar alguns caracteres na senha de logon do SQL Server, você precisa de escape-los com uma barra invertida quando usá-los em um comando do Linux no terminal. Por exemplo, você deve substituir o símbolo de cifrão ($) a qualquer momento que você usá-lo em um script de shell de comando/terminal:

   Não funciona:

   ```bash
   sudo sqlcmd -S myserver -U sa -P Test$$
   ```

   Como funciona:

   ```bash
   sqlcmd -S myserver -U sa -P Test\$\$
   ```

   Recursos: [Caracteres especiais](https://tldp.org/LDP/abs/html/special-chars.html)
   [Escaping](https://tldp.org/LDP/abs/html/escapingsection.html)

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]
