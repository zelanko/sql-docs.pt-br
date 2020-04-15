---
title: ConexãoValidSharedMemory dbmslpcn.dll
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
ms.openlocfilehash: 1f3bb097965563afb458b4529676d1e9967e4899
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303872"
---
# <a name="connectionvalidsharedmemory-function-in-dbmslpcndll-shared-memory"></a>Função ConnectionValidSharedMemory na memória compartilhada dbmslpcn.dll
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  A função determina se a memória compartilhada do servidor SQL está instalada e ativa.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
BOOL ConnectionValidSharedMemory(char * szServerName);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *szServerName*  
  
-   Tipo: **\* char**  
  
-   O nome do servidor SQL.  
  
## <a name="return-value"></a>Valor retornado  
 Tipo: **BOOL**  
  
 Retorna 0 se não for válido; outra coisa retorna não zero.  
  
  
