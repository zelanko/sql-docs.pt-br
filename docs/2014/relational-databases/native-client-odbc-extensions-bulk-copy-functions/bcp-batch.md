---
title: bcp_batch | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_batch
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_batch function
ms.assetid: 0bda489e-86bc-4a7e-80f6-96047e03f281
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c41e8d90adc8ff6eb2058feebe3f33c10edbfa92
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62631380"
---
# <a name="bcp_batch"></a>bcp_batch
  Confirma todas as linhas copiadas em massa anteriormente de variáveis de programa e enviadas para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por [bcp_sendrow](bcp-sendrow.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DBINT bcp_batch (HDBC  
hdbc  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *hdbc*  
 É o identificador de conexão ODBC habilitado para cópia em massa.  
  
## <a name="returns"></a>Retornos  
 O número de linhas salvas depois da última chamada para **bcp_batch**, ou -1 em caso de erro.  
  
## <a name="remarks"></a>Comentários  
 Lotes de cópias em massa definem transações. Quando um aplicativo usar [bcp_bind](bcp-bind.md) e **bcp_sendrow** para copiar linhas em massa de variáveis de programa para tabelas do SQL Server, as linhas serão confirmadas apenas quando o programa chamar **bcp_batch** ou [bcp_done](bcp-done.md).  
  
 Você poderá chamar **bcp_batch** uma vez a cada *n* linhas ou quando houver uma pausa nos dados de entrada (como em um aplicativo de telemetria). Se um aplicativo não chamar **bcp_batch** , as linhas copiadas em massa serão confirmadas apenas quando **bcp_done** for chamado.  
  
## <a name="see-also"></a>Consulte Também  
 [Bulk Copy Functions](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
