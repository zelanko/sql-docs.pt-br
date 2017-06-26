---
title: "Validação após a migração e guia de otimização | Microsoft Docs"
ms.custom: 
ms.date: 5/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- post-migration validation and optimization
- guide, post-migration validation and optimization
ms.assetid: 11f8017e-5bc3-4bab-8060-c16282cfbac1
caps.latest.revision: 3
author: pelopes
ms.author: harinid
manager: 
ms.translationtype: Human Translation
ms.sourcegitcommit: dcbeda6b8372b358b6497f78d6139cad91c8097c
ms.openlocfilehash: 30a271511fff2d9c3c9eab73a0d118bfb3f8130d
ms.contentlocale: pt-br
ms.lasthandoff: 06/23/2017

---
# <a name="post-migration-validation-and-optimization-guide"></a>Validação após a migração e guia de otimização
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]POST etapas da migração é crucial para reconciliar qualquer precisão de dados e integridade, bem como descobrir problemas de desempenho com a carga de trabalho.

# <a name="common-performance-scenarios"></a>Cenários comuns de desempenho 
Abaixo estão alguns dos cenários comuns de desempenho encontrados após a migração para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] plataforma e como resolvê-los. Isso inclui cenários que são específicos para migração de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (versões mais antigas para versões mais recentes), bem como migração de plataforma externa (como Oracle, DB2, MySQL e Sybase) para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

## <a name="CEUpgrade"></a> Regressões de consulta devido a alteração em versão da CE

**Aplica-se a:** migração de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

Ao migrar de versões mais antigas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] ou mais recente e atualizar o [nível de compatibilidade do banco de dados](../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md) para o mais recente, uma carga de trabalho poderá ser exposta ao risco de regressão de desempenho.

Isso ocorre porque, começando com o [!INCLUDE[ssSQL14](../includes/sssql14-md.md)], todas as alterações do Otimizador de Consulta são associadas para o [nível de compatibilidade do banco de dados](../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md) mais recente, portanto, os planos não são alterados diretamente no ponto de atualização, mas sim quando um usuário altera a opção de banco de dados `COMPATIBILITY_LEVEL` para a mais recente. Esse recurso, em combinação com o Repositório de Consultas, fornece um excelente nível de controle sobre o desempenho da consulta no processo de atualização. 

