---
description: Conformidade do JDBC 4.1 com o JDBC Driver
title: Conformidade com JDBC 4.1 para o driver JDBC | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f087fd40-8451-478e-b465-43112c711515
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0b5cbc32712a54d7e783c77e086761be4a274dfd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438358"
---
# <a name="jdbc-41-compliance-for-the-jdbc-driver"></a>Conformidade do JDBC 4.1 com o JDBC Driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

    
> [!NOTE]  
>  Versões anteriores ao Microsoft JDBC Driver 4.2 para SQL Server são compatíveis com as especificações de API do Java Database Connectivity 4.0. Esta seção não se aplica a versões anteriores à versão 4.2.  
  
 A especificação de API do Java Database Connectivity 4.1 tem suporte pelo Microsoft JDBC Driver 4.2 para SQL Server, com os seguintes métodos de API.  
  
 **Classe SQLServerConnection**  
  
|Novo método|Descrição|Implementação do JDBC Driver|  
|----------------|-----------------|--------------------------------|  
|void abort(Executor executor)|Encerra uma conexão aberta com o SQL Server.|Implementados conforme descrito na interface do java.sql.Connection. Para ver mais detalhes, confira [java.sql.Connection](https://docs.oracle.com/javase/7/docs/api/java/sql/Connection.html).|  
|void setSchema(String schema)|Define o esquema para a conexão atual.|O SQL Server não dá suporte a esquema de configuração para a sessão atual. O driver silenciosamente registra uma mensagem de aviso se esse método for chamado. Para ver mais detalhes, confira [java.sql.Connection](https://docs.oracle.com/javase/7/docs/api/java/sql/Connection.html).|  
|Cadeia de caracteres getSchema()|Retorna o nome do esquema para a conexão atual.|Uma vez que o SQL Server não dá suporte a esquema de configuração para a conexão atual, o driver retorna o esquema padrão do usuário. Para ver mais detalhes, confira [java.sql.Connection](https://docs.oracle.com/javase/7/docs/api/java/sql/Connection.html).|  
  
 **classe SQLServerDatabaseMetaData**  
  
|Novo método|Descrição|Implementação do JDBC Driver|  
|----------------|-----------------|--------------------------------|  
|Boolean generatedKeyAlwaysReturned()|Retorna true já que o driver dá suporte a recuperação de chaves geradas|Implementados conforme descrito em java.sql. Interface DatabaseMetaData. Para ver mais detalhes, confira [java.sql.DatabaseMetaData](https://docs.oracle.com/javase/7/docs/api/java/sql/DatabaseMetaData.html).|  
|ResultSet getPseudoColumns (catálogo de cadeia de caracteres, cadeia de caracteres schemaPattern, cadeia de caracteres tableNamePattern, cadeia de caracteres columnNamePattern)|Recupera uma descrição das colunas pseudo/oculta|Retorna um resultado vazio definido, já que o SQL Server não tem uma noção formal de pseudo colunas. Para ver mais detalhes, confira [java.sql.DatabaseMetaData](https://docs.oracle.com/javase/7/docs/api/java/sql/DatabaseMetaData.html).|  
  
 **Classe SQLServerStatement**  
  
|Novo método|Descrição|Implementação do JDBC Driver|  
|----------------|-----------------|--------------------------------|  
|void closeOnCompletion()|Especifica se esta instrução será fechada quando todos os seus conjuntos de resultados dependentes forem fechados.|Implementado conforme descrito na interface java.sql.Statement. Para ver mais detalhes, confira [java.sql.Statement](https://docs.oracle.com/javase/7/docs/api/java/sql/Statement.html).|  
|Boolean isCloseOnCompletion()|Retorna um valor que indica se esta instrução será fechada quando todos os seus conjuntos de resultados dependentes forem fechados.|Implementado conforme descrito na interface java.sql.Statement. Para ver mais detalhes, confira [java.sql.Statement](https://docs.oracle.com/javase/7/docs/api/java/sql/Statement.html).|  
  
 A especificação do API da Conectividade do Banco de Dados Java 4.1 tem suporte pelo Microsoft JDBC Driver 4.2 para SQL Server, com os seguintes recursos.  
  
|Novo recurso|Descrição|  
|-----------------|-----------------|  
|Nova função de Escape<br /><br /> Escape de linhas de retorno limitado|Suporte parcial<br /><br /> Sintaxe de escape: LIMIT \<rows> [OFFSET <row_offset>](using-sql-escape-sequences.md).|  
  
 A especificação de API do Java Database Connectivity 4.1 tem suporte pelo Microsoft JDBC Driver 4.2 para SQL Server, com os mapeamentos de tipo de dados a seguir.  
  
|Mapeamentos de tipo de dados|Descrição|  
|------------------------|-----------------|  
|Novos mapeamentos de tipo de dados agora têm suporte nos métodos PreparedStatement.setObject() e PreparedStatement.setNull().|1. Novo Java para mapeamento de tipo JDBC<br /><br /> (a) java.math.BigInteger para JDBC BIGINT<br /><br /> (b) java.util.Date e java.util.Calendar para JDBC TIMESTAMP<br /><br /> 2. Conversões de novo tipo de dados:<br /><br /> (a) java.math.BigInteger CHAR, VARCHAR, LONGVARCHAR e BIGINT<br /><br /> (b) java.util.Date e java.util.Calendar para CHAR, VARCHAR, LONGVARCHAR, DATE, TIME e TIMESTAMP<br /><br /> Para obter mais detalhes, consulte a especificação do JDBC 4.1.|  
  
  
