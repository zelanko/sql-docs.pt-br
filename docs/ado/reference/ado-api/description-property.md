---
title: Propriedade de descrição | Microsoft Docs
description: Saiba mais sobre a propriedade Description do objeto Error no ADO que retorna um valor de cadeia de caracteres que contém uma descrição do erro.
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::Description
- Error::GetDescription
- Error::get_Description
helpviewer_keywords:
- Description property
ms.assetid: 4b5d6790-6c29-42aa-bf78-d9cfb8ad7965
author: rothja
ms.author: jroth
ms.openlocfilehash: 7060810eba49ad5e1b9385a090788690b43e07eb
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973907"
---
# <a name="description-property"></a>Propriedade Description
Descreve um objeto de [erro](../../../ado/reference/ado-api/error-object.md) .  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um valor de **cadeia de caracteres** que contém uma descrição do erro.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **Descrição** para obter uma breve descrição do erro. Exiba essa propriedade para alertar o usuário sobre um erro que você não pode ou não deseja manipular. A cadeia de caracteres será proveniente do ADO ou de um provedor.  
  
 Os provedores são responsáveis por passar o texto de erro específico para o ADO. O ADO adiciona um objeto de [erro](../../../ado/reference/ado-api/error-object.md) à coleção de **erros** para cada erro de provedor ou aviso recebido. Enumere a coleção de **erros** para rastrear os erros que o provedor passa.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Error](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades Description, HelpContext, ArquivoDeAjuda, NativeError, Number, Source e SQLState (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Exemplo das propriedades Description, HelpContext, ArquivoDeAjuda, NativeError, Number, Source e SQLState (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Propriedades HelpContext, HelpFile](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Propriedade Number (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Propriedade Source (Erro ADO)](../../../ado/reference/ado-api/source-property-ado-error.md)
