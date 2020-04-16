---
title: Tipos de dados XPath (SQLXML)
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
ms.openlocfilehash: 089b2b006d0159c63e480c8627762ac37dec98b8
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/15/2020
ms.locfileid: "75247085"
---
# <a name="xpath-data-types-sqlxml-40"></a>Tipos de dados XPath (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], XPath e XML Schema (XSD) têm tipos de dados muito diferentes. Por exemplo, o XPath não tem tipos de dados de data ou inteiros, mas o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o XSD têm muitos. O XSD usa precisão de nanossegundos para valores de tempo, e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa precisão de no máximo 1/300 segundo. Consequentemente, o mapeamento de um tipo de dados para outro nem sempre é possível. Para obter mais [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] informações sobre o mapeamento de tipos de dados para tipos de dados XSD, consulte [Coercions do Tipo de Dados e a anotação sql:datatype &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md).  
  
 O XPath tem três tipos de dados: **string**, **number**e **boolean**. O tipo de dados **numéu** é sempre um ponto flutuante de dupla precisão Do IEEE 754. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de dados **float (53)** é o mais próximo do **número**XPath . No entanto, **float(53)** não é exatamente IEEE 754. Por exemplo, nem NaN (não é um número) nem infinidade é usado. Tentar converter uma seqüência não numérica em **número** e tentar dividir por zero resulta em um erro.  
  
## <a name="xpath-conversions"></a>Conversões do XPath  
 Quando você usa uma consulta do XPath como `OrderDetail[@UnitPrice > "10.0"]`, conversões de tipos de dados implícitas e explícitas podem alterar sutilmente o significado da consulta. Por isso, é importante entender como são implementados os tipos de dados XPath. A especificação do idioma XPath, xML Path Language (XPath) versão 1.0 W3C Proposta recomendação 8 http://www.w3.org/TR/1999/PR-xpath-19991008.htmlde outubro de 1999, pode ser encontrada no site do W3C em .  
  
 Os operadores de XPath são divididos em quatro categorias:  
  
-   Operadores boolianos (e, ou)  
  
-   Operadores relacionais\<( \<, >, =, >=)  
  
-   Operadores de igualdade (=, !=)  
  
-   Operadores aritméticos (+, -, *, div, mod)  
  
 Cada categoria de operador converte os respectivos operandos de forma diferente. Os operadores de XPath convertem implicitamente seus operandos se necessário. Operadores aritméticos convertem seus operands em **número**e resultam em um valor numério. Operadores booleanos convertem seus operands em **booleanos**, e resultam em um valor booleano. Os operadores relacionais e operadores de igualdade resultam em um valor booliano. Entretanto, eles têm diferentes regras de conversão dependendo dos tipos de dados originais dos respectivos operandos, conforme mostra esta tabela.  
  
|Operando|Operador relacional|Operador de igualdade|  
|-------------|-------------------------|-----------------------|  
|Ambos os operandos são conjuntos de nós.|VERDADE se e somente se houver um nó em um conjunto e um nó no segundo conjunto de tal forma que a comparação de seus valores de **seqüência** é VERDADEIRA.|Idem.|  
|Um é um conjunto de nó, o outro uma **corda.**|TRUE if and only if there is a node in the node-set such that when converted to **number**, the comparison of it with the **string** converted to **number** is TRUE.|TRUE if and only if there is a node in the node-set such that when converted to **string**, the comparison of it with the **string** is TRUE.|  
|Um é um conjunto de nó, o outro um **número.**|TRUE if and only if there is a node in the node-set such that when converted to **number**, the comparison of it with the **number** is TRUE.|Idem.|  
|Um é um nó, o outro um **booleano.**|VERDADE se e somente se houver um nó no nó-set de tal forma que quando convertido em **booleano** e, em seguida, para **número**, a comparação dele com o **booleano** convertido em **número** é VERDADEIRO.|VERDADE se e somente se houver um nó no nó-set de tal forma que quando convertido em **booleano**, a comparação dele com o **booleano** é VERDADEIRA.|  
|Nenhum é um conjunto de nós.|Converta ambas as operações em **número** e depois compare.|Converta ambos os operandos em um tipo comum e compare. Converta-se **em booleano** se for **booleano,** **número** se for **número;** caso contrário, converta em **string**.|  
  
> [!NOTE]  
>  Como os operadores relacionais XPath sempre convertem seus operands em **número,** as comparações **de seqüência** não são possíveis. Para incluir comparações de data, o SQL Server 2000 oferece essa variação à especificação XPath: Quando um operador relacional compara uma **string** a uma **string**, um nó definido a uma **string**ou um nó avaliado em strings para um conjunto de nó saturado de string, uma comparação **de strings** (não uma comparação **numérica)** é realizada.  
  
