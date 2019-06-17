---
title: Os limites de um conjunto de registros | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 967ccb49cd2bbaa805420e7c982cc11721931022
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702351"
---
# <a name="boundaries-of-a-recordset"></a>Limites de um conjunto de registros
**Conjunto de registros** oferece suporte a **BOF** e **EOF** propriedades para delimitar o início e no final, respectivamente, do conjunto de dados. Você pode pensar **BOF** e **EOF** como "fantasmas" registros que são posicionados no início e no final do **conjunto de registros**. Contando **BOF** e **EOF**, em nosso exemplo **Recordset** agora ficaria assim:  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|BOF|||  
|7|Peras secas orgânico de tio Bob|30.0000|  
|14|Bananas|23.2500|  
|28|Rssle chucrute|45.6000|  
|51|Maçãs Secas Manjimup|53.0000|  
|74|Longlife Tofu|10.0000|  
|EOF|||  
  
 Quando um cursor se move além do último registro, **EOF** é definido como **verdadeiro**; caso contrário, seu valor é **False**. Da mesma forma, quando o cursor é movido antes do primeiro registro, **BOF** é definido como **verdadeiro**; caso contrário, seu valor é **False**. Essas propriedades são comumente usadas ao enumerar os registros no conjunto de dados, conforme ilustrado no seguinte fragmento de código JScript.  
  
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
  
 Se os dois **BOF** e **EOF** são **verdadeiro**, o **Recordset** objeto está vazio. Ambas as propriedades serão **falsos** para um recém-aberta, vazio **Recordset** objeto. Você pode usar o **BOF** e **EOF** propriedades juntas para determinar se um **Recordset** objeto está vazio ou não, conforme mostrado no seguinte fragmento de código JScript.  
  
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
  
 Esse esquema funciona para todos os tipos de cursor e é independente dos provedores subjacentes. Se você tentar determinar o par de um **conjunto de registros** objeto verificando se seu **RecordCount** valor da propriedade é zero (0) ou não, você deve tomar precauções para usar um cursor apropriado e o provedor que suporte ao retorno do número de registros no resultado.  
  
 Se você excluir o último registro restante na **Recordset** do objeto, o cursor será deixado em um estado indeterminado. O **BOF** e **EOF** as propriedades podem permanecer **False** até que você tente reposicionar o registro atual, de acordo com o provedor. Para obter mais informações, consulte [registros de exclusão usando o método Delete](../../../ado/guide/data/deleting-records-using-the-delete-method.md).
