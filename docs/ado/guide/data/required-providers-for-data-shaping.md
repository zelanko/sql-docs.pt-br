---
title: Provedores necessários para o Shaping de dados | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: abda9d7a275ce100636efa58430009dd430fac0b
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760942"
---
# <a name="required-providers-for-data-shaping"></a>Provedores necessários para data shaping
A formatação de dados normalmente requer dois provedores. O provedor de serviços, o [Data Shaping Service para OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md), fornece a funcionalidade de formatação de dados e um provedor de dados, como o provedor de OLE DB para SQL Server, fornece linhas de dados para preencher o [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md)moldado.  
  
 O nome do provedor de serviços (MSDataShape) pode ser especificado como o valor da Propriedade do [provedor](../../../ado/reference/ado-api/provider-property-ado.md) de objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md) ou da palavra-chave da cadeia de conexão "Provider = MSDataShape;".  
  
 O nome do provedor de dados pode ser especificado como o valor da propriedade dinâmica **provedor de dados** , que é adicionada à coleção de [Propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) do objeto de **conexão** pelo serviço de data Shaping para OLE DB ou a palavra-chave da cadeia de conexão "**provedor de dados =** _Provider_".  
  
 Nenhum provedor de dados será necessário se o **conjunto de registros** não for preenchido (por exemplo, como em um conjunto de **registros** criei em que as colunas são criadas com a nova palavra-chave). Nesse caso, especifique "**provedor de dados =** None;".  
  
## <a name="example"></a>Exemplo  
  
```  
Dim cnn As New ADODB.Connection  
cnn.Provider = "MSDataShape"  
cnn.Open "Data Provider=SQLOLEDB;Integrated Security=SSPI;Database=Northwind"  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de formatação de dados](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática forma formal](../../../ado/guide/data/formal-shape-grammar.md)   
 [Modelar comandos em geral](../../../ado/guide/data/shape-commands-in-general.md)
