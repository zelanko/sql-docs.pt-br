---
title: Obtendo a versão do Driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5e241d72-16da-4ada-ac67-e6308394108f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2cfe90d0a38cf5e599d82a6208a145daa3a3d1c7
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66781823"
---
# <a name="getting-the-driver-version"></a>Obtendo a versão do driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  A versão do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] instalada pode ser encontrada das seguintes maneiras:  
  
-   Chame os métodos [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) methods [getDriverMajorVersion](../../connect/jdbc/reference/getdrivermajorversion-method-sqlserverdatabasemetadata.md), [getDriverMinorVersion](../../connect/jdbc/reference/getdriverminorversion-method-sqlserverdatabasemetadata.md) ou [getDriverVersion](../../connect/jdbc/reference/getdriverversion-method-sqlserverdatabasemetadata.md).  
  
-   A versão é exibida no arquivo readme.txt da distribuição do produto.  
  
 Além disso, o nome do driver JDBC pode ser retornado da chamada do método [getDriverName](../../connect/jdbc/reference/getdrivername-method-sqlserverdatabasemetadata.md) na classe SQLServerDatabaseMetaData. Ele retornará, por exemplo, "Microsoft JDBC Driver 6.4 para SQL Server".  
  
 Este é um exemplo da saída de chamadas para os métodos da classe SQLServerDatabaseMetaData:  
  
 `getDriverName = Microsoft JDBC Driver 6.4 for SQL Server`  
  
 `getDriverMajorVersion = 6`  
  
 `getDriverMinorVersion = 4`  
  
 `getDriverVersion = 6.4.` *xxx.x*  
  
 Onde "xxx.x" é o número de versão final.  
  
## <a name="see-also"></a>Consulte Também  
 [Diagnosticando problemas com o JDBC Driver](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
