---
title: O método de pesquisa | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 89b82d6efe87cec6643d68837447ed64a6f69059
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47612424"
---
# <a name="seek-method"></a>Método Seek
Pesquisa o índice de um [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) para localizar rapidamente a linha que corresponde aos valores especificados e altera a posição da linha atual para aquela linha.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
recordset.Seek KeyValues, SeekOption  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *KeyValues*  
 Uma matriz de **Variant** valores. Um índice consiste em uma ou mais colunas e a matriz contém um valor a ser comparada com cada coluna correspondente.  
  
 *SeekOption*  
 Um [SeekEnum](../../../ado/reference/ado-api/seekenum.md) valor que especifica o tipo de comparação a ser feita entre as colunas do índice e correspondente *KeyValues*.  
  
## <a name="remarks"></a>Comentários  
 Use o **Seek** método junto com o [índice](../../../ado/reference/ado-api/index-property.md) propriedade se o provedor subjacente que dá suporte a índices no **Recordset** objeto. Use o [dá suporte a](../../../ado/reference/ado-api/supports-method.md)**(adSeek)** método para determinar se o provedor subjacente dá suporte à **busca**e o **Supports(adIndex)** método para determinar se o provedor dá suporte a índices. (Por exemplo, o [OLE DB Provider for Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) dá suporte a **busca** e **índice**.)  
  
 Se **Seek** não localizar a linha desejada, nenhum erro ocorre e a linha é posicionado no final o **conjunto de registros**. Defina as **índice** propriedade para o índice desejada antes de executar esse método.  
  
 Esse método é compatível apenas com cursores do lado do servidor. Busca não é suportado quando o **conjunto de registros** do objeto [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) é o valor da propriedade **adUseClient**.  
  
 Esse método só pode ser usado quando o **conjunto de registros** objeto tenha sido aberto com um [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) valor de **adCmdTableDirect**.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo da propriedade Index (VB) e do método Seek](../../../ado/reference/ado-api/seek-method-and-index-property-example-vb.md)   
 [Exemplo da propriedade Index (VC + +) e do método Seek](../../../ado/reference/ado-api/seek-method-and-index-property-example-vc.md)   
 [Método Find (ADO)](../../../ado/reference/ado-api/find-method-ado.md)   
 [Propriedade Index](../../../ado/reference/ado-api/index-property.md)
