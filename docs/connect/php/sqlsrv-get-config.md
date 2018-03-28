---
title: sqlsrv_get_config | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- sqlsrv_get_config
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_get_config
- sqlsrv_get_config
ms.assetid: ce2befc2-af98-45bb-8d41-60f1674dccfc
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 841cc20172a024ee6f86cfb8151c4f01e70e326e
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="sqlsrvgetconfig"></a>sqlsrv_get_config
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Retorna o valor atual da definição de configuração especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sqlsrv_get_config( string $setting )  
```  
  
#### <a name="parameters"></a>Parâmetros  
*$setting*: a definição de configuração para a qual o valor é retornado. Para obter uma lista das definições configuráveis, consulte [sqlsrv_configure](../../connect/php/sqlsrv-configure.md).  
  
## <a name="return-value"></a>Valor de retorno  
O valor da configuração especificada pelo parâmetro *$setting* . Se uma configuração inválida for especificada, será retornado **false** e um erro será adicionado à coleção de erros.  
  
## <a name="remarks"></a>Remarks  
Se **false** for retornado por **sqlsrv_get_config**, você deverá chamar [sqlsrv_errors](../../connect/php/sqlsrv-errors.md) para determinar se ocorreu um erro ou se **false** é o valor da configuração especificada pelo parâmetro *$setting* .  
  
## <a name="see-also"></a>Consulte também  
[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  

[sqlsrv_configure](../../connect/php/sqlsrv-configure.md)  

[sqlsrv_errors](../../connect/php/sqlsrv-errors.md)  
  
