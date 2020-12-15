---
description: Função ConnectionValidSharedMemory na memória compartilhada dbmslpcn.dll
title: dbmslpcn.dll ConnectionValidSharedMemory
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 6ae35826-7d75-4542-b686-5f79316b6157
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a487eb380ea4e7b0fe246efdb9281cbab63a1303
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97475987"
---
# <a name="connectionvalidsharedmemory-function-in-dbmslpcndll-shared-memory"></a>Função ConnectionValidSharedMemory na memória compartilhada dbmslpcn.dll
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  A função determina se SQL Server memória compartilhada está instalada e ativa.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
BOOL ConnectionValidSharedMemory(char * szServerName);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *szServerName*  
  
-   Tipo: **Char \** _  
  
-   O nome do SQL Server.  
  
## <a name="return-value"></a>Valor retornado  
 Tipo: _ *bool**  
  
 Retornará 0 se não for válido; caso contrário, retorna zero.  
  
  
