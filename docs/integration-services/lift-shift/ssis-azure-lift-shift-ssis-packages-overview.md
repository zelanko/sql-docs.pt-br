---
title: Comparar e deslocar cargas de trabalho do SQL Server Integration Services para a nuvem | Microsoft Docs
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: dbe6f832d4af55ddd15e12fba17a4da490fe19ae
ms.openlocfilehash: 3d22689e440b2a498f76d43ede74ad3f6f756796
ms.contentlocale: pt-br
ms.lasthandoff: 09/25/2017

---
# <a name="lift-and-shift-sql-server-integration-services-workloads-to-the-cloud"></a>Comparar e deslocar cargas de trabalho do SQL Server Integration Services para a nuvem
Agora você pode mover suas cargas de trabalho e pacotes do SQL Server Integration Services (SSIS) para a nuvem do Azure.
-   Armazenar e gerenciar projetos do SSIS e pacotes do banco de dados do catálogo do SSIS (SSISDB) no banco de dados do SQL Azure.
-   Execute pacotes em uma instância do Azure integração do tempo de execução SSIS, introduzido como parte da versão 2 do Azure Data Factory.
-   Use as ferramentas familiares, como o SQL Server Management Studio (SSMS) para essas tarefas comuns.

## <a name="benefits"></a>Benefícios
Mover suas cargas de trabalho SSIS de local para o Azure tem os seguintes benefícios potenciais:
-   **Reduzir os custos operacionais** , reduzindo a infraestrutura local.
-   **Aumentar a disponibilidade alta** com vários nós por cluster, bem como os recursos de alta disponibilidade do Azure e do banco de dados do SQL Azure.
-   **Aumentar a escalabilidade** com a capacidade de especificar vários núcleos por nó (expandir) e vários nós por cluster (expansão).
-   **Evitar as limitações** da execução de SSIS em máquinas virtuais do Azure.

## <a name="architecture-overview"></a>Visão geral da arquitetura
A tabela a seguir destaca as diferenças entre o SSIS no local e o SSIS no Azure. A diferença mais importante é a separação de armazenamento de computação.

| Armazenamento | Tempo de execução | Escalabilidade |
|---|---|---|
| No local (SQL Server) | Tempo de execução do SSIS hospedado pelo SQL Server | SSIS expansão (no SQL Server 2017 e posterior)<br/><br/>Soluções personalizadas (em versões anteriores do SQL Server) |
| No Azure (banco de dados SQL) | Execução de integração do Azure SSIS, um componente do Azure Data Factory versão 2 | Opções de dimensionamento para IR do SSIS |
| | | |

A fábrica de dados do Azure hospeda o mecanismo de tempo de execução para pacotes do SSIS no Azure. O mecanismo de tempo de execução é chamado de tempo de execução do Azure SSIS Integration (SSIS IV).

Quando você provisiona a IV do SSIS, você pode expandir e expansão especificando valores para as seguintes opções:
-   O tamanho de nó (incluindo o número de núcleos) e o número de nós no cluster.
-   A instância existente do banco de dados SQL Azure para hospedar o banco de dados de catálogo do SSIS (SSISDB) e a camada de serviço para o banco de dados.
-   As execuções paralelas máxima por nó.

Você só precisa provisionar o IV SSIS uma vez. Depois disso, você pode usar ferramentas familiares, como SQL Server Data Tools (SSDT) e o SQL Server Management Studio (SSMS) para implantar, configurar, executar, monitorar, agendar e gerenciar pacotes.

Fábrica de dados também dá suporte a outros tipos de tempos de execução de integração. Para saber mais sobre o IV SSIS e outros tipos de tempos de execução de integração, consulte [tempo de execução da integração do Azure Data Factory](/azure/data-factory/concepts-integration-runtime.md).

## <a name="package-features-on-azure"></a>Recursos do pacote no Azure
Quando você provisionar uma instância do banco de dados SQL para hospedar o SSISDB, o Azure Feature Pack para SSIS e o redistribuível de acesso são instalados. Esses componentes fornecem conectividade para o Excel e acessar arquivos e várias fontes de dados do Azure. Você não pode instalar componentes de terceiros para SSIS neste momento.

Continuar projetar e criar pacotes no local no SSDT, ou no Visual Studio com o SSDT instalado.

Você precisa usar o modelo de implantação de projeto, não o modelo de implantação de pacote, para projetos que você implanta em SSISDB no banco de dados do SQL Azure.

O nome do banco de dados SQL que hospeda o SSISDB torna-se a primeira parte do nome de quatro partes para usar ao implantar e gerenciar pacotes de SSDT e SSMS - `<sql_database_name>.database.windows.net`.

Para obter informações sobre como se conectar a fontes de dados locais da nuvem com autenticação do Windows, consulte [conectar a fontes de dados local com a autenticação do Windows](ssis-azure-connect-with-windows-auth.md).

## <a name="common-tasks"></a>Tarefas comuns

### <a name="provision"></a>Provisionar
Antes de implantar e executar pacotes SSIS no Azure, você precisa provisionar o banco de dados de catálogo do SSISDB e o tempo de execução de integração do Azure SSIS. Siga o provisionamento as etapas neste artigo: [comparar e deslocar pacotes do SQL Server Integration Services (SSIS) para o Azure](/azure/data-factory/quickstart-lift-shift-ssis-packages-powershell.md).

### <a name="deploy-and-run-packages"></a>Implantar e executar pacotes
Para implantar projetos e executar pacotes no banco de dados SQL, você pode usar uma das diversas ferramentas familiares e opções de script:
-   SQL Server Management Studio (SSMS)
-   Transact-SQL (do SSMS, código do Visual Studio ou outra ferramenta)
-   Uma ferramenta de linha de comando
-   PowerShell
-   C# e o modelo de objeto de gerenciamento do SSIS

### <a name="monitor-packages"></a>Pacotes do monitor
Para monitorar pacotes em execução no SSMS, você pode usar uma das seguintes ferramentas para relatórios no SSMS.
-   Clique com botão direito **SSISDB**e, em seguida, selecione **operações ativas** para abrir o **operações ativas** caixa de diálogo.
-   Selecione um pacote no Pesquisador de objetos, clique com botão direito e selecione **relatórios**, em seguida, **relatórios padrão**, em seguida, **todas as execuções**.

### <a name="schedule-packages"></a>Pacotes de agenda
Para agendar a execução de pacotes armazenados no banco de dados SQL, você pode usar as seguintes ferramentas:
-   Local do SQL Server Agent
-   A atividade de procedimento armazenado do Data Factory SQL Server

Para obter mais informações, consulte [SSIS de agendamento de execução de pacote no Azure](ssis-azure-schedule-packages.md).

## <a name="next-steps"></a>Próximas etapas
Para começar com cargas de trabalho SSIS no Azure, consulte os seguintes artigos:
-   [Comparar e deslocar pacotes do SQL Server Integration Services (SSIS) para o Azure](/azure/data-factory/quickstart-lift-shift-ssis-packages-powershell.md)
-   [Implantar, executar e monitorar um pacote do SSIS no Azure](ssis-azure-deploy-run-monitor-tutorial.md)

