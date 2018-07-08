---
title: Executar o Assistente de migração de dados da linha de comando (SQL Server) | Microsoft Docs
description: Saiba como executar o Assistente de migração de dados da linha de comando para avaliar os bancos de dados do SQL Server para a migração
ms.custom: ''
ms.date: 09/01/2017
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Command Line
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: 6b364dc03d48cbc1c0487362712e10f7ab0b782e
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37785457"
---
# <a name="run-data-migration-assistant-from-the-command-line"></a>Executar o Assistente de migração de dados da linha de comando
Com a versão 2.1 e posterior, quando você instala o Assistente de migração de dados, ele também instalará dmacmd.exe na *% ProgramFiles %\\Assistente de migração de dados da Microsoft\\*. Use dmacmd.exe para avaliar seus bancos de dados em um modo autônomo e o resultado para o arquivo CSV ou JSON de saída. Esse método é especialmente útil ao avaliar vários bancos de dados ou bancos de dados grandes. 

> [!NOTE]
> Dmacmd.exe dá suporte à execução apenas para avaliações. Não há suporte para migrações no momento.


## <a name="command-line-arguments"></a>Argumentos de linha de comando

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




## <a name="examples"></a>Exemplos

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



## <a name="see-also"></a>Confira também

[Download de Assistente de migração de dados](https://www.microsoft.com/download/details.aspx?id=53595)
