---
title: Executar o Assistente de migração de dados da linha de comando (SQL Server) | Microsoft Docs
description: Saiba como executar o Assistente de migração de dados da linha de comando para avaliar os bancos de dados do SQL Server para a migração
ms.custom: ''
ms.date: 05/06/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Command Line
ms.assetid: ''
author: HJToland3
ms.author: rajpo
manager: jroth
ms.openlocfilehash: 18ac429a536b657b7f7c0cf91c100eed8a152e52
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66794396"
---
# <a name="run-data-migration-assistant-from-the-command-line"></a>Executar o Assistente de migração de dados da linha de comando

Com a versão 2.1 e posterior, quando você instala o Assistente de migração de dados, ele também instalará dmacmd.exe na *% ProgramFiles %\\Assistente de migração de dados da Microsoft\\* . Use dmacmd.exe para avaliar seus bancos de dados em um modo autônomo e o resultado para o arquivo CSV ou JSON de saída. Esse método é especialmente útil ao avaliar vários bancos de dados ou bancos de dados grandes. 

> [!NOTE]
> Dmacmd.exe dá suporte à execução apenas para avaliações. Não há suporte para migrações no momento.

## <a name="assessments-using-the-command-line-interface-cli"></a>Avaliações usando a Interface de linha de comando (CLI)

```
DmaCmd.exe /AssessmentName="string"
/AssessmentDatabases="connectionString1" \["connectionString2"\]
\[/AssessmentSourcePlatform="SourcePlatform"]
\[/AssessmentTargetPlatform="TargetPlatform"\]
/AssessmentEvaluateRecommendations|/AssessmentEvaluateCompatibilityIssues
\[/AssessmentOverwriteResult\]
/AssessmentResultJson="file"|/AssessmentResultCsv="file"
```

|Argumento  |Descrição  | Obrigatório (S/N)
|---------|---------|---------------|
| `/help or /?`     | Como usar o texto de ajuda de dmacmd.exe        | N
|`/AssessmentName`     |   Nome do projeto de avaliação   | S
|`/AssessmentDatabases`     | Lista delimitada por espaço de cadeias de caracteres de conexão. Nome do banco de dados (catálogo inicial) diferencia maiusculas de minúsculas. | S
|`/AssessmentSourcePlatform`     | Plataforma de origem para a avaliação: <br>Valores com suporte para a avaliação: SqlOnPrem, RdsSqlServer (default) <br>Valores com suporte para a avaliação de prontidão de destino: SqlOnPrem RdsSqlServer (padrão), Cassandra (versão prévia)   | N
|`/AssessmentTargetPlatform`     | Plataforma de destino para a avaliação:  <br> Valores com suporte para a avaliação: AzureSqlDatabase, ManagedSqlServer, SqlServer2012, lt;sqlserver2014, SqlServer2016, SqlServerLinux2017 e SqlServerWindows2017 (padrão)  <br> Valores com suporte para a avaliação de prontidão de destino: ManagedSqlServer (padrão), o cosmos DB (versão prévia)   | N
|`/AssessmentEvaluateFeatureParity`  | Execute as regras de paridade de recurso. Se a plataforma de origem é RdsSqlServer, avaliação de paridade de recurso não tem suporte para a plataforma de destino AzureSqlDatabase  | N
|`/AssessmentEvaluateCompatibilityIssues`     | Executar regras de compatibilidade  | S <br> (AssessmentEvaluateCompatibilityIssues ou AssessmentEvaluateRecommendations é necessário.)
|`/AssessmentEvaluateRecommendations`     | Execute as recomendações de recurso        | S <br> (AssessmentEvaluateCompatibilityIssues ou AssessmentEvaluateRecommendations é necessária)
|`/AssessmentOverwriteResult`     | Substituir o arquivo de resultado    | N
|`/AssessmentResultJson`     | Caminho completo para o arquivo de resultado JSON     | S <br> (AssessmentResultJson ou AssessmentResultCsv é necessária)
|`/AssessmentResultCsv`    | Caminho completo para o arquivo de resultado CSV   | S <br> (AssessmentResultJson ou AssessmentResultCsv é necessária)
|`/Action`    | Use SkuRecommendation para obter recomendações de SKU, use AssessTargetReadiness para realizar a avaliação de prontidão de destino.   | N
|`/SourceConnections`    | Lista delimitada de espaço de cadeias de caracteres de conexão. Nome do banco de dados (catálogo inicial) é opcional. Se nenhum nome de banco de dados for fornecido, todos os bancos de dados na origem são avaliados.   | S <br> (Obrigatório se a ação é 'AssessTargetReadiness')
|`/TargetReadinessConfiguration`    | Caminho completo para o arquivo XML que descreve os valores para o nome, conexões de fonte e o arquivo de resultado.   | S <br> (TargetReadinessConfiguration ou SourceConnections é necessária)
|`/FeatureDiscoveryReportJson`    | Caminho para a descoberta do recurso relatório JSON. Se esse arquivo é gerado, ele pode ser usado para executar a avaliação de prontidão de destino novamente sem se conectar à fonte. | N
|`/ImportFeatureDiscoveryReportJson`    | Caminho para o relatório JSON da descoberta de recursos criado anteriormente. Em vez de conexões de origem, esse arquivo será usado.   | N

