---
description: Método Open (ADO MD)
title: Método Open (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 5c7b403ed89ae9933b4169af4e53921205318ccd
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88986227"
---
# <a name="open-method-ado-md"></a>Método Open (ADO MD)
Recupera os resultados de uma consulta multidimensional e retorna os resultados para um [células](./cellset-object-ado-md.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Cellset.Open Source, ActiveConnection  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Origem*  
 Opcional. Uma **variante** que é avaliada como uma consulta multidimensional válida, como uma consulta MDX (multidimensional Expression). O argumento de *origem* corresponde à propriedade [Source](./source-property-ado-md.md) . Para obter mais informações sobre o MDX, consulte a documentação de [OLE DB para processamento analítico online (OLAP)](/previous-versions/windows/desktop/ms717005(v=vs.85)) no SDK do Microsoft Data Access Components.  
  
 *ActiveConnection*  
 Opcional. Uma **variante** que é avaliada como uma cadeia de caracteres especificando um nome de variável de objeto de [conexão](../ado-api/connection-object-ado.md) ADO válido ou uma definição para uma conexão. O argumento *ActiveConnection* especifica a conexão na qual abrir o objeto [células](./cellset-object-ado-md.md) . Se você passar uma definição de conexão para esse argumento, o ADO abrirá uma nova conexão usando os parâmetros especificados. O argumento *ActiveConnection* corresponde à propriedade [ActiveConnection](./activeconnection-property-ado-md.md) .  
  
## <a name="remarks"></a>Comentários  
 O método **Open** gerará um erro se um dos seus parâmetros for omitido e seu valor de propriedade correspondente não tiver sido definido antes de tentar abrir o **células**.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Cellset (ADO MD)](./cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de células (VB)](./cellset-example-vb.md)   
 [Propriedade ActiveConnection (ADO MD)](./activeconnection-property-ado-md.md)   
 [Método Close (ADO MD)](./close-method-ado-md.md)   
 [Objeto de conexão (ADO)](../ado-api/connection-object-ado.md)   
 [Propriedade Source (ADO MD)](./source-property-ado-md.md)   
 [Propriedade State (ADO MD)](./state-property-ado-md.md)