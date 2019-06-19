---
title: HelpContext, HelpFile propriedades | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::GetHelpContext
- Error::GetHelpFile
- Error::get_HelpFile
- Error::get_HelpContext
- Error::HelpContext
- Error::HelpFile
helpviewer_keywords:
- HelpContext property [ADO]
- HelpFile property [ADO]
ms.assetid: 2b9ef441-993c-44d4-8f87-fac0979dac1d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c9c980e293b06e7fa9642ace7d425b7ffd3c0197
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66694811"
---
# <a name="helpcontext-helpfile-properties"></a>Propriedades HelpContext, HelpFile
Indica o arquivo de Ajuda e o tópico associado a um [erro](../../../ado/reference/ado-api/error-object.md) objeto.  
  
## <a name="return-values"></a>Valores de retorno  
  
-   **IdentificaçãoDoContextoDaAjuda** retorna uma ID de contexto, como uma **longo** valor para um tópico em um arquivo de Ajuda.  
  
-   **HelpFile** retorna um **cadeia de caracteres** valor que é avaliada para um caminho totalmente resolvido para um arquivo de Ajuda.  
  
## <a name="remarks"></a>Comentários  
 Se um arquivo de Ajuda é especificado na **HelpFile** propriedade, o **HelpContext** propriedade é usada para exibir o tópico da Ajuda que ele identifica automaticamente. Se não houver nenhum tópico da Ajuda relevante disponíveis, o **HelpContext** propriedade retorna zero e o **HelpFile** propriedade retorna uma cadeia de caracteres de comprimento zero ("").  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Error](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>Consulte também  
 [Descrição, HelpContext, HelpFile, NativeError, número, código-fonte e exemplo de propriedades de SQLState (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Descrição, HelpContext, HelpFile, NativeError, número, código-fonte e SQLState exemplo das propriedades (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Propriedade Description](../../../ado/reference/ado-api/description-property.md)   
 [Propriedade Number (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Propriedade Source (Erro ADO)](../../../ado/reference/ado-api/source-property-ado-error.md)
