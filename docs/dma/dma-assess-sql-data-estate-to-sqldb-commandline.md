---
title: 'DMACMD: avaliar SQL Server prontidão para migrar para o SQL do Azure'
titleSuffix: Data Migration Assistant
description: Saiba como usar Assistente de Migração de Dados ferramenta de linha de comando (DMACMD) para avaliar um espaço de dados de SQL Server para migração para o SQL do Azure
ms.date: 10/02/2020
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, on-premises SQL Server
ms.assetid: ''
author: rajeshsetlem
ms.author: rajpo
ms.custom: ''
ms.openlocfilehash: a631ed40344fc8661cef23b9758aa35feb041c45
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91729246"
---
# <a name="dmacmd-assess-readiness-of-a-sql-server-data-estate-migrating-to-azure-sql-database"></a>DMACMD: avaliar a prontidão de um SQL Server banco de dados migrando para o Azure SQL Database 

Com muitas organizações tentando migrar para o Azure, é essencial avaliar as instâncias de SQL Server locais existentes e identificar o destino SQL do Azure correto-banco de dados SQL do Azure, Azure SQL Instância Gerenciada ou SQL Server em VMs do Azure. 

[Assistente de migração de dados (DMA)](dma-overview.md) ajuda a avaliar uma instância de SQL Server para um destino do Azure SQL específico e avalia a prontidão dos bancos de dados SQL Server migrando para o SQL do Azure. Carregue os resultados da avaliação de DMA para o Hub de migrações para Azure para uma exibição de preparação centralizada de todo o espaço de dados. 

Este artigo ensina a executar avaliações em escala e carregar os resultados para o Hub de migrações para Azure usando a interface de linha de comando DMA (DMACMD). Como alternativa, você pode usar a [GUI do DMA](dma-assess-sql-data-estate-to-sqldb.md) para executar a avaliação. 

## <a name="prerequisites"></a>Pré-requisitos 

Para usar o DMACMD para executar uma avaliação e carregar os resultados para o Hub de migrações para Azure, você precisará do seguinte: 

