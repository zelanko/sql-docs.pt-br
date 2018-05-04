---
title: Conectando e recuperando dados | Microsoft Docs
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
ms.assetid: ce43cc20-46a3-42ff-a3fb-75ad1ed10e08
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cd98a0b7954f5b67bedbaa09833b72d8f5914921
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="connecting-and-retrieving-data"></a>Conectando e recuperando dados
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Quando você estiver trabalhando com o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], há dois métodos principais para estabelecer uma conexão para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados. Um é definir as propriedades de conexão na URL de conexão e, em seguida, chame o método getConnection da classe DriverManager para retornar um [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) objeto.  
  
> [!NOTE]  
>  Para obter uma lista de propriedades de conexão com suporte pelo driver JDBC, consulte [definindo as propriedades de Conexão](../../connect/jdbc/setting-the-connection-properties.md).  
  
 O segundo método envolve definir as propriedades de conexão usando métodos setter a [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) classe e, em seguida, chamar o [getConnection](../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md) método para retornar um SQLServerConnection objeto.  
  
 Os tópicos nesta seção descrevem as diferentes maneiras que você pode se conectar a um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados e também demonstram técnicas diferentes para recuperar dados.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Exemplo de URL de conexão](../../connect/jdbc/connection-url-sample.md)|Descreve como usar uma URL de conexão para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e, em seguida, usar uma instrução SQL para recuperar dados.|  
|[Exemplo de fonte de dados](../../connect/jdbc/data-source-sample.md)|Descreve como usar uma fonte de dados para se conectar ao SQL Server e, em seguida, usar um procedimento armazenado para recuperar dados.|  
  
## <a name="see-also"></a>Consulte também  
 [Aplicativos de exemplo do JDBC Driver](../../connect/jdbc/sample-jdbc-driver-applications.md)  
  
  
