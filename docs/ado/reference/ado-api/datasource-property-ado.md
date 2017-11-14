---
title: Propriedade de fonte de dados (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset20::DataSource
helpviewer_keywords:
- DataSource property [ADO]
ms.assetid: 300a702a-3544-48c5-b759-83b511fe97e0
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b6003f19993835b937828948658e29cfb271cada
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="datasource-property-ado"></a>Propriedade de fonte de dados (ADO)
Indica um objeto que contém dados a ser representado como um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
## <a name="remarks"></a>Comentários  
 Essa propriedade é usada para criar controles associados a dados com o ambiente de dados. O ambiente de dados mantém a chamada de conjuntos de dados (fontes de dados) que contém objetos (membros de dados) que serão representados como um **registros** objeto*.*  
  
 O [DataMember](../../../ado/reference/ado-api/datamember-property.md) e **DataSource** propriedades devem ser usadas em conjunto.  
  
 O objeto referenciado deve implementar o **IDataSource** de interface e deve conter um **IRowset** interface.  
  
## <a name="usage"></a>Uso  
  
```  
Dim rs as New ADODB.Recordset  
rs.DataMember = "Command"     'Name of the rowset to bind to.  
Set rs.DataSource = myDE      'Name of the object containing an IRowset.  
```  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade DataMember](../../../ado/reference/ado-api/datamember-property.md)

