---
title: Propriedade de descrição | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 48b3a6987e6c7b6c3754f5041d90d248520345ab
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67933084"
---
# <a name="description-property"></a>Propriedade Description
Descreve um objeto de [erro](../../../ado/reference/ado-api/error-object.md) .  
  
## <a name="return-value"></a>Valor retornado  
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
