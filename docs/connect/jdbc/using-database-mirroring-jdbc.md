---
title: Como usar o espelhamento de banco de dados (JDBC) | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4ff59218-0d3b-4274-b647-9839c4955865
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e0de521e6ef913d27a020cc76f1dc6de00d0f409
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026431"
---
# <a name="using-database-mirroring-jdbc"></a>Como usar o espelhamento de banco de dados (JDBC)

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

O espelhamento de banco de dados é uma solução de software destinada principalmente a aumentar a disponibilidade do banco de dados e a redundância dos dados. O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece suporte implícito ao espelhamento de banco de dados, de modo que, depois que ele é configurado para o banco de dados, o desenvolvedor não precisa escrever nenhum código nem executar nenhuma outra ação.

O espelhamento de banco de dados, que é implementado para cada banco de dados, mantém uma cópia de um banco de dados de produção do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um servidor em espera. Esse servidor é um servidor em espera ativa ou passiva, dependendo da configuração e do estado da sessão de espelhamento de banco de dados. Um servidor em espera ativa dá suporte a um failover rápido sem perda de transações confirmadas, e um servidor em espera passiva dá suporte ao serviço de imposição (com possível perda de dados).

O banco de dados de produção é chamado de banco de dados _principal_, e a cópia em espera é chamada de banco de dados _espelho_. O banco de dados principal e o banco de dados espelho devem residir em instâncias separadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (instâncias do servidor) e, se possível, em computadores separados.

A instância do servidor de produção, chamada de servidor principal, se comunica com a instância do servidor em espera, chamada de servidor espelho. Os servidores principal e espelho atuam como parceiros em uma sessão de espelhamento de banco de dados. Se o servidor principal falhar, o servidor espelho poderá transformar seu banco de dados no banco de dados principal por meio de um processo chamado _failover_. Por exemplo, Parceiro_A e Parceiro_B são dois servidores parceiros, com o banco de dados principal inicialmente no Parceiro_A como servidor principal e o banco de dados espelho residindo no Parceiro_B como o servidor espelho. Se o Parceiro_A ficar offline, o banco de dados no Parceiro_B pode fazer failover para se tornar o banco de dados principal atual. Quando o Parceiro_A ingressar novamente na sessão de espelhamento, ele se tornará o servidor espelho e seu banco de dados se tornará o banco de dados espelho.

Caso o servidor do Parceiro_A seja danificado de forma irreparável, um servidor do Parceiro_C poderá ser colocado online para agir como o servidor espelho do Parceiro_B, que passa a ser o servidor principal. Porém, nesse cenário, o aplicativo cliente deverá incluir lógica de programação para assegurar que as propriedades de cadeia de conexão sejam atualizadas com os novos nomes de servidor usados na configuração de espelhamento de banco de dados. Caso contrário, poderá ocorrer falha na conexão com os servidores.

Configurações alternativas de espelhamento de banco de dados oferecem diferentes níveis de desempenho e segurança de dados, e dão suporte a diversas formas de failover. Para obter mais informações, veja "Visão geral do espelhamento de banco de dados" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

## <a name="programming-considerations"></a>Considerações sobre programação

Quando o servidor do banco de dados principal falhar, o aplicativo cliente receberá erros em resposta a chamadas API, o que indica que a conexão com o banco de dados foi interrompida. Quando isso acontece, todas as alterações não confirmadas feitas no banco de dados são perdidas e a transação atual é revertida. Nesse caso, o aplicativo deve fechar a conexão (ou liberar o objeto de fonte de dados) e tentar reabri-la. Ao ser estabelecida, a nova conexão é redirecionada, de forma transparente, ao banco de dados espelho, que agora age como o servidor principal, sem que o cliente precise modificar a cadeia de conexão ou o objeto de fonte de dados.

