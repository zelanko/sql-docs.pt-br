---
title: MSSQLSERVER_11409 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 11409 (Database Engine error)
ms.assetid: 99b71a1c-a72d-4ca9-9d00-4230c9042ba5
caps.latest.revision: "9"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: ca191c492eeb5c1d5c717f9a5721c9dcc2a8d0d9
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver11409"></a>MSSQLSERVER_11409
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|11409|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|ALTERCOL_COLSET_DROP|  
|Texto da mensagem|Não é possível remover o conjunto de colunas '%.*ls' na tabela '%.\*ls' porque ela contém mais de 1.025 colunas.|  
  
## <a name="explanation"></a>Explicação  
As tabelas podem conter no máximo 1024 colunas que não estejam designadas como esparsas ou computadas. Quando colunas esparsas fazem com que a tabela exceda as 1024 colunas, é necessário definir um conjunto de colunas para ela. A tabela referenciada tem mais de 1024 colunas, e você tentou remover o conjunto de colunas.  
  
## <a name="user-action"></a>Ação do usuário  
Com as colunas atuais da tabela, você deve reter o conjunto de colunas.  
  
Para remover o conjunto de colunas, remova primeiro as colunas da tabela até que o número de colunas não ultrapasse 1024. Em seguida, você poderá remover o conjunto de colunas.  
  
