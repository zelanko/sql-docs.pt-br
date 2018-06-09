---
title: Ajuste automático | Microsoft Docs
description: Saiba mais sobre o ajuste automático no SQL Server e banco de dados do SQL Azure
ms.custom: ''
ms.date: 08/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: automatic-tuning
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- performance tuning [SQL Server]
ms.assetid: ''
caps.latest.revision: ''
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: 0e77a1d7e24fa2635b3e699672338e588c1f5c1c
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34707764"
---
# <a name="automatic-tuning"></a>Ajuste automático
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  O ajuste automático é um recurso de banco de dados que fornece informações sobre possíveis problemas de desempenho de consultas, recomenda soluções e corrige automaticamente os problemas identificados.

O ajuste automático [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] notifica você sempre que um problema de desempenho potencial é detectado e permite que você aplique ações corretivas ou permite que o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] corrigir automaticamente os problemas de desempenho.
O ajuste automático [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] permite identificar e corrigir problemas de desempenho causados por **regressões de escolha do plano SQL**. O ajuste automático [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] cria índices necessários e descarta os índices não utilizados.

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] monitora as consultas que são executadas no banco de dados e melhora o desempenho da carga de trabalho automaticamente. [!INCLUDE[ssde_md](../../includes/ssde_md.md)] tem um mecanismo de inteligência incorporada que pode ajustar e melhorar o desempenho de suas consultas adaptando dinamicamente o banco de dados para sua carga de trabalho automaticamente. Há dois recursos de ajustes automático que estão disponíveis:

 -  **Correção automática plano** (disponível em [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] e [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]) que identifica os planos de execução de consulta problemático e problemas de desempenho do plano de correções de SQL.
 -  **Gerenciamento de índice automáticas** (disponível apenas no [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]) que identifica os índices devem ser adicionados no seu banco de dados e índices que devem ser removidos.

## <a name="why-automatic-tuning"></a>Por que o ajuste automático?

Uma das principais tarefas de administração clássico do banco de dados está monitorando a carga de trabalho, identificando crítico [!INCLUDE[tsql_md](../../includes/tsql_md.md)] consultas de índices que devem ser adicionados para melhorar o desempenho e raramente usado índices. [!INCLUDE[ssde_md](../../includes/ssde_md.md)] Fornece informações detalhadas sobre as consultas e os índices que você precisa monitorar. No entanto, monitore o banco de dados é uma tarefa difícil e entediante, especialmente ao lidar com muitos bancos de dados. Gerenciar um grande número de bancos de dados pode ser impossível fazer com eficiência. Em vez de monitorar e ajustar o banco de dados manualmente, você pode considerar delegar algumas do monitoramento e ajuste as ações a serem [!INCLUDE[ssde_md](../../includes/ssde_md.md)] usando o recurso de ajuste automático.

### <a name="how-does-automatic-tuning-works"></a>Como funciona o works ajuste automático?

Ajuste automático é um processo de análise que constantemente aprende sobre as características da carga de trabalho e o monitoramento contínuo e identificar possíveis problemas e aprimoramentos.

![Processo de ajuste automático](./media/tuning-process.png)

Esse processo permite que o banco de dados adaptar-se dinamicamente para sua carga de trabalho, localizando quais planos e índices podem melhorar o desempenho das cargas de trabalho e quais índices afetam suas cargas de trabalho. Com base nessas conclusões, ajuste automático aplica-se ajuste ações que melhoram o desempenho da carga de trabalho. Além disso, o banco de dados monitora continuamente desempenho após qualquer alteração feita pelo ajuste automático para garantir que ele melhora o desempenho da carga de trabalho. Qualquer ação que não melhorar o desempenho é revertida automaticamente. Esse processo de verificação é um recurso importante que garante que qualquer alteração feita pelo ajuste automático não diminuir o desempenho da carga de trabalho.

## <a name="automatic-plan-correction"></a>Correção automática de plano

Correção de plano automático é um recurso de ajuste automático que identifica **regressão da escolha de planos SQL** e corrigir automaticamente o problema, forçando o último plano bom conhecido.

### <a name="what-is-sql-plan-choice-regression"></a>O que é regressão de escolha do plano SQL?

[!INCLUDE[ssdenoversion_md](../../includes/ssdenoversion_md.md)] pode usar diferentes planos SQL para executar o [!INCLUDE[tsql_md](../../includes/tsql_md.md)] consultas. Planos de consulta dependem de estatísticas, índices e outros fatores. O plano ideal que deve ser usado para executar algumas [!INCLUDE[tsql_md](../../includes/tsql_md.md)] consulta poderá ser alterada ao longo do tempo. Em alguns casos, o novo plano não pode ser melhor que o anterior, e o novo plano pode causar uma regressão de desempenho.

 ![Regressão de escolha do plano SQL](media/plan-choice-regression.png "regressão de escolha do plano SQL") 

