---
title: Perguntas frequentes sobre o SQL Server em Linux
description: Este artigo fornece respostas para as perguntas frequentes sobre o SQL Server em execução no Linux.
author: VanMSFT
ms.author: vanto
ms.date: 10/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 4fe5ea36b2e60a3a0531e247acc303b70e0db801
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "72929902"
---
# <a name="sql-server-on-linux-frequently-asked-questions-faq"></a>Perguntas frequentes sobre o SQL Server em Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

As seções a seguir fornecem perguntas e respostas comuns sobre o SQL Server em execução no Linux.

## <a name="general-questions"></a>Perguntas gerais

1. **Quais plataformas Linux são compatíveis?**

   No momento, o SQL Server é compatível com Red Hat Enterprise Server, SUSE Linux Enterprise Server e Ubuntu. Ele também é compatível quando em execução em um contêiner com o Docker. Para obter as informações mais recentes sobre as versões compatíveis, confira [Plataformas com suporte](sql-server-linux-setup.md#supportedplatforms).

1. **O SQL Server em Linux funcionará em outras plataformas**?

   O SQL Server é testado e compatível no Linux para as distribuições listadas anteriormente. Outras distribuições do Linux estão fortemente relacionadas e podem ser capazes de executar o SQL Server (por exemplo, o CentOS está fortemente relacionado ao Red Hat Enterprise Server). Porém, se você optar por instalar o SQL Server em um sistema operacional sem suporte, confira a seção **Política de suporte** da [Política de suporte técnico para Microsoft SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server) para entender as implicações de suporte. Observe também que algumas distribuições do Linux mantidas pela comunidade não terão uma maneira formal de receber suporte se o sistema operacional subjacente for o problema.

1. **O SQL Server em Linux é o mesmo que no Windows?**

   O Mecanismo de Banco de Dados principal para o SQL Server é o mesmo no Linux e no Windows. No entanto, atualmente não há suporte para alguns recursos no Linux. Para obter uma lista de recursos que não têm suporte no Linux, confira os [Recursos e serviços sem suporte](sql-server-linux-editions-and-components-2019.md#Unsupported). Leia também os [Problemas conhecidos](sql-server-linux-release-notes.md#known-issues). A menos que especificado nessas listas, outros recursos e serviços do SQL Server têm suporte no Linux.

1. **Qual é a política de suporte para o SQL Server?**

   Para entender a política de suporte, leia a [Política de suporte técnico para o SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server).

1. **Tenho experiência prévia com o Windows SQL Server. Há recursos para ajudar a aprender a usar o SQL Server em Linux?**

   Os [guias de início rápido](sql-server-linux-setup.md#platforms) fornecem instruções passo a passo sobre como instalar o SQL Server em Linux e executar consultas Transact-SQL. Outros tutoriais fornecem instruções adicionais sobre como usar o SQL Server em Linux. Para obter uma lista de dicas de terceiros, confira a [Lista da MSSQLTIPS de dicas sobre o SQL Server em Linux](https://www.mssqltips.com/sql-server-tip-category/226/sql-server-on-linux/).

## <a name="licensing"></a>Licenciamento

1. **Como funciona o licenciamento no Linux?**

   O SQL Server é licenciado da mesma forma para Windows e Linux. Na verdade, você licencia o SQL Server e, em seguida, pode optar por usar essa licença na plataforma de sua escolha. Para saber mais, confira [Como licenciar o SQL Server](https://www.microsoft.com/sql-server/sql-server-2017-pricing).

1. **Qual edição do SQL Server devo escolher quando já o comprei?**

   Ao executar a instalação de mssql-conf, você verá as seguintes opções:
   
   ```
   Choose an edition of SQL Server:
      1. Evaluation (free, no production use rights, 180-day limit)
      2. Developer (free, no production use rights)
      3. Express (free)
      4. Web (PAID)
      5. Standard (PAID)
      6. Enterprise (PAID)
      7. Enterprise Core (PAID)
      8. I bought a license through a retail sales channel and have a product key to enter.
   ```
     
   Se você tiver obtido sua licença por meio do licenciamento por volume como parte de um Contrato Enterprise ou por meio de sua assinatura do MSDN, será necessário selecionar as opções 4 a 7. Esta etapa não solicita que você insira a licença, mas você deve ter adquirido anteriormente a licença apropriada para sua configuração. Se você comprou a Standard Edition por meio de um canal de varejo, selecione a opção 8. Essa opção solicita que você insira uma chave. 

1. **Como faço para verificar a versão e a edição instaladas do SQL Server em Linux?**

   Conecte-se à instância do SQL Server com uma ferramenta de cliente como **sqlcmd**, **mssql-cli** ou Visual Studio Code. Em seguida, execute a seguinte consulta Transact-SQL para verificar a versão e a edição do SQL Server que você está executando: 

   ```sql
   SELECT @@VERSION
   SELECT SERVERPROPERTY('Edition')
   ```

## <a name="installation"></a>Instalação

1. **Como faço para obter o SQL Server instalado em meus servidores Linux?**

   A Microsoft mantém repositórios de pacotes para instalação do SQL Server e dá suporte à instalação por meio de gerenciadores de pacotes nativos, como yum, zypper e apt. Para instalar rapidamente, confira um dos [guias de início rápido](sql-server-linux-setup.md#platforms).

1. **Posso instalar o SQL Server no subsistema Linux para Windows 10?**

   Não. O Linux em execução no Windows 10 não é uma plataforma com suporte no momento para o SQL Server e ferramentas relacionadas.

1. **Quais sistemas de arquivos do Linux o SQL Server pode usar para arquivos de dados?**

   Atualmente, o SQL Server em Linux dá suporte a ext4 e XFS. O suporte para outros sistemas de arquivos será adicionado conforme necessário no futuro.

1. **Posso baixar os pacotes de instalação para instalar o SQL Server offline?**

   Sim. Para obter mais informações, confira os links de download do pacote nas [Notas sobre a versão](sql-server-linux-release-notes.md). Além disso, leia as [instruções para instalações offline](sql-server-linux-setup.md#offline).

1. **Posso executar uma instalação autônoma do SQL Server em Linux?**

   Sim. Para obter uma discussão sobre a instalação autônoma, confira [Orientação de instalação do SQL Server em Linux](sql-server-linux-setup.md#unattended). Confira os scripts de exemplo [Red Hat](sample-unattended-install-redhat.md), [SUSE Linux Enterprise Server](sample-unattended-install-suse.md) e [Ubuntu](sample-unattended-install-ubuntu.md). Você também pode ler [este script de exemplo](https://blogs.msdn.microsoft.com/sqlcat/2017/10/03/unattended-install-and-configuration-for-sql-server-2017-on-linux/) criado pela equipe de consultoria do cliente SQL Server.

## <a name="tools"></a>Ferramentas

1. **Posso usar o cliente SQL Server Management Studio no Windows para acessar o SQL Server em Linux?**

   Sim, você pode usar todas as ferramentas existentes que são executadas no Windows para acessar SQL Server em Linux. Elas incluem ferramentas da Microsoft, como SSMS (SQL Server Management Studio), SSDT (SQL Server Data Tools) e ferramentas de terceiros e OSS.

1. **Existe uma ferramenta como o SSMS que é executada no Linux?**

   O novo Azure Data Studio é uma ferramenta multiplataforma para gerenciamento do SQL Server. Para obter mais informações, confira [O que é o Azure Data Studio](../azure-data-studio/what-is.md).

1. **Comandos como sqlcmd e bcp estão disponíveis no Linux?**

   Sim, [sqlcmd e bcp](sql-server-linux-setup-tools.md) estão disponíveis nativamente no Linux, no macOS e no Windows. Além disso, use a nova ferramenta de linha de comando [mssql-scripter](https://github.com/Microsoft/mssql-scripter) no Linux, no macOS ou no Windows para gerar scripts T-SQL para seu Banco de Dados SQL em execução em qualquer lugar. Além disso, confira a versão prévia para [mssql-cli](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/).

1. **É possível exibir o Monitor de Atividade quando conectado por meio do SSMS no Windows para uma instância em execução no Linux?**

   Sim, você pode usar o SSMS no Windows para se conectar remotamente e usar ferramentas/recursos, como comandos do Monitor de Atividade em uma instância do Linux.

1. **Quais ferramentas estão disponíveis para monitorar o desempenho do SQL Server em Linux?**

   Você pode usar [DMVs (exibições de gerenciamento dinâmico do sistema)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) para coletar vários tipos de informações sobre o SQL Server, incluindo informações de processo do Linux. Você pode usar o [Repositório de Consultas](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md) para melhorar o desempenho da consulta. Outras ferramentas, como o [Painel de Desempenho](https://blogs.msdn.microsoft.com/sql_server_team/new-in-ssms-performance-dashboard-built-in/) interno, funcionam remotamente no SSMS (SQL Server Management Studio) do Windows.

   > [!TIP]
   > Uma forma de melhorar o desempenho é configurar corretamente o sistema operacional Linux e a instância do SQL Server. Para obter mais informações, confira [Práticas recomendadas de desempenho e diretrizes de configuração do SQL Server em Linux](sql-server-linux-performance-best-practices.md).

## <a name="administration"></a>Administração

1. **A Microsoft criou um aplicativo como o SQL Server Configuration Manager no Linux?**

   Sim, há uma ferramenta de configuração para o SQL Server em Linux: [mssql-conf](sql-server-linux-configure-mssql-conf.md).

1. **O SQL Server em Linux dá suporte a várias instâncias no mesmo host?**

   É recomendável executar vários contêineres em um host para ter várias instâncias distintas. Isso é facilmente obtido usando o Docker, mas cada contêiner precisa escutar em uma porta diferente. Para obter mais informações, confira [Executar vários contêineres de SQL Server](sql-server-linux-configure-docker.md#run-multiple-sql-server-containers).

1. **Há suporte para a Autenticação do Active Directory no Linux?**

   Sim. Para obter mais informações, confira [Autenticação do Active Directory com o SQL Server em Linux](sql-server-linux-active-directory-authentication.md).

1. **Há suporte para Always On e clustering no Linux?**

   O clustering de failover e a alta disponibilidade no Linux são obtidos com o Pacemaker no Linux. Para obter mais informações, confira [Recuperação de banco de dados e continuidade dos negócios – SQL Server em Linux](sql-server-linux-business-continuity-dr.md).

1. **É possível configurar a replicação do Linux para o Windows e vice-versa?**

   As réplicas de escala de leitura podem ser usadas entre o Windows e o Linux para replicação de dados unidirecional.

1. **É possível migrar bancos de dados existentes em versões mais antigas do SQL Server do Windows para o Linux?**

   Sim, há [vários métodos](sql-server-linux-migrate-overview.md) de conseguir isso.

1. **Posso migrar meus dados do Oracle e de outros mecanismos de banco de dados para o SQL Server em Linux?**

   Sim. O SSMA dá suporte à migração de vários tipos de mecanismos de banco de dados: Microsoft Access, DB2, MySQL, Oracle e SAP ASE (antigo SAP Sybase ASE). Para obter um exemplo de como usar o SSMA, confira [Migrar um esquema do Oracle para o SQL Server em Linux com o Assistente de Migração do SQL Server](../ssma/oracle/sql-server-linux-convert-from-oracle.md?toc=/sql/toc/toc.json).

1. **Quais permissões são necessárias para arquivos do SQL Server?**

   Todos os arquivos na pasta de arquivos `/var/opt/mssql` devem pertencer ao usuário **mssql** e pertencer ao grupo **mssql**. O usuário e o grupo **mssql** devem ter permissões de leitura/gravação de todos os arquivos e diretórios. Observe os seguintes cenários especiais envolvendo permissões de arquivo e diretório:

   * As permissões para o proprietário e o grupo do mssq são necessárias para compartilhamentos de rede montados que são usados para armazenar arquivos do SQL Server.
   * Se você localizar arquivos de banco de dados ou backups em um diretório não padrão, também deverá definir permissões para esse diretório.
   * Se você alterar o a máscara raiz padrão de 0022, a configuração do SQL Server falhará após a instalação. Você precisa aplicar manualmente as permissões necessárias para a conta de inicialização do SQL Server.

1. **Posso alterar a propriedade de arquivos e diretórios do SQL Server da conta e do grupo do mssql instalado?**

   Não há suporte para alterar a propriedade do diretório e dos arquivos do SQL Server da instalação padrão. A conta e o grupo do mssql são usados especificamente para o SQL Server e não têm acesso de logon interativo.

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]
