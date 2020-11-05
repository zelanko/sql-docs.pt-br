---
description: Validação pós-migração e guia de otimização
title: Validação pós-migração e guia de otimização | Microsoft Docs
ms.date: 01/09/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- post-migration validation and optimization
- guide, post-migration validation and optimization
ms.assetid: 11f8017e-5bc3-4bab-8060-c16282cfbac1
author: pelopes
ms.author: harinid
ms.openlocfilehash: 01b629b65c7f8ab1571aa53a944a8525bd09a0b0
ms.sourcegitcommit: 442fbe1655d629ecef273b02fae1beb2455a762e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93235444"
---
# <a name="post-migration-validation-and-optimization-guide"></a>Validação pós-migração e guia de otimização

[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

A etapa pós-migração do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] é crucial para reconciliar a precisão e a integridade dos dados, bem como descobrir problemas de desempenho com a carga de trabalho.

## <a name="common-performance-scenarios"></a>Cenários comuns de desempenho

Abaixo estão alguns dos cenários comuns de desempenho encontrados após a migração para a plataforma [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e como resolvê-los. Isso inclui cenários que são específicos para migração de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (versões mais antigas para versões mais recentes), bem como migração de plataforma externa (como Oracle, DB2, MySQL e Sybase) para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

## <a name="query-regressions-due-to-change-in-ce-version"></a><a name="CEUpgrade"></a> Regressões de consulta devido à alteração na versão CE

**Aplica-se a: migração de** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

Ao migrar de versões mais antigas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] ou mais recente e atualizar o [nível de compatibilidade do banco de dados](../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md) para o mais recente disponível, uma carga de trabalho poderá ser exposta ao risco de regressão de desempenho.

Isso ocorre porque, começando com o [!INCLUDE[ssSQL14](../includes/sssql14-md.md)], todas as alterações do Otimizador de Consulta são associadas para o [nível de compatibilidade do banco de dados](../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md) mais recente, portanto, os planos não são alterados diretamente no ponto de atualização, mas sim quando um usuário altera a opção de banco de dados `COMPATIBILITY_LEVEL` para a mais recente. Esse recurso, em combinação com o Repositório de Consultas, fornece um excelente nível de controle sobre o desempenho da consulta no processo de atualização. 

Para obter mais informações sobre as alterações do Otimizador de Consulta introduzidas no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)], consulte [Otimizando seus planos de consulta com o estimador de cardinalidade do SQL Server 2014](/previous-versions/dn673537(v=msdn.10)).

### <a name="steps-to-resolve"></a>Etapas para resolver

Altere o [nível de compatibilidade do banco de dados](../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md) para a versão de origem e siga o fluxo de trabalho de atualização recomendado conforme mostrado na figura a seguir:

![Diagrama que mostra o fluxo de trabalho de atualização recomendado.](../relational-databases/performance/media/query-store-usage-5.png "query-store-usage-5")  

Para obter mais informações sobre este tópico, consulte [Manter a estabilidade do desempenho durante a atualização para a versão mais recente do SQL Server](../relational-databases/performance/query-store-usage-scenarios.md#CEUpgrade).

## <a name="sensitivity-to-parameter-sniffing"></a>Sensibilidade do <a name="ParameterSniffing"></a> à detecção de parâmetros

**Aplica-se a:** migração de plataforma externa (como Oracle, DB2, MySQL e Sybase) para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

> [!NOTE]
> Para migrações de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], se esse problema existe na origem de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], migrar para uma versão mais recente do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no estado em que se encontra não resolverá esse cenário. 

