---
description: Atualizando dados
title: Atualizando dados | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ADO], about data updates
- updating data [ADO], about updating data
ms.assetid: 6508e4e9-e33a-4dad-b340-5d632fd78a91
author: rothja
ms.author: jroth
ms.openlocfilehash: 5ea884479e7353b822e8b679a0fff34d70c3fd93
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452638"
---
# <a name="updating-data"></a>Atualizando dados
O comportamento de atualização e a funcionalidade são amplamente dependentes do modo de atualização (tipo de bloqueio), tipo de cursor e local do cursor.  
  
 Use o método **Update** para salvar as alterações feitas no registro atual de um objeto **Recordset** desde chamar o método **AddNew** ou desde a alteração de qualquer valor de campo em um registro existente. O objeto **Recordset** deve dar suporte a atualizações.  
  
 Se o objeto **Recordset** oferecer suporte à atualização em lotes, você poderá armazenar em cache várias alterações em um ou mais registros localmente até chamar o método **UpdateBatch** . Se você estiver editando o registro atual ou adicionando um novo registro ao chamar o método **UpdateBatch** , o ADO chamará automaticamente o método **Update** para salvar as alterações pendentes no registro atual antes de transmitir as alterações em lote para o provedor.  
  
 O registro atual permanece atual depois que você chama os métodos **Update** ou **UpdateBatch** .  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Modo imediato](../../../ado/guide/data/immediate-mode.md)  
  
-   [Modo de lote](../../../ado/guide/data/batch-mode.md)  
  
-   [Processamento de transações](../../../ado/guide/data/transaction-processing.md)
