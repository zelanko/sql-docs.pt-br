---
title: Adicionando registros | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- AddNew method [ADO]
- ADO, editing data
- editing data [ADO], AddNew method
- editing data [ADO], adding data
ms.assetid: dd34669e-6f06-403b-9241-1c85c82aecc2
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 055603ed5db63df42fd7301df84eb615ae4c9833
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="adding-records-to-a-recordset"></a>Adicionando registros para um conjunto de registros
Use o **AddNew** método para criar e inicializar um novo registro em existente **registros**. Você pode usar o **dá suporte a** método com um **CursorOptionEnum** valor **adAddNew** para verificar se você pode adicionar registros a atual **doconjuntoderegistros** objeto.

 Depois de chamar o **AddNew** método, o novo registro se tornará o registro atual e permanece atual depois de chamar o **atualização** método. Se o **registros** objeto não oferece suporte a indicadores, você não poderá acessar o novo registro depois que você vai para outro registro. Portanto, dependendo de seu tipo de cursor, você precisará chamar o **Requery** método para disponibilizar o novo registro.

 Se você chamar **AddNew** ao editar o registro atual ou ao adicionar um novo registro, o ADO chama o **atualização** método para salvar quaisquer alterações e, em seguida, cria o novo registro.

 Esta seção contém os tópicos a seguir.

-   [Adicionando registros usando AddNew](../../../ado/guide/data/adding-records-using-addnew.md)

-   [Adicionando vários campos](../../../ado/guide/data/adding-multiple-fields.md)

-   [Determinando o modo de edição](../../../ado/guide/data/determining-edit-mode.md)

-   [Usando AddNew em modos de lote e imediatos](../../../ado/guide/data/using-addnew-in-immediate-and-batch-modes.md)
