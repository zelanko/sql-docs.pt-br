---
title: Adicionando registros | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- AddNew method [ADO]
- ADO, editing data
- editing data [ADO], AddNew method
- editing data [ADO], adding data
ms.assetid: dd34669e-6f06-403b-9241-1c85c82aecc2
author: rothja
ms.author: jroth
ms.openlocfilehash: c3dbcdf4ab089968741a4d0b08b7b02d1324f26d
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761392"
---
# <a name="adding-records-to-a-recordset"></a>Adicionando registros a um conjunto de registros
Use o método **AddNew** para criar e inicializar um novo registro em um **conjunto de registros**existente. Você pode usar o método com **suporte** com um valor **CursorOptionEnum** de **adAddNew** para verificar se você pode adicionar registros ao objeto **Recordset** atual.

 Depois que você chamar o método **AddNew** , o novo registro se tornará o registro atual e permanecerá atualizado depois que você chamar o método **Update** . Se o objeto **Recordset** não oferecer suporte a indicadores, talvez você não consiga acessar o novo registro depois de mover para outro registro. Portanto, dependendo do tipo de cursor, talvez seja necessário chamar o método **Requery** para tornar o novo registro acessível.

 Se você chamar **AddNew** ao editar o registro atual ou ao adicionar um novo registro, o ADO chamará o método **Update** para salvar as alterações e, em seguida, criará o novo registro.

 Esta seção contém os seguintes tópicos.

-   [Adicionando registros usando AddNew](../../../ado/guide/data/adding-records-using-addnew.md)

-   [Adicionar vários campos](../../../ado/guide/data/adding-multiple-fields.md)

-   [Determinar o modo de edição](../../../ado/guide/data/determining-edit-mode.md)

-   [Usar AddNew em modos de lote e imediatos](../../../ado/guide/data/using-addnew-in-immediate-and-batch-modes.md)
