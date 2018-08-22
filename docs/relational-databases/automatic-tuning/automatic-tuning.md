---
title: O ajuste automático | Microsoft Docs
description: Saiba mais sobre o ajuste automático no SQL Server e banco de dados SQL
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
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: a710c1bd6731feaae662133ff8f18bbf9ac12976
ms.sourcegitcommit: b70b99c2e412b4d697021f3bf1a92046aafcbe37
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2018
ms.locfileid: "40393558"
---
# <a name="automatic-tuning"></a>Ajuste automático
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  O ajuste automático é um recurso de banco de dados que fornece informações sobre possíveis problemas de desempenho de consultas, recomenda soluções e corrige automaticamente os problemas identificados.

Ajuste automático no [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] notifica sempre que um possível problema de desempenho é detectado e permite que você aplique ações corretivas ou permite que o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] corrigir automaticamente problemas de desempenho.
Ajuste automático no [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] permite que você identifique e corrija problemas de desempenho causados por **as regressões de escolha do plano SQL**. Ajuste automático no [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] cria índices necessários e descarta os índices não utilizados.

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] monitora as consultas que são executadas no banco de dados e melhora o desempenho da carga de trabalho automaticamente. [!INCLUDE[ssde_md](../../includes/ssde_md.md)] tem um mecanismo de inteligência interna que pode ajustar e melhorar o desempenho de suas consultas adaptando dinamicamente o banco de dados para sua carga de trabalho automaticamente. Há dois recursos de ajuste automático que estão disponíveis:

 -  **Correção automática de plano** (disponível no [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] e [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]) que identifica os planos de execução de consulta problemático e correções de SQL planejar problemas de desempenho.
 -  **Gerenciamento de índice automático** (disponível apenas no [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]) que identifica os índices que devem ser adicionados ao seu banco de dados e índices que devem ser removidos.

## <a name="why-automatic-tuning"></a>Por que o ajuste automático?

Uma das principais tarefas de administração clássico do banco de dados está monitorando uma carga de trabalho, identificando críticos [!INCLUDE[tsql_md](../../includes/tsql-md.md)] consultas, índices que devem ser adicionados para melhorar o desempenho e raramente usado índices. [!INCLUDE[ssde_md](../../includes/ssde_md.md)] Fornece informações detalhadas sobre as consultas e os índices que você precisa monitorar. No entanto, monitorar constantemente o banco de dados é uma tarefa difícil e entediante, especialmente ao lidar com muitos bancos de dados. Gerenciar um grande número de bancos de dados pode ser impossível de fazer com eficiência. Em vez de monitorar e ajustar seu banco de dados manualmente, você pode considerar delegar algumas do monitoramento e ajuste de ações a serem [!INCLUDE[ssde_md](../../includes/ssde_md.md)] usando o recurso de ajuste automático.

### <a name="how-does-automatic-tuning-works"></a>Como o ajuste automático funciona?

O ajuste automático é um processo de análise que constantemente aprende sobre as características da carga de trabalho e o monitoramento contínuo e identificar possíveis problemas e aprimoramentos.

![Processo de ajuste automático](./media/tuning-process.png)

Esse processo permite que o banco de dados adaptar-se dinamicamente à carga de trabalho, localizando quais planos e índices podem melhorar o desempenho das cargas de trabalho e quais índices afetam suas cargas de trabalho. Com base nessas conclusões, o ajuste automático aplica ações de ajuste que melhoram o desempenho da carga de trabalho. Além disso, o banco de dados monitora continuamente o desempenho após qualquer alteração feita pelo ajuste automático para garantir que ele melhora o desempenho da carga de trabalho. Qualquer ação que não melhorar o desempenho é revertida automaticamente. Esse processo de verificação é um recurso importante que garante que qualquer alteração feita pelo ajuste automático não diminua o desempenho da carga de trabalho.

## <a name="automatic-plan-correction"></a>Correção automática de plano

Correção automática de plano é um recurso de ajuste automático que identifica **regressão da escolha de planos SQL** e corrigir automaticamente o problema, forçando o último plano bom conhecido.

### <a name="what-is-sql-plan-choice-regression"></a>O que é regressão da escolha do plano SQL?