Sempre que você observar a regressão de escolha do plano, você deve encontrar bons anteriores planejar e forçá-lo em vez de usar um atual `sp_query_store_force_plan` procedimento.
[!INCLUDE[ssde_md](../../includes/ssde_md.md)] em [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] fornece informações sobre planos de regressão e as ações corretivas recomendadas.
Além disso, [!INCLUDE[ssde_md](../../includes/ssde_md.md)] permite automatizar esse processo totalmente e permitem [!INCLUDE[ssde_md](../../includes/ssde_md.md)] corrija qualquer problema encontrado relacionadas às alterações de plano.

### <a name="automatic-plan-choice-correction"></a>Correção de escolha do plano automático

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] automaticamente pode alternar para o último plano bom conhecido, sempre que a regressão de escolha do plano é detectado.

![Correção de opção de plano SQL](media/force-last-good-plan.png "correção de opção de plano SQL") 

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] detecta automaticamente qualquer potencial regressão de escolha do plano incluindo o plano deve ser usado em vez do plano incorreto.
Quando o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] aplica-se a última conhecido bom plano, ele automaticamente monitora o desempenho do plano forçado. Se o plano forçado não é melhor do que o plano retornado, o novo plano será unforced e o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] compilará um novo plano. Se [!INCLUDE[ssde_md](../../includes/ssde_md.md)] verifica se o plano forçado é melhor do que um retornadas, o plano forçado será mantido até uma recompilação (por exemplo, na próxima alteração de esquema ou de estatísticas) se ele é melhor do que o plano retornado.

Observação: Qualquer automática de planos forçada não não persit em uma reinicialização da instância do SQL Server.

### <a name="enabling-automatic-plan-choice-correction"></a>Habilitando a correção de escolha do plano automático

Habilite o ajuste automático por banco de dados e especifique que o último bom plano deve ser forçado sempre que uma regressão da alteração do plano for detectada. O ajuste automático é habilitado com o seguinte comando:

```sql   
ALTER DATABASE current
SET AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = ON ); 
```
Depois que você turn-on essa opção, [!INCLUDE[ssde_md](../../includes/ssde_md.md)] automaticamente forçará qualquer recomendação onde o ganho estimado de CPU é maior do que 10 segundos, ou o número de erros no novo plano é maior do que o número de erros no plano recomendado e verificar se a plano forçado é melhor que o atual.

### <a name="alternative---manual-plan-choice-correction"></a>Alternativa - correção de escolha do plano manual

Sem o ajuste automático, os usuários devem monitorar o sistema periodicamente e procurar as consultas regredidas. Se qualquer plano de regressão, o usuário deve encontrar bons anteriores planejar e forçá-lo em vez de usar um atual `sp_query_store_force_plan` procedimento. A prática recomendada seria forçar o último bom plano conhecido como planos mais antigos podem ser inválidos devido a alterações de índice ou estatística. O usuário que força o último plano bom conhecido deve monitorar o desempenho da consulta que é executado usando o plano forçado e verifique se esse plano forçado funciona conforme o esperado. Dependendo dos resultados da análise e monitoramento, o plano deve ser forçado ou usuário deve encontrar uma outra maneira de otimizar a consulta.
Planos forçados manualmente não devem ser forçados para sempre, porque o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] deve ser capaz de aplicar planos de qualidade. O usuário ou o DBA deve, eventualmente, cancelar a imposição de plano usando `sp_query_store_unforce_plan` procedimento e deixe o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] localizar o plano ideal.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece todas as exibições necessárias e procedimentos necessários para monitorar o desempenho e corrigir problemas no repositório de consultas.

Em [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], você pode encontrar regressões de escolha do plano usando exibições de sistema do repositório de consultas. Em [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)], o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] detecta e mostra as regressões de escolha do plano potencial e as ações recomendadas que devem ser aplicadas no [sys.dm_db_tuning_recommendations &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md) exibição. O modo de exibição mostra informações sobre o problema, a importância do problema e detalhes de como a consulta identificada, a ID do plano retornada, a ID do plano que foi usada como linha de base para comparação e o [!INCLUDE[tsql_md](../../includes/tsql_md.md)] instrução que pode ser executada para corrigir o problema.

