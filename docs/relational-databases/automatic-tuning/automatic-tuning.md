---
title: Ajuste automático | Microsoft Docs
description: Saiba mais sobre o ajuste automático no SQL Server e no banco de dados SQL do Azure
ms.custom: fasttrack-edit
ms.date: 08/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- performance tuning [SQL Server]
ms.assetid: ''
author: jovanpop-msft
ms.author: jovanpop
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5ce830c3fcd5661a01ecc0ad3ad84bed420be2e0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "82107977"
---
# <a name="automatic-tuning"></a>Ajuste automático
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

O ajuste automático é um recurso de banco de dados que fornece informações sobre possíveis problemas de desempenho de consultas, recomenda soluções e corrige automaticamente os problemas identificados.

O ajuste automático [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] no notifica sempre que um possível problema de desempenho é detectado e permite que você aplique ações corretivas, ou permite [!INCLUDE[ssde_md](../../includes/ssde_md.md)] que o corrija automaticamente os problemas de desempenho. O ajuste automático [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] no permite que você identifique e corrija problemas de desempenho causados por **regressões de opções de plano de execução de consulta**. O ajuste automático [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] também cria índices necessários e descarta índices não utilizados. Para obter mais informações sobre planos de execução de consulta, consulte [planos de execução](../../relational-databases/performance/execution-plans.md).

O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] monitora as consultas que são executadas no banco de dados e melhora automaticamente o desempenho da carga de trabalho. O [!INCLUDE[ssde_md](../../includes/ssde_md.md)] tem um mecanismo de inteligência interno que pode ajustar e aprimorar automaticamente o desempenho de suas consultas, adaptando dinamicamente o banco de dados para sua carga de trabalho. Há dois recursos de ajuste automático que estão disponíveis:

 -  A **correção automática de plano** identifica planos de execução de consulta problemáticos e corrige problemas de desempenho do plano de execução de consulta. **Aplica-se ao**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Começando pelo [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]
 -  O **gerenciamento automático de índice** identifica os índices que devem ser adicionados ao banco de dados e os índices que devem ser removidos. **Aplica-se ao**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

## <a name="why-automatic-tuning"></a>Por que usar o ajuste automático?

Três das principais tarefas na administração de banco de dados clássica estão monitorando a carga [!INCLUDE[tsql_md](../../includes/tsql-md.md)] de trabalho, identificando consultas críticas e identificando índices que devem ser adicionados para melhorar o desempenho ou índices que raramente são usados e podem ser removidos para melhorar o desempenho. O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] fornece informações detalhadas sobre as consultas e os índices que você precisa monitorar. No entanto, o monitoramento constante de um banco de dados é uma tarefa difícil e entediante, especialmente ao lidar com muitos bancos de dados. O gerenciamento de um grande número de bancos de dados pode ser impossível de fazer com eficiência. Em vez de monitorar e ajustar seu banco de dados manualmente, você pode considerar delegar algumas das ações de monitoramento e [!INCLUDE[ssde_md](../../includes/ssde_md.md)] ajuste ao recurso usando ajuste automático.

### <a name="how-does-automatic-tuning-work"></a>Como funciona o trabalho de ajuste automático?

O ajuste automático é um processo contínuo de monitoramento e análise que aprende constantemente sobre as características de sua carga de trabalho e identifica possíveis problemas e melhorias.

![Processo de ajuste automático](./media/tuning-process.png)

Esse processo permite que o banco de dados se adapte dinamicamente à sua carga de trabalho, localizando quais índices e planos podem melhorar o desempenho de suas cargas de trabalho e quais índices afetam suas cargas de trabalho. Com base nessas descobertas, o ajuste automático aplica ações de ajuste que melhoram o desempenho de sua carga de trabalho. Além disso, o ajuste automático monitora continuamente o desempenho do banco de dados depois de implementar as alterações para garantir que ele melhora o desempenho da carga de trabalho. Qualquer ação que não melhorou o desempenho é revertida automaticamente. Esse processo de verificação é um recurso importante que garante que qualquer alteração feita pelo ajuste automático não diminua o desempenho geral da carga de trabalho.

