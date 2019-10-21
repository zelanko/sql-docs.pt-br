---
title: Embutimento de UDF escalar em bancos de dados Microsoft SQL | Microsoft Docs
description: Recurso de embutimento de UDF escalar para melhorar o desempenho de consultas que invocam UDFs escalares no SQL Server (2018 e posteriores) e no Banco de Dados SQL do Azure.
ms.custom: ''
ms.date: 09/13/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords: ''
ms.assetid: ''
author: s-r-k
ms.author: karam
monikerRange: = azuresqldb-current || >= sql-server-ver15 || = sqlallproducts-allversions
ms.openlocfilehash: cfc56126ae84cc8674e7316b45e855584fdabde7
ms.sourcegitcommit: 4c5fb002719627f1a1594f4e43754741dc299346
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2019
ms.locfileid: "72518004"
---
# <a name="scalar-udf-inlining"></a>Embutimento de UDF escalar

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo apresenta o embutimento de UDF escalar, um recurso sob o conjunto de recursos de processamento de consulta inteligente. Esse recurso melhora o desempenho das consultas que invocam UDFs escalares em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQLv15](../../includes/sssqlv15-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)].

## <a name="t-sql-scalar-user-defined-functions"></a>Funções escalares definidas pelo usuário T-SQL

Funções Definidas pelo Usuário implementadas no Transact-SQL e que retornam um valor de dados único são chamadas de Funções Definidas pelo Usuário Escalares T-SQL. UDFs do T-SQL são uma maneira elegante de obter reutilização e modularidade de código em consultas SQL. Alguns cálculos (como regras de negócios complexas) são mais fáceis de expressar no formulário de UDF imperativa. UDFs ajudam na criação de uma lógica complexa sem exigir experiência em escrever consultas SQL complexas.

## <a name="performance-of-scalar-udfs"></a>Desempenho de UDFs escalares

Normalmente, UDFs escalares acabam tendo um desempenho ruim devido aos seguintes motivos.

- **Invocação iterativa:** UDFs são invocados de maneira iterativa, uma vez a cada tupla qualificada. Isso resulta em custos adicionais repetido de comutação de contexto repetida devido à invocação de função. Especialmente, UDFs que executam consultas SQL em sua definição são gravemente afetadas.
- **Falta de custos:** Durante a otimização, somente operadores relacionais terão o custo calculado, enquanto os operadores escalares não terão. Antes da introdução de UDFs escalares, outros operadores escalares geralmente eram baratos e não exigiam avaliação de custo. Um pequeno custo de CPU adicionado para uma operação de escalar foi suficiente. Há cenários em que o custo real é significativo e ainda assim permanece sub-representado.
- **Execução interpretada:** UDFs são avaliados como um lote de instruções, executados instrução a instrução. Cada instrução em si é compilada e o plano compilado é armazenado em cache. Embora essa estratégia de armazenamento em cache economize algum tempo, pois evita recompilações, cada instrução é executada em isolamento. Nenhuma otimização entre instruções é executada.
- **Execução serial:** O SQL Server não permite paralelismo dentro da consulta em consultas que invocam UDFs. 

## <a name="automatic-inlining-of-scalar-udfs"></a>Embutimento automático de UDFs escalares

A meta do recurso de embutimento de UDF escalar é melhorar o desempenho de consultas que invocam UDFs escalares do T-SQL, em que a execução da UDF é o principal gargalo.

Com esse novo recurso, os UDFs escalares são automaticamente transformados em expressões escalares ou subconsultas escalares substituídas na consulta responsável pela chamada, em vez do operador UDF. Essas expressões e subconsultas então são otimizadas. Como resultado, o plano de consulta não terá mais um operador de função definido pelo usuário, mas seus efeitos serão observados no plano, como modos de exibição ou TVFs embutidos.

### <a name="example-1---single-statement-scalar-udf"></a>Exemplo 1: UDF estado de instrução única

Considere a consulta a seguir