[!INCLUDE[ssdenoversion_md](../../includes/ssdenoversion_md.md)] podem usar diferentes planos SQL para executar o [!INCLUDE[tsql_md](../../includes/tsql-md.md)] consultas. Planos de consulta dependem de estatísticas, índices e outros fatores. O plano ideal que deve ser usado para executar algumas [!INCLUDE[tsql_md](../../includes/tsql-md.md)] consulta poderá ser alterada ao longo do tempo. Em alguns casos, o novo plano não pode ser melhor do que o anterior, e o novo plano pode causar uma regressão de desempenho.

 ![Regressão da escolha do plano SQL](media/plan-choice-regression.png "regressão da escolha do plano SQL") 

Sempre que você observe a regressão da escolha do plano, você deve encontrar alguns bons anteriores planejar e forçá-lo em vez de usar um atual `sp_query_store_force_plan` procedimento.
[!INCLUDE[ssde_md](../../includes/ssde_md.md)] em [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] fornece informações sobre com regressão recente de planos e as ações corretivas recomendadas.
Além disso, [!INCLUDE[ssde_md](../../includes/ssde_md.md)] lhe permite automatizar esse processo totalmente e permitir que [!INCLUDE[ssde_md](../../includes/ssde_md.md)] corrigir qualquer problema encontrado relacionadas às alterações de plano.

### <a name="automatic-plan-choice-correction"></a>Correção da escolha automática de plano

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] muda automaticamente para o último bom plano conhecido sempre que a regressão da escolha do plano é detectada.

![Correção de escolha do plano SQL](media/force-last-good-plan.png "correção de escolha do plano SQL") 

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] detecta automaticamente qualquer regressão da escolha do plano potencial incluindo o plano que deve ser usado em vez do plano errado.
Quando o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] aplica o último bom plano conhecido, ele automaticamente monitora o desempenho do plano forçado. Se o plano forçado não é melhor do que o plano regredido, o novo plano não será forçado e o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] compilará um novo plano. Se [!INCLUDE[ssde_md](../../includes/ssde_md.md)] verifica se o plano forçado é melhor do que o regredido, o plano forçado será retido até uma recompilação (por exemplo, na próxima alteração de esquema ou de estatísticas) se é melhor do que o plano regredido.

Observação: Qualquer automática de planos forçada fazer não persit após uma reinicialização da instância do SQL Server.

### <a name="enabling-automatic-plan-choice-correction"></a>Habilitando a correção da escolha automática de plano

Habilite o ajuste automático por banco de dados e especifique que o último bom plano deve ser forçado sempre que uma regressão da alteração do plano for detectada. O ajuste automático é habilitado com o seguinte comando:

```sql   
ALTER DATABASE current
SET AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = ON ); 
```
Depois que você ativar essa opção, [!INCLUDE[ssde_md](../../includes/ssde_md.md)] automaticamente forçar qualquer recomendação em que o ganho estimado de CPU é maior do que 10 segundos, ou o número de erros no novo plano é maior do que o número de erros no plano recomendado e verificar se a plano forçado é melhor do que o atual.

### <a name="alternative---manual-plan-choice-correction"></a>Alternativa – correção de escolha do plano manual

Sem o ajuste automático, os usuários devem monitorar o sistema periodicamente e procurar as consultas regredidas. Se um plano tiver regredido, o usuário deverá encontrar bons anteriores planejar e forçá-lo em vez de usar um atual `sp_query_store_force_plan` procedimento. A prática recomendada seria forçar o último plano bom conhecido como planos mais antigos podem ser inválidos devido a alterações de índice ou estatística. O usuário que força o último plano bom conhecido deve monitorar o desempenho da consulta que é executado usando o plano forçado e verifique se o plano forçado funciona conforme o esperado. Dependendo do resultado da análise e monitoramento, o plano deve ser forçado ou o usuário deverá encontrar uma outra maneira de otimizar a consulta.
Planos forçados manualmente não devem ser forçados para sempre, pois o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] deve ser capaz de aplicar os planos de qualidade. O usuário ou um DBA deve, eventualmente, não forçar plano usando `sp_query_store_unforce_plan` procedimento e deixar que o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] encontrar o plano ideal.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece todas as exibições necessárias e procedimentos necessários para monitorar o desempenho e corrigir problemas no Query Store.

