---
title: Estimativa de cardinalidade (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 11/24/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- cardinality estimator
- CE (cardinality estimator)
- estimating cardinality
ms.assetid: baa8a304-5713-4cfe-a699-345e819ce6df
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 393c4f88f9ab60f3a25ddaab5bb091fb298e1e02
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48200606"
---
# <a name="cardinality-estimation-sql-server"></a>Estimativa de cardinalidade (SQL Server)
  A lógica de estimativa de cardinalidade, chamada de avaliador de cardinalidade, foi reformulada no [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] para melhorar a qualidade dos planos de consulta e, portanto, para melhorar o desempenho da consulta. O novo avaliador de cardinalidade incorpora as suposições e os algoritmos que funcionam bem em OLTP moderno e em cargas de trabalho de data warehouse. Ele se baseia na pesquisa detalhada da estimativa de cardinalidade em cargas de trabalho modernas, bem como em nosso aprendizado nos últimos 15 anos de aperfeiçoamento do avaliador de cardinalidade do SQL Server. Os comentários dos clientes mostram que, apesar de a maioria das consultas se beneficiarem da alteração ou permanecerem inalteradas, poucas mostram regressões em comparação ao avaliador de cardinalidade anterior.  
  
> [!NOTE]  
>  As estimativas de cardinalidade são uma previsão do número de linhas no resultado da consulta. O otimizador de consulta usa essas estimativas para escolher um plano para executar a consulta. A qualidade do plano de consulta tem um impacto direto sobre a melhoria no desempenho da consulta.  
  
## <a name="performance-testing-and-tuning-recommendations"></a>Teste de desempenho e recomendações de ajuste  
 O novo avaliador de cardinalidade é habilitado para todos os novos bancos de dados criados no [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]. Porém, a atualização para o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] não habilita o novo avaliador de cardinalidade em bancos de dados existentes.  
  
 Para garantir um melhor desempenho de consulta, use essas recomendações para testar sua carga de trabalho com o novo avaliador de cardinalidade antes de habilitá-lo em seu sistema de produção.  
  
1.  Atualize todos os bancos de dados existentes para usar o novo avaliador de cardinalidade. Para fazer isso, use [nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41; ](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level) para definir o nível de compatibilidade do banco de dados como 120.  
  
2.  Execute sua carga de trabalho de teste com o novo avaliador de cardinalidade e, em seguida, solucione qualquer novo problema de desempenho da mesma forma que soluciona os problemas de desempenho atuais.  
  
