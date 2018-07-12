---
title: Função ConnectionValidSharedMemory na memória compartilhada de dbmslpcn | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 6ae35826-7d75-4542-b686-5f79316b6157
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 43131a256781e3f2be9c0884abe87ce3b0a5db80
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37422155"
---
# <a name="connectionvalidsharedmemory-function-in-dbmslpcndll-shared-memory"></a>Função ConnectionValidSharedMemory na dbmslpcn memória compartilhada
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  A função determina se a memória compartilhada do SQL Server está instalado e ativo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
BOOL ConnectionValidSharedMemory(char * szServerName);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *szServerName*  
  
-   Tipo: **char\***  
  
-   O nome do SQL server.  
  
## <a name="return-value"></a>Valor retornado  
 Tipo: **BOOL**  
  
 Retorna 0 se não é válido; Caso contrário, retornará diferentes de zero.  
  
  
