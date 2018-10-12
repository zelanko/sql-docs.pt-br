---
title: sqlsrv_configure | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_configure
apitype: NA
helpviewer_keywords:
- sqlsrv_configure
- API Reference, sqlsrv_configure
ms.assetid: 9393f975-a4ef-4c50-b4dd-14892fc55cc9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 98c3848ad344fcbb964d1b3a5e9ec1a6afe8703f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47618685"
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
|ClientBufferMaxKBSize<sup>1</sup>|Um número não negativo até o limite de memória do PHP.<br /><br />Zero e números negativos não são permitidos.|10240 KB|  
|LogSeverity<sup>2</sup>|SQLSRV_LOG_SEVERITY_ALL (-1)<br /><br />SQLSRV_LOG_SEVERITY_ERROR (1)<br /><br />SQLSRV_LOG_SEVERITY_NOTICE (4)<br /><br />SQLSRV_LOG_SEVERITY_WARNING (2)|SQLSRV_LOG_SEVERITY_ERROR (1)|  
|LogSubsystems<sup>2</sup>|SQLSRV_LOG_SYSTEM_ALL (-1)<br /><br />SQLSRV_LOG_SYSTEM_CONN (2)<br /><br />SQLSRV_LOG_SYSTEM_INIT (1)<br /><br />SQLSRV_LOG_SYSTEM_OFF (0)<br /><br />SQLSRV_LOG_SYSTEM_STMT (4)<br /><br />SQLSRV_LOG_SYSTEM_UTIL (8)|SQLSRV_LOG_SYSTEM_OFF (0)|  
|WarningsReturnAsErrors<sup>3</sup>|**true** (1) ou **false** (0)|**true** (1)|  
  
## <a name="return-value"></a>Valor retornado  
Se **sqlsrv_configure** for chamado com uma configuração ou valor sem suporte, a função retornará **false**. Caso contrário, a função retornará **true**.  
  
## <a name="remarks"></a>Remarks  
(1) Para saber mais sobre as consultas do lado do cliente, confira [Tipos de cursor &#40;SQLSRV Driver&#41;](../../connect/php/cursor-types-sqlsrv-driver.md).  
  
(2) Para saber mais sobre o registro de atividades em log, confira [Logging Activity](../../connect/php/logging-activity.md).  
  
(3) Para saber mais sobre a configuração do tratamento de erros e avisos, confira [Como configurar o tratamento de erros e avisos usando o driver SQLSRV](../../connect/php/how-to-configure-error-and-warning-handling-using-the-sqlsrv-driver.md).  
  
## <a name="see-also"></a>Consulte Também  
[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Guia de programação para os Drivers da Microsoft para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md) 
  