## <a name="automatic-plan-correction"></a>Correção automática de plano

A correção automática de plano é um recurso de ajuste automático que identifica a **regressão da opção do plano de execução** e corrige automaticamente o problema forçando o último plano válido conhecido. Para obter mais informações sobre planos de execução de consulta e o otimizador de consulta, consulte o [Guia de arquitetura de processamento de consultas](../../relational-databases/query-processing-architecture-guide.md).

### <a name="what-is-execution-plan-choice-regression"></a>O que é regressão de opção de plano de execução?

O [!INCLUDE[ssdenoversion_md](../../includes/ssdenoversion_md.md)] pode usar planos de execução diferentes para executar [!INCLUDE[tsql_md](../../includes/tsql-md.md)] as consultas. Os planos de consulta dependem das estatísticas, dos índices e de outros fatores. O plano ideal que deve ser usado para executar uma [!INCLUDE[tsql_md](../../includes/tsql-md.md)] consulta pode mudar ao longo do tempo, dependendo das alterações nesses fatores. Em alguns casos, o novo plano pode não ser melhor do que o anterior, e o novo plano pode causar uma regressão de desempenho.

 ![Regressão da opção do plano de execução de consulta](media/plan-choice-regression.png "Regressão da opção do plano de execução de consulta") 

Sempre que você perceber que uma regressão de escolha de plano ocorreu, você deve encontrar um bom plano anterior e forçá-lo a ser usado em vez do atual. Isso pode ser feito usando o `sp_query_store_force_plan` procedimento. O [!INCLUDE[ssde_md](../../includes/ssde_md.md)] no [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] fornece informações sobre planos regressivos e ações corretivas recomendadas. Além disso [!INCLUDE[ssde_md](../../includes/ssde_md.md)] , o permite automatizar completamente esse processo e deixar [!INCLUDE[ssde_md](../../includes/ssde_md.md)] a correção de qualquer problema encontrado relacionado à alteração do plano.

### <a name="automatic-plan-choice-correction"></a>Correção automática de escolha do plano

O [!INCLUDE[ssde_md](../../includes/ssde_md.md)] pode alternar automaticamente para o último plano bom conhecido sempre que uma regressão de escolha de plano for detectada.

![Correção de opção do plano de execução de consulta](media/force-last-good-plan.png "Correção de opção do plano de execução de consulta") 

O [!INCLUDE[ssde_md](../../includes/ssde_md.md)] detecta automaticamente qualquer regressão de opção de plano potencial, incluindo o plano que deve ser usado em vez do plano errado. Quando o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] aplica o último plano bom conhecido, ele monitora automaticamente o desempenho do plano forçado. Se o plano forçado não for melhor do que o plano regressivo, o novo plano não será forçado e o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] compilará um novo plano. Se o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] verificar se o plano forçado é melhor do que o plano regressivo, o plano forçado será retido. Ele será retido até que ocorra uma recompilação (por exemplo, na próxima atualização de estatísticas ou alteração de esquema).

> [!NOTE]
> Qualquer plano de execução forçado automaticamente não é persistido entre as [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reinicializações da instância.

### <a name="enabling-automatic-plan-choice-correction"></a>Habilitando a correção automática da escolha do plano

Você pode habilitar o ajuste automático por banco de dados e especificar que o último plano bom deve ser forçado sempre que alguma regressão de alteração de plano for detectada. O ajuste automático é habilitado com o seguinte comando:

```sql   
ALTER DATABASE <yourDatabase>
SET AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = ON ); 
```

Depois de habilitar essa opção, o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] forçará automaticamente qualquer recomendação em que o lucro estimado da CPU seja maior que 10 segundos ou o número de erros no novo plano seja maior que o número de erros no plano recomendado e verifique se o plano forçado é melhor do que o atual.

### <a name="alternative---manual-plan-choice-correction"></a>Alternativa – correção manual da escolha do plano

