---
title: CAST e CONVERT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/08/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: b7f2f78bbda485de979c76076404f35122b61277
ms.contentlocale: pt-br
ms.lasthandoff: 10/17/2017

---
# <a name="cast-and-convert-transact-sql"></a>CAST e CONVERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Converte uma expressão de um tipo de dados para outro.  
Por exemplo, os exemplos a seguir alterar o tipo de dados de entrada, em dois outros tipos de dados, com diferentes níveis de precisão.
```sql  
SELECT 9.5 AS Original, CAST(9.5 AS int) AS int, 
    CAST(9.5 AS decimal(6,4)) AS decimal;
SELECT 9.5 AS Original, CONVERT(int, 9.5) AS int, 
    CONVERT(decimal(6,4), 9.5) AS decimal;
```  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
|Original   |int    |decimal |  
|----|----|----|  
|9.5 |9 |9.5000 |  

> [!TIP]
> Muitos [exemplos](#BKMK_examples) estão na parte inferior deste tópico.  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
-- Syntax for CAST:  
CAST ( expression AS data_type [ ( length ) ] )  
  
-- Syntax for CONVERT:  
CONVERT ( data_type [ ( length ) ] , expression [ , style ] )  
```  
  
## <a name="arguments"></a>Argumentos  
*expressão*  
É qualquer [expressão](../../t-sql/language-elements/expressions-transact-sql.md).
  
*data_type*  
É o tipo de dados de destino. Isso inclui **xml**, **bigint**, e **sql_variant**. Tipos de dados alias não podem ser usados.
  
*length*  
É um inteiro opcional que especifica o comprimento do tipo de dados de destino. O valor padrão é 30.
  
*estilo*  
É uma expressão de inteiro que especifica como a função CONVERT converter *expressão*. Se o estilo for NULL, NULL será retornado. O intervalo é determinado pelo *data_type*. 
  
## <a name="return-types"></a>Tipos de retorno
Retorna *expressão* convertido *data_type*.

## <a name="date-and-time-styles"></a>Estilos de data e hora  
Quando *expressão* é um tipo de dados de data ou hora, *estilo* pode ser um dos valores mostrados na tabela a seguir. Outros valores são processados como 0. Começando com [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], os únicos estilos que têm suporte para a conversão de data e hora tipos para **datetimeoffset** são 0 ou 1. Todos os outros estilos de conversão retornam erro 9809.
  
>  [!NOTE]  
>  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tem suporte para o formato de data em árabe usando o algoritmo kuwaitiano.
  
|Sem século (AA) (<sup>1</sup>)|Com século (aaaa)|Standard|Entrada/saída (<sup>3</sup>)|  
|---|---|--|---|
|-|**0** ou **100** (<sup>1,</sup><sup>2</sup>)|Padrão para datetime e smalldatetime|mês dd aaaa hh:miAM (ou PM)|  
|**1**|**101**|EUA|1 = mm/dd/aa<br /> 101 = mm/dd/aaaa|  
|**2**|**102**|ANSI|2 = aa.mm.dd<br /> 102 = aaaa.mm.dd|  
|**3**|**103**|Britânico/francês|3 = dd/mm/aa<br /> 103 = dd/mm/aaaa|  
|**4**|**104**|Alemão|4 = dd.mm.aa<br /> 104 = dd.mm.aaaa|  
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
|-|**126** (<sup>4</sup>)|ISO8601|aaaa-mm-ddThh:mi:ss.mmm (sem espaços)<br /> Observação: Quando o valor de milissegundos (mmm) for 0, o valor de milissegundos não é exibido. Por exemplo, o valor '2012-11-07T18:26:20.000 é exibido como '2012-11-07T18:26:20'.|  
|-|**127**(<sup>6, 7</sup>)|ISO8601 com fuso horário Z.|aaaa-mm-ddThh:mi:ss.mmmZ (sem espaços)<br /> Observação: Quando o valor de milissegundos (mmm) for 0, o valor de milissegundos não é exibido. Por exemplo, o valor '2012-11-07T18:26:20.000 é exibido como '2012-11-07T18:26:20'.|  
|-|**130** (<sup>1,</sup><sup>2</sup>)|Islâmico (<sup>5</sup>)|dd mmm aaaa hh:mi:ss:mmmAM<br /> Neste estilo, mon representa uma representação unicode Hijri de vários tokens do nome completo do mês. Esse valor não sejam renderizadas corretamente em um padrão instalação US do SSMS.|  
|-|**131** (<sup>2</sup>)|Islâmico (<sup>5</sup>)|dd/mm/aaaa hh:mi:ss:mmmAM|  
  
<sup>1</sup> esses valores de estilo retornam resultados não determinísticos. Incluem todos os estilos (aa) (sem século) e um subconjunto de estilos (aaaa) (com século).
  
<sup>2</sup> os valores padrão (*estilo** *0** ou **100**, **9** ou **109**, **13** ou **113**, **20** ou **120**, e **21** ou **121**) sempre retornam o século (AAAA).
  
<sup>3</sup> de entrada quando você converte em **datetime**; saída quando você converte em dados de caractere.
  
<sup>4</sup> projetados para uso XML. Para conversão de **datetime** ou **smalldatetime** para dados de caracteres, o formato de saída é conforme descrito na tabela anterior.
  
<sup>5</sup> islâmico é um sistema de calendário com muitas variações. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa o algoritmo kuwaitiano.
  
> [!IMPORTANT]  
>  Por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpreta anos de dois dígitos com base em um ano de corte de 2049. Isto é, o ano 49 de dois dígitos é interpretado como 2049 e o ano 50 de dois dígitos é interpretado como 1950. Muitos aplicativos cliente, como aqueles que se baseiam em objetos Automation, usam um ano de corte de 2030. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]fornece a opção de configuração de corte de ano de dois dígitos que altera o ano de corte usado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e permite tratamento consistente de datas. É recomendável especificar anos de quatro dígitos.  
  
<sup>6</sup> só tem suporte quando a conversão de dados de caractere para **datetime** ou **smalldatetime**. Quando dados de caracteres que representam somente data ou de componentes de hora são convertidos para o **datetime** ou **smalldatetime** tipos de dados, o componente de tempo não especificado é definido como 00:00:00.000 e o não especificado componente de data é definido como 1900-01-01.
  
<sup>7</sup>o indicador de fuso horário opcional, Z, é usado para tornar mais fácil mapear XML **datetime** valores que têm informações de fuso horário para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** valores que não contêm fuso . Z é o indicador de fuso horário UTC-0. Outros fusos horários são indicados com deslocamento de HH:MM na direção + ou -. Por exemplo: `2006-12-12T23:45:12-08:00`.
  
Quando você converte em dados de caractere **smalldatetime**, os estilos que incluem segundos ou milissegundos mostram zeros nessas posições. É possível truncar partes não desejadas da data ao converter de **datetime** ou **smalldatetime** valores usando adequados **char** ou **varchar** comprimento do tipo de dados.
  
Quando você converte em **datetimeoffset** de dados de caracteres com um estilo que inclui uma hora, um deslocamento de fuso horário é anexado ao resultado.
  
## <a name="float-and-real-styles"></a>estilos float e real
Quando *expressão* é **float** ou **real**, *estilo* pode ser um dos valores mostrados na tabela a seguir. Outros valores são processados como 0.
  
|Valor|Saída|  
|---|---|
|**0** (padrão)|Um máximo de 6 dígitos. Use em notação científica, quando apropriado.|  
|**1**|Sempre 8 dígitos. Use sempre em notação científica.|  
|**2**|Sempre 16 dígitos. Use sempre em notação científica.|  
|**3**|Sempre 17 dígitos. Use para conversão sem perdas. Com esse estilo, cada distinto float ou o valor real é garantido para converter uma cadeia de caracteres distintos.<br /> **Aplica-se a:** [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]e a partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].|  
|**126, 128, 129**|Incluído por razões herdadas e poderia ser preterido em uma versão futura.|  
  
## <a name="money-and-smallmoney-styles"></a>estilos Money e smallmoney
Quando *expressão* é **money** ou **smallmoney**, *estilo* pode ser um dos valores mostrados na tabela a seguir. Outros valores são processados como 0.
  
|Valor|Saída|  
|---|---|
|**0** (padrão)|Nenhuma vírgula a cada três dígitos à esquerda do ponto decimal e dois dígitos à direita do ponto decimal. Por exemplo, 4235.98.|  
|**1**|Vírgulas a cada três dígitos à esquerda do ponto decimal e dois dígitos à direita do ponto decimal. Por exemplo, 3,510.92.|  
|**2**|Nenhuma vírgula a cada três dígitos à esquerda do ponto decimal e quatro dígitos à direita do ponto decimal. Por exemplo, 4235.9819.|  
|**126**|Equivalente ao estilo 2 ao converter para char(n) ou varchar (n)|  
  
## <a name="xml-styles"></a>estilos XML
Quando *expressão* é **xml***, estilo* pode ser um dos valores mostrados na tabela a seguir. Outros valores são processados como 0.
  
|Valor|Saída|  
|---|---|
|**0** (padrão)|Use comportamento de análise padrão que descarta espaço em branco insignificante e não permite um subconjunto de DTD interno.<br /> **Observação:** ao converter para o **xml** tipo de dados, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] espaço em branco insignificante é tratado de maneira diferente no XML 1.0. Para obter mais informações, consulte [criar instâncias de dados XML](../../relational-databases/xml/create-instances-of-xml-data.md).|  
|**1**|Preserva espaço em branco insignificante. Essa configuração de estilo define o padrão **XML: space** tratamento se comporte da mesma como se **XML: space = "preserve"** foi especificado em vez disso.|  
|**2**|Habilita o processamento de subconjunto de DTD interno limitado.<br /><br /> Se habilitado, o servidor poderá usar as seguintes informações fornecidas em um subconjunto de DTD interno para executar operações de análise de não validação.<br /> -Padrões de atributos são aplicados.<br /> -Referências de entidade interno são resolvidas e expandidas.<br /> -O modelo de conteúdo DTD é verificado quanto a exatidão sintática.<br /> O analisador ignorará subconjuntos de DTD externos. Também não avalia a declaração XML para ver se o **autônomo** atributo é definido **Sim** ou **sem**, mas analisa a instância XML como se fosse um autônomo documento.|  
|**3**|Preserva espaço em branco insignificante e habilita processamento de subconjunto de DTD interno limitado.|  
  
## <a name="binary-styles"></a>Estilos binários
Quando *expressão* é **Binary**, **varbinary**, **char**, ou **varchar**, *estilo* pode ser um dos valores mostrados na tabela a seguir. Valores de estilo que não estão listados na tabela retornarão um erro.
  
|Valor|Saída|  
|---|---|
|**0** (padrão)|Converte caracteres ASCII em bytes binários ou bytes binários em caracteres ASCII. Cada caractere ou byte é convertido 1:1.<br /> Se o *data_type* é um tipo binário, os caracteres 0x serão adicionados à esquerda do resultado.|  
|**1**, **2**|Se o *data_type* é um tipo binário, a expressão deve ser uma expressão de caractere. O *expressão* deve ser composto de um número par de dígitos hexadecimais (0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F, a, b, c, d, e, f). Se o *estilo* for definido como 1 os caracteres 0x devem ser os dois primeiros caracteres na expressão. Se a expressão contiver um número de caracteres ímpar ou se algum dos caracteres for inválido, ocorrerá um erro.<br /> Se o comprimento da expressão convertida for maior que o comprimento do *data_type* o resultado será truncado à direita.<br /> Comprimento fixo *data_types* que são maiores do que o resultado convertido tem zeros adicionados à direita do resultado.<br /> Se o data_type for tipo de caractere, a expressão deve ser uma expressão de binária. Cada caractere binário é convertido em dois caracteres hexadecimais. Se o comprimento da expressão convertida for maior do que o *data_type* comprimento, ele será truncado à direita.<br /> Se o *data_type* é um tipo de caractere de tamanho fixo e o comprimento do resultado convertido for menor que o comprimento do *data_type*; espaços são adicionados à direita da expressão convertida para manter um mesmo número de dígitos hexadecimais.<br /> Os caracteres 0x serão adicionados à esquerda do resultado convertido para *estilo* 1.|  
  
## <a name="implicit-conversions"></a>Conversões implícitas
Conversões implícitas são conversões que ocorrem sem especificar a função CAST ou CONVERT. Conversões explícitas são as conversões que exigem que a função CAST ou CONVERT seja especificada. A ilustração a seguir mostra todas as conversões de tipos de dados explícitas e implícitas que são permitidas para tipos de dados fornecidos pelo sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Isso inclui **xml**, **bigint**, e **sql_variant**. Não há nenhuma conversão implícita na atribuição do **sql_variant** tipo de dados, mas não há conversão implícita em **sql_variant**.
  
> [!TIP]  
>  Este gráfico está disponível como um arquivo PDF para download no [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=35834).  
  
![Tabela de conversão de tipo de dados](../../t-sql/data-types/media/lrdatahd.png "tabela de conversão de tipo de dados")
  
Ao converter entre **datetimeoffset** e os tipos de caracteres **char**, **varchar**, **nchar**, e **nvarchar**  o fuso horário convertido parte do deslocamento deve ser sempre de dois dígitos para HH e MM, por exemplo, -08:00.
  
> [!NOTE]  
>  Como dados Unicode sempre usam um número par de bytes, tenha cuidado ao converter **binário** ou **varbinary** em Unicode ou suporte para tipos de dados. Por exemplo, a conversão a seguir não retorna um valor hexadecimal de 41. Ela retorna 4100: `SELECT CAST(CAST(0x41 AS nvarchar) AS varbinary)`.  
  
## <a name="large-value-data-types"></a>Tipos de dados de valor grande
Tipos de dados de valor grande exibem o mesmo comportamento de conversão implícita e explícita que suas contrapartes menores, especificamente o **varchar**, **nvarchar** e **varbinary**tipos de dados. Porém, você deve considerar as seguintes diretrizes:
-   Conversão de **imagem** para **varbinary (max)** e vice-versa é uma conversão implícita, e também são as conversões entre **texto** e **varchar (max)**, e **ntext** e **nvarchar (max)**.  
-   Tipos de conversão de dados de valor grande, como **varchar (max)**, digite um dados de contraparte menor, como **varchar**, é uma conversão implícita, mas o truncamento ocorre se o valor grande é muito grande para o comprimento especificado do tipo de dados menor.  
-   Conversão de **varchar**, **nvarchar**, ou **varbinary** para os dados de valor grande correspondentes tipos é executada implicitamente.  
-   Conversão do **sql_variant** tipo de dados para os tipos de dados de valor grande é uma conversão explícita.  
-   Tipos de dados de valor grande não podem ser convertidos para o **sql_variant** tipo de dados.  
  
Para obter mais informações sobre como converter o **xml** tipo de dados, consulte [criar instâncias de dados XML](../../relational-databases/xml/create-instances-of-xml-data.md).
  
## <a name="xml-data-type"></a>tipo de dados xml
Quando você explicitamente ou implicitamente convertido a **xml** tipo de dados para uma cadeia de caracteres ou tipo de dados binário, o conteúdo do **xml** tipo de dados é serializado com base em um conjunto de regras. Para obter informações sobre essas regras, consulte [definem os dados de serialização de XML](../../relational-databases/xml/define-the-serialization-of-xml-data.md). Para obter informações sobre como converter de outros tipos de dados para o **xml** tipo de dados, consulte [criar instâncias de dados XML](../../relational-databases/xml/create-instances-of-xml-data.md).
  
## <a name="text-and-image-data-types"></a>tipos de dados de texto e imagem
Não há suporte para conversão de tipo de dados automática para o **texto** e **imagem** tipos de dados. Você pode converter explicitamente **texto** dados para dados de caracteres, e **imagem** dados **binário** ou **varbinary**, mas o comprimento máximo é 8000 bytes. Se você tentar uma conversão incorreta, como a conversão de uma expressão de caractere que inclua letras para um **int**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna uma mensagem de erro.
  
## <a name="output-collation"></a>Agrupamento da saída  
Quando a saída de CAST ou CONVERT for uma cadeia de caracteres e a entrada também for uma cadeia de caracteres, a saída terá o mesmo agrupamento e o mesmo rótulo de agrupamento que a entrada. Se a entrada não for uma cadeia de caracteres, a saída terá o agrupamento padrão do banco de dados e um rótulo de agrupamento de padrão coercível. Para obter mais informações, consulte [precedência de agrupamento &#40; Transact-SQL &#41; ](../../t-sql/statements/collation-precedence-transact-sql.md).
  
Para atribuir um agrupamento diferente à saída, aplique a cláusula COLLATE à expressão do resultado da função CAST ou CONVERT. Por exemplo:
  
`SELECT CAST('abc' AS varchar(5)) COLLATE French_CS_AS`
  
## <a name="truncating-and-rounding-results"></a>Truncando e arredondando resultados
Quando você converte caracteres ou expressões binárias (**char**, **nchar**, **nvarchar**, **varchar**, **binário**, ou **varbinary**) para uma expressão de um tipo de dados diferente, dados podem ser truncados, exibidos apenas parcialmente ou um erro será retornado como o resultado é curto demais para ser exibido. Conversões para **char**, **varchar**, **nchar**, **nvarchar**, **binário**, e  **varbinary** são truncados, com exceção das conversões mostradas na tabela a seguir.
  
|De tipo de dados|Em tipo de dados|Resultado|  
|---|---|---|
|**int**, **smallint**, ou **tinyint**|**char**|*|  
||**varchar**|*|  
||**nchar**|E|  
||**nvarchar**|E|  
|**Money**, **smallmoney**, **numérico**, **decimal**, **float**, ou **real**|**char**|E|  
||**varchar**|E|  
||**nchar**|E|  
||**nvarchar**|E|  
  
\*= O comprimento do resultado muito curto para ser exibido. E = Um erro é retornado porque o comprimento de resultado é curto demais para ser exibido.
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]garante que apenas conversões de ida e volta, conversões de convertem um tipo de dados de seu tipo de dados original e voltar novamente, geram os mesmos valores de versão para versão. O exemplo a seguir mostra essa conversão de ida e volta:
  
```sql
DECLARE @myval decimal (5, 2);  
SET @myval = 193.57;  
SELECT CAST(CAST(@myval AS varbinary(20)) AS decimal(10,5));  
-- Or, using CONVERT  
SELECT CONVERT(decimal(10,5), CONVERT(varbinary(20), @myval));  
```  
  
> [!NOTE]  
>  Não tente construir **binário** valores e, em seguida, convertê-los para um tipo de dados da categoria de tipo de dados numéricos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]não garante que o resultado de uma **decimal** ou **numérico** conversão para tipo de dados **binário** será igual entre versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
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
|**float**|**numeric**|Arredondamento<br /><br /> Conversão de **float** valores que usam notação científica para **decimal** ou **numérico** é restrita a valores de precisão de 17 dígitos apenas. Qualquer valor com precisão mais alto que 17 rodadas para zero.|  
|**float**|**datetime**|Arredondamento|  
|**datetime**|**int**|Arredondamento|  
  
Por exemplo, os valores 10.6496 e-10.6496 podem ser truncados ou arredondados durante a conversão para **int** ou **numérico** tipos:
  
```sql
SELECT  CAST(10.6496 AS int) as trunc1,
         CAST(-10.6496 AS int) as trunc2,
         CAST(10.6496 AS numeric) as round1,
         CAST(-10.6496 AS numeric) as round2;
 ```
Resultados da consulta são mostrados na tabela a seguir:
 
|trunc1|trunc2|round1|round2|
|---|---|---|---|
|10|-10|11|-11|
 
Ao converter tipos de dados em que o tipo de dados de destino tem menos casas decimais do que o tipo de dados de origem, o valor é arredondado. Por exemplo, o resultado da seguinte conversão é `$10.3497`:
  
`SELECT CAST(10.3496847 AS money);`
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Retorna uma mensagem de erro quando dados não numéricos **char**, **nchar**, **varchar**, ou **nvarchar** dados são convertidos em **int** , **float**, **numérico**, ou **decimal**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]também retorna um erro quando uma cadeia de caracteres vazia ("") é convertido em **numérico** ou **decimal**.
  
## <a name="certain-datetime-conversions-are-nondeterministic"></a>Determinadas conversões de datetime são não determinísticas
A tabela a seguir lista os estilos para os quais a conversão de cadeia de caracteres em datetime é não determinística.
  
|||  
|-|-|  
|Todos os estilos inferiores a 100<sup>1</sup>|106|  
|107|109|  
|113|130|  
  
<sup>1</sup> com exceção dos estilos 20 e 21
  
## <a name="supplementary-characters-surrogate-pairs"></a>Caracteres suplementares (pares substitutos)
A partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], se você usar agrupamentos de caracteres suplementares (SC), uma operação de CONVERSÃO de **nchar** ou **nvarchar** para um **nchar** ou  **nvarchar** tipo de comprimento menor não truncará dentro de um par substituto; truncará antes do caractere suplementar. Por exemplo, o fragmento de código a seguir deixa `@x` que contém só `'ab'`. Não há espaço suficiente para conter o caractere suplementar.
  
```sql
DECLARE @x NVARCHAR(10) = 'ab' + NCHAR(0x10000);  
SELECT CAST (@x AS NVARCHAR(3));  
```  
  
Ao usar agrupamentos SC, o comportamento de `CONVERT` é análogo ao comportamento de `CAST`.
  
## <a name="compatibility-support"></a>Suporte de compatibilidade
Em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o estilo padrão de operações CAST e CONVERT nos **tempo** e **datetime2** tipos de dados é 121, exceto quando o tipo é usado em uma expressão de coluna computada. Para colunas computadas, o estilo padrão é 0. Esse comportamento afeta as colunas computadas quando são criadas, usadas em consultas que envolvam parametrização automática ou usadas em definições de restrição.
  
No nível de compatibilidade 110 e superior, o estilo padrão das operações CAST e CONVERT em **tempo** e **datetime2** tipos de dados sempre é 121. Se a sua consulta depender do comportamento antigo, use um nível de compatibilidade inferior a 110 ou especifique explicitamente o estilo 0 na consulta afetada.
  
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
O exemplo a seguir concatena expressões não são de caractere usando CONVERSÃO. Usa AdventureWorksDW.
  
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
O exemplo a seguir usa a CONVERSÃO na lista de seleção para converter o `Name` coluna para um **char (10)** coluna. Usa AdventureWorksDW.
  
```sql
SELECT DISTINCT CAST(EnglishProductName AS char(10)) AS Name, ListPrice  
FROM dbo.DimProduct  
WHERE EnglishProductName LIKE 'Long-Sleeve Logo Jersey, M';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Name        UnitPrice
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
FirstName        LastName            SalesYTD         SalesPersonID
---------------- ------------------- ---------------- -------------
Tsvi             Reiter              2811012.7151      279
Syed             Abbas               219088.8836       288
Rachel           Valdez              2241204.0424      289
(3 row(s) affected)  
```
  
### <a name="f-using-convert-or-cast-with-typed-xml"></a>F. Usando CONVERT ou CAST com XML com tipo  
A seguir estão alguns exemplos que mostram como usar CONVERT para converter em XML com tipo usando o [&#40; tipo de dados XML e colunas SQL Server &#41; ](../../relational-databases/xml/xml-data-type-and-columns-sql-server.md).
  
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
  
Para obter mais exemplos, consulte [criar instâncias de dados XML](../../relational-databases/xml/create-instances-of-xml-data.md).
  
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
 
O exemplo a seguir mostra como o estilo 1 pode forçar o resultado a ser truncado. O truncamento é causado por incluir os caracteres 0x no resultado.  
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
 
O exemplo a seguir mostra que o resultado não truncar o estilo 2 porque os caracteres 0x não são incluídos no resultado.  
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
  
Converta o valor do caractere 'Name' para um valor binário.  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="j-using-cast-and-convert"></a>J. Usando CAST e CONVERT  
Este exemplo recupera o nome do produto para os produtos que têm uma `3` no primeiro dígito de preço da lista e converte seu `ListPrice` para **int**. Usa AdventureWorksDW.
  
```sql
SELECT EnglishProductName AS ProductName, ListPrice  
FROM dbo.DimProduct  
WHERE CAST(ListPrice AS int) LIKE '3%';  
```  
  
Este exemplo mostra a mesma consulta, usando CONVERT em vez de CAST. Usa AdventureWorksDW.
  
```sql
SELECT EnglishProductName AS ProductName, ListPrice  
FROM dbo.DimProduct  
WHERE CONVERT(int, ListPrice) LIKE '3%';  
```  
  
### <a name="k-using-cast-with-arithmetic-operators"></a>K. Usando CAST com operadores aritméticos  
O exemplo a seguir calcula uma computação de coluna única, dividindo o preço de unidade do produto (`UnitPrice`) pela porcentagem de desconto (`UnitPriceDiscountPct`). Esse resultado é convertido em um tipo de dados `int` depois de ser arredondado para o número inteiro mais próximo. Usa AdventureWorksDW.
  
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
O exemplo a seguir converte a **money** coluna `ListPrice` para um **int** tipo e, em seguida, para um **char(20)** tipo de forma que ele pode ser usado com a cláusula LIKE. Usa AdventureWorksDW.
  
```sql
SELECT EnglishProductName AS Name, ListPrice  
FROM dbo.DimProduct  
WHERE CAST(CAST(ListPrice AS int) AS char(20)) LIKE '2%';  
```  
  
### <a name="m-using-cast-and-convert-with-datetime-data"></a>M. Usando CAST e CONVERT com dados datetime  
O exemplo a seguir exibe a data e hora atuais, usa a CONVERSÃO para alterar a data e hora atuais para um tipo de dados de caractere, e, em seguida, usa CONVERT exibe a data e hora no formato ISO 8601. Usa AdventureWorksDW.
  
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
  
O exemplo a seguir é aproximadamente o oposto do exemplo anterior. O exemplo exibe uma data e hora como dados de caracteres, usa a CONVERSÃO para alterar os dados de caractere para a **datetime** tipo de dados e, em seguida, usa CONVERT para alterar os dados de caracteres para o **datetime** tipo de dados. Usa AdventureWorksDW.
  
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
  
## <a name="see-also"></a>Consulte também
[Conversão de tipo de dados &#40; mecanismo de banco de dados &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
[Funções do sistema &#40; Transact-SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
[Gravar instruções Transact-SQL internacionais](../../relational-databases/collations/write-international-transact-sql-statements.md)
  

