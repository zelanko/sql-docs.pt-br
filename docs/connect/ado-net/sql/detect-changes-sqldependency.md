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
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 90b11516e9fa8ed993792bfec2a77757249b696d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "78896986"
---
# <a name="detecting-changes-with-sqldependency"></a>Detectando alterações com SqlDependency

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Um objeto <xref:Microsoft.Data.SqlClient.SqlDependency> pode ser associado a um <xref:Microsoft.Data.SqlClient.SqlCommand> para detectar quando os resultados da consulta são diferentes dos recuperados originalmente. Você também pode atribuir um delegado ao evento `OnChange`, que será acionado quando os resultados forem alterados para um comando associado. Antes de executar o comando, você deve associar o <xref:Microsoft.Data.SqlClient.SqlDependency> a ele. A propriedade `HasChanges` do <xref:Microsoft.Data.SqlClient.SqlDependency> também pode ser usada para determinar se os resultados da consulta foram alterados desde que os dados foram recuperados pela primeira vez.

## <a name="security-considerations"></a>Considerações de segurança

A infraestrutura de dependência depende de um <xref:Microsoft.Data.SqlClient.SqlConnection> que é aberto quando <xref:Microsoft.Data.SqlClient.SqlDependency.Start%2A> é chamado para receber notificações de que os dados subjacentes foram alterados para um determinado comando. A capacidade de um cliente iniciar a chamada para `SqlDependency.Start` é controlada por meio do uso de <xref:Microsoft.Data.SqlClient.SqlClientPermission> e de atributos de segurança de acesso do código. Para obter mais informações, confira [Habilitar notificações de consulta](enable-query-notifications.md).

### <a name="example"></a>Exemplo

As seguintes etapas ilustram como declarar uma dependência, executar um comando e receber uma notificação quando o conjunto de resultados for alterado:

1. Inicia uma conexão `SqlDependency` com o servidor.

2. Crie objetos <xref:Microsoft.Data.SqlClient.SqlConnection> e <xref:Microsoft.Data.SqlClient.SqlCommand> para se conectar ao servidor e definir uma instrução Transact-SQL.

3. Crie um objeto `SqlDependency` ou use um existente e associe-o ao objeto `SqlCommand`. Internamente, isso cria um objeto <xref:Microsoft.Data.Sql.SqlNotificationRequest> e o associa ao objeto de comando, conforme necessário. Essa solicitação de notificação contém um identificador interno que identifica exclusivamente esse objeto `SqlDependency`. Ele também iniciará o ouvinte de cliente se ainda não estiver ativo.

4. Assine um manipulador de eventos para o evento `OnChange` do objeto `SqlDependency`.

5. Execute o comando usando qualquer um dos métodos `Execute` do objeto `SqlCommand`. Já que o comando está associado ao objeto de notificação, o servidor reconhece que ele precisa gerar uma notificação e as informações da fila apontarão para a fila de dependências.

6. Interrompa a conexão de `SqlDependency` com o servidor.

Se qualquer usuário alterar posteriormente os dados subjacentes, o Microsoft SQL Server detectará a existência de uma notificação pendente para tal alteração e postará uma notificação que será processada e encaminhada ao cliente por meio do `SqlConnection` subjacente, criado por uma chamada a `SqlDependency.Start`. O ouvinte de cliente recebe a mensagem de invalidação. Em seguida, o ouvinte de cliente localiza o objeto `SqlDependency` associado e aciona o evento `OnChange`.

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
