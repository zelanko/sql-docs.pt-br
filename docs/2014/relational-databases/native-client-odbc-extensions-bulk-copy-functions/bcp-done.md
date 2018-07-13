---
title: bcp_done | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- bcp_done
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_done function
ms.assetid: e59b3f16-5b59-40da-880f-f3edf657d1ee
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 630762fc74a9c1c71d24d40a1ba22bf6627a0d0c
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37414715"
---
# <a name="bcpdone"></a>bcp_done
  Termina uma cópia em massa de variáveis de programa para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executada com [bcp_sendrow](bcp-sendrow.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DBINT bcp_done (  
    HDBC   
hdbc  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *HDBC*  
 É o identificador de conexão ODBC habilitado para cópia em massa.  
  
## <a name="returns"></a>Retorna  
 O número de linhas permanentemente salvas depois da última chamada para [bcp_batch](bcp-batch.md) , ou -1 em caso de erro.  
  
## <a name="remarks"></a>Remarks  
 Chame **bcp_done** depois da última chamada para [bcp_sendrow](bcp-sendrow.md) ou [bcp_moretext](bcp-moretext.md). Falha ao chamar **bcp_done** depois de copiar todos os resultados de dados dos erros.  
  
## <a name="see-also"></a>Consulte também  
 [Funções de cópia em massa](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
