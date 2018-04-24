---
title: CursorLocationEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CursorLocationEnum
helpviewer_keywords:
- CursorLocationEnum enumeration [ADO]
ms.assetid: acb255ff-1734-4b70-89bb-aef862b4c63b
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2e5dc3fa4f78881502f846e828484ea03329d91e
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="cursorlocationenum"></a>CursorLocationEnum
Especifica o local do serviço de cursor.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adUseClient**|3|Usa cursores do lado do cliente fornecidos por uma biblioteca de cursor local. Serviços de cursor local geralmente permitirá que muitos recursos fornecidos pelo driver de cursores não podem, para que usar essa configuração pode fornecer uma vantagem em relação a recursos que serão habilitados. Para compatibilidade com versões anteriores, o sinônimo **adUseClientBatch** também tem suporte.|  
|**adUseNone**|1|Não usa os serviços de cursor. (Esta constante está obsoleta e será exibida apenas para manter a compatibilidade com versões anteriores.)|  
|**adUseServer**|2|Padrão. Usa cursores fornecidos pelo provedor de dados ou driver. Esses cursores, às vezes, são muito flexíveis e permitem sensibilidade adicionais para as alterações feitas por outros usuários à fonte de dados. No entanto, alguns recursos do [o serviço de Cursor do Microsoft para OLE DB](../../../ado/guide/data/the-microsoft-cursor-service-for-ole-db.md), como desassociado<br /><br /> [Conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) objetos, não podem ser simulados com cursores do lado do servidor e esses recursos não estarão disponíveis com esta configuração.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Pacote: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.CursorLocation.CLIENT|  
|AdoEnums.CursorLocation.NONE|  
|AdoEnums.CursorLocation.SERVER|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Propriedade CursorLocation (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md)
