---
description: Propriedades HelpContext, HelpFile
title: Propriedades HelpContext, HelpFile | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: d9ac9c7f712514f50ab8d40704700924ac344d23
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990837"
---
# <a name="helpcontext-helpfile-properties"></a>Propriedades HelpContext, HelpFile
Indica o arquivo de ajuda e o tópico associado a um objeto de [erro](./error-object.md) .  
  
## <a name="return-values"></a>Valores de retorno  
  
-   **HelpContextId** Retorna uma ID de contexto, como um valor **longo** , para um tópico em um arquivo de ajuda.  
  
-   **ArquivoDeAjuda** Retorna um valor de **cadeia de caracteres** que é avaliado como um caminho totalmente resolvido para um arquivo de ajuda.  
  
## <a name="remarks"></a>Comentários  
 Se um arquivo de ajuda for especificado na propriedade **HelpFile** , a propriedade **HelpContext** será usada para exibir automaticamente o tópico da ajuda que ele identifica. Se não houver nenhum tópico de ajuda relevante disponível, a propriedade **HelpContext** retornará zero e a propriedade **HelpFile** retornará uma cadeia de caracteres de comprimento zero ("").  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Error](./error-object.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades Description, HelpContext, ArquivoDeAjuda, NativeError, Number, Source e SQLState (VB)](./description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Exemplo das propriedades Description, HelpContext, ArquivoDeAjuda, NativeError, Number, Source e SQLState (VC + +)](./description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Propriedade de descrição](./description-property.md)   
 [Propriedade Number (ADO)](./number-property-ado.md)   
 [Propriedade Source (Erro ADO)](./source-property-ado-error.md)