---
title: MSSQLSERVER_2516 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 2516 (Database Engine error)
ms.assetid: 79ed14b5-f53c-40c6-8334-8a083f732207
caps.latest.revision: 19
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f82719e1227271a993cb55fba53623170baec38c
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37418795"
---
# <a name="mssqlserver2516"></a>MSSQLSERVER_2516
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|2516|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC_REPAIR_DIFF_MAP_INVALIDATED|  
|Texto da mensagem|A correção invalidou o bitmap diferencial do banco de dados NAME. A cadeia de backup diferencial foi quebrada. Execute um backup total de banco de dados antes de executar um backup diferencial.|  
  
## <a name="explanation"></a>Explicação  
 Essa mensagem informativa é retornada quando o erro MSSQLEngine_2515 é corrigido.  
  
## <a name="user-action"></a>Ação do usuário  
 Execute um backup total do banco de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Criar um backup completo de banco de dados &#40;SQL Server&#41;](../backup-restore/create-a-full-database-backup-sql-server.md)  
  
  
