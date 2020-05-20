---
title: Definir configurações para Assistente de Migração de Dados
description: Saiba como definir as configurações para o Assistente de Migração de Dados atualizando valores no arquivo de configuração
ms.custom: seo-lt-2019
ms.date: 03/12/2019
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
ms.openlocfilehash: bc6805426251e87a8db3dcf4ad9da6343ac0ea12
ms.sourcegitcommit: fb1430aedbb91b55b92f07934e9b9bdfbbd2b0c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82885993"
---
# <a name="configure-settings-for-data-migration-assistant"></a>Definir configurações para Assistente de Migração de Dados

Você pode ajustar determinado comportamento de Assistente de Migração de Dados definindo valores de configuração no arquivo DMA. exe. config. Este artigo descreve os principais valores de configuração.

Você pode encontrar o arquivo DMA. exe. config para o aplicativo de área de trabalho Assistente de Migração de Dados e o utilitário de linha de comando, nas seguintes pastas em seu computador.

- Aplicativo de desktop

  % ProgramFiles% \\ Assistente de migração de dados da Microsoft \\ DMA. exe. config

- Utilitário de linha de comando

  % ProgramFiles% \\ Assistente de migração de dados da Microsoft \\ dmacmd. exe. config 

Lembre-se de salvar uma cópia do arquivo de configuração original antes de fazer qualquer modificação. Depois de fazer alterações, reinicie Assistente de Migração de Dados para que os novos valores de configuração entrem em vigor.

## <a name="number-of-databases-to-assess-in-parallel"></a>Número de bancos de dados a serem avaliados em paralelo

Assistente de Migração de Dados avalia vários bancos de dados em paralelo. Durante a avaliação Assistente de Migração de Dados extrai o dacpac (aplicativo da camada de dados) para entender o esquema de banco de dado.Essa operação poderá atingir o tempo limite se vários bancos de dados no mesmo servidor forem avaliados em paralelo. 

A partir do Assistente de Migração de Dados v 2.0, você pode controlar isso definindo o valor de configuração parallelDatabases. O valor padrão é 8.

```
<advisorGroup>

<workflowSettings>

<assessment parallelDatabases="8" />

</workflowSettings>

</advisorGroup>
```




## <a name="number-of-databases-to-migrate-in-parallel"></a>Número de bancos de dados a serem migrados em paralelo

Assistente de Migração de Dados migra vários bancos de dados em paralelo, antes de migrar logons. Durante a migração, Assistente de Migração de Dados obterá um backup do banco de dados de origem, copiará opcionalmente o backup e, em seguida, restaurá-lo no servidor de destino. Você poderá encontrar falhas de tempo limite quando vários bancos de dados forem selecionados para migração. 

A partir do Assistente de Migração de Dados v 2.0, se você tiver esse problema, poderá reduzir o valor de configuração do parallelDatabases. Você pode aumentar o valor para reduzir o tempo de migração geral.

```
<advisorGroup>

<workflowSettings>

<migration parallelDatabases="8″ />

</workflowSettings>

</advisorGroup>
```


## <a name="dacfx-settings"></a>Configurações de DacFX

Durante a avaliação, Assistente de Migração de Dados extrai o dacpac (aplicativo da camada de dados) para entender o esquema de banco de dado. Essa operação pode falhar com tempos limite para bancos de dados muito grandes ou se o servidor estiver sob carga. A partir da migração de dados v 1.0, você pode modificar os seguintes valores de configuração para evitar erros. 

> [!NOTE]
> A &lt; entrada dacfx inteira &gt; é comentada por padrão. Remova os comentários e, em seguida, modifique o valor conforme necessário.

- commandTimeout

   Esse parâmetro define a Propriedade IDbCommand. CommandTimeout em *segundos*.(Padrão = 60)

- databaseLockTimeout

   Esse parâmetro é equivalente a [definir o \_ tempo limite \_ de tempo](../t-sql/statements/set-lock-timeout-transact-sql.md) limite de bloqueio em *milissegundos*.(Padrão = 5000)

- maxDataReaderDegreeOfParallelism

  Esse parâmetro define o número de conexões do pool de conexão do SQL a ser usado.(Padrão = 8)

```
<advisorGroup>

<advisorSettings>

<dacFx  commandTimeout="60" databaseLockTimeout="5000"
maxDataReaderDegreeOfParallelism="8"/>

</advisorSettings>

</advisorGroup>
```

## <a name="stretch-database-recommendation-threshold"></a>Stretch Database: limite de recomendação

Com o [SQL Server Stretch Database](https://docs.microsoft.com/sql/sql-server/stretch-database/stretch-database), você pode ampliar dinamicamente dados transacionais quentes e frios do Microsoft SQL Server 2016 para o Azure. Stretch Database se destina a bancos de dados transacionais com grandes quantidades de Cold Data. A recomendação de Stretch Database, sob recomendação de recurso de armazenamento, identifica primeiro as tabelas que ele acha que se beneficiarão desse recurso e identifica as alterações que precisam ser feitas para habilitar a tabela para esse recurso.

A partir do Assistente de Migração de Dados v 2.0, você pode controlar esse limite para que uma tabela se qualifique para o recurso de Stretch Database usando o valor de configuração recommendedNumberOfRows. O valor padrão é 100.000 linhas. Se você quiser analisar os recursos de ampliação para tabelas ainda menores, diminua o valor de acordo.

```
<advisorGroup>

<advisorSettings>

<stretchDBAdvisor  recommendedNumberOfRows="100000" />

</advisorSettings>

</advisorGroup>
```


## <a name="sql-connection-timeout"></a>Tempo limite de conexão SQL

Você pode controlar o [tempo limite da conexão SQL](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectiontimeout(v=vs.110).aspx) para instâncias de origem e de destino durante a execução de uma avaliação ou migração, definindo o valor de tempo limite da conexão como um número especificado de segundos. O valor padrão é 15 segundos.

```
<appSettings>

<add key="ConnectionTimeout" value="15" />

</appSettings>
```

## <a name="ignore-error-codes"></a>Ignorar códigos de erro

Cada regra tem um código de erro em seu título. Se você não precisar de regras e quiser ignorá-las, use a propriedade ignoreErrorCodes. Você pode especificar para ignorar um único erro ou vários erros. Para ignorar vários erros, use um ponto-e-vírgula, por exemplo, ignoreErrorCodes = "46010; 71501". O valor padrão é 71501, que está associado a referências não resolvidas identificadas quando um objeto faz referência a objetos do sistema, como procedimentos, exibições, etc.

```
<workflowSettings>

<assessment parallelDatabases="8" ignoreErrorCodes="71501" />

</workflowSettings>
```

## <a name="see-also"></a>Confira também

[Download de Assistente de Migração de Dados](https://www.microsoft.com/download/details.aspx?id=53595)
