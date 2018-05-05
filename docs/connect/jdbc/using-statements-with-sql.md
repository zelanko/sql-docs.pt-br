---
title: Usando as instruções com SQL | Microsoft Docs
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
ms.assetid: fe28f48a-e1bc-48ff-a5e7-c24cd6e5ecc7
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 242b7ca6f483b65e054b43ef0fa370b57bd3f272
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="using-statements-with-sql"></a>Usando instruções com SQL
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Quando você trabalha com dados em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados usando o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] e instruções SQL embutidas, existem classes diferentes que você pode usar. A classe usada depende do tipo de instrução SQL que você deseja executar.  
  
 Se a instrução SQL não contiver parâmetros IN, use o [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) classe, mas se ele contiver parâmetros IN, use o [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) classe.  
  
> [!NOTE]  
>  Se você precisar usar instruções SQL que contêm IN e parâmetros OUT, você deve implementá-las como procedimentos armazenados e chamá-los usando o [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) classe. Para obter mais informações sobre como usar procedimentos armazenados, consulte [usando instruções com procedimentos armazenados](../../connect/jdbc/using-statements-with-stored-procedures.md).  
  
 As seções a seguir descrevem os cenários diferentes para trabalhar com dados em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados usando instruções SQL.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Usando uma instrução SQL sem parâmetros](../../connect/jdbc/using-an-sql-statement-with-no-parameters.md)|Descreve como usar instruções SQL sem parâmetros.|  
|[Usando uma instrução SQL com parâmetros](../../connect/jdbc/using-an-sql-statement-with-parameters.md)|Descreve como usar instruções SQL com parâmetros.|  
|[Usando uma instrução SQL para modificar objetos de banco de dados](../../connect/jdbc/using-an-sql-statement-to-modify-database-objects.md)|Descreve como usar instruções SQL para modificar objetos de banco de dados.|  
|[Usando uma instrução SQL para modificar dados](../../connect/jdbc/using-an-sql-statement-to-modify-data.md)|Descreve como usar instruções SQL para modificar dados em um banco de dados.|  
  
## <a name="see-also"></a>Consulte também  
 [Usando instruções com o JDBC Driver](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
