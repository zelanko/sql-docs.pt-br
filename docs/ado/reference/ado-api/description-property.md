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
manager: jroth
ms.openlocfilehash: 7b743a5fb6673baf886c4b9327bd8ad93b00d3b1
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66698329"
---
# <a name="description-property"></a>Propriedade Description
Descreve um [erro](../../../ado/reference/ado-api/error-object.md) objeto.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um **cadeia de caracteres** valor que contém uma descrição do erro.  
  
## <a name="remarks"></a>Comentários  
 Use o **descrição** propriedade para obter uma breve descrição do erro. Exiba essa propriedade para alertar o usuário a um erro que você não pode ou não deseja manipular. A cadeia de caracteres provenientes do ADO ou um provedor.  
  
 Provedores são responsáveis por passando o texto do erro específico ao ADO. ADO adiciona uma [erro](../../../ado/reference/ado-api/error-object.md) do objeto para o **erros** coleção para cada provedor de erro ou aviso, ele recebe. Enumerar os **erros** coleção para rastrear os erros que o provedor passa.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Error](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>Consulte também  
 [Descrição, HelpContext, HelpFile, NativeError, número, código-fonte e exemplo de propriedades de SQLState (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Descrição, HelpContext, HelpFile, NativeError, número, código-fonte e SQLState exemplo das propriedades (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Propriedades HelpContext, HelpFile](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Propriedade Number (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Propriedade Source (Erro ADO)](../../../ado/reference/ado-api/source-property-ado-error.md)
