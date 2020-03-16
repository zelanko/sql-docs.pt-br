---
title: Solução de problemas do SQL Server em Linux
description: Fornece dicas de solução de problemas para usar o SQL Server em Linux.
author: VanMSFT
ms.author: vanto
ms.date: 05/01/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 99636ee8-2ba6-4316-88e0-121988eebcf9S
ms.openlocfilehash: a4103e22facbb717b6797b91d8b218cc6ce4b0b7
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79288110"
---
# <a name="troubleshoot-sql-server-on-linux"></a>Solução de problemas do SQL Server em Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este documento descreve como solucionar problemas do Microsoft SQL Server em execução no Linux ou em um contêiner do Docker. Ao solucionar problemas do SQL Server em Linux, lembre-se de examinar os recursos compatíveis e as limitações conhecidas nas [Notas sobre a versão do SQL Server em Linux](sql-server-linux-release-notes.md).

> [!TIP]
> Para obter respostas a perguntas frequentes, confira as [Perguntas frequentes sobre o SQL Server em Linux](sql-server-linux-faq.md).

## <a id="connection"></a> Solucionar problemas de falhas de conexão
Se você estiver tendo dificuldades para se conectar ao SQL Server em Linux, haverá algumas coisas a serem verificadas.

- Caso não consiga se conectar localmente usando **localhost**, tente usar o endereço IP 127.0.0.1. É possível que o **localhost** não esteja mapeado corretamente para esse endereço.

