---
title: Identificar a SKU certa de banco de dados de SQL do Azure para seu banco de dados local (Assistente de migração de dados) | Microsoft Docs
description: Saiba como usar o Assistente de migração de dados para identificar o direito de SKU de banco de dados SQL do Azure para seu banco de dados local
ms.custom: ''
ms.date: 10/20/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: pochiraju
ms.author: rajpo
manager: craigg
ms.openlocfilehash: 6e990d8b3320eafccc3da574476fa66cdf52d8d5
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52544114"
---
# <a name="identify-the-right-azure-sql-database-sku-for-your-on-premises-database"></a>Identificar a SKU certa de banco de dados de SQL do Azure para seu banco de dados local

A tarefa de migrar seus bancos de dados para a nuvem é um complicado e demorado, que envolvem um número de variáveis. Escolher o SKU e o destino de banco de dados do Azure correta para seu banco de dados pode ser um desafio. Nosso objetivo com o banco de dados de DMA (Migration Assistant) é para tratar essas questões e fazer com que a migração de banco de dados experiência simples e eficiente.

Este artigo se concentra principalmente no recurso de recomendações de SKU de banco de dados SQL do Azure do DMA, que permite que você identifique o mínimo recomendado de SKU de banco de dados SQL do Azure com base nos contadores de desempenho coletados dos computadores de seus bancos de dados de hospedagem. Esse recurso fornece recomendações relacionadas ao preço da camada, nível de computação e tamanho máximo de dados, bem como o custo estimado por mês. Ele também oferece a capacidade de provisionar todos os seus bancos de dados do Azure em massa.

> [!NOTE] 
> Essa funcionalidade está disponível atualmente apenas por meio de Interface de linha de comando (CLI). Suporte para esse recurso por meio da interface do usuário DMA será adicionado em uma versão futura.

> [!IMPORTANT]
> Recomendações de SKU para o banco de dados SQL estão disponíveis atualmente para migrações do SQL Server 2016 ou posterior.

As instruções a seguir o ajudarão a determinar as recomendações de SKU de banco de dados SQL do Azure e provisionar bancos de dados associados para o Azure, usando o Assistente de migração de dados.

## <a name="prerequisites"></a>Prerequisites

Baixe o Assistente de migração de banco de dados v4.0 ou posterior e, em seguida, instalá-lo. Se você já tiver a ferramenta instalado, feche e reabra-, e você será solicitado a atualizar a ferramenta.

## <a name="collect-performance-counters"></a>Coletar contadores de desempenho

A primeira etapa no processo é coletar contadores de desempenho para seus bancos de dados. Você pode coletar contadores de desempenho, executando um comando do PowerShell no computador que hospeda seus bancos de dados. DMA fornece uma cópia desse arquivo do PowerShell, mas você também pode usar seu próprio método para capturar os contadores de desempenho do seu computador.

Você não precisa executar essa tarefa para cada banco de dados individualmente. Os contadores de desempenho coletados de um computador podem ser usados para recomendar a SKU para todos os bancos de dados hospedados no computador.

> [!IMPORTANT]
> O computador do qual você está executando este comando requer permissões de administrador para o computador que hospeda seus bancos de dados.

1. Verifique se o arquivo do PowerShell necessário para coletar os contadores de desempenho é instalado na pasta DMA.

    ![Arquivo do PowerShell mostrado na pasta DMA](../dma/media/dma-sku-recommend-data-collection-file.png)