## <a name="examples-of-assessments-using-the-cli"></a>Exemplos de avaliações usando a CLI

**Dmacmd.exe**

  `Dmacmd.exe /? or DmaCmd.exe /help`

**Avaliação de banco de dados único usando regras de compatibilidade de autenticação e a execução do Windows**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentEvaluateCompatibilityIssues /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
```

**Avaliação de banco de dados único usando a recomendação de recurso de autenticação e a execução do SQL Server**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;User Id=myUsername;Password=myPassword;"
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```

**Avaliação do banco de dados único para a plataforma de destino SQL Server 2012, salvar resultados em arquivo. JSON e. csv**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentTargetPlatform="SqlServer2012"
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```

**Avaliação de banco de dados de único para a plataforma de destino de banco de dados do SQL Azure, salvar resultados em arquivo. JSON e. csv**

```
DmaCmd.exe /AssessmentName="TestAssessment" 
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentTargetPlatform="AzureSqlDatabaseV12"
/AssessmentEvaluateCompatibilityIssues /AssessmentEvaluateFeatureParity
/AssessmentOverwriteResult 
/AssessmentResultCsv="C:\\temp\\AssessmentReport.csv" 
/AssessmentResultJson="C:\\temp\\AssessmentReport.json"
```

**Avaliação de vários bancos de dados**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName1;Initial
Catalog=DatabaseName1;Integrated Security=true"
"Server=SQLServerInstanceName1;Initial Catalog=DatabaseName2;Integrated
Security=true" "Server=SQLServerInstanceName2;Initial
Catalog=DatabaseName3;Integrated Security=true"
/AssessmentTargetPlatform="SqlServer2016"
/AssessmentEvaluateCompatibilityIssues /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
/AssessmentResultJson="C:\\Results\\test2016.json"
```

**Avaliação de prontidão de destino de banco de dados único usando a autenticação do Windows**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/AssessmentName="TestAssessment" 
/SourceConnections="Server=SQLServerInstanceName;Initial Catalog=DatabaseName;Integrated Security=true" 
/AssessmentOverwriteResult 
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"
```

**Avaliação de prontidão de destino de banco de dados único usando a autenticação do SQL Server**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/AssessmentName="TestAssessment" 
/SourceConnections="Server=SQLServerInstanceName;Initial Catalog=DatabaseName;User Id=myUsername;Password=myPassword;" /AssessmentEvaluateRecommendations 
/AssessmentOverwriteResult 
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json" 

```

**Avaliação de banco de dados de único para a plataforma de destino de banco de dados do SQL Azure, salvar resultados em arquivo. JSON e. csv**

```
DmaCmd.exe /AssessmentName="TestAssessment" 
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentSourcePlatform="SqlOnPrem"
/AssessmentTargetPlatform="AzureSqlDatabase"
/AssessmentEvaluateCompatibilityIssues /AssessmentEvaluateFeatureParity
/AssessmentOverwriteResult 
/AssessmentResultCsv="C:\\temp\\AssessmentReport.csv" 
/AssessmentResultJson="C:\\temp\\AssessmentReport.json"

```

**Avaliação de prontidão de destino de vários bancos de dados**

