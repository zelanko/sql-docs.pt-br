---
title: CAST e CONVERT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/28/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CAST_TSQL
- CONVERT_TSQL
- CAST
- CONVERT
dev_langs:
- TSQL
helpviewer_keywords:
- CAST function
- automatic data type conversion
- varbinary data type
- CONVERT function
- data types [SQL Server], converting
- large value data types
- implicit data type conversions
- image data type, converting
- explicit data type conversions [SQL Server]
- binary [SQL Server], converting
- text data type, converting
- date and time [SQL Server], cast and convert
- truncating conversions
- converting data types [SQL Server], conversion functions
- time zones [SQL Server]
- roundtrip conversions
ms.assetid: a87d0850-c670-4720-9ad5-6f5a22343ea8
caps.latest.revision: 136
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: cd868d10f9a7d6edab413341c18be9613962c981
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2018
---
# <a name="cast-and-convert-transact-sql"></a>CAST e CONVERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Converte uma expressão de um tipo de dados para outro.  
**Exemplo.** Altere o tipo de dados de entrada.

**Converter**
```sql  
SELECT 9.5 AS Original, CAST(9.5 AS int) AS int, 
    CAST(9.5 AS decimal(6,4)) AS decimal;

```  
**Converter**
```sql  

SELECT 9.5 AS Original, CONVERT(int, 9.5) AS int, 
    CONVERT(decimal(6,4), 9.5) AS decimal;
```  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
|Original   |INT    |Decimal |  
|----|----|----|  
|9.5 |9 |9.5000 |  

