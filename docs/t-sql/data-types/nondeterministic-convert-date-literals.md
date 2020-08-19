---
description: Conversão não determinística de cadeias de caracteres literais de data em valores de DATA
title: Conversão não determinística de literais de data | Microsoft Docs
ms.custom: ''
ms.date: 11/19/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4c1d50cc58995479aa61b4c62639f9d13de6f400
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88445864"
---
# <a name="nondeterministic-conversion-of-literal-date-strings-into-date-values"></a>Conversão não determinística de cadeias de caracteres literais de data em valores de DATA

Tenha cuidado ao permitir que a conversão de suas cadeias de CARACTERES em tipos de dados de DATA. O motivo é que essas conversões frequentemente _não são determinísticas_.

Você controla essas conversões não determinísticas considerado as configurações [SET LANGUAGE](../statements/set-language-transact-sql.md) e [SET DATEFORMAT](../statements/set-dateformat-transact-sql.md).



## <a name="set-language-example-month-name-in-polish"></a>Exemplo de SET LANGUAGE: nome do mês em polonês

- `SET LANGUAGE Polish;`

Uma cadeia de caracteres pode ser o nome de um mês. Mas é o nome está inglês, polonês, croata ou em outro idioma? A sessão do usuário será definida como o idioma correspondente correto?

Por exemplo, considere a palavra _listopad_, que é o nome de um mês. Mas qual mês depende do idioma que o sistema SQL acredita que está sendo usado:
- Se for polonês, então _listopad_ será traduzido como o mês 11 (_novembro_ em português).
- Se croata, então _listopad_ será traduzido como o mês 10 (_outubro_ em português).

#### <a name="code-example-of-set-language"></a>Exemplo de código de SET LANGUAGE

```sql
--SELECT alias FROM sys.syslanguages ORDER BY alias;

DECLARE @yourInputDate  NVARCHAR(32) = '28 listopad 2018';

SET LANGUAGE Polish;
SELECT CONVERT(DATE, @yourInputDate) AS [SL_Polish];

SET LANGUAGE Croatian;
SELECT CONVERT(DATE, @yourInputDate) AS [SL_Croatian];

SET LANGUAGE English;


/***  Actual output:  For the two months, note the 11 versus the 10.
SL_Polish
2018-11-28

SL_Croatian
2018-10-28
***/
```



## <a name="set-dateformat-example"></a>Exemplo de SET DATEFORMAT

- `SET DATEFORMAT dmy;`

O formato **dma** anterior diz que uma cadeia de caracteres de data de exemplo de '01-03-2018' deve ser interpretada como _o primeiro dia de março do ano de 2018_.

Em vez disso, **mda** fosse especificado, a mesma cadeia de caracteres '01-03-2018' significaria _o terceiro dia de janeiro de 2018_.

E se **amd** tivesse sido especificado, não haveria nenhuma garantia de qual seria a saída. O valor numérico de '2018' é muito grande para ser um dia.
<!--
The preceding claim of "no guarantee" might be incorrect, in the minds of the SQL query engine Developer team?
-->

#### <a name="specific-countries"></a>Países específicos

No Japão e na China, DATEFORMAT de **amd** é usado. As partes do formato estão em uma sequência lógica da maior unidade para a menor. Assim, esse formato é bem classificado. Esse formato é considerado o formato _internacional_. É internacional porque os quatro dígitos do ano são não ambíguos e nenhum país na Terra usa o formato arcaico do **adm**.

Em outros países, como Alemanha e França, DATEFORMAT é **dma**, que significa **'dd-mm-aaaa'**. O formato **dma** não é bem classificado, mas é uma sequência lógica da menor unidade para a maior.

Os Estados Unidos e os Estados Federados da Micronésia, são os únicos países que usam **mda**, que não é classificado. A sequência mista de formato corresponde ao padrão de discurso verbal em datas faladas.

#### <a name="code-example-of-set-dateformat-mdy-versus-dmy"></a>Exemplo de código de SET DATEFORMAT: *mda* versus *dma*

O exemplo de código Transact-SQL a seguir usa a mesma cadeia de caracteres de data com três configurações diferentes de DATEFORMAT. Uma execução do código produz a saída mostrada no comentário:

```sql
DECLARE @yourDateString NVARCHAR(10) = '12-09-2018';
PRINT @yourDateString + '  = the input.';

SET DATEFORMAT dmy;
SELECT CONVERT(DATE, @yourDateString) AS [DMY-Interpretation-of-input-format];

SET DATEFORMAT mdy;
SELECT CONVERT(DATE, @yourDateString) AS [MDY-Interpretation-of-input-format];

SET DATEFORMAT ymd;
SELECT CONVERT(DATE, @yourDateString) AS [YMD-Interpretation--?--NotGuaranteed];


/***  Actual output:
12-09-2018  = the input.

DMY-Interpretation-of-input-format
2018-09-12

MDY-Interpretation-of-input-format
2018-12-09

YMD-Interpretation--?--NotGuaranteed
2018-12-09
***/
```

No exemplo de código anterior, o exemplo final tem uma incompatibilidade entre o formato **amd** versus a cadeia de caracteres de entrada. O terceiro nó da cadeia de caracteres de entrada representa um valor numérico muito grande para ser um dia. A Microsoft não garante o valor de saída dessas incompatibilidades.

#### <a name="convert-offers-explicit-codes-for-_deterministic_-control-of-date-formats"></a>CONVERT oferece códigos explícitos para controle _determinístico_ dos formatos de data

Nosso artigo de documentação CAST e CONVERT lista códigos explícitos que você pode usar com a função CONVERT para controlar de _modo determinístico_ conversões de data. A cada mês, o artigo tem uma de nossas contagens de exibições de página mais altas.

- [CAST e CONVERT (Transact-SQL): estilos de data e hora](../functions/cast-and-convert-transact-sql.md#date-and-time-styles)
- [CAST e CONVERT (Transact-SQL): algumas conversões de datetime não são determinísticas](../functions/cast-and-convert-transact-sql.md#certain-datetime-conversions-are-nondeterministic)



## <a name="compatibility-level-90-and-above"></a>Nível de compatibilidade 90 e superior

No SQL Server 2000, o nível de compatibilidade era 80. Para configurações de nível 80 ou inferior, as conversões de data implícita eram determinísticas.

Começando com o SQL Server 2005 e seu nível de compatibilidade 90, conversões de data implícita passaram a não ser determinísticas. Conversões de data tornaram-se dependentes de SET LANGUAGE e SET DATEFORMAT do nível 90 em diante.

#### <a name="unicode"></a>Unicode

<!-- The next live sentence needs an explanatory example!  N'somethingHere?'.
-->
Conversão de dados de caractere não Unicode entre ordenações também é considerada não determinística.



## <a name="see-also"></a>Confira também

- [Definir um idioma de sessão](../../relational-databases/collations/set-a-session-language.md)
- [tipos de dados e funções de data e hora (Transact-SQL)](../functions/date-and-time-data-types-and-functions-transact-sql.md)
- [FORMAT (Transact-SQL)](../functions/format-transact-sql.md)
- [ISDATE (Transact-SQL)](../functions/isdate-transact-sql.md)



<!--
This new article is linked-to by the following articles (at least initially on 2018/11/19).....
...
* docs/relational-databases/views/create-indexed-views.md
* docs/relational-databases/indexes/indexes-on-computed-columns.md
* docs/t-sql/functions/cast-and-convert-transact-sql.md
...
As a reaction to public PR 1279, this approach of creating a new article to link to is a better alternative than a docs/includes/ approach.
GeneMi (MightyPen), 2018/11/19
-->