- A [versão mais recente do assistente de migração de dados (DMA)](https://www.microsoft.com/en-us/download/details.aspx?id=53595).
- Um [projeto de migrações para Azure](dma-assess-sql-data-estate-to-sqldb.md#create-a-project-and-add-a-tool). 
- Acesso à função colaborador para o recurso de projeto migrações para Azure.

## <a name="use-dmacmd"></a>Usar DMACMD

Use um arquivo XML como entrada para executar avaliações em escala usando a interface de linha de comando (DMACMD.exe). 

Use o seguinte comando de exemplo para passar um arquivo XML para DMACMD e iniciar a avaliação:

```console
C:\Program Files\Microsoft Data Migration Assistant\DmaCmd.exe /Action=Assess /AssessmentConfiguration= C:\Demo\ScaleAssessment\Assess-for-AzureSQLMI.xml
```

O conteúdo de exemplo `Assess-for-AzureSQLMI.xml` define os elementos para avaliar SQL Server instâncias para um destino do SQL instância gerenciada: 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<AssessmentConfiguration xmlns="http://microsoft.com/schemas/SqlServer/Advisor/AssessmentConfiguration">
   <AssessmentName>Scale-Assessment-for-AzureSQLManagedInstance</AssessmentName>
   <AssessmentSourcePlatform>SqlOnPrem</AssessmentSourcePlatform>
   <AssessmentTargetPlatform>ManagedSqlServer</AssessmentTargetPlatform>
   <AssessmentDatabases>
      <AssessmentDatabase>Server=ServerName\SQL2017;Integrated Security=true</AssessmentDatabase>
      <AssessmentDatabase>Server=ServerName\SQL2016;Integrated Security=true;Initial Catalog=AdventureWorks2016</AssessmentDatabase>
      <AssessmentDatabase>Server=ServerName\SQL2016;Integrated Security=true;Initial Catalog=TestDB</AssessmentDatabase>
   </AssessmentDatabases>
   <AssessmentResultDma>C:\Demo\ScaleAssessment\AssessmentConfiguration\Scale-Assessment-for-AzureSQLManagedInstance.dma</AssessmentResultDma>
   <AssessmentResultJson>C:\Demo\ScaleAssessment\AssessmentConfiguration\Scale-Assessment-for-AzureSQLManagedInstance.json</AssessmentResultJson>
   <AssessmentResultCsv>C:\Demo\ScaleAssessment\AssessmentConfiguration\Scale-Assessment-for-AzureSQLManagedInstance.csv</AssessmentResultCsv>
   <AssessmentOverwriteResult>true</AssessmentOverwriteResult>
   <AssessmentEvaluateCompatibilityIssues>true</AssessmentEvaluateCompatibilityIssues>
   <AssessmentEvaluateFeatureParity>true</AssessmentEvaluateFeatureParity>
   <AzureCloudEnvironment>Azure</AzureCloudEnvironment>
   <SubscriptionId>xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxx</SubscriptionId>
   <AzureMigrateProjectName>Scale-Assessment-for-AzureSQLMI</AzureMigrateProjectName>
   <ResourceGroupName>Resource-Group-Name</ResourceGroupName>
   <AzureAuthenticationInteractiveAuthentication>true</AzureAuthenticationInteractiveAuthentication>
   <AzureAuthenticationTenantId>xxxxxxxx-xxxx-xxxxxxxx</AzureAuthenticationTenantId>
   <EnableAssessmentUploadToAzureMigrate>true</EnableAssessmentUploadToAzureMigrate>
</AssessmentConfiguration>
```



## <a name="xml-elements"></a>Elementos XML 

Os elementos XML que são passados para DMACMD são definidos na tabela a seguir: 


|**Elemento XML** |**Definição**  |
|---------|---------|
|`AssessmentName`|O nome da avaliação|
|`AssessmentSourcePlatform`|Plataforma de SQL Server de origem. O valor padrão é `SqlOnPrem`.|
|`AssessmentTargetPlatform`|Plataforma de SQL Server de destino.  </br> `AzureSqlDatabase` é para um destino de banco de dados SQL do Azure. </br> `ManagedSqlServer` é para um destino do Azure SQL Instância Gerenciada. </br></br>O exemplo de **avaliação-para-AzureSQLMI** avalia um destino do SQL instância gerenciada.|
|`AssessmentDatabases`|Se você precisar avaliar todos os bancos de dados em uma instância, especifique apenas o nome da instância, senão, os bancos de dados específicos em cada linha. </br></br>O exemplo de **avaliação-para-AzureSQLMI** avalia todos os bancos de dados em instância `Servername\SQL2017` e dois bancos de dados específicos na instância `Servername\SQL2016` .  |
|`AssessmentResultDma` </br> `AssessmentResultJson` </br> `AssessmentResultCsv` | Especifica o formato do arquivo de resultado. `.DMA`, `.JSON` e `.CSV` respectivamente. Clique duas vezes `.DMA` para abrir na interface do usuário do DMA. <br> `AssessmentResultDma` é necessário para carregar os resultados da avaliação para o Hub de migrações para Azure.  |
|`AssessmentOverwriteResult`| Indica se um arquivo de resultado de avaliação existente deve ser substituído pelo mesmo caminho que `AssessmentResultJson` `AssessmentResultDma` ou `AssessmentResultCsv` .|
|`AssessmentEvaluateCompatibilityIssues` </br> `AssessmentEvaluateFeatureParity` |Execute a avaliação para avaliar problemas de compatibilidade e problemas de paridade de recursos, respectivamente.|
|`AzureCloudEnvironment`|Ambiente de nuvem do Azure ao qual se conectar, o padrão é a nuvem pública do Azure. </br></br> Valores com suporte: </br>`Azure (default)`, `AzureChina`, `AzureGermany`, `AzureUSGovernment`.|
|`SubscriptionId`|Id de assinatura do Azure.|
|`AzureMigrateProjectName`|O Azure migra o nome do projeto para carregar os resultados da avaliação.|
|`ResourceGroupName`|Nome do grupo de recursos de migrações para Azure.|
|`AzureAuthenticationInteractiveAuthentication`|Defina como `true` para exibir a janela de autenticação.|
|`AzureAuthenticationTenantId`|ID do locatário do Microsoft Azure Active Directory. </br></br>Obtenha isso na folha **visão geral** de Azure Active Directory no [portal do Azure](https://portal.azure.com). |
|`EnableAssessmentUploadToAzureMigrate`| Defina como `true` para carregar e publicar os resultados da avaliação no Hub de migrações para Azure.|
|   |   |


## <a name="results"></a>Resultados 

DMACMD gera um status quando ele é concluído com êxito. 


Veja a seguir uma saída de resultado de exemplo: 

```console
Assessment finished for project: Scale-Assessment-for-AzureSQLManagedInstance
DATABASES:
Succeeded             : 4
Failed                : 0
SERVER INSTANCES:
Succeeded             : 2
Failed                : 0
CSV result file       : C:\Demo\ScaleAssessment\Scale-Assessment-for-AzureSQLManagedInstance.csv
JSON result file      : C:\Demo\ScaleAssessment\Scale-Assessment-for-AzureSQLManagedInstance.json
--------------------------------------------------------------------------------
```

Exibir resultados carregados no [Azure migra](dma-assess-sql-data-estate-to-sqldb.md#view-target-readiness-assessment-results) para uma exibição centralizada de todo o espaço de dados. . 

## <a name="best-practices"></a>Práticas recomendadas 

Considere as seguintes práticas recomendadas ao usar o DMACMD: 

- Agrupe logicamente as instâncias de SQL Server de destino e bancos de dados com base no aplicativo, em vez de avaliar todas as instâncias de SQL Server em todo o espaço de dados. 
- Crie um projeto de migrações do Azure separado para cada destino SQL do Azure para evitar a substituição de resultados. 
- O tempo para executar uma avaliação depende do número de objetos de banco de dados. Se possível, evite executar avaliações no sistema de produção e descarregar em uma máquina virtual ou em um servidor de preparo, especialmente para bancos de dados com um grande número de objetos. 


## <a name="see-also"></a>Confira também

* [AMD (Assistente de Migração de Dados)](../dma/dma-overview.md)
* [Assistente de Migração de Dados: definições de configuração](../dma/dma-configurationsettings.md)
* [Assistente de Migração de Dados: práticas recomendadas](../dma/dma-bestpractices.md)
