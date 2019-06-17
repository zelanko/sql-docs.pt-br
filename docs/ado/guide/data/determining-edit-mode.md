---
title: Determinando o modo de edição | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], edit mode
- ADO, editing data
ms.assetid: 4c7e010d-08cd-4e22-9b32-23c36f02f88c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7345f75d43d302c71db91aefa9097a4d34e72d94
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700970"
---
# <a name="determining-edit-mode"></a>Determinar o modo de edição
ADO mantém um buffer de edição associado ao registro atual. O **EditMode** propriedade indica se foram feitas alterações a esse buffer ou se um novo registro tiver sido criado. Use **EditMode** para determinar o status de edição do registro atual. Você pode testar as alterações pendentes se um processo de edição foi interrompido e determinar se é necessário usar o **atualização** ou **CancelUpdate** método.  
  
 **EditMode** retorna um dos **EditModeEnum** constantes, que são listadas na tabela a seguir.  
  
|Constante|Descrição|  
|--------------|-----------------|  
|**adEditNone**|Indica que nenhuma operação de edição está em andamento.|  
|**adEditInProgress**|Indica que os dados no registro atual foram modificados mas não salvos.|  
|**adEditAdd**|Indica que o **AddNew** método foi chamado e o registro atual no buffer de cópia é um novo registro não foi salvo no banco de dados.|  
|**adEditDelete**|Indica que o registro atual foi excluído.|  
  
 **EditMode** pode retornar um valor válido somente se houver um registro atual. **EditMode** retornará um erro se **BOF** ou **EOF** é **True** ou se o registro atual tiver sido excluído.
