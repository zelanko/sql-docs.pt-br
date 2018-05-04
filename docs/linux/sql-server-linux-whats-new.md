---
title: Novidades do SQL Server de 2017 no Linux | Microsoft Docs
description: Este artigo destaca o que há de novo para 2017 do SQL Server no Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/20/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 456b6f31-6b97-4e31-80ab-b40151ec4868
ms.openlocfilehash: 3d1f841f2ea2e0169aa27cb8ec7853be2e90665e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="whats-new-for-sql-server-2017-on-linux"></a>Novidades do SQL Server 2017 no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo descreve os principais recursos e serviços disponíveis para 2017 do SQL Server em execução no Linux.

> [!NOTE]
> Além dessas capacidades neste artigo, as atualizações cumulativas são lançadas em intervalos regulares após o lançamento. Essas atualizações cumulativas fornecem várias melhorias e correções. Para obter informações sobre a versão mais recente de atualizações Cumulativas, consulte [ http://aka.ms/sql2017cu ](http://aka.ms/sql2017cu). Para baixar os pacotes e problemas conhecidos, consulte o [notas de versão](sql-server-linux-release-notes.md).

## <a name="sql-server-database-engine"></a>Mecanismo de Banco de Dados do SQL Server

- Habilitar os recursos principais do mecanismo de banco de dados do SQL Server.
- Suporte para caminhos nativo do Linux.
- Suporte a IPv6.
- Suporte para os arquivos de banco de dados em NFS.
- Habilitado [segurança de camada transparente](sql-server-linux-encrypted-connections.md) criptografia (TLS).
- Habilitado [autenticação do Active Directory](sql-server-linux-active-directory-authentication.md).
- [Funcionalidade de grupos de disponibilidade](sql-server-linux-availability-group-overview.md) para alta disponibilidade.
- [Pesquisa de texto completo](sql-server-linux-setup-full-text-search.md) suporte.

## <a name="sql-server-agent"></a>SQL Server Agent

- Habilitado [do SQL Server Agent](sql-server-linux-setup-sql-agent.md) suporte para as seguintes tarefas:
  - [Trabalhos de Transact-SQL](sql-server-linux-run-sql-server-agent-job.md)
  - [Email de banco de dados](sql-server-linux-db-mail-sql-agent.md)
  - [Envio de logs](sql-server-linux-use-log-shipping.md)

## <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)

- Capacidade de executar pacotes SSIS no Linux. Para obter mais informações, consulte [configurar o SQL Server Integration Services no Linux com o ssis conf](sql-server-linux-configure-ssis.md).

## <a name="other-improvements"></a>Outros aprimoramentos

- Ferramenta de configuração de linha de comando [mssql conf](sql-server-linux-configure-mssql-conf.md).
- Suporte de instalação autônoma com [variáveis de ambiente](sql-server-linux-configure-environment-variables.md).
- Plataforma cruzada [extensão do Visual Studio Code mssql server](sql-server-linux-develop-use-vscode.md).
- Gerador de script de plataforma cruzada, [scripter mssql](https://github.com/Microsoft/sql-xplat-cli/blob/dev/doc/usage_guide.md).
- Monitor de modo de exibição de gerenciamento dinâmico (DMV) de plataforma cruzada, [ferramenta DBFS](https://github.com/Microsoft/dbfs).

## <a name="next-steps"></a>Próximas etapas

Para instalar o SQL Server no Linux, use um dos seguintes tutoriais:

- [Instalar no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-docker.md)
- [Provisionar uma VM SQL no Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)

Para ver outros aprimoramentos introduzidos no SQL Server 2017, consulte [Novidades no SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md).

> [!TIP]
> Para obter respostas para perguntas frequentes, consulte o [SQL Server nas perguntas frequentes sobre o Linux](sql-server-linux-faq.md).

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
