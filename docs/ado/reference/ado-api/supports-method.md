---
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1d1df1d780cf9e1e631f6b146e45cc0a34da9438
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66710686"
---
# <a name="supports-method"></a>Método Supports
Determina se um especificado [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto dá suporte a um determinado tipo de funcionalidade.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um **Boolean** valor que indica se todos os recursos identificados pela *CursorOptions* argumento são suportados pelo provedor.  
  
#### <a name="parameters"></a>Parâmetros  
 *CursorOptions*  
 Um **longo** expressão consiste em um ou mais [CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md) valores.  
  
## <a name="remarks"></a>Comentários  
 Use o **dá suporte a** método para determinar quais tipos de funcionalidade um **Recordset** objeto dá suporte. Se o **conjunto de registros** objeto suporta os recursos cujos constantes correspondentes estão no *CursorOptions*, o **dá suporte a** retorno do método **True**. Caso contrário, retornará **falsos**.  
  
> [!NOTE]
>  Embora o **suporta** método pode retornar **verdadeiro** para uma determinada funcionalidade, ele não garante que o provedor pode disponibilizar o recurso em todas as circunstâncias. O **dá suporte a** método simplesmente retorna se o provedor pode dar suporte a funcionalidade especificada, supondo que determinadas condições forem atendidas. Por exemplo, o **suporta** método pode indicar que um **conjunto de registros** objeto dá suporte a atualizações, mesmo que o cursor estiver baseado em uma junção múltipla de tabela, algumas colunas que não são atualizáveis.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Dá suporte ao exemplo do método (VB)](../../../ado/reference/ado-api/supports-method-example-vb.md)   
 [Dá suporte ao exemplo do método (VC + +)](../../../ado/reference/ado-api/supports-method-example-vc.md)   
 [Propriedade CursorType (ADO)](../../../ado/reference/ado-api/cursortype-property-ado.md)
