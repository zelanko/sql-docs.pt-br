---
description: Fabricar conjuntos de registros hierárquicos
title: Conjuntos de registros hierárquicos fabricando | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 2f418d2eb21f2cb02223234f6231efb39b232faa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453398"
---
# <a name="fabricating-hierarchical-recordsets"></a>Fabricar conjuntos de registros hierárquicos
O exemplo a seguir mostra como malhar um conjunto de registros hierárquico sem uma fonte de dados subjacente usando a gramática de formatação de dados para definir colunas para conjuntos de **registros**pai, filho e neto.  
  
 Para malhar um **conjunto de registros**hierárquico, você deve especificar o [serviço de modelagem de dados da Microsoft para OLE DB (provedor de serviços ADO)](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (MSDataShape) e pode especificar um valor de provedor de dados de nenhum no parâmetro de cadeia de conexão do método [Open](../../../ado/reference/ado-api/open-method-ado-connection.md) do objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md) . Para obter mais informações, consulte [provedores necessários para o Shaping de dados](../../../ado/guide/data/required-providers-for-data-shaping.md).  
  
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
  
 Assim que o **conjunto de registros** tiver sido criei, ele poderá ser populado, manipulado ou persistido em um arquivo.  
  
## <a name="see-also"></a>Consulte Também  
 [Acessando linhas em um conjunto de registros hierárquico](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [Gramática forma formal](../../../ado/guide/data/formal-shape-grammar.md)   
 [Provedores necessários para o Shaping de dados](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Cláusula de ANEXAção de forma](../../../ado/guide/data/shape-append-clause.md)   
 [Modelar comandos em geral](../../../ado/guide/data/shape-commands-in-general.md)