```sql
SELECT L_SHIPDATE, O_SHIPPRIORITY, SUM (L_EXTENDEDPRICE *(1 - L_DISCOUNT)) 
FROM LINEITEM
INNER JOIN ORDERS
  ON O_ORDERKEY = L_ORDERKEY 
GROUP BY L_SHIPDATE, O_SHIPPRIORITY ORDER BY L_SHIPDATE;
```

Essa consulta calcula a soma dos preços com desconto para itens de linha e apresenta os resultados agrupados por data de envio e prioridade de envio. A expressão `L_EXTENDEDPRICE *(1 - L_DISCOUNT)` é a fórmula para o preço com desconto para um determinado item de linha. Essas fórmulas podem ser extraídas em funções para o benefício de modularidade e da reutilização.

```sql
CREATE FUNCTION dbo.discount_price(@price DECIMAL(12,2), @discount DECIMAL(12,2)) 
RETURNS DECIMAL (12,2) AS
BEGIN
  RETURN @price * (1 - @discount);
END

```

Agora, a consulta pode ser modificada para invocar essa UDF.

```sql
SELECT L_SHIPDATE, O_SHIPPRIORITY, SUM (dbo.discount_price(L_EXTENDEDPRICE, L_DISCOUNT)) 
FROM LINEITEM
INNER JOIN ORDERS
  ON O_ORDERKEY = L_ORDERKEY 
GROUP BY L_SHIPDATE, O_SHIPPRIORITY ORDER BY L_SHIPDATE
```

Devido a motivos descritos anteriormente, a consulta com a UDF tem um mau desempenho. Agora, com o embutimento de UDF escalar, a expressão escalar no corpo da UDF é substituída diretamente na consulta. Os resultados da execução dessa consulta são mostrados na tabela a seguir:

| Consulta: | Consulta sem UDF | Consultar com UDF (sem embutimento) | Consultar com embutimento de UDF escalar | 
| --- | --- | --- | --- |
| Tempo de execução: | 1,6 segundo | 29 minutos e 11 segundos | 1,6 segundo |

Esses números são baseados em um banco de dados CCI de 10 GB (usando o esquema do TPC-H), em execução em um computador com processador duplo (12 núcleos), 96 GB de RAM, apoiado por SSD. Os números incluem a compilação e o tempo de execução com um pool de buffers e cache de procedimento frio. A configuração padrão foi usada e nenhum outro índice foi criado.

### <a name="example-2---multi-statement-scalar-udf"></a>Exemplo 2: UDF escalar de várias instruções

UDFs escalares implementadas usando várias instruções T-SQL, como atribuições de variáveis e ramificação condicional, também podem ser embutidos. Considere a seguinte UDF escalar que, dada uma chave de cliente, determina a categoria de serviço para esse cliente. Ele chega na categoria computando primeiro o preço total de todos os pedidos feitos pelo cliente usando uma consulta SQL. Então, ela usa uma lógica `IF-ELSE` para decidir a categoria com base no preço total.

```sql
CREATE OR ALTER FUNCTION dbo.customer_category(@ckey INT) 
RETURNS CHAR(10) AS
BEGIN
  DECLARE @total_price DECIMAL(18,2);
  DECLARE @category CHAR(10);

  SELECT @total_price = SUM(O_TOTALPRICE) FROM ORDERS WHERE O_CUSTKEY = @ckey;

  IF @total_price < 500000
    SET @category = 'REGULAR';
  ELSE IF @total_price < 1000000
    SET @category = 'GOLD';
  ELSE 
    SET @category = 'PLATINUM';

  RETURN @category;
END

```

Agora, considere uma consulta que invoque essa UDF.

```sql
SELECT C_NAME, dbo.customer_category(C_CUSTKEY) FROM CUSTOMER;
```

O plano de execução para essa consulta no SQL Server 2017 (nível de compatibilidade 140 e anterior) é o seguinte:

![Plano de consulta sem embutimento](./media/query-plan-without-udf-inlining.png)

Como mostra o plano, o SQL Server adota uma estratégia simples aqui: para cada tupla na tabela `CUSTOMER`, invoca a UDF e produz os resultados. Essa estratégia é ingênua e ineficiente. Com embutimento, essas UDFs são transformadas em subconsultas escalares equivalentes, que são substituídas na consulta responsável pela chamada no lugar da UDF.

Para a mesma consulta, o plano com a UDF embutida se parece com o abaixo.

![Plano de consulta com embutimento](./media/query-plan-with-udf-inlining.png)

Como mencionado anteriormente, o plano de consulta não tem mais um operador de função definida pelo usuário, mas seus efeitos agora são observáveis no plano, como modos de exibição ou TVFs embutidos. Aqui estão algumas observações importantes do plano de acima:

1. O SQL Server inferiu a junção implícita entre `CUSTOMER` e `ORDERS` e tornou isso explícito por meio de um operador de junção.
2. O SQL Server também inferiu o `GROUP BY O_CUSTKEY on ORDERS` implícito e usou IndexSpool + StreamAggregate implementá-lo.
3. O SQL Server agora está usando o paralelismo em todos os operadores.

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

Dependendo da complexidade da lógica na UDF, o plano de consulta resultante também poderá ficar maior e mais complexo. Como podemos ver, as operações dentro da UDF agora não são mais uma caixa preta e, portanto, o otimizador de consulta é capaz de calcular o custo e otimizar essas operações. Além disso, uma vez que a UDF não está mais no plano, invocação da UDF iterativa é substituída por um plano que evita completamente a sobrecarga de chamada de função.

## <a name="inlineable-scalar-udfs-requirements"></a>Requisitos de UDFs escalares que podem ser embutidas

Uma UDF T-SQL escalar poderá ser embutida se todas as seguintes condições forem verdadeiras:

- A UDF é escrita usando as seguintes construções:
    - `DECLARE`, `SET`: Declaração de variável e atribuições.
    - `SELECT`: Consulta SQL com atribuições variáveis únicas/múltiplas<sup>1</sup>.
    - `IF`/`ELSE`: Ramificação com níveis arbitrários de aninhamento.
    - `RETURN`: Instruções de retorno únicas ou múltiplas.
    - `UDF`: Chamadas de função aninhadas/recursivas<sup>2</sup>.
    - Outros: Operações relacionais, como `EXISTS`, `ISNULL`.
- A UDF não invoca nenhuma função intrínseca que seja dependente de tempo (como `GETDATE()`) ou tenha efeitos colaterais<sup>3</sup> (como `NEWSEQUENTIALID()`).
- A UDF usa a cláusula `EXECUTE AS CALLER` (o comportamento padrão se a cláusula `EXECUTE AS` não for especificada).
- A UDF não faz referência a variáveis de tabela nem parâmetros com valor de tabela.
- A consulta que invoca uma UDF escalar não faz referência a uma chamada UDF escalar em sua cláusula `GROUP BY`.
- A consulta que invoca um UDF escalar em sua lista de seleção com a cláusula `DISTINCT` não tem a cláusula `ORDER BY`.
- O UDF não é usado na cláusula `ORDER BY`.
- A UDF não é compilada nativamente (há suporte para interoperabilidade).
- A UDF não é usada em uma coluna computada nem em uma definição de restrição de verificação.
- A UDF não faz referência a tipos definidos pelo usuário.
- Não há assinaturas adicionadas à UDF.
- A UDF não é uma função de partição.

<sup>1</sup> `SELECT` com acúmulo/agregação variável (por exemplo, `SELECT @val += col1 FROM table1`) não há suporte para embutimento.

<sup>2</sup> UDFs recursivos serão embutidos em uma profundidade determinada apenas.

