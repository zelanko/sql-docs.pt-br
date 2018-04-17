---
title: Migrar cargas de trabalho do SQL Server Integration Services por lift-and-shift para a nuvem | Microsoft Docs
ms.date: 10/31/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: ''
ms.component: lift-shift
ms.suite: sql
ms.custom: ''
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 82a6ab09504edd0a5df17a05de62ae5fd44a1c18
ms.sourcegitcommit: 8f1d1363e18e0c32ff250617ab6cb2da2147bf8e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/03/2018
---
# <a name="lift-and-shift-sql-server-integration-services-workloads-to-the-cloud"></a>Migrar cargas de trabalho do SQL Server Integration Services por lift-and-shift para a nuvem
Agora você pode mover suas cargas de trabalho e pacotes do SQL Server Integration Services (SSIS) para a nuvem do Azure.
-   Armazene e gerencie projetos e pacotes do SSIS no SSISDB (banco de dados do catálogo do SSIS) no Banco de Dados SQL do Azure ou Instância Gerenciada do Banco de Dados SQL do Azure (Versão prévia).
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
| No Azure (Banco de Dados SQL ou Instância Gerenciada do Banco de Dados SQL (Versão prévia)) | Azure SSIS Integration Runtime, um componente do Azure Data Factory versão 2 | Opções de dimensionamento para IR do SSIS |
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

## <a name="version-info"></a>Informações sobre versão

É possível implantar um pacote criado com qualquer versão do SSIS no Azure. Quando você implantar um pacote no Azure, se não houver nenhum erro de validação, o pacote será atualizado automaticamente para o formato de pacote mais recente. Em outras palavras, ele sempre será atualizado para a versão mais recente do SSIS.

O processo de implantação valida os pacotes para garantir que eles possam ser executados no Integration Runtime do SSIS-Azure. Para obter mais informações, consulte [Validar pacotes do SSIS implantados no Azure](ssis-azure-validate-packages.md).

## <a name="prerequisites"></a>Prerequisites

As funcionalidades descritas neste artigo requerem as seguintes versões do SSDT (SQL Server Data Tools):
-   Para o Visual Studio 2017, versão 15.3 (versão prévia) ou posterior.
-   Para o Visual Studio 2015, versão 17.2 ou posterior.

Para obter mais informações sobre os pré-requisitos no Azure, consulte [Implantar pacotes do SSIS para o Azure](https://docs.microsoft.com/azure/data-factory/tutorial-create-azure-ssis-runtime-portal).

## <a name="provision-ssis-on-azure"></a>Provisionar o SSIS no Azure
Antes de implantar e executar os pacotes do SSIS no Azure, é necessário provisionar o SSISDB (banco de dados do catálogo do SSIS) e o Azure-SSIS Integration Runtime. Siga as etapas de provisionamento neste artigo: [Implantar pacotes do SSIS para o Azure](https://docs.microsoft.com/azure/data-factory/tutorial-create-azure-ssis-runtime-portal).

O **nome do banco de dados SQL** que hospeda o SSISDB torna-se a primeira parte do nome de quatro partes a ser usado ao implantar e gerenciar pacotes de SSDT e SSMS – `<sql_database_name>.database.windows.net`.

Para obter informações sobre como se conectar ao banco de dados do catálogo do SSIS, consulte [Connect to the SSISDB Catalog database on Azure](ssis-azure-connect-to-catalog-database.md) (Conectar-se ao banco de dados do Catálogo do SSISDB no Azure).

## <a name="design-packages"></a>Criar pacotes
Você pode continuar a **projetar e criar pacotes** localmente no SSDT ou então no Visual Studio com o SSDT instalado.

Para obter informações sobre como se conectar a fontes de dados locais da nuvem com a **Autenticação do Windows**, consulte [Conectar-se às fontes de dados e compartilhamentos de arquivo do Azure locais com a Autenticação do Windows](ssis-azure-connect-with-windows-auth.md).

Para obter informações sobre como conectar-se aos arquivos e compartilhamentos de arquivos, consulte [Armazenar e recuperar arquivos em compartilhamentos de arquivos local e no Azure com o SSIS](ssis-azure-files-file-shares.md).

Quando você provisiona uma instância do Banco de Dados SQL para hospedar o SSISDB, o Azure Feature Pack para SSIS e o Access Redistribuível também são instalados. Esses componentes fornecem conectividade com várias fontes de dados do **Azure** e com os arquivos do **Excel e do Access**, além das fontes de dados compatíveis com os componentes internos.

No momento, não é possível instalar nem usar **componentes de terceiros** para o SSIS (incluindo os componentes de terceiros da Microsoft, como os componentes do Oracle e Teradata da Attunity e da SAP BI).

## <a name="deploy-and-run-packages"></a>Implantar e executar pacotes
É necessário usar o **modelo de implantação de projeto**, não o modelo de implantação de pacote, quando você implanta projetos no SSISDB no Azure.

Para implantar projetos e executar pacotes no Azure, é possível usar uma das diversas ferramentas e opções de script conhecidas:
-   SQL Server Management Studio (SSMS)
-   Transact-SQL (do SSMS, Visual Studio Code ou outra ferramenta)
-   Uma ferramenta de linha de comando
-   PowerShell
-   C# e o modelo do objeto de gerenciamento do SSIS

Para começar, confira [Implantar, executar e monitorar um pacote SSIS no Azure](ssis-azure-deploy-run-monitor-tutorial.md).

## <a name="monitor-packages"></a>Monitorar pacotes
Para monitorar pacotes em execução no SSMS, você pode usar uma das ferramentas de relatório a seguir no SSMS.
-   Clique com o botão direito do mouse em **SSISDB** e, em seguida, selecione **Operações Ativas** para abrir a caixa de diálogo **Operações Ativas**.
-   Selecione um pacote no Pesquisador de Objetos, clique com o botão direito do mouse e selecione, sucessivamente, **Relatórios**, **Relatórios Padrão** e **Todas as Execuções**.

## <a name="schedule-packages"></a>Agendar pacotes
Para agendar a execução de pacotes armazenados no Banco de Dados SQL, você pode usar as seguintes ferramentas:
-   SQL Server Agent local
-   A atividade de procedimento armazenado do Data Factory SQL Server

Para obter mais informações, consulte [Agendar execução de pacote SSIS no Azure](ssis-azure-schedule-packages.md).

## <a name="next-steps"></a>Próximas etapas
Para uma introdução às cargas de trabalho de SSIS no Azure, consulte os seguintes artigos:
-   [Implantar pacotes do SSIS para o Azure](https://docs.microsoft.com/azure/data-factory/tutorial-create-azure-ssis-runtime-portal)
-   [Implantar, executar e monitorar um pacote do SSIS no Azure](ssis-azure-deploy-run-monitor-tutorial.md)
