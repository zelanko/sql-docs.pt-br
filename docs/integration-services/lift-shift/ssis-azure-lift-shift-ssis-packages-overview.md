---
title: Implante e execute pacotes SSIS no Azure | Microsoft Docs
description: Saiba como mover suas cargas de trabalho, pacotes e projetos do SSIS (SQL Server Integration Services) para a nuvem do Microsoft Azure.
ms.date: 09/23/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: swinarko
ms.author: sawinark
ms.reviewer: douglasl
manager: craigg
ms.openlocfilehash: 4c9c881cbbefc5fa8fb9f0810a5c8ea26f375a56
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65721473"
---
# <a name="lift-and-shift-sql-server-integration-services-workloads-to-the-cloud"></a>Migrar cargas de trabalho do SQL Server Integration Services por lift-and-shift para a nuvem

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Agora você pode mover suas cargas de trabalho, pacotes e projetos do SSIS (SQL Server Integration Services) para a nuvem do Microsoft Azure. Implante, execute e gerencie projetos do SSIS e pacotes no Catálogo SSIS (SSISDB) no Banco de Dados SQL do Azure ou na Instância Gerenciada do Banco de Dados SQL com ferramentas familiares, como o SSMS (SQL Server Management Studio).

## <a name="benefits"></a>Benefícios
Mover suas cargas de trabalho SSIS de local para o Azure tem os seguintes benefícios potenciais:
-   **Redução dos custos operacionais** e redução da carga de gerenciar a infraestrutura que você tem ao executar o SSIS localmente ou em máquinas virtuais do Azure.
-   **Aumento da alta disponibilidade** com a capacidade de especificar vários nós por cluster, bem como os recursos de alta disponibilidade do Azure e do Banco de Dados SQL do Azure.
-   **Aumento da escalabilidade** com a capacidade de especificar vários núcleos por nó (expandir verticalmente) e vários nós por cluster (expansão).

## <a name="architecture-of-ssis-on-azure"></a>Arquitetura do SSIS no Azure
A tabela a seguir destaca as diferenças entre o SSIS local e o SSIS no Azure.