| Tipo | descrição | DATETIME | score | detalhes | … |
| --- | --- | --- | --- | --- | --- |
| `FORCE_LAST_GOOD_PLAN` | Tempo de CPU alterado de 4 ms para ms 14 | 3/17/2017 | 83 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |
| `FORCE_LAST_GOOD_PLAN` | Tempo de CPU alterado de 37 ms para 84 ms | 3/16/2017 | 26 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |

Algumas colunas nessa exibição são descritas na lista a seguir:
 - Tipo de ação recomendado - `FORCE_LAST_GOOD_PLAN`.
 - Descrição que contém informações sobre por que [!INCLUDE[ssde_md](../../includes/ssde_md.md)] considera que essa alteração de plano é uma regressão de desempenho potencial.
 - Data e hora a regressão potencial é detectada.
 - Pontuação dessa recomendação. 
 - Detalhes sobre os problemas, como ID do plano detectado, a ID do plano retornado, ID do plano que deve ser forçado para corrigir o problema [!INCLUDE[tsql_md](../../includes/tsql_md.md)]
 script que pode ser aplicado para corrigir o problema, etc. Os detalhes estão armazenados [formato JSON](../../relational-databases/json/index.md).

Use a consulta a seguir para obter um script que corrige o problema e obter informações adicionais sobre o estimado obter:

```sql   
SELECT reason, score,
      script = JSON_VALUE(details, '$.implementationDetails.script'),
      planForceDetails.*,
      estimated_gain = (regressedPlanExecutionCount+recommendedPlanExecutionCount)
                  *(regressedPlanCpuTimeAverage-recommendedPlanCpuTimeAverage)/1000000,
      error_prone = IIF(regressedPlanErrorCount>recommendedPlanErrorCount, 'YES','NO')
FROM sys.dm_db_tuning_recommendations
  CROSS APPLY OPENJSON (Details, '$.planForceDetails')
    WITH (  [query_id] int '$.queryId',
            [current plan_id] int '$.regressedPlanId',
            [recommended plan_id] int '$.recommendedPlanId',

            regressedPlanErrorCount int,
            recommendedPlanErrorCount int,

            regressedPlanExecutionCount int,
            regressedPlanCpuTimeAverage float,
            recommendedPlanExecutionCount int,
            recommendedPlanCpuTimeAverage float

          ) as planForceDetails;
```

[!INCLUDE[ssresult-md](../../includes/ssresult-md.md)]     

| reason | score | script | consulta\_id | plano atual\_id | recomendado plano\_id | estimado\_obter | Erro\_propensas
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Tempo de CPU alterado de 3 ms para ms 46 | 36 | EXEC sp\_consulta\_armazenar\_forçar\_plano 12, 17; | 12 | 28 | 17 | 11.59 | 0

`estimated_gain` representa o número estimado de segundos que seria economizado se o plano recomendado seria executado em vez do plano atual. O plano recomendado deve ser forçado em vez do plano atual se o ganho for maior que 10 segundos. Se não houver mais erros (por exemplo, tempos limite ou anuladas execuções) no plano atual que em recomendada planejar, a coluna `error_prone` será definido como o valor `YES`. Plano sujeitos a erros é outra razão por que o plano recomendado deve ser forçado, em vez do ano atual.

Embora [!INCLUDE[ssde_md](../../includes/ssde_md.md)] fornece todas as informações necessárias para identificar as regressões de escolha do plano; contínua monitorar e corrigir problemas de desempenho podem ser um processo entediante. Ajuste automático torna esse processo muito mais fácil.

Observação: Os dados nessa DMV não persistem após uma reinicialização da instância do SQL Server.

## <a name="automatic-index-management"></a>Gerenciamento de índice automáticas

Em [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)], gerenciamento de índice é fácil porque [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] aprende sobre sua carga de trabalho e garante que seus dados sempre ideal são indexados. Design de índice apropriado é crucial para otimizar o desempenho da carga de trabalho e gerenciamento de índice automáticas pode ajudar a otimizar seus índices. Gerenciamento automático de índice pode corrigir problemas de desempenho em bancos de dados indexados incorretamente ou manter e aprimore os índices no esquema de banco de dados existente. O ajuste automático [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] executa as seguintes ações:

 - Identifica os índices que podem melhorar o desempenho das consultas do T-SQL que leem dados das tabelas.
 - Identifica os índices de redundância ou índices que não foram usados em um período mais longo de tempo que pode ser removido. Removendo índices desnecessários melhora o desempenho das consultas que atualizam dados em tabelas.

### <a name="why-do-you-need-index-management"></a>Por que você precisa de gerenciamento de índice?

