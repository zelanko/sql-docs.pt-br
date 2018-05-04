---
title: Determinar o modo de edição | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], edit mode
- ADO, editing data
ms.assetid: 4c7e010d-08cd-4e22-9b32-23c36f02f88c
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4532f65823d4aed88c4db05e03571497f8eac6b5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="determining-edit-mode"></a>Determinar o modo de edição
ADO mantém um buffer de edição associado ao registro atual. O **EditMode** propriedade indica se foram feitas alterações a esse buffer ou se um novo registro foi criado. Use **EditMode** para determinar o status de edição do registro atual. Você pode testar alterações pendentes se um processo de edição foi interrompido e determinar se é necessário usar o **atualização** ou **CancelUpdate** método.  
  
 **EditMode** retorna um do **EditModeEnum** constantes, que são listadas na tabela a seguir.  
  
|Constante|Description|  
|--------------|-----------------|  
|**adEditNone**|Indica que nenhuma operação de edição está em andamento.|  
|**adEditInProgress**|Indica que os dados no registro atual foram modificados, mas não foi salvos.|  
|**adEditAdd**|Indica que o **AddNew** método foi chamado e o registro atual no buffer de cópia é um novo registro que não foram salvas no banco de dados.|  
|**adEditDelete**|Indica que o registro atual foi excluído.|  
  
 **EditMode** pode retornar um valor válido somente se houver um registro atual. **EditMode** retornará um erro se **BOF** ou **EOF** é **True** ou se o registro atual foi excluído.