- Verifique se o nome do servidor ou o endereço IP pode ser acessado no computador cliente.

   > [!TIP]
   > Para localizar o endereço IP de seu computador Ubuntu, execute o comando ifconfig como no seguinte exemplo:
   >
   >   ```bash
   >   sudo ifconfig eth0 | grep 'inet addr'
   >   ```
   > Para o Red Hat, use o endereço IP como no seguinte exemplo:
   >
   >   ```bash
   >   sudo ip addr show eth0 | grep "inet"
   >   ```
   > Uma exceção a essa técnica está relacionada às VMs do Azure. Para VMs do Azure, [localize o IP público da VM no portal do Azure](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine#connect).

- Se aplicável, verifique se você abriu a porta do SQL Server (padrão 1433) no firewall.

- Para VMs do Azure, verifique se você tem uma [regra de grupo de segurança de rede para a porta padrão do SQL Server](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine#remote).

- Verifique se o nome de usuário e a senha não contêm erros de digitação, espaços extras ou uso incorreto de maiúsculas.

- Tente definir explicitamente o protocolo e o número da porta com o nome do servidor, como no seguinte exemplo: **tcp:servername,1433**.

- Problemas de conectividade de rede também podem causar erros de conexão e tempos limite. Depois de verificar as informações de conexão e a conectividade de rede, tente estabelecer a conexão novamente.

## <a name="manage-the-sql-server-service"></a>Gerenciar o serviço SQL Server

As seções a seguir mostram como iniciar, parar, reiniciar e verificar o status do serviço SQL Server.

### <a name="manage-the-mssql-server-service-in-red-hat-enterprise-linux-rhel-and-ubuntu"></a>Gerenciar o serviço mssql-server no RHEL (Red Hat Enterprise Linux) e no Ubuntu 

Verifique o status do serviço SQL Server usando este comando:

   ```bash
   sudo systemctl status mssql-server
   ```

Você pode parar, iniciar ou reiniciar o serviço SQL Server, conforme necessário, usando os seguintes comandos:

   ```bash
   sudo systemctl stop mssql-server
   sudo systemctl start mssql-server
   sudo systemctl restart mssql-server
   ```

### <a name="manage-the-execution-of-the-mssql-docker-container"></a>Gerenciar a execução do contêiner mssql do Docker

Obtenha o status e a ID do contêiner criado mais recentemente do Docker do SQL Server executando o seguinte comando (a ID está abaixo da coluna **CONTAINER ID**):

   ```bash
   sudo docker ps -l
   ```
   
Você pode parar ou reiniciar o serviço SQL Server, conforme necessário, usando os seguintes comandos:
   
   ```bash
   sudo docker stop <container ID>
   sudo docker restart <container ID>
   ```

> [!TIP]
> Para obter mais dicas de solução de problemas para o Docker, confira [Solução de problemas de contêineres do Docker do SQL Server](sql-server-linux-configure-docker.md#troubleshooting).

## <a name="access-the-log-files"></a>Acessar os arquivos de log
   
O mecanismo do SQL Server registra em log o arquivo /var/opt/mssql/log/errorlog nas instalações do Linux e do Docker. Você precisa estar no modo 'superusuário' para procurar arquivos nesse diretório.

O instalador registra-os em log aqui: /var/opt/mssql/setup-<carimbo de data/hora que representa a hora de instalação> Você pode procurar os arquivos de log de erros com qualquer ferramenta compatível com UTF-16, como 'vim' ou 'cat' da seguinte maneira: 

   ```bash
   sudo cat errorlog
   ```

Se preferir, converta também os arquivos em UTF-8 para lê-los com 'more' ou 'less' com o seguinte comando:
   
   ```bash
   sudo iconv -f UTF-16LE -t UTF-8 <errorlog> -o <output errorlog file>
   ```
## <a name="extended-events"></a>Eventos estendidos

Os eventos estendidos podem ser consultados por meio de um comando SQL.  Encontre mais informações sobre eventos estendidos [aqui](https://technet.microsoft.com/library/bb630282.aspx):

## <a name="crash-dumps"></a>Despejos de memória 

Procure despejos no diretório de log do Linux. Verifique no diretório /var/opt/mssql/log os despejos do Linux Core (extensão .tar.gz2) ou minidespejos do SQL (extensão .mdmp)

Para despejos do Core 
   ```bash
   sudo ls /var/opt/mssql/log | grep .tar.gz2 
   ```

Para despejos do SQL 
   ```bash
   sudo ls /var/opt/mssql/log | grep .mdmp 
   ```
   
## <a name="start-sql-server-in-minimal-configuration-or-in-single-user-mode"></a>Iniciar o SQL Server no modo de usuário único ou de configuração mínima

### <a name="start-sql-server-in-minimal-configuration-mode"></a>Iniciar o SQL Server no modo de configuração mínima
Isso será útil se a definição de um valor de configuração (por exemplo, sobrecarga de confirmação de memória) impediu o servidor de ser iniciado.
  
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -f
   ```

### <a name="start-sql-server-in-single-user-mode"></a>Iniciar o SQL Server no modo de usuário único
Em algumas circunstâncias, pode ser necessário iniciar uma instância do SQL Server no modo de usuário único usando a opção de inicialização -m. Por exemplo, você pode querer mudar as opções de configuração de servidor ou recuperar um banco de dados mestre danificado ou outro banco de dados do sistema. Por exemplo, você pode desejar alterar as opções de configuração de servidor ou recuperar um banco de dados mestre danificado ou outro banco de dados do sistema   

Iniciar o SQL Server no modo de usuário único
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -m
   ```

Iniciar o SQL Server no modo de usuário único com o sqlcmd
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -m SQLCMD
   ```
  
> [!WARNING]  
>  Inicie o SQL Server no Linux com o usuário “mssql” para evitar problemas futuros de inicialização. Exemplo: “sudo -u mssql /opt/mssql/bin/sqlservr [STARTUP OPTIONS]” 

Se você tiver iniciado o SQL Server acidentalmente com outro usuário, altere a propriedade de arquivos de banco de dados do SQL Server novamente para o usuário 'mssql' antes de iniciar o SQL Server com systemd. Por exemplo, para alterar a propriedade de todos os arquivos de banco de dados em /var/opt/mssql para o usuário 'mssql', execute o comando a seguir

   ```bash
   chown -R mssql:mssql /var/opt/mssql/
   ```

## <a name="rebuild-system-databases"></a>Recompilar bancos de dados do sistema
Como último recurso, você pode optar por recompilar os bancos de dados mestre e modelo novamente para as versões padrão.

> [!WARNING]
> Estas etapas **EXCLUIRÃO todos os dados do sistema do SQL Server** que você configurou. Isso inclui informações sobre os bancos de dados de usuário (mas não os bancos de dados de usuário propriamente ditos). Isso também excluirá outras informações armazenadas nos bancos de dados do sistema, incluindo as seguintes: informações de chave mestra, todos os certificados carregados no mestre, a senha de logon SA, informações relacionadas ao trabalho do msdb, informações sobre o DB Mail do msdb e opções sp_configure. Use-as apenas se você entender as implicações.

1. Interrompa o SQL Server.

   ```bash
   sudo systemctl stop mssql-server
   ```

1. Execute **sqlservr** com o parâmetro **force-setup**. 

   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr --force-setup
   ```
   
   > [!WARNING]
   > Confira o aviso anterior. Além disso, você precisa executar isso como o usuário **mssql**, conforme mostrado aqui.

1. Depois de ver a mensagem "A recuperação foi concluída", pressione CTRL+C. Isso desligará o SQL Server

1. Reconfigure a senha SA.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set-sa-password
   ```
   
1. Inicie o SQL Server e reconfigure o servidor. Isso inclui a restauração ou a nova anexação de qualquer banco de dados de usuário.

   ```bash
   sudo systemctl start mssql-server
   ```

## <a name="improve-performance"></a>Melhorar o desempenho

Há muitos fatores que afetam o desempenho, incluindo design de banco de dados, hardware e demandas de carga de trabalho. Se desejar melhorar o desempenho, comece examinando as melhores práticas no artigo [Melhores práticas de desempenho e diretrizes de configuração para o SQL Server em Linux](sql-server-linux-performance-best-practices.md). Em seguida, explore algumas das ferramentas disponíveis para solucionar problemas de desempenho.

- [Repositório de Consultas](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)
- [DMVs (exibições de gerenciamento dinâmico) do sistema](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
- [Painel de desempenho no SQL Server Management Studio](https://blogs.msdn.microsoft.com/sql_server_team/new-in-ssms-performance-dashboard-built-in/)

## <a name="common-issues"></a>Problemas comuns

1. Não é possível se conectar à Instância remota do SQL Server.

   Confira a seção de solução de problemas do artigo [Conectar-se ao SQL Server em Linux](#connection).

2. ERRO: O nome do host precisa ter 15 caracteres ou menos.

   Esse é um problema conhecido que ocorre sempre que o nome do computador que está tentando instalar o pacote do Debian do SQL Server tem mais de 15 caracteres. Atualmente, não há soluções alternativas além da alteração do nome do computador. Uma maneira de fazer isso é editando o arquivo do nome do host e reinicializando o computador. O [guia do site](https://www.cyberciti.biz/faq/ubuntu-change-hostname-command/) a seguir explica isso em detalhes.

3. Como redefinir a senha SA (administração do sistema).

   Se você esqueceu a senha SA (administrador do sistema) ou precisa redefini-la por algum outro motivo, siga estas etapas.

   > [!NOTE]
   > As etapas a seguir interrompem o serviço SQL Server temporariamente.

   Faça logon no terminal do host, execute os seguintes comandos e siga os prompts para redefinir a senha SA:

   ```bash
   sudo systemctl stop mssql-server
   sudo /opt/mssql/bin/mssql-conf setup
   ```

4. Como usar caracteres especiais em uma senha.

   Se você usar alguns caracteres na senha de logon do SQL Server, talvez precise fazer escape deles com uma barra invertida quando usá-los em um comando do Linux no terminal. Por exemplo, você precisará fazer escape do cifrão ($) sempre que usá-lo em um script de shell/comando de terminal:

   Não funciona:

   ```bash
   sudo sqlcmd -S myserver -U sa -P Test$$
   ```

   Funciona:

   ```bash
   sqlcmd -S myserver -U sa -P Test\$\$
   ```

   Recursos: [Caracteres especiais](https://tldp.org/LDP/abs/html/special-chars.html)
   [Escape](https://tldp.org/LDP/abs/html/escapingsection.html)

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]