Quando uma conexão é estabelecida inicialmente, o servidor principal envia a identidade de seu parceiro de failover ao cliente que será usado quando ocorrer um failover. Quando um aplicativo tenta estabelecer uma conexão inicial com um servidor principal falho, o cliente não sabe a identidade do parceiro de failover. Para que os clientes tenham a oportunidade de lidar com esse cenário, a propriedade de cadeia de conexão failoverPartner e, opcionalmente, o método de fonte de dados [setFailoverPartner](../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md) permitem ao cliente especificar a identidade do parceiro de failover por sua própria conta. A propriedade do cliente é usada apenas nesse cenário; se o servidor principal estiver disponível, ela não será usada.

> [!NOTE]  
> Quando uma propriedade failoverPartner é especificada na cadeia de conexão ou com um objeto de fonte de dados, a propriedade databaseName também deve ser definida; caso contrário, uma exceção será lançada. Se as propriedades failoverPartner e databaseName não forem especificadas explicitamente, o aplicativo não tentará fazer failover quando ocorrer falha no servidor de banco de dados principal. Em outras palavras, o redirecionamento transparente só funcionará para conexões que especifiquem explicitamente failoverPartner e databaseName. Para obter mais informações sobre FailoverPartner foi e outras propriedades de cadeia de conexão, consulte [definindo as propriedades de conexão](../../connect/jdbc/setting-the-connection-properties.md).

Se o servidor do parceiro de failover fornecido pelo cliente não se referir a um servidor que funciona como um parceiro de failover para o banco de dados especificado, e se o servidor/banco de dados referenciado estiver em uma disposição de espelhamento, a conexão será recusada pelo servidor. Embora a classe [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) forneça o método [getFailoverPartner](../../connect/jdbc/reference/getfailoverpartner-method-sqlserverdatasource.md), esse método só retorna o nome do parceiro de failover especificado na cadeia de conexão ou no método setFailoverPartner. Para recuperar o nome do parceiro de failover real que está em uso no momento, use a seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)]:

```sql
SELECT m.mirroring_role_DESC, m.mirroring_state_DESC,  
m.mirroring_partner_instance FROM sys.databases as db,  
sys.database_mirroring AS m WHERE db.name = 'MirroringDBName'  
AND db.database_id = m.database_id  
```

> [!NOTE]  
> Você precisará alterar essa instrução para usar o nome do seu banco de dados de espelhamento.

Considere o armazenamento em cache das informações do parceiro para atualizar a cadeia de conexão ou crie uma estratégia de repetição em caso de falha da primeira tentativa de estabelecer uma conexão.

## <a name="example"></a>Exemplo

No exemplo a seguir, primeiro é feita uma tentativa de conectar ao servidor principal. Se isso falhar e uma exceção for lançada, será feita uma tentativa de conectar ao servidor espelho, que pode ter sido elevado a novo servidor principal. Observe o uso da propriedade failoverPartner na cadeia de conexão.

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

public class ClientFailover {
    public static void main(String[] args) {

        String connectionUrl = "jdbc:sqlserver://serverA:1433;"
                + "databaseName=AdventureWorks;integratedSecurity=true;"
                + "failoverPartner=serverB";

        // Establish the connection to the principal server.
        try (Connection con = DriverManager.getConnection(connectionUrl);
                Statement stmt = con.createStatement();) {
            System.out.println("Connected to the principal server.");

            // Note that if a failover of serverA occurs here, then an
            // exception will be thrown and the failover partner will
            // be used in the first catch block below.

            // Execute a SQL statement that inserts some data.

            // Note that the following statement assumes that the
            // TestTable table has been created in the AdventureWorks
            // sample database.
            stmt.executeUpdate("INSERT INTO TestTable (Col2, Col3) VALUES ('a', 10)");
        }
        catch (SQLException se) {
            System.out.println("Connection to principal server failed, " + "trying the mirror server.");
            // The connection to the principal server failed,
            // try the mirror server which may now be the new
            // principal server.
            try (Connection con = DriverManager.getConnection(connectionUrl);
                    Statement stmt = con.createStatement();) {
                System.out.println("Connected to the new principal server.");
                stmt.executeUpdate("INSERT INTO TestTable (Col2, Col3) VALUES ('a', 10)");
            }
            // Handle any errors that may have occurred.
            catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}
```

## <a name="see-also"></a>Confira também

[Conectando ao SQL Server com o JDBC Driver](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)
