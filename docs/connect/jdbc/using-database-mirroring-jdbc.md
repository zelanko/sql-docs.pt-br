---
title: Usando o banco de dados de espelhamento (JDBC) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4ff59218-0d3b-4274-b647-9839c4955865
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7528a85cd8e2eb258a89e6d7971ce0f80fa90258
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32852681"
---
# <a name="using-database-mirroring-jdbc"></a>Usando o espelhamento de banco de dados (JDBC)
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  O espelhamento de banco de dados é uma solução de software destinada principalmente a aumentar a disponibilidade do banco de dados e a redundância dos dados. O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece suporte implícito ao espelhamento de banco de dados, de forma que o desenvolvedor não precisa escrever nenhum código nem executar qualquer outra ação quando ele foi configurado para o banco de dados.  
  
 Banco de dados de espelhamento, que é implementado em uma base por banco de dados, mantém uma cópia de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados de produção em um servidor em espera. Esse servidor é um servidor em espera ativa ou passiva, dependendo da configuração e do estado da sessão de espelhamento de banco de dados. Um servidor em espera ativa dá suporte a um failover rápido sem perda de transações confirmadas, e um servidor em espera passiva dá suporte ao serviço de imposição (com possível perda de dados).  
  
 O banco de dados de produção é chamado de *principal* banco de dados e a cópia em espera é chamada de *espelho* banco de dados. O banco de dados principal e o banco de dados espelho devem residir em instâncias separadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] (instâncias de servidor), e eles devem residir em computadores separados, se possível.  
  
 A instância do servidor de produção, chamada de servidor principal, se comunica com a instância do servidor em espera, chamada de servidor espelho. Os servidores principal e espelho atuam como parceiros em uma sessão de espelhamento de banco de dados. Se o servidor principal falhar, o servidor espelho poderá transformar seu banco de dados no banco de dados principal por meio de um processo chamado *failover*. Por exemplo, Parceiro_A e Parceiro_B são dois servidores parceiros, com o banco de dados principal inicialmente no Parceiro_A como servidor principal e o banco de dados espelho residindo no Parceiro_B como o servidor espelho. Se o Parceiro_A ficar offline, o banco de dados no Parceiro_B pode fazer failover para se tornar o banco de dados principal atual. Quando o Parceiro_A ingressar novamente na sessão de espelhamento, ele se tornará o servidor espelho e seu banco de dados se tornará o banco de dados espelho.  
  
 Caso o servidor do Parceiro_A seja danificado de forma irreparável, um servidor do Parceiro_C poderá ser colocado online para agir como o servidor espelho do Parceiro_B, que passa a ser o servidor principal. Porém, nesse cenário, o aplicativo cliente deverá incluir lógica de programação para assegurar que as propriedades de cadeia de conexão sejam atualizadas com os novos nomes de servidor usados na configuração de espelhamento de banco de dados. Caso contrário, poderá ocorrer falha na conexão com os servidores.  
  
 Configurações alternativas de espelhamento de banco de dados oferecem diferentes níveis de desempenho e segurança de dados, e dão suporte a diversas formas de failover. Para obter mais informações, consulte "Visão geral do banco de dados de espelhamento" [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Manuais Online.  
  
## <a name="programming-considerations"></a>Considerações sobre programação  
 Quando o servidor do banco de dados principal falhar, o aplicativo cliente receberá erros em resposta a chamadas API, o que indica que a conexão com o banco de dados foi interrompida. Quando isso acontece, todas as alterações não confirmadas feitas no banco de dados são perdidas e a transação atual é revertida. Nesse caso, o aplicativo deve fechar a conexão (ou liberar o objeto de fonte de dados) e tentar reabri-la. Ao ser estabelecida, a nova conexão é redirigida, de forma transparente, ao banco de dados espelho, que agora age como o servidor principal, sem que o cliente precise modificar a cadeia de conexão ou o objeto de fonte de dados.  
  
 Quando uma conexão é estabelecida inicialmente, o servidor principal envia a identidade de seu parceiro de failover ao cliente que será usado quando ocorrer um failover. Quando um aplicativo tenta estabelecer uma conexão inicial com um servidor principal falho, o cliente não sabe a identidade do parceiro de failover. Para permitir que os clientes a oportunidade de lidar com esse cenário, a propriedade de cadeia de conexão failoverPartner e, opcionalmente, o [setFailoverPartner](../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md) método de fonte de dados permite que o cliente especifique a identidade do failover parceiro por conta própria. A propriedade do cliente é usada apenas nesse cenário; se o servidor principal estiver disponível, ela não será usada.  
  
> [!NOTE]  
>  Quando uma propriedade failoverPartner é especificada na cadeia de conexão ou com um objeto de fonte de dados, a propriedade databaseName também deve ser definida; caso contrário, uma exceção será lançada. Se as propriedades failoverPartner e databaseName não forem especificadas explicitamente, o aplicativo não tentará fazer failover quando ocorrer falha no servidor de banco de dados principal. Em outras palavras, o redirecionamento transparente só funcionará para conexões que especifiquem explicitamente failoverPartner e databaseName. Para obter mais informações sobre failoverPartner e outras propriedades de cadeia de caracteres de conexão, consulte [definindo as propriedades de Conexão](../../connect/jdbc/setting-the-connection-properties.md).  
  
 Se o servidor do parceiro de failover fornecido pelo cliente não se referir a um servidor que funciona como um parceiro de failover para o banco de dados especificado, e se o servidor/banco de dados referenciado estiver em uma disposição de espelhamento, a conexão será recusada pelo servidor. Embora o [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) classe fornece a [getFailoverPartner](../../connect/jdbc/reference/getfailoverpartner-method-sqlserverdatasource.md) método, esse método só retorna o nome do parceiro de failover especificado na cadeia de conexão ou o método setFailoverPartner. Para recuperar o nome do parceiro de failover real que está sendo usado, use a seguinte [!INCLUDE[tsql](../../includes/tsql_md.md)] instrução:  
  
```  
SELECT m.mirroring_role_DESC, m.mirroring_state_DESC,  
m.mirroring_partner_instance FROM sys.databases as db,  
sys.database_mirroring AS m WHERE db.name = 'MirroringDBName'  
AND db.database_id = m.database_id  
```  
  
> [!NOTE]  
>  Você precisará alterar essa instrução para usar o nome do seu banco de dados de espelhamento.  
  
 Considere o armazenamento em cache das informações do parceiro para atualizar a cadeia de conexão ou crie uma estratégia de repetição em caso de falha da primeira tentativa de estabelecer uma conexão.  
  
## <a name="example"></a>Exemplo  
 No exemplo a seguir, primeiro é feita uma tentativa de conectar ao servidor principal. Se isso falhar e uma exceção for lançada, será feita uma tentativa de conectar ao servidor espelho, que pode ter sido elevado a novo servidor principal. Observe o uso da propriedade failoverPartner na cadeia de conexão.  
  
```  
import java.sql.*;  
  
public class clientFailover {  
  
   public static void main(String[] args) {  
  
      // Create a variable for the connection string.  
      String connectionUrl = "jdbc:sqlserver://serverA:1433;" +  
         "databaseName=AdventureWorks;integratedSecurity=true;" +  
         "failoverPartner=serverB";  
  
      // Declare the JDBC objects.  
      Connection con = null;  
      Statement stmt = null;  
  
      try {  
         // Establish the connection to the principal server.  
         Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
         con = DriverManager.getConnection(connectionUrl);  
         System.out.println("Connected to the principal server.");  
  
         // Note that if a failover of serverA occurs here, then an  
         // exception will be thrown and the failover partner will  
         // be used in the first catch block below.  
  
         // Create and execute an SQL statement that inserts some data.  
         stmt = con.createStatement();  
  
         // Note that the following statement assumes that the   
         // TestTable table has been created in the AdventureWorks  
         // sample database.  
         stmt.executeUpdate("INSERT INTO TestTable (Col2, Col3) VALUES ('a', 10)");  
      }  
  
      // Handle any errors that may have occurred.  
      catch (SQLException se) {  
         try {  
            // The connection to the principal server failed,  
            // try the mirror server which may now be the new  
            // principal server.  
            System.out.println("Connection to principal server failed, " +  
            "trying the mirror server.");  
            con = DriverManager.getConnection(connectionUrl);  
            System.out.println("Connected to the new principal server.");  
            stmt = con.createStatement();  
            stmt.executeUpdate("INSERT INTO TestTable (Col2, Col3) VALUES ('a', 10)");  
         }  
         catch (Exception e) {  
            e.printStackTrace();  
         }  
      }  
      catch (Exception e) {  
         e.printStackTrace();  
      }  
      // Close the JDBC objects.  
      finally {  
         if (stmt != null) try { stmt.close(); } catch(Exception e) {}  
         if (con != null) try { con.close(); } catch(Exception e) {}  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Conectando ao SQL Server com o JDBC Driver](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
