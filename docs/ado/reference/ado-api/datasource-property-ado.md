---
title: Propriedade DataSource (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::DataSource
helpviewer_keywords:
- DataSource property [ADO]
ms.assetid: 300a702a-3544-48c5-b759-83b511fe97e0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad42ea14e58e28bf5eee0e5aac66c5a8fc309f2f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47801269"
---
# <a name="datasource-property-ado"></a>Propriedade DataSource (ADO)
Indica um objeto que contém dados a ser representado como uma [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
## <a name="remarks"></a>Comentários  
 Essa propriedade é usada para criar controles associados a dados com o ambiente de dados. O ambiente de dados mantém a chamada de coleções de dados (fontes de dados) que contém objetos (membros de dados) que serão representados como uma **conjunto de registros** objeto *.*  
  
 O [DataMember](../../../ado/reference/ado-api/datamember-property.md) e **DataSource** propriedades devem ser usadas em conjunto.  
  
 O objeto referenciado deve implementar o **IDataSource** interface e deve conter um **IRowset** interface.  
  
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
