---
title: Fabricando conjuntos de registros hierárquicos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset fabrication [ADO]
- hierarchical Recordsets [ADO]
- fabricating hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: a584e642-a4a3-418e-bc20-3aff81a5625a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 17cf661e092e253e206b595dec5d807a35b895fb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47770884"
---
# <a name="fabricating-hierarchical-recordsets"></a>Fabricar conjuntos de registros hierárquicos
O exemplo a seguir mostra como fabricar um conjunto de registros hierárquico sem uma fonte de dados subjacente usando os dados de formatação a gramática para definir as colunas para o pai, filho e neto **conjuntos de registros**.  
  
 Para fabricar hierárquico **conjunto de registros**, você deve especificar o [Microsoft Data Shaping Service para OLE DB (provedor de serviços do ADO)](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (MSDataShape), e você pode especificar um valor nenhum no provedor de dados a parâmetro de cadeia de caracteres de conexão das [aberto](../../../ado/reference/ado-api/open-method-ado-connection.md) método da [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto. Para obter mais informações, consulte [provedores necessários para Data Shaping](../../../ado/guide/data/required-providers-for-data-shaping.md).  
  
```  
Dim cn As New ADODB.Connection  
Dim rsCustomers As New ADODB.Recordset  
  
cn.Open "Provider=MSDataShape;Data Provider=NONE;"  
  
strShape = _  
"SHAPE APPEND NEW adInteger AS CustID," & _  
            " NEW adChar(25) AS FirstName," & _  
            " NEW adChar(25) AS LastName," & _  
            " NEW adChar(12) AS SSN," & _  
            " NEW adChar(50) AS Address," & _  
         " ((SHAPE APPEND NEW adChar(80) AS VIN_NO," & _  
                        " NEW adInteger AS CustID," & _  
                        " NEW adChar(20) AS BodyColor, " & _  
                     " ((SHAPE APPEND NEW adChar(80) AS VIN_NO," & _  
                                    " NEW adChar(20) AS Make, " & _  
                                    " NEW adChar(20) AS Model," & _  
                                    " NEW adChar(4) AS Year) " & _  
                        " AS VINS RELATE VIN_NO TO VIN_NO))" & _  
            " AS Vehicles RELATE CustID TO CustID) "  
  
rsCustomers.Open strShape, cn, adOpenStatic, adLockOptimistic, -1  
```  
  
 Assim que o **Recordset** tiver sido gerados, ele pode ser preenchido, manipulado ou mantido em um arquivo.  
  
## <a name="see-also"></a>Consulte também  
 [Acessando linhas em um conjunto de registros hierárquico](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [Gramática de forma formal](../../../ado/guide/data/formal-shape-grammar.md)   
 [Provedores necessários para Data Shaping](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Cláusula APPEND de forma](../../../ado/guide/data/shape-append-clause.md)   
 [Modelar comandos em geral](../../../ado/guide/data/shape-commands-in-general.md)
