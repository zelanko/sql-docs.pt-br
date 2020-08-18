---
description: Método Open (ADO MD)
title: Método Open (ADO MD) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 56d6a216b7d21723d84d374b09a9c0b8c6c4806b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440818"
---
# <a name="open-method-ado-md"></a>Método Open (ADO MD)
Recupera os resultados de uma consulta multidimensional e retorna os resultados para um [células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Cellset.Open Source, ActiveConnection  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Origem*  
 Opcional. Uma **variante** que é avaliada como uma consulta multidimensional válida, como uma consulta MDX (multidimensional Expression). O argumento de *origem* corresponde à propriedade [Source](../../../ado/reference/ado-md-api/source-property-ado-md.md) . Para obter mais informações sobre o MDX, consulte a documentação de [OLE DB para processamento analítico online (OLAP)](https://msdn.microsoft.com/8a7673c6-3ca1-4411-9f1e-adf1e47df4f3) no SDK do Microsoft Data Access Components.  
  
 *ActiveConnection*  
 Opcional. Uma **variante** que é avaliada como uma cadeia de caracteres especificando um nome de variável de objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md) ADO válido ou uma definição para uma conexão. O argumento *ActiveConnection* especifica a conexão na qual abrir o objeto [células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) . Se você passar uma definição de conexão para esse argumento, o ADO abrirá uma nova conexão usando os parâmetros especificados. O argumento *ActiveConnection* corresponde à propriedade [ActiveConnection](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md) .  
  
## <a name="remarks"></a>Comentários  
 O método **Open** gerará um erro se um dos seus parâmetros for omitido e seu valor de propriedade correspondente não tiver sido definido antes de tentar abrir o **células**.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Cellset (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de células (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Propriedade ActiveConnection (ADO MD)](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md)   
 [Método Close (ADO MD)](../../../ado/reference/ado-md-api/close-method-ado-md.md)   
 [Objeto de conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Propriedade Source (ADO MD)](../../../ado/reference/ado-md-api/source-property-ado-md.md)   
 [Propriedade State (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)
