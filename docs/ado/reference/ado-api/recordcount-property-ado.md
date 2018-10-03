---
title: Propriedade RecordCount (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::RecordCount
- Recordset15::GetRecordCount
- Recordset15::get_RecordCount
helpviewer_keywords:
- RecordCount property [ADO]
ms.assetid: 834f0121-394a-44d4-ad7d-999b43a6fe63
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fa6f29c480244919de71d06cf3d56e672f00c47f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47623090"
---
# <a name="recordcount-property-ado"></a>Propriedade RecordCount (ADO)

Indica o número de registros em uma [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.
  
## <a name="return-value"></a>Valor retornado

Retorna um **longo** valor que indica o número de registros na **conjunto de registros**.
  
## <a name="remarks"></a>Comentários

Use o **RecordCount** são de propriedade para descobrir quantos registros em uma **Recordset** objeto. A propriedade retornará -1 quando o ADO não é possível determinar o número de registros ou se o tipo de cursor ou o provedor não suportar **RecordCount**. Lendo a **RecordCount** propriedade em um fechado **Recordset** causa um erro.

#### <a name="bookmarks-or-approximate-positioning"></a>Indicadores ou aproximado de posicionamento

Se o objeto Recordset *faz* oferecer suporte a qualquer um dos indicadores ou aproximado de posicionamento, essa propriedade retorna o número exato de registros no conjunto de registros. Essa propriedade retorna o número exato, independentemente se o conjunto de registros foi totalmente preenchido.

Por outro lado, se o objeto Recordset *não* dão suporte a indicadores ou aproximado de posicionamento, acessar essa propriedade pode ser um dreno significativo nos recursos. O que consome ocorre porque todos os registros devem ser recuperados e contadas para retornar um valor de RecordCount preciso.

- **adBookmark** relacionados aos indicadores.
- **adApproxPosition** relacionada ao posicionamento aproximado.

> [!NOTE]
> Nas versões do ADO 2.8 e anteriores, o provedor SQLOLEDB busca todos os registros quando um cursor do lado do servidor é usado, apesar do fato de que ele retorna **verdadeira** para ambos **dá suporte a (adApproxPosition)** e **Dá suporte a (adBookmark)**.
  
O tipo de cursor do **Recordset** objeto afeta se o número de registros pode ser determinado. O **RecordCount** propriedade retornará -1 para um cursor de somente avanço; a contagem real para um estático ou cursor de conjunto de chaves; e o -1 ou a contagem real para um cursor dinâmico, dependendo da fonte de dados.
  
## <a name="applies-to"></a>Aplica-se a

[Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também

[Exemplo de Filter e RecordCount propriedades (VB)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)   
[Exemplo de Filter e RecordCount propriedades (VC + +)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)   
[Propriedade AbsolutePosition (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
[Propriedade PageCount (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)