A diferença mais importante é a separação do armazenamento do tempo de execução. O Azure Data Factory hospeda o mecanismo de tempo de execução para pacotes do SSIS no Azure. O mecanismo de tempo de execução é chamado de IR do Azure-SSIS (Integration Runtime do Azure-SSIS). Para obter mais informações, veja [Integration Runtime do Azure-SSIS](https://docs.microsoft.com/azure/data-factory/concepts-integration-runtime#azure-ssis-integration-runtime).

| Local | Armazenamento | Tempo de execução | Escalabilidade |
|---|---|---|---|
| No local | SQL Server | Tempo de execução do SSIS hospedado pelo SQL Server | SSIS Scale Out (no SQL Server 2017 e posterior)<br/><br/>Soluções personalizadas (em versões anteriores do SQL Server) |
| No Azure | Banco de Dados SQL ou Instância Gerenciada do Banco de Dados SQL | Integration Runtime do Azure-SSIS, um componente do Azure Data Factory | Opções de colocação em escala para o Integration Runtime do Azure-SSIS |
| | | | |

## <a name="provision-ssis-on-azure"></a>Provisionar o SSIS no Azure

**Provisione**. Antes de implantar e executar os pacotes SSIS no Azure, é necessário provisionar o SSISDB (Catálogo do SSIS) e o Azure-SSIS Integration Runtime.

-   Para provisionar o SSIS no Azure, usando o portal do Azure, siga as etapas de provisionamento deste artigo: [Provisionar o Azure-SSIS Integration Runtime no Azure Data Factory](https://docs.microsoft.com/azure/data-factory/tutorial-deploy-ssis-packages-azure). 

-   Para provisionar o SSIS no Azure, usando o PowerShell, siga as etapas de provisionamento neste artigo: [Provisionar o Azure-SSIS Integration Runtime no Azure Data Factory com o PowerShell](https://docs.microsoft.com/azure/data-factory/tutorial-deploy-ssis-packages-azure-powershell).

Você só precisa provisionar o IR do Azure-SSIS uma vez. Depois disso, você pode usar ferramentas familiares, como SSDT (SQL Server Data Tools) e o SSMS (SQL Server Management Studio) para implantar, configurar, executar, monitorar, agendar e gerenciar pacotes.

> [!NOTE]
> O Azure-SSIS Integration Runtime ainda não está disponível em todas as regiões do Azure. Para obter informações sobre as regiões com suporte, consulte [Produtos disponíveis por região – Microsoft Azure](https://azure.microsoft.com/regions/services/).

**Escale verticalmente e horizontalmente**. Quando você provisiona o IR do Azure-SSIS, pode escalar vertical e horizontalmente especificando valores para as seguintes opções:
-   O tamanho de nó (incluindo o número de núcleos) e o número de nós no cluster.
-   A instância existente do Banco de Dados SQL do Azure para hospedar o SSISDB (banco de dados de catálogo do SSIS) e a camada de serviço para o banco de dados.
-   O número máximo de execuções paralelas por nó.

**Aumente o desempenho**. Para obter mais informações, veja [Configurar o Integration Runtime do Azure-SSIS para alto desempenho](https://docs.microsoft.com/azure/data-factory/configure-azure-ssis-integration-runtime-performance).

**Reduza os custos**. Para reduzir os custos, execute o Azure-SSIS IR somente quando necessário. Para saber mais, confira [Como agendar o início e a parada de um tempo de execução de integração do Azure SSIS](https://docs.microsoft.com/azure/data-factory/how-to-schedule-azure-ssis-integration-runtime).

## <a name="design-packages"></a>Criar pacotes

Você pode continuar a **projetar e criar pacotes** localmente no SSDT ou então no Visual Studio com o SSDT instalado.

### <a name="connect-to-data-sources"></a>Conectar-se às fontes de dados

Para se conectar a fontes de dados locais da nuvem com a **autenticação do Windows**, confira [Conectar-se a fontes de dados e compartilhamentos de arquivos com a Autenticação do Windows de pacotes do SSIS no Azure](ssis-azure-connect-with-windows-auth.md).

Para se conectar a arquivos e compartilhamentos de arquivos, confira [Abrir e salvar arquivos no local e no Azure com pacotes SSIS implantados no Azure](ssis-azure-files-file-shares.md).

### <a name="available-ssis-components"></a>Componentes do SSIS disponíveis

Quando você provisiona uma instância do Banco de Dados SQL para hospedar o SSISDB, o Azure Feature Pack para SSIS e o Access Redistribuível também são instalados. Esses componentes fornecem conectividade com várias fontes de dados do **Azure** e com os arquivos do **Excel e do Access**, além das fontes de dados compatíveis com os componentes internos.

Também é possível instalar componentes adicionais, por exemplo, é possível instalar um driver não instalado por padrão. Para saber mais, confira [Personalizar a instalação para o tempo de execução de integração do Azure-SSIS](/azure/data-factory/how-to-configure-azure-ssis-ir-custom-setup).

Se você tiver uma licença do Enterprise Edition, os componentes adicionais estarão disponíveis. Para saber mais, confira [Provisionar a Enterprise Edition para o Azure-SSIS Integration Runtime](https://docs.microsoft.com/azure/data-factory/how-to-configure-azure-ssis-ir-enterprise-edition).

Se você for um ISV, poderá atualizar a instalação dos componentes licenciados para disponibilizá-las no Azure. Para saber mais, confira [Instalar componentes personalizados pagos ou licenciados para o Integration Runtime do Azure-SSIS](https://docs.microsoft.com/azure/data-factory/how-to-develop-azure-ssis-ir-licensed-components).

### <a name="transaction-support"></a>Suporte à transação

Com o SQL Server local e em máquinas virtuais do Azure, você pode usar transações do MSDTC (Coordenador de Transações Distribuídas da Microsoft). Para configurar o MSDTC em cada nó do IR do Azure SSIS, use a funcionalidade de instalação personalizada. Para obter mais informações, consulte [Instalação personalizada para o tempo de execução de integração do Azure-SSIS](https://docs.microsoft.com/azure/data-factory/how-to-configure-azure-ssis-ir-custom-setup).

Com o Banco de Dados SQL do Azure, você só pode usar transações elásticas. Para obter mais informações, consulte [Transações distribuídas entre bancos de dados de nuvem](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-transactions-overview).

## <a name="deploy-and-run-packages"></a>Implantar e executar pacotes

Para começar, confira [Tutorial: implantar e executar um pacote SSIS (SQL Server Integration Services) no Azure](ssis-azure-deploy-run-monitor-tutorial.md).

### <a name="prerequisites"></a>Prerequisites

Para implantar pacotes do SSIS para o Azure, você precisa ter uma das seguintes versões do SSDT (SQL Server Data Tools):
-   Para o Visual Studio 2017, versão 15.3 ou posterior.
-   Para o Visual Studio 2015, versão 17.2 ou posterior.

### <a name="connect-to-ssisdb"></a>Conectar-se ao SSISDB

O **nome do Banco de Dados SQL** que hospeda o SSISDB torna-se a primeira parte do nome de quatro partes a ser usado ao implantar e executar pacotes de SSDT e SSMS, no seguinte formato – `<sql_database_name>.database.windows.net`. Para saber mais sobre como se conectar ao banco de dados do Catálogo do SSIS no Azure, veja [Conectar-se ao SSISDB (Catálogo do SSIS) no Azure](ssis-azure-connect-to-catalog-database.md).

### <a name="deploy-projects-and-packages"></a>Implantar projetos e pacotes

É necessário usar o **modelo de implantação de projeto**, não o modelo de implantação de pacote, quando você implanta projetos no SSISDB no Azure.

Para implantar projetos no Azure, é possível usar uma das diversas ferramentas e opções de script conhecidas:
-   SQL Server Management Studio (SSMS)
-   Transact-SQL (do SSMS, Visual Studio Code ou outra ferramenta)
-   Uma ferramenta de linha de comando
-   PowerShell ou C# e o modelo do objeto de gerenciamento do SSIS

O processo de implantação valida os pacotes para garantir que eles possam ser executados no Integration Runtime do SSIS-Azure. Para saber mais, confira [Validar pacotes SSIS (SQL Server Integration Services) implantados no Azure](ssis-azure-validate-packages.md).

Confira um exemplo de implantação que usa o SSMS e o Assistente de implantação do Integration Services no [Tutorial: implantar e executar um pacote SSIS (SQL Server Integration Services) no Azure](ssis-azure-deploy-run-monitor-tutorial.md).

### <a name="version-support"></a>Suporte à versão

É possível implantar um pacote criado com qualquer versão do SSIS no Azure. Quando você implantar um pacote no Azure, se não houver nenhum erro de validação, o pacote será atualizado automaticamente para o formato de pacote mais recente. Em outras palavras, ele sempre será atualizado para a versão mais recente do SSIS.

### <a name="run-packages"></a>Executar pacotes

Para executar pacotes do SSIS implantados no Azure, você pode usar diversos métodos. Para saber mais, confira [Executar pacotes SSIS (SQL Server Integration Services) implantados no Azure](ssis-azure-run-packages.md).

### <a name="run-packages-in-an-azure-data-factory-pipeline"></a>Executar pacotes em um pipeline do Azure Data Factory

Para executar um pacote do SSIS em um pipeline do Azure Data Factory, use a Atividade Executar Pacote do SSIS. Para obter mais informações, consulte [Executar um pacote do SSIS usando a atividade Executar pacote do SSIS no Azure Data Factory](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity).

Quando você executa um pacote em um pipeline do Data Factory com a Atividade Executar Pacote do SSIS, pode passar valores para o pacote em tempo de execução. Para passar um ou mais valores de tempo de execução, crie ambientes de execução do SSIS no SSISDB com o SQL Server Management Studio (SSMS). Em cada ambiente, crie variáveis e atribua valores correspondentes aos parâmetros dos seus projetos ou pacotes. Configure seus pacotes do SSIS no SSMS para associar as variáveis de ambiente aos parâmetros do seu projeto ou pacote. Ao executar os pacotes no pipeline, alterne entre ambientes especificando diferentes caminhos de ambiente na guia Configurações da interface do usuário da atividade Executar pacote do SSIS. Para saber mais sobre ambientes do SSIS, confira [Criar e mapear um ambiente de servidor](../packages/deploy-integration-services-ssis-projects-and-packages.md#create-and-map-a-server-environment).

## <a name="monitor-packages"></a>Monitorar pacotes

Para monitorar pacotes em execução, use as seguintes opções de geração de relatórios no SSMS.
-   Clique com o botão direito do mouse em **SSISDB** e, em seguida, selecione **Operações Ativas** para abrir a caixa de diálogo **Operações Ativas**.
-   Selecione um pacote no Pesquisador de Objetos, clique com o botão direito do mouse e selecione, sucessivamente, **Relatórios**, **Relatórios Padrão** e **Todas as Execuções**.

Para monitorar o Integration Runtime do Azure-SSIS, veja [Monitorar o Integration Runtime do Azure-SSIS](https://docs.microsoft.com/azure/data-factory/monitor-integration-runtime#azure-ssis-integration-runtime).

## <a name="schedule-packages"></a>Agendar pacotes
Para agendar a execução de pacotes implantados no Azure, você pode usar uma variedade de ferramentas. Para saber mais, confira [Agendar a execução de pacotes SSIS (SQL Server Integration Services) implantados no Azure](ssis-azure-schedule-packages.md).

## <a name="next-steps"></a>Próximas etapas
Para uma introdução às cargas de trabalho de SSIS no Azure, consulte os seguintes artigos:
-   [Tutorial: implantar e executar um pacote SSIS (SQL Server Integration Services) no Azure](ssis-azure-deploy-run-monitor-tutorial.md)
-   [Provisionar o Azure-SSIS Integration Runtime no Azure Data Factory](https://docs.microsoft.com/azure/data-factory/tutorial-deploy-ssis-packages-azure)
