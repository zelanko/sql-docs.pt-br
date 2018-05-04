---
title: Solucionar problemas do SQL Server no Linux | Microsoft Docs
description: Fornece dicas de solução de problemas para usar o SQL Server 2017 no Linux.
author: annashres
ms.author: anshrest
manager: craigg
ms.date: 04/30/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 99636ee8-2ba6-4316-88e0-121988eebcf9S
ms.openlocfilehash: e699d921a6100c3f8381b4a5ad1ba3054c258961
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="troubleshoot-sql-server-on-linux"></a>Solucionar problemas do SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este documento descreve como solucionar problemas de Microsoft SQL Server em execução no Linux ou em um contêiner do Docker. Ao solucionar problemas do SQL Server no Linux, lembre-se de examinar os recursos com suporte e as limitações conhecidas no [Linux notas de versão do SQL Server](sql-server-linux-release-notes.md).

> [!TIP]
> Para obter respostas para perguntas frequentes, consulte o [SQL Server nas perguntas frequentes sobre o Linux](sql-server-linux-faq.md).

## <a id="connection"></a> Solucionar problemas de falhas de conexão
Se você estiver tendo dificuldade para se conectar ao seu SQL Server do Linux, há algumas coisas para verificar. 

- Verifique se o nome do servidor ou endereço IP acessível a partir do computador cliente.

   > [!TIP]
   > Para localizar o endereço IP do seu computador Ubuntu, você pode executar o comando ifconfig como no exemplo a seguir:
   >
   >   ```bash
   >   sudo ifconfig eth0 | grep 'inet addr'
   >   ```
   > Para o Red Hat, você pode usar o endereço ip, como no exemplo a seguir:
   >
   >   ```bash
   >   sudo ip addr show eth0 | grep "inet"
   >   ```
   > Uma exceção a essa técnica se relaciona com VMs do Azure. Para VMs do Azure, [localizar o IP público para a VM no portal do Azure](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine#connect).

- Se aplicável, verifique que você abriu a porta do SQL Server (padrão 1433) no firewall.

- Para VMs do Azure, verifique se você tem um [regra do grupo de segurança de rede para a porta do SQL Server padrão](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine#remote).

- Verifique se o nome de usuário e a senha não contém quaisquer erros de digitação ou espaços adicionais ou incorretova maiusculas e minúsculas.

- Tente definir explicitamente o número de porta e protocolo com o nome do servidor com o seguinte exemplo: **tcp:servername, 1433**.

- Problemas de conectividade de rede também podem causar tempos limite e erros de conexão. Depois de verificar as informações de conexão e a conectividade de rede, tente novamente a conexão.

## <a name="manage-the-sql-server-service"></a>Gerenciar o serviço SQL Server

As seções a seguir mostram como iniciar, parar, reiniciar e verificar o status do serviço do SQL Server. 

### <a name="manage-the-mssql-server-service-in-red-hat-enterprise-linux-rhel-and-ubuntu"></a>Gerenciar o serviço mssql server no Red Hat Enterprise Linux (RHEL) e no Ubuntu 

Verifique o status do serviço do SQL Server usando este comando:

   ```bash
   sudo systemctl status mssql-server
   ```

Você pode parar, iniciar ou reiniciar o serviço SQL Server conforme necessário usando os seguintes comandos:

   ```bash
   sudo systemctl stop mssql-server
   sudo systemctl start mssql-server
   sudo systemctl restart mssql-server
   ```

### <a name="manage-the-execution-of-the-mssql-docker-container"></a>Gerenciar a execução do contêiner Docker mssql

Você pode obter a ID de status e o contêiner do contêiner do Docker do SQL Server mais recente criado executando o comando a seguir (a ID está sob o **ID de CONTÊINER** coluna):

   ```bash
   sudo docker ps -l
   ```
   
Você pode interromper ou reiniciar o serviço SQL Server, conforme necessário usando os seguintes comandos:
   
   ```bash
   sudo docker stop <container ID>
   sudo docker restart <container ID>
   ```

> [!TIP]
> Para mais dicas de solução de problemas para Docker, consulte [contêineres de solução de problemas Docker do SQL Server](sql-server-linux-configure-docker.md#troubleshooting).

## <a name="access-the-log-files"></a>Acessar os arquivos de log
   
Os logs de mecanismo do SQL Server para o arquivo /var/opt/mssql/log/errorlog nas instalações do Linux e o Docker. Você precisa estar no modo de "superusuário" para procurar esse diretório.

O instalador registra aqui: / var/opt/mssql/instalação-< carimbo de hora que representa o tempo de instalação > você pode procurar os arquivos de log de erros com qualquer ferramenta compatível UTF-16 como 'vim' ou 'cat' esta aparência: 

   ```bash
   sudo cat errorlog
   ```

Se preferir, você também pode converter os arquivos UTF-8 para lê-los com 'mais' ou 'menos' com o seguinte comando:
   
   ```bash
   sudo iconv –f UTF-16LE –t UTF-8 <errorlog> -o <output errorlog file>
   ```
## <a name="extended-events"></a>Eventos estendidos

Eventos estendidos podem ser consultados por meio de um comando SQL.  Para obter mais informações sobre eventos estendidos podem ser encontradas [aqui](https://technet.microsoft.com/en-us/library/bb630282.aspx):

## <a name="crash-dumps"></a>Despejos de memória 

Procure os despejos de memória no diretório de log no Linux. Verifique no diretório /var/opt/mssql/log de despejos de memória do núcleo do Linux (. tar.gz2 extensão) ou SQL minidespejos (extensão. mdmp)

Para dumps principais 
   ```bash
   sudo ls /var/opt/mssql/log | grep .tar.gz2 
   ```

Para despejos de memória do SQL 
   ```bash
   sudo ls /var/opt/mssql/log | grep .mdmp 
   ```
   
## <a name="start-sql-server-in-minimal-configuration-or-in-single-user-mode"></a>Inicie o SQL Server em uma configuração mínima ou em modo de usuário único

### <a name="start-sql-server-in-minimal-configuration-mode"></a>Inicie o SQL Server no modo de configuração mínima
Isso será útil se a definição de um valor de configuração (por exemplo, sobrecarga de confirmação de memória) impediu o servidor de ser iniciado.
  
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -f
   ```

### <a name="start-sql-server-in-single-user-mode"></a>Inicie o SQL Server no modo de usuário único
Em determinadas circunstâncias, pode ser necessário iniciar uma instância do SQL Server no modo de usuário único usando o opção de inicialização -m. Por exemplo, você pode querer mudar as opções de configuração de servidor ou recuperar um banco de dados mestre danificado ou outro banco de dados do sistema. Por exemplo, você talvez queira alterar as opções de configuração de servidor ou recuperar um banco de dados mestre danificado ou outro banco de dados do sistema   

Inicie o SQL Server no modo de usuário único
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -m
   ```

Inicie o SQL Server no modo de usuário único com SQLCMD
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -m SQLCMD
   ```
  
> [!WARNING]  
>  Inicie o SQL Server no Linux com o usuário “mssql” para evitar problemas futuros de inicialização. Exemplo: “sudo -u mssql /opt/mssql/bin/sqlservr [STARTUP OPTIONS]” 

Se você acidentalmente iniciou do SQL Server com outro usuário, você deve alterar a propriedade dos arquivos de banco de dados do SQL Server para o usuário 'mssql' antes de iniciar o SQL Server com systemd. Por exemplo, para alterar a propriedade de todos os arquivos de banco de dados em /var/opt/mssql para o usuário 'mssql', execute o seguinte comando

   ```bash
   chown -R mssql:mssql /var/opt/mssql/
   ```

## <a name="rebuild-system-databases"></a>Recriar bancos de dados do sistema
Como último recurso, você pode escolher recriar o mestre e bancos de dados modelo de volta para versões padrão.

> [!WARNING]
> Essas etapas serão **excluir todos os dados de sistema do SQL Server** que você tenha configurado! Isso inclui informações sobre os bancos de dados do usuário (mas não os usuário próprios bancos de dados). Isso também excluirá outras informações armazenadas nos bancos de dados system, incluindo o seguinte: informações de chave mestra, quaisquer certificados carregados no mestre, a senha de logon de SA, informações relacionada ao trabalho do msdb, informações de email de banco de dados do msdb e opções de sp_configure. Use apenas se você compreender as implicações!

1. Interrompa o SQL Server.

   ```bash
   sudo systemctl stop mssql-server
   ```

1. Executar **sqlservr** com o **Forçar instalação** parâmetro. 

   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr --force-setup
   ```
   
   > [!WARNING]
   > Consulte o aviso anterior! Além disso, você deve executar este como o **mssql** usuário conforme mostrado aqui.

1. Depois de ver a mensagem "A recuperação foi concluída", pressione CTRL + C. Isso desligará do SQL Server

1. Reconfigure a senha de SA.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set-sa-password
   ```
   
1. Iniciar o SQL Server e reconfigurar o servidor. Isso inclui restaurar ou anexar novamente a qualquer banco de dados do usuário.

   ```bash
   sudo systemctl start mssql-server
   ```

## <a name="common-issues"></a>Problemas comuns

1. Você não pode se conectar à instância do SQL Server remota.

   Consulte a seção solução de problemas do artigo, [conectar-se ao SQL Server no Linux](#connection).

2. Erro: O nome do host deve ter 15 caracteres ou menos.

   Este é um problema conhecido que ocorre sempre que o nome do computador que está tentando instalar o pacote Debian do SQL Server é maior do que 15 caracteres. Atualmente, não há nenhuma solução alternativa diferente alterando o nome da máquina. É uma maneira de fazer isso editando o arquivo de nome de host e reinicializar o computador. O seguinte [guia site](http://www.cyberciti.biz/faq/ubuntu-change-hostname-command/) isso explica detalhadamente.

3. Redefinindo a senha de administração (SA) do sistema.

   Se você tiver esquecido a senha de administrador do sistema ou precisa redefini-la por algum outro motivo, siga estas etapas.

   > [!NOTE]
   > As etapas a seguir parar temporariamente o serviço do SQL Server.

   Faça logon no terminal host, execute os seguintes comandos e siga os prompts para redefinir a senha de SA:

   ```bash
   sudo systemctl stop mssql-server
   sudo /opt/mssql/bin/mssql-conf setup
   ```

4. Usar caracteres especiais na senha.

   Se você usar alguns caracteres na senha de logon do SQL Server, você precisará reservá-los com uma barra invertida, quando você usá-los em um comando do Linux no terminal. Por exemplo, você deve substituir o símbolo de cifrão ($) sempre que você usá-lo em um script de shell de comando/terminal:

   Não funciona:

   ```bash
   sudo sqlcmd -S myserver -U sa -P Test$$
   ```

   Como funciona:

   ```bash
   sqlcmd -S myserver -U sa -P Test\$\$
   ```

   Recursos: [caracteres especiais](http://tldp.org/LDP/abs/html/special-chars.html)
   [Escaping](http://tldp.org/LDP/abs/html/escapingsection.html)

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]
