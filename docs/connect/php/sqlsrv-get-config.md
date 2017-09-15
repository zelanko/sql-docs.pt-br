---
title: sqlsrv_get_config | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- sqlsrv_get_config
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_get_config
- sqlsrv_get_config
ms.assetid: ce2befc2-af98-45bb-8d41-60f1674dccfc
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a5712c6f98da82b422e76a7cb6c8d07adac86b5e
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

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
  
## <a name="remarks"></a>Comentários  
Se **false** for retornado por **sqlsrv_get_config**, você deverá chamar [sqlsrv_errors](../../connect/php/sqlsrv-errors.md) para determinar se ocorreu um erro ou se **false** é o valor da configuração especificada pelo parâmetro *$setting* .  
  
## <a name="see-also"></a>Consulte também  
[Referência da API do driver JDBC](../../connect/php/sqlsrv-driver-api-reference.md)  
[sqlsrv_configure](../../connect/php/sqlsrv-configure.md)  
[sqlsrv_errors](../../connect/php/sqlsrv-errors.md)  
  