Sem o ajuste automático, os usuários devem monitorar periodicamente o sistema e procurar as consultas que foram regressivas. Se qualquer plano tiver se regressivo, o usuário deverá encontrar um bom plano anterior e forçá-lo em vez do atual `sp_query_store_force_plan` usando o procedimento. A prática recomendada seria forçar o último plano bom conhecido porque os planos mais antigos podem ser inválidos devido a alterações de índice ou estatística. O usuário que força o último plano bom conhecido deve monitorar o desempenho da consulta executada usando o plano forçado e verificar se o plano forçado funciona conforme o esperado. Dependendo dos resultados do monitoramento e da análise, o plano deve ser forçado ou o usuário deve encontrar outra maneira de otimizar a consulta, como regravá-la. Os planos forçados manualmente não devem ser forçados para [!INCLUDE[ssde_md](../../includes/ssde_md.md)] sempre, porque o deve ser capaz de aplicar planos ideais. O usuário ou DBA deve eventualmente não forçar o plano usando `sp_query_store_unforce_plan` o procedimento e deixar que [!INCLUDE[ssde_md](../../includes/ssde_md.md)] a encontre o plano ideal. 

> [!TIP]
> Como alternativa, use as **consultas com planos forçados** repositório de consultas exibição para localizar e não forçar planos.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]fornece todas as exibições e os procedimentos necessários para monitorar o desempenho e corrigir problemas no Repositório de Consultas.

No [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], você pode encontrar regressões de escolha de plano usando exibições do sistema repositório de consultas. No [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)], o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] detecta e mostra regressões de escolha de plano potencial e as ações recomendadas que devem ser aplicadas na exibição de [&#41;sys. dm_db_tuning_recommendations &#40;Transact-SQL](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md) . A exibição mostra informações sobre o problema, a importância do problema e detalhes como a consulta identificada, a ID do plano regressivo, a ID do plano que foi usado como linha de base para comparação e a [!INCLUDE[tsql_md](../../includes/tsql-md.md)] instrução que pode ser executada para corrigir o problema.

| type | descrição | DATETIME | score | detalhes | ... |
| --- | --- | --- | --- | --- | --- |
| `FORCE_LAST_GOOD_PLAN` | Tempo de CPU alterado de 4 ms para 14 MS | 3/17/2017 | 83 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |
| `FORCE_LAST_GOOD_PLAN` | Tempo de CPU alterado de 37 MS para 84 MS | 16/03/2017 | 26 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |

Algumas colunas dessa exibição são descritas na lista a seguir:
 - Tipo da ação recomendada-`FORCE_LAST_GOOD_PLAN`
 - Descrição que contém informações por que [!INCLUDE[ssde_md](../../includes/ssde_md.md)] o pensa que essa alteração de plano é uma regressão de desempenho potencial
 - DateTime quando a regressão potencial é detectada
 - Pontuação dessa recomendação
 - Detalhes sobre os problemas, como ID do plano detectado, ID do plano regressivo, ID do plano que deve ser forçado a corrigir o problema, [!INCLUDE[tsql_md](../../includes/tsql-md.md)] script que pode ser aplicado para corrigir o problema, etc. Os detalhes são armazenados no [formato JSON](../../relational-databases/json/index.md)

Use a consulta a seguir para obter um script que corrige o problema e informações adicionais sobre o lucro estimado:

```sql   
SELECT reason, score,
      script = JSON_VALUE(details, '$.implementationDetails.script'),
      planForceDetails.*,
      estimated_gain = (regressedPlanExecutionCount + recommendedPlanExecutionCount)
                  * (regressedPlanCpuTimeAverage - recommendedPlanCpuTimeAverage)/1000000,
      error_prone = IIF(regressedPlanErrorCount > recommendedPlanErrorCount, 'YES','NO')
FROM sys.dm_db_tuning_recommendations
CROSS APPLY OPENJSON (Details, '$.planForceDetails')
    WITH (  [query_id] int '$.queryId',
            regressedPlanId int '$.regressedPlanId',
            recommendedPlanId int '$.recommendedPlanId',
            regressedPlanErrorCount int,
            recommendedPlanErrorCount int,
            regressedPlanExecutionCount int,
            regressedPlanCpuTimeAverage float,
            recommendedPlanExecutionCount int,
            recommendedPlanCpuTimeAverage float
          ) AS planForceDetails;
```

[!INCLUDE[ssresult-md](../../includes/ssresult-md.md)]     

| reason | score | script | ID\_da consulta | ID do\_plano atual | ID do\_plano recomendado | lucro\_estimado | propenso a erros\_
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Tempo de CPU alterado de 3 ms para 46 MS | 36 | Repositório\_de\_consultas\_do SP\_exec forçar plano 12, 17; | 12 | 28 | 17 | 11,59 | 0

A coluna `estimated_gain` representa o número estimado de segundos que seria salvo se o plano recomendado fosse usado para execução de consulta em vez do plano atual. O plano recomendado deve ser forçado em vez do plano atual se o lucro for maior que 10 segundos. Se houver mais erros (por exemplo, tempos limite ou execuções anuladas) no plano atual do que no plano recomendado, a coluna `error_prone` será definida como o valor. `YES` Um plano propenso a erros é outro motivo pelo qual o plano recomendado deve ser forçado em vez do atual.

Embora o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] forneça todas as informações necessárias para identificar regressões de escolha de plano, o monitoramento contínuo e a correção de problemas de desempenho podem se tornar um processo entediante. O ajuste automático torna esse processo muito mais fácil.