```
DmaCmd.exe /Action=AssessTargetReadiness
/AssessmentName="TestAssessment"
/AssessmentSourcePlatform=SourcePlatform
/AssessmentTargetPlatform=TargetPlatform
/SourceConnections="Server=SQLServerInstanceName1;Initial Catalog=DatabaseName1;Integrated Security=true" "Server=SQLServerInstanceName1;Initial Catalog=DatabaseName2;Integrated Security=true" "Server=SQLServerInstanceName2;Initial Catalog=DatabaseName3;Integrated Security=true"
/AssessmentOverwriteResult  
/AssessmentResultJson="C:\Results\test2016.json"

(/AssessmentSourcePlatform and /AssessmentTargetPlatform are optional.)
```

**Avaliação de prontidão de destino para todos os bancos de dados em um servidor usando a autenticação do Windows**

```
DmaCmd.exe /Action=AssessTargetReadiness
/AssessmentName="TestAssessment"
/SourceConnections="Server=SQLServerInstanceName;Integrated Security=true"
/AssessmentOverwriteResult
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"

```

**Avaliação de prontidão de destino com a importação de relatório de descoberta do recurso criado anteriormente**

```
DmaCmd.exe /Action=AssessTargetReadiness
/AssessmentName="TestAssessment"
/ImportFeatureDiscoveryReportJson="c:\temp\feature_report.json" 
/AssessmentOverwriteResult
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"

```

**Avaliação de prontidão de destino, fornecendo o arquivo de configuração**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/TargetReadinessConfiguration=.\Config.xml
```

Conexões de fonte de conteúdo do arquivo de configuração ao usar:

```
<?xml version="1.0" encoding="utf-8" ?>
<TargetReadinessConfiguration xmlns="http://microsoft.com/schemas/SqlServer/Advisor/TargetReadinessConfiguration">
  <AssessmentName>name</AssessmentName>
  <SourcePlatform>Source Platform</SourcePlatform> <!-- Optional. The default is SqlOnPrem -->
  <TargetPlatform>TargetPlatform</TargetPlatform> <!-- Optional. The default is ManagedSqlServer -->
  <SourceConnections>
    <SourceConnection>connection string 1</SourceConnection>
    <SourceConnection>connection string 2</SourceConnection>
    <!-- ... -->
    <SourceConnection>connection string n</SourceConnection>
  </SourceConnections>
  <AssessmentResultJson>path\to\file.json</AssessmentResultJson>
  <FeatureDiscoveryReportJson>path\to\featurediscoveryreport.json</FeatureDiscoveryReportJson>
  <OverwriteResult>true</OverwriteResult> <!-- or false -->
</TargetReadinessConfiguration>
```

Conteúdo do arquivo de configuração durante a importação do recurso relatório de descoberta:

```
<TargetReadinessConfiguration xmlns="http://microsoft.com/schemas/SqlServer/Advisor/TargetReadinessConfiguration">
  <AssessmentName>name</AssessmentName>
  <ImportFeatureDiscoveryReportJson>path\to\featurediscoveryfile.json</ImportFeatureDiscoveryReportJson>
  <AssessmentResultJson>path\to\resultfile.json</AssessmentResultJson>
  <OverwriteResult>true</OverwriteResult><!-- or false -->
</TargetReadinessConfiguration>
```

## <a name="azure-sql-databasemanaged-instance-sku-recommendations-using-the-cli"></a>Banco de dados SQL/gerenciado instância SKU recomendações do Azure usando a CLI

Esses comandos recomendações de suporte para o banco de dados individual do banco de dados SQL e opções de implantação de instância gerenciada.

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true 
```