3.  Quando sua carga de trabalho está em execução com o novo avaliador de cardinalidade (nível de compatibilidade de banco de dados (SQL Server 2014) de 120), e uma consulta específica já foi retornada, você pode executar a consulta com o sinalizador de rastreamento 9481 para usar a versão do avaliador de cardinalidade usado em [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]e versões anteriores. Para executar uma consulta com um sinalizador de rastreamento, consulte o artigo de banco de dados [Habilitar o comportamento do otimizador de consulta do SQL Server que afeta o plano e pode ser controlado por diferentes sinalizadores de rastreamento em um nível de consulta específico](http://support.microsoft.com/kb/2801413)  
  
4.  Se você não pode alterar todos os bancos de dados ao mesmo tempo, para usar o novo avaliador de cardinalidade, você pode usar o avaliador de cardinalidade anterior para todos os bancos de dados usando [nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41; ](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level) para Defina o nível de compatibilidade do banco de dados como 110.  
  
5.  Se a carga de trabalho está em execução com o nível de compatibilidade 110 do banco de dados, e você deseja testar ou executar uma consulta específica com o novo avaliador de cardinalidade, pode executar a consulta com o sinalizador de rastreamento 2312 para usar a versão 2014 do SQL Server do avaliador de cardinalidade.  Para executar uma consulta com um sinalizador de rastreamento, consulte o artigo de banco de dados [Habilitar o comportamento do otimizador de consulta do SQL Server que afeta o plano e pode ser controlado por diferentes sinalizadores de rastreamento em um nível de consulta específico](http://support.microsoft.com/kb/2801413)  
  
## <a name="new-xevents"></a>Novos XEvents  
 Há dois novos XEvents query_optimizer_estimate_cardinality para dar suporte aos novos planos de consulta.  
  
-   *query_optimizer_estimate_cardinality* ocorre quando o otimizador de consulta calcula a cardinalidade em uma expressão relacional.  
  
-   *query_optimizer_force_both_cardinality_estimation*_behaviors ocorre quando ambos os sinalizadores de rastreamento 2312 e 9481 estão habilitados, tentando forçar ao mesmo tempo os comportamentos anterior e novo da estimativa de cardinalidade.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir mostram algumas das alterações nas novas estimativas de cardinalidade. O código para calcular a cardinalidade foi recriado. A lógica é complexa e não é possível fornecer uma lista completa de todas as alterações.  
  
> [!NOTE]  
>  Esses exemplos são fornecidos como informações conceituais. Nenhuma ação é necessária de sua parte para alterar o modo como cria bancos de dados e consultas.  
  
### <a name="example-a-new-cardinality-estimates-use-an-average-cardinality-for-recently-added-ascending-data"></a>Exemplo A. As novas estimativas de cardinalidade usam uma cardinalidade média dos dados mais recentes em ordem crescente  
 Este exemplo demonstra como o novo avaliador de cardinalidade pode melhorar estimativas de cardinalidade para dados em ordem crescente que excedem o valor máximo na tabela durante a atualização das estatísticas mais recentes.  
  
```  
SELECT item, category, amount FROM dbo.Sales AS s WHERE Date = '2013-12-19';  
```  
  
 Neste exemplo, novas linhas são adicionadas à tabela Sales diariamente, a consulta solicita vendas ocorridas em 19/12/2013, e as estatísticas foram atualizadas pela última vez em 18/12/2013. O avaliador de cardinalidade anterior supõe que os valores de 19/12/2013 não existem, pois a data excede a data máxima e as estatísticas não foram atualizadas para incluir os valores de 19/12/2013. Essa situação, conhecida como o problema de chave crescente, ocorrerá se você carregar dados durante o dia e, depois, executar consultas nos dados antes da atualização de estatísticas.  
  
 Esse comportamento foi alterado. Agora, mesmo se as estatísticas não foram atualizadas para os dados mais recentes em ordem crescente, adicionados desde a última atualização das estatísticas, o novo avaliador de cardinalidade suporá que os valores existem e usará a cardinalidade média para cada valor na coluna como a estimativa de cardinalidade.  
  
### <a name="example-b-new-cardinality-estimates-assume-filtered-predicates-on-the-same-table-have-some-correlation"></a>Exemplo B. As novas estimativas de cardinalidade consideram que predicados filtrados na mesma tabela têm alguma correlação  
 Para este exemplo, suponha que a tabela Cars tem 1000 linhas, Make tem 200 correspondências para 'Honda”, Model tem 50 correspondências para 'Civic', e que todos os carros Civic são Honda. Consequentemente, 20% dos valores na coluna Make são 'Honda', 5% dos valores na coluna Model são 'Civic', e o número real de carros Civic da Honda é 50. As estimativas de cardinalidade anteriores consideram que os valores nas colunas Make e Model são independentes. O otimizador de consulta anterior estima há 10 Civic da Honda (.05 *.20 \* 1000 linhas = 10 linhas).  
  
```  
SELECT year, purchase_price FROM dbo.Cars WHERE Make = 'Honda' AND Model = 'Civic';  
```  
  
 Esse comportamento foi alterado. Agora, as novas estimativas de cardinalidade supõem que as colunas Make e Model têm *alguma* correlação. O otimizador de consulta calcula uma cardinalidade superior, adicionando um componente exponencial à equação de avaliação. O otimizador de consulta agora calcula que 22,36 linhas (.05 * SQRT(.20) \* 1000 linhas = 22,36 linhas) correspondem ao predicado. Para este cenário e a distribuição de dados específica, o valor de 22,36 linhas está mais próximo de 50 linhas reais que a consulta retornará.  
  
 Observe que a nova lógica do avaliador de cardinalidade classifica as seletividades de predicado e aumenta o expoente. Por exemplo, se as seletividades de predicado eram.05,.20 e.25, a estimativa de cardinalidade seria (.05 * SQRT(.20) \* SQRT(SQRT(.25))).  
  
### <a name="example-c-new-cardinality-estimates-assume-filtered-predicates-on-different-tables-are-independent"></a>Exemplo C. As novas estimativas de cardinalidade supõem que predicados filtrados em tabelas diferentes são independentes  
 Para este exemplo, o avaliador de cardinalidade anterior considera que os filtros de predicado s.type e r.date estão correlacionados. No entanto, os resultados de testes em cargas de trabalho modernas mostraram que os filtros de predicado em colunas em tabelas diferentes não costumam estar correlacionados.  
  
```  
SELECT s.ticket, s.customer, r.store FROM dbo.Sales AS s CROSS JOIN dbo.Returns AS r  
WHERE s.ticket = r.ticket AND s.type = 'toy' AND r.date = '2013-12-19';  
```  
  
 Esse comportamento foi alterado. Agora, a nova lógica de avaliador de cardinalidade supõe que s.type não está correlacionado com r.date. Em termos práticos, a suposição é que toys são retornados diariamente, e não apenas em um dia específico. Neste caso, o valor das novas estimativas de cardinalidade será menor do que o das estimativas de cardinalidade anteriores.  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar e ajustar o desempenho](monitor-and-tune-for-performance.md)  
  
  