> [!NOTE]
> Os dados na DMV sys. dm_db_tuning_recommendations não são persistidos entre as [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reinicializações da instância.

## <a name="automatic-index-management"></a>Gerenciamento de índice automático

No [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)], o gerenciamento de índice é [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] fácil porque aprende sobre sua carga de trabalho e garante que seus dados sejam sempre indexados de forma ideal. Um design de índice apropriado é crucial para otimizar o desempenho da carga de trabalho e o gerenciamento de índice automático pode ajudar a otimizar seus índices. O gerenciamento de índice automático pode corrigir problemas de desempenho em bancos de dados indexados incorretamente ou manter e aprimorar os índices no esquema de banco de dados existente. O ajuste automático [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] no executa as seguintes ações:

 - Identifica índices que podem melhorar o desempenho de suas [!INCLUDE[tsql_md](../../includes/tsql-md.md)] consultas que lêem dados das tabelas.
 - Identifica índices ou índices redundantes que não foram usados em um período de tempo maior que pode ser removido. A remoção de índices desnecessários melhora o desempenho das consultas que atualizam dados em tabelas.

### <a name="why-do-you-need-index-management"></a>Por que você precisa de gerenciamento de índice?

Os índices aceleram algumas de suas consultas que lêem dados das tabelas, no entanto, eles podem retardar as consultas que atualizam dados. Você precisa analisar cuidadosamente quando criar um índice e quais colunas você precisa incluir no índice. Alguns índices podem não ser mais necessários após algum tempo. Portanto, você precisaria identificar e descartar periodicamente esses índices que não trazem nenhum benefício. Se você ignorar os índices não utilizados, o desempenho das consultas que atualizar dados será reduzido sem nenhum benefício para as consultas que lêem dados. Índices não utilizados também afetam o desempenho geral do sistema porque atualizações adicionais precisam do log desnecessário.

Descobrir o conjunto ideal de índices que melhoram o desempenho das consultas de leitura de dados das tabelas e que tenham um impacto mínimo sobre as atualizações pode exigir uma análise contínua e complexa.

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]usa inteligência interna e regras avançadas que analisam suas consultas, identificam índices que seriam ideais para suas cargas de trabalho atuais e identificam os índices que talvez precisem ser removidos. O banco de dados SQL do Azure garante que você tenha um conjunto mínimo necessário de índices que otimizam as consultas que lêem dados, com impacto minimizado sobre as outras consultas.

### <a name="automatic-index-management"></a>Gerenciamento de índice automático