Há **muito mais [exemplos](#BKMK_examples)** na parte inferior deste tópico. 
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
-- Syntax for CAST:  
CAST ( expression AS data_type [ ( length ) ] )  
  
-- Syntax for CONVERT:  
CONVERT ( data_type [ ( length ) ] , expression [ , style ] )  
```  
  
## <a name="arguments"></a>Argumentos  
*expressão*  
É qualquer [expressão](../../t-sql/language-elements/expressions-transact-sql.md) válida.
  
*data_type*  
É o tipo de dados de destino. Isso inclui **xml**, **bigint**, e **sql_variant**. Tipos de dados alias não podem ser usados.
  
*length*  
É um inteiro opcional que especifica o comprimento do tipo de dados de destino. O valor padrão é 30.
  
*style*  
É uma expressão de inteiro que especifica como a função CONVERT deve ser convertida em *expression*. Se o estilo for NULL, NULL será retornado. O intervalo é determinado por *data_type*. 
  
## <a name="return-types"></a>Tipos de retorno
Retorna *expression* convertida em *data_type*.

## <a name="date-and-time-styles"></a>Estilos de data e hora  
Quando *expression* é um tipo de dados de data ou hora, *style* pode ser um dos valores mostrados na tabela a seguir. Outros valores são processados como 0. Começando pelo [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], os únicos estilos compatíveis ao converter dos tipos de data e hora em **datetimeoffset** são 0 ou 1. Todos os outros estilos de conversão retornam erro 9809.
  
>  [!NOTE]  
>  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tem suporte para o formato de data em árabe usando o algoritmo kuwaitiano.
  
|Sem século (yy) (<sup>1</sup>)|Com século (aaaa)|Standard|Entrada/saída (<sup>3</sup>)|  
|---|---|--|---|
|-|**0** ou **100** (<sup>1,</sup><sup>2</sup>)|Padrão para datetime e smalldatetime|mês dd aaaa hh:miAM (ou PM)|  
|**1**|**101**|EUA|1 = mm/dd/aa<br /> 101 = mm/dd/aaaa|  
|**2**|**102**|ANSI|2 = aa.mm.dd<br /> 102 = aaaa.mm.dd|  
|**3**|**103**|Britânico/francês|3 = dd/mm/aa<br /> 103 = dd/mm/aaaa|  
|**4**|**104**|German|4 = dd.mm.aa<br /> 104 = dd.mm.aaaa|  
|**5**|**105**|Italiano|5 = dd-mm-aa<br /> 105 = dd-mm-aaaa|  
|**6**|**106** <sup>(1)</sup>|-|6 = dd mês aa<br /> 106 = dd mês aaaa|  
|**7**|**107** <sup>(1)</sup>|-|7 = Mês dd, aa<br /> 107 = Mês dd, aaaa|  
|**8**|**108**|-|hh:mi:ss|  
|-|**9** ou **109** (<sup>1,</sup><sup>2</sup>)|Padrão + milissegundos|mês dd aaaa hh:mi:ss:mmmAM (ou PM)|  
|**10**|**110**|EUA|10 = mm-dd-aa<br /> 110 = mm-dd-aaaa|  
|**11**|**111**|JAPÃO|11 = aa/mm/dd<br /> 111 = aaaa/mm/dd|  
|**12**|**112**|ISO|12 = aammdd<br /> 112 = aaaammdd|  
|-|**13** ou **113** (<sup>1,</sup><sup>2</sup>)|Padrão Europa + milissegundos|dd mês aaaa hh:mi:ss:mmm (24h)|  
|**14**|**114**|-|hh:mi:ss:mmm(24h)|  
|-|**20** ou **120** (<sup>2</sup>)|ODBC canônico|aaaa-mm-dd hh:mi:ss(24h)|  
|-|**21** ou **121** (<sup>2</sup>)|ODBC canônico (com milissegundos) padrão para hora, data, datetime2 e datetimeoffset|aaaa-mm-dd hh:mi:ss.mmm(24h)|  
|-|**126** (<sup>4</sup>)|ISO8601|aaaa-mm-ddThh:mi:ss.mmm (sem espaços)<br /> Observação: quando o valor de milissegundos (mmm) é 0, o valor de milissegundos não é exibido. Por exemplo, o valor '2012-11-07T18:26:20.000 é exibido como '2012-11-07T18:26:20'.|  
|-|**127**(<sup>6, 7</sup>)|ISO8601 com fuso horário Z.|aaaa-mm-ddThh:mi:ss.mmmZ (sem espaços)<br /> Observação: quando o valor de milissegundos (mmm) é 0, o valor de milissegundos não é exibido. Por exemplo, o valor '2012-11-07T18:26:20.000 é exibido como '2012-11-07T18:26:20'.|  
|-|**130** (<sup>1,</sup><sup>2</sup>)|Islâmico (<sup>5</sup>)|dd mmm aaaa hh:mi:ss:mmmAM<br /> Neste estilo, mon representa uma representação unicode Hijri de vários tokens do nome completo do mês. Esse valor não é renderizado corretamente em uma instalação em inglês dos EUA padrão do SSMS.|  
|-|**131** (<sup>2</sup>)|Islâmico (<sup>5</sup>)|dd/mm/aaaa hh:mi:ss:mmmAM|  
  
<sup>1</sup> Esses valores de estilo retornam resultados não determinísticos. Incluem todos os estilos (aa) (sem século) e um subconjunto de estilos (aaaa) (com século).
  
<sup>2</sup> Os valores padrão (*style** *0** ou **100**, **9** ou **109**, **13** ou **113**, **20** ou **120** e **21** ou **121**) sempre retornam o século (yyyy).
  
<sup>3</sup> Entrada quando é feita a conversão em **datetime**; saída quando é feita a conversão em dados de caractere.
  
<sup>4</sup> Criado para uso do XML. Para conversão de **datetime** ou **smalldatetime** em dados de caractere, o formato de saída é descrito na tabela anterior.
  
<sup>5</sup> Islâmico é um sistema de calendário com diversas variações. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa o algoritmo kuwaitiano.
  
> [!IMPORTANT]  
>  Por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpreta anos de dois dígitos com base em um ano de corte de 2049. Isto é, o ano 49 de dois dígitos é interpretado como 2049 e o ano 50 de dois dígitos é interpretado como 1950. Muitos aplicativos cliente, como aqueles que se baseiam em objetos Automation, usam um ano de corte de 2030. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece a opção de configuração two digit year cutoff que altera o ano de corte usado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e permite o tratamento consistente de datas. É recomendável especificar anos de quatro dígitos.  
  
<sup>6</sup> Apenas compatível na conversão de dados de caractere em **datetime** ou **smalldatetime**. Quando dados de caractere que representam apenas componentes de data ou hora são convertidos em tipos de dados **datetime** ou **smalldatetime**, o componente de hora não especificado é definido como 00:00:00.000 e o componente de data não especificado é definido como 1900-01-01.
  
<sup>7</sup>O indicador de fuso horário opcional, Z, é usado para facilitar o mapeamento de valores **datetime** XML que contêm informações de fuso horário para valores **datetime** do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não contêm fuso horário. Z é o indicador de fuso horário UTC-0. Outros fusos horários são indicados com deslocamento de HH:MM na direção + ou -. Por exemplo: `2006-12-12T23:45:12-08:00`.
  
Quando você converte em dados de caractere de **smalldatetime**, os estilos que incluem segundos ou milissegundos mostram zeros nessas posições. É possível truncar partes de data não desejadas ao converter de valores de **datetime** ou **smalldatetime** usando um tamanho de tipo de dados **char** ou **varchar** adequado.
  
Quando você converte **datetimeoffset** de dados de caractere com um estilo que inclui uma hora, um deslocamento de fuso horário é acrescentado ao resultado.
  
## <a name="float-and-real-styles"></a>Estilos float e real
Quando *expression* é **float** ou **real**, *style* pode ser um dos valores mostrados na tabela a seguir. Outros valores são processados como 0.
  
|Valor|Saída|  
|---|---|
|**0** (padrão)|Um máximo de 6 dígitos. Use em notação científica, quando apropriado.|  
|**1**|Sempre 8 dígitos. Use sempre em notação científica.|  
|**2**|Sempre 16 dígitos. Use sempre em notação científica.|  
|**3**|Sempre 17 dígitos. Use-o para a conversão sem perdas. Com esse estilo, cada valor float ou real distinto tem a garantia de ser convertido em uma cadeia de caracteres distinta.<br /> **Aplica-se a:** [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] e do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] em diante.|  
|**126, 128, 129**|Incluído por razões herdadas e poderia ser preterido em uma versão futura.|  
  
## <a name="money-and-smallmoney-styles"></a>Estilos money e smallmoney
Quando *expression* é **money** ou **smallmoney**, *style* pode ser um dos valores mostrados na tabela a seguir. Outros valores são processados como 0.
  
|Valor|Saída|  
|---|---|
|**0** (padrão)|Nenhuma vírgula a cada três dígitos à esquerda do ponto decimal e dois dígitos à direita do ponto decimal. Por exemplo, 4235.98.|  
|**1**|Vírgulas a cada três dígitos à esquerda do ponto decimal e dois dígitos à direita do ponto decimal. Por exemplo, 3,510.92.|  
|**2**|Nenhuma vírgula a cada três dígitos à esquerda do ponto decimal e quatro dígitos à direita do ponto decimal. Por exemplo, 4235.9819.|  
|**126**|Equivalente ao estilo 2 ao converter para char(n) ou varchar (n)|  
  
## <a name="xml-styles"></a>Estilos xml
Quando *expression* é **xml***, style* pode ser um dos valores mostrados na tabela a seguir. Outros valores são processados como 0.
  
|Valor|Saída|  
|---|---|
|**0** (padrão)|Use comportamento de análise padrão que descarta espaço em branco insignificante e não permite um subconjunto de DTD interno.<br /> **Observação:** ao fazer a conversão no tipo de dados **xml**, o espaço em branco insignificante do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é tratado de maneira diferente do XML 1.0. Para obter mais informações, consulte [Criar instâncias de dados XML](../../relational-databases/xml/create-instances-of-xml-data.md).|  
|**1**|Preserva espaço em branco insignificante. Essa configuração de estilo define o tratamento de **xml:space** padrão para se comportar da mesma forma como se **xml:space="preserve"** tivesse sido especificado em seu lugar.|  
|**2**|Habilita o processamento de subconjunto de DTD interno limitado.<br /><br /> Se habilitado, o servidor poderá usar as seguintes informações fornecidas em um subconjunto de DTD interno para executar operações de análise de não validação.<br /> - Os padrões de atributos são aplicados.<br /> - As referências a entidades internas são resolvidas e expandidas.<br /> - A correção sintática do modelo de conteúdo DTD é verificada.<br /> O analisador ignora subconjuntos de DTD externos. Ele também não avalia a declaração XML para verificar se o atributo **standalone** está definido como **yes** ou **no**, mas analisa a instância XML como se ela fosse um documento autônomo.|  
|**3**|Preserva espaço em branco insignificante e habilita processamento de subconjunto de DTD interno limitado.|  
  
## <a name="binary-styles"></a>Estilos binários
Quando *expression* é **binary(n)**, **varbinary(n)**, **char(n)** ou **varchar(n)**, *style* pode ser um dos valores mostrados na tabela a seguir. Valores de estilo que não estão listados na tabela retornarão um erro.
  
|Valor|Saída|  
|---|---|
|**0** (padrão)|Converte caracteres ASCII em bytes binários ou bytes binários em caracteres ASCII. Cada caractere ou byte é convertido 1:1.<br /> Se o *data_type* for um tipo binário, o caracteres 0x serão adicionados à esquerda do resultado.|  
|**1**, **2**|Se o *data_type* for um tipo binário, a expressão deverá ser uma expressão de caractere. A *expression* deve ser composta por um número par de dígitos hexadecimais (0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F, a, b, c, d, e, f). Se o *style* for definido como 1, os caracteres 0x deverão ser os dois primeiros caracteres na expressão. Se a expressão contiver um número de caracteres ímpar ou se algum dos caracteres for inválido, ocorrerá um erro.<br /> Se o tamanho da expressão convertida for maior que o tamanho do *data_type*, o resultado será truncado à direita.<br /> *data_types* de comprimento fixo que são maiores que o resultado convertido têm zeros adicionados à direita do resultado.<br /> Se o data_type for tipo de caractere, a expressão deve ser uma expressão de binária. Cada caractere binário é convertido em dois caracteres hexadecimais. Se o tamanho da expressão convertida for maior que o tamanho de *data_type*, ela será truncada à direita.<br /> Se o *data_type* for um tipo de caractere de tamanho fixo e o tamanho do resultado convertido for menor que o tamanho do *data_type*, serão adicionados espaços à direita da expressão convertida para manter um número par de dígitos hexadecimais.<br /> Os caracteres 0x serão adicionados à esquerda do resultado convertido para *style* 1.|  
  
## <a name="implicit-conversions"></a>Conversões implícitas
Conversões implícitas são conversões que ocorrem sem especificar a função CAST ou CONVERT. Conversões explícitas são as conversões que exigem que a função CAST ou CONVERT seja especificada. A ilustração a seguir mostra todas as conversões de tipos de dados explícitas e implícitas que são permitidas para tipos de dados fornecidos pelo sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Isso inclui **xml**, **bigint** e **sql_variant**. Não há nenhuma conversão implícita na atribuição do tipo de dados **sql_variant**, mas há uma conversão implícita em **sql_variant**.
  
> [!TIP]  
>  Este gráfico está disponível como um arquivo PDF para download no [Centro de Download da Microsoft](http://www.microsoft.com/download/details.aspx?id=35834).  
  
![Tabela de conversão de tipo de dados](../../t-sql/data-types/media/lrdatahd.png "Data type conversion table")
  
Ao converter entre **datetimeoffset** e os tipos de caracteres **char**, **varchar**, **nchar** e **nvarchar**, a parte do deslocamento de fuso horário convertido sempre deve ter dois dígitos para HH e MM, por exemplo, -08:00.
  
> [!NOTE]  
>  Como os dados Unicode sempre usam um número par de bytes, tenha cuidado ao converter **binary** ou **varbinary** bidirecionalmente em tipos de dados Unicode compatíveis. Por exemplo, a conversão a seguir não retorna um valor hexadecimal de 41. Ela retorna 4100: `SELECT CAST(CAST(0x41 AS nvarchar) AS varbinary)`.  
  
## <a name="large-value-data-types"></a>Tipos de dados de valor grande
Tipos de dados de valor grande exibem o mesmo comportamento de conversão implícita e explícita que suas contrapartes menores, principalmente os tipos de dados **varchar**, **nvarchar** e **varbinary**. Porém, você deve considerar as seguintes diretrizes:
-   A conversão de **image** para **varbinary(max)** e vice-versa é uma conversão implícita, assim como as conversões entre **text** e **varchar(max)** e **ntext** e **nvarchar(max)**.  
-   A conversão de tipos de dados de valor grande, como **varchar(max)**, em um tipo de dados de contraparte menor, como **varchar**, é uma conversão implícita, mas ocorrerá truncamento se o valor grande for grande demais para o tamanho especificado do tipo de dados menor.  
-   A conversão de **varchar**, **nvarchar** ou **varbinary** em seus tipos de dados de valor grande correspondentes é feita implicitamente.  
-   A conversão de tipo de dados **sql_variant** em tipos de dados de valor grande é uma conversão explícita.  
-   Tipos de dados de valor grande não podem ser convertidos no tipo de dados **sql_variant**.  
  
Para obter mais informações sobre como converter o tipo de dados **xml**, consulte [Criar instâncias de dados XML](../../relational-databases/xml/create-instances-of-xml-data.md).
  
## <a name="xml-data-type"></a>tipo de dados xml
Ao converter o tipo de dados **xml** explícita ou implicitamente em um tipo de dados de cadeia de caracteres ou binário, o conteúdo do tipo de dados **xml** é serializado de acordo com um conjunto de regras. Para obter informações sobre essas regras, consulte [Definir a serialização de dados XML](../../relational-databases/xml/define-the-serialization-of-xml-data.md). Para obter informações sobre como converter de outros tipos de dados no tipo de dados **xml**, consulte [Criar instâncias de dados XML](../../relational-databases/xml/create-instances-of-xml-data.md).
  
## <a name="text-and-image-data-types"></a>Tipos de dados text e image
Não há compatibilidade com a conversão automática dos tipos de dados **text** e **image**. Você pode converter explicitamente os dados **text** em dados de caractere, e os dados **image** em **binary** ou **varbinary**, mas o tamanho máximo é de 8.000 bytes. Se você tentar uma conversão incorreta, como a conversão de uma expressão de caractere que inclui letras em um **int**, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará uma mensagem de erro.
  
## <a name="output-collation"></a>Agrupamento da saída  
Quando a saída de CAST ou CONVERT for uma cadeia de caracteres e a entrada também for uma cadeia de caracteres, a saída terá o mesmo agrupamento e o mesmo rótulo de agrupamento que a entrada. Se a entrada não for uma cadeia de caracteres, a saída terá o agrupamento padrão do banco de dados e um rótulo de agrupamento de padrão coercível. Para obter mais informações, consulte [Precedência de agrupamento &#40;Transact-SQL&#41;](../../t-sql/statements/collation-precedence-transact-sql.md).
  
Para atribuir um agrupamento diferente à saída, aplique a cláusula COLLATE à expressão do resultado da função CAST ou CONVERT. Por exemplo:
  
`SELECT CAST('abc' AS varchar(5)) COLLATE French_CS_AS`
  
## <a name="truncating-and-rounding-results"></a>Truncando e arredondando resultados
Ao converter expressões de caractere ou binárias (**char**, **nchar**, **nvarchar**, **varchar**, **binary** ou **varbinary**) em uma expressão de um tipo de dados diferente, os dados podem ser truncados, exibidos apenas parcialmente ou um erro é retornado porque o resultado é curto demais para ser exibido. Conversões em **char**, **varchar**, **nchar**, **nvarchar**, **binary** e **varbinary** são truncadas, com exceção das conversões mostradas na tabela a seguir.
  
|De tipo de dados|Em tipo de dados|Resultado|  
|---|---|---|
|**int**, **smallint** ou **tinyint**|**char**|*|  
||**varchar**|*|  
||**nchar**|E|  
||**nvarchar**|E|  
|**money**, **smallmoney**, **numeric**, **decimal**, **float** ou **real**|**char**|E|  
||**varchar**|E|  
||**nchar**|E|  
||**nvarchar**|E|  
  
\* = O tamanho do resultado é curto demais para ser exibido. E = Um erro é retornado porque o comprimento de resultado é curto demais para ser exibido.
  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] garante que apenas conversões de ida e volta, conversões que convertem um tipo de dados original e, em seguida, novamente no tipo de dados original, geram os mesmos valores de versão para versão. O exemplo a seguir mostra essa conversão de ida e volta:
  
```sql
DECLARE @myval decimal (5, 2);  
SET @myval = 193.57;  
SELECT CAST(CAST(@myval AS varbinary(20)) AS decimal(10,5));  
-- Or, using CONVERT  
SELECT CONVERT(decimal(10,5), CONVERT(varbinary(20), @myval));  
```  
  
> [!NOTE]  
>  Não tente construir valores **binary** e depois convertê-los em um tipo de dados da categoria de tipo de dados numeric. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não assegura que o resultado de uma conversão de tipo de dados **decimal** ou **numeric** em **binary** será igual entre as versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
O exemplo a seguir mostra uma expressão resultante que é muito pequena para ser exibida.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT p.FirstName, p.LastName, SUBSTRING(p.Title, 1, 25) AS Title,
    CAST(e.SickLeaveHours AS char(1)) AS [Sick Leave]  
FROM HumanResources.Employee e JOIN Person.Person p 
    ON e.BusinessEntityID = p.BusinessEntityID  
WHERE NOT e.BusinessEntityID >5;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```   
FirstName   LastName      Title   Sick Leave
---------   ------------- ------- --------`
Ken         Sanchez       NULL   *
Terri       Duffy         NULL   *
Roberto     Tamburello    NULL   *
Rob         Walters       NULL   *
Gail        Erickson      Ms.    *
(5 row(s) affected)  
```
  
Ao converter tipos de dados que têm casas decimais diferentes, às vezes o valor resultante é truncado e em outras vezes ele é arredondado. A tabela a seguir mostra o comportamento.
  
|De|Para|Comportamento|  
|---|---|---|
|**numeric**|**numeric**|Arredondamento|  
|**numeric**|**int**|Truncar|  
|**numeric**|**money**|Arredondamento|  
|**money**|**int**|Arredondamento|  
|**money**|**numeric**|Arredondamento|  
|**float**|**int**|Truncar|  
|**float**|**numeric**|Arredondamento<br /><br /> A conversão de valores **float** que usam notação científica para **decimal** ou **numeric** é restrita a valores de precisão de 17 dígitos apenas. Qualquer valor com precisão mais alto que 17 rodadas para zero.|  
|**float**|**datetime**|Arredondamento|  
|**datetime**|**int**|Arredondamento|  
  
Por exemplo, os valores 10,6496 e -10,6496 podem ser truncados ou arredondados durante a conversão em tipos **int** ou **numeric**:
  
```sql
SELECT  CAST(10.6496 AS int) as trunc1,
         CAST(-10.6496 AS int) as trunc2,
         CAST(10.6496 AS numeric) as round1,
         CAST(-10.6496 AS numeric) as round2;
 ```
Os resultados da consulta são mostrados na seguinte tabela:
 
|trunc1|trunc2|round1|round2|
|---|---|---|---|
|10|-10|11|-11|
 
Ao converter tipos de dados em que o tipo de dados de destino tem menos casas decimais do que o tipo de dados de origem, o valor é arredondado. Por exemplo, o resultado da seguinte conversão é `$10.3497`:
  
`SELECT CAST(10.3496847 AS money);`
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna uma mensagem de erro quando dados não numéricos **char**, **nchar**, **varchar** ou **nvarchar** são convertidos em **int**, **float**, **numeric** ou **decimal**. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também retorna erro quando uma cadeia de caracteres vazia (" ") é convertida em **numeric** ou **decimal**.
  
## <a name="certain-datetime-conversions-are-nondeterministic"></a>Algumas conversões de datetime não são determinísticas
A tabela a seguir lista os estilos para os quais a conversão de cadeia de caracteres em datetime é não determinística.
  
|||  
|-|-|  
|Todos os estilos inferiores a 100<sup>1</sup>|106|  
|107|109|  
|113|130|  
  
<sup>1</sup> Com exceção dos estilos 20 e 21
  
## <a name="supplementary-characters-surrogate-pairs"></a>Caracteres suplementares (pares alternativos)
Começando pelo [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], se você usar agrupamentos SC (caracteres suplementares), uma operação CAST de **nchar** ou **nvarchar** em um tipo **nchar** ou **nvarchar** de tamanho menor não será truncada dentro de um par alternativo; ela será truncada antes do caractere suplementar. Por exemplo, o fragmento de código a seguir deixa `@x` que contém só `'ab'`. Não há espaço suficiente para conter o caractere suplementar.
  
```sql
DECLARE @x NVARCHAR(10) = 'ab' + NCHAR(0x10000);  
SELECT CAST (@x AS NVARCHAR(3));  
```  
  
Ao usar agrupamentos SC, o comportamento de `CONVERT` é análogo ao comportamento de `CAST`.
  
## <a name="compatibility-support"></a>Suporte de compatibilidade
Nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o estilo padrão das operações CAST e CONVERT nos tipos de dados **time** e **datetime2** é 121, exceto quando um dos tipos é usado em uma expressão de coluna computada. Para colunas computadas, o estilo padrão é 0. Esse comportamento afeta as colunas computadas quando são criadas, usadas em consultas que envolvam parametrização automática ou usadas em definições de restrição.
  
No nível de compatibilidade 110 e superior, o estilo padrão das operações CAST e CONVERT nos tipos de dados **time** e **datetime2** sempre é 121. Se a sua consulta depender do comportamento antigo, use um nível de compatibilidade inferior a 110 ou especifique explicitamente o estilo 0 na consulta afetada.
  
A atualização do banco de dados para o nível de compatibilidade 110 e superior não alterará os dados de usuário que foram armazenados em disco. Você deve corrigir esses dados manualmente conforme apropriado. Por exemplo, se você usou SELECT INTO para criar uma tabela com base em uma fonte que continha uma expressão de coluna computada descrita acima, os dados (usando o estilo 0) serão armazenados, em vez da própria definição de coluna computada. Você precisará atualizar manualmente esses dados para que coincidam com o estilo 121.
  
## <a name="BKMK_examples"></a> Exemplos  
  
### <a name="a-using-both-cast-and-convert"></a>A. Usando CAST e CONVERT  
Cada exemplo recupera o nome dos produtos que têm um `3` no primeiro dígito de seu preço de lista e converte seu `ListPrice` em `int`.
  
```sql
-- Use CAST  
USE AdventureWorks2012;  
GO  
SELECT SUBSTRING(Name, 1, 30) AS ProductName, ListPrice  
FROM Production.Product  
WHERE CAST(ListPrice AS int) LIKE '3%';  
GO  
  
-- Use CONVERT.  
USE AdventureWorks2012;  
GO  
SELECT SUBSTRING(Name, 1, 30) AS ProductName, ListPrice  
FROM Production.Product  
WHERE CONVERT(int, ListPrice) LIKE '3%';  
GO  
```  
  
### <a name="b-using-cast-with-arithmetic-operators"></a>B. Usando CAST com operadores aritméticos  
O exemplo a seguir calcula uma única computação da coluna (`Computed`) dividindo as vendas totais acumuladas no ano (`SalesYTD`) pela porcentagem de comissão (`CommissionPCT`). Esse resultado é convertido em um tipo de dados `int` depois de ser arredondado para o número inteiro mais próximo.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT CAST(ROUND(SalesYTD/CommissionPCT, 0) AS int) AS Computed  
FROM Sales.SalesPerson   
WHERE CommissionPCT != 0;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
```  
Computed
------
379753754
346698349
257144242
176493899
281101272
0  
301872549
212623750
298948202
250784119
239246890
101664220
124511336
97688107
(14 row(s) affected)  
```  
  
### <a name="c-using-cast-to-concatenate"></a>C. Usando CAST para concatenar  
O exemplo a seguir concatena expressões de não caractere usando CAST. Usa o AdventureWorksDW.
  
```sql
SELECT 'The list price is ' + CAST(ListPrice AS varchar(12)) AS ListPrice  
FROM dbo.DimProduct  
WHERE ListPrice BETWEEN 350.00 AND 400.00;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
ListPrice
------------------------
The list price is 357.06
The list price is 364.09
The list price is 364.09
The list price is 364.09
The list price is 364.09  
```  
  
### <a name="d-using-cast-to-produce-more-readable-text"></a>D. Usando CAST para produzir texto mais legível  
O exemplo a seguir usa CAST na lista SELECT para converter a coluna `Name` em uma coluna **char(10)**. Usa o AdventureWorksDW.
  
```sql
SELECT DISTINCT CAST(EnglishProductName AS char(10)) AS Name, ListPrice  
FROM dbo.DimProduct  
WHERE EnglishProductName LIKE 'Long-Sleeve Logo Jersey, M';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Name        ListPrice
----------  ---------
Long-Sleev  31.2437
Long-Sleev  32.4935
Long-Sleev  49.99  
```  
  
### <a name="e-using-cast-with-the-like-clause"></a>E. Usando CAST com a cláusula LIKE  
O exemplo a seguir converte a coluna `money` `SalesYTD` em uma `int` e, em seguida, em uma coluna `char(20)` de forma que ela possa ser usada com a cláusula `LIKE`.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT p.FirstName, p.LastName, s.SalesYTD, s.BusinessEntityID  
FROM Person.Person AS p   
JOIN Sales.SalesPerson AS s   
    ON p.BusinessEntityID = s.BusinessEntityID  
WHERE CAST(CAST(s.SalesYTD AS int) AS char(20)) LIKE '2%';  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
FirstName        LastName            SalesYTD         BusinessEntityID
---------------- ------------------- ---------------- -------------
Tsvi             Reiter              2811012.7151      279
Syed             Abbas               219088.8836       288
Rachel           Valdez              2241204.0424      289
(3 row(s) affected)  
```
  
### <a name="f-using-convert-or-cast-with-typed-xml"></a>F. Usando CONVERT ou CAST com XML com tipo  
Veja a seguir vários exemplos que mostram como usar CONVERT para fazer uma conversão em XML tipado usando [Tipo de dados e colunas XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-type-and-columns-sql-server.md).
  
Este exemplo converte uma cadeia de caracteres com espaço em branco, texto e marcação em XML com tipo e remove todos os espaços em branco insignificantes (espaço em branco delimitador entre nós):
  
```sql
CONVERT(XML, '<root><child/></root>')  
```  
  
Este exemplo converte uma cadeia de caracteres semelhante com espaço em branco, texto e marcação em XML com tipo e preserva todos os espaços em branco insignificantes (espaço em branco delimitador entre nós):
  
```sql
CONVERT(XML, '<root>          <child/>         </root>', 1)  
```  
  
Este exemplo converte uma cadeia de caracteres com espaço branco, texto e marcação em XML com tipo:
  
```sql
CAST('<Name><FName>Carol</FName><LName>Elliot</LName></Name>'  AS XML)  
```  
  
Para obter mais exemplos, consulte [Criar instâncias de dados XML](../../relational-databases/xml/create-instances-of-xml-data.md).
  
### <a name="g-using-cast-and-convert-with-datetime-data"></a>G. Usando CAST e CONVERT com dados datetime  
O exemplo a seguir exibe a data e a hora atuais, usa `CAST` para alterar a data e a hora atuais em um tipo de dados de caracteres e, em seguida, usa `CONVERT` para exibir a data e a hora no formato `ISO 8901`.
  
```sql
SELECT   
   GETDATE() AS UnconvertedDateTime,  
   CAST(GETDATE() AS nvarchar(30)) AS UsingCast,  
   CONVERT(nvarchar(30), GETDATE(), 126) AS UsingConvertTo_ISO8601  ;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
UnconvertedDateTime     UsingCast              UsingConvertTo_ISO8601
----------------------- ---------------------- ------------------------------
2006-04-18 09:58:04.570 Apr 18 2006  9:58AM    2006-04-18T09:58:04.570
(1 row(s) affected)  
```
  
O exemplo a seguir é aproximadamente o oposto do exemplo anterior. O exemplo exibe uma data e hora como dados de caracteres, usa `CAST` para alterar os dados de caracteres no tipo de dados `datetime` e, em seguida, usa `CONVERT` para alterar os dados de caracteres no tipo de dados `datetime`.
  
```sql
SELECT   
   '2006-04-25T15:50:59.997' AS UnconvertedText,  
   CAST('2006-04-25T15:50:59.997' AS datetime) AS UsingCast,  
   CONVERT(datetime, '2006-04-25T15:50:59.997', 126) AS UsingConvertFrom_ISO8601 ;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
UnconvertedText         UsingCast               UsingConvertFrom_ISO8601
----------------------- ----------------------- ------------------------
2006-04-25T15:50:59.997 2006-04-25 15:50:59.997 2006-04-25 15:50:59.997
(1 row(s) affected)  
```
  
### <a name="h-using-convert-with-binary-and-character-data"></a>H. Usando CONVERT com dados binários e de caractere  
Os exemplos a seguir mostram os resultados da conversão de dados binários e de caractere usando estilos diferentes.
  
```sql
--Convert the binary value 0x4E616d65 to a character value.  
SELECT CONVERT(char(8), 0x4E616d65, 0) AS [Style 0, binary to character];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 0, binary to character
----------------------------
Name  
(1 row(s) affected)  
```
 
O exemplo a seguir mostra como o Style 1 pode forçar o truncamento do resultado. O truncamento é causado pela inclusão dos caracteres 0x no resultado.  
```sql  
SELECT CONVERT(char(8), 0x4E616d65, 1) AS [Style 1, binary to character];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 1, binary to character
------------------------------
0x4E616D
(1 row(s) affected)  
```  
 
O exemplo a seguir mostra que Style 2 não trunca o resultado porque os caracteres 0x não são incluídos no resultado.  
```sql  
SELECT CONVERT(char(8), 0x4E616d65, 2) AS [Style 2, binary to character];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 2, binary to character
------------------------------
4E616D65
(1 row(s) affected)  
```
  
Converta o valor de caractere 'Name' em um valor binário.  
```sql
SELECT CONVERT(binary(8), 'Name', 0) AS [Style 0, character to binary];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 0, character to binary
----------------------------
0x4E616D6500000000
(1 row(s) affected)  
```
  
```sql
SELECT CONVERT(binary(4), '0x4E616D65', 1) AS [Style 1, character to binary];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 1, character to binary
---------------------------- 
0x4E616D65
(1 row(s) affected)  
```  

```sql
SELECT CONVERT(binary(4), '4E616D65', 2) AS [Style 2, character to binary];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 2, character to binary  
----------------------------------  
0x4E616D65
(1 row(s) affected)  
```  
  
### <a name="i-converting-date-and-time-data-types"></a>I. Convertendo os tipos de dados de data e hora  
O seguinte exemplo demonstra a conversão de data, hora e tipos de dados de datetime.
  
```sql
DECLARE @d1 date, @t1 time, @dt1 datetime;  
SET @d1 = GETDATE();  
SET @t1 = GETDATE();  
SET @dt1 = GETDATE();  
SET @d1 = GETDATE();  
-- When converting date to datetime the minutes portion becomes zero.  
SELECT @d1 AS [date], CAST (@d1 AS datetime) AS [date as datetime];  
-- When converting time to datetime the date portion becomes zero   
-- which converts to January 1, 1900.  
SELECT @t1 AS [time], CAST (@t1 AS datetime) AS [time as datetime];  
-- When converting datetime to date or time non-applicable portion is dropped.  
SELECT @dt1 AS [datetime], CAST (@dt1 AS date) AS [datetime as date], 
   CAST (@dt1 AS time) AS [datetime as time];  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="j-using-cast-and-convert"></a>J. Usando CAST e CONVERT  
Este exemplo recupera o nome dos produtos que têm um `3` no primeiro dígito de seu preço de lista e converte seu `ListPrice` em **int**. Usa o AdventureWorksDW.
  
```sql
SELECT EnglishProductName AS ProductName, ListPrice  
FROM dbo.DimProduct  
WHERE CAST(ListPrice AS int) LIKE '3%';  
```  
  
Este exemplo mostra a mesma consulta, usando CONVERT em vez de CAST. Usa o AdventureWorksDW.
  
```sql
SELECT EnglishProductName AS ProductName, ListPrice  
FROM dbo.DimProduct  
WHERE CONVERT(int, ListPrice) LIKE '3%';  
```  
  
### <a name="k-using-cast-with-arithmetic-operators"></a>K. Usando CAST com operadores aritméticos  
O exemplo a seguir faz um cálculo de coluna única, dividindo o preço unitário do produto (`UnitPrice`) pelo percentual de desconto (`UnitPriceDiscountPct`). Esse resultado é convertido em um tipo de dados `int` depois de ser arredondado para o número inteiro mais próximo. Usa o AdventureWorksDW.
  
```sql
SELECT ProductKey, UnitPrice,UnitPriceDiscountPct,  
       CAST(ROUND (UnitPrice*UnitPriceDiscountPct,0) AS int) AS DiscountPrice  
FROM dbo.FactResellerSales  
WHERE SalesOrderNumber = 'SO47355'   
      AND UnitPriceDiscountPct > .02;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
ProductKey  UnitPrice  UnitPriceDiscountPct  DiscountPrice
----------  ---------  --------------------  -------------
323         430.6445   0.05                  22
213         18.5043    0.05                  1
456         37.4950    0.10                  4
456         37.4950    0.10                  4
216         18.5043    0.05                  1  
```  
  
### <a name="l-using-cast-with-the-like-clause"></a>L. Usando CAST com a cláusula LIKE  
O exemplo a seguir converte o `ListPrice` da coluna **money** em um tipo **int** e, em seguida, em um tipo **char(20)**, de modo que ele possa ser usado com a cláusula LIKE. Usa o AdventureWorksDW.
  
```sql
SELECT EnglishProductName AS Name, ListPrice  
FROM dbo.DimProduct  
WHERE CAST(CAST(ListPrice AS int) AS char(20)) LIKE '2%';  
```  
  
### <a name="m-using-cast-and-convert-with-datetime-data"></a>M. Usando CAST e CONVERT com dados datetime  
O exemplo a seguir exibe a data e a hora atuais, usa CAST para alterar a data e a hora atuais em um tipo de dados de caractere e, em seguida, usa CONVERT para exibir a data e a hora no formato ISO 8601. Usa o AdventureWorksDW.
  
```sql
SELECT TOP(1)  
   SYSDATETIME() AS UnconvertedDateTime,  
   CAST(SYSDATETIME() AS nvarchar(30)) AS UsingCast,  
   CONVERT(nvarchar(30), SYSDATETIME(), 126) AS UsingConvertTo_ISO8601  
FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
UnconvertedDateTime     UsingCast                     UsingConvertTo_ISO8601  
---------------------   ---------------------------   ---------------------------  
07/20/2010 1:44:31 PM   2010-07-20 13:44:31.5879025   2010-07-20T13:44:31.5879025  
```  
  
O exemplo a seguir é aproximadamente o oposto do exemplo anterior. O exemplo exibe uma data e hora como dados de caractere, usa CAST para alterar os dados de caractere para o tipo de dados **datetime** e, em seguida, usa CONVERT para alterar os dados de caractere para o tipo de dados **datetime**. Usa o AdventureWorksDW.
  
```sql
SELECT TOP(1)   
   '2010-07-25T13:50:38.544' AS UnconvertedText,  
CAST('2010-07-25T13:50:38.544' AS datetime) AS UsingCast,  
   CONVERT(datetime, '2010-07-25T13:50:38.544', 126) AS UsingConvertFrom_ISO8601  
FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
UnconvertedText         UsingCast               UsingConvertFrom_ISO8601
----------------------- ----------------------- ------------------------
2010-07-25T13:50:38.544 07/25/2010 1:50:38 PM   07/25/2010 1:50:38 PM  
```  
  
## <a name="see-also"></a>Confira também
 [Conversão de tipo de dados &#40;Mecanismo de Banco de Dados&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
 [FORMAT &#40;Transact-SQL&#41;](../../t-sql/functions/format-transact-sql.md)  
 [STR &#40;Transact-SQL&#41;](../../t-sql/functions/str-transact-sql.md)  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
 [Funções do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
 [Gravar instruções Transact-SQL internacionais](../../relational-databases/collations/write-international-transact-sql-statements.md)
  
