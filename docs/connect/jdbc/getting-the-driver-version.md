---
title: Obter a versão do Driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5e241d72-16da-4ada-ac67-e6308394108f
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d3828c04f418a31e2dacddb97472ec3b2f776a5e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getting-the-driver-version"></a>Obtendo a versão do driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  A versão do instalado [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] pode ser encontrada das seguintes maneiras:  
  
-   Chamar o [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) métodos [getDriverMajorVersion](../../connect/jdbc/reference/getdrivermajorversion-method-sqlserverdatabasemetadata.md), [getDriverMinorVersion](../../connect/jdbc/reference/getdriverminorversion-method-sqlserverdatabasemetadata.md), ou [getDriverVersion](../../connect/jdbc/reference/getdriverversion-method-sqlserverdatabasemetadata.md).  
  
-   A versão é exibida no arquivo readme.txt da distribuição do produto.  
  
 Além disso, o nome do driver JDBC pode ser retornado do [getDriverName](../../connect/jdbc/reference/getdrivername-method-sqlserverdatabasemetadata.md) chamada de método na classe SQLServerDatabaseMetaData. Ela retornará, por exemplo, "Microsoft JDBC Driver 6.4 para SQL Server".  
  
 Este é um exemplo da saída de chamadas para os métodos da classe SQLServerDatabaseMetaData:  
  
 `getDriverName = Microsoft JDBC Driver 6.4 for SQL Server`  
  
 `getDriverMajorVersion = 6`  
  
 `getDriverMinorVersion = 4`  
  
 `getDriverVersion = 6.4.` *xxx.x*  
  
 Onde "xxx.x" é o número de versão final.  
  
## <a name="see-also"></a>Consulte também  
 [Diagnosticando problemas com o JDBC Driver](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
