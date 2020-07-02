---
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 43a4bdb3b5e20246fc464d347710fb57f0584f0c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85657493"
---
# <a name="connectionvalidsharedmemory-function-in-dbmslpcndll-shared-memory"></a>Função ConnectionValidSharedMemory na memória compartilhada dbmslpcn.dll
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  A função determina se SQL Server memória compartilhada está instalada e ativa.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
BOOL ConnectionValidSharedMemory(char * szServerName);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *szServerName*  
  
-   Tipo: **Char \* **  
  
-   O nome do SQL Server.  
  
## <a name="return-value"></a>Retornar valor  
 Tipo: **bool**  
  
 Retornará 0 se não for válido; caso contrário, retorna zero.  
  
  
