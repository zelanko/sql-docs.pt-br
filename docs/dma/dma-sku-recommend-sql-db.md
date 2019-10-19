---
title: Identificar o SKU do banco de dados SQL do Azure correto para seu banco de dados local (Assistente de Migração de Dados) | Microsoft Docs
description: Saiba como usar Assistente de Migração de Dados para identificar o SKU do banco de dados SQL do Azure correto para seu banco de dados local
ms.custom: ''
ms.date: 05/06/2019
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
ms.author: jtoland
ms.openlocfilehash: d6d329b97946d9d8042641653ed0167510a19b17
ms.sourcegitcommit: ac90f8510c1dd38d3a44a45a55d0b0449c2405f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2019
ms.locfileid: "72586734"
---
# <a name="identify-the-right-azure-sql-databasemanaged-instance-sku-for-your-on-premises-database"></a>Identificar o SKU do banco de dados SQL/Instância Gerenciada do Azure correto para seu banco de dados local

A migração de bancos de dados para a nuvem pode ser complicada, especialmente ao tentar selecionar o melhor destino de banco de dados do Azure e SKU para seu banco de dados. Nossa meta com o Assistente de Migração de banco de dados (DMA) é ajudar a resolver essas perguntas e facilitar sua experiência de migração de banco de dados fornecendo essas recomendações de SKU em uma saída amigável.

Este artigo se concentra no recurso de recomendações de SKU do banco de dados SQL do Azure do DMA. O banco de dados SQL do Azure tem várias opções de implantação, incluindo:

- Banco de dados individual
- Pools elásticos
- Instância gerenciada

O recurso de recomendações de SKU permite que você identifique o banco de dados individual do banco de dados SQL do Azure ou o SKU de instância gerenciada mínimo recomendado com base nos contadores de desempenho coletados dos computadores que hospedam seus bancos de dados. O recurso fornece recomendações relacionadas ao tipo de preço, nível de computação e tamanho máximo de dados, bem como ao custo estimado por mês. Ele também oferece a capacidade de provisionar em massa bancos de dados individuais e instâncias gerenciadas no Azure para todos os bancos de dados recomendados.

> [!NOTE]
> Essa funcionalidade está disponível no momento apenas por meio da CLI (interface de linha de comando).

Veja a seguir as instruções para ajudá-lo a determinar as recomendações de SKU do banco de dados SQL do Azure e provisionar os bancos de dados individuais correspondentes ou instâncias gerenciadas no Azure usando DMA.

## <a name="prerequisites"></a>Pré-requisitos

