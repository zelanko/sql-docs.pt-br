---
title: Automática de estatísticas (Analytics Platform System)
description: Descreve o recurso de estatísticas automática introduzido no Analytics Platform System AU7.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
monikerRange: '>= aps-pdw-2016-au7 || = sqlallproducts-allversions'
ms.openlocfilehash: 000a31f76118a3f2acaf702ce5c74c1dd5703422
ms.sourcegitcommit: 3e5f1545e5c6c92fa32e116ee3bff1018ca946a2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37107134"
---
# <a name="configure-auto-statistics"></a>Configurar estatísticas automaticamente

Saiba como configurar o Parallel Data Warehouse para usar automática de estatísticas para criar e atualizar estatísticas automaticamente.  Usar esse recurso para melhorar planos de consulta e, portanto, melhorar o desempenho da consulta.

**Aplica-se a:** APS (começando com 2016 AU7)

## <a name="what-are-statistics"></a>Quais são as estatísticas?
Estatísticas de otimização da consulta são objetos que contêm informações estatísticas sobre a distribuição de valores em uma ou mais colunas de uma tabela. O otimizador de consulta usa essas estatísticas para estimar a cardinalidade, ou resulta de número de linhas na consulta. Essas estimativas de cardinalidade permitem que o otimizador de consulta criar um plano de consulta de alta qualidade. Por exemplo, no APS, os usos de Otimizador de consulta MPP estimativas de cardinalidade para escolher a ordem aleatória ou replicar a menor das duas tabelas usadas em uma cláusula join e assim melhorar o desempenho da consulta.  Para obter mais informações, consulte [estatísticas](../relational-databases/statistics/statistics.md) e [DBCC SHOW_STATISTICS](../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)

## <a name="what-are-auto-statistics"></a>Quais são as estatísticas automaticamente?
Estatística automática é as estatísticas que o otimizador de consulta cria e atualiza automaticamente para melhorar o plano de consulta. As estatísticas podem ficar desatualizadas após os carregamentos, insere, atualizam e exclui operações. Sem estatísticas automaticamente, você precisará fazer sua própria análise para entender quais colunas precisam de estatísticas e quando as estatísticas precisam ser atualizados.

Estatística automática inclui as três configurações a seguir: 

### <a name="autocreatestatistics"></a>AUTO_CREATE_STATISTICS
Quando a criação automática de opção de estatísticas, AUTO_CREATE_STATISTICS, está ON, o otimizador de consulta cria estatísticas em colunas individuais no predicado da consulta, conforme necessário, para melhorar as estimativas de cardinalidade para o plano de consulta. Essas estatísticas de coluna única são criadas em colunas que ainda não têm um histograma em um objeto de estatísticas existente.

### <a name="autoupdatestatistics"></a>AUTO_UPDATE_STATISTICS 
Quando a opção de atualização automática de estatísticas, AUTO_UPDATE_STATISTICS, está ativada, o otimizador de consulta determina quando as estatísticas podem estar desatualizadas e as atualiza quando são usadas por uma consulta. As estatísticas ficam desatualizadas depois que operações de inserção, atualização, exclusão ou mesclagem alteram a distribuição dos dados na tabela ou na exibição indexada. O otimizador de consulta determina quando estatísticas podem estar desatualizadas contando o número de modificações de dados desde a última atualização das estatísticas e comparando o número de modificações a um limite. O limite se baseia no número de linhas na tabela ou na exibição indexada.

### <a name="autoupdatestatisticsasync"></a>AUTO_UPDATE_STATISTICS_ASYNC
A opção de atualização de estatísticas assíncrona, AUTO_UPDATE_STATISTICS_ASYNC, determina se o otimizador de consulta usa atualizações de estatísticas síncronas ou assíncronas. Para pontos de acesso, a opção de atualização de estatísticas assíncrona está ON por padrão e o otimizador de consulta atualiza estatísticas de forma assíncrona. A opção AUTO_UPDATE_STATISTICS_ASYNC se aplica a objetos de estatísticas criados para índices, colunas únicas em predicados de consulta e estatísticas criadas com a instrução CREATE STATISTICS.

## <a name="configuration-settings-for-system-administrators"></a>Definições de configuração para os administradores do sistema
Após a atualização para AU7 APS, automática de estatísticas é habilitada por padrão. O administrador do sistema pode habilitar ou desabilitar estatísticas automaticamente com o [comutador de recurso](appliance-feature-switch.md) opção no Gerenciador de configuração do dispositivo.  Uma vez habilitada, os usuários podem alterar as configurações de estatísticas por banco de dados.
Alterar quaisquer valores de comutador de recurso exige uma reinicialização do serviço em pontos de acesso.

## <a name="change-auto-statistics-settings-on-a-database"></a>Alterar configurações de estatísticas automática em um banco de dados
Quando automática de estatísticas é habilitada pelo administrador do sistema, você pode usar [ALTER DATABASE (Parallel Data Warehouse)](/sql/t-sql/statements/alter-database-parallel-data-warehouse) para alterar as configurações de estatísticas em um banco de dados. Se o comutador de recurso de estatísticas automático estiver habilitado pelo administrador do sistema, quaisquer novos bancos de dados criados após a atualização para AU7 terá automática de estatísticas habilitada. Todos os bancos de dados que existiam antes da atualização para AU7 têm estatísticas automaticamente desabilitadas. O exemplo a seguir habilita automática de estatísticas sobre o myPDW de banco de dados existente.

```sql
ALTER DATABASE myPDW SET AUTO_CREATE_STATISTICS ON
ALTER DATABASE myPDW SET AUTO_UPDATE_STATISTICS ON 
ALTER DATABASE myPDW SET AUTO_UPDATE_STATISTICS_ASYNC ON
```
 
Opção de AUTO_UPDATE STATISTICS_ASYNC só funcionará se AUTO_UPDATE_STATISTICS está ON.  Portanto, as estatísticas não são atualizadas quando AUTO_UPDATE_STATISTICS está OFF e AUTO_UPDATE_STATISTICS_ASYNC está ON. 

### <a name="error-messages"></a>Mensagens de erro
Você pode receber a mensagem de erro "essa opção não tem suporte no PDW".  Esse erro ocorre quando o administrador do sistema não tiver habilitado estatísticas automaticamente e você tentar definir qualquer um dos automático opções de estatísticas no banco de dados ALTER. 

### <a name="limitations-and-restrictions"></a>Limitações e restrições
Estatística automática não funciona em tabelas externas. 

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

Um valor de retorno 1 significa que a configuração está em e 0 significa que a configuração está desativada. 

## <a name="next-steps"></a>Próximas etapas
Para ver como estão o desempenho de suas consultas, consulte [monitorando consultas ativas](monitoring-active-queries.md)
