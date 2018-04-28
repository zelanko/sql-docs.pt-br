---
title: Usando metadados de parâmetro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: db2c1957-91c6-4989-a07b-9f8be6d2033a
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9299c3cff07a594ab58014b4835b4ad796756b5c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="using-parameter-metadata"></a>Usando metadados de parâmetro
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Para consultar um [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) ou um [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) objeto sobre os parâmetros que eles contêm, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] implementa o [ SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md) classe. Esta classe contém diversos campos e métodos que retornam informações como um único valor.  
  
 Para criar um objeto SQLServerParameterMetaData, você pode usar o [getParameterMetaData](../../connect/jdbc/reference/getparametermetadata-method-sqlserverpreparedstatement.md) métodos das classes SQLServerPreparedStatement e SQLServerCallableStatement.  
  
 No exemplo a seguir, uma conexão aberta para o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo é passado para a função, o método getParameterMetaData da classe SQLServerCallableStatement é usado para retornar um objeto SQLServerParameterMetaData e, em seguida, várias métodos do objeto SQLServerParameterMetaData são usados para exibir informações sobre o tipo e o modo dos parâmetros que estão contidos dentro do procedimento armazenado de Uspupdateemployeehireinfo.  
  
 [!code[JDBC#UsingParamMetaData1](../../connect/jdbc/codesnippet/Java/using-parameter-metadata_1.java)]  
    
> [!NOTE]  
Existem algumas limitações ao usar a classe SQLServerParameterMetaData com instruções preparadas. 
**Com o Microsoft JDBC Driver 6.0 (ou superior) para o SQL Server**: ao usar o SQL Server 2008 ou 2008 R2, o driver JDBC oferece suporte a instruções SELECT, DELETE, INSERT e UPDATE, desde que essas instruções não contêm subconsultas e/ou junções.  

Consultas de mesclagem também não há suporte para classe SQLServerParameterMetaData ao usar o SQL Server 2008 ou 2008 R2. Para o SQL Server 2012 e metadados de parâmetro de versões anteriores com consultas complexas que têm suporte.  

Não há suporte para a recuperação de metadados de parâmetro para colunas criptografadas. **Com o Microsoft JDBC Driver 4.1 ou 4.2 para SQL Server**: O JDBC driver dá suporte a instruções SELECT, DELETE, INSERT e UPDATE desde que essas instruções não contêm subconsultas e/ou junções. Consultas de mesclagem também não têm suporte para a classe SQLServerParameterMetaData.  
  
  
