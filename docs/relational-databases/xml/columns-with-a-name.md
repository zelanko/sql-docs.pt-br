---
title: Colunas com um nome | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- names [SQL Server], columns with
ms.assetid: c994e089-4cfc-4e9b-b7fc-e74f6014b51a
caps.latest.revision: 8
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: b4b9a8774565dd0e31caf940cf3e8254b0987205
ms.openlocfilehash: 3a2651e6e67cceb648049f99ab9588a44b7f3fb0
ms.contentlocale: pt-br
ms.lasthandoff: 11/08/2017

---
# <a name="columns-with-a-name"></a>Colunas com um nome
  As seguintes são as condições específicas nas quais colunas de conjunto de linhas com um nome são mapeadas, diferenciando maiúsculas e minúsculas, para o XML resultante:  
  
-   O nome da coluna começa com uma arroba (@).  
  
-   O nome da coluna não começa com uma arroba (@).  
  
-   O nome da coluna não começa com uma arroba @ e contém uma barra (/).  
  
-   Várias colunas compartilham o mesmo prefixo.  
  
-   Uma coluna tem um nome diferente.  
  
## <a name="column-name-starts-with-an-at-sign-"></a>O nome da coluna começa com uma arroba (@)  
 Se o nome da coluna começa com um sinal de arroba (@) e não contém uma barra (/), um atributo do `row` elemento que tem o valor da coluna correspondente é criado. Por exemplo, a seguinte consulta retorna um conjunto de linhas (@PmId, Nome) de duas colunas. No XML resultante, um **PmId** atributo é adicionado ao correspondente `row` elemento e um valor de ProductModelID é atribuído a ele.  
  
```  
  
SELECT ProductModelID as "@PmId",  
       Name  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH   
go  
  
```  
  
 Este é o resultado:  
  
```  
<row PmId="7">  
  <Name>HL Touring Frame</Name>  
</row>  
```  
  
 Observe que os atributos devem vir antes de quaisquer outros tipos de nós, como nós de elemento e nós de texto, no mesmo nível. A consulta a seguir retornará um erro:  
  
```  
SELECT Name,  
       ProductModelID as "@PmId"  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH   
go  
```  
  
## <a name="column-name-does-not-start-with-an-at-sign-"></a>O nome da coluna não começa com uma arroba (@)  
 Se o nome da coluna não começa com um sinal de arroba (@), não é um dos testes de nó XPath e não contiver uma barra (/), um elemento XML que é um subelemento do elemento linha, `row` por padrão, é criado.  
  
 A consulta a seguir especifica o nome da coluna, o resultado. Portanto, um `result` elemento filho é adicionado para o `row` elemento.  
  
```  
SELECT 2+2 as result  
for xml PATH  
```  
  
 Este é o resultado:  
  
```  
<row>  
  <result>4</result>  
</row>  
```  
  
 O exemplo a seguir especifica o nome da coluna, ManuWorkCenterInformation, para o XML retornado pelo XQuery especificado em relação à coluna Instructions de tipo **xml**. Portanto, um `ManuWorkCenterInformation` elemento é adicionado como um filho de `row` elemento.  
  
```  
SELECT   
       ProductModelID,  
       Name,  
       Instructions.query('declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
                /MI:root/MI:Location   
              ') as ManuWorkCenterInformation  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH   
go  
```  
  
 Este é o resultado:  
  
```  
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
  
## <a name="column-name-does-not-start-with-an-at-sign--and-contains-a-slash-mark-"></a>O nome da coluna não começa com uma arroba @ e contém uma barra (/)  
 Se o nome da coluna não começar com uma arroba (@), mas contiver uma barra (/), o nome da coluna indicará uma hierarquia XML. Por exemplo, se o nome da coluna for “Name1/Name2/Name3.../Name***n*** ”, cada Name***i*** representará um nome do elemento que está aninhado no elemento da linha atual (para i=1) ou que está sob o elemento que tem o nome Name***i-1***. Se Name***n*** começar com '@', ele será mapeado para um atributo de elemento Name***n-1*** .  
  
 Por exemplo, a consulta a seguir retorna a ID e o nome de um funcionário que são representados como um elemento complexo EmpName que contém um Nome, Segundo nome e Sobrenome.  
  
```  
SELECT EmployeeID "@EmpID",   
       FirstName  "EmpName/First",   
       MiddleName "EmpName/Middle",   
       LastName   "EmpName/Last"  
