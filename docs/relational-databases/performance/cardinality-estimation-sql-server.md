---
title: Estimativa de cardinalidade (SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 09/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: performance
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cardinality estimator
- CE (cardinality estimator)
- estimating cardinality
ms.assetid: baa8a304-5713-4cfe-a699-345e819ce6df
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: b1c53b09fe118de3a90c78bd1393da90a915385b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="cardinality-estimation-sql-server"></a>Estimativa de cardinalidade (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  
Este artigo ilustra como você pode avaliar e escolher a melhor configuração de CE (estimativa de cardinalidade) para o sistema SQL. A maior parte dos sistemas se beneficia da CE mais recente, pois ela é a mais precisa. A CE prevê o número de linhas que sua consulta provavelmente retornará. A previsão de cardinalidade é usada pelo Otimizador de Consulta para gerar o plano de consulta ideal. Com estimativas mais precisas, o Otimizador de Consulta normalmente pode fazer um trabalho melhor de produção de um plano de consulta melhor.  
  
Provavelmente, seu sistema de aplicativos poderia ter uma consulta importante cujo plano é alterado para um plano mais lento devido à nova CE. Uma consulta desse tipo pode ser parecida com esta:  
  
- Uma consulta OLTP (processamento de transações online) executada com tanta frequência que várias instâncias dessa geralmente são executadas ao mesmo tempo.  
- SELECT com agregação significativa que é executado durante o horário comercial do OLTP.  
  
Você tem técnicas para identificar uma consulta que tem um desempenho mais lento com a nova CE. Além disso, você tem opções para resolver o problema de desempenho.  
  
  
## <a name="versions-of-the-ce"></a>Versões da CE  
  
 Em 1998, uma atualização importante da CE fazia parte do Microsoft SQL Server 7.0, para o qual o nível de compatibilidade era 70. Atualizações posteriores iniciadas com o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], significando níveis de compatibilidade 120 e acima. As atualizações da CE dos níveis 120 e acima incorporam suposições e algoritmos que funcionam bem em data warehousing moderno e em cargas de trabalho OLTP.  
  
 **Nível de compatibilidade:** você pode garantir que seu banco de dados está em determinado nível usando o seguinte código Transact-SQL para [COMPATIBILITY_LEVEL](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  

```tsql  
SELECT ServerProperty('ProductVersion');  
go  
  
ALTER DATABASE <yourDatabase>  
    SET COMPATIBILITY_LEVEL = 130;  
go  
  
SELECT d.name, d.compatibility_level  
    FROM sys.databases AS d  
    WHERE d.name = 'yourDatabase';  
go  
```  
  
 Para um banco de dados do SQL Server definido no nível de compatibilidade 120 ou acima, a ativação do [sinalizador de rastreamento 9481](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) força o sistema a usar o CE versão 70.  
  
 **CE herdada:** para um banco de dados do SQL Server definido no nível de compatibilidade 120 e acima, o CE versão 70 pode ser ativado usando o nível do banco de dados usando [ALTERAR A CONFIGURAÇÃO NO ESCOPO DO BANCO DE DADOS](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).
  
```tsql  
ALTER DATABASE
    SCOPED CONFIGURATION  
        SET LEGACY_CARDINALITY_ESTIMATION = ON;  
go  
  
SELECT name, value  
    FROM sys.database_scoped_configurations  
    WHERE name = 'LEGACY_CARDINALITY_ESTIMATION';  
```  
 
 Ou a partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1, o [Dica de Consulta](../../t-sql/queries/hints-transact-sql-query.md) `USE HINT ('FORCE_LEGACY_CARDINALITY_ESTIMATION')`.
 
 ```tsql  
SELECT CustomerId, OrderAddedDate  
    FROM OrderTable  
    WHERE OrderAddedDate >= '2016-05-01'; 
    OPTION (USE HINT ('FORCE_LEGACY_CARDINALITY_ESTIMATION'));  
```
 
 **Repositório de consultas:** a começar no [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], o repositório de consultas é uma ferramenta útil para examinar o desempenho de suas consultas. No [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)], no **Pesquisador de Objetos**, no nó do seu banco de dados, um nó **Repositório de Consultas** é exibido quando o repositório de consultas está habilitado.  
  
```tsql  
ALTER DATABASE <yourDatabase>  
    SET QUERY_STORE = ON;  
go  
  
SELECT  
        q.actual_state_desc AS [actual_state_desc-ofQueryStore],  
        q.desired_state_desc,  
        q.query_capture_mode_desc  
    FROM  
        sys.database_query_store_options  AS q;  
go  
  
ALTER DATABASE <yourDatabase>  
    SET QUERY_STORE CLEAR;  
```  
  
 > [!TIP] 
 > É recomendado instalar a versão mais recente do [Management Studio](http://msdn.microsoft.com/library/mt238290.aspx) e atualizá-lo com frequência.  
  
 Outra opção para acompanhar o processo de estimativa de cardinalidade é usar o evento estendido chamado **query_optimizer_estimate_cardinality**. O exemplo de código T-SQL a seguir é executado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ele grava um arquivo .xel em C:\Temp\ (embora o caminho possa ser alterado). Quando você abre o arquivo .xel no [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)], as informações detalhadas são exibidas de forma amigável.  
  
```tsql  
DROP EVENT SESSION Test_the_CE_qoec_1 ON SERVER;  
go  
  
CREATE EVENT SESSION Test_the_CE_qoec_1  
    ON SERVER  
    ADD EVENT sqlserver.query_optimizer_estimate_cardinality  
    (  
        ACTION (sqlserver.sql_text)  
            WHERE (  
                sql_text LIKE '%yourTable%'  
                and sql_text LIKE '%SUM(%'  
            )  
    )  
    ADD TARGET package0.asynchronous_file_target   
        (SET  
            filename = 'c:\temp\xe_qoec_1.xel',  
            metadatafile = 'c:\temp\xe_qoec_1.xem'  
        );  
go  
  
ALTER EVENT SESSION Test_the_CE_qoec_1  
    ON SERVER  
    STATE = START;  --STOP;  
go  
```  
  
 Para obter informações sobre eventos estendidos adaptados para o [!INCLUDE[ssSDS](../../includes/sssds-md.md)], veja [Eventos estendidos no Banco de Dados SQL](http://azure.microsoft.com/documentation/articles/sql-database-xevent-db-diff-from-svr/).  
  
  
## <a name="steps-to-assess-the-ce-version"></a>Etapas para avaliar a versão da CE  
  
 A seguir, veja as etapas que você pode usar para avaliar se qualquer uma das suas consultas mais importantes tem um desempenho inferior na CE mais recente. Algumas das etapas são realizadas com a execução de um exemplo de código apresentado em uma seção anterior.  
  
1.  Abra o [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)]. Verifique se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]banco de dados é definido como o mais alto nível de compatibilidade disponível.  
  
