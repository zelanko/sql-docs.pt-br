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
manager: craigg
ms.openlocfilehash: cc580a6032a19eb8248759669278f8730fc617cb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66092945"
---
# <a name="remove-the-cdc-schema-if-you-plan-to-enable-change-data-capture"></a>Remover o esquema cdc se você planeja habilitar o Change Data Capture
  Um banco de dados já contém um esquema cdc. Se você estiver planejando habilitar o Change Data Capture após a atualização, primeiro descarte esse esquema cdc. Quando você habilitar um banco de dados para o Change Data Capture, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] criará um novo esquema denominado cdc.  
  
  
