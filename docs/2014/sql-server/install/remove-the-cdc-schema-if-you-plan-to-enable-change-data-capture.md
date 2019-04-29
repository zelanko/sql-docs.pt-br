---
title: Remover o esquema cdc se você planeja habilitar o change data capture | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- cdc schema
- change data capture
ms.assetid: 6a84aa25-0f31-4be3-b2dd-4f249b8254ae
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a5d162635a9162871e51fe0664198302804aa487
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62855753"
---
# <a name="remove-the-cdc-schema-if-you-plan-to-enable-change-data-capture"></a>Remover o esquema cdc se você planeja habilitar o Change Data Capture
  Um banco de dados já contém um esquema cdc. Se você estiver planejando habilitar o Change Data Capture após a atualização, primeiro descarte esse esquema cdc. Quando você habilitar um banco de dados para o Change Data Capture, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] criará um novo esquema denominado cdc.  
  
  
