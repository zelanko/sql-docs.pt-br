---
title: Colunas com um nome | Microsoft Docs
description: Saiba mais sobre as colunas com um nome nas consultas SQL e as condições específicas nas quais as colunas de conjunto de linhas com nome são mapeadas para o XML resultante.
ms.custom: fresh2019may
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns with
ms.assetid: c994e089-4cfc-4e9b-b7fc-e74f6014b51a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 14bc7706a7e3f562b2a3f4f01d8ab08a3684d313
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775566"
---
# <a name="columns-with-a-name"></a>Colunas com um nome

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

As seguintes são as condições específicas nas quais colunas de conjunto de linhas com um nome são mapeadas, diferenciando maiúsculas e minúsculas, para o XML resultante:  
  
-   O nome da coluna começa com uma arroba (\@).  
  
-   O nome da coluna não começa com uma arroba (\@).  
  
-   O nome da coluna não começa com uma arroba \@ e contém uma barra (/).  
  
-   Várias colunas compartilham o mesmo prefixo.  
  
-   Uma coluna tem um nome diferente.  
  
## <a name="column-name-starts-with-an-at-sign-"></a>O nome da coluna começa com uma arroba (\@)  
 Se o nome da coluna começar com uma arroba (\@) e não contiver uma barra (/), um atributo do elemento `row` que tem o valor da coluna correspondente será criado. Por exemplo, a consulta a seguir retorna um conjunto de linhas de duas colunas (\@PmId, Name). No XML resultante, um atributo **PmId** é adicionado ao elemento `row` correspondente e um valor de ProductModelID é atribuído a ele.  
  
```sql
SELECT ProductModelID as "@PmId",  
       Name  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH;
```  
  
 Este é o resultado:  
  
```xml
<row PmId="7">  
  <Name>HL Touring Frame</Name>  
</row>  
```  
  
 Observe que os atributos devem vir antes de quaisquer outros tipos de nós, como nós de elemento e nós de texto, no mesmo nível. A consulta a seguir retornará um erro:  
  
```sql
SELECT Name,  
       ProductModelID as "@PmId"  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH;
```  
  
## <a name="column-name-does-not-start-with-an-at-sign-"></a>O nome da coluna não começa com uma arroba (\@)  
 Se o nome da coluna não começar com uma arroba (\@), não for um dos testes do nó XPath e não contiver uma barra (/), um elemento XML que é um subelemento do elemento linha, `row`, será criado, por padrão.  
  
 A consulta a seguir especifica o nome da coluna, o resultado. Portanto, um filho do elemento `result` é adicionado ao elemento `row`.  
  
```sql
SELECT 2+2 as result  
for xml PATH;
```  
  
 Este é o resultado:  
  
```xml
<row>  
  <result>4</result>  
</row>  
```  
  
 O exemplo a seguir especifica o nome da coluna, ManuWorkCenterInformation, para o XML retornado pelo XQuery especificado em relação à coluna Instructions de tipo **xml**. Portanto, um elemento `ManuWorkCenterInformation` é adicionado como um filho do elemento `row`.  
  
```sql
SELECT
  ProductModelID,  
  Name,  
  Instructions.query(
    'declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";
     /MI:root/MI:Location
    ') as ManuWorkCenterInformation  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH;
```  
  
 Este é o resultado:  
  
```xml
<row>  
  <ProductModelID>7</ProductModelID>  
  <Name>HL Touring Frame</Name>  
  <ManuWorkCenterInformation>  
    <MI:Location ...LocationID="10" ...></MI:Location>  
    <MI:Location ...LocationID="20" ...></MI:Location>  
     ...  
  </ManuWorkCenterInformation>  
</row>  
```  
  
## <a name="column-name-does-not-start-with-an-at-sign--and-contains-a-slash-mark-"></a>O nome da coluna não começa com uma arroba \@ e contém uma barra (/)  
 Se o nome da coluna não começar com uma arroba (\@), mas contiver uma barra (/), o nome da coluna indicará uma hierarquia XML. Por exemplo, se o nome da coluna for “Name1/Name2/Name3.../Name***n*** ”, cada Name***i*** representará um nome do elemento que está aninhado no elemento da linha atual (para i=1) ou que está sob o elemento que tem o nome Name***i-1***. Se Name***n*** começar com "\@", ele será mapeado para um atributo de elemento Name ***n-1***.  
  
 Por exemplo, a consulta a seguir retorna a ID e o nome de um funcionário que são representados como um elemento complexo EmpName que contém um Nome, Segundo nome e Sobrenome.  
  
```sql
SELECT EmployeeID "@EmpID",   
       FirstName  "EmpName/First",   
       MiddleName "EmpName/Middle",   
       LastName   "EmpName/Last"  
FROM   HumanResources.Employee E, Person.Contact C  
WHERE  E.EmployeeID = C.ContactID  AND
       E.EmployeeID=1  
FOR XML PATH;
```  
  
 Os nomes de colunas são usados como um caminho para construir XML no modo PATH. O nome da coluna que contém valores de ID de funcionário, começa com “\@”. Portanto, um atributo **EmpID** é adicionado ao elemento `row`. Todas as outras colunas incluem uma barra ('/') no nome da coluna que indica hierarquia. O XML resultante terá o filho `EmpName` sob o elemento `row` e o filho `EmpName` terá os filhos dos elementos `First`, `Middle` e `Last`.  
  
