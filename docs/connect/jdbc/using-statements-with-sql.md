---
title: Como usar instruções com SQL
description: Tenha uma visão geral do uso de diferentes tipos de instruções SQL com o Microsoft JDBC Driver para SQL Server.
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: fe28f48a-e1bc-48ff-a5e7-c24cd6e5ecc7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 49ab0f6367353847bdf3a9e0a7aff13975b4d711
ms.sourcegitcommit: 129f8574eba201eb6ade1f1620c6b80dfe63b331
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/30/2020
ms.locfileid: "87435281"
---
# <a name="using-statements-with-sql"></a>Como usar instruções com SQL

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Quando você trabalha com os dados em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] e as instruções SQL embutidas, pode usar diferentes classes. A classe usada depende do tipo de instrução SQL que você deseja executar.  
  
Se a instrução SQL não contiver parâmetros IN, use a classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md); se ela contiver parâmetros IN, use a classe [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).  
  
> [!NOTE]  
> Se você precisar usar instruções SQL contendo os parâmetros IN e OUT, deverá implementá-las como procedimentos armazenados e chamá-las usando a classe [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md). Para obter mais informações sobre o uso de procedimentos armazenados, confira [Como usar instruções com procedimentos armazenados](../../connect/jdbc/using-statements-with-stored-procedures.md).  
  
As seções a seguir descrevem os cenários diferentes para trabalhar usando dados em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com instruções SQL.  

## <a name="in-this-section"></a>Nesta seção  

| Tópico                                                                                                                        | Descrição                                                       |
| ---------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| [Como usar uma instrução SQL sem parâmetros](../../connect/jdbc/using-an-sql-statement-with-no-parameters.md)                 | Descreve como usar instruções SQL sem parâmetros.   |
| [Como usar uma instrução SQL com parâmetros](../../connect/jdbc/using-an-sql-statement-with-parameters.md)                       | Descreve como usar instruções SQL com parâmetros.      |
| [Como usar uma instrução SQL para modificar objetos de banco de dados](../../connect/jdbc/using-an-sql-statement-to-modify-database-objects.md) | Descreve como usar instruções SQL para modificar objetos de banco de dados.   |
| [Como usar uma instrução SQL para modificar dados](../../connect/jdbc/using-an-sql-statement-to-modify-data.md)                         | Descreve como usar instruções SQL para modificar dados em um banco de dados. |
  
## <a name="see-also"></a>Confira também

[Como usar instruções com o JDBC Driver](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
