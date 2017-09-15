---
title: "Oferece suporte ao método | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::raw_Supports
- Recordset15::Supports
helpviewer_keywords:
- Supports method [ADO]
ms.assetid: 298fc41c-0b55-42fc-b373-c5133b4da6a5
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 60e3039e48ea203b0585dba1ecbeaf7ad3e57907
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="supports-method"></a>Oferece suporte ao método
Determina se um especificado [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto oferece suporte a um determinado tipo de funcionalidade.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um **booliano** valor que indica se todos os recursos identificado pelo *CursorOptions* argumento são suportados pelo provedor.  
  
#### <a name="parameters"></a>Parâmetros  
 *CursorOptions*  
 Um **longo** expressão que consiste em um ou mais [CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md) valores.  
  
## <a name="remarks"></a>Comentários  
 Use o **dá suporte a** método para determinar quais tipos de funcionalidade um **registros** objeto oferece suporte. Se o **registros** objeto suporta os recursos cujos constantes correspondentes estão em *CursorOptions*, o **dá suporte a** método retorna **True**. Caso contrário, retornará **False**.  
  
> [!NOTE]
>  Embora o **dá suporte a** método pode retornar **True** para uma determinada funcionalidade, ele não garante que o provedor pode tornar o recurso disponível em todas as circunstâncias. O **suporta** método simplesmente retorna se o provedor pode oferecer suporte a funcionalidade especificada, supondo que determinadas condições forem atendidas. Por exemplo, o **dá suporte a** método pode indicar que um **registros** objeto dá suporte a atualizações, embora o cursor é baseado em uma associação de tabela de várias, algumas colunas que não são atualizáveis.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo do método dá suporte a (VB)](../../../ado/reference/ado-api/supports-method-example-vb.md)   
 [Dá suporte ao método de exemplo (VC + +)](../../../ado/reference/ado-api/supports-method-example-vc.md)   
 [Propriedade CursorType (ADO)](../../../ado/reference/ado-api/cursortype-property-ado.md)

