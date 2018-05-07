---
title: sqlsrv_configure | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- sqlsrv_configure
apitype: NA
helpviewer_keywords:
- sqlsrv_configure
- API Reference, sqlsrv_configure
ms.assetid: 9393f975-a4ef-4c50-b4dd-14892fc55cc9
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 449c20bcbe3ff21675c51f483519607d5c37b034
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsrvconfigure"></a>sqlsrv_configure
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Altera as configurações de opções de registro em log e de tratamento de erros.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sqlsrv_configure( string $setting, mixed $value )  
```  
  
#### <a name="parameters"></a>Parâmetros  
*$setting*: o nome da configuração a ser alterada. Consulte a tabela abaixo para obter uma lista de configurações.  
  
*$value*: o valor a ser aplicado à configuração especificada no parâmetro *$setting* . Os valores possíveis para esse parâmetro dependem da configuração especificada. A tabela a seguir apresenta as possíveis combinações:  
  
|Configuração|Valores possíveis para o parâmetro $value (inteiro equivalente entre parênteses)|Valor padrão|  
|-----------|------------------------------------------------------------------------------|-----------------|  
|ClientBufferMaxKBSize<sup>1</sup>|Um número não negativo até o limite de memória do PHP.<br /><br />Zero (0) significa que não há limite para o tamanho do buffer.|10240|  
|LogSeverity<sup>2</sup>|SQLSRV_LOG_SEVERITY_ALL (-1)<br /><br />SQLSRV_LOG_SEVERITY_ERROR (1)<br /><br />SQLSRV_LOG_SEVERITY_NOTICE (4)<br /><br />SQLSRV_LOG_SEVERITY_WARNING (2)|SQLSRV_LOG_SEVERITY_ERROR (1)|  
|LogSubsystems<sup>2</sup>|SQLSRV_LOG_SYSTEM_ALL (-1)<br /><br />SQLSRV_LOG_SYSTEM_CONN (2)<br /><br />SQLSRV_LOG_SYSTEM_INIT (1)<br /><br />SQLSRV_LOG_SYSTEM_OFF (0)<br /><br />SQLSRV_LOG_SYSTEM_STMT (4)<br /><br />SQLSRV_LOG_SYSTEM_UTIL (8)|SQLSRV_LOG_SYSTEM_OFF (0)|  
|WarningsReturnAsErrors<sup>3</sup>|**True** (1) ou **false** (0)|**True** (1)|  
  
## <a name="return-value"></a>Valor de retorno  
Se **sqlsrv_configure** for chamado com uma configuração ou valor sem suporte, a função retornará **false**. Caso contrário, a função retornará **true**.  
  
## <a name="remarks"></a>Remarks  
(1) para obter mais informações sobre consultas de cliente, consulte [tipos de Cursor &#40;Driver SQLSRV&#41;](../../connect/php/cursor-types-sqlsrv-driver.md).  
  
(2) para obter mais informações sobre a atividade de registro em log, consulte [o log da atividade](../../connect/php/logging-activity.md).  
  
(3) para obter mais informações sobre como configurar o tratamento de erros e aviso, consulte [como: configurar o tratamento de erros e aviso usando o Driver SQLSRV](../../connect/php/how-to-configure-error-and-warning-handling-using-the-sqlsrv-driver.md).  
  
## <a name="see-also"></a>Consulte também  
[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Programação de guia para os Drivers da Microsoft para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md) 
  
