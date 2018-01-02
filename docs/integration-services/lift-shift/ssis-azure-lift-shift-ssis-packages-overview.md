---
title: Migrar cargas de trabalho do SQL Server Integration Services por lift-and-shift para a nuvem | Microsoft Docs
ms.date: 10/31/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: lift-shift
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f1fd45ef05d5469acb83a80e3463329976b9a843
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="lift-and-shift-sql-server-integration-services-workloads-to-the-cloud"></a>Migrar cargas de trabalho do SQL Server Integration Services por lift-and-shift para a nuvem
Agora você pode mover suas cargas de trabalho e pacotes do SQL Server Integration Services (SSIS) para a nuvem do Azure.
-   Armazenar e gerenciar projetos do SSIS e pacotes no SSISDB (banco de dados do catálogo do SSIS) no Banco de Dados SQL do Azure.
-   Execute pacotes em uma instância do Azure SSIS Integration Runtime, introduzido como parte da versão 2 do Azure Data Factory.
-   Use as ferramentas familiares, como o SSMS (SQL Server Management Studio) para essas tarefas comuns.

## <a name="benefits"></a>Benefícios
Mover suas cargas de trabalho SSIS de local para o Azure tem os seguintes benefícios potenciais:
-   **Redução dos custos operacionais** e redução da carga de gerenciar a infraestrutura que você tem ao executar o SSIS localmente ou em máquinas virtuais do Azure.
-   **Aumento da alta disponibilidade** com a capacidade de especificar vários nós por cluster, bem como os recursos de alta disponibilidade do Azure e do Banco de Dados SQL do Azure.
-   **Aumento da escalabilidade** com a capacidade de especificar vários núcleos por nó (expandir verticalmente) e vários nós por cluster (expansão).

## <a name="architecture-overview"></a>Visão geral de arquitetura
A tabela a seguir destaca as diferenças entre o SSIS local e o SSIS no Azure. A diferença mais importante é a separação do armazenamento da computação.

| Armazenamento | Tempo de execução | Escalabilidade |
|---|---|---|
| Localmente (SQL Server) | Tempo de execução do SSIS hospedado pelo SQL Server | SSIS Scale Out (no SQL Server 2017 e posterior)<br/><br/>Soluções personalizadas (em versões anteriores do SQL Server) |
| No Azure (Banco de Dados SQL) | Azure SSIS Integration Runtime, um componente do Azure Data Factory versão 2 | Opções de dimensionamento para IR do SSIS |
| | | |

O Azure Data Factory hospeda o mecanismo de tempo de execução para pacotes do SSIS no Azure. O mecanismo de tempo de execução é chamado de Azure SSIS IR (SSIS Integration Runtime).

Quando você provisiona o SSIS IR, você pode expandir vertical e horizontalmente especificando valores para as seguintes opções:
-   O tamanho de nó (incluindo o número de núcleos) e o número de nós no cluster.
-   A instância existente do Banco de Dados SQL do Azure para hospedar o SSISDB (banco de dados de catálogo do SSIS) e a camada de serviço para o banco de dados.
-   O número máximo de execuções paralelas por nó.

Você só precisa provisionar o SSIS IR uma vez. Depois disso, você pode usar ferramentas familiares, como SSDT (SQL Server Data Tools) e o SSMS (SQL Server Management Studio) para implantar, configurar, executar, monitorar, agendar e gerenciar pacotes.

