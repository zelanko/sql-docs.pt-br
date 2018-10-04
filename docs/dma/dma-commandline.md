---
title: Executar o Assistente de migração de dados da linha de comando (SQL Server) | Microsoft Docs
description: Saiba como executar o Assistente de migração de dados da linha de comando para avaliar os bancos de dados do SQL Server para a migração
ms.custom: ''
ms.date: 08/29/2018
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
manager: craigg
ms.openlocfilehash: 2fa770fad98918ab9e15231822b499787790a900
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47745274"
---
# <a name="run-data-migration-assistant-from-the-command-line"></a>Executar o Assistente de migração de dados da linha de comando
Com a versão 2.1 e posterior, quando você instala o Assistente de migração de dados, ele também instalará dmacmd.exe na *% ProgramFiles %\\Assistente de migração de dados da Microsoft\\*. Use dmacmd.exe para avaliar seus bancos de dados em um modo autônomo e o resultado para o arquivo CSV ou JSON de saída. Esse método é especialmente útil ao avaliar vários bancos de dados ou bancos de dados grandes. 

> [!NOTE]
> Dmacmd.exe dá suporte à execução apenas para avaliações. Não há suporte para migrações no momento.


## <a name="assessments-using-the-command-line-interface-cli"></a>Avaliações usando a Interface de linha de comando (CLI)

```
DmaCmd.exe /AssessmentName="string"
/AssessmentDatabases="connectionString1" \["connectionString2"\]
\[/AssessmentTargetPlatform="TargetPlatform"\]
/AssessmentEvaluateRecommendations|/AssessmentEvaluateCompatibilityIssues
\[/AssessmentOverwriteResult\]
/AssessmentResultJson="file"|/AssessmentResultCsv="file"
```

|Argumento  |Description  | Obrigatório (S/N)
|---------|---------|---------------|
| `/help or /?`     | Como usar o texto de ajuda de dmacmd.exe        | N
|`/AssessmentName`     |   Nome do projeto de avaliação   | S
|`/AssessmentDatabases`     | Lista delimitada por espaço de cadeias de caracteres de conexão. Nome do banco de dados (catálogo inicial) diferencia maiusculas de minúsculas. | S
|`/AssessmentTargetPlatform`     | Plataforma de destino para a avaliação, os valores com suporte: SqlServer2012, lt;sqlserver2014, SqlServer2016 e AzureSqlDatabaseV12. O padrão é SqlServer2016   | N
|`/AssessmentEvaluateFeatureParity`  | Executar regras de paridade de recurso  | N
|`/AssessmentEvaluateCompatibilityIssues`     | Executar regras de compatibilidade  | S <br> (AssessmentEvaluateCompatibilityIssues ou AssessmentEvaluateRecommendations é necessário.)
|`/AssessmentEvaluateRecommendations`     | Execute as recomendações de recurso        | S <br> (AssessmentEvaluateCompatibilityIssues ou AssessmentEvaluateRecommendationsis necessária)
|`/AssessmentOverwriteResult`     | Substituir o arquivo de resultado    | N
|`/AssessmentResultJson`     | Caminho completo para o arquivo de resultado JSON     | S <br> (AssessmentResultJson ou AssessmentResultCsv é necessária)
|`/AssessmentResultCsv`    | Caminho completo para o arquivo de resultado CSV   | S <br>(AssessmentResultJson ou AssessmentResultCsv é necessária)


## <a name="examples-of-assessments-using-the-cli"></a>Exemplos de avaliações usando a CLI

**Dmacmd.exe**

  `Dmacmd.exe /? or DmaCmd.exe /help`

**Avaliação de banco de dados único usando regras de compatibilidade de autenticação e a execução do Windows**


```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;***Integrated Security=true*"**
***/AssessmentEvaluateCompatibilityIssues*** /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
```

**Avaliação de banco de dados único usando a recomendação de recurso de autenticação e a execução do SQL Server**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;***User Id=myUsername;Password=myPassword;***"
***/AssessmentEvaluateRecommendations*** /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```

**Avaliação do banco de dados único para a plataforma de destino SQL Server 2012, salvar resultados em arquivo. JSON e. csv**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
***/AssessmentTargetPlatform="SqlServer2012"***
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
***/AssessmentResultJson***="C:\\temp\\Results\\AssessmentReport.json"
***/AssessmentResultCsv***="C:\\temp\\Results\\AssessmentReport.csv"
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
***/AssessmentDatabases="Server=SQLServerInstanceName1;Initial
Catalog=DatabaseName1;Integrated Security=true"
"Server=SQLServerInstanceName1;Initial Catalog=DatabaseName2;Integrated
Security=true" "Server=SQLServerInstanceName2;Initial
Catalog=DatabaseName3;Integrated Security=true"***
/AssessmentTargetPlatform="SqlServer2016"
/AssessmentEvaluateCompatibilityIssues /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
/AssessmentResultJson="C:\\Results\\test2016.json"
```

