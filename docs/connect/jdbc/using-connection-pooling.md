---
title: Como usar o pool de conexões
description: Saiba como o Driver JDBC para SQL Server fornece interfaces em conformidade com JDBC para dar suporte ao pool de conexões em Java.
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 699d4e8a-34bf-4c60-b0d5-4a10dad6084a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c3bcacec5f85150f7de437d936463a3b3807f9ef
ms.sourcegitcommit: cb620c77fe6bdefb975968837706750c31048d46
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2020
ms.locfileid: "86391742"
---
# <a name="using-connection-pooling"></a>Como usar o pool de conexões

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] oferece suporte a pool de conexões para Plataforma Java e Enterprise Edition (Java EE). O driver JDBC implementa interfaces do JDBC 3.0 necessárias para permitir que o driver participe de qualquer implementação de pool de conexões fornecida através de fornecedores de middleware e compatível com JDBC 3.0. Middleware como servidores de aplicativos Java EE geralmente fornecem instalações de pool de conexões compatíveis. O driver JDBC participará de conexões em pool nestes ambientes.  
  
> [!NOTE]  
> Embora o driver JDBC suporte pool de conexão de Java EE, ele não fornece sua própria implementação de pool. O driver depende de Servidores de Aplicativos Java de terceiros para gerenciar as conexões.  
  
## <a name="remarks"></a>Comentários

As classes para a implementação do pool de conexões são as seguintes.  
  
| Classe                                                           | Implementa                                                    | Descrição                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --------------------------------------------------------------- | ------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| com.microsoft.sqlserver.jdbc. SQLServerXADataSource             | javax.sql.ConnectionPoolDataSource and javax.sql.XADataSource | Nós recomendamos que você use a classe [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) para todas as suas necessidades de servidor Java EE, porque ela implementa todo o pool de JDBC 3.0 e todas as interfaces XA.                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| com.microsoft.sqlserver.jdbc. SQLServerConnectionPoolDataSource | javax.sql.ConnectionPoolDataSource                            | Esta classe é uma fábrica de conexão que permite que o servidor de aplicativos Java EE popule seu pool de conexão com conexões físicas. Se a configuração de seu fornecedor Java EE exigir uma classe que implementa javax.sql.ConnectionPoolDataSource, especifique o nome de classe como [SQLServerConnectionPoolDataSource](../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md). Nós geralmente recomendamos que você use a classe [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md), porque ela implementa tanto pool quanto interfaces XA, além de ter sido verificada em mais configurações de servidor Java EE. |
  
 O código do aplicativo JDBC sempre deve fechar explicitamente as conexões para poder tirar o melhor proveito do pool. Quando o aplicativo fecha uma conexão explicitamente, a implementação de pool pode reutilizar a conexão imediatamente. Se a conexão não for fechada, outros aplicativos não poderão reutilizá-la. Os aplicativos podem usar o constructo `finally` para ter certeza de que as conexões em pool estão fechadas mesmo que ocorra uma exceção.  
  
> [!NOTE]  
> O driver JDBC não chama o procedimento armazenado sp_reset_connection atualmente quando volta a conexão para o pool. Em vez disso, o driver depende de Servidores de Aplicativos Java de terceiros para voltar as conexões para os seus estados originais.  
  
## <a name="see-also"></a>Confira também

[Conectando ao SQL Server com o JDBC Driver](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