No [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], você pode encontrar as regressões de escolha de plano usando exibições do sistema de Store de consulta. Na [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)], o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] detecta e mostra as regressões de escolha do plano potencial e as ações recomendadas que devem ser aplicadas na [DM db_tuning_recommendations &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md) exibição. O modo de exibição mostra informações sobre o problema, a importância do problema e detalhes de como a consulta identificada, a ID do plano regredido, o ID do plano que foi usado como linha de base para comparação e o [!INCLUDE[tsql_md](../../includes/tsql-md.md)] instrução que pode ser executada para corrigir o problema.

| Tipo | descrição | DATETIME | score | detalhes | … |
| --- | --- | --- | --- | --- | --- |
| `FORCE_LAST_GOOD_PLAN` | Tempo de CPU alterado de 4 ms a ms 14 | 3/17/2017 | 83 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |
| `FORCE_LAST_GOOD_PLAN` | Tempo de CPU alterado de 37 ms a ms 84 | 3/16/2017 | 26 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |

Algumas colunas nessa exibição são descritas na lista a seguir:
 - Tipo de ação recomendado - `FORCE_LAST_GOOD_PLAN`.
 - Descrição que contém informações sobre por que [!INCLUDE[ssde_md](../../includes/ssde_md.md)] pensa que essa alteração de plano é uma regressão de desempenho potencial.
 - Data e hora quando a regressão potencial for detectada.
 - Pontuação dessa recomendação. 
 - Detalhes sobre os problemas, como ID do plano detectado, ID do plano regredido, o ID do plano que deve ser forçado para corrigir o problema, [!INCLUDE[tsql_md](../../includes/tsql-md.md)] script que possa ser aplicada para corrigir o problema, etc. Os detalhes estão armazenados [formato JSON](../../relational-databases/json/index.md).

Use a consulta a seguir para obter um script que corrige o problema e obter informações adicionais sobre a estimados obter:

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

| reason | score | script | consulta\_id | plano atual\_id | recomendado plano\_id | estimado\_obter | Erro\_sujeito a
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Tempo de CPU alterado de 3 ms a ms 46 | 36 | EXEC sp\_consulta\_armazenar\_forçar\_plano 12, 17; | 12 | 28 | 17 | 11.59 | 0

`estimated_gain` representa o número estimado de segundos que seria economizado se o plano recomendado seria executado em vez do plano atual. Plano recomendado deve ser forçado em vez do plano atual, se o ganho for maior que 10 segundos. Se houver mais erros (por exemplo, os tempos limite ou execuções anuladas) no plano de que no recomendada planejar, a coluna `error_prone` seria definido como o valor `YES`. Plano de sujeito a erro é outra razão por que o plano recomendado deve ser forçado em vez do atual.

Embora [!INCLUDE[ssde_md](../../includes/ssde_md.md)] fornece todas as informações necessárias para identificar as regressões de escolha do plano; contínua monitorando e corrigindo problemas de desempenho podem ser um processo entediante. O ajuste automático torna esse processo muito mais fácil.

Observação: Os dados nessa DMV não persistem após uma reinicialização da instância do SQL Server.

## <a name="automatic-index-management"></a>Gerenciamento de índice automático

Na [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)], o gerenciamento de índice é fácil porque [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] aprende sobre sua carga de trabalho e garante que seus dados são indexados sempre da melhor forma. Design de índice apropriado é crucial para otimizar o desempenho da carga de trabalho e gerenciamento de índice automático pode ajudá-lo a otimizar seus índices. Gerenciamento de índice automático pode corrigir problemas de desempenho em bancos de dados indexados incorretamente ou manter e aprimorar os índices no esquema de banco de dados existente. Ajuste automático no [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] executa as seguintes ações:

 - Identifica os índices que podem melhorar o desempenho das consultas do T-SQL que leem dados das tabelas.
 - Identifica os índices redundantes ou índices que não foram usados em um período mais longo de tempo que pode ser removido. Removendo índices desnecessários melhora o desempenho das consultas que atualizam dados em tabelas.

### <a name="why-do-you-need-index-management"></a>Por que você precisa de gerenciamento de índice?

Os índices aceleram algumas de suas consultas que leem dados das tabelas; No entanto, eles podem retardar as consultas que atualizam dados. Você precisa analisar cuidadosamente quando criar um índice e quais colunas você precisa incluir no índice. Alguns índices podem não ser necessárias mais tarde. Portanto, você precisa identificar periodicamente e descartar os índices que não geram nenhum benefício. Se você ignorar os índices não utilizados, o desempenho das consultas que atualizam dados será reduzido sem nenhum benefício nas consultas de leitura de dados. Índices não utilizados também afetam o desempenho geral do sistema porque atualizações adicionais precisam do log desnecessário.

