---
title: Propriedade RecordCount (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::RecordCount
- Recordset15::GetRecordCount
- Recordset15::get_RecordCount
helpviewer_keywords:
- RecordCount property [ADO]
ms.assetid: 834f0121-394a-44d4-ad7d-999b43a6fe63
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a6ee9d1ea1c4e996c9608bc1ce76ff3f1baa7c62
ms.sourcegitcommit: ccb05cb5a4cccaf7ffa9e85a4684fa583bab914e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2018
---
# <a name="recordcount-property-ado"></a>Propriedade RecordCount (ADO)

Indica o número de registros em um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.
  
## <a name="return-value"></a>Valor de retorno

Retorna um **longo** valor que indica o número de registros a **registros**.
  
## <a name="remarks"></a>Remarks

Use o **RecordCount** são de propriedade para descobrir quantos registros em um **registros** objeto. A propriedade retorna -1 quando o ADO não é possível determinar o número de registros ou se o tipo de cursor ou o provedor não oferece suporte **RecordCount**. Lendo o **RecordCount** propriedade em um fechado **registros** causa um erro.

#### <a name="bookmarks-or-approximate-positioning"></a>Indicadores ou aproximado de posicionamento

Se o objeto de conjunto de registros *does* oferecer suporte a qualquer um dos indicadores ou aproximado de posicionamento, essa propriedade retorna o número exato de registros no conjunto de registros. Essa propriedade retorna o número exato, independentemente se o conjunto de registros foi totalmente preenchido.

Por outro lado, se o objeto de conjunto de registros não *não* oferece suporte a indicadores ou posicionamento aproximado, acessar essa propriedade pode ser um consumo significativo de recursos. O consumo ocorre porque todos os registros devem ser recuperados e contadas para retornar um valor de RecordCount exato.

- **adBookmark** relacionados para os indicadores.
- **adApproxPosition** relacionada ao posicionamento aproximado.

> [!NOTE]
> Nas versões do ADO 2.8 e anteriores, o provedor SQLOLEDB busca todos os registros quando um cursor do lado do servidor é usado, apesar do fato de que ela retorna **True** para ambos **suporta (adApproxPosition)** e **Suporta (adBookmark)**.
  
O tipo de cursor a **registros** objeto afeta o número de registros pode ser determinado. O **RecordCount** propriedade retornará -1 para um cursor de somente avanço; a contagem real para um static ou cursor de conjunto de chaves; e -1 ou a contagem real de um cursor dinâmico, dependendo da fonte de dados.
  
## <a name="applies-to"></a>Aplica-se a

[Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também

[Exemplo de propriedades de RecordCount (VB) e filtro](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)   
[Exemplo de propriedades de RecordCount (VC + +) e filtro](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)   
[Propriedade AbsolutePosition (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
[Propriedade PageCount (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)
