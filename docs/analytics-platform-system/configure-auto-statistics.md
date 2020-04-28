---
title: Estatísticas automáticas
description: Descreve o recurso de estatísticas automáticas introduzido no Analytics Platform System AU7.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
monikerRange: '>= aps-pdw-2016-au7 || = sqlallproducts-allversions'
ms.openlocfilehash: 7071c9cb46bde6e2d353293cec9f01451c0b4f67
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401280"
---
# <a name="configure-auto-statistics"></a>Configurar estatísticas automáticas

Saiba como configurar o data warehouse paralelo para usar estatísticas automáticas para criar e atualizar estatísticas automaticamente.  Use essa capacidade para melhorar os planos de consulta e, portanto, melhorar o desempenho da consulta.

**Aplica-se a:** APS (começando com 2016-AU7)

## <a name="what-are-statistics"></a>O que são estatísticas?
As estatísticas de otimização de consulta são objetos que contêm informações estatísticas sobre a distribuição de valores em uma ou mais colunas de uma tabela. O otimizador de consulta usa essas estatísticas para estimar a cardinalidade, ou número de linhas, no resultado de consulta. Essas estimativas de cardinalidade permitem que o otimizador de consulta crie um plano de consulta de alta qualidade. Como exemplo, no APS, o otimizador de consulta MPP usa estimativas de cardinalidade para optar por embaralhar ou replicar o menor de duas tabelas usadas em uma cláusula JOIN e, ao fazer isso, melhorar o desempenho da consulta.  Para obter mais informações, consulte [estatísticas](../relational-databases/statistics/statistics.md) e [DBCC SHOW_STATISTICS](../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)

## <a name="what-are-auto-statistics"></a>O que são estatísticas automáticas?
Estatísticas automáticas são estatísticas que o otimizador de consulta cria e atualiza automaticamente para melhorar o plano de consulta. As estatísticas podem ficar desatualizadas depois de carregar, inserir, atualizar e excluir operações. Sem estatísticas automáticas, você precisa fazer sua própria análise para entender quais colunas precisam de estatísticas e quando as estatísticas precisam ser atualizadas.

As estatísticas automáticas incluem as três seguintes configurações: 

### <a name="auto_create_statistics"></a>AUTO_CREATE_STATISTICS
Quando a opção de criação automática de estatísticas, AUTO_CREATE_STATISTICS, está ativada, o otimizador de consulta cria estatísticas em colunas individuais no predicado da consulta, conforme necessário, a fim de melhorar as estimativas de cardinalidade do plano de consulta. Essas estatísticas de coluna única são criadas em colunas que ainda não têm um histograma em um objeto de estatísticas existente.

### <a name="auto_update_statistics"></a>AUTO_UPDATE_STATISTICS 
Quando a opção de atualização automática de estatísticas, AUTO_UPDATE_STATISTICS, está ativada, o otimizador de consulta determina quando as estatísticas podem estar desatualizadas e as atualiza quando são usadas por uma consulta. As estatísticas ficam desatualizadas depois que operações de inserção, atualização, exclusão ou mesclagem alteram a distribuição dos dados na tabela ou na exibição indexada. O otimizador de consulta determina quando estatísticas podem estar desatualizadas contando o número de modificações de dados desde a última atualização das estatísticas e comparando o número de modificações a um limite. O limite se baseia no número de linhas na tabela ou na exibição indexada.

### <a name="auto_update_statistics_async"></a>AUTO_UPDATE_STATISTICS_ASYNC
A opção de atualização de estatísticas assíncrona, AUTO_UPDATE_STATISTICS_ASYNC, determina se o otimizador de consulta usa atualizações de estatísticas síncronas ou assíncronas. Para APS, a opção de atualização de estatísticas assíncrona está ativada por padrão e o otimizador de consulta atualiza estatísticas de forma assíncrona. A opção AUTO_UPDATE_STATISTICS_ASYNC se aplica a objetos de estatísticas criados para índices, colunas únicas em predicados de consulta e estatísticas criadas com a instrução CREATE STATISTICS.

## <a name="configuration-settings-for-system-administrators"></a>Definições de configuração para administradores do sistema
Após a atualização para o APS AU7, as estatísticas automáticas são habilitadas por padrão. O administrador do sistema pode habilitar ou desabilitar estatísticas automáticas com a opção [switch de recurso](appliance-feature-switch.md) no Configuration Manager do dispositivo.  Uma vez habilitado, os usuários podem alterar as configurações de estatísticas por banco de dados.
A alteração de qualquer valor de opção de recurso requer uma reinicialização do serviço no APS.

## <a name="change-auto-statistics-settings-on-a-database"></a>Alterar as configurações de estatísticas automáticas em um banco de dados
Quando estatísticas automáticas são habilitadas pelo administrador do sistema, você pode usar [ALTER DATABASE (Parallel Data warehouse)](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw) para alterar as configurações de estatísticas em um banco de dados. Se a opção de recurso de estatísticas automáticas for habilitada pelo administrador do sistema, todos os novos bancos de dados criados após a atualização para o AU7 terão estatísticas automáticas habilitadas. Todos os bancos de dados que existiam antes da atualização para AU7 têm estatísticas automáticas desabilitadas. O exemplo a seguir habilita estatísticas automáticas no banco de dados myPDW existente.

```sql
ALTER DATABASE myPDW SET AUTO_CREATE_STATISTICS ON
ALTER DATABASE myPDW SET AUTO_UPDATE_STATISTICS ON 
ALTER DATABASE myPDW SET AUTO_UPDATE_STATISTICS_ASYNC ON
```
 
AUTO_UPDATE opção STATISTICS_ASYNC só funcionará se AUTO_UPDATE_STATISTICS estiver ativado.  Portanto, as estatísticas não são atualizadas quando AUTO_UPDATE_STATISTICS está desativado e AUTO_UPDATE_STATISTICS_ASYNC está ativada. 

### <a name="error-messages"></a>Mensagens de erro
Você pode receber a mensagem de erro "esta opção não tem suporte no PDW".  Esse erro ocorre quando o administrador do sistema não habilitou estatísticas automáticas e você tenta definir qualquer uma das opções de estatísticas automáticas em ALTER DATABASE. 

### <a name="limitations-and-restrictions"></a>Limitações e Restrições
As estatísticas automáticas não funcionam em tabelas externas. 

### <a name="check-the-current-values"></a>Verificar os valores atuais
A consulta a seguir retorna os valores atuais das configurações de estatísticas automáticas para todos os bancos de dados.

```sql
SELECT NAME
    , IS_AUTO_CREATE_STATS_ON 
    , IS_AUTO_UPDATE_STATS_ON
    , IS_AUTO_UPDATE_STATS_ASYNC_ON
FROM
    sys.databases;
```

Um valor de retorno 1 significa que a configuração está ativada, e 0 significa que a configuração está desativada. 

## <a name="next-steps"></a>Próximas etapas
Para ver como as consultas estão sendo executadas, consulte [monitorando consultas ativas](monitoring-active-queries.md)
