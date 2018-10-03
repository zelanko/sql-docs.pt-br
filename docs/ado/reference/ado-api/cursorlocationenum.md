---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 832372ee3f8e80a9da4a758c759d9b5399a20a57
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47614730"
---
# <a name="cursorlocationenum"></a>CursorLocationEnum
Especifica o local do serviço de cursor.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adUseClient**|3|Usa cursores do lado do cliente fornecidos por uma biblioteca de cursor local. Serviços de cursor local geralmente permitirá que muitos recursos fornecidos pelo driver de cursores não podem, para que usar essa configuração pode fornecer uma vantagem em relação aos recursos que serão habilitados. Para compatibilidade com versões anteriores, o sinônimo **adUseClientBatch** também tem suporte.|  
|**adUseNone**|1|Não usa os serviços de cursor. (Essa constante é obsoleta e será exibida apenas para fins de compatibilidade com versões anteriores.)|  
|**adUseServer**|2|Padrão. Usa cursores fornecidos pelo provedor de dados ou driver. Esses cursores, às vezes, são muito flexíveis e permitem a sensibilidade adicional para as alterações feitas por outras pessoas para a fonte de dados. No entanto, alguns recursos do [o Microsoft Cursor Service para OLE DB](../../../ado/guide/data/the-microsoft-cursor-service-for-ole-db.md), tais como desassociado<br /><br /> [Conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) objetos, não podem ser simulados com cursores do lado do servidor e esses recursos não estarão disponíveis com essa configuração.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.CursorLocation.CLIENT|  
|AdoEnums.CursorLocation.NONE|  
|AdoEnums.CursorLocation.SERVER|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Propriedade CursorLocation (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md)