Para obter mais informações sobre as alterações do Otimizador de Consulta introduzidas no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)], consulte [Otimizando seus planos de consulta com o estimador de cardinalidade do SQL Server 2014](http://msdn.microsoft.com/library/dn673537.aspx).

### <a name="steps-to-resolve"></a>Etapas para resolver

Altere o [nível de compatibilidade do banco de dados](../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md) para a versão de origem e siga o fluxo de trabalho de atualização recomendado conforme mostrado na figura a seguir:

![query-store-usage-5](../relational-databases/performance/media/query-store-usage-5.png "query-store-usage-5")  

Para obter mais informações sobre este tópico, consulte [Manter a estabilidade do desempenho durante a atualização para a versão mais recente do SQL Server](../relational-databases/performance/query-store-usage-scenarios.md#CEUpgrade).

## <a name="ParameterSniffing"></a>Sensibilidade a detecção de parâmetro

**Aplica-se a:** plataforma externa (por exemplo, Oracle, DB2, MySQL e Sybase) para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] migração.

> [!NOTE]
> Para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] migrações, se esse problema existe na origem [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], migrando para uma versão mais recente do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] como-será não abordar esse cenário. 

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]compila os planos de consulta em procedimentos armazenados usando a detecção de parâmetros de entrada em que a primeira compilação, gerando um plano com parâmetros e reutilizável, otimizado para distribuição de dados de entrada. Mesmo se os procedimentos armazenados não, a maioria das instruções que geram planos triviais serão parametrizadas. Depois que o primeiro é armazenado em cache um plano, qualquer execução futura é mapeado para um plano armazenado em cache anteriormente.
Um possível problema surge quando essa primeira compilação pode não ter usado os mais comuns conjuntos de parâmetros para a carga de trabalho normal. Para parâmetros diferentes, o mesmo plano de execução se torna ineficiente. Para obter mais informações sobre este tópico, consulte [Detecção de parâmetro](../relational-databases/query-processing-architecture-guide.md#ParamSniffing).

### <a name="steps-to-resolve"></a>Etapas para resolver

1.  Use o `RECOMPILE` dica. Um plano é calculado sempre adaptada para cada valor de parâmetro.
2.  Reescreva o procedimento armazenado para usar a opção `(OPTIMIZE FOR(<input parameter> = <value>))`. Decida qual valor usar que se adapta à maioria da carga de trabalho relevantes, criar e manter um plano que se torna eficiente para o valor com parâmetros.
3.  Reescreva o procedimento armazenado usando uma variável local dentro do procedimento. Agora que o otimizador usa o vetor de densidade para estimativas, resultando no mesmo plano, independentemente do valor do parâmetro.
4.  Reescreva o procedimento armazenado para usar a opção `(OPTIMIZE FOR UNKNOWN)`. Mesmo efeito que usar a técnica de variável local.
5.  Reescreva a consulta para usar a dica `DISABLE_PARAMETER_SNIFFING`. Mesmo efeito que usar a técnica de variável local por totalmente desabilitar a detecção de parâmetro, a menos que `OPTION(RECOMPILE)`, `WITH RECOMPILE` ou `OPTIMIZE FOR <value>` é usado.

> [!TIP] 
> Aproveite o [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] recurso de análise de plano para identificar rapidamente se esse for um problema. Mais informações disponíveis [aqui](https://blogs.msdn.microsoft.com/sql_server_team/new-in-ssms-query-performance-troubleshooting-made-easier/).

## <a name="MissingIndexes"></a>Índices ausentes

**Aplica-se a:** plataforma externa (por exemplo, Oracle, DB2, MySQL e Sybase) e [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] migração.

Índices ausentes ou incorretos faz com que o extra e/s que leva a memória extra e a CPU seja desperdiçada. Isso pode ser porque o perfil de carga de trabalho foi alterada como o uso de predicados diferentes, invalidando existente índice design. Evidência de uma estratégia de indexação ruim ou alterações no perfil de carga de trabalho incluem:
-   Procure duplicata, redundante, raramente usado e índices não utilizados completamente.
-   Cuidado especial com índices não utilizados com atualizações.

### <a name="steps-to-resolve"></a>Etapas para resolver

1.  Aproveite o plano de execução gráfica para todas as referências de índice ausente.
2.  Indexação sugestões gerados por [orientador de otimização do mecanismo de banco de dados](../tools/dta/tutorial-database-engine-tuning-advisor.md).
3.  Aproveite o [DMV de índices ausentes](../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md) ou por meio de [painel de desempenho do SQL Server](https://www.microsoft.com/en-us/download/details.aspx?id=29063).
4.  Utilize scripts pré-existentes que podem usar DMVs existentes para fornecer informações sobre qualquer índice ausente, duplicado, redundante, raramente utilizado e completamente não utilizado, mas também se qualquer referência de índice é sugerido/hard-coded em procedimentos existentes e funções no banco de dados. 

> [!TIP] 
> Exemplos de tais scripts pré-existentes [criação de índice](https://github.com/Microsoft/tigertoolbox/tree/master/Index-Creation) e [informações de índice](https://github.com/Microsoft/tigertoolbox/tree/master/Index-Information). 

## <a name="InabilityPredicates"></a>Predicados dificuldades para usar para filtrar dados

**Aplica-se a:** plataforma externa (por exemplo, Oracle, DB2, MySQL e Sybase) e [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] migração.

> [!NOTE]
> Para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] migrações, se esse problema existe na origem [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], migrando para uma versão mais recente do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] como-será não abordar esse cenário.

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Otimizador de consulta pode considera apenas informações que são conhecidas em tempo de compilação. Se uma carga de trabalho se baseia em predicados que podem ser conhecidos apenas em tempo de execução, aumenta a possibilidade de uma opção de plano ruim. Para um plano de melhor qualidade, os predicados devem ser **SARGable**, ou **S**pesquisar **Arg**umento**capaz de**.

Alguns exemplos de predicados de não-SARGable:
-   Conversões implícitas de dados, como VARCHAR para NVARCHAR ou INT para VARCHAR. Procure os avisos de CONVERT_IMPLICIT de tempo de execução em planos de execução real. Converter de um tipo para outro, também pode causar perda de precisão.
-   Expressões complexas de indeterminada, como `WHERE UnitPrice + 1 < 3.975`, mas não `WHERE UnitPrice < 320 * 200 * 32`.
-   Expressões que usam funções, como `WHERE ABS(ProductID) = 771` ou`WHERE UPPER(LastName) = 'Smith'`
-   Cadeias de caracteres com um caractere curinga à esquerda, como `WHERE LastName LIKE '%Smith'`, mas não `WHERE LastName LIKE 'Smith%'`.

### <a name="steps-to-resolve"></a>Etapas para resolver

1. Sempre declarar variáveis/parâmetros como o destino pretendido [tipo de dados](../t-sql/data-types/data-types-transact-sql.md). 
  -   Isso pode envolver a comparar qualquer construção de código definido pelo usuário que é armazenada no banco de dados (como procedimentos armazenados, funções definidas pelo usuário ou exibições) com tabelas do sistema que armazenam informações sobre os tipos de dados usados nas tabelas subjacentes (como [Columns](../relational-databases/system-catalog-views/sys-columns-transact-sql.md)).
2. Se não for possível percorrer todo o código para o ponto anterior, para a mesma finalidade, altere o tipo de dados na tabela para corresponder a qualquer declaração de variável/parâmetro.
3. Motivo out a utilidade das construções a seguir:
  -   Funções que estão sendo usadas como predicados;
  -   Pesquisas com curinga;
  -   Expressões complexas com base em dados Colunar – avaliar a necessidade de criar colunas computadas persistentes, que podem ser indexadas;

> [!NOTE] 
> Todas as opções acima podem ser feitas programaticamente.

## <a name="TableValuedFunctions"></a>Uso de funções com valor de tabela (várias instruções vs embutido)

**Aplica-se a:** plataforma externa (por exemplo, Oracle, DB2, MySQL e Sybase) e [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] migração.

> [!NOTE]
> Para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] migrações, se esse problema existe na origem [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], migrando para uma versão mais recente do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] como-será não abordar esse cenário.