2. Execute o script do PowerShell com os seguintes argumentos:
    - **ComputerName**: O nome do computador que hospeda seus bancos de dados.
    - **OutputFilePath**: O caminho do arquivo de saída para salvar os contadores coletados.
    - **CollectionTimeInSeconds**: A quantidade de tempo durante o qual você deseja coletar dados do contador de desempenho.
      Capture os contadores de desempenho para pelo menos de 40 minutos obter uma recomendação significativa. Quanto maior a duração da captura, mais precisos a recomendação será.
    - **DbConnectionString**: A cadeia de caracteres de Conexão que aponta para o banco de dados mestre, hospedado no computador do qual você está coletando dados do contador de desempenho.
     
    Aqui está uma invocação de exemplo:

    ```
    .\SkuRecommendationDataCollectionScript.ps1
     -ComputerName Foobar1
     -OutputFilePath D:\counters2.csv
     -CollectionTimeInSeconds 10
     -DbConnectionString "Server=localhost;Initial Catalog=master;Integrated Security=SSPI;"
    ```
    
    Depois que o comando é executado, o processo produzirá um arquivo com contadores de desempenho no local especificado. Esse arquivo pode ser usado como entrada para o comando de recomendação de SKU na próxima seção.

## <a name="use-the-dma-cli-to-get-sku-recommendations"></a>Usar a CLI de DMA para obter recomendações de SKU

Use o arquivo de saída de contadores de desempenho da etapa anterior como entrada para esta etapa. O DMA lhe fornecerá recomendações para o banco de dados do SQL Azure tipo de preço, o nível de computação e o tamanho máximo dos dados para cada banco de dados em seu computador. O DMA também fornecerá o custo mensal estimado para cada banco de dados.

Execute o dmacmd.exe com os seguintes argumentos:

- **/ Ação = SkuRecommendation**: Insira esse argumento para executar avaliações de SKU.
- **/ SkuRecommendationInputDataFilePath**: O caminho para o arquivo de contador são coletados na seção anterior.
- **/ SkuRecommendationTsvOutputResultsFilePath**: O caminho para gravar os resultados de saída no formato TSV.
- **/ SkuRecommendationJsonOutputResultsFilePath**: O caminho para gravar os resultados de saída no formato JSON.
- **/ SkuRecommendationHtmlResultsFilePath**: Caminho no qual gravar os resultados de saída no formato HTML.

Além disso, você precisa escolher um dos argumentos a seguir:
- Impedir que a atualização de preço
    - **/ SkuRecommendationPreventPriceRefresh**: Impede que o preço de atualização ocorra. Use se executando no modo offline.
