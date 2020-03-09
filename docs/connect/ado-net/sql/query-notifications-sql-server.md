---
title: Notificações de consulta no SQL Server
description: Descreve como os aplicativos .NET podem solicitar notificações do SQL Server quando os dados foram alterados.
ms.date: 08/15/2019
ms.assetid: 0f0ba1a1-3180-4af8-87f7-c795dc8f8f55
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 57222c852ac2ba8c1aedf42075b69587a4b3843d
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/07/2020
ms.locfileid: "78896571"
---
# <a name="query-notifications-in-sql-server"></a>Notificações de consulta no SQL Server

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Com base na infraestrutura do Service Broker, as notificações de consulta permitem que os aplicativos sejam notificados em caso de alteração nos dados. Esse recurso é particularmente útil para aplicativos que fornecem um cache de informações de um banco de dados, como um aplicativo da Web, e precisam ser notificados quando os dados de origem são alterados.  
  
Há três maneiras pelas quais você pode implementar notificações de consulta usando o ADO.NET:  
  
- A implementação de nível baixo é fornecida pela classe `SqlNotificationRequest`, que expõe a funcionalidade do lado do servidor, permitindo que você execute um comando com uma solicitação de notificação.  
  
- A implementação de alto nível é fornecida pela classe `SqlDependency`, que é uma classe que fornece uma abstração de alto nível da funcionalidade de notificação entre o aplicativo de origem e o SQL Server, permitindo que você use uma dependência para detectar alterações no servidor. Na maioria dos casos, essa é a maneira mais simples e eficiente de aproveitar a funcionalidade de notificações do SQL Server por aplicativos cliente gerenciados usando o Provedor de Dados do Microsoft SqlClient para SQL Server.  
  
- Além disso, os aplicativos Web criados usando o ASP.NET 2.0 ou posterior podem usar as classes auxiliares `SqlCacheDependency`.  
  
As notificações de consulta são usadas para aplicativos que precisam atualizar exibições ou caches em resposta a alterações nos dados subjacentes. O Microsoft SQL Server permite que os aplicativos .NET enviem um comando para o SQL Server e solicitem notificação caso a execução do mesmo comando viesse a produzir conjuntos de resultados diferentes daqueles recuperados inicialmente. As notificações geradas no servidor são enviadas pelas filas para serem processadas posteriormente.  
  
Você pode configurar notificações para as instruções SELECT e EXECUTE. Ao usar uma instrução EXECUTE, o SQL Server registra uma notificação para o comando executado e não a própria instrução EXECUTE. O comando deve atender os requisitos e as limitações de uma instrução SELECT. Quando um comando que registra uma notificação contiver mais de uma instrução, o Mecanismo de Banco de Dados criará uma notificação para cada instrução no lote.  
  
Se você estiver desenvolvendo um aplicativo em que precise receber notificações confiáveis imediatamente quando os dados forem alterados, examine as seções **Planejando uma estratégia eficiente das notificações de consulta** e **Alternativas para notificações de consulta** no tópico [Planejando para notificações](https://go.microsoft.com/fwlink/?LinkId=211984) nos Manuais Online do SQL Server. Para obter mais informações sobre as notificações de consulta e o SQL Server Service Broker, confira os links a seguir para tópicos nos Manuais Online do SQL Server.  
  
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
Demonstra como usar notificações de consulta em um aplicativo ASP.NET.  
  
[Detectando alterações com SqlDependency](detect-changes-sqldependency.md)  
Demonstra como detectar quando os resultados da consulta serão diferentes daqueles recebidos originalmente.  
  
[Execução de SqlCommand com um SqlNotificationRequest](sqlcommand-execution-sqlnotificationrequest.md)  
Demonstra como configurar um objeto <xref:Microsoft.Data.SqlClient.SqlCommand> para trabalhar com uma notificação de consulta.  
  
## <a name="reference"></a>Referência  
<xref:Microsoft.Data.Sql.SqlNotificationRequest>  
Descreve a classe <xref:Microsoft.Data.Sql.SqlNotificationRequest> e todos os membros dela.  
  
<xref:Microsoft.Data.SqlClient.SqlDependency>  
Descreve a classe <xref:Microsoft.Data.SqlClient.SqlDependency> e todos os membros dela.  
  
<xref:System.Web.Caching.SqlCacheDependency>  
Descreve a classe <xref:System.Web.Caching.SqlCacheDependency> e todos os membros dela.  
  
## <a name="next-steps"></a>Próximas etapas
- [SQL Server e ADO.NET](index.md)