2.  Realize as seguintes etapas preliminares:  
  
    1.  Abra o [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)].  
  
    2.  Execute o T-SQL para garantir que o banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é definido com o nível de compatibilidade mais alto disponível.  
  
    3.  Verifique se o seu banco de dados tem a configuração `LEGACY_CARDINALITY_ESTIMATION` como OFF.  
  
    4.  LIMPE seu repositórios de consultas. É claro, verifique se seu repositório de consultas está ON.  
  
    5.  Execute a instrução: `SET NOCOUNT OFF;`  
  
3.  Execute a instrução: `SET STATISTICS XML ON;`  
  
4.  Execute a consulta importante.  
  
5.  No painel de resultados, na guia **Mensagens** , observe o número real de linhas afetadas.  
  
6.  No painel de resultados, na guia **Resultados** , clique duas vezes na célula que contém as estatísticas em formato XML. Um plano de consulta gráfico é exibido.  
  
7.  Clique com o botão direito do mouse na primeira caixa do plano de consulta gráfico e clique em **Propriedades**.  
  
8.  Para a comparação posterior com uma configuração diferente, observe os valores das seguintes propriedades:  
  
    -   **CardinalityEstimationModelVersion**.  
  
    -   **Número Estimado de Linhas**.  
  
    -   **Estimated I/O Cost**e várias propriedades *Estimated* semelhantes que envolvem o desempenho real em vez de previsões de contagem de linha.  
  
    -   **Operação Lógica** e **Operação Física**. *Parallelism* é um valor aceitável.  
  
    -   **Modo de Execução Real**. *Batch* é um valor aceitável, melhor que *Row*.  
  
9. Compare o número estimado de linhas com o número real de linhas. A CE não é precisa em % 1 (alto ou baixo) ou 10%?  
  
10. Execute: `SET STATISTICS XML OFF;`  
  
11. Execute o T-SQL para diminuir o nível de compatibilidade do banco de dados em um nível (por exemplo, 130 até 120).  
  
12. Execute novamente todas as etapas não preliminares.  
  
13. Compare os valores de propriedade da CE das duas execuções.  
  
    - O percentual de imprecisão na CE mais recente está abaixo da CE mais antiga?  
  
14. Por fim, compare vários valores de propriedade de desempenho das duas execuções.  
  
    -   Sua consulta usou um plano diferente nas duas estimativas de CE diferentes?  
  
    -   A consulta foi executada mais lentamente na CE mais recente?  
  
    -   A menos que a consulta tenha um desempenho melhor e com um plano diferente na CE mais antiga, certamente, será recomendável a CE mais recente.  
  
    -   No entanto, se sua consulta for executada com um plano mais rápido na CE mais antiga, considere forçar o sistema para usar o plano mais rápido e ignorar a CE. Dessa forma, você pode ter a CE mais recente para tudo, ao mesmo tempo que mantém o plano mais rápido por via das dúvidas.  
  
## <a name="how-to-activate-the-best-query-plan"></a>Como ativar o melhor plano de consulta  
  
Suponha que, com a nova CE, um plano de consulta mais lento seja gerado para sua consulta. Aqui estão algumas opções para ativar o plano mais rápido.  
  
Você pode definir o nível de compatibilidade de todo o seu banco de dados com um valor menor do que o valor mais recente disponível.  
  
