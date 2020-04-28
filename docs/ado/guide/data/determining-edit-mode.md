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
ms.openlocfilehash: 22e63bad49586bbbc1a5616114055779cd3ea041
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925543"
---
# <a name="determining-edit-mode"></a>Determinar o modo de edição
O ADO mantém um buffer de edição associado ao registro atual. A propriedade **EditMode** indica se foram feitas alterações nesse buffer ou se um novo registro foi criado. Use **EditMode** para determinar o status de edição do registro atual. Você pode testar as alterações pendentes se um processo de edição tiver sido interrompido e determinar se você precisa usar o método **Update** ou **CancelUpdate** .  
  
 **EditMode** retorna uma das constantes **EditModeEnum** , que são listadas na tabela a seguir.  
  
|Constante|Descrição|  
|--------------|-----------------|  
|**adEditNone**|Indica que nenhuma operação de edição está em andamento.|  
|**adEditInProgress**|Indica que os dados no registro atual foram modificados, mas não salvos.|  
|**adEditAdd**|Indica que o método **AddNew** foi chamado e o registro atual no buffer de cópia é um novo registro que não foi salvo no banco de dados.|  
|**adEditDelete**|Indica que o registro atual foi excluído.|  
  
 **EditMode** só poderá retornar um valor válido se houver um registro atual. O **EditMode** retornará um erro se **BOF** ou **EOF** for **true** ou se o registro atual tiver sido excluído.
