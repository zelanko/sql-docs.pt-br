---
title: Coleção Fields (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Fields
- Recordset15::Fields
- _Record::Fields
helpviewer_keywords:
- Fields collection [ADO]
ms.assetid: 7c371474-b88f-4730-afa5-44163a0488d5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9c9216ee655e371633837c5653ebac56fac1a782
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67918713"
---
# <a name="fields-collection-ado"></a>Coleção Fields (ADO)
Contém todos os objetos de [campo](../../../ado/reference/ado-api/field-object.md) de um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) ou objeto de [registro](../../../ado/reference/ado-api/record-object-ado.md) .  
  
## <a name="remarks"></a>Comentários  
 Um objeto **Recordset** tem uma coleção **Fields** composta de objetos **Field** . Cada objeto de **campo** corresponde a uma coluna no **conjunto de registros**. Você pode preencher a coleção **Fields** antes de abrir o **conjunto de registros** chamando o método [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) na coleção.  
  
> [!NOTE]
>  Consulte o tópico objeto **Field** para obter uma explicação mais detalhada de como usar objetos **Field** .  
  
 A coleção **Fields** tem um método [Append](../../../ado/reference/ado-api/append-method-ado.md) , que cria e adiciona um objeto **Field** à coleção, e um método **Update** , que finaliza quaisquer adições ou exclusões.  
  
 Um objeto de **registro** tem dois campos especiais que podem ser indexados com constantes [FieldEnum](../../../ado/reference/ado-api/fieldenum.md) . Uma constante acessa um campo que contém o fluxo padrão para o **registro**e o outro acessa um campo que contém a cadeia de caracteres de URL absoluta para o **registro**.  
  
 Determinados provedores (por exemplo, o [provedor de OLE DB da Microsoft para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)) podem preencher a coleção **Fields** com um subconjunto de campos disponíveis para o **registro** ou **conjunto de registros**. Outros campos não serão adicionados à coleção até que eles sejam referenciados pela primeira vez pelo nome ou indexados pelo seu código.  
  
 Se você tentar fazer referência a um campo inexistente por nome, um novo objeto de **campo** será anexado à coleção **Fields** com um [status](../../../ado/reference/ado-api/status-property-ado-field.md) de **adFieldPendingInsert**. Quando você chama [Update](../../../ado/reference/ado-api/update-method.md), o ADO criará um novo campo na fonte de dados, se permitido pelo seu provedor.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos da coleção Fields](../../../ado/reference/ado-api/fields-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto Campo](../../../ado/reference/ado-api/field-object.md)
