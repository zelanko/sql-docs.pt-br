---
title: Padrão de tipos de dados do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- default data types
- converting data types
ms.assetid: 65c7c211-96d3-4e65-a1de-1fe8d21348e7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9f3259d713fd846e59020b2551d5598f77b7d5d5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47704374"
---
# <a name="default-sql-server-data-types"></a>Tipos de dados do SQL Server padrão
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Quando dados forem enviados para o servidor, os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] os converterão do tipo de dados do PHP em um tipo de dados do SQL Server se nenhum tipo de dados do SQL Server tiver sido especificado pelo usuário. A tabela a seguir lista o tipo de dados do PHP (o tipo de dados que está sendo enviado para o servidor) e o tipo de dados do SQL Server padrão (o tipo de dados no qual os dados são convertidos). Para obter detalhes sobre como especificar tipos de dados ao enviar dados para o servidor, consulte [Como especificar tipos de dados do SQL Server usando o driver SQLSRV](../../connect/php/how-to-specify-sql-server-data-types-when-using-the-sqlsrv-driver.md).  
  
|Tipo de dados do PHP|Tipo do SQL Server padrão no driver SQLSRV|Tipo do SQL Server padrão no driver PDO_SQLSRV|  
|-----------------|------------------------------------------------|-----------------------------------------------------|  
|NULL|varchar(1)|sem suporte|  
|Booliano|bit|bit|  
|Integer|INT|INT|  
|float|float(24)|sem suporte|  
|Cadeia de caracteres (comprimento menor que 8.000 bytes)|varchar(<string length>)|varchar(<string length>)|  
|Cadeia de caracteres (comprimento maior que 8.000 bytes)|varchar(max)|varchar(max)|  
|Recurso|Sem suporte.|Sem suporte.|  
|Fluxo (codificação: não binário)|varchar(max)|varchar(max)|  
|Fluxo (codificação: binário)|varbinary|varbinary|  
|Array|Sem suporte.|Sem suporte.|  
|Object|Sem suporte.|Sem suporte.|  
|DateTime (1)|DATETIME|Sem suporte.|  
  
## <a name="see-also"></a>Consulte Também  
[Constantes &#40;Drivers da Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)

[Convertendo tipos de dados](../../connect/php/converting-data-types.md)

[sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md)

[Tipos do PHP](http://php.net/manual/language.types.php)

[Tipos de dados (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql)  
  
