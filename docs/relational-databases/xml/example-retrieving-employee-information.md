---
title: "Exemplo: Recuperando informa&#231;&#245;es de funcion&#225;rios | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-xml"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "modo EXPLICIT"
ms.assetid: 63cd6569-2600-485b-92b4-1f6ba09db219
caps.latest.revision: 9
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 9
---
# Exemplo: Recuperando informa&#231;&#245;es de funcion&#225;rios
  Este exemplo recupera uma ID e um nome de funcionário para cada funcionário. No banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], a employeeID pode ser obtida na coluna BusinessEntityID da tabela Employee. Nomes de funcionários podem ser obtidos da tabela Person. A coluna BusinessEntityID pode ser usada para unir as tabelas.  
  
 Digamos que você queira a transformação de FOR XML EXPLICIT para gerar XML, conforme mostrado aqui:  
  
```  
<Employee EmpID="1" >  
  <Name FName="Ken" LName="Sánchez" />  
</Employee>  
...  
```  
  
 Como há dois níveis na hierarquia, você escreve duas consultas `SELECT` e aplica UNION ALL. Esta é a primeira consulta que recupera valores do elemento <`Employee`> e seus atributos. A consulta atribui `1` como o valor de `Tag` para o elemento <`Employee`> e NULL como `Parent`, pois ele é o elemento de nível superior.  
  
```  
SELECT 1    as Tag,  
       NULL as Parent,  
       E.BusinessEntityID AS [Employee!1!EmpID],  
       NULL       as [Name!2!FName],  
       NULL       as [Name!2!LName]  
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
ON  E.BusinessEntityID = P.BusinessEntityID;  
```  
  
 Esta é a segunda consulta. Ela recupera valores do elemento <`Name`>. Ela atribui `2` como o valor `Tag` do elemento <`Name`> e `1` como o valor de marca `Parent` que identifica <`Employee`> como o pai.  
  
```  
SELECT 2 as Tag,  
       1 as Parent,  
       E.BusinessEntityID,  
       FirstName,   
       LastName   
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
ON  E.BusinessEntityID = P.BusinessEntityID;  
```  
  
 Você combina estas consultas com `UNION AL`L, aplica `FOR XML EXPLICIT`, e especifica a cláusula `ORDER BY` exigida. Você deve classificar o conjunto de linhas primeiro por `BusinessEntityID` e, em seguida, pelo nome para que os valores NULL no nome sejam exibidos primeiro. Se você executar a consulta a seguir sem a cláusula FOR XML, poderá ver a tabela universal gerada.  
  
 Esta é a consulta final:  
  
```  
SELECT 1    as Tag,  
       NULL as Parent,  
       E.BusinessEntityID as [Employee!1!EmpID],  
       NULL       as [Name!2!FName],  
       NULL       as [Name!2!LName]  
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
ON  E.BusinessEntityID = P.BusinessEntityID  
UNION ALL  
SELECT 2 as Tag,  
       1 as Parent,  
       E.BusinessEntityID,  
       FirstName,   
       LastName   
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
ON  E.BusinessEntityID = P.BusinessEntityID  
ORDER BY [Employee!1!EmpID],[Name!2!FName]  
FOR XML EXPLICIT;  
```  
  
 Este é o resultado parcial:  
  
 `<Employee EmpID="1">`  
  
 `<Name FName="Ken" LName="Sánchez" />`  
  
 `</Employee>`  
  
 `<Employee EmpID="2">`  
  
 `<Name FName="Terri" LName="Duffy" />`  
  
 `</Employee>`  
  
 `...`  
  
 O primeiro `SELECT` especifica nomes para as colunas no conjunto de linhas resultante. Esses nomes formam dois grupos de colunas. O grupo que tem o valor da `Tag` `1` no nome da coluna identifica `Employee` como um elemento e `EmpID` como o atributo. O outro grupo de colunas tem o valor da `Tag` `2` na coluna e identifica <`Name`> como o elemento e `FName` e `LName` como os atributos.  
  
 Esta tabela mostra o conjunto de linhas parcial gerado pela consulta:  
  
 `Tag Parent  Employee!1!EmpID Name!2!FName Name!2!LName`  
  
 `--- ------  ---------------- ------------ ------------`  
  
 `1   NULL    1                NULL         NULL`  
  
 `2   1       1                Ken          Sánchez`  
  
 `1   NULL    2                NULL         NULL`  
  
 `2   1       2                Terri        Duffy`  
  
 `1   NULL    3                NULL         NULL`  
  
 `2   1       3                Roberto      Tamburello`  
  
 `...`  
  
 É assim que as linhas na tabela universal são processadas para produzir a árvore XML resultante:  
  
 A primeira linha identifica o valor 1 da `Tag` `1`. Portanto, o grupo de colunas que tem o valor da `Tag` `1` é identificado, `Employee!1!EmpID`. Essa coluna identifica `Employee` como o nome do elemento. Em seguida, é criado um elemento <`Employee`> que tem os atributos `EmpID`. Os valores das colunas correspondentes são atribuídos a esses atributos.  
  
 A segunda linha tem o valor da `Tag` `2`. Portanto, o grupo de colunas que tem o valor da `Tag` `2` no nome da coluna, `Name!2!FName`, `Name!2!LName`, é identificado. Esses nomes de colunas identificam `Name` como o nome do elemento. É criado um elemento <`Name`> que tem os atributos `FName` e `LName`. Em seguida, os valores das colunas correspondentes são atribuídos a esses atributos. Essa linha identifica `1` como `Parent`. Esse elemento filho é adicionado ao elemento <`Employee`> anterior.  
  
 Esse processo é repetido para o restante das linhas do conjunto de linhas. Observe a importância de ordenar as linhas na tabela universal de forma que FOR XML EXPLICIT possa processar o conjunto de linhas em ordem e gerar o XML desejado.  
  
## Consulte também  
 [Usar o modo EXPLICIT com FOR XML](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
  
  