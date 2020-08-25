---
description: Propriedade Number (ADO)
title: Propriedade Number (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::Number
- Error::GetNumber
- Error::get_Number
helpviewer_keywords:
- number property [ADO]
ms.assetid: f92323c5-dd11-4a63-a505-d9014a0f067f
author: rothja
ms.author: jroth
ms.openlocfilehash: fe4984a9bdbeff69f7c2beba4d91833cdca85f50
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88774095"
---
# <a name="number-property-ado"></a>Propriedade Number (ADO)
Indica o número que identifica exclusivamente um objeto de [erro](./error-object.md) .  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um valor **longo** que pode corresponder a uma das constantes [ErrorValueEnum](./errorvalueenum.md) .  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **Number** para determinar qual erro ocorreu. O valor da propriedade é um número exclusivo que corresponde à condição de erro.  
  
 A coleção de [erros](./errors-collection-ado.md) retorna um HRESULT em formato hexadecimal (por exemplo, 0x80004005) ou um valor longo (por exemplo, 2147467259). Esses HRESULTs podem ser gerados por componentes subjacentes, como OLE DB ou até mesmo OLE. Para obter mais informações sobre esses números, consulte [erros (OLE DB)](/previous-versions/windows/desktop/ms724533(v=vs.85)) na [referência do programador de OLE DB](/previous-versions/windows/desktop/ms713643(v=vs.85))*.*  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Error](./error-object.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades Description, HelpContext, ArquivoDeAjuda, NativeError, Number, Source e SQLState (VB)](./description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Exemplo das propriedades Description, HelpContext, ArquivoDeAjuda, NativeError, Number, Source e SQLState (VC + +)](./description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Propriedade de descrição](./description-property.md)   
 [Propriedades HelpContext, HelpFile](./helpcontext-helpfile-properties.md)   
 [Propriedade Source (Erro ADO)](./source-property-ado-error.md)