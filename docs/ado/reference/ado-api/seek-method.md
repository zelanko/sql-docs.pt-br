---
title: Método de busca | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset21::Seek
- Recordset21::raw_Seek
helpviewer_keywords:
- Seek method [ADO]
ms.assetid: 129293d2-19d3-4940-bf64-483ee72fb4a1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3e2ee81ac2ede53eb4fdbcfe8d3b5987db96f1ad
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67917013"
---
# <a name="seek-method"></a>Método Seek
Pesquisa o índice de um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) para localizar rapidamente a linha que corresponde aos valores especificados e altera a posição da linha atual para essa linha.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
recordset.Seek KeyValues, SeekOption  
```  
  
#### <a name="parameters"></a>parâmetros  
 *Valores de*  
 Uma matriz de valores **variantes** . Um índice consiste em uma ou mais colunas e a matriz contém um valor a ser comparado com cada coluna correspondente.  
  
 *SeekOption*  
 Um valor [SeekEnum](../../../ado/reference/ado-api/seekenum.md) que especifica o tipo de comparação a ser feita entre as colunas do índice e os *valores*correspondentes.  
  
## <a name="remarks"></a>Comentários  
 Use o método **Seek** em conjunto com a propriedade [index](../../../ado/reference/ado-api/index-property.md) se o provedor subjacente oferecer suporte a índices no objeto **Recordset** . Use o método de [suporte](../../../ado/reference/ado-api/supports-method.md)**(adSeek)** para determinar se o provedor subjacente dá suporte à **busca**e ao método de **suporte (adIndex)** para determinar se o provedor oferece suporte a índices. (Por exemplo, o [provedor de OLE DB para Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) dá suporte a **busca** e **índice**.)  
  
 Se o **Seek** não localizar a linha desejada, nenhum erro ocorrerá e a linha será posicionada no final do **conjunto de registros**. Defina a propriedade **index** para o índice desejado antes de executar esse método.  
  
 Esse método tem suporte apenas com cursores do lado do servidor. Não há suporte para busca quando o valor da propriedade [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) do objeto **Recordset** é **adUseClient**.  
  
 Esse método só pode ser usado quando o objeto **Recordset** tiver sido aberto com um valor [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) de **adCmdTableDirect**.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método Seek e da propriedade index (VB)](../../../ado/reference/ado-api/seek-method-and-index-property-example-vb.md)   
 [Exemplo da propriedade index e do método Seek (VC + +)](../../../ado/reference/ado-api/seek-method-and-index-property-example-vc.md)   
 [Método Find (ADO)](../../../ado/reference/ado-api/find-method-ado.md)   
 [Propriedade Index](../../../ado/reference/ado-api/index-property.md)
