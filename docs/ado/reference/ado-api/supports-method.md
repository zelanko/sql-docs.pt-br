---
description: Método Supports
title: Dá suporte ao método | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Supports
- Recordset15::Supports
helpviewer_keywords:
- Supports method [ADO]
ms.assetid: 298fc41c-0b55-42fc-b373-c5133b4da6a5
author: rothja
ms.author: jroth
ms.openlocfilehash: 8b0c05118b0f4b8f952b933bc2474bd1f0879865
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441748"
---
# <a name="supports-method"></a>Método Supports
Determina se um objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) especificado dá suporte a um tipo específico de funcionalidade.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um valor **booliano** que indica se todos os recursos identificados pelo argumento *CursorOptions* têm suporte do provedor.  
  
#### <a name="parameters"></a>Parâmetros  
 *CursorOptions*  
 Uma expressão **longa** que consiste em um ou mais valores [CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md) .  
  
## <a name="remarks"></a>Comentários  
 Use o método de **suporte** para determinar os tipos de funcionalidade aos quais um objeto **Recordset** dá suporte. Se o objeto **Recordset** der suporte aos recursos cujas constantes correspondentes estão em *CursorOptions*, o método de **suporte** retornará **true**. Caso contrário, retornará **false**.  
  
> [!NOTE]
>  Embora o método de **suporte** possa retornar **true** para uma determinada funcionalidade, ele não garante que o provedor possa disponibilizar o recurso em todas as circunstâncias. O método de **suporte** simplesmente retorna se o provedor pode dar suporte à funcionalidade especificada, supondo que determinadas condições sejam atendidas. Por exemplo, o método de **suporte** pode indicar que um objeto **Recordset** dá suporte a atualizações, embora o cursor seja baseado em uma junção com várias tabelas, algumas colunas que não são atualizáveis.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método de suporte (VB)](../../../ado/reference/ado-api/supports-method-example-vb.md)   
 [Exemplo do método de suporte (VC + +)](../../../ado/reference/ado-api/supports-method-example-vc.md)   
 [Propriedade CursorType (ADO)](../../../ado/reference/ado-api/cursortype-property-ado.md)
