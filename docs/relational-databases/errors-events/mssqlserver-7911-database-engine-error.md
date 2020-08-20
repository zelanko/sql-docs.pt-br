---
description: MSSQLSERVER_7911
title: MSSQLSERVER_7911 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 7911 (Database Engine error)
ms.assetid: dd8390f3-0f77-4fb2-ba94-631a56e42bc6
author: MashaMSFT
ms.author: mathoma
robots: noindex,nofollow
ms.openlocfilehash: 57258696ea1d8051817a1e0f99aa089c4c60ad83
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88470815"
---
# <a name="mssqlserver_7911"></a>MSSQLSERVER_7911
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|7911|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC2_REPAIR_PAGE_DEALLOCATED|  
|Texto da mensagem|Reparar: A página P_ID foi desalocada da ID de objeto O_ID, ID de índice I_ID, ID de partição PN_ID, ID de unidade de alocação A_ID (tipo TYPE).|  
  
## <a name="explanation"></a>Explicação  
Essa é uma mensagem informativa da cláusula REPAIR que afirma que uma página foi desalocada da matriz de slot com uma única página de uma página IAM.  
  
## <a name="user-action"></a>Ação do usuário  
Nenhum  
  
