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
ms.openlocfilehash: 73be4e0bc7a20a8a592493badf95a123ad6ade84
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37970051"
---
# <a name="working-with-data-types-jdbc"></a>Trabalhando com tipos de dados (JDBC)
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  A função primária do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] é permitir que os desenvolvedores Java acessem dados contidos nos bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Para realizar isso, o driver JDBC atua como mediador da conversão entre tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e tipos e objetos da linguagem Java.  
  
> [!NOTE]  
>  Para acompanhar uma discussão detalhada dos tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e do driver JDBC, incluindo as suas diferenças e como eles são convertidos para tipos de dados da linguagem Java, veja [Compreendendo os tipos de dados do driver JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md).  
  
 Para trabalhar com tipos de dados do SQL Server, o driver JDBC fornece métodos get\<Type> e set\<Type> para as classes [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) e [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md), e fornece os métodos get\<Type> e update\<Type> para a classe [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md). Qual método você usa depende do tipo de dados com os quais você está trabalhando, e se você está usando conjuntos de resultados ou consultas.  
  
 Os tópicos nesta seção descrevem como usar os tipos de dados do driver JDBC para acessar dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] em seus aplicativos Java.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Exemplo de tipos de dados básicos](../../connect/jdbc/basic-data-types-sample.md)|Descreve como usar métodos getter de conjunto de resultados para recuperar valores de tipo de dados básicos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], além de como usar métodos de atualização de conjunto de resultados para atualizar esses valores.|  
|[Exemplo de tipo de dados SQLXML](../../connect/jdbc/sqlxml-data-type-sample.md)|Descreve como armazenar dados XML em um banco de dados relacional, como recuperar dados XML de um banco de dados, e como analisar dados XML com um tipo de dados **SQLXML** Java.|  
  
## <a name="see-also"></a>Consulte Também  
 [Aplicativos de exemplo do JDBC Driver](../../connect/jdbc/sample-jdbc-driver-applications.md)  
  
  