- Isso ativa a CE herdada, mas faz com que todas as consultas fiquem sujeitas à CE antiga e menos precisa.  
  
- Além disso, a compatibilidade do nível anterior também perde excelente melhorias no otimizador de consultas.  
  
Você poderá usar `LEGACY_CARDINALITY_ESTIMATION` para fazer com que todo o banco de dados use a CE mais antiga ou apenas uma consulta específica, enquanto mantém as melhorias no otimizador de consulta.  
  
Para o controle mais refinado, você poderá *forçar* o sistema SQL a usar o plano gerado com a CE antiga durante o teste. Depois de *fixar* seu plano preferido, você poderá definir o banco de dados inteiro para usar o nível de compatibilidade e a CE mais recentes. A opção é elaborada a seguir.  
  
### <a name="how-to-force-a-particular-query-plan"></a>Como forçar um plano de consulta específico  
  
O repositório de consultas oferece diferentes maneiras pelas quais você pode forçar o sistema a usar um plano de consulta específico:  
  
- Execute **sp_query_store_force_plan**.  
  
- No [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)], expanda o nó **Repositório de Consultas**, clique com o botão direito do mouse em **Nós que Consomem Mais Recursos** e clique em **Exibir Nós que Consomem Mais Recursos**. A exibição mostra os botões rotulados **Forçar Plano** e **Não Forçar Plano**.  
  
 Para obter mais informações sobre o repositório de consultas, veja [Monitorando o desempenho com o repositório de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md).  
  
  
## <a name="examples-of-ce-improvements"></a>Exemplos de melhorias de CE  
  
Esta seção descreve consultas de exemplo que se beneficiam das melhorias implementadas na CE em versões recentes. Essas são as informações básicas que não exigem ação específica de sua parte.  
  
### <a name="example-a-ce-understands-maximum-value-might-be-higher-than-when-statistics-were-last-gathered"></a>Exemplo A. A CE entende que o valor máximo pode ser maior do que quando as estatísticas foram coletadas pela última vez  
  
Suponha que as estatísticas para OrderTable foram coletadas pela última vez em 30/04/2016, quando a OrderAddedDate máxima era 30/04/2016. A CE de nível de compatibilidade 120 (e para níveis mais altos) entende que as colunas em OrderTable que contêm dados *crescentes* podem ter valores maiores do que o máximo registrado pelas estatísticas. Essa compreensão melhora o plano de consulta para SQL SELECTs como a mostrada a seguir.  
  
```tsql  
SELECT CustomerId, OrderAddedDate  
    FROM OrderTable  
    WHERE OrderAddedDate >= '2016-05-01';  
```  
  
### <a name="example-b-ce-understands-that-filtered-predicates-on-the-same-table-are-often-correlated"></a>Exemplo B. A CE entende que os predicados filtrados na mesma tabela estão frequentemente correlacionados  
  
Na instrução SELECT a seguir, vemos predicados filtrados em Model e ModelVariant. Intuitivamente, entendemos que quando Model é 'Xbox' há uma possibilidade de ModelVariant ser 'One', uma vez que o Xbox tem uma variante chamada One.  
  
A CE de nível 120 entende que pode haver uma correlação entre as duas colunas na mesma tabela, Model e ModelVariant. A CE faz uma estimativa mais precisa de quantas linhas serão retornadas pela consulta, e o otimizador de consulta gera um plano melhor.  
  
```tsql  
SELECT Model, Purchase_Price  
    FROM dbo.Hardware  
    WHERE  
        Model  = 'Xbox'  AND  
        ModelVariant = 'One';  
```  
  
### <a name="example-c-ce-no-longer-assumes-any-correlation-between-filtered-predicates-from-different-tablescc"></a>Exemplo C. A CE não pressupõe mais nenhuma correlação entre os predicados filtrados de tabelas diferentes 
Com a nova e ampla pesquisa sobre cargas de trabalho modernas e dados corporativos reais, descobriu-se que, em geral, não há correlação entre os filtros de predicado de diferentes tabelas. Na consulta a seguir, a CE pressupõe que não há nenhuma correlação entre s.type e r.date. Portanto, a CE faz uma estimativa inferior do número de linhas retornadas.  
  
```tsql  
SELECT s.ticket, s.customer, r.store  
    FROM  
                   dbo.Sales    AS s  
        CROSS JOIN dbo.Returns  AS r  
    WHERE  
        s.ticket = r.ticket  AND  
        s.type   = 'toy'     AND  
        r.date   = '2016-05-11';  
```  
  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar e ajustar o desempenho](../../relational-databases/performance/monitor-and-tune-for-performance.md)  
  [Otimizar os planos de consulta com o avaliador de cardinalidade do SQL Server 2014](http://msdn.microsoft.com/library/dn673537.aspx)  
 [Dicas de consulta](../../t-sql/queries/hints-transact-sql-query.md)  
 [Monitorando o desempenho com o repositório de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
 [Guia de arquitetura de processamento de consultas](../../relational-databases/query-processing-architecture-guide.md)
