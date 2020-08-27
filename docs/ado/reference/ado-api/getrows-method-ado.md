---
description: Método GetRows (ADO)
title: Método GetRows (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 666eabf1a375c6a86826bc94600846bd10a0ecfe
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990907"
---
# <a name="getrows-method-ado"></a>Método GetRows (ADO)
Recupera vários registros de um objeto [Recordset](./recordset-object-ado.md) em uma matriz.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
array = recordset.GetRows(Rows, Start, Fields )  
```  
  
## <a name="return-value"></a>Valor retornado  
 Retorna uma **variante** cujo valor é uma matriz bidimensional.  
  
#### <a name="parameters"></a>Parâmetros  
 *Linhas*  
 Opcional. Um valor [GetRowsOptionEnum](./getrowsoptionenum.md) que indica o número de registros a serem recuperados. O padrão é **adGetRowsRest**.  
  
 *Iniciar*  
 Opcional. Um valor de **cadeia de caracteres** ou uma **variante** que é avaliada como o indicador para o registro do qual a operação **GetRows** deve começar. Você também pode usar um valor [BookmarkEnum](./bookmarkenum.md) .  
  
 *Fields*  
 Opcional. Uma **variante** que representa um único nome de campo ou posição ordinal, ou uma matriz de nomes de campo ou números de posição ordinais. O ADO retorna apenas os dados nesses campos.  
  
## <a name="remarks"></a>Comentários  
 Use o método **GetRows** para copiar registros de um **conjunto de registros** em uma matriz bidimensional. O primeiro subscrito identifica o campo e o segundo identifica o número do registro. A variável de *matriz* é automaticamente dimensionada para o tamanho correto quando o método **GetRows** retorna os dados.  
  
 Se você não especificar um valor para o argumento *Rows* , o método **GetRows** recuperará automaticamente todos os registros no objeto **Recordset** . Se você solicitar mais registros do que o disponível, **GetRows** retornará apenas o número de registros disponíveis.  
  
 Se o objeto **Recordset** der suporte a indicadores, você poderá especificar em qual registro o método **GetRows** deve começar a recuperar dados, passando o valor da propriedade [Bookmark](./bookmark-property-ado.md) do registro no argumento *Start* .  
  
 Se você quiser restringir os campos que a chamada **GetRows** retorna, poderá passar um único campo nome/número ou uma matriz de nomes/números de campo no argumento *campos* .  
  
 Depois que você chamar **GetRows**, o próximo registro não lido se tornará o registro atual ou a propriedade [EOF](./bof-eof-properties-ado.md) será definida como **true** se não houver mais registros.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método GetRows (VB)](./getrows-method-example-vb.md)   
 [Exemplo do método GetRows (VC++)](./getrows-method-example-vc.md)