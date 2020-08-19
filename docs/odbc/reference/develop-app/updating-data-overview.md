---
description: Atualizar a visão geral de dados
title: Visão geral de atualização de dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], about updating data
- data updates [ODBC]
- updating data [ODBC]
- data updates [ODBC], about data updates
ms.assetid: 062036a4-cda6-4aaa-9765-f1ec3e0b31b1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2b1755ea75426030a96ed7b349cc82f0fc7e282a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424418"
---
# <a name="updating-data-overview"></a>Atualizar a visão geral de dados
Os aplicativos podem atualizar os dados executando instruções SQL ou chamando **SQLSetPos** ou **SQLBulkOperations**. As instruções **Update**, **delete**e **Insert** agem diretamente na fonte de dados e geralmente são suportadas pelos drivers. As instruções UPDATE e Delete pesquisadas contêm uma especificação das linhas a serem alteradas. As instruções UPDATE e DELETE posicionadas e **SQLSetPos** atuam na fonte de dados por meio de um cursor e têm menos suporte.  
  
 Se os cursores podem detectar alterações feitas no conjunto de resultados com os métodos descritos nesta seção dependem do tipo de cursor e de como ele é implementado. Os cursores de somente avanço não revisitam linhas e, portanto, não detectarão nenhuma alteração. Para obter informações sobre se os cursores roláveis podem detectar alterações, consulte [cursores roláveis](../../../odbc/reference/develop-app/scrollable-cursors.md).  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Instruções UPDATE, DELETE e INSERT](../../../odbc/reference/develop-app/update-delete-and-insert-statements.md)  
  
-   [Instruções de atualização e exclusão posicionadas](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)  
  
-   [Simular instruções de exclusão e atualização posicionadas](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)  
  
-   [Determinar o número de linhas afetadas](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)  
  
-   [Atualizar dados com SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)  
  
-   [Atualizar dados com SQLBulkOperations](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)  
  
-   [Dados Long e SQLSetPos e SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)
