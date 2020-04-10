---
title: Obter a versão do driver | Microsoft Docs
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
ms.openlocfilehash: 1a1c5c6d4dcc3a5bd5acaac37ffdcdadc184e497
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924654"
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
  
  