```xml
<row EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
    <Last>Achong</Last>  
  </EmpName>  
</row>  
```  
  
 O segundo nome do funcionário é nulo e, por padrão, o valor nulo é mapeado para a ausência do elemento ou atributo. Se você quiser elementos gerados para os valores NULL, poderá especificar a diretiva ELEMENTS com XSINIL conforme mostrado nesta consulta.  
  
```sql
SELECT EmployeeID "@EmpID",   
       FirstName  "EmpName/First",   
       MiddleName "EmpName/Middle",   
       LastName   "EmpName/Last"  
FROM   HumanResources.Employee E, Person.Contact C  
WHERE  E.EmployeeID = C.ContactID  AND
       E.EmployeeID=1  
FOR XML PATH, ELEMENTS XSINIL;
```  
  
 Este é o resultado:  
  
```xml
<row xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
    <Middle xsi:nil="true" />  
    <Last>Achong</Last>  
  </EmpName>  
</row>  
```  
  
 Por padrão, o modo PATH gera XML centrado em elemento. Portanto especificar a diretiva ELEMENTS em uma consulta em modo PATH não tem nenhum efeito. No entanto, conforme mostrado no exemplo anterior, a diretiva ELEMENTS é útil com XSINIL para gerar elementos para valores nulos.  
  
 Além da ID e do nome, a consulta a seguir recupera um endereço de funcionário. De acordo com o caminho nos nomes das colunas de endereço, um filho do elemento `Address` é adicionado ao elemento `row` e os detalhes do endereço são adicionados como filhos do elemento `Address`.  
  
```sql
SELECT EmployeeID   "@EmpID",   
       FirstName    "EmpName/First",   
       MiddleName   "EmpName/Middle",   
       LastName     "EmpName/Last",  
       AddressLine1 "Address/AddrLine1",  
       AddressLine2 "Address/AddrLIne2",  
       City         "Address/City"  
FROM   HumanResources.Employee E,
       Person.Contact C,
       Person.Address A  
WHERE  E.EmployeeID = C.ContactID  
AND    E.AddressID = A.AddressID  
AND    E.EmployeeID=1  
FOR XML PATH;
```  
  
 Este é o resultado:  
  
```xml
<row EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
    <Last>Achong</Last>  
  </EmpName>  
  <Address>  
    <AddrLine1>7726 Driftwood Drive</AddrLine1>  
    <City>Monroe</City>  
  </Address>  
</row>  
```  
  
## <a name="several-columns-share-the-same-path-prefix"></a>Várias colunas compartilham o mesmo prefixo  
 Se várias colunas subsequentes compartilharem o mesmo prefixo de caminho, elas serão agrupadas sob o mesmo nome. Se diferentes prefixos de namespace estiverem sendo usados, mesmo que estejam associados ao mesmo namespace, um caminho será considerado diferente. Na consulta anterior, as colunas FirstName, MiddleName e LastName compartilham o mesmo prefixo EmpName. Portanto, elas são adicionadas como filhos do elemento `EmpName`. Esse também é o caso quando o elemento `Address` foi criado no exemplo anterior.  
  
## <a name="one-column-has-a-different-name"></a>Uma coluna tem um nome diferente  
 Se uma coluna com um nome diferente aparecer no meio, ela quebrará o agrupamento, conforme mostrado na seguinte consulta modificada. A consulta quebra o agrupamento de FirstName, MiddleName e LastName, conforme especificado na consulta anterior, adicionando colunas de endereço no meio das colunas FirstName e MiddleName.  
  
```sql
SELECT EmployeeID "@EmpID",   
       FirstName "EmpName/First",   
       AddressLine1 "Address/AddrLine1",  
       AddressLine2 "Address/AddrLIne2",  
       City "Address/City",  
       MiddleName "EmpName/Middle",   
       LastName "EmpName/Last"  
FROM   HumanResources.EmployeeAddress E,
       Person.Contact C,
       Person.Address A  
WHERE  E.EmployeeID = C.ContactID  
AND    E.AddressID = A.AddressID  
AND    E.EmployeeID=1  
FOR XML PATH;
```  
  
 Como resultado, a consulta cria dois elementos `EmpName`. O primeiro elemento `EmpName` tem o filho do elemento `FirstName` e o segundo elemento `EmpName` tem os filhos dos elementos `MiddleName` e `LastName`.  
  
 Este é o resultado:  
  
```xml
<row EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
  </EmpName>  
  <Address>  
    <AddrLine1>7726 Driftwood Drive</AddrLine1>  
    <City>Monroe</City>  
  </Address>  
  <EmpName>  
    <Last>Achong</Last>  
  </EmpName>  
</row>  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Usar o modo PATH com FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
