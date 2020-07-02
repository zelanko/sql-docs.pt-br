---
title: Tipos de dados XPath (SQLXML)
description: Saiba mais sobre os tipos de dados XPath no SQLXML 4,0 e como eles se comparam aos tipos de dados Microsoft SQL Server e XSD (esquema XML).
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- mapping XDR types to XPath types [SQLXML]
- data types [XPath]
- arithmetic operators
- mapping data types [SQLXML]
- relational operators [SQLXML]
- node-set [SQLXML]
- data types [SQLXML], XPath
- XPath operators [SQLXML]
- XDR data type [SQLXML]
- equality operators [SQLXML]
- XPath conversions [SQLXML]
- converting data types [SQLXML]
- Boolean operators
- XPath queries [SQLXML], data types
- XPath data types [SQLXML]
- operators [SQLXML]
ms.assetid: a90374bf-406f-4384-ba81-59478017db68
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: eade5e3328993176f8795d27e511902a42468192
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85764868"
---
# <a name="xpath-data-types-sqlxml-40"></a>Tipos de dados XPath (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], XPath e XSD (esquema XML) têm tipos de dados muito diferentes. Por exemplo, o XPath não tem tipos de dados de data ou inteiros, mas o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o XSD têm muitos. O XSD usa precisão de nanossegundos para valores de tempo, e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa precisão de no máximo 1/300 segundo. Consequentemente, o mapeamento de um tipo de dados para outro nem sempre é possível. Para obter mais informações sobre mapeamento [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de tipos de dados para tipos de dados XSD, consulte [coerção de tipo de dados e a anotação sql: DataType &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md).  
  
 O XPath tem três tipos de dados: **cadeia de caracteres**, **número**e **booliano**. O tipo de dados **Number** é sempre um ponto flutuante de precisão dupla IEEE 754. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados **float (53)** é o **número**mais próximo do XPath. No entanto, **float (53)** não é exatamente IEEE 754. Por exemplo, nem NaN (não é um número) nem infinidade é usado. A tentativa de converter uma cadeia de caracteres não numérica em um **número** e tentar dividir por zero resulta em um erro.  
  
## <a name="xpath-conversions"></a>Conversões do XPath  
 Quando você usa uma consulta do XPath como `OrderDetail[@UnitPrice > "10.0"]`, conversões de tipos de dados implícitas e explícitas podem alterar sutilmente o significado da consulta. Por isso, é importante entender como são implementados os tipos de dados XPath. A especificação de linguagem XPath, o XPath (XML Path Language) versão 1,0, recomendação proposta de 8 de outubro de 1999, pode ser encontrada no site da W3C em http://www.w3.org/TR/1999/PR-xpath-19991008.html .  
  
 Os operadores de XPath são divididos em quatro categorias:  
  
-   Operadores boolianos (e, ou)  
  
-   Operadores relacionais ( \<, > , \<=, > =)  
  
-   Operadores de igualdade (=, !=)  
  
-   Operadores aritméticos (+, -, *, div, mod)  
  
 Cada categoria de operador converte os respectivos operandos de forma diferente. Os operadores de XPath convertem implicitamente seus operandos se necessário. Os operadores aritméticos convertem seus operandos em **número**e resultam em um valor numérico. Os operadores boolianos convertem seus operandos em **booliano**e resultam em um valor booliano. Os operadores relacionais e operadores de igualdade resultam em um valor booliano. Entretanto, eles têm diferentes regras de conversão dependendo dos tipos de dados originais dos respectivos operandos, conforme mostra esta tabela.  
  
|Operando|Operador relacional|Operador de igualdade|  
|-------------|-------------------------|-----------------------|  
|Ambos os operandos são conjuntos de nós.|TRUE se e somente se houver um nó em um conjunto e um nó no segundo conjunto, de modo que a comparação de seus valores de **cadeia de caracteres** for true.|Idem.|  
|Um é um conjunto de nós, a outra **cadeia de caracteres**.|TRUE se e somente se houver um nó no conjunto de nós, de modo que, quando convertido em **Number**, a comparação dele com a **cadeia de caracteres** convertida em **Number** seja true.|TRUE se e somente se houver um nó no conjunto de nós, de modo que, quando convertido em **String**, a comparação com a **cadeia de caracteres** seja true.|  
|Um é um conjunto de nós, o outro **número**.|TRUE se e somente se houver um nó no conjunto de nós, de modo que, quando convertido em **Number**, a comparação dele com o **número** seja true.|Idem.|  
|Um é um conjunto de nós, o outro **booliano**.|TRUE se e somente se houver um nó no conjunto de nós, de modo que, quando convertido em **booliano** e, em seguida, em **Number**, a comparação dele com o **booliano** convertido em **Number** seja true.|TRUE se e somente se houver um nó no conjunto de nós, de modo que, quando convertido em **booliano**, a comparação com o **booliano** seja true.|  
|Nenhum é um conjunto de nós.|Converta ambos os operandos em **Number** e compare.|Converta ambos os operandos em um tipo comum e compare. Converter em **booliano** se for **booliano**, **Number** se for um **número**; caso contrário, converta em **cadeia de caracteres**.|  
  
