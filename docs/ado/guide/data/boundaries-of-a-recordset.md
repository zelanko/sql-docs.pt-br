---
title: Limites de um conjunto de registros | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- EOF property [ADO], boundaries of a Recordset
- Recordset object [ADO], boundaries of a Recordset
- BOF property [ADO], boundaries of a Recordset
ms.assetid: c0dd4a0f-478d-4c5e-b5d5-7535f211d064
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 66dec387cc91a2d0bd4d3aded73a6b4301aff593
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="boundaries-of-a-recordset"></a>Limites de um conjunto de registros
**Conjunto de registros** oferece suporte a **BOF** e **EOF** propriedades para delimitar o início e término, respectivamente, do conjunto de dados. Você pode pensar **BOF** e **EOF** como "fantasmas" registros que são posicionados no início e fim do **registros**. Contagem de **BOF** e **EOF**, nosso exemplo **registros** agora ficaria assim:  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|BOF|||  
|7|Peras secas orgânicos de tio de Bob|30.0000|  
|14|Tofu|23.2500|  
|28|Rssle chucrute|45.6000|  
|51|Maçãs Secas Manjimup|53.0000|  
|74|Longlife Tofu|10.0000|  
|EOF|||  
  
 Quando um cursor se move além do último registro, **EOF** é definido como **True**; caso contrário, seu valor é **False**. Da mesma forma, quando o cursor se move antes do primeiro registro, **BOF** é definido como **True**; caso contrário, seu valor é **False**. Essas propriedades são geralmente usadas para enumerar os registros no conjunto de dados, como ilustrado no seguinte fragmento de código JScript.  
  
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
  
 Se ambos os **BOF** e **EOF** são **True**, o **registros** objeto está vazio. Ambas as propriedades serão **False** para um recém-aberta, não vazio **registros** objeto. Você pode usar o **BOF** e **EOF** propriedades juntos para determinar se um **registros** objeto está vazio ou não, conforme mostrado no seguinte fragmento de código JScript.  
  
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
  
 Esse esquema funciona para todos os tipos de cursor e é independente dos provedores subjacentes. Se você tentar determinar o emptiness de um **registros** objeto verificando se seu **RecordCount** valor da propriedade é zero (0) ou não, você deve tomar precauções para usar um cursor apropriado e o provedor que suporte ao retorno do número de registros no resultado.  
  
 Se você excluir o último registro restante no **registros** do objeto, o cursor será deixado em um estado indeterminado. O **BOF** e **EOF** propriedades podem permanecer **False** até que você tente reposicionar o registro atual, de acordo com o provedor. Para obter mais informações, consulte [excluindo registros usando o método Delete](../../../ado/guide/data/deleting-records-using-the-delete-method.md).
