---
title: "Usando o pool de Conexão | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 699d4e8a-34bf-4c60-b0d5-4a10dad6084a
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 47a65bf1c9ce6afdedd1f68c0431912af4aea402
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="using-connection-pooling"></a>Usando pool de conexões
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] oferece suporte para plataforma Java, Enterprise Edition (Java EE) pooling de conexão. O driver JDBC implementa interfaces do JDBC 3.0 necessárias para permitir que o driver participe de qualquer implementação de pool de conexões fornecida através de fornecedores de middleware e compatível com JDBC 3.0. Middleware como servidores de aplicativos Java EE geralmente fornecem instalações de pool de conexões compatíveis. O driver JDBC participará de conexões em pool nestes ambientes.  
  
> [!NOTE]  
>  Embora o driver JDBC suporte pool de conexão de Java EE, ele não fornece sua própria implementação de pool. O driver depende de Servidores de Aplicativos Java de terceiros para gerenciar as conexões.  
  
## <a name="remarks"></a>Comentários  
 As classes para a implementação do pool de conexões são as seguintes.  
  
|Classe|Implements|Description|  
|-----------|----------------|-----------------|  
|com.microsoft.SQLServer.JDBC. SQLServerXADataSource|javax.sql.ConnectionPoolDataSource and javax.sql.XADataSource|Recomendamos que você use o [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) precisa de classe para o servidor de Java EE, porque ela implementa todo o pool de JDBC 3.0 e XA interfaces.|  
|com.microsoft.SQLServer.JDBC. SQLServerConnectionPoolDataSource|javax.sql.ConnectionPoolDataSource|Esta classe é uma fábrica de conexão que permite que o servidor de aplicativos Java EE popule seu pool de conexão com conexões físicas. Se a configuração de seu fornecedor Java EE exigir uma classe que implementa javax.SQL. connectionpooldatasource, especifique o nome de classe como [SQLServerConnectionPoolDataSource](../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md). Nós geralmente recomendamos que você use o [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) classe em vez disso, porque ela implementa tanto pool quanto interfaces XA e ter sido verificada em mais configurações de servidor Java EE.|  
  
 O código do aplicativo JDBC sempre deve fechar explicitamente as conexões para poder tirar o melhor proveito do pool. Quando o aplicativo fecha uma conexão explicitamente, a implementação de pool pode reutilizar a conexão imediatamente. Se a conexão não for fechada, outros aplicativos não poderão reutilizá-la. Os aplicativos podem usar o `finally` construção para certificar-se de que as conexões em pool estão fechadas mesmo que ocorra uma exceção.  
  
> [!NOTE]  
>  O driver JDBC não chama o procedimento armazenado sp_reset_connection atualmente quando volta a conexão para o pool. Em vez disso, o driver depende de Servidores de Aplicativos Java de terceiros para voltar as conexões para os seus estados originais.  
  
## <a name="see-also"></a>Consulte também  
 [Conectando ao SQL Server com o JDBC Driver](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
