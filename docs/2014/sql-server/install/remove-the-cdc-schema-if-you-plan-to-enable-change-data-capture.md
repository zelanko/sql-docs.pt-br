---
title: Remover o esquema cdc se você planeja habilitar o change data capture | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- cdc schema
- change data capture
ms.assetid: 6a84aa25-0f31-4be3-b2dd-4f249b8254ae
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: cf7a9173e268b35f5a0a567a0812dc0e0b48ae91
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118042"
---
# <a name="remove-the-cdc-schema-if-you-plan-to-enable-change-data-capture"></a>Remover o esquema cdc se você planeja habilitar o Change Data Capture
  Um banco de dados já contém um esquema cdc. Se você estiver planejando habilitar o Change Data Capture após a atualização, primeiro descarte esse esquema cdc. Quando você habilitar um banco de dados para o Change Data Capture, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] criará um novo esquema denominado cdc.  
  
  