> [!NOTE]
> Durante essa visualização pública, o Azure SSIS Integration Runtime ainda não está disponível em todas as regiões. Para obter informações sobre as regiões com suporte, consulte [Produtos disponíveis por região – Microsoft Azure](https://azure.microsoft.com/regions/services/).

O Data Factory também dá suporte a outros tipos de Integration Runtimes. Para saber mais sobre o SSIS IR e outros tipos de Integration Runtimes, consulte [Integration Runtime no Azure Data Factory](https://docs.microsoft.com/azure/data-factory/concepts-integration-runtime).

## <a name="prerequisites"></a>Pré-requisitos
As funcionalidades descritas neste artigo não exigem o SQL Server 2017 ou o SQL Server 2016.

Essas funcionalidades exigem as seguintes versões do SSDT (SQL Server Data Tools):
-   Para o Visual Studio 2017, versão 15.3 (versão prévia) ou posterior.
-   Para o Visual Studio 2015, versão 17.2 ou posterior.

> [!NOTE]
> Quando você implanta pacotes no Azure, o Assistente de Implantação de Pacotes sempre faz upgrade dos pacotes para o formato de pacote mais recente.

Para obter mais informações sobre pré-requisitos no Azure, consulte [Migrar pacotes do SSIS (SQL Server Integration Services) por lift-and-shit para o Azure](https://docs.microsoft.com/azure/data-factory/tutorial-deploy-ssis-packages-azure).

## <a name="ssis-features-on-azure"></a>Recursos do SSIS no Azure

Quando você provisiona uma instância do Banco de Dados SQL para hospedar o SSISDB, o Azure Feature Pack para SSIS e o Access Redistribuível também são instalados. Esses componentes fornecem conectividade a arquivos do **Excel e Access** e para várias fontes de dados do **Azure**, além de fontes de dados compatíveis com os componentes internos. Você não pode instalar **componentes de terceiros** para SSIS (incluindo os componentes de terceiros da Microsoft, tais como os componentes da Attunity e SAP BI) no momento.

O **nome do banco de dados SQL** que hospeda o SSISDB torna-se a primeira parte do nome de quatro partes a ser usado ao implantar e gerenciar pacotes de SSDT e SSMS – `<sql_database_name>.database.windows.net`.

Você deve usar o **modelo de implantação de projeto**, não o modelo de implantação de pacote, para projetos que você implanta em SSISDB no Banco de Dados SQL do Azure.

Você pode continuar a **projetar e criar pacotes** localmente no SSDT ou então no Visual Studio com o SSDT instalado.

Para obter informações sobre como se conectar a **fontes de dados locais** da nuvem com autenticação do Windows, consulte [Conectar a fontes de dados locais com a Autenticação do Windows](ssis-azure-connect-with-windows-auth.md).

## <a name="common-tasks"></a>Tarefas comuns

### <a name="provision"></a>Provisionar
Antes de implantar e executar pacotes SSIS no Azure, você precisa provisionar o banco de dados de catálogo do SSISDB e o Azure SSIS Integration Runtime. Siga as etapas de provisionamento neste artigo: [Migrar pacotes do SSIS (SQL Server Integration Services) por lift-and-shit para o Azure](https://docs.microsoft.com/azure/data-factory/tutorial-deploy-ssis-packages-azure).

### <a name="deploy-and-run-packages"></a>Implantar e executar pacotes
Para implantar projetos e executar pacotes no Banco de Dados SQL, você pode usar uma das diversas ferramentas e opções de script familiares:
-   SQL Server Management Studio (SSMS)
-   Transact-SQL (do SSMS, Visual Studio Code ou outra ferramenta)
-   Uma ferramenta de linha de comando
-   PowerShell
-   C# e o modelo do objeto de gerenciamento do SSIS

### <a name="monitor-packages"></a>Monitorar pacotes
Para monitorar pacotes em execução no SSMS, você pode usar uma das ferramentas de relatório a seguir no SSMS.
-   Clique com o botão direito do mouse em **SSISDB** e, em seguida, selecione **Operações Ativas** para abrir a caixa de diálogo **Operações Ativas**.
-   Selecione um pacote no Pesquisador de Objetos, clique com o botão direito do mouse e selecione, sucessivamente, **Relatórios**, **Relatórios Padrão** e **Todas as Execuções**.

### <a name="schedule-packages"></a>Agendar pacotes
Para agendar a execução de pacotes armazenados no Banco de Dados SQL, você pode usar as seguintes ferramentas:
-   SQL Server Agent local
-   A atividade de procedimento armazenado do Data Factory SQL Server

Para obter mais informações, consulte [Agendar execução de pacote SSIS no Azure](ssis-azure-schedule-packages.md).

## <a name="next-steps"></a>Próximas etapas
Para uma introdução às cargas de trabalho de SSIS no Azure, consulte os seguintes artigos:
-   [Migrar pacotes do SSIS (SQL Server Integration Services) por lift-and-shift para o Azure](https://docs.microsoft.com/azure/data-factory/tutorial-deploy-ssis-packages-azure)
-   [Implantar, executar e monitorar um pacote do SSIS no Azure](ssis-azure-deploy-run-monitor-tutorial.md)
