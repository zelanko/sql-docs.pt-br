---
title: Conectando e recuperando dados | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ce43cc20-46a3-42ff-a3fb-75ad1ed10e08
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f76b740c9ba64439719a12d016cadaa7db2a7cc3
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66778251"
---
# <a name="connecting-and-retrieving-data"></a>Conectando e recuperando dados

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Quando você trabalha com o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], há dois métodos principais para estabelecer uma conexão com um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Um é definir as propriedades de conexão na URL de conexão e, em seguida, chamar o método getConnection da classe DriverManager para retornar um objeto [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
> [!NOTE]  
> Para obter uma lista de propriedades de conexão com suporte pelo driver JDBC, consulte [definindo as propriedades de Conexão](../../connect/jdbc/setting-the-connection-properties.md).  
  
O segundo método envolve definir as propriedades de conexão usando métodos setter da classe [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) e, em seguida, chamar o método [getConnection](../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md) para retornar um objeto SQLServerConnection.  
  
Os tópicos nesta seção descrevem os modos diferentes nos quais você pode se conectar a um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e também demonstram técnicas diferentes para recuperar dados.  
  
## <a name="in-this-section"></a>Nesta seção  
  
| Tópico                                                                | Descrição                                                                                                                                                   |
| -------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Exemplo de URL de conexão](../../connect/jdbc/connection-url-sample.md) | Descreve como usar uma URL de conexão para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e usar uma instrução SQL para recuperar dados. |
| [Exemplo de fonte de dados](../../connect/jdbc/data-source-sample.md)       | Descreve como usar uma fonte de dados para se conectar ao SQL Server e, em seguida, usar um procedimento armazenado para recuperar dados.                                                 |
  
## <a name="see-also"></a>Consulte Também

[Aplicativos de exemplo do JDBC Driver](../../connect/jdbc/sample-jdbc-driver-applications.md)  
  
