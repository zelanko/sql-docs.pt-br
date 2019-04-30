---
title: Avaliar uma empresa e consolidar relatórios de avaliação (SQL Server) | Microsoft Docs
description: Saiba como usar o DMA para avaliar uma empresa e consolidar relatórios de avaliação antes de atualizar o SQL Server ou migrando para o banco de dados SQL.
ms.custom: ''
ms.date: 03/19/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: HJToland3
ms.author: rajpo
manager: craigg
ms.openlocfilehash: 15513348d4a747b0335bca8dd6345070e2c84ef0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63156191"
---
# <a name="assess-an-enterprise-and-consolidate-assessment-reports-with-dma"></a>Avaliar uma empresa e consolidar relatórios de avaliação com o DMA

As seguintes instruções passo a passo ajudam você a usar o Assistente de migração de dados para realizar uma avaliação de dimensionado com êxito para a atualização do SQL Server no local ou a execução do SQL Server em VMs do Azure ou para migrar para o banco de dados SQL.

## <a name="prerequisites"></a>Prerequisites

- Designe um computador de ferramentas em sua rede do qual o DMA será iniciado. Certifique-se de que esse computador tenha conectividade com seus destinos do SQL Server.
- Baixe e instale:
    - [Assistente de migração de dados](https://www.microsoft.com/download/details.aspx?id=53595) v 3.6 ou posterior.
    - [PowerShell](https://aka.ms/wmf5download) v 5.0 ou superior.
    - [.NET framework](https://www.microsoft.com/download/details.aspx?id=30653) v4.5 ou superior.
    - [SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 17.0 ou superior.
    - [Power BI desktop](https://docs.microsoft.com/power-bi/desktop-get-the-desktop).
    - [Módulos do PowerShell do Azure](https://docs.microsoft.com/powershell/azure/install-az-ps?view=azps-1.0.0)
- Baixe e extraia:
    - O [modelo do Power BI DMA relatórios](https://techcommunity.microsoft.com/gxcuf89792/attachments/gxcuf89792/MicrosoftDataMigration/56/2/PowerBI-Reports.zip).
    - O [LoadWarehouse script](https://techcommunity.microsoft.com/gxcuf89792/attachments/gxcuf89792/MicrosoftDataMigration/56/1/LoadWarehouse1.zip).

## <a name="loading-the-powershell-modules"></a>Carregando os módulos do PowerShell
Salvar os módulos do PowerShell para o diretório de módulos do PowerShell permite que você chame os módulos sem a necessidade de carregar explicitamente-los antes do uso.

Para carregar os módulos, execute as seguintes etapas:
1. Navegue até C:\Program files\windowspowershell\modules. e, em seguida, crie uma pasta chamada **DataMigrationAssistant**.
2. Abra o [módulos do PowerShell](https://techcommunity.microsoft.com/gxcuf89792/attachments/gxcuf89792/MicrosoftDataMigration/56/3/PowerShell-Modules2.zip)e, em seguida, salvá-los para a pasta que você criou.

      ![Módulos do PowerShell](../dma/media//dma-consolidatereports/dma-powershell-modules.png)

    Cada pasta contém o arquivo psm1 associados, conforme mostrado no gráfico a seguir:

   ![Arquivos de psm1 de módulos do PowerShell](../dma/media//dma-consolidatereports/dma-powershell-modules-psm1-files.png)

   > [!NOTE]
   > A pasta e arquivo psm1 contém devem ter o mesmo nome.

   > [!IMPORTANT]
   > Você talvez precise desbloquear os arquivos do PowerShell depois de salvá-los para o diretório do WindowsPowerShell para garantir que os módulos a serem carregados corretamente. Para desbloquear um arquivo do PowerShell, clique com botão direito no arquivo, selecione **propriedades**, selecione o **Unblock** caixa de texto e, em seguida, selecione **Okey**.

   ![Propriedades do arquivo psm1](../dma/media//dma-consolidatereports/dma-psm1-file-properties.png)

    PowerShell agora deve carregar esses módulos automaticamente quando uma nova sessão do PowerShell é iniciado.

## <a name="create-inventory"></a> Criar um inventário de servidores SQL
Antes de executar o script do PowerShell para avaliar seus servidores SQL, você precisa criar um inventário dos SQL Servers que você deseja avaliar.

Esse inventário pode estar em uma das duas formas:
- Arquivo CSV do Excel
- Tabela do SQL Server

### <a name="if-using-a-csv-file"></a>Se usando um arquivo CSV

> [!IMPORTANT]
> Certifique-se de que o arquivo de inventário é salvo como arquivo separados por vírgulas (CSV).
>
> Para instâncias padrão, defina o nome da instância MSSQLSERVER.


Ao usar um arquivo csv para importar os dados, verifique se há apenas duas colunas de dados - **nome da instância** e **nome do banco de dados**, e que as colunas não tem linhas de cabeçalho.
 
 ![conteúdo do arquivo CSV](../dma/media//dma-consolidatereports/dma-csv-file-contents.png)

### <a name="if-using-a-sql-server-table"></a>Se usar uma tabela do SQL Server

> [!IMPORTANT]
> Para instâncias padrão, defina o nome da instância MSSQLSERVER.

Criar um banco de dados chamado **EstateInventory** e uma tabela chamada **DatabaseInventory**. A tabela que contém esses dados de inventário pode ter qualquer número de colunas, contanto que existam quatro colunas seguintes:
- ServerName
- InstanceName
- DatabaseName
- AssessmentFlag

![Conteúdo da tabela do SQL Server](../dma/media//dma-consolidatereports/dma-sql-server-table-contents.png)

Se esse banco de dados não estiver no computador de ferramentas, certifique-se de que o computador de ferramentas tem conectividade de rede para esta instância do SQL Server.

A vantagem de usar uma tabela do SQL Server em um arquivo CSV é que você pode usar a coluna do sinalizador de avaliação para controlar a instância / banco de dados que obtém selecionadas para avaliação, o que torna mais fácil separar as avaliações em partes menores.  Em seguida, você pode abranger várias avaliações (consulte a seção sobre como executar uma avaliação neste artigo), que é mais fácil do que a manutenção de vários arquivos CSV.

Tenha em mente que, dependendo do número de objetos e suas complexidades, uma avaliação pode levar um tempo muito longo (horas +), portanto, é recomendável separar a avaliação em partes gerenciáveis.

## <a name="running-a-scaled-assessment"></a>Executar uma avaliação em escala
Depois de carregar os módulos do PowerShell para o diretório de módulos e criar um inventário, você precisará executar uma avaliação em escala abrindo o PowerShell e executando a função dmaDataCollector.
 
  ![listagens de função dmaDataCollector](../dma/media//dma-consolidatereports/dma-dmaDataCollector-function-listing.png)

Os parâmetros associados à função dmaDataCollector são descritos na tabela a seguir.

|Parâmetro  |Descrição |
|---------|---------|
|**getServerListFrom** | Seu inventário. Os valores possíveis são **SqlServer** e **CSV**.<br/>Para obter mais informações, consulte [criar um inventário de servidores SQL](#create-inventory). |
|**csvPath** | O caminho para o arquivo CSV de inventário.  Usado somente quando **getServerListFrom** é definido como **CSV**. |
|**serverName** | O nome da instância do SQL Server do inventário ao usar **SqlServer** na **getServerListFrom** parâmetro. |
|**databaseName** | O banco de dados que hospeda a tabela de estoque. |
|**AssessmentName** | O nome da avaliação de DMA. |
|**TargetPlatform** | O tipo de destino de avaliação que você deseja executar.  Os valores possíveis são **AzureSQLDatabase**, **SQLServer2012**, **lt;sqlserver2014**, **SQLServer2016**,  **SQLServerLinux2017**, **SQLServerWindows2017**, e **ManagedSqlServer**. |
|**AuthenticationMethod** | O método de autenticação para se conectar aos destinos do SQL Server que você deseja avaliar. Os valores possíveis são **SQLAuth** e **WindowsAuth**. |
|**OutputLocation** | O diretório no qual armazenar o JSON de avaliação do arquivo de saída. Dependendo do número de bancos de dados que está sendo avaliado e o número de objetos nos bancos de dados, as avaliações podem levar um tempo muito longo. O arquivo será gravado depois de concluíram todas as avaliações. |

Se houver um erro inesperado, a janela de comando que obtém iniciada por esse processo será encerrada.  Examine o log de erros para determinar o motivo da falha.
 
  ![Local do log de erros](../dma/media//dma-consolidatereports/dma-error-log-file-location.png)

## <a name="consuming-the-assessment-json-file"></a>Consumindo o arquivo JSON de avaliação

Após a avaliação, você agora está pronto para importar os dados no SQL Server para análise. Para consumir o arquivo JSON de avaliação, abra o PowerShell e execute a função dmaProcessor.
 
  ![listagem de função dmaProcessor](../dma/media//dma-consolidatereports/dma-dmaProcessor-function-listing.png)

Os parâmetros associados à função dmaProcessor são descritos na tabela a seguir.

|Parâmetro  |Descrição |
|---------|---------|
|**processTo** | O local para o qual o arquivo JSON será processado. Os valores possíveis são **SQLServer** e **AzureSQLDatabase**. |
|**serverName** | A instância do SQL Server para o qual os dados serão processados.  Se você especificar **AzureSQLDatabase** para o **processTo** parâmetro, em seguida, inclua apenas o nome do SQL Server (não inclua. database.windows.net). Você será solicitado a fornecer dois logons durante o direcionamento para o banco de dados SQL Azure; a primeira é suas credenciais de locatário do Azure, enquanto o segundo é o logon de administrador para o servidor do SQL Azure. |
|**CreateDMAReporting** | O banco de dados temporário criar para processar o arquivo JSON.  Se o banco de dados especificado já existe e você definir esse parâmetro para um, os objetos não são criados.  Esse parâmetro é útil para a recriação de um único objeto que foi descartado. |
|**CreateDataWarehouse** | Cria o data warehouse que será usado pelo relatório do Power BI. |
|**databaseName** | O nome do banco de dados DMAReporting. |
|**warehouseName** | O nome do banco de dados de depósito de dados. |
|**jsonDirectory** | O diretório que contém o arquivo JSON de avaliação.  Se há vários arquivos JSON no diretório, eles são processados individualmente. |

A função dmaProcessor deve levar apenas alguns segundos para processar um único arquivo.

## <a name="loading-the-data-warehouse"></a>Carrega o data warehouse
O dmaProcessor terminar de processar os arquivos de avaliação, após os dados serão carregados no banco de dados DMAReporting na tabela de dados do relatório. Neste ponto, você precisará carregar o data warehouse.

1. Use o script de LoadWarehouse para preencher valores ausentes nas dimensões.

    O script irá pegar os dados da tabela de dados do relatório no banco de dados DMAReporting e carregá-lo para o warehouse.  Se houver erros durante esse processo de carregamento, elas são provavelmente resultado de entradas ausentes nas tabelas de dimensões.

2. Carregar o data warehouse.
 
      ![LoadWarehouse conteúdo carregado](../dma/media//dma-consolidatereports/dma-LoadWarehouse-loaded.png)

## <a name="set-your-database-owners"></a>Defina seus proprietários de banco de dados
Embora não seja obrigatório, para obter mais valor dos relatórios, é recomendável que você defina os proprietários de banco de dados **dimDBOwner** da dimensão e, em seguida, atualize **DBOwnerKey** no  **FactAssessment** tabela.  Seguir esse processo permitirá que a divisão e filtragem de relatório do Power BI com base em proprietários de banco de dados específico.

Você também pode usar o script LoadWarehouse para fornecer as instruções TSQL básicas para definir os proprietários de banco de dados.

  ![Proprietários de configuração LoadWarehouse](../dma/media//dma-consolidatereports/dma-LoadWarehouse-set-owners.png)

## <a name="dma-reports"></a>Relatórios DMA

1. Abra o modelo de DMA relatórios Power BI no Power BI Desktop.
2. Insira os detalhes do servidor que apontam para seus **DMAWarehouse** do banco de dados e, em seguida, selecione **carga**.

   ![Modelo do Power BI DMA relatórios carregados](../dma/media//dma-consolidatereports/dma-reports-powerbi-template-loaded.png)

   Depois que o relatório tiver atualizado os dados a partir de **DMAWarehouse** banco de dados, você verá um relatório semelhante ao seguinte.

   ![Modo de exibição de relatório DMAWarehouse](../dma/media//dma-consolidatereports/dma-DMAWarehouse-report1.png)

   > [!TIP]
   > Se você não vir os dados que você esperava, tente alterar o indicador de Active Directory.  Para obter mais informações, consulte o os detalhes na seção a seguir.

## <a name="working-with-dma-reports"></a>Trabalhando com relatórios DMA
Para trabalhar com relatórios DMA, use os indicadores e segmentações de dados para filtrar por:
- Tipos de avaliação (BD SQL do Azure, Azure SQL MI, SQL no local) 
- Nome da Instância
- Nome do Banco de Dados
- Nome da equipe

Para acessar a folha de indicadores e filtros, selecione o indicador de filtros, na página do relatório principal:

![Filtros e indicadores de relatório DMA](../dma/media//dma-consolidatereports/dma-report-bookmarks-filters.png)

Isso permite que a folha a seguir:

![Folha de exibições de relatório de DMA](../dma/media//dma-consolidatereports/dma-report-views-blade.png)

Você pode usar indicadores para alternar o contexto de geração de relatórios entre:
- Avaliações de nuvem de banco de dados SQL do Azure
- Avaliações de nuvem do Azure SQL MI
- Avaliações de local

![Indicadores de exibições de relatório de DMA](../dma/media//dma-consolidatereports/dma-report-bookmarks1.png)

Para ocultar a folha de filtros, CTRL + clique no botão Voltar:

![Botão de voltar de modos de exibição de relatório de DMA](../dma/media//dma-consolidatereports/dma-report-bookmarks-back.png)

Há um prompt na parte inferior esquerda da página do relatório para mostrar se um filtro estiver aplicado no momento em qualquer uma das seguintes opções:
* FactAssessment – InstanceName
* FactAssessment – DatabaseName
* dimDBOwner - DBOwner

![Prompt de filtro aplicado](../dma/media//dma-consolidatereports/dma-filter-applied-prompt.png)

> [!NOTE]
> Se você só pode executar uma avaliação do banco de dados SQL, somente os relatórios de nuvem são preenchidos. Por outro lado, se você só pode executar uma avaliação de locais, somente os relatórios de local são preenchidos. No entanto, se você executar o Azure e uma avaliação de local e, em seguida, carregar as duas avaliações em seu warehouse, você pode alternar entre os relatórios de nuvem e local, clicando em CTRL o ícone associado.

## <a name="reports-visuals"></a>Elementos visuais de relatórios
Os detalhes exibidos em relatórios do Power BI é mostrado nas seções a seguir.

### <a name="readiness-"></a>% De preparação

  ![Porcentagem de preparação de DMA](../dma/media//dma-consolidatereports/dma-readiness-percentage.png)

Este visual é atualizado com base no contexto de seleção (tudo, de instância, banco de dados [múltiplos de]).

### <a name="readiness-count"></a>Contagem de preparação

  ![Contagem de preparação de DMA](../dma/media//dma-consolidatereports/dma-readiness-count.png)

Este visual mostra a contagem de bancos de dados que está pronto para migrar a contagem de bancos de dados que ainda não estão prontos para migrar.

### <a name="readiness-bucket"></a>Bucket de preparação

  ![Bucket de preparação de DMA](../dma/media//dma-consolidatereports/dma-readiness-bucket.png)

Este visual mostra uma divisão dos bancos de dados por buckets de preparação a seguir:
- PRONTO PARA 100%
- PRONTO PARA 99 75%
- PRONTO PARA 50 A 75%
- NÃO ESTÁ PRONTO

### <a name="issues-word-cloud"></a>Nuvem de palavra de problemas
 
  ![Problemas DMA WordCloud](../dma/media//dma-consolidatereports/dma-issues-word-cloud.png)

Este visual mostra os problemas que estão ocorrendo no momento dentro no contexto de seleção (tudo, de instância, banco de dados [múltiplos de]). Quanto maior a palavra aparece na tela, maior o número de problemas nessa categoria. Focalizar o ponteiro do mouse sobre uma palavra mostra o número de problemas que ocorrem nessa categoria.

### <a name="database-readiness"></a>Preparação do banco de dados

  ![Relatório de preparação do banco de dados de DMA](../dma/media//dma-consolidatereports/dma-database-readiness-report.png)

Esta seção é a parte principal do relatório, que mostra a preparação de uma instância de banco de dados. Este relatório tem uma hierarquia de busca detalhada de:
- InstanceDatabase
- ChangeCategory
- Title
- ObjectType
- ImpactedObjectName

 ![Análise de dados de relatório de preparação do banco de dados de DMA](../dma/media//dma-consolidatereports/dma-database-readiness-report-drilldown.png)

Este relatório também serve como o ponto de filtro para criar o relatório de plano de correção.

Para analisar o relatório de plano de correção, clique com botão direito em um ponto de dados nesse gráfico, aponte para **detalhamento**e, em seguida, selecione **planos de correção**.

Essa tarefa filtra o relatório de plano de correção para o nível de hierarquia atual com base no ponto em que você selecionar a opção de detalhamento.

  ![Preparação do banco de dados de DMA busca detalhada do relatório filtrada](../dma/media//dma-consolidatereports/dma-database-readiness-report-drilldown-filtered.png)

  ![Relatório de plano de correção de DMA](../dma/media//dma-consolidatereports/dma-remediation-plan-report.png)

Você também pode usar o relatório de plano de correção no plano de seu próprio para compilar uma solução personalizada usando os filtros na **filtros de visualizações** folha.
 
  ![Opções de filtro de relatório plano de correção de DMA](../dma/media//dma-consolidatereports/dma-remediation-plan-report-filter-options.png)

### <a name="script-disclaimer"></a>Isenção de responsabilidade de script
*Não há suporte para os scripts de exemplo fornecidos neste artigo em qualquer serviço ou programa de suporte padrão da Microsoft. Todos os scripts são fornecidos como estão, sem garantias de qualquer tipo. Microsoft também se isenta de todas as garantias implícitas, sem limitação, qualquer implícitas de comercialização ou adequação a uma finalidade específica. Todos os riscos resultantes do uso ou do desempenho dos scripts de exemplo e documentação de responsabilidade do usuário. Em nenhuma hipótese Microsoft, seus autores ou qualquer pessoa else envolvidas na criação, produção ou entrega dos scripts será responsável por quaisquer danos (incluindo, sem limitação, danos por perda de lucros comerciais, interrupção dos negócios, perda de informações de negócios, ou outras perdas PECUNIÁRIAS) decorrente do uso ou da incapacidade de usar os scripts de exemplo ou a documentação, mesmo que a Microsoft tenha sido informada da possibilidade de tais danos.  Busca de permissão antes de relançando esses scripts em outros sites/repositórios/blogs.*
