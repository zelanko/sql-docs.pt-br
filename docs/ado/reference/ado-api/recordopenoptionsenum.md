---
title: RecordOpenOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordOpenOptionsEnum
helpviewer_keywords:
- RecordOpenOptionsEnum enumeration [ADO]
ms.assetid: 9028aba4-90fc-4dfc-88e4-fa8a7b6fedee
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ba165d51dde5224dac65467061eac0d38aeefc7c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931421"
---
# <a name="recordopenoptionsenum"></a>RecordOpenOptionsEnum
Especifica opções para abrir um [registro](../../../ado/reference/ado-api/record-object-ado.md). Esses valores podem ser combinados usando ou.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adDelayFetchFields**|0x8000|Indica ao provedor que os campos associados com o **registro** não precisam ser recuperados inicialmente, mas pode ser recuperado na primeira tentativa de acessar o campo. O comportamento padrão, indicado pela ausência desse sinalizador é recuperar todos os **registro** campos do objeto.|  
|**adDelayFetchStream**|0x4000|Indica ao provedor que o fluxo padrão associado a **registro** não precisam ser recuperados inicialmente. O comportamento padrão, indicado pela ausência desse sinalizador é recuperar o fluxo padrão associado a **registro** objeto.|  
|**adOpenAsync**|0x1000|Indica que o **registro** objeto é aberto no modo assíncrono.|  
|**adOpenExecuteCommand**|0x10000|Indica que a cadeia de caracteres de origem contém o texto do comando que deve ser executado. Esse valor é equivalente a **adCmdText** opção **Recordset.Open**.|  
|**adOpenRecordUnspecified**|-1|Padrão. Indica que nenhuma opção foi especificada.|  
|**adOpenOutput**|0x800000|Indica que se a origem aponta para um nó que contém um script executável (como um. Página ASP), em seguida, aberta **registro** conterá os resultados do script executado. Esse valor só é válido com registros não seja de coleção.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Essas constantes não têm equivalentes do ADO/WFC.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Método Open (Registro do ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)
