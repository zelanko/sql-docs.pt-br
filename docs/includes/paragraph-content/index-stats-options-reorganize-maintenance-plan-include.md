

### <a name="index-stats-options"></a>Opções de estatísticas de índice

<!--
This includes/paragraph-content/ file was created when processing vsts sqlbuvsts01 2999014 (5589131).  genemi  2017-07-21

Initially used in:
- relational-databases/maintenance-plans/rebuild-index-task-maintenance-plan.md
- relational-databases/maintenance-plans/reorganize-index-task-maintenance-plan.md
-->


Em versões anteriores do Microsoft SQL Server, isso poderia causar lentidão de sistema para reorganizar ou recompilar um índice grande. O SQL Server 2016 implementou aprimoramentos de desempenho importantes para essas operações de índice.

Além disso, em versões anteriores, a granularidade do controle era menos refinada. Isso fazia com que o sistema reorganizasse ou recompilasse alguns índices, mesmo quando os índices não estavam muito fragmentados, o que era desnecessário. Controles mais recentes na interface do usuário (UI) do Plano de Manutenção permitem a exclusão de índices que não precisam ser atualizados, com base em critérios de estatísticas de índice. Para isso, as seguintes exibições de gerenciamento dinâmico (DMVs) de Transact-SQL são usadas internamente:


- [sys.dm_db_index_usage_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)
- [sys.dm_db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)


 **Tipo de exame**  
 O sistema deve consumir recursos para coletar estatísticas de índice. Você pode escolher entre consumir relativamente menos ou mais recursos dependendo de quanta precisão você considera necessária para as estatísticas de índice. A interface do usuário oferece a seguinte lista de níveis de precisão para sua escolha:


- Rápido
- Amostra
- Detalhado


 **Otimize o índice somente se:**  
 A interface do usuário oferecer os seguintes filtros ajustáveis, que você pode usar para evitar a atualização de índices que ainda não precisam de atualizações:


- Fragmentação &gt; *(%)*
- Contagem de páginas &gt;
- Usado nos últimos *(dias)*

