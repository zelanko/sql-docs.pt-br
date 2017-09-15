---
title: Conectando e recuperando dados | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ce43cc20-46a3-42ff-a3fb-75ad1ed10e08
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ff00f7cfde3f75a653be5d89064d9b3d56268295
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="connecting-and-retrieving-data"></a>Conectando e recuperando dados
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Quando você estiver trabalhando com o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)], há dois métodos principais para estabelecer uma conexão para um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] banco de dados. Um é definir as propriedades de conexão na URL de conexão e, em seguida, chame o método getConnection da classe DriverManager para retornar um [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto.  
  
> [!NOTE]  
>  Para obter uma lista de propriedades de conexão com suporte pelo driver JDBC, consulte [definindo as propriedades de Conexão](../../../connect/jdbc/setting-the-connection-properties.md).  
  
 O segundo método envolve definir as propriedades de conexão usando métodos setter a [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) classe e, em seguida, chamar o [getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md) método para retornar um SQLServerConnection objeto.  
  
 Os tópicos nesta seção descrevem as diferentes maneiras que você pode se conectar a um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] banco de dados e também demonstram técnicas diferentes para recuperar dados.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Exemplo de URL de conexão](../../../connect/jdbc/connection-url-sample.md)|Descreve como usar uma URL de conexão para se conectar ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] e, em seguida, usar uma instrução SQL para recuperar dados.|  
|[Exemplo de fonte de dados](../../../connect/jdbc/data-source-sample.md)|Descreve como usar uma fonte de dados para se conectar ao SQL Server e, em seguida, usar um procedimento armazenado para recuperar dados.|  
  
## <a name="see-also"></a>Consulte também  
 [Aplicativos de exemplo do JDBC Driver](../../../connect/jdbc/sample-jdbc-driver-applications.md)  
  
  
