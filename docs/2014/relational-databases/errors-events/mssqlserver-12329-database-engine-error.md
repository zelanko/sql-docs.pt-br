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
ms.openlocfilehash: 9b99e65e90a61ff32b0ed8962b46f2b0fda9c48e
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552321"
---
# <a name="mssqlserver_12329"></a>MSSQLSERVER_12329
    
## <a name="details"></a>Detalhes  
  
|Atributo|Valor|  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|12329|  
|Origem do Evento|MSSQLSERVER|  
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
  
  
