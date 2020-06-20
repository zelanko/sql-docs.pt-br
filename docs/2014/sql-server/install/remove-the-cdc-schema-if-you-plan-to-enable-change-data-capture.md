---
title: Remova o esquema CDC se você planeja habilitar a captura de dados de alterações | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- cdc schema
- change data capture
ms.assetid: 6a84aa25-0f31-4be3-b2dd-4f249b8254ae
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: abdb33fa3d1ff022a65ed569f19d48bcf4468501
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059151"
---
# <a name="remove-the-cdc-schema-if-you-plan-to-enable-change-data-capture"></a>Remover o esquema cdc se você planeja habilitar o Change Data Capture
  Um banco de dados já contém um esquema cdc. Se você estiver planejando habilitar o Change Data Capture após a atualização, primeiro descarte esse esquema cdc. Quando você habilitar um banco de dados para o Change Data Capture, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] criará um novo esquema denominado cdc.  
  
  