> [!NOTE]  
>  Como os operadores relacionais XPath sempre convertem seus operandos em **número**, as comparações de **cadeia de caracteres** não são possíveis. Para incluir comparações de data, o SQL Server 2000 oferece essa variação à especificação XPath: quando um operador relacional compara uma **cadeia** de caracteres com **uma cadeia de caracteres, um**conjunto de nós com uma **cadeia**de caracteres ou um conjunto de nós com valor de cadeia de caracteres para um conjunto de nós com valor de cadeia de caracteres, uma comparação de **cadeia de caracteres** (não uma comparação de **número** ) é  
  
## <a name="node-set-conversions"></a>Conversões de conjuntos de nós  
 As conversões de conjuntos de nós nem sempre são intuitivas. Um conjunto de nós é convertido em uma **cadeia de caracteres** por meio do valor da cadeia de caracteres apenas do primeiro nó no conjunto. Um conjunto de nós é convertido em **número** convertendo-o em **cadeia de caracteres**e, em seguida, convertendo cadeia de **caracteres** em **número**. Um conjunto de nós é convertido em **booliano** testando sua existência.  
  
> [!NOTE]  
>  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não executa a seleção posicional nos conjuntos de nós: por exemplo, a consulta do XPath `Customer[3]` significa o terceiro cliente; não há suporte a esse tipo de seleção posicional no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Portanto, as conversões de node-set-to-**String** ou node-set-to-**Number** , conforme descrito pela especificação XPath, não são implementadas. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa "qualquer" semântica sempre que a especificação do XPath define "primeira" semântica. Por exemplo, com base na especificação XPath do W3C, a consulta XPath `Order[OrderDetail/@UnitPrice > 10.0]` seleciona esses pedidos com a primeira **OrderDetail** com **PreçoUnitário** maior que 10,0. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , essa consulta XPath seleciona esses pedidos com qualquer **OrderDetail** que tenha um **PreçoUnitário** maior que 10,0.  
  
 A conversão para **booliano** gera um teste de existência; Portanto, a consulta XPath `Products[@Discontinued=true()]` é equivalente à expressão SQL "produtos. descontinuados não é NULL", e não à expressão SQL "Products. Discontinued = 1". Para tornar a consulta equivalente à última expressão SQL, primeiro converta o node-set em um tipo não**booliano** , como **Number**. Por exemplo, `Products[number(@Discontinued) = true()]`.  
  
 Como a maioria dos operadores é definida como TRUE se é TRUE para qualquer um ou para um dos nós do conjunto, essas operações sempre avaliam como FALSE se o conjunto está vazio. Assim, se A está vazio, tanto `A = B` quanto `A != B` são FALSE, e `not(A=B)` e `not(A!=B)` são TRUE.  
  
 Normalmente, um atributo ou elemento que mapeia para uma coluna existe se o valor dessa coluna no banco de dados não for **nulo**. Os elementos que fazem o mapeamento para linhas existirão se qualquer um dos filhos existir.  
  
> [!NOTE]  
>  Os elementos anotados com **is-constant** sempre existem. Consequentemente, os predicados XPath não podem ser usados em elementos **is-constant** .  
  
 Quando um conjunto de nós é convertido em **cadeia de caracteres** ou **número**, seu tipo de XDR (se houver) é inspecionado no esquema anotado e esse tipo é usado para determinar a conversão necessária.  
  
## <a name="mapping-xdr-data-types-to-xpath-data-types"></a>Mapeando tipos de dados XDR para tipos de dados XPath  
 O tipo de dados XPath de um nó é derivado do tipo de dados XDR no esquema, conforme mostrado na tabela a seguir (o nó **EmployeeID** é usado para fins ilustrativos).  
  
|Tipo de dados XDR|Equivalente<br /><br /> tipos de dados XPath|Conversão do SQL Server usada|  
|-------------------|------------------------------------|--------------------------------|  
|Nonebin.base64bin.hex|N/D|NoneEmployeeID|  
|booleano|booleano|CONVERT(bit, EmployeeID)|  
|number, int, float,i1, i2, i4, i8,r4, r8ui1, ui2, ui4, ui8|número|CONVERT(float(53), EmployeeID)|  
|id, idref, idrefsentity, entities, enumerationnotation, nmtoken, nmtokens, chardate, Timedate, Time.tz, string, uri, uuid|string|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|fixed14.4|N/D (não há nenhum tipo de dados no XPath equivalente ao tipo de dados XDR fixed14.4)|CONVERT(money, EmployeeID)|  
|date|string|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|time<br /><br /> time.tz|string|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
 As conversões de data e hora são projetadas para funcionar se o valor é armazenado no banco de dados usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dado **DateTime** ou uma **cadeia de caracteres**. Observe que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados **DateTime** não usa o **fuso horário** e tem uma precisão menor do que o tipo de dados **tempo** XML. Para incluir o tipo de dados **timezone** ou a precisão adicional, armazene os dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando um tipo de **cadeia de caracteres** .  
  
 Quando um nó é convertido do tipo de dados XDR no tipo de dados XPath, às vezes é necessária conversão adicional (de um tipo de dados XPath para outro tipo de dados XPath). Por exemplo, considere esta consulta do XPath:  
  
