---
description: CursorLocationEnum
title: CursorLocationEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 206d9da9130c0dce78e0f8748bf3ace8634dab44
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974417"
---
# <a name="cursorlocationenum"></a>CursorLocationEnum
Especifica o local do serviço de cursor.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adUseClient**|3|Usa cursores do lado do cliente fornecidos por uma biblioteca de cursores local. Os serviços de cursor local geralmente permitirão muitos recursos que os cursores fornecidos por driver podem não, portanto, usar essa configuração pode fornecer uma vantagem em relação aos recursos que serão habilitados. Para compatibilidade com versões anteriores, também há suporte para o sinônimo **adUseClientBatch** .|  
|**adUseNone**|1|Não usa serviços de cursor. (Essa constante é obsoleta e aparece apenas para fins de compatibilidade com versões anteriores.)|  
|**adUseServer**|2|Padrão. Usa cursores fornecidos pelo driver ou provedor de dados. Às vezes, esses cursores são muito flexíveis e permitem sensibilidade adicional às alterações que outras pessoas fazem na fonte de dados. No entanto, alguns recursos do [serviço de cursor da Microsoft para OLE DB](../../guide/data/the-microsoft-cursor-service-for-ole-db.md), como desassociados<br /><br /> Os objetos [Recordset](./recordset-object-ado.md) , não podem ser simulados com cursores do lado do servidor e esses recursos ficarão indisponíveis com essa configuração.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. CursorLocation. CLIENT|  
|AdoEnums. CursorLocation. NONE|  
|AdoEnums. CursorLocation. SERVER|  
  
## <a name="applies-to"></a>Aplica-se A  
 [Propriedade CursorLocation (ADO)](./cursorlocation-property-ado.md)