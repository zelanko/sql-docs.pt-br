---
description: Propriedade RecordCount (ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 5c7615a61622be136b0be951b71a1788d5f45bab
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442478"
---
# <a name="recordcount-property-ado"></a>Propriedade RecordCount (ADO)

Indica o número de registros em um objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) .
  
## <a name="return-value"></a>Valor de retorno

Retorna um valor **longo** que indica o número de registros no **conjunto**de registros.
  
## <a name="remarks"></a>Comentários

Use a propriedade **RecordCount** para descobrir quantos registros estão em um objeto **Recordset** . A propriedade retorna-1 quando ADO não pode determinar o número de registros ou se o provedor ou o tipo de cursor não dá suporte a **RecordCount**. A leitura da propriedade **RecordCount** em um **conjunto de registros** fechado causa um erro.

#### <a name="bookmarks-or-approximate-positioning"></a>Indicadores ou posicionamento aproximado

Se *o objeto Recordset* oferecer suporte a indicadores ou posicionamento aproximado, essa propriedade retornará o número exato de registros no conjunto de registros. Essa propriedade retorna o número exato, independentemente de o conjunto de registros ter sido totalmente preenchido.

Por outro lado, se o objeto Recordset *não oferecer suporte* a indicadores ou posicionamento aproximado, o acesso a essa propriedade poderá ser um dreno significativo nos recursos. O dreno ocorre porque todos os registros devem ser recuperados e contados para retornar um valor de RecordCount preciso.

- **adBookmark** relacionados a indicadores.
- **adApproxPosition** está relacionado ao posicionamento aproximado.

> [!NOTE]
> No ADO versões 2,8 e anteriores, o provedor SQLOLEDB busca todos os registros quando um cursor do lado do servidor é usado, apesar do fato de que ele retorna **true** para **suporte (AdApproxPosition)** e **dá suporte a (adBookmark)**.
  
O tipo de cursor do objeto **Recordset** afeta se o número de registros pode ser determinado. A propriedade **RecordCount** retornará-1 para um cursor de somente avanço; a contagem real para um cursor estático ou de conjunto de chaves; e-1 ou a contagem real de um cursor dinâmico, dependendo da fonte de dados.
  
## <a name="applies-to"></a>Aplica-se A

[Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também

[Exemplo das propriedades Filter e RecordCount (VB)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)   
[Exemplo das propriedades Filter e RecordCount (VC + +)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)   
[Propriedade AbsolutePosition (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
[Propriedade PageCount (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)
