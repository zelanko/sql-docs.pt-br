---
title: sqlsrv_get_config | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_get_config
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_get_config
- sqlsrv_get_config
ms.assetid: ce2befc2-af98-45bb-8d41-60f1674dccfc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ef4f53e4ee4ae1c9022ea8bfab0ba7a66c147c08
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922759"
---
# <a name="sqlsrv_get_config"></a>sqlsrv_get_config
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Retorna o valor atual da definição de configuração especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sqlsrv_get_config( string $setting )  
```  
  
#### <a name="parameters"></a>parâmetros  
*$setting*: a definição de configuração para a qual o valor é retornado. Para obter uma lista das definições configuráveis, consulte [sqlsrv_configure](../../connect/php/sqlsrv-configure.md).  
  
## <a name="return-value"></a>Valor retornado  
O valor da configuração especificada pelo parâmetro *$setting* . Se uma configuração inválida for especificada, será retornado **false** e um erro será adicionado à coleção de erros.  
  
## <a name="remarks"></a>Comentários  
Se **false** for retornado por **sqlsrv_get_config**, você deverá chamar [sqlsrv_errors](../../connect/php/sqlsrv-errors.md) para determinar se ocorreu um erro ou se **false** é o valor da configuração especificada pelo parâmetro *$setting* .  
  
## <a name="see-also"></a>Consulte Também  
[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  

[sqlsrv_configure](../../connect/php/sqlsrv-configure.md)  

[sqlsrv_errors](../../connect/php/sqlsrv-errors.md)  
  