Localizar o conjunto ideal de índices que melhoram o desempenho das consultas que leem dados suas tabelas e tenham impacto mínimo sobre as atualizações pode exigir análise contínua e complexa.

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] usos de inteligência interna e regras avançadas para analisar suas consultas, identifique os índices que seriam ideais para suas cargas de trabalho atuais e os índices podem ser removidos. Banco de dados SQL do Azure garante que você tenha um conjunto mínimo necessário de índices que otimizam as consultas que leem dados, com o menor impacto sobre as outras consultas.

### <a name="automatic-index-management"></a>Gerenciamento de índice automático

Além de detecção, [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] pode aplicar automaticamente as recomendações identificadas. Se você achar que as regras internas melhorar o desempenho de seu banco de dados, você pode permitir que [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] gerenciar automaticamente seus índices.

Para habilitar o ajuste automático no banco de dados SQL e permitir que o recurso de ajuste automático totalmente gerencie sua carga de trabalho, consulte [habilitar o ajuste automático no banco de dados do SQL Azure usando o portal do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-automatic-tuning-enable).

Quando o [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] aplica-se uma recomendação CREATE INDEX ou DROP INDEX, ele automaticamente monitora o desempenho das consultas que são afetados pelo índice. Novo índice será mantido somente se o desempenho das consultas afetadas é aprimorado. O índice ignorado será recriado automaticamente se houver algumas consultas que são executados mais lentamente, devido à ausência do índice.

### <a name="automatic-index-management-considerations"></a>Considerações sobre gerenciamento de índice automático

As ações necessárias para criar índices necessários em [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] pode consumir recursos e afetar o desempenho da carga de trabalho temporariamente. Para minimizar o impacto da criação de índice no desempenho da carga de trabalho, o banco de dados do SQL Azure localiza a janela de tempo apropriado para qualquer operação de gerenciamento de índice. Ação de ajuste é adiada Se o banco de dados precisa de recursos para executar sua carga de trabalho e iniciada quando o banco de dados tem suficiente recursos não utilizados que podem ser usados para a tarefa de manutenção. Um recurso importante no gerenciamento de índice automático é a verificação das ações. Quando o banco de dados SQL cria ou descarta o índice, um processo de monitoramento analisa o desempenho da carga de trabalho para verificar se a ação melhorou o desempenho. Se ele não gerar uma melhoria significativa a ação será revertida imediatamente. Dessa forma, o banco de dados SQL do Azure garante que ações automáticas não afetam negativamente o desempenho da carga de trabalho. Índices criados pelo ajuste automático são transparentes para a operação de manutenção no esquema subjacente. Alterações de esquema como remover ou renomear colunas não são bloqueadas pela presença de índices criados automaticamente. Índices criados automaticamente pelo banco de dados SQL são imediatamente descartados quando relacionadas a tabela ou colunas for descartada.

### <a name="alternative---manual-index-management"></a>Alternativa – gerenciamento de índice manual

Sem gerenciamento de índice automático, usuário precisaria manualmente consultar [DM db_missing_index_details &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md) para localizar os índices que podem melhorar o desempenho, criar índices usando os detalhes fornecido neste modo de exibição e manualmente monitorar o desempenho da consulta. Para localizar os índices que devem ser descartados, os usuários devem monitorar estatísticas de uso operacional dos índices para índices de find raramente usado.

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] simplifica o processo. [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] analisa sua carga de trabalho, identifica as consultas que podem ser executadas mais rapidamente com um novo índice e identifica os índices duplicados ou não utilizados. Encontrar mais informações sobre a identificação de índices que devem ser alterados em [encontrar recomendações de índice no portal do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-advisor-portal).

## <a name="see-also"></a>Consulte também  
 [ALTER DATABASE SET AUTOMATIC_TUNING &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [sys.database_automatic_tuning_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)  
 [sys.dm_db_tuning_recommendations &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)   
 [sys.dm_db_missing_index_details &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [sp_query_store_force_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)     
 [sp_query_store_unforce_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)           
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [Funções JSON](../../relational-databases/json/index.md)