O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] compila os planos de consulta em procedimentos armazenados usando a detecção de parâmetros de entrada na primeira compilação, gerando um plano parametrizado, reutilizável e otimizado para distribuição de dados de entrada. Mesmo se não forem procedimentos armazenados, a maioria das instruções que gera planos triviais será parametrizada. Depois que o primeiro plano é armazenado em cache, qualquer execução futura é mapeada para um plano previamente armazenado em cache.
Um possível problema surge quando essa primeira compilação pode não ter usado os conjuntos de parâmetros mais comuns para a carga de trabalho normal. Para parâmetros diferentes, o mesmo plano de execução se torna ineficaz. Para obter mais informações sobre este tópico, consulte [Detecção de parâmetro](../relational-databases/query-processing-architecture-guide.md#ParamSniffing).

### <a name="steps-to-resolve"></a>Etapas para resolver

1.  Use a dica `RECOMPILE`. Um plano é calculado toda vez e adaptado para cada valor de parâmetro.
2.  Reescreva o procedimento armazenado para usar a opção `(OPTIMIZE FOR(<input parameter> = <value>))`. Decida qual valor deve ser usado para adaptar-se à carga de trabalho mais relevante, criar e manter um plano que se torna eficiente para o valor parametrizado.
3.  Reescreva o procedimento armazenado usando uma variável local dentro do procedimento. Agora o otimizador usa o vetor de densidade para estimativas, resultando no mesmo plano independentemente do valor do parâmetro.
4.  Reescreva o procedimento armazenado para usar a opção `(OPTIMIZE FOR UNKNOWN)`. Mesmo efeito que usar a técnica de variável local.
5.  Reescreva a consulta para usar a dica `DISABLE_PARAMETER_SNIFFING`. Mesmo efeito de usar a técnica de variável local desabilitando totalmente a detecção de parâmetros, exceto se `OPTION(RECOMPILE)`, `WITH RECOMPILE` ou `OPTIMIZE FOR <value>` for usado.

> [!TIP] 
> Aproveite o recurso de Análise de Plano do [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] para identificar rapidamente se isso é um problema. Mais informações estão disponíveis [aqui](/archive/blogs/sql_server_team/new-in-ssms-query-performance-troubleshooting-made-easier).

## <a name="missing-indexes"></a>Índices ausentes do <a name="MissingIndexes"></a>

**Aplica-se a:** migração de plataforma externa (por exemplo, Oracle, DB2, MySQL e Sybase) e [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

Índices ausentes ou incorretos causam E/S extra, o que leva a uso de memória extra e desperdício de CPU. Isso pode ser devido a uma alteração do perfil de carga de trabalho usando predicados diferentes, invalidando o design de índice existente. Evidência de uma estratégia de indexação ineficaz ou de alterações no perfil de carga de trabalho incluem:
-   Procure índices duplicados, redundantes, raramente usados ou nunca utilizados.
-   Tenha cuidado especial com índices não utilizados com atualizações.

### <a name="steps-to-resolve"></a>Etapas para resolver

1.  Aproveite o plano de execução gráfica para todas as referências de índice ausentes.
2.  Sugestões de indexação geradas pelo [Orientador de Otimização do Mecanismo de Banco de Dados](../tools/dta/tutorial-database-engine-tuning-advisor.md).
3.  Aproveite o [DMV de índices ausentes](../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md) ou por meio do [Painel de Desempenho do SQL Server](https://www.microsoft.com/download/details.aspx?id=29063).
4.  Utilize scripts pré-existentes que podem usar DMVs existentes para fornecer insights sobre qualquer índice ausente, duplicado, redundante, raramente usado e nunca utilizado, mas também se alguma referência de índice é sugerida/embutida no código em procedimentos existentes e funções no banco de dados. 

> [!TIP] 
> Exemplos de tais scripts pré-existentes incluem [Criação de Índice](https://github.com/Microsoft/tigertoolbox/tree/master/Index-Creation) e [Informações de Índice](https://github.com/Microsoft/tigertoolbox/tree/master/Index-Information). 

## <a name="inability-to-use-predicates-to-filter-data"></a>Impossibilidade do <a name="InabilityPredicates"></a> para usar predicados para filtrar dados

**Aplica-se a:** migração de plataforma externa (por exemplo, Oracle, DB2, MySQL e Sybase) e [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

> [!NOTE]
> Para migrações de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], se esse problema existe na origem de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], migrar para uma versão mais recente do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no estado em que se encontra não resolverá esse cenário.

O Otimizador de Consulta do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode considerar apenas informações que são conhecidas no tempo de compilação. Se uma carga de trabalho se baseia em predicados que podem ser conhecidos apenas no tempo de execução, a possibilidade de escolher um plano ineficaz aumenta. Para um plano de melhor qualidade, os predicados devem ser **SARGable** ou **S** earch **Arg** ument **able** (argumentos pesquisáveis).

Alguns exemplos de predicados não SARGable:
-   Conversões implícitas de dados, como VARCHAR para NVARCHAR ou INT para VARCHAR. Procure os avisos de CONVERT_IMPLICIT de runtime nos Planos de Execução Reais. Converter de um tipo para outro também pode causar perda de precisão.
-   Expressões complexas indeterminadas como `WHERE UnitPrice + 1 < 3.975`, mas não `WHERE UnitPrice < 320 * 200 * 32`.
-   Expressões que usam funções, como `WHERE ABS(ProductID) = 771` ou `WHERE UPPER(LastName) = 'Smith'`
-   Cadeias de caracteres com um caractere curinga à esquerda como `WHERE LastName LIKE '%Smith'`, mas não `WHERE LastName LIKE 'Smith%'`.

### <a name="steps-to-resolve"></a>Etapas para resolver

1. Sempre declare variáveis/parâmetros como o [tipo de dados](../t-sql/data-types/data-types-transact-sql.md) de destino pretendido. 
  -   Isso pode envolver a comparação de qualquer constructo de código definido pelo usuário que é armazenada no banco de dados (como procedimentos armazenados, funções definidas pelo usuário ou exibições) com tabelas do sistema que contém informações sobre os tipos de dados usados nas tabelas subjacentes (como [sys.columns](../relational-databases/system-catalog-views/sys-columns-transact-sql.md)).
2. Se não for possível percorrer todo o código até o ponto anterior, para a mesma finalidade, altere o tipo de dados na tabela para corresponder a qualquer declaração de variável/parâmetro.
3. Pondere a utilidade das construções a seguir:

  -   Funções que estão sendo usadas como predicados;
  -   Pesquisas com curinga;
  -   Expressões complexas baseadas em dados de coluna – avalie a necessidade de criar colunas computadas persistentes que possam ser indexadas;

> [!NOTE] 
> Todas as opções acima podem ser feitas programaticamente.

## <a name="use-of-table-valued-functions-multi-statement-vs-inline"></a>Uso do <a name="TableValuedFunctions"></a> de funções com valor de tabela (várias instruções vs embutido)

**Aplica-se a:** migração de plataforma externa (por exemplo, Oracle, DB2, MySQL e Sybase) e [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

> [!NOTE]
> Para migrações de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], se esse problema existe na origem de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], migrar para uma versão mais recente do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no estado em que se encontra não resolverá esse cenário.

Funções com valor de tabela retornam um tipo de dados de tabela que pode ser uma alternativa a exibições. Enquanto as exibições são limitadas a uma única instrução `SELECT`, funções definidas pelo usuário podem conter instruções adicionais que permitem mais lógica que é possível nas exibições.

> [!IMPORTANT] 
> Como a tabela de saída de um MSTVF (função com valor de tabela de várias instruções) não é criada no tempo de compilação, o Otimizador de Consulta do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] conta com heurística e não estatísticas reais, para determinar as estimativas de linha. Mesmo se os índices forem adicionados às tabelas, isso não vai ajudar. Para MSTVFs, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa uma estimativa fixa de 1 para o número de linhas esperado a ser retornado por um MSTVF (a partir do [!INCLUDE[ssSQL14](../includes/sssql14-md.md)], essa estimativa é fixa em 100 linhas).

### <a name="steps-to-resolve"></a>Etapas para resolver

1.  Se a TVF de várias instruções tiver somente uma instrução, converta-a em TVF embutida.

    ```sql
    CREATE FUNCTION dbo.tfnGetRecentAddress(@ID int)
    RETURNS @tblAddress TABLE
    ([Address] VARCHAR(60) NOT NULL)
    AS
    BEGIN
      INSERT INTO @tblAddress ([Address])
      SELECT TOP 1 [AddressLine1]
      FROM [Person].[Address]
      WHERE  AddressID = @ID
      ORDER BY [ModifiedDate] DESC
    RETURN
    END
    ```

    O exemplo de formato em linha é exibido a seguir.

    ```sql
    CREATE FUNCTION dbo.tfnGetRecentAddress_inline(@ID int)
    RETURNS TABLE
    AS
    RETURN (
      SELECT TOP 1 [AddressLine1] AS [Address]
      FROM [Person].[Address]
      WHERE  AddressID = @ID
      ORDER BY [ModifiedDate] DESC
    )
    ```

2.  Se for mais complexa, considere usar os resultados intermediários armazenados em tabelas com otimização de memória ou tabelas temporárias.

##  <a name="additional-reading"></a><a name="Additional_Reading"></a> Leitura adicional

 [Melhor prática com o Repositório de Consultas](../relational-databases/performance/best-practice-with-the-query-store.md)  
[Memory-Optimized Tables](./in-memory-oltp/sample-database-for-in-memory-oltp.md)  
[Funções definidas pelo usuário](../relational-databases/user-defined-functions/user-defined-functions.md)  
[Variáveis de tabela e estimativas de linha — Parte 1](/archive/blogs/blogdoezequiel/table-variables-and-row-estimations-part-1)  
[Variáveis de tabela e estimativas de linha — Parte 2](/archive/blogs/blogdoezequiel/table-variables-and-row-estimations-part-2)  
[Reutilização e armazenamento em cache do plano de execução](../relational-databases/query-processing-architecture-guide.md#execution-plan-caching-and-reuse)