Funções com valor de tabela retornar um tipo de dados de tabela que pode ser uma alternativa a modos de exibição. Enquanto as exibições são limitadas a um único `SELECT` instrução, funções definidas pelo usuário podem conter instruções adicionais que permitem mais lógica que é possível nos modos de exibição.

> [!IMPORTANT] 
> Desde que a tabela de saída de um MSTVF (função com valor de várias instruções tabela) não é criada em tempo de compilação, a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Otimizador de consulta se baseia em heurística e estatísticas não reais, para determinar as estimativas de linha. Mesmo se os índices são adicionados para as tabelas base, isso não vai ajudar. Para MSTVFs, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa uma estimativa fixa de 1 para o número de linhas esperado a ser retornado por um MSTVF (começando com [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] fixa estimativa é 100 linhas).

### <a name="steps-to-resolve"></a>Etapas para resolver
1.  Se a TVF com várias instruções somente a única instrução, converta em Inline TVF.

    ```tsql
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
    Para 

    ```tsql
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

2.  Se mais complexo, considere usar os resultados intermediários armazenados em tabelas com otimização de memória ou tabelas temporárias.

##  <a name="Additional_Reading"></a> Leitura adicional  
 [Melhor prática com o Repositório de Consultas](../relational-databases/performance/best-practice-with-the-query-store.md)  
[Tabelas com otimização de memória](../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
[Funções definidas pelo usuário](../relational-databases/user-defined-functions/user-defined-functions.md)  
[Variáveis de tabela e linha estimativas - parte 1](https://blogs.msdn.microsoft.com/blogdoezequiel/2012/11/30/table-variables-and-row-estimations-part-1/)  
[Variáveis de tabela e linha estimativas - parte 2](https://blogs.msdn.microsoft.com/blogdoezequiel/2012/12/09/table-variables-and-row-estimations-part-2/)  
[Cache de plano de execução e reutilização](../relational-databases/query-processing-architecture-guide.md#execution-plan-caching-and-reuse)

