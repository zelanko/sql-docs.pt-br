---
title: Notificações de consulta no SQL Server
description: Descreve como os aplicativos .NET podem solicitar notificações de SQL Server quando os dados são alterados.
ms.date: 08/15/2019
ms.assetid: 0f0ba1a1-3180-4af8-87f7-c795dc8f8f55
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: d47241e3656e3ca7b4f5ea0eebe9f2cc8b571bf6
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452076"
---
# <a name="query-notifications-in-sql-server"></a>Notificações de consulta no SQL Server

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Com base na infraestrutura do Service Broker, as notificações de consulta permitem que os aplicativos sejam notificados em caso de alteração nos dados. Esse recurso é particularmente útil para aplicativos que fornecem um cache de informações de um banco de dados, como um aplicativo da Web, e precisam ser notificados quando os dados de origem são alterados.  
  
Há três maneiras pelas quais você pode implementar notificações de consulta usando o ADO.NET:  
  
- A implementação de nível baixo é fornecida pela classe `SqlNotificationRequest` que expõe a funcionalidade do lado do servidor, permitindo que você execute um comando com uma solicitação de notificação.  
  
- A implementação de alto nível é fornecida pela classe `SqlDependency`, que é uma classe que fornece uma abstração de alto nível da funcionalidade de notificação entre o aplicativo de origem e SQL Server, permitindo que você use uma dependência para detectar alterações no servidor. Na maioria dos casos, essa é a maneira mais simples e eficiente de aproveitar SQL Server funcionalidade de notificações por aplicativos cliente gerenciados usando o Microsoft SqlClient Provedor de Dados para SQL Server.  
  
- Além disso, os aplicativos Web criados usando o ASP.NET 2,0 ou posterior podem usar as classes auxiliares `SqlCacheDependency`.  
  
As notificações de consulta são usadas para aplicativos que precisam atualizar exibições ou caches em resposta a alterações nos dados subjacentes. Microsoft SQL Server permite que os aplicativos .NET enviem um comando para SQL Server e solicite notificação se a execução do mesmo comando produzir conjuntos de resultados diferentes daqueles recuperados inicialmente. As notificações geradas no servidor são enviadas pelas filas para serem processadas posteriormente.  
  
Você pode configurar notificações para instruções SELECT e EXECUTE. Ao usar uma instrução EXECUTE, SQL Server registra uma notificação para o comando executado em vez da própria instrução EXECUTE. O comando deve atender os requisitos e as limitações de uma instrução SELECT. Quando um comando que registra uma notificação contiver mais de uma instrução, o Mecanismo de Banco de Dados criará uma notificação para cada instrução no lote.  
  
Se você estiver desenvolvendo um aplicativo em que precise receber notificações confiáveis imediatamente quando os dados forem alterados, examine as seções **Planejando uma estratégia eficiente das notificações de consulta** e **Alternativas para notificações de consulta** no tópico [Planejando para notificações](https://go.microsoft.com/fwlink/?LinkId=211984) nos Manuais Online do SQL Server. Para obter mais informações sobre notificações de consulta e SQL Server Service Broker, consulte os links a seguir para tópicos em Manuais Online do SQL Server.  
  
**Documentação do SQL Server**  
  
- [Usando notificações de consulta](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms175110(v=sql.105))  
  
- [Criando uma consulta para notificação](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms181122(v=sql.105))  
  
- [Desenvolvimento (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522889(v=sql.105))  
  
- [Service Broker Developer InfoCenter](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms166100(v=sql.105))  
  
- [Guia do desenvolvedor (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522908(v=sql.105))  
  
## <a name="in-this-section"></a>Nesta seção  
[Habilitando notificações de consulta](enable-query-notifications.md)  
Discute como usar notificações de consulta, incluindo os requisitos para habilitá-las e usá-las.  
  
[SqlDependency em um aplicativo ASP.NET](sqldependency-aspnet-app.md)  
Demonstra como usar notificações de consulta de um aplicativo ASP.NET.  
  
[Detectando alterações com SqlDependency](detect-changes-sqldependency.md)  
Demonstra como detectar quando os resultados da consulta serão diferentes daqueles recebidos originalmente.  
  
[Execução de SqlCommand com um SqlNotificationRequest](sqlcommand-execution-sqlnotificationrequest.md)  
Demonstra como configurar um objeto <xref:Microsoft.Data.SqlClient.SqlCommand> para trabalhar com uma notificação de consulta.  
  
## <a name="reference"></a>Referência  
<xref:Microsoft.Data.Sql.SqlNotificationRequest>  
Descreve a classe <xref:Microsoft.Data.Sql.SqlNotificationRequest> e todos os seus membros.  
  
<xref:Microsoft.Data.SqlClient.SqlDependency>  
Descreve a classe <xref:Microsoft.Data.SqlClient.SqlDependency> e todos os seus membros.  
  
<xref:System.Web.Caching.SqlCacheDependency>  
Descreve a classe <xref:System.Web.Caching.SqlCacheDependency> e todos os seus membros.  
  
## <a name="next-steps"></a>Próximas etapas
- [SQL Server e ADO.NET](index.md)
