---
title: Identificar a SKU certa de banco de dados de SQL do Azure para seu banco de dados local (Assistente de migração de dados) | Microsoft Docs
description: Saiba como usar o Assistente de migração de dados para identificar o direito de SKU de banco de dados SQL do Azure para seu banco de dados local
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
manager: craigg
ms.openlocfilehash: c67eca111ecd0a51bc8e70d747cb7b713fe54ca8
ms.sourcegitcommit: 249c0925f81b7edfff888ea386c0deaa658d56ec
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/30/2019
ms.locfileid: "66413635"
---
# <a name="identify-the-right-azure-sql-databasemanaged-instance-sku-for-your-on-premises-database"></a>Identificar o direito de SKU de instância de banco de dados/gerenciado do Azure SQL para seu banco de dados local

Migrando bancos de dados para a nuvem podem ser complicados, especialmente ao tentar selecionar o melhor destino de banco de dados do Azure e o SKU do banco de dados. Nosso objetivo com o banco de dados de DMA (Migration Assistant) é ajudar a tratar essas questões e facilitar a migração de banco de dados a experiência, fornecendo essas recomendações de SKU em uma saída amigável.

Este artigo se concentra no recurso de recomendações de SKU de banco de dados SQL do Azure do DMA. Banco de dados SQL do Azure tem várias opções de implantação, incluindo:

- Banco de dados individual
- Pools Elásticos
- instância gerenciada

As recomendações de SKU de recurso permite que você identifique o mínimo recomendado de banco de dados individual do banco de dados SQL ou instância gerenciada SKU com base nos contadores de desempenho coletados dos computadores de seus bancos de dados de hospedagem. O recurso fornece recomendações relacionadas ao preço da camada, nível de computação e tamanho máximo de dados, bem como o custo estimado por mês. Ele também oferece a capacidade de provisionar em massa bancos de dados único e instâncias gerenciadas no Azure para todos os bancos de dados recomendados.

> [!NOTE]
> Essa funcionalidade está disponível atualmente apenas por meio de Interface de linha de comando (CLI).

A seguir estão as instruções para ajudá-lo a determinar as recomendações de SKU de banco de dados SQL do Azure e provisionar bancos de dados únicos correspondentes ou instância (s) gerenciado no Azure usando o DMA.

## <a name="prerequisites"></a>Prerequisites

