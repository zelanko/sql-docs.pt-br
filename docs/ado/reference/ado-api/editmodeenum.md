---
title: EditModeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EditModeEnum
helpviewer_keywords:
- EditModeEnum enumeration [ADO]
ms.assetid: 45d54b6e-db2c-4553-9fd0-528147d6da2f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 34583128e3da1bec00003fe194d3387783815275
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47788774"
---
# <a name="editmodeenum"></a>EditModeEnum
Especifica o status de edição de um registro.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adEditNone**|0|Indica que nenhuma operação de edição está em andamento.|  
|**adEditInProgress**|1|Indica que os dados no registro atual foram modificados mas não salvos.|  
|**adEditAdd**|2|Indica que o [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) método foi chamado e o registro atual no buffer de cópia é um novo registro não foi salvo no banco de dados.|  
|**adEditDelete**|4|Indica que o registro atual foi excluído.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.EditMode.NONE|  
|AdoEnums.EditMode.INPROGRESS|  
|AdoEnums.EditMode.ADD|  
|AdoEnums.EditMode.DELETE|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Propriedade EditMode](../../../ado/reference/ado-api/editmode-property.md)
