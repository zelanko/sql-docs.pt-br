---
description: MSSQLSERVER_2516
title: MSSQLSERVER_2516 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2516 (Database Engine error)
ms.assetid: 79ed14b5-f53c-40c6-8334-8a083f732207
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b62b3d0fcf702b25882c0dee3d312d5339e879f6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428778"
---
# <a name="mssqlserver_2516"></a>MSSQLSERVER_2516
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|2516|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC_REPAIR_DIFF_MAP_INVALIDATED|  
|Texto da mensagem|A correção invalidou o bitmap diferencial do banco de dados NAME. A cadeia de backup diferencial foi quebrada. Execute um backup total de banco de dados antes de executar um backup diferencial.|  
  
## <a name="explanation"></a>Explicação  
Essa mensagem informativa é retornada quando o erro MSSQLEngine_2515 é corrigido.  
  
## <a name="user-action"></a>Ação do usuário  
Execute um backup total do banco de dados.  
  
## <a name="see-also"></a>Consulte Também  
[Criar um backup completo de banco de dados &#40;SQL Server&#41;](~/relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
