---
title: Executar linha de comando (SQL Server Data Migration Assistant) | Microsoft Docs
ms.custom: 
ms.date: 09/01/2017
ms.prod: sql-non-specified
ms.prod_service: dma
ms.service: 
ms.component: dma
ms.reviewer: 
ms.suite: sql
ms.technology: sql-dma
ms.tgt_pltfrm: 
ms.topic: article
keywords: 
helpviewer_keywords: Data Migration Assistant, Command Line
ms.assetid: 
caps.latest.revision: 
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eba6ced7109283f7f083058e64b7a9166401c2b4
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="run-data-migration-assistant-from-the-command-line"></a>Executar o Assistente de migração de dados da linha de comando
Com a versão 2.1 e posterior, quando você instala o Assistente de migração de dados, ele também instalará dmacmd.exe em *% ProgramFiles %\\Assistente de migração de dados da Microsoft\\*. Use dmacmd.exe para avaliar seus bancos de dados em um modo autônomo e gerar o resultado em um arquivo CSV ou JSON. Isso é especialmente útil quando a avaliação de vários bancos de dados ou bancos de dados grandes. 

> [!NOTE]
> Dmacmd.exe oferece suporte apenas a avaliações em execução. Não há suporte para migrações neste momento.


## <a name="command-line-arguments"></a>Argumentos de linha de comando

```
DmaCmd.exe /AssessmentName="string"
/AssessmentDatabases="connectionString1" \["connectionString2"\]
\[/AssessmentTargetPlatform="TargetPlatform"\]
/AssessmentEvaluateRecommendations|/AssessmentEvaluateCompatibilityIssues
\[/AssessmentOverwriteResult\]
/AssessmentResultJson="file"|/AssessmentResultCsv="file"
```


|Argumento  |Description  | Necessário (Y/N)
|---------|---------|---------------|
| `/help or /?`     | Como usar o texto de ajuda de dmacmd.exe        | N
|`/AssessmentName`     |   Nome do projeto de avaliação   | S
|`/AssessmentDatabases`     | Lista de cadeias de caracteres de conexão delimitada por espaço. Nome do banco de dados (catálogo inicial) diferencia maiusculas de minúsculas. | S
|`/AssessmentTargetPlatform`     | Plataforma de destino para a avaliação de valores com suporte: SqlServer2012, SqlServer2014, SqlServer2016 e AzureSqlDatabaseV12. O padrão é SqlServer2016   | N
|`/AssessmentEvaluateFeatureParity`  | Executar as regras de paridade de recursos  | N
|`/AssessmentEvaluateCompatibilityIssues`     | Execute as regras de compatibilidade  | S <br> (AssessmentEvaluateCompatibilityIssues ou AssessmentEvaluateRecommendations é necessário.)
|`/AssessmentEvaluateRecommendations`     | Execute as recomendações do recurso        | S <br> (AssessmentEvaluateCompatibilityIssues ou AssessmentEvaluateRecommendationsis necessário)
|`/AssessmentOverwriteResult`     | Substituir o arquivo de resultado    | N
|`/AssessmentResultJson`     | Caminho completo para o arquivo de resultado JSON     | S <br> (AssessmentResultJson ou AssessmentResultCsv é necessário)
|`/AssessmentResultCsv`    | Caminho completo para o arquivo de resultado CSV   | S <br>(AssessmentResultJson ou AssessmentResultCsv é necessário)




## <a name="examples"></a>Exemplos

**Dmacmd.exe**

  `Dmacmd.exe /? or DmaCmd.exe /help`

**Avaliação de banco de dados único com o uso de regras de compatibilidade de autenticação e a execução do Windows**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;***Integrated Security=true*"**
***/AssessmentEvaluateCompatibilityIssues*** /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
```



**Avaliação de banco de dados único com o uso de recomendação de recurso de autenticação e a execução do SQL Server**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;***User Id=myUsername;Password=myPassword;***"
***/AssessmentEvaluateRecommendations*** /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```


**Avaliação de banco de dados único para a plataforma de destino do SQL Server 2012 e salvar resultados em arquivo. JSON e. csv**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
***/AssessmentTargetPlatform="SqlServer2012"***
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
***/AssessmentResultJson***="C:\\temp\\Results\\AssessmentReport.json"
***/AssessmentResultCsv***="C:\\temp\\Results\\AssessmentReport.csv"
```


**Avaliação de banco de dados único para a plataforma de destino do banco de dados do SQL Azure salvar resultados em arquivo. JSON e. csv**

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



## <a name="see-also"></a>Consulte também

[Download de Assistente de migração de dados](https://www.microsoft.com/download/details.aspx?id=53595)
