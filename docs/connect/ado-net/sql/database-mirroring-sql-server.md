---
title: Espelhamento de banco de dados no SQL Server
description: Descreve a funcionalidade de espelhamento de banco de dados.
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: 89befaff-bb46-4290-8382-e67cdb0e3de9
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 1c78f52f376ff6c333b952b8d013e17eefce45ea
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452278"
---
# <a name="database-mirroring-in-sql-server"></a>Espelhamento de banco de dados no SQL Server

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

O espelhamento de banco de dados no SQL Server permite que você mantenha uma cópia, ou espelho, de um banco de dados SQL Server em um servidor em espera. O espelhamento garante que duas cópias separadas dos dados existam o tempo todo, fornecendo alta disponibilidade e redundância completa de dados. O provedor do Microsoft SqlClient para SQL Server fornece suporte implícito para espelhamento de banco de dados, para que o desenvolvedor não precise realizar nenhuma ação ou escrever qualquer código depois de ter sido configurado para um banco de dados SQL Server. Além disso, o objeto <xref:Microsoft.Data.SqlClient.SqlConnection> dá suporte a um modo de conexão explícito que permite fornecer o nome de um servidor de parceiro de failover no <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A>.  
  
A seguinte sequência simplificada de eventos ocorre para um objeto <xref:Microsoft.Data.SqlClient.SqlConnection> que tem como alvo um banco de dados configurado para espelhamento:  
  
1. O aplicativo cliente se conecta com êxito ao banco de dados principal e o servidor envia de volta o nome do servidor parceiro, que é armazenado em cache no cliente.  
  
2. Se o servidor que contém o banco de dados principal falhar ou se a conectividade for interrompida, a conexão e o estado da transação serão perdidos. O aplicativo cliente tenta restabelecer uma conexão com o banco de dados principal e falha.  
  
3. O aplicativo cliente tenta, de modo transparente, estabelecer uma conexão com o banco de dados espelho no servidor parceiro. Se tiver sucesso, a conexão será redirecionada para o banco de dados espelho, que se tornará o novo banco de dados principal.  
  
## <a name="specifying-the-failover-partner-in-the-connection-string"></a>Especificando o parceiro de failover na cadeia de conexão  
Se você fornecer o nome de um servidor de parceiro de failover na cadeia de conexão, o cliente tentará, de modo transparente, uma conexão com o parceiro de failover se o banco de dados principal não estiver disponível quando o aplicativo cliente se conectar pela primeira vez.  
  
```csharp
";Failover Partner=PartnerServerName"  
```  
  
Se você omitir o nome do servidor de parceiro de failover e o banco de dados principal não estiver disponível quando o aplicativo cliente se conectar pela primeira vez, um <xref:Microsoft.Data.SqlClient.SqlException> será gerado.  
  
Quando um <xref:Microsoft.Data.SqlClient.SqlConnection> é aberto com êxito, o nome do parceiro de failover é retornado pelo servidor e substitui todos os valores fornecidos na cadeia de conexão.  
  
> [!NOTE]
>  Você deve especificar explicitamente o nome do catálogo ou do banco de dados inicial na cadeia de conexão para cenários de espelhamento de banco de dados. Se o cliente receber informações de failover em uma conexão que não tenha um catálogo inicial ou banco de dados especificado explicitamente, as informações de failover não serão armazenadas em cache e o aplicativo não tentará fazer failover se o servidor principal falhar. Se uma cadeia de conexão tiver um valor para o parceiro de failover, mas nenhum valor para o catálogo ou banco de dados inicial, um `InvalidArgumentException` será gerado.  
  
## <a name="retrieving-the-current-server-name"></a>Recuperando o nome do servidor atual  
No caso de um failover, você pode recuperar o nome do servidor ao qual a conexão atual está realmente conectada usando a propriedade <xref:Microsoft.Data.SqlClient.SqlConnection.DataSource%2A> de um objeto <xref:Microsoft.Data.SqlClient.SqlConnection>. O fragmento de código a seguir recupera o nome do servidor ativo, supondo que a variável de conexão faça referência a um <xref:Microsoft.Data.SqlClient.SqlConnection> aberto.  
  
Quando ocorre um evento de failover e a conexão é alternada para o servidor espelho, a propriedade **DataSource** é atualizada para refletir o nome do espelho.  
  
```csharp  
string activeServer = connection.DataSource;  
```  
  
## <a name="sqlclient-mirroring-behavior"></a>Comportamento de espelhamento do SqlClient  
O cliente sempre tenta se conectar ao servidor principal atual. Se ele falhar, ele tentará o parceiro de failover. Se o banco de dados espelho já tiver sido alternado para a função principal no servidor parceiro, a conexão terá sucesso e o novo mapeamento de principal-Mirror será enviado ao cliente e armazenado em cache durante o tempo de vida do <xref:System.AppDomain> de chamada. Não é armazenado no repositório persistente e não está disponível para conexões subsequentes em um **AppDomain** ou processo diferente. No entanto, está disponível para conexões subsequentes dentro do mesmo **AppDomain**. Observe que outro **AppDomain** ou processo que é executado no mesmo computador ou em um computador diferente sempre tem o pool de conexões, e essas conexões não são redefinidas. Nesse caso, se o banco de dados primário falhar, cada processo ou **AppDomain** falhará uma vez, e o pool será automaticamente limpo.  
  
> [!NOTE]
>  O suporte ao espelhamento no servidor é configurado de acordo com o banco de dados. Se as operações de manipulação de dados forem executadas em outros bancos de dado não incluídos no conjunto principal/de espelhamento, seja usando nomes com várias partes ou alterando o banco de dados atual, as alterações nesses outros bancos não serão propagadas em caso de falha. Nenhum erro será gerado quando os dados forem modificados em um banco de dados que não seja espelhado. O desenvolvedor deve avaliar o possível impacto dessas operações.  
  
## <a name="next-steps"></a>Próximas etapas
### <a name="database-mirroring-resources"></a>Recursos de espelhamento de bancos de dados  
Para obter a documentação conceitual e as informações sobre como configurar, implantar e administrar o espelhamento, consulte os seguintes recursos na documentação do SQL Server.  
  
|Recurso|Descrição|  
|--------------|-----------------|  
|[Espelhamento de Banco de Dados](../../../database-engine/database-mirroring/database-mirroring-sql-server.md)|Descreve como configurar e configurar o espelhamento no SQL Server.|  
