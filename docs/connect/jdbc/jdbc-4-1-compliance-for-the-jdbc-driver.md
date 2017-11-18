---
title: JDBC 4.1 conformidade para o Driver JDBC | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f087fd40-8451-478e-b465-43112c711515
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: d5b8e44c007766354e5c03058d16a41cbb72ad0e
ms.contentlocale: pt-br
ms.lasthandoff: 09/27/2017

---
# <a name="jdbc-41-compliance-for-the-jdbc-driver"></a>Conformidade do JDBC 4.1 com o JDBC Driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

    
> [!NOTE]  
>  Versões anteriores ao Microsoft JDBC Driver 4.2 para SQL Server são compatíveis com as especificações de API do Java Database Connectivity 4.0. Esta seção não se aplica a versões anteriores à versão 4.2.  
  
 A especificação de API do Java Database Connectivity 4.1 tem suporte pelo Microsoft JDBC Driver 4.2 para SQL Server, com os seguintes métodos de API.  
  
 **Classe SQLServerConnection**  
  
|Novo método|Description|Implementação do JDBC Driver|  
|----------------|-----------------|--------------------------------|  
|void abort(Executor executor)|Encerra uma conexão aberta com o SQL Server.|Implementados conforme descrito na interface do java.sql.Connection. Para obter mais detalhes, consulte [Java.SQL](http://docs.oracle.com/javase/7/docs/api/java/sql/Connection.html).|  
|void setSchema(String schema)|Define o esquema para a conexão atual.|O SQL Server não dá suporte a esquema de configuração para a sessão atual. O driver silenciosamente registra uma mensagem de aviso se esse método for chamado. Para obter mais detalhes, consulte [Java.SQL](http://docs.oracle.com/javase/7/docs/api/java/sql/Connection.html).|  
|Cadeia de caracteres getSchema()|Retorna o nome do esquema para a conexão atual.|Uma vez que o SQL Server não dá suporte a esquema de configuração para a conexão atual, o driver retorna o esquema padrão do usuário. Para obter mais detalhes, consulte [Java.SQL](http://docs.oracle.com/javase/7/docs/api/java/sql/Connection.html).|  
  
 **Classe SQLServerDatabaseMetaData**  
  
|Novo método|Description|Implementação do JDBC Driver|  
|----------------|-----------------|--------------------------------|  
|Boolean generatedKeyAlwaysReturned()|Retorna true já que o driver dá suporte a recuperação de chaves geradas|Implementados conforme descrito em java.sql. Interface DatabaseMetaData. Para obter mais detalhes, consulte [DatabaseMetadata](http://docs.oracle.com/javase/7/docs/api/java/sql/DatabaseMetaData.html).|  
|ResultSet getPseudoColumns (catálogo de cadeia de caracteres, cadeia de caracteres schemaPattern, cadeia de caracteres tableNamePattern, cadeia de caracteres columnNamePattern)|Recupera uma descrição das colunas pseudo/oculta|Retorna um resultado vazio definido, já que o SQL Server não tem uma noção formal de pseudo colunas. Para obter mais detalhes, consulte [DatabaseMetadata](http://docs.oracle.com/javase/7/docs/api/java/sql/DatabaseMetaData.html).|  
  
 **Classe SQLServerStatement**  
  
|Novo método|Description|Implementação do JDBC Driver|  
|----------------|-----------------|--------------------------------|  
|void closeOnCompletion()|Especifica se esta instrução será fechada quando todos os seus conjuntos de resultados dependentes forem fechados.|Implementado conforme descrito na interface java.sql.Statement. Para obter mais detalhes, consulte [Java.SQL. Statement](http://docs.oracle.com/javase/7/docs/api/java/sql/Statement.html).|  
|Boolean isCloseOnCompletion()|Retorna um valor que indica se esta instrução será fechada quando todos os seus conjuntos de resultados dependentes forem fechados.|Implementado conforme descrito na interface java.sql.Statement. Para obter mais detalhes, consulte [Java.SQL. Statement](http://docs.oracle.com/javase/7/docs/api/java/sql/Statement.html).|  
  
 A especificação do API da Conectividade do Banco de Dados Java 4.1 tem suporte pelo Microsoft JDBC Driver 4.2 para SQL Server, com os seguintes recursos.  
  
|Novo recurso|Description|  
|-----------------|-----------------|  
|Nova função de Escape<br /><br /> Escape de linhas de retorno limitado|Suporte parcial<br /><br /> Sintaxe de escape: limite \<linhas > [OFFSET < linha_offset >](using-sql-escape-sequences.md).|  
  
 A especificação de API do Java Database Connectivity 4.1 tem suporte pelo Microsoft JDBC Driver 4.2 para SQL Server, com os mapeamentos de tipo de dados a seguir.  
  
|Mapeamentos de tipo de dados|Description|  
|------------------------|-----------------|  
|Novos mapeamentos de tipo de dados agora têm suporte nos métodos PreparedStatement.setObject() e PreparedStatement.setNull().|1. Novo Java para mapeamento de tipo JDBC<br /><br /> (a) java.math.BigInteger para JDBC BIGINT<br /><br /> (b) java.util.Date e java.util.Calendar para JDBC TIMESTAMP<br /><br /> 2. Conversões de novo tipo de dados:<br /><br /> (a) java.math.BigInteger CHAR, VARCHAR, LONGVARCHAR e BIGINT<br /><br /> (b) java.util.Date e java.util.Calendar para CHAR, VARCHAR, LONGVARCHAR, DATE, TIME e TIMESTAMP<br /><br /> Para obter mais detalhes, consulte a especificação do JDBC 4.1.|  
  
  

