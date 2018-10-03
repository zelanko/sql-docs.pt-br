---
title: MSSQLSERVER_2539 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2539 (Database Engine error)
ms.assetid: e638efcc-56f4-40f9-9740-17ef67b47d79
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 17ddd73792d4ce530b5fb87249033f059d4cddd9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47746864"
---
# <a name="mssqlserver2539"></a>MSSQLSERVER_2539
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|2539|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC_ALLOCATION_SUMMARY_FOR_DATABASE|  
|Texto da mensagem|O número total de extensões = EXTENTS, páginas usadas = USED_PAGES, páginas reservadas = RESERVED_PAGES neste banco de dados.|  
  
## <a name="explanation"></a>Explicação  
Essas informações fazem parte da saída do comando DBCC CHECKALLOC. Elas são um resumo de extensões alocadas, páginas usadas e páginas reservadas para o banco de dados especificado.  
  
## <a name="user-action"></a>Ação do usuário  
None  
  
