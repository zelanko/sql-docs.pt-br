---
description: Propriedade Source (Erro ADO)
title: Propriedade Source (erro ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::get_Source
- Error::Source
- Error::GetSource
helpviewer_keywords:
- Source property [ADO Error]
ms.assetid: 4044ba15-f013-4c4c-9fe1-b4410fe9a778
author: rothja
ms.author: jroth
ms.openlocfilehash: fa7fc5c5098b6e429960e5d72702111abab55ac2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442048"
---
# <a name="source-property-ado-error"></a>Propriedade Source (Erro ADO)
Indica o nome do objeto ou aplicativo que originalmente gerou um erro.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um valor de **cadeia de caracteres** que indica o nome de um objeto ou aplicativo.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **Source** em um objeto [Error](../../../ado/reference/ado-api/error-object.md) para determinar o nome do objeto ou aplicativo que originalmente gerou um erro. Pode ser o nome da classe do objeto ou a ID programática. Para erros no ADO, o valor da propriedade será **ADODB.** _Objectname_, em que *objectname* é o nome do objeto que disparou o erro. Para o ADOX e o ADO MD, o valor será **ADOX.** _Objectname_ e **ADOMD.** _Objectname_, respectivamente.  
  
 Com base na documentação de erro das propriedades de **origem**, [número](../../../ado/reference/ado-api/number-property-ado.md)e [Descrição](../../../ado/reference/ado-api/description-property.md) dos objetos de **erro** , você pode escrever código que manipulará o erro adequadamente.  
  
 A propriedade **Source** é somente leitura para objetos de **erro** .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto de erro](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades Description, HelpContext, ArquivoDeAjuda, NativeError, Number, Source e SQLState (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Exemplo das propriedades Description, HelpContext, ArquivoDeAjuda, NativeError, Number, Source e SQLState (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Propriedade de descrição](../../../ado/reference/ado-api/description-property.md)   
 [Propriedades HelpContext, HelpFile](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Propriedade Number (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Propriedade Source (registro ADO)](../../../ado/reference/ado-api/source-property-ado-record.md)   
 [Propriedade Source (Conjunto de registros ADO)](../../../ado/reference/ado-api/source-property-ado-recordset.md)