FROM   HumanResources.Employee E, Person.Contact C  
WHERE  E.EmployeeID = C.ContactID  
AND    E.EmployeeID=1  
FOR XML PATH  
```  
  
 Os nomes de colunas são usados como um caminho para construir XML no modo PATH. O nome da coluna que contém valores de ID de funcionário, começa com '\@'. Portanto, um atributo **EmpID**, é adicionada para o `row` elemento. Todas as outras colunas incluem uma barra ('/') no nome da coluna que indica hierarquia. O XML resultante terá o `EmpName` filho sob o `row` elemento e o `EmpName` filho terá `First`, `Middle` e `Last` filhos do elemento.  
  
```  
<row EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
    <Last>Achong</Last>  
  </EmpName>  
</row>  
```  
  
 O segundo nome do funcionário é nulo e, por padrão, o valor nulo é mapeado para a ausência do elemento ou atributo. Se você quiser elementos gerados para os valores NULL, poderá especificar a diretiva ELEMENTS com XSINIL conforme mostrado nesta consulta.  
  
```  
SELECT EmployeeID "@EmpID",   
       FirstName  "EmpName/First",   
       MiddleName "EmpName/Middle",   
       LastName   "EmpName/Last"  
FROM   HumanResources.Employee E, Person.Contact C  
WHERE  E.EmployeeID = C.ContactID  
AND    E.EmployeeID=1  
FOR XML PATH, ELEMENTS XSINIL  
```  
  
 Este é o resultado:  
  
```  
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
  
 Além da ID e do nome, a consulta a seguir recupera um endereço de funcionário. De acordo com o caminho nos nomes das colunas para colunas de endereço, um `Address` elemento filho é adicionado para o `row` elemento e os detalhes do endereço são adicionados como filhos do elemento a `Address` elemento.  
  
```  
SELECT EmployeeID   "@EmpID",   
       FirstName    "EmpName/First",   
       MiddleName   "EmpName/Middle",   
       LastName     "EmpName/Last",  
       AddressLine1 "Address/AddrLine1",  
       AddressLine2 "Address/AddrLIne2",  
       City         "Address/City"  
FROM   HumanResources.Employee E, Person.Contact C, Person.Address A  
WHERE  E.EmployeeID = C.ContactID  
AND    E.AddressID = A.AddressID  
AND    E.EmployeeID=1  
FOR XML PATH  
```  
  
 Este é o resultado:  
  
```  
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
 Se várias colunas subsequentes compartilharem o mesmo prefixo de caminho, elas serão agrupadas sob o mesmo nome. Se diferentes prefixos de namespace estiverem sendo usados, mesmo que estejam associados ao mesmo namespace, um caminho será considerado diferente. Na consulta anterior, as colunas FirstName, MiddleName e LastName compartilham o mesmo prefixo EmpName. Portanto, eles são adicionados como filhos do `EmpName` elemento. Isso também é o caso quando for criar o `Address` elemento no exemplo anterior.  
  
## <a name="one-column-has-a-different-name"></a>Uma coluna tem um nome diferente  
 Se uma coluna com um nome diferente aparecer no meio, ela quebrará o agrupamento, conforme mostrado na seguinte consulta modificada. A consulta quebra o agrupamento de FirstName, MiddleName e LastName, conforme especificado na consulta anterior, adicionando colunas de endereço no meio das colunas FirstName e MiddleName.  
  
```  
SELECT EmployeeID "@EmpID",   
       FirstName "EmpName/First",   
       AddressLine1 "Address/AddrLine1",  
       AddressLine2 "Address/AddrLIne2",  
       City "Address/City",  
       MiddleName "EmpName/Middle",   
       LastName "EmpName/Last"  
FROM   HumanResources.EmployeeAddress E, Person.Contact C, Person.Address A  
WHERE  E.EmployeeID = C.ContactID  
AND    E.AddressID = A.AddressID  
AND    E.EmployeeID=1  
FOR XML PATH  
```  
  
 Como resultado, a consulta cria dois `EmpName` elementos. A primeira `EmpName` elemento tem o `FirstName` filho do elemento e a segunda `EmpName` elemento tem o `MiddleName` e `LastName` filhos do elemento.  
  
 Este é o resultado:  
  
```  
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
  
## <a name="see-also"></a>Consulte também  
 [Usar o modo PATH com FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  

