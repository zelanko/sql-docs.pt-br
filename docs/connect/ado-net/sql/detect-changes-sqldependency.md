---
title: Detectando alterações com SqlDependency
description: Demonstra como detectar quando os resultados da consulta serão diferentes daqueles recebidos originalmente.
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: e6a58316-f005-4477-92e1-45cc2eb8c5b4
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 2d2c4c48a9085fa83d6104233be5f2e1c6b11318
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452240"
---
# <a name="detecting-changes-with-sqldependency"></a>Detectando alterações com SqlDependency

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Um objeto <xref:Microsoft.Data.SqlClient.SqlDependency> pode ser associado a um <xref:Microsoft.Data.SqlClient.SqlCommand> para detectar quando os resultados da consulta são diferentes dos recuperados originalmente. Você também pode atribuir um delegado ao evento `OnChange`, que será acionado quando os resultados forem alterados para um comando associado. Você deve associar o <xref:Microsoft.Data.SqlClient.SqlDependency> ao comando antes de executar o comando. A propriedade `HasChanges` da <xref:Microsoft.Data.SqlClient.SqlDependency> também pode ser usada para determinar se os resultados da consulta foram alterados desde que os dados foram recuperados pela primeira vez.

## <a name="security-considerations"></a>Considerações sobre segurança

A infraestrutura de dependência depende de um <xref:Microsoft.Data.SqlClient.SqlConnection> que é aberto quando <xref:Microsoft.Data.SqlClient.SqlDependency.Start%2A> é chamado para receber notificações de que os dados subjacentes foram alterados para um determinado comando. A capacidade de um cliente iniciar a chamada para `SqlDependency.Start` é controlada por meio do uso de <xref:Microsoft.Data.SqlClient.SqlClientPermission> e de atributos de segurança de acesso a código. Para obter mais informações, consulte [habilitando notificações de consulta](enable-query-notifications.md).

### <a name="example"></a>Exemplo

As etapas a seguir ilustram como declarar uma dependência, executar um comando e receber uma notificação quando o conjunto de resultados for alterado:

1. Inicia uma conexão `SqlDependency` com o servidor.

2. Crie <xref:Microsoft.Data.SqlClient.SqlConnection> e <xref:Microsoft.Data.SqlClient.SqlCommand> objetos para se conectar ao servidor e definir uma instrução Transact-SQL.

3. Crie um novo objeto `SqlDependency` ou use um existente e vincule-o ao objeto `SqlCommand`. Internamente, isso cria um objeto <xref:Microsoft.Data.Sql.SqlNotificationRequest> e o associa ao objeto Command, conforme necessário. Essa solicitação de notificação contém um identificador interno que identifica exclusivamente esse `SqlDependency` objeto. Ele também inicia o ouvinte de cliente se ele ainda não estiver ativo.

4. Assine um manipulador de eventos para o evento `OnChange` do objeto `SqlDependency`.

5. Execute o comando usando qualquer um dos métodos `Execute` do objeto `SqlCommand`. Como o comando está associado ao objeto de notificação, o servidor reconhece que ele deve gerar uma notificação e as informações da fila apontarão para a fila de dependências.

6. Pare a conexão `SqlDependency` com o servidor.

Se qualquer usuário alterar posteriormente os dados subjacentes, Microsoft SQL Server detectar que há uma notificação pendente para tal alteração e posta uma notificação que é processada e encaminhada ao cliente por meio do `SqlConnection` subjacente que foi criado pelo chamando `SqlDependency.Start`. O ouvinte de cliente recebe a mensagem de invalidação. Em seguida, o ouvinte de cliente localiza o objeto de `SqlDependency` associado e aciona o evento `OnChange`.

O fragmento de código a seguir mostra o padrão de design que você usaria para criar um aplicativo de exemplo.

```csharp
void Initialization()
{
    // Create a dependency connection.
    SqlDependency.Start(connectionString, queueName);
}

void SomeMethod()
{
    // Assume connection is an open SqlConnection.

    // Create a new SqlCommand object.
    using (SqlCommand command=new SqlCommand(
        "SELECT ShipperID, CompanyName, Phone FROM dbo.Shippers",
        connection))
    {

        // Create a dependency and associate it with the SqlCommand.
        SqlDependency dependency=new SqlDependency(command);
        // Maintain the reference in a class member.

        // Subscribe to the SqlDependency event.
        dependency.OnChange+=new
           OnChangeEventHandler(OnDependencyChange);

        // Execute the command.
        using (SqlDataReader reader = command.ExecuteReader())
        {
            // Process the DataReader.
        }
    }
}

// Handler method
void OnDependencyChange(object sender,
   SqlNotificationEventArgs e )
{
  // Handle the event (for example, invalidate this cache entry).
}

void Termination()
{
    // Release the dependency.
    SqlDependency.Stop(connectionString, queueName);
}
```

## <a name="next-steps"></a>Próximas etapas
- [Notificações de consulta no SQL Server](query-notifications-sql-server.md)
