---
title: Função Count (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:count function
- count function [XQuery]
ms.assetid: a9f7131f-23e1-4d4d-a36c-180447543926
author: rothja
ms.author: jroth
ms.openlocfilehash: f1b56d549d00fb0b76c530a5274adb6a9c82c80c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85643714"
---
# <a name="aggregate-functions---count"></a>Funções de Agregação – count
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  Retorna o número de itens contidos na sequência especificada por *$ARG*.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn:count($arg as item()*) as xs:integer  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Itens a serem contados.  
  
## <a name="remarks"></a>Comentários  
 Retornará 0 se *$ARG* for uma sequência vazia.  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em relação a instâncias XML que são armazenadas em várias colunas de tipo **XML** no banco de dados AdventureWorks.  
  
### <a name="a-using-the-count-xquery-function-to-count-the-number-of-work-center-locations-in-the-manufacturing-of-a-product-model"></a>a. Usando a função count() XQuery para contar o número de locais de centro de trabalho na fabricação de um modelo de produto  
 A consulta a seguir conta o número de locais de centro de trabalho no processo de fabricação de um modelo de produto (ProductModelID=7).  
  
```  
SELECT Production.ProductModel.ProductModelID,   
       Production.ProductModel.Name,   
       Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
       <NoOfWorkStations>  
          { count(/AWMI:root/AWMI:Location) }  
       </NoOfWorkStations>  
') as WorkCtrCount  
FROM Production.ProductModel  
WHERE Production.ProductModel.ProductModelID=7  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   A palavra-chave **namespace** no [prólogo XQuery](../xquery/modules-and-prologs-xquery-prolog.md) define um prefixo de namespace. O prefixo é então usado no corpo do XQuery.  
  
-   A consulta constrói XML que inclui o elemento <`NoOfWorkStations`>.  
  
-   A função **Count ()** no corpo do XQuery conta o número de <`Location` elementos>.  
  
 Este é o resultado:  
  
```  
ProductModelID   Name                 WorkCtrCount       
-------------- ---------------------------------------------------  
7             HL Touring Frame  <NoOfWorkStations>6</NoOfWorkStations>     
```  
  
 Você também pode construir o XML para incluir o nome e a ID do modelo do produto, como mostrado na seguinte consulta:  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
       <NoOfWorkStations  
             ProductModelID= "{ sql:column("Production.ProductModel.ProductModelID") }"   
             ProductModelName = "{ sql:column("Production.ProductModel.Name") }" >  
          { count(/AWMI:root/AWMI:Location) }  
       </NoOfWorkStations>  
') as WorkCtrCount  
FROM Production.ProductModel  
WHERE Production.ProductModel.ProductModelID= 7  
```  
  
 Este é o resultado:  
  
```  
<NoOfWorkStations ProductModelID="7"   
                  ProductModelName="HL Touring Frame">6</NoOfWorkStations>  
```  
  
 Em vez de XML, você pode retornar esses valores como tipo não xml, como mostrado na consulta a seguir. A consulta usa o [método Value () (tipo de dados XML)](../t-sql/xml/value-method-xml-data-type.md) para recuperar a contagem de locais do centro de trabalho.  
  
```  
SELECT  ProductModelID,   
        Name,   
        Instructions.value('declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
           count(/AWMI:root/AWMI:Location)', 'int' ) as WorkCtrCount  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Este é o resultado:  
  
```  
ProductModelID    Name            WorkCtrCount  
-------------- ---------------------------------  
7              HL Touring Frame        6     
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções XQuery em tipos de dados xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
