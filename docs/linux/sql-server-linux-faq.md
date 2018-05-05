---
title: SQL Server no Linux perguntas Frequentes | Microsoft Docs
description: Este artigo fornece respostas para perguntas frequentes sobre o SQL Server em execução no Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/22/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.openlocfilehash: 608a59138f86cf68a9e8311a4c082b15f1179ba5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sql-server-on-linux-frequently-asked-questions-faq"></a>SQL Server no Linux perguntas frequentes (FAQ)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

As seções a seguir fornecem as perguntas e respostas comuns para o SQL Server em execução no Linux.

## <a name="general-questions"></a>Perguntas gerais

1. **Há suporte para quais plataformas Linux?**

   Atualmente há suporte para o SQL Server no Red Hat Enterprise Server, SUSE Linux Enterprise Server e Ubuntu. Ele também tem suporte em execução em um contêiner com o Docker. Para obter as informações mais recentes sobre as versões com suporte, consulte [as plataformas com suporte](sql-server-linux-setup.md#supportedplatforms).

1. **SQL Server no Linux funcionará em outras plataformas**?

   SQL Server é testado e suportado no Linux para as distribuições listadas anteriormente. Outras distribuições de Linux estão intimamente relacionadas e pode ser capazes de executar o SQL Server (por exemplo, CentOS está intimamente relacionado para Red Hat Enterprise Server). Mas se você optar por instalar o SQL Server em um sistema operacional sem suporte, examine o **política de suporte** seção o [política de suporte técnico para o Microsoft SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server) a entender o suporte implicações. Além disso, observe que alguns comunidade mantidos distribuições do Linux não tem uma maneira formal para receber suporte se o sistema operacional subjacente é o problema.

1. **Quais recursos do SQL Server têm suporte no Linux?**

   Para obter uma lista completa de recursos com suporte e problemas conhecidos, consulte o [notas de versão](sql-server-linux-release-notes.md).

1. **Qual é a política de suporte para o SQL Server?**

   Para entender a política de suporte, revise o [política de suporte técnico para o SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server).

1. **Eu estou provenientes de um plano de fundo do Windows SQL Server. Há recursos para ajudar a aprender a usar o SQL Server no Linux?**

   O [início rápido](sql-server-linux-setup.md#platforms) fornecem instruções passo a passo sobre como instalar o SQL Server no Linux e executar consultas Transact-SQL. Outros tutoriais fornecem instruções adicionais sobre como usar o SQL Server no Linux. Para obter uma lista de produtos de terceiros de dicas, consulte o [lista MSSQLTIPS do SQL Server no Linux dicas](https://www.mssqltips.com/sql-server-tip-category/226/sql-server-on-linux/).

## <a name="installation"></a>Instalação

1. **Como faço para SQL Server instalada em meus servidores Linux?**

   A Microsoft mantém repositórios do pacote de instalação do SQL Server e oferece suporte à instalação por meio de gerenciadores de pacotes nativo como yum, zypper e apt. Para instalar rapidamente, consulte um do [início rápido do](sql-server-linux-setup.md#platforms).

1. **Pode instalar o SQL Server no subsistema do Linux para Windows 10?**

   Nenhum. Linux em execução no Windows 10 atualmente não é uma plataforma com suporte do SQL Server e ferramentas relacionadas.

1. **Quais sistemas de arquivos Linux 2017 do SQL Server pode usar arquivos de dados?**

   Atualmente o SQL Server no Linux oferece suporte a ext4 e XFS. Suporte para outros sistemas de arquivos será adicionado conforme necessário no futuro.

1. **Posso baixar os pacotes de instalação para instalar o SQL Server offline?**

   Sim. Para obter mais informações, consulte o pacote de download de links de [notas de versão](sql-server-linux-release-notes.md). Além disso, examine o [instruções para instalações offline](sql-server-linux-setup.md#offline).

1. **Pode executar uma instalação autônoma do SQL Server no Linux?**

   Sim. Para obter uma discussão de instalação autônoma, consulte [orientação de instalação do SQL Server no Linux](sql-server-linux-setup.md#unattended). Consulte os scripts de exemplo para [Red Hat](sample-unattended-install-redhat.md), [SUSE Linux Enterprise Server](sample-unattended-install-suse.md), e [Ubuntu](sample-unattended-install-ubuntu.md). Você também pode analisar [esse script de exemplo](https://blogs.msdn.microsoft.com/sqlcat/2017/10/03/unattended-install-and-configuration-for-sql-server-2017-on-linux/) criado pela equipe de consultoria ao cliente do SQL Server.

## <a name="tools"></a>Ferramentas

1. **Posso usar o cliente do SQL Server Management Studio no Windows para acessar o SQL Server no Linux?**

   Sim, você pode usar as ferramentas existentes que executam o Windows para acessar o SQL Server no Linux. Isso inclui as ferramentas da Microsoft, como SQL Server Management Studio (SSMS), SQL Server Data Tools (SSDT) e sistemas operacionais e as ferramentas de terceiros.

1. **Há uma ferramenta como o SSMS que executa no Linux?**

   O novo Microsoft SQL Operations Studio (preview) é uma ferramenta de plataforma cruzada para o gerenciamento do SQL Server. Para obter mais informações, consulte [o que é o Studio de operações do Microsoft SQL (visualização)](../sql-operations-studio/what-is.md).

1. **Os comandos sqlcmd e bcp estão disponíveis no Linux?**

   Sim, [sqlcmd e bcp](sql-server-linux-setup-tools.md) estão disponíveis no Windows, Linux e macOS nativamente. Além disso, use a nova [scripter mssql](https://github.com/Microsoft/mssql-scripter) ferramenta de linha de comando no Linux, macOS ou Windows para gerar scripts do T-SQL para seu banco de dados SQL em execução em qualquer lugar. Consulte também a visualização de versão do [mssql cli](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/).

1. **É possível exibir o Monitor de atividade quando conectado por meio do SSMS no Windows para uma instância em execução no Linux?**

   Sim, você pode usar o SSMS no Windows para se conectar remotamente, e use ferramentas / recursos, como comandos de Monitor de atividade em uma instância do Linux.

1. **As ferramentas que estão disponíveis para monitorar o desempenho do SQL Server no Linux?**

   Você pode usar [exibições de gerenciamento dinâmico (DMVs) do sistema](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) para coletar vários tipos de informações sobre o SQL Server, incluindo informações de processo do Linux. Você pode usar [repositório de consultas](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md) para melhorar o desempenho da consulta. Outras ferramentas, como o interno [painel de desempenho](https://blogs.msdn.microsoft.com/sql_server_team/new-in-ssms-performance-dashboard-built-in/), trabalhar remotamente no SQL Server Management Studio (SSMS) do Windows.

## <a name="administration"></a>Administração

1. **Microsoft criou um aplicativo como o SQL Server Configuration Manager no Linux?**

   Sim, há uma ferramenta de configuração para o SQL Server no Linux: [mssql conf](sql-server-linux-configure-mssql-conf.md).

1. **SQL Server no Linux oferece suporte a várias instâncias no mesmo host?**

   É recomendável executar vários contêineres em um host para ter várias instâncias distintas. Cada contêiner deve escutar em uma porta diferente. Para obter mais informações, consulte [executar vários contêineres de SQL Server](sql-server-linux-configure-docker.md#run-multiple-sql-server-containers).

1. **Autenticação do Active Directory é suportada no Linux?**

   Sim. Para obter mais informações, consulte [autenticação do Active Directory com o SQL Server no Linux](sql-server-linux-active-directory-authentication.md).

1. **São sempre ligado e clustering com suporte no Linux?**

   Clustering de failover e alta disponibilidade no Linux são obtidos com Pacemaker no Linux. Para obter mais informações, consulte [recuperação de banco de dados e continuidade dos negócios - SQL Server no Linux](sql-server-linux-business-continuity-dr.md).

1. **É possível configurar a replicação do Linux para Windows e vice-versa?**

   Réplicas de escala de leitura podem ser usadas entre o Windows e Linux para replicação de dados unidirecional.

1. **É possível migrar bancos de dados existentes em versões mais antigas do SQL Server do Windows para o Linux?**

   Sim, há [vários métodos](sql-server-linux-migrate-overview.md) de conseguir isso.

1. **Posso migrar meus dados da Oracle e outros mecanismos de banco de dados para o SQL Server no Linux?**

   Sim. O SSMA dá suporte à migração de vários tipos de mecanismos de banco de dados: Microsoft Access, DB2, MySQL, Oracle e SAP ASE (anteriormente conhecida como SAP Sybase ASE). Para obter um exemplo de como usar o SSMA, consulte [migrar um esquema do Oracle para 2017 do SQL Server no Linux com o SQL Server Migration Assistant](../ssma/oracle/sql-server-linux-convert-from-oracle.md?toc=%2fsql%2flinux%2ftoc.json).

1. **Quais permissões são necessárias para arquivos do SQL Server?**

   Todos os arquivos no `/var/opt/mssql` pasta do arquivo deve pertencer a **mssql** usuário e pertencem ao **mssql** grupo. Ambos os **mssql** usuário e grupo devem ter permissões de leitura-gravação de todos os arquivos e diretórios. Observe os seguintes cenários especiais que envolve permissões de arquivo e diretório:

   * Mssql proprietário e grupo são necessárias permissões para compartilhamentos de rede montado que são usados para armazenar arquivos do SQL Server.
   * Se você localizar arquivos de banco de dados ou backups em um diretório diferente do padrão, você também deve definir permissões para aquele diretório.
   * Se você alterar o padrão raiz umask 0022, falha na configuração do SQL Server após a instalação. Em seguida, você deverá aplicar manualmente as permissões necessárias à conta de inicialização do SQL Server.

1. **Pode alterar a propriedade de diretórios e arquivos do SQL Server da conta mssql instalado e grupo?**

   Não oferecemos suporte alterando a propriedade do diretório do SQL Server e os arquivos de instalação padrão. O mssql conta e o grupo é usado especificamente para o SQL Server e sem acesso de logon interativo.

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]