## <a name="node-set-conversions"></a>Conversões de conjuntos de nós  
 As conversões de conjuntos de nós nem sempre são intuitivas. Um conjunto de nós é convertido em uma **seqüência,** tomando o valor de seqüência de apenas o primeiro nó no conjunto. Um conjunto de nós é convertido em **número** convertendo-o em **string**e, em seguida, convertendo **string** em **número**. Um conjunto de nós é convertido em **booleano,** testando sua existência.  
  
> [!NOTE]  
>  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não executa a seleção posicional nos conjuntos de nós: por exemplo, a consulta do XPath `Customer[3]` significa o terceiro cliente; não há suporte a esse tipo de seleção posicional no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Portanto, as conversões de nó-set-to-string ou set-to-number, conforme descrito pela especificação XPath, não são implementadas.**string** **number** O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa "qualquer" semântica sempre que a especificação do XPath define "primeira" semântica. Por exemplo, com base na especificação W3C XPath, a consulta `Order[OrderDetail/@UnitPrice > 10.0]` XPath seleciona essas ordens com o primeiro **OrderDetail** que tem um **UnitPrice** maior que 10.0. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta consulta XPath seleciona essas ordens com qualquer **OrderDetail** que tenha um **UnitPrice** maior que 10.0.  
  
 A conversão para **booleangera** um teste de existência; portanto, a consulta `Products[@Discontinued=true()]` XPath é equivalente à expressão SQL "Products.Descontinuado não é nulo", e não a expressão SQL "Products.Descontinuado = 1". Para tornar a consulta equivalente à última expressão SQL, primeiro converta o nó definido em um tipo não**booleano,** como **número**. Por exemplo, `Products[number(@Discontinued) = true()]`.  
  
 Como a maioria dos operadores é definida como TRUE se é TRUE para qualquer um ou para um dos nós do conjunto, essas operações sempre avaliam como FALSE se o conjunto está vazio. Assim, se A está vazio, tanto `A = B` quanto `A != B` são FALSE, e `not(A=B)` e `not(A!=B)` são TRUE.  
  
 Normalmente, um atributo ou elemento que mapeia para uma coluna existe se o valor dessa coluna no banco de dados não for **nulo**. Os elementos que fazem o mapeamento para linhas existirão se qualquer um dos filhos existir.  
  
> [!NOTE]  
>  Elementos anotados com **constante sis sempre** existem. Consequentemente, os predicados XPath não podem ser usados em elementos **constantes.**  
  
 Quando um conjunto de nós é convertido em **string** ou **número,** seu tipo XDR (se houver) é inspecionado no esquema anotado e esse tipo é usado para determinar a conversão necessária.  
  
## <a name="mapping-xdr-data-types-to-xpath-data-types"></a>Mapeando tipos de dados XDR para tipos de dados XPath  
 O tipo de dados XPath de um nó é derivado do tipo de dados XDR no esquema, como mostrado na tabela a seguir (o nó **EmployeeID** é usado para fins ilustrativos).  
  
|Tipo de dados XDR|Equivalente<br /><br /> tipos de dados XPath|Conversão do SQL Server usada|  
|-------------------|------------------------------------|--------------------------------|  
|Nonebin.base64bin.hex|N/D|NoneEmployeeID|  
|booleano|booleano|CONVERT(bit, EmployeeID)|  
|number, int, float,i1, i2, i4, i8,r4, r8ui1, ui2, ui4, ui8|número|CONVERT(float(53), EmployeeID)|  
|id, idref, idrefsentity, entities, enumerationnotation, nmtoken, nmtokens, chardate, Timedate, Time.tz, string, uri, uuid|string|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|fixed14.4|N/D (não há nenhum tipo de dados no XPath equivalente ao tipo de dados XDR fixed14.4)|CONVERT(money, EmployeeID)|  
|date|string|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|time<br /><br /> time.tz|string|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
 As conversões de data e hora são projetadas para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]funcionar se o valor é armazenado no banco de dados usando o tipo de dados **de data ou** uma **seqüência**. Observe que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o tipo de dados **de data-hora** não usa **fuso horário** e tem uma precisão menor do que o tipo de dados **de tempo** XML. Para incluir o tipo de dados **de fuso horário** ou precisão adicional, armazene os dados usando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] um tipo de **string.**  
  
 Quando um nó é convertido do tipo de dados XDR no tipo de dados XPath, às vezes é necessária conversão adicional (de um tipo de dados XPath para outro tipo de dados XPath). Por exemplo, considere esta consulta do XPath:  
  
