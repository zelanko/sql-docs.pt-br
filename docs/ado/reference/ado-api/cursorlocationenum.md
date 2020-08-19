---
description: CursorLocationEnum
title: CursorLocationEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CursorLocationEnum
helpviewer_keywords:
- CursorLocationEnum enumeration [ADO]
ms.assetid: acb255ff-1734-4b70-89bb-aef862b4c63b
author: rothja
ms.author: jroth
ms.openlocfilehash: 67cd645a7eca33d949055a1de6fd264bc7a4b942
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444288"
---
# <a name="cursorlocationenum"></a>CursorLocationEnum
Especifica o local do serviço de cursor.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adUseClient**|3|Usa cursores do lado do cliente fornecidos por uma biblioteca de cursores local. Os serviços de cursor local geralmente permitirão muitos recursos que os cursores fornecidos por driver podem não, portanto, usar essa configuração pode fornecer uma vantagem em relação aos recursos que serão habilitados. Para compatibilidade com versões anteriores, também há suporte para o sinônimo **adUseClientBatch** .|  
|**adUseNone**|1|Não usa serviços de cursor. (Essa constante é obsoleta e aparece apenas para fins de compatibilidade com versões anteriores.)|  
|**adUseServer**|2|Padrão. Usa cursores fornecidos pelo driver ou provedor de dados. Às vezes, esses cursores são muito flexíveis e permitem sensibilidade adicional às alterações que outras pessoas fazem na fonte de dados. No entanto, alguns recursos do [serviço de cursor da Microsoft para OLE DB](../../../ado/guide/data/the-microsoft-cursor-service-for-ole-db.md), como desassociados<br /><br /> Os objetos [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) , não podem ser simulados com cursores do lado do servidor e esses recursos ficarão indisponíveis com essa configuração.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. CursorLocation. CLIENT|  
|AdoEnums. CursorLocation. NONE|  
|AdoEnums. CursorLocation. SERVER|  
  
## <a name="applies-to"></a>Aplica-se A  
 [Propriedade CursorLocation (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md)
