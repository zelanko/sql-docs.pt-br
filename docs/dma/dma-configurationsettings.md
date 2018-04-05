---
title: As definições de configuração (SQL Server Data Migration Assistant) | Microsoft Docs
ms.custom: ''
ms.date: 08/31/2017
ms.prod: sql-non-specified
ms.prod_service: dma
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-dma
ms.tgt_pltfrm: ''
ms.topic: article
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3dde0c93d09a8c273e74820428a617a24f7ee150
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="configuration-settings-for-data-migration-assistant"></a>Definições de configuração para o Assistente de migração de dados

Você pode ajustar o comportamento específico de dados Assistente de migração usando os valores de configuração no arquivo dma.exe.config. Este artigo descreve os valores de chave de configuração.

Você pode encontrar o arquivo dma.exe.config para o aplicativo de desktop do Assistente de migração de dados e o utilitário de linha de comando, as pastas a seguir em seu computador.

- Aplicativo de área de trabalho

  % ProgramFiles %\\Assistente de migração de dados da Microsoft\\dma.exe.config

- Utilitário de linha de comando

  % ProgramFiles %\\Assistente de migração de dados da Microsoft\\dmacmd.exe.config 

Certifique-se de salvar uma cópia do arquivo de configuração original antes de fazer modificações. Depois de fazer alterações, reinicie dados Assistente de migração para os novos valores de configuração entrem em vigor.

## <a name="number-of-databases-to-assess-in-parallel"></a>Número de bancos de dados para avaliar em paralelo

Assistente de migração de dados avalia vários bancos de dados em paralelo. Durante a avaliação de Assistente de migração de dados extrai o aplicativo de camada de dados (dacpac) para compreender o esquema de banco de dados. Essa operação pode tempo limite se vários bancos de dados no mesmo servidor são avaliados em paralelo. 

Começando com a v 2.0 Assistente de migração de dados, você pode controlar isso definindo o parallelDatabases valor de configuração. Valor padrão é 8.

```
<advisorGroup>

<workflowSettings>

<assessment parallelDatabases="8" />

</workflowSettings>

</advisorGroup>
```




## <a name="number-of-databases-to-migrate-in-parallel"></a>Número de bancos de dados para migrar em paralelo

Assistente de migração de dados faz a migração de vários bancos de dados em paralelo, antes migrando logons. Durante a migração, Assistente de migração de dados será fazer um backup do banco de dados de origem, opcionalmente, copie o backup e, em seguida, restaurá-lo no servidor de destino. Você pode encontrar falhas de tempo limite quando vários bancos de dados são selecionados para migração. 

Começando com o Assistente de migração de dados v 2.0, se você tiver esse problema, você pode reduzir o valor da configuração parallelDatabases. Você pode aumentar o valor para reduzir o tempo geral de migração.

```
<advisorGroup>

<workflowSettings>

<migration parallelDatabases=”8″ />

</workflowSettings>

</advisorGroup>
```


## <a name="dacfx-settings"></a>Configurações de DacFX

Durante a avaliação, o Assistente de migração de dados extrai o aplicativo de camada de dados (dacpac) para compreender o esquema de banco de dados. Essa operação pode falhar com tempos limite para bancos de dados muito grandes, ou se o servidor estiver sob carga. Começando com a v 1.0 de migração de dados, você pode modificar os seguintes valores de configuração para evitar erros. 

> [!NOTE]
> Todo o &lt;dacfx&gt; entrada é marcado como ignorada por padrão. Remova os comentários e, em seguida, modifique o valor conforme necessário.

- CommandTimeout

   Isso define a propriedade IDbCommand.CommandTimeout em *segundos*. (Padrão = 60)

- databaseLockTimeout

   Isso é equivalente a [bloqueio definido\_tempo limite de tempo limite\_período ](../t-sql/statements/set-lock-timeout-transact-sql.md) na *milissegundos*. (Padrão = 5000)

- maxDataReaderDegreeOfParallelism

   Número de conexões do pool de conexão SQL para usar. (Padrão = 8)

```
<advisorGroup>

<advisorSettings>

<dacFx  commandTimeout="60" databaseLockTimeout="5000"
maxDataReaderDegreeOfParallelism="8"/>

</advisorSettings>

</advisorGroup>
```


## <a name="stretch-database-recommendation-threshold"></a>Banco de dados de ampliação: Limite de recomendação

Com [banco de dados do SQL Server Stretch](https://docs.microsoft.com/sql/sql-server/stretch-database/stretch-database), você pode ampliar dinamicamente dados quentes e frios transacionais do Microsoft SQL Server 2016 no Azure. Stretch Database destinos bancos de dados transacionais com grandes quantidades de dados frios. A recomendação de Stretch Database, na recomendação de recurso de armazenamento, primeiro identifica tabelas que ele achar que irá se beneficiar desse recurso, e, em seguida, ele identifica alterações que precisam ser feitas para habilitar a tabela para esse recurso.

Começando com a v 2.0 Assistente de migração de dados, você pode controlar esse limite para uma tabela para se qualificar para o recurso Stretch Database usando o valor de configuração recommendedNumberOfRows. Valor padrão é 100.000 linhas. Se você quiser analisar os recursos de ampliação para tabelas ainda menores, diminua o valor adequadamente.

```
<advisorGroup>

<advisorSettings>

<stretchDBAdvisor  recommendedNumberOfRows="100000" />

</advisorSettings>

</advisorGroup>
```


## <a name="sql-connection-timeout"></a>Tempo limite de conexão do SQL

Você pode controlar o [tempo limite de conexão SQL](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectiontimeout(v=vs.110).aspx) para instâncias de origem e de destino durante a execução de uma avaliação ou a migração, definindo o valor de tempo limite de conexão para um número especificado de segundos. O valor padrão é 15 segundos.

```
<appSettings>

<add key="ConnectionTimeout" value="15" />

</appSettings>
```


## <a name="see-also"></a>Consulte também

[Download de Assistente de migração de dados](https://www.microsoft.com/download/details.aspx?id=53595)
