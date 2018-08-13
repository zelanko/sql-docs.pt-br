---
title: Usando instruções com SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: fe28f48a-e1bc-48ff-a5e7-c24cd6e5ecc7
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1d044c1747b13f94c6f7feb902144d51b50af870
ms.sourcegitcommit: 2f9cafc1d7a3773a121bdb78a095018c8b7c149f
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39662218"
---
# <a name="using-statements-with-sql"></a>Usando instruções com SQL

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Quando você trabalha com os dados em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] usando o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] e as instruções SQL embutidas, pode usar diferentes classes. A classe usada depende do tipo de instrução SQL que você deseja executar.  
  
Se a instrução SQL não contiver parâmetros IN, use a classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md); se ela contiver parâmetros IN, use a classe [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).  
  
> [!NOTE]  
> Se você precisar usar instruções SQL contendo os parâmetros IN e OUT, deverá implementá-las como procedimentos armazenados e chamá-las usando a classe [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md). Para obter mais informações sobre como usar procedimentos armazenados, consulte [usando instruções com procedimentos armazenados](../../connect/jdbc/using-statements-with-stored-procedures.md).  
  
As seções a seguir descrevem os cenários diferentes para trabalhar usando dados em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] com instruções SQL.  

## <a name="in-this-section"></a>Nesta seção  

| Tópico                                                                                                                        | Descrição                                                       |
| ---------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| [Usando uma instrução SQL sem parâmetros](../../connect/jdbc/using-an-sql-statement-with-no-parameters.md)                 | Descreve como usar instruções SQL sem parâmetros.   |
| [Usando uma instrução SQL com parâmetros](../../connect/jdbc/using-an-sql-statement-with-parameters.md)                       | Descreve como usar instruções SQL com parâmetros.      |
| [Usando uma instrução SQL para modificar objetos de banco de dados](../../connect/jdbc/using-an-sql-statement-to-modify-database-objects.md) | Descreve como usar instruções SQL para modificar objetos de banco de dados.   |
| [Usando uma instrução SQL para modificar dados](../../connect/jdbc/using-an-sql-statement-to-modify-data.md)                         | Descreve como usar instruções SQL para modificar dados em um banco de dados. |
  
## <a name="see-also"></a>Consulte Também

[Usando instruções com o JDBC Driver](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