- Obter os preços mais recentes 
    - **/ SkuRecommendationCurrencyCode**: A moeda na qual exibir os preços (por exemplo "US").
    - **/ SkuRecommendationOfferName**: A oferta de nome (por exemplo "MS-AZR - 0003P"). Para obter mais informações, consulte o [detalhes da oferta do Microsoft Azure](https://azure.microsoft.com/support/legal/offer-details/) página.
    - **/ SkuRecommendationRegionName**: A região (por exemplo, nomeie "Oeste dos EUA").
    - **/ SkuRecommendationSubscriptionId**: A ID da assinatura.
    - **/ AzureAuthenticationTenantId**: O locatário de autenticação.
    - **/ AzureAuthenticationClientId**: A ID do cliente do aplicativo AAD usado para autenticação.
    - Uma das seguintes opções de autenticação:
        - Interativo
            - **AzureAuthenticationInteractiveAuthentication**: Definido como true para uma janela pop-up de autenticação.
        - Baseada em certificado
            - **AzureAuthenticationCertificateStoreLocation**: Definido como o repositório de certificados local (por exemplo "CurrentUser").
            - **AzureAuthenticationCertificateThumbprint**: Defina a impressão digital do certificado.
        - Baseada em token
            - **AzureAuthenticationToken**: Defina como o token de certificado.

Aqui estão alguns invocações de exemplo:

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationCurrencyCode=USD
/SkuRecommendationOfferName=MS-AZR-0044p
/SkuRecommendationRegionName=UKWest
/SkuRecommendationSubscriptionId=<Your Subscription Id>
/AzureAuthenticationInteractiveAuthentication=true
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
```

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true
```

O arquivo de saída TSV conterá as colunas mostradas no gráfico a seguir:

   ![Arquivo do PowerShell mostrado na pasta DMA](../dma/media/dma-tsv-file-column.png)

Segue uma descrição de cada coluna.

- **DatabaseName** -o nome do banco de dados.
- **MetricName** - se de uma métrica foi executada ou não.
- **MetricType** -camada recomendada banco de dados SQL.
- **MetricValue** -recomendado do banco de dados SQL do Azure SKU.
- **SQLMiEquivalentCores** -se você escolher Ir para o banco de dados de instância gerenciada do SQL, você pode usar esse valor para contagem de núcleos.
- **IsTierRecommended** -podemos fazer uma recomendação mínima do SKU para cada camada. Em seguida, aplicamos heurística para determinar a camada certa para seu banco de dados. 
- **ExclusionReasons** -esse valor estará em branco se uma camada é recomendada. Para cada camada que não é recomendada, nós fornecemos os motivos por que ele não foi escolhido.
- **AppliedRules** -uma notação curta das regras que foram aplicadas.

O valor recomendado é o SKU mínimo necessário para suas consultas para execução no Azure com uma taxa de sucesso semelhante a seus bancos de dados local. Por exemplo, se a SKU de mínima recomendada é S4 para a camada standard, em seguida, escolha S3 ou abaixo será fazer com que consultas atingir o tempo limite ou não ser executada.

O arquivo HTML contém essas informações em um formato gráfico. Você pode usar o arquivo HTML para inserir informações de assinatura do Azure, escolha o tipo de preço, computação nível e o tamanho máximo de dados para seus bancos de dados e gerar um script para provisionar seus bancos de dados. Esse script pode ser executado usando o PowerShell.

## <a name="provision-your-databases-to-azure"></a>Provisionar seus bancos de dados do Azure
Com apenas alguns cliques, você pode usar as recomendações da etapa anterior para provisionar bancos de dados de destino no Azure para o qual você pode migrar seus bancos de dados. Você também pode fazer alterações para as recomendações, atualizando o arquivo HTML da seguinte maneira.

1. Abra o arquivo HTML e insira as seguintes informações:
    - **ID da assinatura** -a ID da assinatura da assinatura do Azure ao qual você deseja provisionar os bancos de dados.
    - **Região** -a região na qual você deseja provisionar bancos de dados. Certifique-se de que sua assinatura dá suporte a região de select.
    - **Grupo de recursos** -o grupo de recursos ao qual você deseja implantar os bancos de dados. Insira um grupo de recursos existente.
    - **Nome do servidor** -servidor o banco de dados do SQL do Azure ao qual você deseja que os bancos de dados implantados. Se você inserir um nome de servidor que não existe, ele será criado.
    - **Admin Username\Password** -o nome de usuário de administrador de servidor e a senha.

2. Analise as recomendações para cada banco de dados e modificar o tipo de preço, computação nível e o tamanho máximo de dados conforme necessário. Certifique-se de desmarcar quaisquer bancos de dados que você não deseja atualmente para provisionar.

3. Selecione **Gerar Script de provisionamento**, salve o script e, em seguida, executá-lo no PowerShell.

    Esse processo deve criar todos os bancos de dados que você selecionou na página HTML.

Você pode executar todas as etapas neste processo em um único computador ou você pode executá-las em vários computadores para determinar as recomendações de SKU em grande escala. O DMA torna uma experiência simples e escalonável, oferecendo suporte a todas essas etapas por meio da Interface de linha de comando. Novamente, suporte para esse recurso por meio da interface do usuário DMA estará disponível posteriormente neste ano.

## <a name="next-steps"></a>Próximas etapas
- Baixe a versão mais recente do [Assistente de migração de dados](https://aka.ms/get-dma).
- Consulte o artigo [executar Assistente de migração dados da linha de comando](https://docs.microsoft.com/sql/dma/dma-commandline?view=sql-server-2017) para obter uma lista completa de comandos para executar o DMA da CLI.
