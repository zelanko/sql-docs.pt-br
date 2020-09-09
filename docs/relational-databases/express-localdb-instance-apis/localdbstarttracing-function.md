---
description: Função LocalDBStartTracing
title: Função LocalDBStartTracing | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apiname:
- LocalDBStartTracing
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: c7b83833-6d2a-4a06-9cb7-42767bed52c6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 854a840375601a6d571afa21b734cec6fb23b2b5
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542931"
---
# <a name="localdbstarttracing-function"></a>Função LocalDBStartTracing
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Habilita o rastreamento de chamadas de API para todas as instâncias de LocalDB do SQL Server Express de propriedade do usuário atual do Windows.  
  
 **Arquivo de cabeçalho:** sqlncli.h  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT LocalDBStartTracing();  
```  
  
## <a name="returns"></a>Retornos  
 S_OK  
 A função foi bem-sucedida.  
  
 [LOCALDB_ERROR_XEVENT_FAILED](../../relational-databases/express-localdb-error-messages/localdb-error-xevent-failed.md)  
 Falha ao iniciar o mecanismo XEvent na API da Instância de LocalDB.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 Erro inesperado. Consulte o log de eventos para obter detalhes.  
  
## <a name="remarks"></a>Comentários  
 Para obter uma amostra do código que usa a API LocalDB, consulte [SQL Server Express LocalDB Reference](../../relational-databases/sql-server-express-localdb-reference.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Cabeçalho e informações de versão de LocalDB do SQL Server Express](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
