---
title: Campos de coleção (ADO) | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918713"
---
# <a name="fields-collection-ado"></a>Coleção Fields (ADO)
Contém todos os [campo](../../../ado/reference/ado-api/field-object.md) objetos de uma [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) ou [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto.  
  
## <a name="remarks"></a>Comentários  
 Um **conjunto de registros** objeto tem um **campos** coleção composta por **campo** objetos. Cada **campo** objeto corresponde a uma coluna na **conjunto de registros**. Você pode preencher a **campos** coleção antes de abrir o **conjunto de registros** chamando o [atualizar](../../../ado/reference/ado-api/refresh-method-ado.md) método na coleção.  
  
> [!NOTE]
>  Consulte a **campo** tópico de objeto para obter uma explicação mais detalhada de como usar **campo** objetos.  
  
 O **campos** coleção tem um [Append](../../../ado/reference/ado-api/append-method-ado.md) método, que provisoriamente cria e adiciona uma **campo** objeto à coleção e um **atualizar**método, que finaliza quaisquer adições ou exclusões.  
  
 Um **registro** objeto tem dois campos especiais que podem ser indexados com [FieldEnum](../../../ado/reference/ado-api/fieldenum.md) constantes. Uma constante acessa um campo que contém o fluxo padrão para o **registro**, e o outro acessa um campo que contém a cadeia de caracteres de URL absoluta para o **registro**.  
  
 Determinados provedores (por exemplo, o [Microsoft OLE DB Provider para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)) pode preencher o **campos** coleção com um subconjunto de campos disponíveis para o **registro** ou **conjunto de registros**. Outros campos não serão adicionados à coleção até que o primeiro são referenciadas por nome ou indexados pelo seu código.  
  
 Se você tentar fazer referência a um campo inexistente pelo nome, um novo **campo** será acrescentado ao objeto de **campos** coleção com uma [Status](../../../ado/reference/ado-api/status-property-ado-field.md) de  **adFieldPendingInsert**. Quando você chama [atualização](../../../ado/reference/ado-api/update-method.md), ADO criará um novo campo na fonte de dados se permitido pelo seu provedor.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades de coleção de campos, métodos e eventos](../../../ado/reference/ado-api/fields-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)
