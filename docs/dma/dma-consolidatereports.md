---
title: Avaliar uma empresa e consolidar relatórios de avaliação com Assistente de Migração de Dados
description: Saiba como usar o DMA para avaliar uma empresa e consolidar relatórios de avaliação antes de atualizar SQL Server ou migrar para o banco de dados SQL do Azure.
ms.date: 06/21/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: rajeshsetlem
ms.author: rajpo
ms.custom: seo-lt-2019
ms.openlocfilehash: fd6563881127b7a5c1cf134711a52fdedde629c4
ms.sourcegitcommit: 129f8574eba201eb6ade1f1620c6b80dfe63b331
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/30/2020
ms.locfileid: "87435171"
---
# <a name="assess-an-enterprise-and-consolidate-assessment-reports-with-dma"></a>Avaliar uma empresa e consolidar relatórios de avaliação com o Assistente de Migração de Dados

As instruções passo a passo a seguir ajudam a usar o Assistente de Migração de Dados para executar uma avaliação dimensionada com êxito para atualização de SQL Server locais ou SQL Server em execução em VMs do Azure ou para migrar para o banco de dados SQL do Azure.

## <a name="prerequisites"></a>Pré-requisitos

- Designe um computador de ferramentas em sua rede a partir do qual o DMA será iniciado. Verifique se este computador tem conectividade com seus destinos de SQL Server.
- Baixe e instale:
  - [Assistente de migração de dados](https://www.microsoft.com/download/details.aspx?id=53595) v 3.6 ou superior.
  - [PowerShell](https://aka.ms/wmf5download) v 5.0 ou superior.
  - [.NET Framework](https://www.microsoft.com/download/details.aspx?id=30653) v 4.5 ou superior.
  - [SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 17,0 ou superior.
  - [Power bi área de trabalho](/power-bi/fundamentals/desktop-get-the-desktop).
  - [Módulos do Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-az-ps?view=azps-1.0.0)
- Baixar e extrair:
  - O [modelo de Power bi de relatórios de DMA](https://techcommunity.microsoft.com/gxcuf89792/attachments/gxcuf89792/MicrosoftDataMigration/161/2/PowerBI-Reports.zip).
  - O [script loadwarehouse](https://techcommunity.microsoft.com/gxcuf89792/attachments/gxcuf89792/MicrosoftDataMigration/161/3/LoadWarehouse1.zip).

## <a name="loading-the-powershell-modules"></a>Carregando os módulos do PowerShell

Salvar os módulos do PowerShell no diretório de módulos do PowerShell permite que você chame os módulos sem a necessidade de carregá-los explicitamente antes de usar.

Para carregar os módulos, execute as seguintes etapas:

1. Navegue até C:\Program Files\WindowsPowerShell\Modules e, em seguida, crie uma pasta chamada **DataMigrationAssistant**.
2. Abra o [PowerShell-modules](https://techcommunity.microsoft.com/gxcuf89792/attachments/gxcuf89792/MicrosoftDataMigration/161/1/PowerShell-Modules2.zip)e salve-os na pasta que você criou.

      ![Módulos do PowerShell](../dma/media//dma-consolidatereports/dma-powershell-modules.png)

    Cada pasta contém o arquivo psm1 associado, conforme mostrado no gráfico a seguir:

   ![Arquivos psm1 de módulos do PowerShell](../dma/media//dma-consolidatereports/dma-powershell-modules-psm1-files.png)

   > [!NOTE]
   > A pasta e o arquivo psm1 que ele contém devem ter o mesmo nome.

   > [!IMPORTANT]
   > Talvez seja necessário desbloquear os arquivos do PowerShell depois de salvá-los no diretório WindowsPowerShell para garantir que os módulos sejam carregados corretamente. Para desbloquear um arquivo do PowerShell, clique com o botão direito do mouse no arquivo, selecione **Propriedades**, selecione a caixa de texto **desbloquear** e, em seguida, selecione **OK**.

   ![Propriedades do arquivo psm1](../dma/media//dma-consolidatereports/dma-psm1-file-properties.png)

    O PowerShell agora deve carregar esses módulos automaticamente quando uma nova sessão do PowerShell é iniciada.

## <a name="create-an-inventory-of-sql-servers"></a><a name="create-inventory"></a>Criar um inventário de servidores SQL

Antes de executar o script do PowerShell para avaliar seus SQL Servers, você precisa criar um inventário dos SQL Servers que você deseja avaliar.

Esse inventário pode estar em uma das duas formas:

- Arquivo CSV do Excel
- Tabela do SQL Server

### <a name="if-using-a-csv-file"></a>Se estiver usando um arquivo CSV

> [!IMPORTANT]
> Certifique-se de que o arquivo de inventário seja salvo como um arquivo CSV (separado por vírgulas).
>
> Para instâncias padrão, defina o nome da instância como MSSQLServer.

Ao usar um arquivo CSV para importar os dados, certifique-se de que há apenas duas colunas de **nome da instância** de dados e nome do **banco**de dado, e que as colunas não têm linhas de cabeçalho.

 ![conteúdo do arquivo CSV](../dma/media//dma-consolidatereports/dma-csv-file-contents.png)

### <a name="if-using-a-sql-server-table"></a>Se estiver usando uma tabela SQL Server

> [!IMPORTANT]
> Para instâncias padrão, defina o nome da instância como MSSQLServer.

Crie um banco de dados chamado **EstateInventory** e uma tabela chamada **DatabaseInventory**. A tabela que contém esses dados de inventário pode ter qualquer número de colunas, desde que existam quatro colunas a seguir:

- ServerName
- InstanceName
- DatabaseName
- AssessmentFlag

![SQL Server conteúdo da tabela](../dma/media//dma-consolidatereports/dma-sql-server-table-contents-database-inventory.png)

Se esse banco de dados não estiver no computador ferramentas, verifique se o computador das ferramentas tem conectividade de rede com essa SQL Server instância.

O benefício de usar uma tabela de SQL Server em um arquivo CSV é que você pode usar a coluna sinalizador de avaliação para controlar a instância/banco de dados que é selecionada para avaliação, o que torna mais fácil separar as avaliações em partes menores.  Em seguida, você pode abranger várias avaliações (consulte a seção sobre como executar uma avaliação mais adiante neste artigo), que é mais fácil do que manter vários arquivos CSV.

Tenha em mente que, dependendo do número de objetos e da sua complexidade, uma avaliação pode levar um tempo muito longo (horas +), portanto, é prudente separar a avaliação em partes gerenciáveis.

### <a name="if-using-an-instance-inventory"></a>Se estiver usando um inventário de instância

Crie um banco de dados chamado **EstateInventory** e uma tabela chamada **InstanceInventory**. A tabela que contém esses dados de inventário pode ter qualquer número de colunas, desde que existam quatro colunas a seguir:

- ServerName
- InstanceName
- Porta
- AssessmentFlag

![SQL Server conteúdo da tabela](../dma/media//dma-consolidatereports/dma-sql-server-table-contents-instance-inventory.png)

## <a name="running-a-scaled-assessment"></a>Executando uma avaliação dimensionada

Depois de carregar os módulos do PowerShell no diretório Modules e criar um inventário, você precisará executar uma avaliação dimensionada abrindo o PowerShell e executando a função dmaDataCollector.

  ![Listagens de funções dmaDataCollector](../dma/media//dma-consolidatereports/dma-dmaDataCollector-function-listing.png)

Os parâmetros associados à função dmaDataCollector são descritos na tabela a seguir.

|Parâmetro  |Descrição |
|---------|---------|
|**getServerListFrom** | Seu inventário. Os valores possíveis são **SqlServer** e **CSV**.<br/>Para obter mais informações, consulte [criar um inventário de servidores SQL](#create-inventory). |
|**csvPath** | O caminho para o arquivo de inventário CSV.  Usado somente quando **getServerListFrom** é definido como **CSV**. |
|**serverName** | O SQL Server nome da instância do inventário ao usar o **SqlServer** no parâmetro **getServerListFrom** . |
|**NomeDoBancoDeDados** | O banco de dados que hospeda a tabela de inventário. |
|**useInstancesOnly** | Sinalizador de bits para especificar se deve ser usada uma lista de instâncias para avaliação ou não.  Se definido como 0, a tabela DatabaseInventory será usada para criar a lista de destino de avaliação. |
|**AssessmentName** | O nome da avaliação DMA. |
|**TargetPlatform** | O tipo de destino da avaliação que você deseja executar.  Os valores possíveis são **AzureSQLDatabase**, **ManagedSqlServer**, **SQLServer2012**, **SQLServer2014**, **SQLServer2016**, **SQLServerLinux2017**, **SQLServerWindows2017**, **SqlServerWindows2019**e **SqlServerLinux2019**.  |
|**AuthenticationMethod** | O método de autenticação para se conectar aos destinos de SQL Server que você deseja avaliar. Os valores possíveis são **SQLAuth** e **WindowsAuth**. |
|**OutputLocation** | O diretório no qual armazenar o arquivo de saída de avaliação JSON. Dependendo do número de bancos de dados que estão sendo avaliados e do número de objetos dentro dos bancos de dados, as avaliações podem levar um tempo excepcionalmente longo. O arquivo será gravado depois que todas as avaliações forem concluídas. |

Se houver um erro inesperado, a janela de comando que é iniciada por esse processo será encerrada.  Examine o log de erros para determinar por que ele falhou.

  ![Local do log de erros](../dma/media//dma-consolidatereports/dma-error-log-file-location.png)

## <a name="consuming-the-assessment-json-file"></a>Consumindo o arquivo JSON de avaliação

Após a conclusão da avaliação, agora você estará pronto para importar os dados para SQL Server para análise. Para consumir o arquivo JSON de avaliação, abra o PowerShell e execute a função dmaProcessor.

  ![listagem de funções dmaProcessor](../dma/media//dma-consolidatereports/dma-dmaProcessor-function-listing.png)

Os parâmetros associados à função dmaProcessor são descritos na tabela a seguir.

|Parâmetro  |Descrição |
|---------|---------|
|**processo** | O local para o qual o arquivo JSON será processado. Os valores possíveis são **SqlServer** e **AzureSQLDatabase**. |
|**serverName** | A instância de SQL Server para a qual os dados serão processados.  Se você especificar **AzureSQLDatabase** para o parâmetro **processto** , inclua somente o nome SQL Server (não include. Database.Windows.net). Você será solicitado a fornecer dois logons ao direcionar o banco de dados SQL do Azure; a primeira é suas credenciais de locatário do Azure, enquanto a segunda é seu logon de administrador para o SQL Server do Azure. |
|**CreateDMAReporting** | O banco de dados de preparo a ser criado para processar o arquivo JSON.  Se o banco de dados especificado já existir e você definir esse parâmetro como um, os objetos não serão criados.  Esse parâmetro é útil para recriar um único objeto que foi Descartado. |
|**Createdatawarehouse** | Cria o data warehouse que será usado pelo relatório de Power BI. |
|**NomeDoBancoDeDados** | O nome do banco de dados DMAReporting. |
|**warehousename** | O nome do banco de dados data warehouse. |
|**jsonDirectory** | O diretório que contém o arquivo de avaliação JSON.  Se houver vários arquivos JSON no diretório, então eles serão processados um a um. |

A função dmaProcessor deve levar apenas alguns segundos para processar um único arquivo.

## <a name="loading-the-data-warehouse"></a>Carregando o data warehouse

Depois que o dmaProcessor concluir o processamento dos arquivos de avaliação, os dados serão carregados no banco de dado DMAReporting na tabela ReportData. Neste ponto, você precisa carregar o data warehouse.

1. Use o script loadwarehouse para preencher os valores ausentes nas dimensões.

    O script obterá os dados da tabela ReportData no banco de dados DMAReporting e o carregará no warehouse.  Se houver erros durante esse processo de carregamento, eles provavelmente são resultado de entradas ausentes nas tabelas de dimensões.

2. Carregue o data warehouse.

  ![Conteúdo do loadwarehouse carregado](../dma/media//dma-consolidatereports/dma-load-warehouse-loaded.png)

## <a name="set-your-database-owners"></a>Definir seus proprietários de banco de dados

Embora não seja obrigatório, para obter o maior valor dos relatórios, é recomendável que você defina os proprietários do banco de dados na dimensão **dimDBOwner** e, em seguida, atualize **DBOwnerKey** na tabela **FactAssessment** .  Seguir esse processo permitirá a divisão e a filtragem do relatório de Power BI com base em proprietários de banco de dados específicos.

Você também pode usar o script loadwarehouse para fornecer as instruções TSQL básicas para definir os proprietários do banco de dados.

  ![Proprietários de configuração do loadwarehouse](../dma/media//dma-consolidatereports/dma-load-warehouse-set-owners.png)

## <a name="dma-reports"></a>Relatórios de DMA

1. Abra o modelo relatórios de DMA Power BI no Power BI Desktop.
2. Insira os detalhes do servidor que apontam para o banco de dados **DMAWarehouse** e, em seguida, selecione **carregar**.

   ![O modelo de relatórios de DMA Power BI carregado](../dma/media//dma-consolidatereports/dma-reports-powerbi-template-loaded.png)

   Depois que o relatório atualizar os dados do banco de **DMAWarehouse** , você verá um relatório semelhante ao seguinte.

   ![Exibição de relatório DMAWarehouse](../dma/media//dma-consolidatereports/dma-DMAWarehouse-report1.png)

   > [!TIP]
   > Se você não vir os dados esperados, tente alterar o indicador ativo.  Para obter mais informações, consulte os detalhes na seção a seguir.

## <a name="working-with-dma-reports"></a>Trabalhando com relatórios de DMA

Para trabalhar com relatórios DMA, use marcadores e segmentações para filtrar por:

- Tipos de avaliação (banco de BD SQL do Azure, SQL do Azure MI, SQL local) 
- Nome da Instância
- Nome do Banco de Dados
- Nome da equipe

Para acessar a folha indicadores e filtros, selecione o indicador filtros na página principal do relatório:

![Indicadores e filtros de relatório DMA](../dma/media//dma-consolidatereports/dma-report-bookmarks-filters.png)

A seleção do indicador filtros habilita a seguinte folha:

![Folha de modos de exibição de relatório DMA](../dma/media//dma-consolidatereports/dma-report-views-blade.png)

Você pode usar indicadores para alternar o contexto de relatório entre:

- Avaliações de nuvem do BD SQL do Azure
- Avaliações de nuvem do Azure SQL MI
- Avaliações locais

![Indicadores de exibições de relatório de DMA](../dma/media//dma-consolidatereports/dma-report-bookmarks1.png)

Para ocultar a folha filtros, pressione CTRL e clique no botão voltar:

![Botão voltar dos modos de exibição de relatório DMA](../dma/media//dma-consolidatereports/dma-report-bookmarks-back.png)

Há um prompt na parte inferior esquerda da página do relatório para mostrar se um filtro está aplicado no momento em qualquer um dos seguintes itens:

- FactAssessment – InstanceName
- FactAssessment – DatabaseName
- dimDBOwner-DBOwner

![Filtrar prompt aplicado](../dma/media//dma-consolidatereports/dma-filter-applied-prompt.png)

> [!NOTE]
> Se você executar apenas uma avaliação do banco de dados SQL do Azure, somente os relatórios de nuvem serão preenchidos. Por outro lado, se você executar apenas uma avaliação local, somente os relatórios locais serão preenchidos. No entanto, se você executar uma avaliação do Azure e local e, em seguida, carregar ambas as avaliações em seu depósito, poderá alternar entre os relatórios de nuvem e os relatórios locais pressionando CTRL e clicando no ícone associado.

## <a name="reports-visuals"></a>Visuais de relatórios

Os detalhes exibidos na Power BI relatórios são mostrados nas seções a seguir.

### <a name="readiness-"></a>Preparação

  ![Percentual de preparação de DMA](../dma/media//dma-consolidatereports/dma-readiness-percentage.png)

Esse visual é atualizado com base no contexto de seleção (tudo, instância, banco de dados [múltiplos de]).

### <a name="readiness-count"></a>Contagem de preparação

  ![Contagem de preparação de DMA](../dma/media//dma-consolidatereports/dma-readiness-count.png)

Este visual mostra a contagem de bancos de dados que estão prontos para migrar a contagem de bancos de dados que ainda não estão prontos para serem migrados.

### <a name="readiness-bucket"></a>Bucket de preparação

  ![Bucket de preparação de DMA](../dma/media//dma-consolidatereports/dma-readiness-bucket.png)

Este visual mostra uma divisão dos bancos de dados pelos seguintes buckets de preparação:

- 100% PRONTO
- 75-99% PRONTO
- 50-75% PRONTO
- NÃO ESTÁ PRONTO

### <a name="issues-word-cloud"></a>Problemas na nuvem do Word

  ![Problemas de DMA WordCloud](../dma/media//dma-consolidatereports/dma-issues-word-cloud.png)

Este visual mostra os problemas que estão ocorrendo no momento no contexto de seleção (tudo, instância, banco de dados [múltiplos de]). Quanto maior a palavra aparecer na tela, maior será o número de problemas nessa categoria. Focalizar o ponteiro do mouse sobre uma palavra mostra o número de problemas que ocorrem nessa categoria.

### <a name="database-readiness"></a>Preparação do banco de dados

  ![Relatório de prontidão do banco de dados DMA](../dma/media//dma-consolidatereports/dma-database-readiness-report.png)

Esta seção é a parte principal do relatório, que mostra a prontidão de um banco de dados de instância. Este relatório tem uma hierarquia de busca detalhada de:

- InstanceDatabase
- ChangeCategory
- Título
- ObjectType
- ImpactedObjectName

 ![Análise do relatório de prontidão do banco de dados DMA](../dma/media//dma-consolidatereports/dma-database-readiness-report-drilldown.png)

Esse relatório também serve como o ponto de filtro para criar o relatório do plano de correção.

Para analisar o relatório do plano de correção, clique com o botão direito do mouse em um ponto de dados neste grafo, aponte para **detalhamento**e selecione **planos de correção**.

Esta tarefa filtra o relatório do plano de correção para o nível de hierarquia atual com base no ponto em que você seleciona a opção Drill-through.

  ![Detalhamento de relatório de prontidão do banco de dados DMA filtrado](../dma/media//dma-consolidatereports/dma-database-readiness-report-drilldown-filtered.png)

  ![Relatório de plano de correção de DMA](../dma/media//dma-consolidatereports/dma-remediation-plan-report.png)

Você também pode usar o relatório de plano de correção por conta própria para criar um plano de correção personalizado usando os filtros na folha **filtros de visualizações** .

  ![Opções de filtro de relatório do plano de correção DMA](../dma/media//dma-consolidatereports/dma-remediation-plan-report-filter-options.png)

### <a name="script-disclaimer"></a>Aviso de script

*Os scripts de exemplo fornecidos neste artigo não têm suporte em nenhum programa ou serviço de suporte padrão da Microsoft. Todos os scripts são fornecidos como estão sem garantias de qualquer tipo. A Microsoft também se isenta de todas as garantias implícitas, incluindo, sem limitação, quaisquer garantias implícitas de comercialização ou adequação a uma finalidade específica. Todo o risco resultante do uso ou do desempenho dos scripts de exemplo e da documentação permanece com você. Em nenhuma circunstância a Microsoft, seus autores ou qualquer outra pessoa envolvida na criação, a produção, ou a entrega dos scripts, é responsabilizada por qualquer dano (incluindo, sem limitação, danos à perda de lucros comerciais, interrupções de negócios, perda de informações comerciais ou outra perda de pecuniary) resultante do uso ou incapacidade de usar os scripts de exemplo ou a documentação, mesmo que a Microsoft tenha sido avisada da possibilidade de tais danos.  Procure permissão antes de republicar esses scripts em outros sites/repositórios/Blogs.*