- Baixe e instale a versão mais recente do [DMA](https://aka.ms/get-dma). Se você já tiver uma versão anterior da ferramenta, abri-lo, e você será solicitado a atualizar o DMA.
- Certifique-se de que o computador tenha [PowerShell versão 5.1](https://www.microsoft.com/download/details.aspx?id=54616) ou posterior, que é necessário para executar todos os scripts. Para obter informações sobre findoug qual versão do PowerShell é instalada em seu computador, consulte o artigo [Baixe e instale o Windows PowerShell 5.1](https://docs.microsoft.com/skypeforbusiness/set-up-your-computer-for-windows-powershell/download-and-install-windows-powershell-5-1).
- Certifique-se de que o computador tenha o módulo do Powershell do Azure instalado. Para obter mais informações, consulte o artigo [instalar o módulo Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-az-ps?view=azps-1.8.0).
- Verificar se o arquivo do PowerShell **SkuRecommendationDataCollectionScript.ps1**, que é necessário para coletar os contadores de desempenho, é instalado na pasta DMA.
- Certifique-se de que o computador no qual você vai executar esse processo tem permissões de administrador no computador que hospeda seus bancos de dados.

## <a name="collect-performance-counters"></a>Coletar contadores de desempenho

A primeira etapa no processo é coletar contadores de desempenho para seus bancos de dados. Você pode coletar contadores de desempenho, executando um comando do PowerShell no computador que hospeda seus bancos de dados. DMA fornece uma cópia desse arquivo do PowerShell, mas você também pode usar seu próprio método para capturar os contadores de desempenho do seu computador.

Você não precisa executar essa tarefa para cada banco de dados individualmente. Os contadores de desempenho coletados de um computador podem ser usados para recomendar a SKU para todos os bancos de dados hospedados no computador.

1. Na pasta DMA, localize o arquivo do PowerShell SkuRecommendationDataCollectionScript.ps1. Este arquivo é necessário para coletar os contadores de desempenho.

    ![Arquivo do PowerShell mostrado na pasta DMA](../dma/media/dma-sku-recommend-data-collection-file.png)

2. Execute o script do PowerShell com os seguintes argumentos:
    - **ComputerName**: O nome do computador que hospeda seus bancos de dados.
    - **OutputFilePath**: O caminho do arquivo de saída para salvar os contadores coletados.
    - **CollectionTimeInSeconds**: A quantidade de tempo durante o qual você deseja coletar dados do contador de desempenho. Capture os contadores de desempenho para pelo menos de 40 minutos obter uma recomendação significativa. Quanto maior a duração da captura, mais precisos a recomendação será. Além disso, verifique se que as cargas de trabalho estão em execução para os bancos de dados desejados habilitar as recomendações mais precisas.
    - **DbConnectionString**: A cadeia de caracteres de Conexão que aponta para o banco de dados mestre, hospedado no computador do qual você está coletando dados do contador de desempenho.

    Aqui está uma invocação de exemplo:

    ```
    .\SkuRecommendationDataCollectionScript.ps1
     -ComputerName Foobar1
     -OutputFilePath D:\counters2.csv
     -CollectionTimeInSeconds 2400
     -DbConnectionString "Server=localhost;Initial Catalog=master;Integrated Security=SSPI;"
    ```

    Depois que o comando é executado, o processo produzirá um arquivo, incluindo contadores de desempenho para o local especificado. Você pode usar esse arquivo como entrada para a próxima parte do processo, que fornece recomendações de SKU para o banco de dados individual e opções de instâncias gerenciadas.

## <a name="use-the-dma-cli-to-get-sku-recommendations"></a>Usar a CLI de DMA para obter recomendações de SKU

Use o arquivo de saída de contadores de desempenho você criou como entrada para esse processo.

Para a opção de banco de dados individual, DMA fornece recomendações para o banco de dados SQL único banco de dados de tipo de preço, o nível de computação e o tamanho máximo dos dados para cada banco de dados em seu computador. Se você tiver vários bancos de dados em seu computador, você também pode especificar os bancos de dados para o qual você deseja que as recomendações. O DMA também fornecerá o custo mensal estimado para cada banco de dados.

Para a instância gerenciada, as recomendações de suportam a um cenário de lift-and-shift. Como resultado, o DMA fornecerá recomendações para a instância gerenciada do banco de dados SQL tipo de preço, o nível de computação e o tamanho máximo dos dados para o conjunto de bancos de dados em seu computador. Novamente, se você tiver vários bancos de dados em seu computador, você também pode especificar os bancos de dados para o qual você deseja que as recomendações. O DMA também fornecerá o custo mensal estimado para a instância gerenciada.

Para usar a CLI DMA para obter recomendações de SKU, no prompt de comando, execute dmacmd.exe com os seguintes argumentos:

- **/Action=SkuRecommendation**: Insira esse argumento para executar avaliações de SKU.
- **/SkuRecommendationInputDataFilePath**: O caminho para o arquivo de contador são coletados na seção anterior.
- **/SkuRecommendationTsvOutputResultsFilePath**: O caminho para gravar os resultados de saída no formato TSV.
- **/SkuRecommendationJsonOutputResultsFilePath**: O caminho para gravar os resultados de saída no formato JSON.
- **/SkuRecommendationHtmlResultsFilePath**: Caminho no qual gravar os resultados de saída no formato HTML.

Além disso, selecione um dos argumentos a seguir:

- Impedir que a atualização de preço
  - **/SkuRecommendationPreventPriceRefresh**: Se definido como verdadeiro, impede que a atualização de preço ocorra e pressupõe que os preços padrão. Use se executando no modo offline. Se você não usar esse parâmetro, você deve especificar os parâmetros a seguir para obter os preços mais recentes com base em uma região especificada.
- Obter os preços mais recentes
  - **/SkuRecommendationCurrencyCode**: A moeda na qual exibir os preços (por exemplo "US").
  - **/SkuRecommendationOfferName**: A oferta de nome (por exemplo "MS-AZR-0003P"). Para obter mais informações, consulte o [detalhes da oferta do Microsoft Azure](https://azure.microsoft.com/support/legal/offer-details/) página.
    - **/SkuRecommendationRegionName**: O nome da região (por exemplo, "Oeste dos EUA").
    - **/SkuRecommendationSubscriptionId**: A ID da assinatura.
    - **/AzureAuthenticationTenantId**: O locatário de autenticação.
    - **/AzureAuthenticationClientId**: A ID do cliente do aplicativo AAD usado para autenticação.
    - Uma das seguintes opções de autenticação:
      - Interativo
        - **AzureAuthenticationInteractiveAuthentication**: Definido como true para uma janela pop-up de autenticação.
      - Baseada em certificado
        - **AzureAuthenticationCertificateStoreLocation**: Defina como o repositório de certificados local (por exemplo, "CurrentUser").
        - **AzureAuthenticationCertificateThumbprint**: Defina a impressão digital do certificado.
      - Baseada em token
        - **AzureAuthenticationToken**: Defina como o token de certificado.

> [!NOTE]
> Para obter o ClientId e TenantId para a autenticação interativa, você precisará configurar um novo aplicativo do AAD. Para obter mais informações sobre autenticação e obter essas credenciais, no artigo [exemplos de código de API de cobrança do Microsoft Azure: API RateCard](https://azure.microsoft.com/resources/samples/billing-python-ratecard-api/), siga as instruções em **etapa 1: Configurar um aplicativo cliente nativo em seu locatário do AAD**.

Finalmente, há um argumento opcional que você pode usar para especificar os bancos de dados para o qual você deseja que as recomendações: 

- **/SkuRecommendationDatabasesToRecommend**: Uma lista de bancos de dados para o qual fazer recomendações. O banco de dados nomes diferenciam maiusculas de minúsculas e devem (1) encontrado no. csv de entrada, (2) cada ser cercada por aspas duplas e (3) ser separados por um único espaço entre nomes (por exemplo, /SkuRecommendationDatabasesToRecommend = "Database1" "Database2" "Database3") . Omitir esse parâmetro Certifique-se de que as recomendações são fornecidas para todos os bancos de dados de usuário, identificados no arquivo de entrada. csv.  

Abaixo estão alguns invocações de exemplo:

**Exemplo 1: Obtendo recomendações aos preços padrão. Use quando em execução no modo offline ou quando você não tem credenciais de autenticação.**

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true
```

**Exemplo 2: Obter recomendações com preços mais recentes para a região especificada (por exemplo, "UKWest").**

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

**Exemplo 3: Obter recomendações para bancos de dados específicos (por exemplo “TPCDS1G,EDW_3G,TPCDS10G”).**

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

Para obter recomendações de banco de dados individual, o arquivo de saída TSV será semelhante ao seguinte:

![Arquivo do PowerShell único-banco de dados mostrado na pasta DMA](../dma/media/dma-sku-recommend-single-db-recommendations.png)

Para obter recomendações de instância gerenciada, o arquivo de saída TSV será semelhante ao seguinte:

![Arquivo de instância gerenciada do PowerShell mostrado na pasta DMA](../dma/media/dma-sku-recommend-mi-recommendations.png)

Segue uma descrição de cada coluna no arquivo de saída.

- **DatabaseName** -o nome do banco de dados.
- **MetricType** -camada recomendada do Azure SQL Database único banco de dados/gerenciado da instância.
- **MetricValue** -recomendado do Azure SQL Database único banco de dados/gerenciado da instância SKU.
- **PricePerMonth** – preço estimado por mês para a SKU correspondente.
- **RegionName** – o nome da região para a SKU correspondente. 
- **IsTierRecommended** -podemos fazer uma recomendação mínima do SKU para cada camada. Em seguida, aplicamos heurística para determinar a camada certa para seu banco de dados. Isso reflete a camada é recomendada para o banco de dados. 
- **ExclusionReasons** -esse valor estará em branco se uma camada é recomendada. Para cada camada que não é recomendada, nós fornecemos os motivos por que ele não foi escolhido.
- **AppliedRules** -uma notação curta das regras que foram aplicadas.

A camada recomendada final (ou seja, **MetricType**) e o valor (ou seja, **MetricValue**)-encontrado em que o **IsTierRecommended** coluna é TRUE - reflete a SKU mínimo necessário para suas consultas para execução no Azure com uma taxa de sucesso semelhante a seus bancos de dados local. Para a instância gerenciada, o DMA atualmente dá suporte a recomendações para o 8vcore mais comumente usado para SKUs 40vcore. Por exemplo, se a SKU de mínima recomendada é S4 para a camada standard, em seguida, escolha S3 ou abaixo será fazer com que consultas atingir o tempo limite ou não ser executada.

O arquivo HTML contém essas informações em um formato gráfico. Ele fornece um meio fácil de usar de exibir a recomendação final e a próxima parte do processo de provisionamento. Mais informações sobre a saída HTML estão na seção a seguir.

## <a name="provision-recommended-skus-to-azure"></a>Provisionar recomendado SKUs para o Azure

Com apenas alguns cliques, você pode usar as recomendações identificadas para provisionar destino SKUs a no Azure para o qual você pode migrar seus bancos de dados. Você pode usar o arquivo HTML para entrada de assinatura do Azure; Escolher tipo de preço, computação nível e o tamanho máximo de dados para bancos de dados; e gerar um script para provisionar seus bancos de dados. Você pode executar esse script usando o PowerShell.

Você pode executar esse processo em um único computador, ou é possível executá-lo em vários computadores para determinar as recomendações de SKU em grande escala. O DMA atualmente torna uma experiência simples e escalonável, oferecendo suporte a todo o processo por meio da Interface de linha de comando.

Para informações de provisionamento de entrada e fazer alterações para as recomendações, atualize o arquivo HTML da seguinte maneira.

**Para obter recomendações de banco de dados individual**

![Tela de recomendações de SKU do banco de dados SQL do Azure](../dma/media/dma-sku-recommend-single-db-recommendations1.png)

1. Abra o arquivo HTML e insira as seguintes informações:
    - **ID da assinatura** -a ID da assinatura da assinatura do Azure ao qual você deseja provisionar os bancos de dados.
    - **Grupo de recursos** -o grupo de recursos ao qual você deseja implantar os bancos de dados. Insira um grupo de recursos existente.
    - **Região** -a região na qual você deseja provisionar bancos de dados. Certifique-se de que sua assinatura dá suporte a região de select.
    - **Nome do servidor** -servidor o banco de dados do SQL do Azure ao qual você deseja que os bancos de dados implantados. Se você inserir um nome de servidor que não existe, ele será criado.
    - **Admin Username** -o nome de usuário de administrador do servidor.
    - **Senha de administrador** -a senha de administrador do servidor. A senha deve ter pelo menos oito caracteres e não mais de 128 caracteres. Sua senha deve conter caracteres de três das seguintes categorias – inglês letras maiusculas, letras minúsculas, números (0-9) e caracteres não alfanuméricos (!, $, #, %, etc.). A senha não pode conter todos ou parte (3 + letras consecutivas) do nome de usuário.

2. Analise as recomendações para cada banco de dados e modificar o tipo de preço, computação nível e o tamanho máximo de dados conforme necessário. Certifique-se de desmarcar quaisquer bancos de dados que você não deseja atualmente para provisionar.

3. Selecione **Gerar Script de provisionamento**, salve o script e, em seguida, executá-lo no PowerShell.

    Esse processo deve criar todos os bancos de dados que você selecionou na página HTML.

**Para obter recomendações de instância gerenciada**

![Tela de recomendações de SKU de MI de SQL do Azure](../dma/media/dma-sku-recommend-mi-recommendations1.png)

1. Abra o arquivo HTML e insira as seguintes informações:
    - **ID da assinatura** -a ID da assinatura da assinatura do Azure ao qual você deseja provisionar os bancos de dados.
    - **Grupo de recursos** -o grupo de recursos ao qual você deseja implantar os bancos de dados. Insira um grupo de recursos existente.
    - **Região** -a região na qual você deseja provisionar bancos de dados. Certifique-se de que sua assinatura dá suporte a região de select.
    - **Nome da instância** – a instância da instância gerenciada do SQL para o qual você deseja migrar os bancos de dados. O nome da instância pode conter somente letras minúsculas, números e '-', mas ele não pode começar ou terminar com '-' nem ter mais de 63 caracteres.
    - **Instância Admin Username** – o nome de usuário do administrador de instância. Verifique se seu nome de logon atende aos requisitos a seguir, é um identificador de SQL e não um nome de sistema típico (como admin, administrator, sa, raiz, dbmanager, loginmanager, etc.), ou um usuário de banco de dados interno ou função (como dbo, guest, public, etc.). Verifique se o nome não contém espaços em branco, caracteres Unicode ou caracteres não alfabéticos e que ele não começa com números ou símbolos. 
    - **Senha do administrador da instância** -a senha de administrador da instância. Sua senha deve ter pelo menos 16 caracteres e não mais de 128 caracteres. Sua senha deve conter caracteres de três das seguintes categorias – inglês letras maiusculas, letras minúsculas, números (0-9) e caracteres não alfanuméricos (!, $, #, %, etc.). A senha não pode conter todos ou parte (3 + letras consecutivas) do nome de usuário.
    - **Nome da rede virtual** – nome da VNet a sob a qual a instância gerenciada deve ser provisionada. Insira um nome de rede virtual existente.
    - **Nome da sub-rede** – nome da sub-rede a sob a qual a instância gerenciada deve ser provisionada. Insira um nome de sub-rede existente.

2. Analise as recomendações para cada instância e modifique o tipo de preço, computação nível e o tamanho máximo de dados conforme necessário. Embora as recomendações estão limitadas a 8vcore para SKUs 40vcore, ainda há a opção para provisionar os SKUs 64vcore e 80vcore se desejado. Certifique-se de desmarcar todas as instâncias que você não deseja atualmente para provisionar.

    Esse processo deve criar todos os bancos de dados que você selecionou na página HTML.

    > [!NOTE]
    > Criação de instâncias gerenciadas em uma sub-rede (especialmente pela primeira vez) pode levar várias horas para ser concluída. Após executar o script de provisionamento por meio do PowerShell, você pode verificar o status da implantação no Portal do Azure.

## <a name="next-step"></a>Próxima etapa

- Para obter uma lista completa de comandos para executar o DMA da CLI, consulte o artigo [executar Assistente de migração dados da linha de comando](https://docs.microsoft.com/sql/dma/dma-commandline?view=sql-server-2017).