<sup>3</sup> Funções intrínsecas cujos resultados dependem da hora do sistema atual são dependente de hora. Uma função intrínseca que pode atualizar algum estado global interno é um exemplo de uma função com efeitos colaterais. Essas funções retornam resultados diferentes cada vez que são chamadas, com base no estado interno.

### <a name="checking-whether-or-not-a-udf-can-be-inlined"></a>Verificar se uma UDF pode ser embutida ou não

Para cada UDF escalar do T-SQL, a exibição de catálogo [sys.sql_modules](../system-catalog-views/sys-sql-modules-transact-sql.md) inclui uma propriedade chamada `is_inlineable`, que indica se uma UDF pode ser embutida ou não. Um valor de 1 indica que ele é pode ser embutido e 0 indica o contrário. Essa propriedade terá um valor de 1 para todos as TVFs embutidos também. Para todos os outros módulos, o valor será 0.

>[!NOTE]
>Se uma UDF escalar puder ser embutida, isso não implica que ele sempre será embutido. O SQL Server decidirá qual (por consulta, por UDF) se embutirá uma UDF ou não. Por exemplo, se a definição da UDF for executada em milhares de linhas de código, o SQL Server poderá optar por não embuti-la. Outro exemplo é uma UDF em uma cláusula `GROUP BY` – que não será embutida. Essa decisão é tomada quando a consulta que referencia uma UDF escalar é compilada.

### <a name="checking-whether-inlining-has-happened-or-not"></a>Verificar se embutimento ocorreu ou não

Se todas as pré-condições forem atendidas e o SQL Server decidir executar embutimento, ele transformará a UDF em uma expressão relacional. Do plano de consulta, é fácil descobrir se embutimento ocorreu ou não:

- O xml do plano não terá um nó xml `<UserDefinedFunction>` para uma UDF que tenha sido embutida com êxito. 
- Determinados XEvents são emitidos.

## <a name="enabling-scalar-udf-inlining"></a>Como habilitar o embutimento de UDF escalar

Você pode automaticamente qualificar as cargas de trabalho para inlining de UDF escalar habilitando o nível de compatibilidade 150 para o banco de dados.? Você pode definir isso usando o Transact-SQL.?Por exemplo:  

```sql
ALTER DATABASE [WideWorldImportersDW] SET COMPATIBILITY_LEVEL = 150;
```

Além disso, não há nenhuma outra alteração que precise ser feita para consultas ou UDFs para aproveitar esse recurso.

## <a name="disabling-scalar-udf-inlining-without-changing-the-compatibility-level"></a>Como desabilitar o embutimento de UDF Escalar sem alterar o nível de compatibilidade

O embutimento de UDF escalar pode ser desabilitado no escopo da UDF, da instrução ou do banco de dados enquanto ainda mantém o nível de compatibilidade do banco de dados 150 e superior. Para desabilitar o embutimento de UDF escalar no escopo do banco de dados, execute a seguinte instrução dentro do contexto do banco de dados aplicável: 

```sql
ALTER DATABASE SCOPED CONFIGURATION SET TSQL_SCALAR_UDF_INLINING = OFF;
```

Para habilitar novamente o embutimento de UDF escalar para o banco de dados, execute a seguinte instrução dentro do contexto do banco de dados aplicável:

```sql
ALTER DATABASE SCOPED CONFIGURATION SET TSQL_SCALAR_UDF_INLINING = ON;
```

Quando LIGADA, essa configuração aparecerá como habilitada em [`sys.database_scoped_configurations`](../system-catalog-views/sys-database-scoped-configurations-transact-sql.md). Você também pode desabilitar o embutimento de UDF escalar de uma consulta específica designando `DISABLE_TSQL_SCALAR_UDF_INLINING` como uma dica de consulta `USE HINT`. Por exemplo:

```sql
SELECT L_SHIPDATE, O_SHIPPRIORITY, SUM (dbo.discount_price(L_EXTENDEDPRICE, L_DISCOUNT)) 
FROM LINEITEM
INNER JOIN ORDERS
  ON O_ORDERKEY = L_ORDERKEY 
GROUP BY L_SHIPDATE, O_SHIPPRIORITY ORDER BY L_SHIPDATE
OPTION (USE HINT('DISABLE_TSQL_SCALAR_UDF_INLINING'));
```

