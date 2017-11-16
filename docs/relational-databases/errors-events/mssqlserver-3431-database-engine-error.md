---
title: MSSQLSERVER_3431 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 3431 (Database Engine error)
ms.assetid: 9541217f-e5c6-4a12-a19a-006058f1d3f3
caps.latest.revision: "18"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: fbad9e04b6f558f4c2c992051436c3cae56eb4e6
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver3431"></a>MSSQLSERVER_3431
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|3431|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|UNRESOLVED_XACT|  
|Texto da mensagem|Não foi possível recuperar o banco de dados '%.*ls' (ID do banco de dados %d) devido a resultados de transação não resolvidos. As transações do MS DTC (Coordenador de Transações Distribuídas da Microsoft) foram preparadas, mas o MS DTC não pôde determinar a resolução. Para resolver, corrija o MS DTC, repare o banco de dados ou restaure-o usando um backup completo.|  
  
## <a name="explanation"></a>Explicação  
Uma ou mais transações distribuídas que estavam usando o MS DTC (Coordenador de Transações Distribuídas da [!INCLUDE[msCoName](../../includes/msconame-md.md)]) estavam incompletas quando o banco de dados foi desligado. A recuperação desse banco de dados falhou porque o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode concluir nem reverter as transações sem mais informações do MS DTC.  
  
## <a name="user-action"></a>Ação do usuário  
Para recuperar esse banco de dados, você precisa primeiro resolver o problema no MS DTC. Para investigar o problema com o MS DTC, examine os logs de eventos do Windows. Se você não conseguir resolver o problema com o MS DTC para recuperar o banco de dados, restaure um backup do banco de dados.  
  