```  
(@m + 3) = 4  
```  
  
 Se @m for do tipo de dados **Fixo14.4** XDR, a conversão do tipo de dados XDR para o tipo de dados XPath é realizada usando:  
  
```  
CONVERT(money, m)  
```  
  
 Nesta conversão, o `m` nó é convertido de **fixo14,4** para **dinheiro**. Porém, a adição do valor de 3 exige conversão adicional:  
  
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
||X é a incógnita|X é **string**|X é **o número**|X é **booleano**|  
|string(X)|CONVERT (nvarchar(4000), X, 126)|-|CONVERT (nvarchar(4000), X, 126)|CASE WHEN X THEN N'true' ELSE N'false' END|  
|number(X)|CONVERT (float(53), X)|CONVERT (float(53), X)|-|CASE WHEN X THEN 1 ELSE 0 END|  
|boolean(X)|-|LEN(X) > 0|X != 0|-|  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-convert-a-data-type-in-an-xpath-query"></a>a. Converter um tipo de dados em uma consulta do XPath  
 Na consulta XPath a seguir especificada em um esquema XSD anotado, a consulta seleciona todos os nós **do Funcionário** com o valor de atributo **EmployeeID** do E-1, onde "E-" é o prefixo especificado usando a annotação **sql:id-prefixo.**  
  
 `Employee[@EmployeeID="E-1"]`  
  
 O predicado na consulta é equivalente à expressão SQL:  
  
 `N'E-' + CONVERT(nvarchar(4000), Employees.EmployeeID, 126) = N'E-1'`  
  
 Como **o EmployeeID** é um dos valores de **id** **(idref,** **idrefs,** **nmtokens, nmtokens,** e assim por diante) valores de tipo de dados no esquema XSD, o **EmployeeID** é convertido para o tipo de dados **xPath de cadeia** usando as regras de conversão descritas anteriormente. **nmtoken**  
  
 `CONVERT(nvarchar(4000), Employees.EmployeeID, 126)`  
  
 O prefixo "E -" é adicionado à cadeia de caracteres, e o resultado é comparado com `N'E-1'`.  
  
### <a name="b-perform-several-data-type-conversions-in-an-xpath-query"></a>B. Executar várias conversões de tipo de dados em uma consulta do XPath  
 Considere esta consulta do XPath especificada com base em um esquema XSD anotado: `OrderDetail[@UnitPrice * @OrderQty > 98]`  
  
 Esta consulta XPath retorna todos os `@UnitPrice * @OrderQty > 98` ** \<** elementos orderDetail>que satisfazem o predicado . Se o **UnitPrice** for anotado com um tipo de dados **fixo14.4** no esquema anotado, este predicado é equivalente à expressão SQL:  
  
 `CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice)) * CONVERT(float(53), OrderDetail.OrderQty) > CONVERT(float(53), 98)`  
  
 Ao converter os valores na consulta do XPath, ocorre a primeira conversão do tipo de dados XDR no tipo de dados XPath. Como o tipo de dados XSD do **UnitPrice** é **fixo14.4**, como descrito na tabela anterior, esta é a primeira conversão que é usada:  
  
```  
CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 Como os operadores aritméticos convertem seus operands para o tipo de dados **xPath número,** a segunda conversão (de um tipo de dados XPath para outro tipo de dados XPath) é aplicada na qual o valor é convertido para **flutuar(53)** **(float(53)** está próximo do tipo de dados **do número** XPath):  
  
```  
CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 Supondo que o atributo **OrderQty** não tenha nenhum tipo de dados XSD, **o OrderQty** é convertido em um tipo de dados XPath **de número** em uma única conversão:  
  
```  
CONVERT(float(53), OrderDetail.OrderQty)  
```  
  
 Da mesma forma, o valor 98 é convertido para o tipo de dados **xPath número:**  
  
```  
CONVERT(float(53), 98)  
```  
  
> [!NOTE]  
>  Se o tipo de dados XSD usado no esquema for incompatível com o tipo de dados subjacente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no banco de dados ou se for executada uma conversão impossível de tipo de dados XPath, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderá retornar um erro. Por exemplo, se o atributo **EmployeeID** for anotado com anotação `Employee[@EmployeeID=1]` **de prefixo de id,** o XPath gerará um erro, porque o **EmployeeID** tem a anotação **de prefixo id** e não pode ser convertido em **número**.  
  
  
