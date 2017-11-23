---
title: RecordOpenOptionsEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: RecordOpenOptionsEnum
helpviewer_keywords: RecordOpenOptionsEnum enumeration [ADO]
ms.assetid: 9028aba4-90fc-4dfc-88e4-fa8a7b6fedee
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4b94b5bf6c47fa824e7ff5f542d749b509376376
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="recordopenoptionsenum"></a>RecordOpenOptionsEnum
Especifica opções para abrir um [registro](../../../ado/reference/ado-api/record-object-ado.md). Esses valores podem ser combinados usando ou.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adDelayFetchFields**|0x8000|Indica ao provedor que os campos associados a **registro** não precisam ser recuperados inicialmente, mas pode ser recuperado na primeira tentativa de acessar o campo. É o comportamento padrão, indicado pela ausência desse sinalizador recuperar todos os **registro** campos do objeto.|  
|**adDelayFetchStream**|0x4000|Indica ao provedor que o fluxo padrão associado a **registro** não precisam ser recuperados inicialmente. É o comportamento padrão, indicado pela ausência desse sinalizador recuperar o fluxo padrão associado a **registro** objeto.|  
|**adOpenAsync**|0x1000|Indica que o **registro** objeto é aberto no modo assíncrono.|  
|**adOpenExecuteCommand**|0x10000|Indica que a cadeia de caracteres de origem contém o texto do comando que deve ser executado. Esse valor é equivalente a **adCmdText** opção **Recordset.Open**.|  
|**adOpenRecordUnspecified**|-1|Padrão. Indica que nenhuma opção for especificada.|  
|**adOpenOutput**|0x800000|Indica que se os pontos de origem para um nó que contém um script executável (como um. Página ASP), em seguida, aberto **registro** conterá os resultados do script executado. Esse valor só é válido com coleção não registros.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Constantes não têm equivalentes do ADO/WFC.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Método Open (Registro do ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)
