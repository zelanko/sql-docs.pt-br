---
title: Método (ADO MD) Open | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Open
- Cellset::Open
helpviewer_keywords:
- Open method [ADO MD]
ms.assetid: a87d8080-a238-45e5-bc80-9a8625b3810f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 237639f949b67d015cd37ccdf50a9e9a758a9210
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47702055"
---
# <a name="open-method-ado-md"></a>Método Open (ADO MD)
Recupera os resultados de uma consulta multidimensional e retorna os resultados para um [conjunto de células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Cellset.Open Source, ActiveConnection  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Origem*  
 Opcional. Um **Variant** que é avaliada como uma consulta multidimensional válida, como uma consulta MDX (Multidimensional Expression). O *fonte* argumento corresponde à [origem](../../../ado/reference/ado-md-api/source-property-ado-md.md) propriedade. Para obter mais informações sobre o MDX, consulte o [OLE DB para Online Analytical Processing (OLAP)](http://msdn.microsoft.com/8a7673c6-3ca1-4411-9f1e-adf1e47df4f3) documentação do Microsoft Data Access Components SDK.  
  
 *ActiveConnection*  
 Opcional. Um **Variant** que é avaliada como uma cadeia de caracteres especificando a um ADO válido [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) nome de variável ou uma definição para uma conexão do objeto. O *ActiveConnection* argumento especifica a conexão no qual abrir o [conjunto de células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) objeto. Se você passar uma definição de conexão para esse argumento, o ADO abre uma nova conexão usando os parâmetros especificados. O *ActiveConnection* argumento corresponde à [ActiveConnection](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md) propriedade.  
  
## <a name="remarks"></a>Comentários  
 O **abra** método gerará um erro se qualquer um dos seus parâmetros for omitido e seu valor de propriedade correspondente não foi definido antes da tentativa de abrir o **conjunto de células**.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Cellset (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de conjunto de células (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Propriedade ActiveConnection (ADO MD)](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md)   
 [Feche o método (ADO MD)](../../../ado/reference/ado-md-api/close-method-ado-md.md)   
 [Objeto de Conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Propriedade Source (ADO MD)](../../../ado/reference/ado-md-api/source-property-ado-md.md)   
 [Propriedade State (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)
