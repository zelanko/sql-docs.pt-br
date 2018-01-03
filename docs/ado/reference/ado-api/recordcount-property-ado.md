---
title: Propriedade RecordCount (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::RecordCount
- Recordset15::GetRecordCount
- Recordset15::get_RecordCount
helpviewer_keywords: RecordCount property [ADO]
ms.assetid: 834f0121-394a-44d4-ad7d-999b43a6fe63
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f33a73aa4aa322d6eb0a00612789f4048a24e85d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="recordcount-property-ado"></a>Propriedade RecordCount (ADO)
Indica o número de registros em um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um **longo** valor que indica o número de registros a **registros**.  
  
## <a name="remarks"></a>Remarks  
 Use o **RecordCount** são de propriedade para descobrir quantos registros em um **registros** objeto. A propriedade retorna -1 quando o ADO não é possível determinar o número de registros ou se o tipo de cursor ou o provedor não oferece suporte **RecordCount**. Lendo o **RecordCount** propriedade em um fechado **registros** causa um erro.  
  
 Se o **registros** objeto oferece suporte ao posicionamento aproximado ou indicadores??? ou seja, **suporta (adApproxPosition)** ou **suporta (adBookmark)**, respectivamente, retornar **True**??? Esse valor será o número exato de registros de **registros**, independentemente de se ele foi totalmente preenchido. Se o **registros** objeto não dá suporte para o posicionamento aproximado, essa propriedade pode ser um consumo significativo de recursos porque todos os registros terá que ser recuperados e contadas para retornar uma precisão **RecordCount** valor.  
  
> [!NOTE]
>  Nas versões do ADO 2.8 e anteriores, o provedor SQLOLEDB busca todos os registros quando um cursor do lado do servidor é usado, apesar do fato de que ela retorna **True** para ambos **suporta (adApproxPosition)** e **Suporta (adBookmark)**.  
  
 O tipo de cursor a **registros** objeto afeta o número de registros pode ser determinado. O **RecordCount** propriedade retornará -1 para um cursor de somente avanço; a contagem real para um static ou cursor de conjunto de chaves; e -1 ou a contagem real de um cursor dinâmico, dependendo da fonte de dados.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de propriedades de RecordCount (VB) e filtro](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)   
 [Exemplo de propriedades de RecordCount (VC + +) e filtro](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)   
 [Propriedade AbsolutePosition (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
 [Propriedade PageCount (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)
