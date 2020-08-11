---
title: Obtendo a versão do driver
description: Saiba como e onde encontrar a versão do Microsoft JDBC Driver para SQL Server.
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5e241d72-16da-4ada-ac67-e6308394108f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f90f521457f5df17be814a179353d138a3245aea
ms.sourcegitcommit: b2ab989264dd9d23c184f43fff2ec8966793a727
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/14/2020
ms.locfileid: "86381190"
---
# <a name="getting-the-driver-version"></a>Obtendo a versão do driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  A versão do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] instalada pode ser encontrada das seguintes maneiras:  
  
-   Chame os métodos [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) methods [getDriverMajorVersion](../../connect/jdbc/reference/getdrivermajorversion-method-sqlserverdatabasemetadata.md), [getDriverMinorVersion](../../connect/jdbc/reference/getdriverminorversion-method-sqlserverdatabasemetadata.md) ou [getDriverVersion](../../connect/jdbc/reference/getdriverversion-method-sqlserverdatabasemetadata.md).  
  
-   A versão é exibida no arquivo readme.txt da distribuição do produto.  
  
 Além disso, o nome do driver JDBC pode ser retornado da chamada do método [getDriverName](../../connect/jdbc/reference/getdrivername-method-sqlserverdatabasemetadata.md) na classe SQLServerDatabaseMetaData. Ele retornará, por exemplo, "Microsoft JDBC Driver 6.4 para SQL Server".  
  
 A seguir, confira um exemplo da saída de chamadas para os métodos da classe SQLServerDatabaseMetaData:  
  
 `getDriverName = Microsoft JDBC Driver 6.4 for SQL Server`  
  
 `getDriverMajorVersion = 6`  
  
 `getDriverMinorVersion = 4`  
  
 `getDriverVersion = 6.4.` *xxx.x*  
  
 Onde "xxx.x" é o número de versão final.  
  
## <a name="see-also"></a>Confira também  
 [Diagnosticando problemas com o JDBC Driver](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
