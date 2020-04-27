---
title: Método GetRows (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::GetRows
- Recordset15::raw_GetRows
helpviewer_keywords:
- Getrows method [ADO]
ms.assetid: 14b92860-4171-47d9-a413-dd60dd6a8880
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d96b7968c7aba8d1249db2f43b53fc8a22596419
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67918455"
---
# <a name="getrows-method-ado"></a>Método GetRows (ADO)
Recupera vários registros de um objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) em uma matriz.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
array = recordset.GetRows(Rows, Start, Fields )  
```  
  
## <a name="return-value"></a>Valor retornado  
 Retorna uma **variante** cujo valor é uma matriz bidimensional.  
  
#### <a name="parameters"></a>Parâmetros  
 *Linhas*  
 Opcional. Um valor [GetRowsOptionEnum](../../../ado/reference/ado-api/getrowsoptionenum.md) que indica o número de registros a serem recuperados. O padrão é **adGetRowsRest**.  
  
 *Início*  
 Opcional. Um valor de **cadeia de caracteres** ou uma **variante** que é avaliada como o indicador para o registro do qual a operação **GetRows** deve começar. Você também pode usar um valor [BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md) .  
  
 *Fields*  
 Opcional. Uma **variante** que representa um único nome de campo ou posição ordinal, ou uma matriz de nomes de campo ou números de posição ordinais. O ADO retorna apenas os dados nesses campos.  
  
## <a name="remarks"></a>Comentários  
 Use o método **GetRows** para copiar registros de um **conjunto de registros** em uma matriz bidimensional. O primeiro subscrito identifica o campo e o segundo identifica o número do registro. A variável de *matriz* é automaticamente dimensionada para o tamanho correto quando o método **GetRows** retorna os dados.  
  
 Se você não especificar um valor para o argumento *Rows* , o método **GetRows** recuperará automaticamente todos os registros no objeto **Recordset** . Se você solicitar mais registros do que o disponível, **GetRows** retornará apenas o número de registros disponíveis.  
  
 Se o objeto **Recordset** der suporte a indicadores, você poderá especificar em qual registro o método **GetRows** deve começar a recuperar dados, passando o valor da propriedade [Bookmark](../../../ado/reference/ado-api/bookmark-property-ado.md) do registro no argumento *Start* .  
  
 Se você quiser restringir os campos que a chamada **GetRows** retorna, poderá passar um único campo nome/número ou uma matriz de nomes/números de campo no argumento *campos* .  
  
 Depois que você chamar **GetRows**, o próximo registro não lido se tornará o registro atual ou a propriedade [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) será definida como **true** se não houver mais registros.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método GetRows (VB)](../../../ado/reference/ado-api/getrows-method-example-vb.md)   
 [Exemplo do método GetRows (VC++)](../../../ado/reference/ado-api/getrows-method-example-vc.md)   
