---
description: Limites de um conjunto de registros
title: Limites de um conjunto de registros | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- EOF property [ADO], boundaries of a Recordset
- Recordset object [ADO], boundaries of a Recordset
- BOF property [ADO], boundaries of a Recordset
ms.assetid: c0dd4a0f-478d-4c5e-b5d5-7535f211d064
author: rothja
ms.author: jroth
ms.openlocfilehash: d89f25dc6e37c0b5c569d5db7c4f8486115ce94a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453708"
---
# <a name="boundaries-of-a-recordset"></a>Limites de um conjunto de registros
O **conjunto de registros** dá suporte às propriedades **BOF** e **EOF** para delinear o início e o fim, respectivamente, do conjunto de linhas. Você pode considerar **BOF** e **EOF** como registros "fantasma" posicionados no início e no final do **conjunto de registros**. Contando **BOF** e **EOF**, nosso **conjunto de registros** de exemplo terá a seguinte aparência:  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|BOF|||  
|7|Pêras secas-orgânicas do tio Bob|30, 0|  
|14|Tofu|23,2500|  
|28|Rssle chucrute|45,6000|  
|51|Maçãs secas Manjimup|53, 0|  
|74|Longlife Tofu|10, 0|  
|EOF|||  
  
 Quando um cursor passa para o último registro, **EOF** é definido como **true**; caso contrário, seu valor será **false**. Da mesma forma, quando o cursor se move antes do primeiro registro, **BOF** é definido como **true**; caso contrário, seu valor será **false**. Essas propriedades são comumente usadas para enumerar registros no conjunto de recursos, conforme ilustrado no fragmento de código do JScript a seguir.  
  
```  
while (objRecordset.EOF != true)   
{  
   // Work on the current record.  
   ...  
   // Advance the cursor forward to the next record.  
   objRecordset.MoveNext();  
}  
or  
while (objRecordset.BOF != true)   
{  
   // Work on the current record.  
   ...  
   // Move the cursor to the previous record.  
   objRecordset.MovePrevious();  
}  
```  
  
 Se **BOF** e **EOF** forem **verdadeiros**, o objeto **Recordset** estará vazio. Ambas as propriedades serão **false** para um objeto **Recordset** aberto recentemente e não vazio. Você pode usar as propriedades **BOF** e **EOF** juntas para determinar se um objeto **Recordset** está vazio ou não, conforme mostrado no fragmento de código JScript a seguir.  
  
```  
if (objRecordset.EOF == true && objRecordset.BOF == true)  
{  
   WScript.Echo("we got an empty dataset.");  
}  
else  
{  
   WScript.Echo("we got a full dataset.");  
}  
```  
  
 Esse esquema funciona para todos os tipos de cursor e é independente dos provedores subjacentes. Se você tentar determinar a desmarcação de um objeto **Recordset** verificando se o valor da propriedade **RecordCount** é zero (0) ou não, deverá tomar precauções para usar um cursor e um provedor apropriados que ofereçam suporte ao retorno do número de registros no resultado.  
  
 Se você excluir o último registro restante no objeto **Recordset** , o cursor será deixado em um estado indeterminado. As propriedades **BOF** e **EOF** podem permanecer **falsas** até que você tente reposicionar o registro atual, dependendo do provedor. Para obter mais informações, consulte [excluindo registros usando o método Delete](../../../ado/guide/data/deleting-records-using-the-delete-method.md).