Uma dica de consulta `USE HINT` tem precedência sobre a configuração no escopo do banco de dados ou a configuração de nível de compatibilidade.

O embutimento de UDF escalar também pode ser desabilitado para uma UDF específica usando a cláusula INLINE na instrução `CREATE FUNCTION` ou `ALTER FUNCTION`.
Por exemplo:

```sql
CREATE OR ALTER FUNCTION dbo.discount_price(@price DECIMAL(12,2), @discount DECIMAL(12,2))
RETURNS DECIMAL (12,2)
WITH INLINE = OFF
AS
BEGIN
    RETURN @price * (1 - @discount);
END
```

Depois que a declaração acima é executada, essa UDF nunca será embutida em nenhuma consulta que a invoque. Para habilitar novamente o embutimento para essa UDF, execute a seguinte instrução:

```sql
CREATE OR ALTER FUNCTION dbo.discount_price(@price DECIMAL(12,2), @discount DECIMAL(12,2))
RETURNS DECIMAL (12,2)
WITH INLINE = ON
AS
BEGIN
    RETURN @price * (1 - @discount);
END
```

>[!NOTE]
>A cláusula `INLINE` não é obrigatória. Se a cláusula `INLINE` não for especificada, ela será automaticamente definida como `ON`/`OFF` com base em se a UDF pode ser embutida. Se `INLINE=ON` for especificado, mas a UDF for considerada não qualificada para embutimento, um erro será gerado.

## <a name="important-notes"></a>Observações importantes

Conforme descrito neste artigo, o embutimento de UDF escalar transforma uma consulta com UDFs escalares em uma consulta com uma subconsulta escalar equivalente. Devido a essa transformação, os usuários podem observar algumas diferenças no comportamento nos seguintes cenários:

1. O embutimento resultará em um hash de consulta diferente para o mesmo texto da consulta.
1. Determinados avisos em instruções dentro da UDF (como divisão por zero etc.) que podem ter sido ocultados anteriormente, pode aparecer devido ao embutimento.
1. Dicas de junção no nível da consulta talvez não sejam válidas, pois o embutimento pode introduzir novas junções. Dicas de junção local precisarão ser usadas em vez disso.
1. Exibições que referenciam UDFs embutidos escalares não podem ser indexadas. Se você precisar criar um índice nessas exibições, desabilite embutimento para UDFs referenciadas.
1. Pode haver algumas diferenças no comportamento de [Máscara de Dados Dinâmicos](../security/dynamic-data-masking.md) com embutimento de UDF. Em certas situações (dependendo da lógica na UDF), embutimento pode ser mais conservador no que diz respeito ao mascaramento de colunas de saída. Em cenários em que as colunas referenciadas em uma UDF não são colunas de saída, elas não são mascaradas. 
1. Se uma UDF fizer referência a funções internas, como `SCOPE_IDENTITY()`, o valor retornado pela função interna será alterado com o embutimento. Essa alteração no comportamento ocorre porque o embutimento altera o escopo das instruções dentro da UDF.

## <a name="see-also"></a>Consulte Também

[Central de desempenho do Mecanismo de Banco de Dados do SQL Server e do Banco de Dados SQL do Azure](../../relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database.md)

[Guia de arquitetura de processamento de consultas](../../relational-databases/query-processing-architecture-guide.md)

[Referência de operadores físicos e lógicos de plano de execução](../../relational-databases/showplan-logical-and-physical-operators-reference.md)

[Junções](../../relational-databases/performance/joins.md)

[Demonstrando o Processamento de Consulta Adaptável](https://github.com/joesackmsft/Conferences/blob/master/Data_AMP_Detroit_2017/Demos/AQP_Demo_ReadMe.md)
