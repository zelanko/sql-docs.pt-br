---
description: Objeto Catalog (ADO MD)
title: Objeto de catálogo (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Catalog
helpviewer_keywords:
- Catalog object [ADO MD]
ms.assetid: 11f6f896-d69c-44a4-94cd-d54c93140e4a
author: rothja
ms.author: jroth
ms.openlocfilehash: b198e9765a8d0e68e61ecd3f9ed334e34c714ea8
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778335"
---
# <a name="catalog-object-ado-md"></a>Objeto Catalog (ADO MD)
Contém informações de esquema multidimensional (ou seja, cubos e dimensões subjacentes, hierarquias, níveis e membros) específicas para um provedor de dados multidimensional (MDP).  
  
## <a name="remarks"></a>Comentários  
 Com as coleções e propriedades de um objeto de **Catálogo** , você pode fazer o seguinte:  
  
-   Abra o catálogo definindo a propriedade [ActiveConnection](./activeconnection-property-ado-md.md) como um objeto de [conexão](../ado-api/connection-object-ado.md) ADO padrão ou como uma cadeia de conexão válida.  
  
-   Identifique o **Catálogo** com a propriedade [Name](./name-property-ado-md.md) .  
  
-   Itere pelos cubos em um catálogo usando a coleção [CubeDefs](./cubedefs-collection-ado-md.md) .  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos](./catalog-object-properties-methods-and-events-ado-md.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de catálogo (VB)](./catalog-example-vb.md)   
 [Objeto de conexão (ADO)](../ado-api/connection-object-ado.md)   
 [Coleção CubeDefs (ADO MD)](./cubedefs-collection-ado-md.md)