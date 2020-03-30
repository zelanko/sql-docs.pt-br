---
title: Novidades do SQL Server 2017 em Linux
description: Este artigo destaca as novidades do SQL Server 2017 em Linux.
author: VanMSFT
ms.author: vanto
ms.date: 10/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 6874c34c70b562ef726bda5abbda2aebe615cc08
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "72890551"
---
# <a name="whats-new-for-sql-server-2017-on-linux"></a>Novidades do SQL Server 2017 em Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo descreve os principais recursos e serviços disponíveis para o SQL Server 2017 em execução no Linux.

> [!NOTE]
> Além das funcionalidades descritas neste artigo, as atualizações cumulativas são lançadas em intervalos regulares. Essas atualizações cumulativas fornecem várias melhorias e correções. Informações detalhadas sobre a última versão de CU estão disponíveis em [https://aka.ms/sql2017cu](https://aka.ms/sql2017cu). Para saber mais sobre os downloads de pacotes e problemas conhecidos, confira as [Notas sobre a versão](sql-server-linux-release-notes.md).

## <a name="sql-server-database-engine"></a>Mecanismo de Banco de Dados do SQL Server

- Habilitação das funcionalidades principais do Mecanismo de Banco de Dados do SQL Server.
- Suporte para caminhos nativos do Linux.
- Suporte a IPv6.
- Suporte para arquivos de banco de dados no NFS.
- Habilitação da criptografia [TLS](sql-server-linux-encrypted-connections.md).
- Habilitação da [Autenticação do Active Directory](sql-server-linux-active-directory-authentication.md).
- [Funcionalidade de Grupos de Disponibilidade](sql-server-linux-availability-group-overview.md) para alta disponibilidade.
- Suporte à [pesquisa de texto completo](sql-server-linux-setup-full-text-search.md).

## <a name="sql-server-agent"></a>SQL Server Agent

- Habilitação do suporte ao [SQL Server Agent](sql-server-linux-setup-sql-agent.md) nas seguintes tarefas:
  - [Trabalhos Transact-SQL](sql-server-linux-run-sql-server-agent-job.md)
  - [DB Mail](sql-server-linux-db-mail-sql-agent.md)
  - [Envio de logs](sql-server-linux-use-log-shipping.md)

## <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)

- Habilidade de executar pacotes SSIS no Linux. Para obter mais informações, confira [Configurar o SQL Server Integration Services no Linux com ssis-conf](sql-server-linux-configure-ssis.md).

## <a name="other-improvements"></a>Outras melhorias

- Ferramenta de configuração de linha de comando, [mssql-conf](sql-server-linux-configure-mssql-conf.md).
- Suporte à instalação autônoma com [variáveis de ambiente](sql-server-linux-configure-environment-variables.md).
- Extensão multiplataforma [mssql-server do Visual Studio Code](sql-server-linux-develop-use-vscode.md).
- Gerador de script multiplataforma, [mssql-scripter](https://github.com/Microsoft/sql-xplat-cli/blob/dev/doc/usage_guide.md).
- Monitor de DMV (exibição de gerenciamento dinâmico) multiplataforma, [ferramenta DBFS](https://github.com/Microsoft/dbfs).

## <a name="next-steps"></a>Próximas etapas

Para instalar o SQL Server em Linux, use um dos seguintes tutoriais:

- [Instalação no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalação no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-docker.md)
- [Provisionar uma VM SQL no Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)

Para obter respostas a perguntas frequentes, confira as [Perguntas frequentes sobre o SQL Server em Linux](sql-server-linux-faq.md). Para ver outras melhorias introduzidas no SQL Server 2017, confira [Novidades do SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md).

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
