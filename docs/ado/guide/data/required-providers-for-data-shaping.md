---
title: Necessário provedores para Data Shaping | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], data shaping
- data shaping [ADO], providers required
ms.assetid: d49d48d2-ac2d-4c11-895c-5a149b444620
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7edd3b3cacd097380b5d14ad55ed115ff93cf072
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63280501"
---
# <a name="required-providers-for-data-shaping"></a>Provedores necessários para data shaping
Formatação de dados normalmente requer que dois provedores. O provedor de serviço [Data Shaping Service para OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md), fornece os dados de modelagem de funcionalidade e um provedor de dados, como o provedor OLE DB para SQL Server, fornece linhas de dados para popular o moldado [conjunto de registros ](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
 O nome do provedor de serviços (MSDataShape) pode ser especificado como o valor da [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto [provedor](../../../ado/reference/ado-api/provider-property-ado.md) propriedade ou a palavra-chave de cadeia de conexão "Provider = MSDataShape;".  
  
 O nome do provedor de dados pode ser especificado como o valor do **provedor de dados** propriedade dinâmica, que é adicionada para o **Conexão** objeto [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção por a Data Shaping Service para OLE DB ou a palavra-chave de cadeia de conexão "**provedor de dados =**_provedor_".  
  
 Nenhum provedor de dados é necessária se o **conjunto de registros** não é preenchida (por exemplo, como em um fabricadas **Recordset** onde as colunas são criadas com a nova palavra-chave). Nesse caso, especifique "**provedor de dados =** none;".  
  
## <a name="example"></a>Exemplo  
  
```  
Dim cnn As New ADODB.Connection  
cnn.Provider = "MSDataShape"  
cnn.Open "Data Provider=SQLOLEDB;Integrated Security=SSPI;Database=Northwind"  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de Data Shaping](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática de forma formal](../../../ado/guide/data/formal-shape-grammar.md)   
 [Modelar comandos em geral](../../../ado/guide/data/shape-commands-in-general.md)
