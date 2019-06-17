---
title: MSSQLSERVER_12329 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 12329 (Database Engine error)
ms.assetid: 43f90287-36d5-46c2-ac91-a37202dcf6d3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1ab8f54e274f92e3ff9a320c57bd91b527d474ed
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62915877"
---
# <a name="mssqlserver12329"></a>MSSQLSERVER_12329
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|12329|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|HK_UNSUPPORTED_NON_LATIN_CODEPAGE|  
|Texto da mensagem|Não há suporte para os tipos de dados char(n) e varchar(n) que usam uma ordenação com uma página de código diferente de 1252 com *construct*.|  
  
## <a name="explanation"></a>Explicação  
 Não use os tipos de dados char(n) e varchar(n) que empreguem uma ordenação com uma página de código diferente de 1252.  
  
## <a name="user-action"></a>Ação do usuário  
 Uma situação inesperada que pode gerar esse erro é:  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = 'us_english')  
```  
  
 Use isto:  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
```  
  
  
