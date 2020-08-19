---
description: EditModeEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 64310c3399d24d557fc0896587dad0dc4fde091b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444038"
---
# <a name="editmodeenum"></a>EditModeEnum
Especifica o status de edição de um registro.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adEditNone**|0|Indica que nenhuma operação de edição está em andamento.|  
|**adEditInProgress**|1|Indica que os dados no registro atual foram modificados, mas não salvos.|  
|**adEditAdd**|2|Indica que o método [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) foi chamado e o registro atual no buffer de cópia é um novo registro que não foi salvo no banco de dados.|  
|**adEditDelete**|4|Indica que o registro atual foi excluído.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums.EditMode.NONE|  
|AdoEnums.EditMode.INPROGRESS|  
|AdoEnums.EditMode.ADD|  
|AdoEnums.EditMode.DELETE|  
  
## <a name="applies-to"></a>Aplica-se A  
 [Propriedade EditMode](../../../ado/reference/ado-api/editmode-property.md)