- Baixe e instale a versão mais recente do [DMA](https://aka.ms/get-dma). Se você já tiver uma versão anterior da ferramenta, abra-a e será solicitado a atualizar o DMA.
- Verifique se o computador tem o [PowerShell versão 5,1](https://www.microsoft.com/download/details.aspx?id=54616) ou posterior, que é necessário para executar todos os scripts. Para obter informações sobre como findoug a versão do PowerShell que está instalada em seu computador, consulte o artigo [baixar e instalar o Windows PowerShell 5,1](https://docs.microsoft.com/skypeforbusiness/set-up-your-computer-for-windows-powershell/download-and-install-windows-powershell-5-1).
- Verifique se o seu computador tem o módulo do Azure PowerShell instalado. Para obter mais informações, consulte o artigo [instalar o Azure PowerShell Module](https://docs.microsoft.com/powershell/azure/install-az-ps?view=azps-1.8.0).
- Verifique se o arquivo do PowerShell **SkuRecommendationDataCollectionScript. ps1**, que é necessário para coletar os contadores de desempenho, está instalado na pasta DMA.
- Verifique se o computador no qual você executará esse processo tem permissões de administrador para o computador que está hospedando seus bancos de dados.

## <a name="collect-performance-counters"></a>Coletar contadores de desempenho

A primeira etapa do processo é coletar contadores de desempenho para seus bancos de dados. Você pode coletar contadores de desempenho executando um comando do PowerShell no computador que hospeda seus bancos de dados. O DMA fornece uma cópia desse arquivo do PowerShell, mas você também pode usar seu próprio método para capturar contadores de desempenho do seu computador.

Você não precisa executar essa tarefa individualmente para cada banco de dados. Os contadores de desempenho coletados de um computador podem ser usados para recomendar a SKU para todos os bancos de dados hospedados no computador.

1. Na pasta DMA, localize o arquivo do PowerShell SkuRecommendationDataCollectionScript. ps1. Esse arquivo é necessário para coletar os contadores de desempenho.

    ![Arquivo do PowerShell mostrado na pasta DMA](../dma/media/dma-sku-recommend-data-collection-file.png)

2. Execute o script do PowerShell com os seguintes argumentos:
    - **ComputerName**: o nome do computador que hospeda seus bancos de dados.
    - **OutputFilePath**: o caminho do arquivo de saída para salvar os contadores coletados.
    - **CollectionTimeInSeconds**: a quantidade de tempo durante a qual você deseja coletar dados do contador de desempenho. Capture contadores de desempenho por pelo menos 40 minutos para obter uma recomendação significativa. Quanto maior a duração da captura, mais precisa será a recomendação. Além disso, verifique se as cargas de trabalho estão em execução para os bancos de dados desejados para permitir recomendações mais precisas.
    - **Dbconnectionstring**: a cadeia de conexão que aponta para o banco de dados mestre hospedado no computador a partir do qual você está coletando dado do contador de desempenho.

    Aqui está uma invocação de exemplo:

    ```
    .\SkuRecommendationDataCollectionScript.ps1
     -ComputerName Foobar1
     -OutputFilePath D:\counters2.csv
     -CollectionTimeInSeconds 2400
     -DbConnectionString "Server=localhost;Initial Catalog=master;Integrated Security=SSPI;"
    ```

    Depois que o comando for executado, o processo produzirá um arquivo que inclui contadores de desempenho para o local especificado. Você pode usar esse arquivo como entrada para a próxima parte do processo, o que fornecerá recomendações de SKU para as opções de banco de dados único e instâncias gerenciadas.

## <a name="use-the-dma-cli-to-get-sku-recommendations"></a>Usar a CLI do DMA para obter recomendações de SKU

Use o arquivo de saída dos contadores de desempenho que você criou como entrada para esse processo.

Para a opção de banco de dados individual, o DMA fornecerá recomendações para o tipo de preço de banco de dados único do banco de dado SQL do Azure, o nível de computação e o tamanho máximo para cada um deles no computador. Se você tiver vários bancos de dados em seu computador, também poderá especificar os bancos de dados para os quais deseja obter recomendações. O DMA também fornecerá o custo mensal estimado para cada banco de dados.

Para a instância gerenciada, as recomendações dão suporte a um cenário de comparação de precisão e deslocamento. Como resultado, o DMA fornecerá recomendações para o tipo de preço da instância gerenciada do banco de dados SQL do Azure, o nível de computação e o tamanho máximo do dado para o conjunto de bancos de dados em seu computador. Novamente, se você tiver vários bancos de dados em seu computador, também poderá especificar os bancos de dados para os quais deseja obter recomendações. O DMA também fornecerá o custo mensal estimado para a instância gerenciada.

Para usar a CLI do DMA para obter recomendações de SKU, no prompt de comando, execute dmacmd. exe com os seguintes argumentos:

- **/Action = SkuRecommendation**: Insira este argumento para executar avaliações de SKU.
- **/SkuRecommendationInputDataFilePath**: o caminho para o arquivo de contador coletado na seção anterior.
- **/SkuRecommendationTsvOutputResultsFilePath**: o caminho para gravar os resultados de saída no formato TSV.
- **/SkuRecommendationJsonOutputResultsFilePath**: o caminho para gravar os resultados de saída no formato JSON.
- **/SkuRecommendationHtmlResultsFilePath**: caminho para gravar os resultados da saída em formato HTML.

Além disso, selecione um dos seguintes argumentos:

- Impedir atualização de preço
  - **/SkuRecommendationPreventPriceRefresh**: se definido como true, impede que a atualização de preço ocorra e assuma os preços padrão. Use se estiver executando no modo offline. Se você não usar esse parâmetro, deverá especificar os parâmetros abaixo para obter os preços mais recentes com base em uma região especificada.
- Obter os preços mais recentes
  - **/SkuRecommendationCurrencyCode**: a moeda na qual os preços são exibidos (por exemplo, "USD").
  - **/SkuRecommendationOfferName**: o nome da oferta (por exemplo, "MS-AZR-0003P"). Para obter mais informações, consulte a página [detalhes da oferta de Microsoft Azure](https://azure.microsoft.com/support/legal/offer-details/) .
    - **/SkuRecommendationRegionName**: o nome da região (por exemplo, "westus").
    - **/SkuRecommendationSubscriptionId**: a ID da assinatura.
    - **/AzureAuthenticationTenantId**: o locatário de autenticação.
    - **/AzureAuthenticationClientId**: a ID do cliente do aplicativo AAD usado para autenticação.
    - Uma das seguintes opções de autenticação:
      - Interactive
        - **AzureAuthenticationInteractiveAuthentication**: Defina como true para uma janela pop-up de autenticação.
      - Baseado em certificado
        - **AzureAuthenticationCertificateStoreLocation**: defina para o local do repositório de certificados (por exemplo, "CurrentUser").
        - **AzureAuthenticationCertificateThumbprint**: defina para a impressão digital do certificado.
      - Baseado em token
        - **AzureAuthenticationToken**: Defina como o token de certificado.

> [!NOTE]
> Para obter o ClientId e a Tenantid para autenticação interativa, você precisa configurar um novo aplicativo do AAD. Para obter mais informações sobre autenticação e obter essas credenciais, no artigo [Microsoft Azure exemplos de código de API de cobrança: API RateCard](https://github.com/Azure-Samples/billing-dotnet-ratecard-api), siga as instruções em **etapa 1: configurar um aplicativo cliente nativo em seu locatário do AAD**.

Por fim, há um argumento opcional que você pode usar para especificar os bancos de dados para os quais deseja obter recomendações: 

- **/SkuRecommendationDatabasesToRecommend**: uma lista de bancos de dados para os quais fazer recomendações. Os nomes de banco de dados diferenciam maiúsculas de minúsculas e devem (1) ser encontrados em Input. csv, (2) cada um entre aspas duplas e (3) cada um deles separado por um único espaço entre os nomes (por exemplo,/SkuRecommendationDatabasesToRecommend = "Database1" "Database2" "Database3") . Omitir esse parâmetro garante que as recomendações sejam fornecidas para todos os bancos de dados de usuário identificados no arquivo Input. csv.  

Abaixo estão algumas invocações de exemplo:

**Exemplo 1: obtendo recomendações com preços padrão. Use ao executar no modo offline ou quando você não tiver credenciais de autenticação.**

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true
```

**Exemplo 2: obtendo recomendações com os preços mais recentes para a região especificada (por exemplo, "UKWest").**

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

**Exemplo 3: obtendo recomendações para bancos de dados específicos (por exemplo, "TPCDS1G, EDW_3G, TPCDS10G").**

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
/SkuRecommendationDatabasesToRecommend=“TPCDS1G” “EDW_3G” “TPCDS10G” 
/AzureAuthenticationInteractiveAuthentication=true 
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId> 
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
```

Para obter recomendações de banco de dados individual, o arquivo de saída TSV terá a seguinte aparência:

![Arquivo de BD único do PowerShell mostrado na pasta DMA](../dma/media/dma-sku-recommend-single-db-recommendations.png)

Para recomendações de instância gerenciada, o arquivo de saída TSV terá a seguinte aparência:

![Arquivo de instância gerenciada do PowerShell mostrado na pasta DMA](../dma/media/dma-sku-recommend-mi-recommendations.png)

Segue uma descrição de cada coluna no arquivo de saída.

- **DatabaseName** -o nome do seu banco de dados.
- **Metrictype** -camada de instância gerenciada/banco de dados SQL do banco de dados único do Azure recomendado.
- **Metricvalue** -SKU do banco de dados SQL do Azure/instância gerenciada recomendada.
- **PricePerMonth** – o preço estimado por mês para o SKU correspondente.
- **RegionName** – o nome da região do SKU correspondente. 
- **IsTierRecommended** – fazemos uma recomendação de SKU mínima para cada camada. Em seguida, aplicamos a heurística para determinar a camada correta para seu banco de dados. Isso reflete qual camada é recomendada para o banco de dados. 
- **ExclusionReasons** -esse valor estará em branco se uma camada for recomendada. Para cada camada que não é recomendada, fornecemos os motivos pelos quais ela não foi selecionada.
- **AppliedRules** – uma breve notação das regras que foram aplicadas.

A camada final recomendada (ou seja, **metrictype**) e o valor (ou seja, **metricvalue**)-encontrados onde a coluna **IsTierRecommended** é true – reflete a SKU mínima necessária para que suas consultas sejam executadas no Azure com uma taxa de êxito semelhante à sua bancos de dados locais. Para a instância gerenciada, o DMA atualmente dá suporte a recomendações para as 8vcore mais usadas para SKUs 40vcore. Por exemplo, se o SKU mínimo recomendado for S4 para a camada Standard, a escolha S3 ou abaixo fará com que as consultas expirem o tempo limite ou falham na execução.

O arquivo HTML contém essas informações em um formato gráfico. Ele fornece um meio amigável de exibir a recomendação final e provisionar a próxima parte do processo. Mais informações sobre a saída HTML estão na seção a seguir.

## <a name="provision-recommended-skus-to-azure"></a>Provisionar SKUs recomendados para o Azure

Com apenas alguns cliques, você pode usar as recomendações identificadas para provisionar SKUs de destino no Azure para os quais você pode migrar seus bancos de dados. Você pode usar o arquivo HTML para inserir a assinatura do Azure; Escolha o tipo de preço, o nível de computação e o tamanho máximo dos dados para seus bancos de dado; e gerar um script para provisionar seus bancos de dados. Você pode executar esse script usando o PowerShell.

Você pode executar esse processo em um único computador ou pode executá-lo em vários computadores para determinar as recomendações de SKU em escala. Atualmente, o DMA torna uma experiência simples e escalonável ao dar suporte a todo o processo por meio da interface de linha de comando.

Para inserir informações de provisionamento e fazer alterações nas recomendações, atualize o arquivo HTML da seguinte maneira.

**Para obter recomendações de banco de dados individual**

![Tela de recomendações de SKU do BD SQL do Azure](../dma/media/dma-sku-recommend-single-db-recommendations1.png)

1. Abra o arquivo HTML e insira as seguintes informações:
    - **ID da assinatura** -a ID da assinatura do Azure para a qual você deseja provisionar os bancos de dados.
    - **Grupo de recursos** -o grupo de recursos no qual você deseja implantar os bancos de dados. Insira um grupo de recursos que exista.
    - **Região** -a região na qual provisionar bancos de dados. Verifique se sua assinatura dá suporte à região selecionada.
    - **Nome do servidor** -o servidor do banco de dados SQL do Azure para o qual você deseja implantar os bancos. Se você inserir um nome de servidor que não existe, ele será criado.
    - **Nome de usuário do administrador** -o nome de usuário do administrador do servidor.
    - **Senha de administrador** -a senha de administrador do servidor. A senha deve ter pelo menos oito caracteres e no máximo 128 caracteres de comprimento. Sua senha deve conter caracteres de três das seguintes categorias – letras maiúsculas, letras minúsculas, números (0-9) e caracteres não alfanuméricos (!, $, #,%, etc.). A senha não pode conter todo ou parte (3 + letras consecutivas) do nome de usuário.

2. Revise as recomendações para cada banco de dados e modifique o tipo de preço, o nível de computação e o tamanho máximo do dado, conforme necessário. Certifique-se de anular a seleção de todos os bancos de dados que você não deseja provisionar no momento.

3. Selecione **gerar script de provisionamento**, salve o script e, em seguida, execute-o no PowerShell.

    Esse processo deve criar todos os bancos de dados selecionados na página HTML.

**Para recomendações de instância gerenciada**

![Tela de recomendações de SKU do SQL do Azure](../dma/media/dma-sku-recommend-mi-recommendations1.png)

1. Abra o arquivo HTML e insira as seguintes informações:
    - **ID da assinatura** -a ID da assinatura do Azure para a qual você deseja provisionar os bancos de dados.
    - **Grupo de recursos** -o grupo de recursos no qual você deseja implantar os bancos de dados. Insira um grupo de recursos que exista.
    - **Região** -a região na qual provisionar bancos de dados. Verifique se sua assinatura dá suporte à região selecionada.
    - **Nome da instância** – a instância do Azure SQL instância gerenciada para a qual você deseja migrar os bancos de dados. O nome da instância pode conter apenas letras minúsculas, números e '-', mas não pode começar ou terminar com '-' ou ter mais de 63 caracteres.
    - **Nome de usuário administrador da instância** – o nome de usuário do administrador da instância. Verifique se o nome de logon atende aos seguintes requisitos – é um identificador SQL e não um nome de sistema típico (como admin, administrador, SA, raiz, DBManager, loginmanager, etc.) ou um usuário ou função de banco de dados interno (como dbo, Guest, público etc.). Verifique se seu nome não contém espaços em branco, caracteres Unicode ou caracteres não alfabéticos e se ele não começa com números ou símbolos. 
    - **Senha do administrador da instância** -a senha de administrador da instância. Sua senha deve ter pelo menos 16 caracteres e no máximo 128 caracteres de comprimento. Sua senha deve conter caracteres de três das seguintes categorias – letras maiúsculas, letras minúsculas, números (0-9) e caracteres não alfanuméricos (!, $, #,%, etc.). A senha não pode conter todo ou parte (3 + letras consecutivas) do nome de usuário.
    - **Nome da vnet** – o nome da vnet sob a qual a instância gerenciada deve ser provisionada. Insira um nome de VNet existente.
    - **Nome da sub-rede** – o nome da sub-rede sob a qual a instância gerenciada deve ser provisionada. Insira um nome de sub-rede existente.

2. Examine as recomendações para cada instância e modifique o tipo de preço, o nível de computação e o tamanho máximo dos dados conforme necessário. Embora as recomendações estejam atualmente limitadas a 8vcore para SKUs 40vcore, ainda há a opção de provisionar SKUs 64vcore e 80vcore, se desejado. Não se esqueça de desmarcar as instâncias que você não deseja provisionar no momento.

    Esse processo deve criar todos os bancos de dados selecionados na página HTML.

    > [!NOTE]
    > A criação de instâncias gerenciadas em uma sub-rede (especialmente pela primeira vez) pode levar várias horas para ser concluída. Depois de executar o script de provisionamento por meio do PowerShell, você pode verificar o status de sua implantação no portal do Azure.

## <a name="next-step"></a>Próxima etapa

- Para obter uma lista completa de comandos para executar o DMA da CLI, consulte o artigo [executar assistente de migração de dados na linha de comando](https://docs.microsoft.com/sql/dma/dma-commandline?view=sql-server-2017).
