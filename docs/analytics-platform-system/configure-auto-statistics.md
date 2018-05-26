---
title: Automática de estatísticas (Analytics Platform System)
description: Descreve o recurso de estatísticas de auto introduzido no AU7 de sistema de plataforma de análise.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/24/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 1c0f4623adad35ab874330b42aa54f6e1b91d961
ms.sourcegitcommit: fc3cd23685c6b9b6972d6a7bab2cc2fc5ebab5f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/25/2018
---
# <a name="configure-auto-statistics"></a>Configurar estatísticas automaticamente

Saiba como configurar o Parallel Data Warehouse para usar automática de estatísticas para criar e atualizar estatísticas automaticamente.  Use esse recurso para melhorar planos de consulta e, portanto, melhorar o desempenho da consulta.

**Aplica-se a:** APS (começando com AU7)

## <a name="what-are-statistics"></a>Quais são as estatísticas?
As estatísticas de otimização da consulta são objetos que contêm informações estatísticas sobre a distribuição de valores em uma ou mais colunas de uma tabela. O otimizador de consulta usa essas estatísticas para estimar a cardinalidade ou resulta de número de linhas na consulta. Essas estimativas de cardinalidade permitem que o otimizador de consulta criar um plano de consulta de alta qualidade. Por exemplo, pontos de acesso, os usos de Otimizador de consulta MPP estimativas de cardinalidade para escolher a ordem aleatória ou replicar a menor das duas tabelas usadas em uma cláusula join e assim melhorar o desempenho de consulta.  Para obter mais informações, consulte [estatísticas](../relational-databases/statistics/statistics.md) e [DBCC SHOW_STATISTICS](../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)

## <a name="what-are-auto-statistics"></a>Quais são as estatísticas automaticamente?
Estatísticas automaticamente são as estatísticas que o otimizador de consulta cria e atualiza automaticamente para melhorar o plano de consulta. Estatísticas podem ficar desatualizadas depois cargas, inserirem, atualizações e exclusões operações. Sem automática de estatísticas, você precisa fazer sua própria análise para entender as colunas que precisam de estatísticas e quando as estatísticas precisam ser atualizados.

Estatísticas automaticamente incluem as três configurações a seguir: 

### <a name="autocreatestatistics"></a>AUTO_CREATE_STATISTICS
Quando a criação automática de opção de estatísticas, AUTO_CREATE_STATISTICS, está ON, o otimizador de consulta cria estatísticas em colunas individuais no predicado da consulta, conforme necessário, para aprimorar as estimativas de cardinalidade do plano de consulta. Essas estatísticas de coluna única são criadas em colunas que ainda não têm um histograma em um objeto de estatísticas existente.

### <a name="autoupdatestatistics"></a>AUTO_UPDATE_STATISTICS 
Quando a opção de atualização automática de estatísticas, AUTO_UPDATE_STATISTICS, está ativada, o otimizador de consulta determina quando as estatísticas podem estar desatualizadas e as atualiza quando são usadas por uma consulta. As estatísticas ficam desatualizadas depois que operações insert, update, delete ou mesclagem alteram a distribuição de dados na tabela ou exibição indexada. O otimizador de consulta determina quando estatísticas podem estar desatualizadas contando o número de modificações de dados desde a última atualização das estatísticas e comparando o número de modificações a um limite. O limite se baseia no número de linhas na tabela ou na exibição indexada.

### <a name="autoupdatestatisticsasync"></a>AUTO_UPDATE_STATISTICS_ASYNC
A opção de atualização de estatísticas assíncrona, AUTO_UPDATE_STATISTICS_ASYNC, determina se o otimizador de consulta usa atualizações de estatísticas síncronas ou assíncronas. Para pontos de acesso, a opção de atualização de estatísticas assíncrona está ativado por padrão e o otimizador de consulta atualiza estatísticas de forma assíncrona. A opção AUTO_UPDATE_STATISTICS_ASYNC se aplica a objetos de estatísticas criados para índices, colunas únicas em predicados de consulta e estatísticas criadas com a instrução CREATE STATISTICS.

## <a name="configuration-settings-for-system-administrators"></a>Definições de configuração para os administradores do sistema
Após a atualização para AU7 APS, automática de estatísticas é habilitada por padrão. O administrador do sistema pode habilitar ou desabilitar estatísticas automaticamente com o [opção](appliance-feature-switch.md) opção no Gerenciador de configuração do dispositivo.  Uma vez habilitada, os usuários podem alterar as configurações de estatísticas por banco de dados.
Alterar quaisquer valores de chave de recurso requer uma reinicialização do serviço em pontos de acesso.

## <a name="change-auto-statistics-settings-on-a-database"></a>Alterar as configurações de estatísticas automática em um banco de dados
Quando automática de estatísticas é habilitada pelo administrador do sistema, você pode usar [ALTER DATABASE (Parallel Data Warehouse)](/sql/t-sql/statements/alter-database-parallel-data-warehouse) para alterar as configurações de estatísticas em um banco de dados. Se a opção de recurso de estatísticas automática estiver habilitada pelo administrador do sistema, quaisquer novos bancos de dados criados após a atualização para AU7 terá estatísticas automaticamente habilitadas. Todos os bancos de dados que existiam antes da atualização para AU7 têm estatísticas automaticamente desabilitadas. O exemplo a seguir habilita automática de estatísticas de myPDW de banco de dados existente.

```sql
ALTER DATABASE myPDW SET AUTO_CREATE_STATISTICS ON
ALTER DATABASE myPDW SET AUTO_UPDATE_STATISTICS ON 
ALTER DATABASE myPDW SET AUTO_UPDATE_STATISTICS_ASYNC ON
```
 
Opção AUTO_UPDATE STATISTICS_ASYNC só funcionará se AUTO_UPDATE_STATISTICS está ON.  Portanto, as estatísticas não são atualizadas quando AUTO_UPDATE_STATISTICS está OFF e AUTO_UPDATE_STATISTICS_ASYNC está ON. 

### <a name="error-messages"></a>Mensagens de erro
Você pode receber a mensagem de erro "essa opção não é suportada no PDW".  Esse erro ocorre quando o administrador do sistema não habilitou automática de estatísticas, e você tentar definir qualquer automático de opções de estatísticas no banco de dados ALTER. 

### <a name="limitations-and-restrictions"></a>Limitações e restrições
Automática de estatísticas não funciona em tabelas externas. 

### <a name="check-the-current-values"></a>Verifique os valores atuais
A consulta a seguir retorna os valores atuais das configurações de estatísticas automática para todos os bancos de dados.

```sql
SELECT NAME
    , IS_AUTO_CREATE_STATS_ON 
    , IS_AUTO_UPDATE_STATS_ON
    , IS_AUTO_UPDATE_STATS_ASYNC_ON
FROM
    sys.databases;
```

Um valor de retorno 1 indica a configuração está em e 0 significa que a configuração está desativada. 

## <a name="next-steps"></a>Próximas etapas
Para ver o desempenho de suas consultas, consulte [monitoramento consultas ativas](monitoring-active-queries.md)
