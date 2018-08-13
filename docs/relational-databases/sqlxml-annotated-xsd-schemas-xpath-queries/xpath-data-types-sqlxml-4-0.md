---
title: Tipos de dados XPath (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
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
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 2998ec10089c6c1c4a7d61f59ae2663cc311c510
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39560746"
---
# <a name="xpath-data-types-sqlxml-40"></a>Tipos de dados XPath (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  O [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], XPath e Esquema XML (XSD) têm tipos de dados bem diferentes. Por exemplo, o XPath não tem tipos de dados de data ou inteiros, mas o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o XSD têm muitos. O XSD usa precisão de nanossegundos para valores de tempo, e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa precisão de no máximo 1/300 segundo. Consequentemente, o mapeamento de um tipo de dados para outro nem sempre é possível. Para obter mais informações sobre o mapeamento [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados para os tipos de dados XSD, consulte [coerções de tipo de dados e a anotação SQL: DataType &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md).  
  
 XPath tem três tipos de dados: **cadeia de caracteres**, **número**, e **booliano**. O **número** tipo de dados é sempre um IEEE 754 de precisão dupla de ponto flutuante. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **float(53)** tipo de dados é o mais próximo de XPath **número**. No entanto, **float(53)** não é exatamente IEEE 754. Por exemplo, nem NaN (não é um número) nem infinidade é usado. A tentativa de converter uma cadeia de caracteres não numérica **número** e tentar dividir por zero resulta em um erro.  
  
## <a name="xpath-conversions"></a>Conversões do XPath  
 Quando você usa uma consulta do XPath como `OrderDetail[@UnitPrice > "10.0"]`, conversões de tipos de dados implícitas e explícitas podem alterar sutilmente o significado da consulta. Por isso, é importante entender como são implementados os tipos de dados XPath. A especificação da linguagem XPath, XML Path Language (XPath) version 1.0 W3C Proposed Recommendation 8 de October de 1999, pode ser encontrado no site da W3C em http://www.w3.org/TR/1999/PR-xpath-19991008.html.  
  
 Os operadores de XPath são divididos em quatro categorias:  
  
-   Operadores boolianos (e, ou)  
  
-   Operadores relacionais (\<, >, \<=, > =)  
  
-   Operadores de igualdade (=, !=)  
  
-   Operadores aritméticos (+, -, *, div, mod)  
  
 Cada categoria de operador converte os respectivos operandos de forma diferente. Os operadores de XPath convertem implicitamente seus operandos se necessário. Operadores aritméticos convertem seus operandos em **número**e o resultado em um valor numérico. Operadores boolianos convertem seus operandos em **boolean**e o resultado em um valor booliano. Os operadores relacionais e operadores de igualdade resultam em um valor booliano. Entretanto, eles têm diferentes regras de conversão dependendo dos tipos de dados originais dos respectivos operandos, conforme mostra esta tabela.  
  
|Operando|Operador relacional|Operador de igualdade|  
|-------------|-------------------------|-----------------------|  
|Ambos os operandos são conjuntos de nós.|TRUE se e somente se houver um nó em um conjunto e um nó no segundo conjunto de modo que a comparação dos seus **cadeia de caracteres** valores é TRUE.|Idem.|  
|Um é um conjunto de nós, o outro um **cadeia de caracteres**.|TRUE se e somente se houver um nó no conjunto de nós, de modo que quando convertido em **número**, a comparação dele com o **cadeia de caracteres** convertido em **número** é TRUE.|TRUE se e somente se houver um nó no conjunto de nós, de modo que quando convertido em **cadeia de caracteres**, a comparação dele com o **cadeia de caracteres** é TRUE.|  
|Um é um conjunto de nós, o outro um **número**.|TRUE se e somente se houver um nó no conjunto de nós, de modo que quando convertido em **número**, a comparação dele com o **número** é TRUE.|Idem.|  
|Um é um conjunto de nós, o outro um **boolean**.|TRUE se e somente se houver um nó no conjunto de nós, de modo que quando convertido em **boolean** e, em seguida, para **número**, a comparação dele com o **booliano** convertido em **número** é TRUE.|TRUE se e somente se houver um nó no conjunto de nós, de modo que quando convertido em **boolean**, a comparação dele com o **booliano** for TRUE.|  
|Nenhum é um conjunto de nós.|Converta ambos os operandos para **número** e, em seguida, comparar.|Converta ambos os operandos em um tipo comum e compare. Converter em **boolean** se um deles estiver **booliano**, **número** se alguma for **número**; caso contrário, converter em **decadeiadecaracteres**.|  
  
> [!NOTE]  
>  Porque os operadores relacionais de XPath sempre convertem seus operandos em **número**, **cadeia de caracteres** comparações não são possíveis. Para incluir comparações de data, o SQL Server 2000 oferece essa variação a especificação do XPath: quando um operador relacional compara uma **cadeia de caracteres** para um **cadeia de caracteres**, um conjunto de nós para um **decadeiadecaracteres**, ou um com valor de cadeia de caracteres de nó-definida como um valor de cadeia de caracteres de conjunto de nós, um **cadeia de caracteres** comparação (não um **número** comparação) é executada.  
  
## <a name="node-set-conversions"></a>Conversões de conjuntos de nós  
 As conversões de conjuntos de nós nem sempre são intuitivas. Um conjunto de nós é convertido em um **cadeia de caracteres** obtendo o valor de cadeia de caracteres de apenas o primeiro nó no conjunto. Um conjunto de nós é convertido em **número** , convertendo-a **cadeia de caracteres**e, em seguida, convertendo **cadeia de caracteres** para **número**. Um conjunto de nós é convertido em **boolean** testando sua existência.  
  
> [!NOTE]  
>  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não executa a seleção posicional nos conjuntos de nós: por exemplo, a consulta do XPath `Customer[3]` significa o terceiro cliente; não há suporte a esse tipo de seleção posicional no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Portanto, o nó-definido-para-**cadeia de caracteres** ou nó-definido-para-**número** conversões conforme descrito pela especificação do XPath não são implementadas. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa "qualquer" semântica sempre que a especificação do XPath define "primeira" semântica. Por exemplo, com base na especificação XPath do W3C, a consulta XPath `Order[OrderDetail/@UnitPrice > 10.0]` seleciona os pedidos com a primeira **OrderDetail** que tem um **UnitPrice** maior do que 10.0. Na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa consulta XPath seleciona os pedidos com qualquer **OrderDetail** que tem um **UnitPrice** maior do que 10.0.  
  
 A conversão em **boolean** gera uma existência teste; portanto, a consulta XPath `Products[@Discontinued=true()]` é equivalente à expressão SQL "Discontinued is not null", não à expressão SQL "Discontinued = 1". Para tornar a consulta equivalente à última expressão SQL, primeiro converta o conjunto de nós em um não -**boolean** tipo, como **número**. Por exemplo, `Products[number(@Discontinued) = true()]`.  
  
 Como a maioria dos operadores é definida como TRUE se é TRUE para qualquer um ou para um dos nós do conjunto, essas operações sempre avaliam como FALSE se o conjunto está vazio. Assim, se A está vazio, tanto `A = B` quanto `A != B` são FALSE, e `not(A=B)` e `not(A!=B)` são TRUE.  
  
 Normalmente, um atributo ou elemento que mapeia para uma coluna existe se o valor dessa coluna no banco de dados não for **nulo**. Os elementos que fazem o mapeamento para linhas existirão se qualquer um dos filhos existir.  
  
> [!NOTE]  
>  Elementos anotados com **constante é** sempre existe. Consequentemente, os predicados do XPath não podem ser usados na **constante é** elementos.  
  
 Quando um conjunto de nós é convertido em **cadeia de caracteres** ou **número**, seu tipo XDR (se houver) é inspecionado no esquema anotado e esse tipo é usado para determinar a conversão é necessária.  
  
## <a name="mapping-xdr-data-types-to-xpath-data-types"></a>Mapeando tipos de dados XDR para tipos de dados XPath  
 O tipo de dados XPath de um nó é derivado do tipo de dados XSD no esquema, conforme mostrado na tabela a seguir (o nó **EmployeeID** é usado para fins meramente ilustrativos).  
  
|Tipo de dados XDR|Equivalente<br /><br /> tipos de dados XPath|Conversão do SQL Server usada|  
|-------------------|------------------------------------|--------------------------------|  
|Nonebin.base64bin.hex|N/A|NoneEmployeeID|  
|booleano|booleano|CONVERT(bit, EmployeeID)|  
|number, int, float,i1, i2, i4, i8,r4, r8ui1, ui2, ui4, ui8|number|CONVERT(float(53), EmployeeID)|  
|id, idref, idrefsentity, entities, enumerationnotation, nmtoken, nmtokens, chardate, Timedate, Time.tz, string, uri, uuid|cadeia de caracteres|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|fixed14.4|N/D (não há nenhum tipo de dados no XPath equivalente ao tipo de dados XDR fixed14.4)|CONVERT(money, EmployeeID)|  
|Data|cadeia de caracteres|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|time<br /><br /> time.tz|cadeia de caracteres|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
 As conversões de data e hora são projetadas para funcionar independentemente do valor é armazenado no banco de dados usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** tipo de dados ou uma **cadeia de caracteres**. Observe que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** tipo de dados não usa **fuso horário** e tem uma precisão menor que o XML **tempo** tipo de dados. Para incluir a **fuso horário** tipo de dados ou precisão adicional, armazene os dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando um **cadeia de caracteres** tipo.  
  
 Quando um nó é convertido do tipo de dados XDR no tipo de dados XPath, às vezes é necessária conversão adicional (de um tipo de dados XPath para outro tipo de dados XPath). Por exemplo, considere esta consulta do XPath:  
  
```  
(@m + 3) = 4  
```  
  
 Se @m é o **fixed14.4** tipo de dados XDR, a conversão de tipo de dados XDR para XPath que tipo de dados é realizado usando:  
  
```  
CONVERT(money, m)  
```  
  
 Nessa conversão, o nó `m` é convertido de **fixed14.4** à **dinheiro**. Porém, a adição do valor de 3 exige conversão adicional:  
  
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
||X é a incógnita|X é **cadeia de caracteres**|X é **número**|X é **booliano**|  
|string(X)|CONVERT (nvarchar(4000), X, 126)|-|CONVERT (nvarchar(4000), X, 126)|CASE WHEN X THEN N'true' ELSE N'false' END|  
|number(X)|CONVERT (float(53), X)|CONVERT (float(53), X)|-|CASE WHEN X THEN 1 ELSE 0 END|  
|boolean(X)|-|LEN(X) > 0|X != 0|-|  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-convert-a-data-type-in-an-xpath-query"></a>A. Converter um tipo de dados em uma consulta do XPath  
 A seguinte consulta XPath especificada com base em um esquema XSD anotado, a consulta seleciona todos os **funcionário** nós com o **EmployeeID** atributo valor de 1, onde "E-" é o prefixo especificado usando o **SQL: ID-prefixo** anotação.  
  
 `Employee[@EmployeeID="E-1"]`  
  
 O predicado na consulta é equivalente à expressão SQL:  
  
 `N'E-' + CONVERT(nvarchar(4000), Employees.EmployeeID, 126) = N'E-1'`  
  
 Porque **EmployeeID** é um dos **id** (**idref**, **idrefs**, **nmtoken**,  **NMTOKENS**e assim por diante) valores de tipo de dados no esquema XSD, **EmployeeID** é convertido para o **cadeia de caracteres** tipo de dados XPath usando as regras de conversão descritas anteriormente.  
  
 `CONVERT(nvarchar(4000), Employees.EmployeeID, 126)`  
  
 O prefixo "E -" é adicionado à cadeia de caracteres, e o resultado é comparado com `N'E-1'`.  
  
### <a name="b-perform-several-data-type-conversions-in-an-xpath-query"></a>B. Executar várias conversões de tipo de dados em uma consulta do XPath  
 Considere esta consulta do XPath especificada com base em um esquema XSD anotado: `OrderDetail[@UnitPrice * @OrderQty > 98]`  
  
 Essa consulta XPath retorna todos os  **\<OrderDetail >** elementos que satisfazem o predicado `@UnitPrice * @OrderQty > 98`. Se o **UnitPrice** é anotado com um **fixed14.4** de tipo de dados no esquema anotado, esse predicado é equivalente à expressão SQL:  
  
 `CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice)) * CONVERT(float(53), OrderDetail.OrderQty) > CONVERT(float(53), 98)`  
  
 Ao converter os valores na consulta do XPath, ocorre a primeira conversão do tipo de dados XDR no tipo de dados XPath. Como o tipo de dados XSD de **UnitPrice** é **fixed14.4**, conforme descrito na tabela anterior, isso é a primeira conversão usada:  
  
```  
CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 Porque os operadores aritméticos convertem seus operandos para o **número** tipo de dados XPath, a segunda conversão (de um tipo de dados XPath em outro tipo de dados XPath) é aplicada no qual o valor é convertido em **float(53)**  (**float(53)** está perto o XPath **número** tipo de dados):  
  
```  
CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 Supondo que o **OrderQty** atributo não tem nenhum tipo de dados XSD, **OrderQty** é convertido em um **número** tipo de dados XPath em uma única conversão:  
  
```  
CONVERT(float(53), OrderDetail.OrderQty)  
```  
  
 Da mesma forma, o valor 98 é convertido para o **número** tipo de dados XPath:  
  
```  
CONVERT(float(53), 98)  
```  
  
> [!NOTE]  
>  Se o tipo de dados XSD usado no esquema for incompatível com o tipo de dados subjacente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no banco de dados ou se for executada uma conversão impossível de tipo de dados XPath, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderá retornar um erro. Por exemplo, se o **EmployeeID** atributo é anotado com **id-prefix** anotação, o XPath `Employee[@EmployeeID=1]` gerará um erro, pois **EmployeeID** tem o **id-prefix** anotação e não pode ser convertido em **número**.  
  
  
