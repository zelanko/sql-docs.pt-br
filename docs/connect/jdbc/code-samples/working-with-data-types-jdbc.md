---
title: Trabalhando com tipos de dados (JDBC) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b39f44d0-3710-4bc6-880c-35bd8c10a734
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6ccecd482516979a2f3ace2a4ce2c039af3ad1c4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="working-with-data-types-jdbc"></a>Trabalhando com tipos de dados (JDBC)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  A principal função do [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] é permitir que os desenvolvedores Java acessem dados contidos em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] bancos de dados. Para fazer isso, o driver JDBC atua como mediador da conversão entre [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipos de dados e tipos de linguagem Java e objetos.  
  
> [!NOTE]  
>  Para uma discussão detalhada sobre o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] e tipos de dados do driver JDBC, incluindo as suas diferenças e como eles são convertidos para tipos de dados de linguagem Java, consulte [Noções básicas sobre os tipos de dados do Driver JDBC](../../../connect/jdbc/understanding-the-jdbc-driver-data-types.md).  
  
 Para trabalhar com tipos de dados do SQL Server, o driver JDBC fornece get\<tipo > e defina\<tipo > métodos para o [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) e [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) classes e fornece get\<tipo > e atualizar\<tipo > métodos para o [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) classe. Qual método você usa depende do tipo de dados com os quais você está trabalhando, e se você está usando conjuntos de resultados ou consultas.  
  
 Os tópicos nesta seção descrevem como usar os tipos de dados do driver JDBC para acessar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] dados em seus aplicativos Java.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Exemplo de tipos de dados básicos](../../../connect/jdbc/basic-data-types-sample.md)|Descreve como usar métodos de getter de conjunto de resultados para recuperar básico [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] valores e como usar métodos de atualização de conjunto de resultados para atualizar esses valores de tipo de dados.|  
|[Exemplo de tipo de dados SQLXML](../../../connect/jdbc/sqlxml-data-type-sample.md)|Descreve como armazenar dados XML em um banco de dados relacional, como recuperar dados XML de um banco de dados e como analisar dados XML com o **SQLXML** tipo de dados Java.|  
  
## <a name="see-also"></a>Consulte também  
 [Aplicativos de exemplo do JDBC Driver](../../../connect/jdbc/sample-jdbc-driver-applications.md)  
  
  