Além da detecção, [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] o pode aplicar automaticamente as recomendações identificadas. Se você achar que as regras internas melhoram o desempenho do banco de dados, você poderá permitir [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] que o gerencie automaticamente seus índices.

Para habilitar o ajuste automático [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] no e permitir que o recurso de ajuste automático gerencie totalmente sua carga de trabalho, consulte [habilitar o ajuste automático no banco de dados SQL do Azure usando portal do Azure](/azure/sql-database/sql-database-automatic-tuning-enable).

Quando o [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] aplica uma recomendação criar índice ou DROP INDEX, ele monitora automaticamente o desempenho das consultas afetadas pelo índice. O novo índice será retido somente se o desempenho das consultas afetadas for melhorado. O índice removido será recriado automaticamente se houver algumas consultas que são executadas mais lentamente devido à ausência do índice.

### <a name="automatic-index-management-considerations"></a>Considerações sobre o gerenciamento de índice automático

As ações necessárias para criar os índices [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] necessários no podem consumir recursos e afetar o desempenho da carga de trabalho de tempo temporal. Para minimizar o impacto da criação do índice no desempenho da [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] carga de trabalho, o localiza uma janela de tempo apropriada para qualquer operação de gerenciamento de índice. A ação de ajuste será adiada se o banco de dados precisar de recursos para executar a carga de trabalho e for reiniciado quando o banco de dados tiver recursos não utilizados suficientes que possam ser usados para a tarefa de manutenção. Um recurso importante no gerenciamento de índice automático é a verificação das ações. Quando [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] o cria ou descarta um índice, um processo de monitoramento analisa o desempenho de sua carga de trabalho para verificar se a ação melhorou o desempenho geral. Se ele não levasse um aprimoramento significativo, a ação é revertida imediatamente. Dessa forma, [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] o garante que as ações de ajuste automático não afetem negativamente o desempenho da carga de trabalho. Os índices criados com o ajuste automático são transparentes para a operação de manutenção no esquema subjacente. Alterações de esquema como remover ou renomear colunas não são bloqueadas pela presença de índices criados automaticamente. Os índices criados automaticamente pelo [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] são imediatamente descartados quando a tabela ou as colunas relacionadas são descartadas.

### <a name="alternative---manual-index-management"></a>Alternativa-gerenciamento de índice manual

Sem o gerenciamento automático de índice, um usuário ou DBA precisaria consultar manualmente a exibição de [&#41;sys. dm_db_missing_index_details &#40;Transact-SQL](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md) ou usar o relatório do [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] painel de desempenho no para localizar índices que possam melhorar o desempenho, criar índices usando os detalhes fornecidos nessa exibição e monitorar manualmente o desempenho da consulta. Para localizar os índices que devem ser descartados, os usuários devem monitorar as estatísticas de uso operacional dos índices para localizar índices raramente usados.

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]simplifica esse processo. [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]analisa sua carga de trabalho, identifica as consultas que poderiam ser executadas mais rapidamente com um novo índice e identifica índices não utilizados ou duplicados. Encontre mais informações sobre a identificação de índices que devem ser alterados em [Encontrar recomendações de índice no portal do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-advisor-portal).

## <a name="see-also"></a>Consulte Também  
 [ALTER DATABASE SET AUTOMATIC_TUNING &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [sys. database_automatic_tuning_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)  
 [sys. dm_db_tuning_recommendations &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)   
 [sys. dm_db_missing_index_details &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_query_store_force_plan](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)     
 [&#41;&#40;Transact-SQL de sp_query_store_unforce_plan](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)           
 [sys. database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [Funções JSON](../../relational-databases/json/index.md)    
 [Planos de execução](../../relational-databases/performance/execution-plans.md)    
 [Monitorar e ajustar o desempenho](../../relational-databases/performance/monitor-and-tune-for-performance.md)     
 [Ferramentas de monitoramento e ajuste de desempenho](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)     
 [Monitorando o desempenho com o repositório de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
 [Assistente de Ajuste de Consulta](../../relational-databases/performance/upgrade-dbcompat-using-qta.md)
