---
title: SearchDirectionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SearchDirectionEnum
helpviewer_keywords:
- SearchDirectionEnum enumeration [ADO]
ms.assetid: 81272ae3-2165-4f4e-adfe-9ede0368cb17
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a5c1c3869b144bb770ca893595986288b07aa596
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66711448"
---
# <a name="searchdirectionenum"></a>SearchDirectionEnum
Especifica a direção de uma pesquisa de registro dentro de uma [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adSearchBackward**|-1|Parando no início de pesquisas com versões anteriores, o **conjunto de registros**. Se uma correspondência não for encontrada, o ponteiro de registro está posicionado em [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md).|  
|**adSearchForward**|1|Encaminham pesquisas, parando no final de **conjunto de registros**. Se uma correspondência não for encontrada, o ponteiro de registro está posicionado em [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md).|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Package: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.SearchDirection.BACKWARD|  
|AdoEnums.SearchDirection.FORWARD|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Método Find (ADO)](../../../ado/reference/ado-api/find-method-ado.md)
