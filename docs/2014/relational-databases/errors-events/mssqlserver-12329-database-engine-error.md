---
title: MSSQLSERVER_12329 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 12329 (Database Engine error)
ms.assetid: 43f90287-36d5-46c2-ac91-a37202dcf6d3
caps.latest.revision: 5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8fd526df2e17aea8935918b388d0965d49173cc3
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37407914"
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
|Texto da mensagem|Não há suporte para os tipos de dados char(n) e varchar(n) que usam um agrupamento com uma página de código diferente de 1252 com *construct*.|  
  
## <a name="explanation"></a>Explicação  
 Não use os tipos de dados char(n) e varchar(n) que empreguem um agrupamento com uma página de código diferente de 1252.  
  
## <a name="user-action"></a>Ação do usuário  
 Uma situação inesperada que pode gerar esse erro é:  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = 'us_english')  
```  
  
 Use isto:  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
```  
  
  
