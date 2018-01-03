---
title: "Campos de coleção (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Fields
- Recordset15::Fields
- _Record::Fields
helpviewer_keywords: Fields collection [ADO]
ms.assetid: 7c371474-b88f-4730-afa5-44163a0488d5
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 32b9f8cff20d7b2e82479985af4219439c8b2233
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="fields-collection-ado"></a>Coleção de campos (ADO)
Contém todos os [campo](../../../ado/reference/ado-api/field-object.md) objetos de um [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) ou [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto.  
  
## <a name="remarks"></a>Remarks  
 Um **registros** objeto tem um **campos** coleção composta de **campo** objetos. Cada **campo** objeto corresponde a uma coluna de **registros**. Você pode preencher o **campos** coleção antes de abrir o **registros** chamando o [atualizar](../../../ado/reference/ado-api/refresh-method-ado.md) método na coleção.  
  
> [!NOTE]
>  Consulte o **campo** tópico para obter uma explicação mais detalhada de como usar **campo** objetos.  
  
 O **campos** coleção tem um [Append](../../../ado/reference/ado-api/append-method-ado.md) método, que provisoriamente cria e adiciona um **campo** objeto à coleção e um **atualizar**método, que finaliza adições ou exclusões.  
  
 Um **registro** objeto tem dois campos especiais que podem ser indexados com [FieldEnum](../../../ado/reference/ado-api/fieldenum.md) constantes. Uma constante acessa um campo que contém o fluxo padrão para o **registro**, e o outro acessa um campo que contém a cadeia de caracteres de URL absoluta para o **registro**.  
  
 Alguns provedores (por exemplo, o [Microsoft OLE DB Provider para publicação de Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)) pode preencher o **campos** coleção com um subconjunto de campos disponíveis para o **registro** ou **registros**. Outros campos não serão adicionados à coleção até que o primeiro são referenciadas por nome ou indexados por seu código.  
  
 Se você tentar fazer referência a um campo inexistente por nome, um novo **campo** objeto será acrescentado ao **campos** coleção com uma [Status](../../../ado/reference/ado-api/status-property-ado-field.md) de  **adFieldPendingInsert**. Quando você chama [atualização](../../../ado/reference/ado-api/update-method.md), ADO criará um novo campo na fonte de dados se permitido pelo provedor.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades de coleção de campos, métodos e eventos](../../../ado/reference/ado-api/fields-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)
