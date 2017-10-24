---
title: "Necessário provedores para modelagem de dados | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- providers [ADO], data shaping
- data shaping [ADO], providers required
ms.assetid: d49d48d2-ac2d-4c11-895c-5a149b444620
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c2dc7048ea3442a77f6aadf7d7b1868c2ac9d833
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="required-providers-for-data-shaping"></a>Provedores necessários para modelagem de dados
Modelagem de dados normalmente requer dois provedores. O provedor de serviços, [Data Shaping Service para OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md), fornece os dados de formatação de funcionalidade e um provedor de dados, como o provedor OLE DB para SQL Server, que fornece linhas de dados para preencher a forma [conjunto de registros ](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
 O nome do provedor de serviço (MSDataShape) pode ser especificado como o valor da [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto [provedor](../../../ado/reference/ado-api/provider-property-ado.md) propriedade ou a palavra-chave cadeia de caracteres de conexão "Provider = MSDataShape;".  
  
 O nome do provedor de dados pode ser especificado como o valor do **provedor de dados** propriedades dinâmicas, que é adicionada para o **Conexão** objeto [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção por o Data Shaping Service para OLE DB ou a palavra-chave cadeia de caracteres de conexão "**provedor de dados =***provedor*".  
  
 Nenhum provedor de dados é necessária se o **registros** não é populada (por exemplo, como um fabricadas **registros** onde as colunas são criadas com a nova palavra-chave). Nesse caso, especifique "**provedor de dados =**none;".  
  
## <a name="example"></a>Exemplo  
  
```  
Dim cnn As New ADODB.Connection  
cnn.Provider = "MSDataShape"  
cnn.Open "Data Provider=SQLOLEDB;Integrated Security=SSPI;Database=Northwind"  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de modelagem de dados](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática de forma formal](../../../ado/guide/data/formal-shape-grammar.md)   
 [Modelar comandos em geral](../../../ado/guide/data/shape-commands-in-general.md)