Índices de acelerar algumas de suas consultas que leem dados das tabelas; No entanto, eles podem retardar as consultas que atualizam dados. Você precisa analisar cuidadosamente quando criar um índice e quais colunas você precisa incluir no índice. Alguns índices não podem ser necessárias após algum tempo. Portanto, você precisa identificar periodicamente e descartar os índices que não coloque nenhum benefício. Se você ignorar os índices não utilizados, desempenho das consultas que atualizam dados deve ser diminuído sem nenhum benefício nas consultas que ler dados. Índices não utilizados também afetam o desempenho geral do sistema porque atualizações adicionais precisam do log desnecessário.

Localizar o conjunto ideal de índices que melhoram o desempenho das consultas que ler dados das tabelas e têm impacto mínimo sobre as atualizações pode exigir análise contínua e complexa.

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] inteligência interna usa e regras avançadas para analisar suas consultas, identificar índices que seriam ideais para suas cargas de trabalho atuais e os índices podem ser removidos. Banco de dados SQL do Azure garante que você tenha um conjunto mínimo necessário de índices que otimizam as consultas que leem dados, com o menor impacto sobre as outras consultas.

### <a name="automatic-index-management"></a>Gerenciamento de índice automáticas

Além de detecção, [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] podem aplicar automaticamente as recomendações identificadas. Se você achar que as regras internas melhorar o desempenho do banco de dados, você pode permitir que [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] gerenciar automaticamente seus índices.

Para habilitar o ajuste automático no banco de dados do SQL Azure e permitir que o recurso de ajuste automático gerenciar totalmente a carga de trabalho, consulte [Ativar ajuste automático no banco de dados do SQL Azure usando o portal do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-automatic-tuning-enable).

Quando o [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] aplica uma recomendação CREATE INDEX ou DROP INDEX, ele automaticamente monitora o desempenho das consultas que são afetados pelo índice. Novo índice será mantido apenas se o desempenho das consultas afetadas é aprimorado. O índice ignorado será recriado automaticamente se não houver algumas consultas que fique mais lento devido à ausência do índice.

### <a name="automatic-index-management-considerations"></a>Considerações sobre o gerenciamento automático de índice

Ações necessárias para criar índices necessários no [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] pode consumir recursos e afetar o desempenho da carga de trabalho temporariamente. Para minimizar o impacto da criação de índice no desempenho da carga de trabalho, o banco de dados do SQL Azure localiza a janela de tempo apropriado para qualquer operação de gerenciamento de índice. Ação de ajuste é adiada Se o banco de dados precisa de recursos para executar sua carga de trabalho e iniciado quando o banco de dados tem suficiente recursos não utilizados que podem ser usados para a tarefa de manutenção. Um recurso importante no gerenciamento de índice automático é a verificação das ações. Quando o banco de dados do SQL Azure cria ou descarta o índice, um processo de monitoramento analisa o desempenho da carga de trabalho para verificar se a ação de desempenho aprimorado. Se ele não colocar uma melhoria significativa – a ação será revertida imediatamente. Dessa forma, o banco de dados do SQL Azure garante que ações automáticas não afetar negativamente o desempenho da carga de trabalho. Índices criados com o ajuste automático são transparentes para a operação de manutenção no esquema subjacente. Alterações de esquema, como remover ou renomear colunas não são bloqueadas pela presença de índices criados automaticamente. Os índices são criados automaticamente pelo banco de dados do SQL Azure imediatamente são descartados quando relacionadas a tabela ou colunas é descartada.

### <a name="alternative---manual-index-management"></a>Alternativa - gerenciamento de índice manual

Sem o gerenciamento automático de índice, usuário precisa consultar manualmente [sys.DM db_missing_index_details &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md) para localizar os índices que podem melhorar o desempenho, criar índices usando os detalhes fornecido neste modo de exibição e manualmente monitorar o desempenho da consulta. Para localizar os índices devem ser descartados, os usuários devem monitorar estatísticas de uso operacional dos índices para índices de localizar raramente usada.

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] simplifica o processo. [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] analisa a carga de trabalho, identifica as consultas que podem ser executadas mais rapidamente com um novo índice e identifica os índices duplicados ou não utilizados. Encontre mais informações sobre a identificação de índices que devem ser alteradas em [encontrar recomendações de índice no portal do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-advisor-portal).

## <a name="see-also"></a>Consulte também  
 [ALTER DATABASE SET AUTOMATIC_TUNING &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [sys.database_automatic_tuning_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)  
 [sys.dm_db_tuning_recommendations &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)   
 [sys.dm_db_missing_index_details &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [sp_query_store_force_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)     
 [sp_query_store_unforce_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)           
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [Funções JSON](../../relational-databases/json/index.md)
