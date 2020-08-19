---
description: Propriedade DataSource (ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 8b85f163ddb3f1fc31116966127bc01efa17a262
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444218"
---
# <a name="datasource-property-ado"></a>Propriedade DataSource (ADO)
Indica um objeto que contém dados a serem representados como um objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) .  
  
## <a name="remarks"></a>Comentários  
 Essa propriedade é usada para criar controles ligados a dados com o ambiente de dados. O ambiente de dados mantém coleções de dados (fontes de dados) que contêm objetos nomeados (membros de dados) que serão representados como um objeto **Recordset** .  
  
 As propriedades [DataMember](../../../ado/reference/ado-api/datamember-property.md) e **DataSource** devem ser usadas em conjunto.  
  
 O objeto referenciado deve implementar a interface **IDataSource** e deve conter uma interface **IRowset** .  
  
## <a name="usage"></a>Uso  
  
```  
Dim rs as New ADODB.Recordset  
rs.DataMember = "Command"     'Name of the rowset to bind to.  
Set rs.DataSource = myDE      'Name of the object containing an IRowset.  
```  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedade DataMember](../../../ado/reference/ado-api/datamember-property.md)