## <a name="azure-sql-database-sku-recommendations-using-the-cli"></a>Recomendações de SKU do banco de dados SQL do Azure usando a CLI

> [!IMPORTANT]
> Recomendações de SKU para o banco de dados SQL estão disponíveis atualmente para migrações do SQL Server 2016 ou posterior.

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

|Argumento  |Description  | Obrigatório (S/N)
|---------|---------|---------------|
|`/Action=SkuRecommendation` | Executar avaliação de SKU usando a linha de comando DMA | S
|`/SkuRecommendationInputDataFilePath`  | Caminho completo para o arquivo de contador de desempenho coletado do computador que hospeda seus bancos de dados |    S
|`/SkuRecommendationTsvOutputResultsFilePath`   | Caminho completo para o arquivo de resultado TSV |    S <br>(O caminho do arquivo TSV ou JSON ou HTML é necessário)
|`/SkuRecommendationJsonOutputResultsFilePath`  | Caminho completo para o arquivo de resultado JSON |   S <br>(O caminho do arquivo TSV ou JSON ou HTML é necessário)
|`/SkuRecommendationHtmlResultsFilePath` |  Caminho completo para o arquivo de resultado HTML | S <br>(O caminho do arquivo TSV ou JSON ou HTML é necessário)
|`/SkuRecommendationPreventPriceRefresh` |  Impede que o preço de atualização ocorra. Use se executando no modo offline. |    S <br>(Esse argumento é selecionado para preços estáticos ou todos os argumentos abaixo precisam ser selecionado para obter os preços mais recentes)
|`/SkuRecommendationCurrencyCode` | A moeda na qual exibir os preços (por exemplo "US") | S <br>(Se você deseja obter os preços mais recentes)
|`/SkuRecommendationOfferName` |    A oferta de nome (por exemplo "MS-AZR - 0003P"). Para obter mais informações, consulte o [detalhes da oferta do Microsoft Azure](https://azure.microsoft.com/support/legal/offer-details/) página. |   S <br>(Se você deseja obter os preços mais recentes)
|`/SkuRecommendationRegionName` |   A região (por exemplo, nomeie "Oeste dos EUA") |   S <br>(Se você deseja obter os preços mais recentes)
|`/SkuRecommendationSubscriptionId` | A ID da assinatura. |    S <br>(Se você deseja obter os preços mais recentes)
|`/AzureAuthenticationTenantId` | O locatário de autenticação. |  S <br>(Se você deseja obter os preços mais recentes)
|`/AzureAuthenticationClientId` | A ID do cliente do aplicativo AAD usado para autenticação. | S <br>(Se você deseja obter os preços mais recentes)
|`/AzureAuthenticationInteractiveAuthentication`    | Defina como verdadeiro para a janela pop-up. |   S <br>(Se você deseja obter os preços mais recentes) <br>(Escolha uma das opções de 3 autenticação - opção 1)
|`/AzureAuthenticationCertificateStoreLocation` | Definido como o repositório de certificados local (por exemplo "CurrentUser"). | S <br>(Se você deseja obter os preços mais recentes) <br>(Escolha uma das opções de 3 autenticação - opção 2)
|`/AzureAuthenticationCertificateThumbprint`    | Definido como a impressão digital do certificado. | S <br>(Se você deseja obter os preços mais recentes) <br>(Escolha uma das opções de 3 autenticação - opção 2)
|`/AzureAuthenticationToken` |  Defina como o token de certificado. | S <br>(Se você deseja obter os preços mais recentes) <br>(Escolha uma das opções de 3 autenticação - opção 3)

## <a name="examples-of-sku-assessments-using-the-cli"></a>Exemplos de avaliações de SKU usando a CLI

**Dmacmd.exe**

  `Dmacmd.exe /? or DmaCmd.exe /help`

**Recomendações de SKU do banco de dados SQL do Azure com a atualização de preço (get preços mais recentes) - autenticação interativa** 
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

**Recomendações de SKU do banco de dados SQL do Azure com a atualização de preço (get preços mais recentes) - autenticação de certificado**
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

**O Token de recomendações de SKU do banco de dados SQL do Azure com a atualização de preço (get preços mais recentes) - autenticação**  
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
/AzureAuthenticationToken=<Your Authentication Token> 
```

**Recomendações de SKU do banco de dados SQL do Azure sem a atualização de preço (preços estática de uso)** 
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