|Argumento  |Descrição  | Obrigatório (S/N)
|---------|---------|---------------|
|`/Action=SkuRecommendation` | Executar avaliação de SKU usando a linha de comando DMA | S
|`/SkuRecommendationInputDataFilePath` | Caminho completo para o arquivo de contador de desempenho coletado do computador que hospeda seus bancos de dados | S
|`/SkuRecommendationTsvOutputResultsFilePath` | Caminho completo para o arquivo de resultado TSV | S <br> (Requer o caminho do arquivo TSV ou JSON ou HTML)
|`/SkuRecommendationJsonOutputResultsFilePath` | Caminho completo para o arquivo de resultado JSON | S <br> (Requer o caminho do arquivo TSV ou JSON ou HTML)
|`/SkuRecommendationHtmlResultsFilePath` | Caminho completo para o arquivo de resultado HTML | S <br> (Requer o caminho do arquivo TSV ou JSON ou HTML)
|`/SkuRecommendationPreventPriceRefresh` | Impede que o preço de atualização ocorra. Use se executando no modo offline (por exemplo, true). | S <br> (Selecione qualquer um desse argumento para preços estáticos ou abaixo de todos os argumentos precisam ser selecionados para obter os preços mais recentes)
|`/SkuRecommendationCurrencyCode` | A moeda na qual exibir os preços (por exemplo "USD") | S <br> (Para os preços mais recentes)
|`/SkuRecommendationOfferName` | A oferta de nome (por exemplo "MS-AZR-0003P"). Para obter mais informações, consulte o [detalhes da oferta do Microsoft Azure](https://azure.microsoft.com/support/legal/offer-details/) página. | S <br> (Para os preços mais recentes)
|`/SkuRecommendationRegionName` | A região (por exemplo, nomeie "WestUS") | S <br> (Para os preços mais recentes)
|`/SkuRecommendationSubscriptionId` | A ID da assinatura. | S <br> (Para os preços mais recentes)
|`/SkuRecommendationDatabasesToRecommend` | Lista separada por espaços dos bancos de dados a ser recomendado (por exemplo "Database1" "Database2" "Database3"). Nomes diferenciam maiusculas de minúsculas e devem ser colocados entre aspas duplas. Se omitido, as recomendações são fornecidas para todos os bancos de dados. | N
|`/AzureAuthenticationTenantId` | O locatário de autenticação. | S <br> (Para os preços mais recentes)
|`/AzureAuthenticationClientId` | A ID do cliente do aplicativo AAD usado para autenticação. | S <br> (Para os preços mais recentes)
|`/AzureAuthenticationInteractiveAuthentication` | Defina como verdadeiro para a janela pop-up. | S <br> (Para os preços mais recentes) <br>(Escolha uma das opções de 3 autenticação - opção 1)
|`/AzureAuthenticationCertificateStoreLocation` | Definido como o repositório de certificados local (por exemplo "CurrentUser"). | S <br>(Para os preços mais recentes) <br> (Escolha uma das opções de 3 autenticação - opção 2)
|`/AzureAuthenticationCertificateThumbprint` | Definido como a impressão digital do certificado. | S <br> (Para os preços mais recentes) <br>(Escolha uma das opções de 3 autenticação - opção 2)
|`/AzureAuthenticationToken` | Defina como o token de certificado. | S <br> (Para os preços mais recentes) <br>(Escolha uma das opções de 3 autenticação - opção 3)

## <a name="examples-of-sku-assessments-using-the-cli"></a>Exemplos de avaliações de SKU usando a CLI

**Dmacmd.exe**

`Dmacmd.exe /? or DmaCmd.exe /help`

**Recomendações de SKU de MI/banco de dados SQL do Azure com a atualização de preço (get preços mais recentes) - autenticação interativa** 

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
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
/AzureAuthenticationInteractiveAuthentication=true 
```

**Recomendações de SKU de MI/banco de dados SQL do Azure com a atualização de preço (get preços mais recentes) - autenticação de certificado**

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
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
/AzureAuthenticationCertificateStoreLocation=<Your Certificate Store Location>
/AzureAuthenticationCertificateThumbprint=<Your Certificate Thumbprint>  
```

**Recomendações de SKU/MI de banco de dados de SQL do Azure com a atualização de preço (get preços mais recentes) - autenticação de Token e especifique os bancos de dados para recomendar**
  
```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationCurrencyCode=USD
/SkuRecommendationOfferName=MS-AZR-0044p
/SkuRecommendationRegionName=UKWest
/SkuRecommendationDatabasesToRecommend=“TPCDS1G,EDW_3G,TPCDS10G”
/SkuRecommendationSubscriptionId=<Your Subscription Id>
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
/AzureAuthenticationToken=<Your Authentication Token> 
```

**Recomendações de SKU de MI/banco de dados SQL do Azure sem a atualização de preço (preços estática de uso)** 
```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true  
```

## <a name="see-also"></a>Confira também
- [Assistente de migração de dados](https://aka.ms/get-dma) baixar.
- O artigo [identificar a SKU certa de banco de dados de SQL do Azure para seu banco de dados local](https://aka.ms/dma-sku-recommend-sqldb).
