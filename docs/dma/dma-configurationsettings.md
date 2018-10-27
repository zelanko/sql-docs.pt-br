---
title: Definir as configurações para o Assistente de migração de dados (SQL Server) | Microsoft Docs
description: Saiba como definir as configurações para o Assistente de migração de dados atualizando os valores no arquivo de configuração
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
ms.openlocfilehash: 9801afda1a876f486e7b7042d3dad082c70c99fa
ms.sourcegitcommit: 38f35b2f7a226ded447edc6a36665eaa0376e06e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49643814"
---
# <a name="configure-settings-for-data-migration-assistant"></a>Definir as configurações para o Assistente de migração de dados

Você pode ajustar o comportamento específico do Assistente de migração de dados, definindo valores de configuração no arquivo dma.exe.config. Este artigo descreve os valores de configuração de chave.

Você pode encontrar o arquivo dma.exe.config para aplicativo de desktop do Assistente de migração de dados e o utilitário de linha de comando, nas seguintes pastas em seu computador.

- Aplicativo da área de trabalho

  % ProgramFiles %\\Assistente de migração de dados da Microsoft\\dma.exe.config

- Utilitário de linha de comando

  % ProgramFiles %\\Assistente de migração de dados da Microsoft\\dmacmd.exe.config 

Certifique-se de salvar uma cópia do arquivo de configuração original antes de fazer modificações. Depois de fazer alterações, reinicie o Assistente de migração dados para os novos valores de configuração entrem em vigor.

## <a name="number-of-databases-to-assess-in-parallel"></a>Número de bancos de dados para avaliar em paralelo

Assistente de migração de dados avalia vários bancos de dados em paralelo. Durante a avaliação de Assistente de migração de dados extrai camada de dados dacpac (aplicativo) para compreender o esquema de banco de dados. Essa operação pode atingir o tempo limite se vários bancos de dados no mesmo servidor são avaliados em paralelo. 

Começando com o Assistente de migração de dados v2.0, você pode controlar isso definindo o parallelDatabases valor de configuração. Valor padrão é 8.

```
<advisorGroup>

<workflowSettings>

<assessment parallelDatabases="8" />

</workflowSettings>

</advisorGroup>
```




## <a name="number-of-databases-to-migrate-in-parallel"></a>Número de bancos de dados para migrar em paralelo

Assistente de migração de dados faz a migração de vários bancos de dados em paralelo, antes migrando logons. Durante a migração, Assistente de migração de dados será fazer um backup de banco de dados de origem, como opção, copie o backup e, em seguida, restaurá-lo no servidor de destino. Você pode encontrar falhas de tempo limite quando vários bancos de dados são selecionados para migração. 

Começando com o Assistente de migração de dados v 2.0, se você tiver esse problema, você pode reduzir o valor da configuração parallelDatabases. Você pode aumentar o valor para reduzir o tempo geral de migração.

```
<advisorGroup>

<workflowSettings>

<migration parallelDatabases=”8″ />

</workflowSettings>

</advisorGroup>
```


## <a name="dacfx-settings"></a>Configurações de DacFX

Durante a avaliação, o Assistente de migração de dados extrai camada de dados dacpac (aplicativo) para compreender o esquema de banco de dados. Esta operação poderá falhar com os tempos limite para bancos de dados extremamente grandes, ou se o servidor estiver sob carga. Começando com v 1.0 de migração de dados, você pode modificar os seguintes valores de configuração para evitar erros. 

> [!NOTE]
> Todo o &lt;dacfx&gt; entrada é comentada por padrão. Remova os comentários e, em seguida, modifique o valor conforme necessário.

- commandTimeout

   Esse parâmetro define a propriedade IDbCommand.CommandTimeout na *segundos*. (Padrão = 60)

- databaseLockTimeout

   Esse parâmetro é equivalente a [bloqueio definido\_tempo limite de tempo limite\_período](../t-sql/statements/set-lock-timeout-transact-sql.md) na *milissegundos*. (Padrão = 5000)

- maxDataReaderDegreeOfParallelism

  Esse parâmetro define o número de conexões de pool de conexão SQL para usar. (Padrão = 8)

```
<advisorGroup>

<advisorSettings>

<dacFx  commandTimeout="60" databaseLockTimeout="5000"
maxDataReaderDegreeOfParallelism="8"/>

</advisorSettings>

</advisorGroup>
```

## <a name="stretch-database-recommendation-threshold"></a>Stretch Database: Limite de recomendação

Com o [SQL Server Stretch Database](https://docs.microsoft.com/sql/sql-server/stretch-database/stretch-database), você pode ampliar dinamicamente quentes e frios dados transacionais do Microsoft SQL Server 2016 no Azure. Stretch Database destinos bancos de dados transacionais com grandes quantidades de dados frios. A recomendação do Stretch Database, na recomendação de recurso de armazenamento, primeiro identifica tabelas que ele achar que irão se beneficiar desse recurso e, em seguida, ele identifica as alterações que precisam ser feitas para habilitar a tabela para esse recurso.

Começando com o Assistente de migração de dados v2.0, você pode controlar esse limite para uma tabela para se qualificar para o recurso Stretch Database usando o valor de configuração recommendedNumberOfRows. Valor padrão é 100.000 linhas. Se você quiser analisar os recursos de ampliação para tabelas ainda menores, reduza o valor adequadamente.

```
<advisorGroup>

<advisorSettings>

<stretchDBAdvisor  recommendedNumberOfRows="100000" />

</advisorSettings>

</advisorGroup>
```


## <a name="sql-connection-timeout"></a>Tempo limite de conexão do SQL

Você pode controlar a [tempo limite de conexão SQL](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectiontimeout(v=vs.110).aspx) para instâncias de origem e de destino durante a execução de uma avaliação ou a migração, definindo o valor de tempo limite de conexão para um número especificado de segundos. O valor padrão é 15 segundos.

```
<appSettings>

<add key="ConnectionTimeout" value="15" />

</appSettings>
```


## <a name="see-also"></a>Confira também

[Download de Assistente de migração de dados](https://www.microsoft.com/download/details.aspx?id=53595)
