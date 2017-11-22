---
title: "Propriedade de descrição | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Error::Description
- Error::GetDescription
- Error::get_Description
helpviewer_keywords: Description property
ms.assetid: 4b5d6790-6c29-42aa-bf78-d9cfb8ad7965
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fc23f481c709c0901eb6a2020b51629a16f659eb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="description-property"></a>Propriedade Description
Descreve um [erro](../../../ado/reference/ado-api/error-object.md) objeto.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um **cadeia de caracteres** valor que contém uma descrição do erro.  
  
## <a name="remarks"></a>Comentários  
 Use o **descrição** propriedade para obter uma descrição curta do erro. Exiba esta propriedade para alertar o usuário a um erro que você não pode ou não desejar tratar. A cadeia de caracteres será proveniente do ADO ou um provedor.  
  
 Provedores são responsáveis por passar o texto do erro específico para ADO. ADO adiciona um [erro](../../../ado/reference/ado-api/error-object.md) o objeto para o **erros** coleção para cada provedor de erro ou aviso que ele recebe. Enumerar o **erros** coleção para rastrear os erros que o provedor transmite.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Error](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>Consulte também  
 [Descrição, HelpContext, HelpFile, NativeError, número, fonte e exemplo de propriedades de SQLState (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Descrição, HelpContext, HelpFile, NativeError, número, fonte e exemplo de propriedades de SQLState (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Propriedades HelpContext e HelpFile](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Propriedade de número (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Propriedade Source (Erro ADO)](../../../ado/reference/ado-api/source-property-ado-error.md)
