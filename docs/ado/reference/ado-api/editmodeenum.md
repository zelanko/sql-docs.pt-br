---
title: EditModeEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- EditModeEnum
helpviewer_keywords:
- EditModeEnum enumeration [ADO]
ms.assetid: 45d54b6e-db2c-4553-9fd0-528147d6da2f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2b59850d8b04854ee74f94664b53dc22242c6913
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="editmodeenum"></a>EditModeEnum
Especifica o status de edição de um registro.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adEditNone**|0|Indica que nenhuma operação de edição está em andamento.|  
|**adEditInProgress**|1|Indica que os dados no registro atual foram modificados, mas não foi salvos.|  
|**adEditAdd**|2|Indica que o [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) método foi chamado e o registro atual no buffer de cópia é um novo registro que não foram salvas no banco de dados.|  
|**adEditDelete**|4|Indica que o registro atual foi excluído.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Pacote: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.EditMode.NONE|  
|AdoEnums.EditMode.INPROGRESS|  
|AdoEnums.EditMode.ADD|  
|AdoEnums.EditMode.DELETE|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Propriedade EditMode](../../../ado/reference/ado-api/editmode-property.md)