```  
(@m + 3) = 4  
```  
  
 Se @m for do tipo de dados de **14.4 XDR corrigido** , a conversão do tipo de dados XDR para o tipo de dados XPath será realizada usando:  
  
```  
CONVERT(money, m)  
```  
  
 Nessa conversão, o nó `m` é convertido do **14.4 do Fixed** para o **Money**. Porém, a adição do valor de 3 exige conversão adicional:  
  
```  
CONVERT(float(CONVERT(money, m))  
```  
  
 A expressão do XPath é avaliada como:  
  
```  
CONVERT(float(CONVERT(money, m)) + CONVERT(float(53), 3) = CONVERT(float(53), 3)  
```  
  
 Conforme mostra a tabela a seguir, essa é a mesma conversão aplicada para outras expressões do XPath (como literais ou expressões compostas).  
  
||||||  
|-|-|-|-|-|  
||X é a incógnita|X é uma **cadeia de caracteres**|X é o **número**|X é **booliano**|  
|string(X)|CONVERT (nvarchar(4000), X, 126)|-|CONVERT (nvarchar(4000), X, 126)|CASE WHEN X THEN N'true' ELSE N'false' END|  
|number(X)|CONVERT (float(53), X)|CONVERT (float(53), X)|-|CASE WHEN X THEN 1 ELSE 0 END|  
|boolean(X)|-|LEN (X) > 0|X != 0|-|  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-convert-a-data-type-in-an-xpath-query"></a>a. Converter um tipo de dados em uma consulta do XPath  
 Na consulta XPath a seguir especificada em um esquema XSD anotado, a consulta seleciona todos os nós de **funcionário** com o valor de atributo **EmployeeID** de e-1, em que "E-" é o prefixo especificado usando a anotação **SQL: id-prefix** .  
  
 `Employee[@EmployeeID="E-1"]`  
  
 O predicado na consulta é equivalente à expressão SQL:  
  
 `N'E-' + CONVERT(nvarchar(4000), Employees.EmployeeID, 126) = N'E-1'`  
  
 Como **EmployeeID** é um dos valores de tipo de dados **ID** (**IDREF**, **IDREFS**, **NMTOKEN**, **NMTOKENS**e assim por diante) no esquema XSD, **EmployeeID** é convertido para o tipo de dados XPath de **cadeia de caracteres** usando as regras de conversão descritas anteriormente.  
  
 `CONVERT(nvarchar(4000), Employees.EmployeeID, 126)`  
  
 O prefixo "E -" é adicionado à cadeia de caracteres, e o resultado é comparado com `N'E-1'`.  
  
### <a name="b-perform-several-data-type-conversions-in-an-xpath-query"></a>B. Executar várias conversões de tipo de dados em uma consulta do XPath  
 Considere esta consulta do XPath especificada com base em um esquema XSD anotado: `OrderDetail[@UnitPrice * @OrderQty > 98]`  
  
 Essa consulta XPath retorna todos os **\<OrderDetail>** elementos que atendem ao predicado `@UnitPrice * @OrderQty > 98` . Se o **PreçoUnitário** for anotado com um tipo de dados do **14.4 fixo** no esquema anotado, esse predicado será equivalente à expressão SQL:  
  
 `CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice)) * CONVERT(float(53), OrderDetail.OrderQty) > CONVERT(float(53), 98)`  
  
 Ao converter os valores na consulta do XPath, ocorre a primeira conversão do tipo de dados XDR no tipo de dados XPath. Como o tipo de dados XSD de **PreçoUnitário** é **fixo 14.4**, conforme descrito na tabela anterior, esta é a primeira conversão que é usada:  
  
```  
CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 Como os operadores aritméticos convertem seus operandos para o tipo de dados de **número** XPath, a segunda conversão (de um tipo de dados XPath para outro tipo de dados XPath) é aplicada na qual o valor é convertido em **float (53)** (**float (53)** é próximo ao tipo de dados de **número** XPath):  
  
```  
CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 Supondo que o atributo **OrderQty** não tenha nenhum tipo de dados XSD, **OrderQty** é convertido em um tipo de dados XPath de **número** em uma única conversão:  
  
```  
CONVERT(float(53), OrderDetail.OrderQty)  
```  
  
 Da mesma forma, o valor 98 é convertido para o tipo de dados de **número** XPath:  
  
```  
CONVERT(float(53), 98)  
```  
  
> [!NOTE]  
>  Se o tipo de dados XSD usado no esquema for incompatível com o tipo de dados subjacente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no banco de dados ou se for executada uma conversão impossível de tipo de dados XPath, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderá retornar um erro. Por exemplo, se o **atributo EmployeeID** for anotado com a anotação **id-prefix** , o XPath `Employee[@EmployeeID=1]` gerará um erro, pois **EmployeeID** tem a anotação **id-prefix** e não pode ser convertido em **Number**.  
  
  
