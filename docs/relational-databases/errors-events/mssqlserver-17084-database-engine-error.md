---
description: MSSQLSERVER_17084
title: MSSQLSERVER_17084 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17084 (Database Engine error)
ms.assetid: e579d104-3307-4edd-8587-b14ecbc02ed9
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: bf44aa95cca35e56f836306f7870bd2c2de9be7a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471106"
---
# <a name="mssqlserver_17084"></a>MSSQLSERVER_17084
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|17084|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|P3_ATOMIC_WITH_MISSING_OPTION|  
|Texto da mensagem|A cláusula WITH da instrução BEGIN ATOMIC deve especificar um valor para a opção '%ls'.|  
  
## <a name="explanation"></a>Explicação  
A cláusula WITH da instrução BEGIN ATOMIC não especificou um valor para uma opção.  
  
## <a name="user-action"></a>Ação do usuário  
Blocos **ATOMIC** exigem valores para as opções **WITH** **TRANSACTION ISOLATION LEVEL** e **LANGUAGE**. Por exemplo:  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE= N'us_english')  
```  
  
Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Consulte Também  
[OLTP in-memory &#40;Otimização na memória&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
