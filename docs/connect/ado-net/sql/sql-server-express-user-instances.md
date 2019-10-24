---
title: Instâncias de usuário do SQL Server Express
description: Descreve o suporte para SQL Server Express instâncias de usuário.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 00c12376-cb26-4317-86ad-e6e9c089be57
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 3b3ac1e395cc1240693ca0dc27324766964e0cfa
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452014"
---
# <a name="sql-server-express-user-instances"></a>Instâncias de usuário do SQL Server Express

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

O Microsoft SQL Server Express Edition (SQL Server Express) dá suporte ao recurso de instância de usuário, que só está disponível ao usar o Provedor de Dados do Microsoft SqlClient para SQL Server. Uma instância de usuário é uma instância separada do Mecanismo de Banco de Dados de SQL Server Express que é gerada por uma instância pai. As instâncias de usuário permitem que os usuários que não são administradores em seus computadores locais se conectem e se conectem a bancos de dados do SQL Server Express. Cada instância é executada sob o contexto de segurança do usuário individual, em uma base de uma instância por usuário.  
  
## <a name="user-instance-capabilities"></a>Recursos da instância do usuário  
As instâncias de usuário são úteis para usuários que executam o Windows sob uma conta de usuário com privilégios mínimos (LUA), pois cada usuário SQL Server tem privilégios de `sysadmin` (administrador do sistema) na instância em execução no computador sem a necessidade de ser executado como um Windows administrador também. O software em execução em uma instância de usuário com permissões limitadas não pode fazer alterações em todo o sistema, pois a instância do SQL Server Express está sendo executada sob a conta do Windows não administrador do usuário, não como um serviço. Cada instância de usuário é isolada de sua instância pai e de qualquer outra instância de usuário que estiver em execução no mesmo computador. Os bancos de dados em execução em uma instância de usuário são abertos somente no modo de usuário único e não é possível que vários usuários se conectem a bancos de dados em execução em uma instância de usuário. A replicação e as consultas distribuídas também são desabilitadas para instâncias de usuário.  
  
Para obter mais informações, consulte "instâncias de usuário" em Manuais Online do SQL Server.  
  
> [!NOTE]
>  As instâncias de usuário não são necessárias para os usuários que já são administradores em seus próprios computadores ou para cenários que envolvem vários usuários de banco de dados.  
  
## <a name="enabling-user-instances"></a>Habilitando instâncias de usuário  
Para gerar instâncias de usuário, uma instância pai do SQL Server Express deve estar em execução. As instâncias de usuário são habilitadas por padrão quando o SQL Server Express é instalado, e podem ser habilitadas ou desabilitadas explicitamente por um administrador do sistema que esteja executando o procedimento armazenado do sistema **sp_configure** na instância pai.  
  
```sql
-- Enable user instances.  
sp_configure 'user instances enabled','1'   
  
-- Disable user instances.  
sp_configure 'user instances enabled','0'  
```  
  
O protocolo de rede para instâncias de usuário deve ser pipes nomeados locais. Uma instância de usuário não pode ser iniciada em uma instância remota do SQL Server e não são permitidos logons do SQL Server.  
  
## <a name="connecting-to-a-user-instance"></a>Fazendo a conexão com uma instância de usuário  
As palavras-chave `User Instance` e `AttachDBFilename`<xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A> permitem que <xref:Microsoft.Data.SqlClient.SqlConnection> se conecte a uma instância de usuário. As instâncias de usuário também têm suporte nas propriedades <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder> `UserInstance` e `AttachDBFilename`.  
  
Observe o seguinte sobre a cadeia de conexão de exemplo mostrada abaixo:  
  
- A palavra-chave `Data Source` refere-se à instância pai do SQL Server Express que está gerando a instância do usuário. A instância padrão é .\sqlexpress.  
  
- `Integrated Security` está definido como `true`. Para se conectar a uma instância de usuário, a autenticação do Windows é necessária; Não há suporte para logons do SQL Server.  
  
- O `User Instance` é definido como `true`, que invoca uma instância de usuário. (O padrão é `false`.)  
  
- A palavra-chave da cadeia de conexão `AttachDbFileName` é usada para anexar o arquivo de banco de dados primário (. MDF), que deve incluir o nome do caminho completo. `AttachDbFileName` também corresponde às chaves "Propriedades estendidas" e "nome do arquivo inicial" em uma cadeia de conexão <xref:Microsoft.Data.SqlClient.SqlConnection>.  
  
- A cadeia de caracteres de substituição de `|DataDirectory|` incluída nos símbolos de pipe refere-se ao diretório de dados do aplicativo que abre a conexão e fornece um caminho relativo que indica o local dos arquivos. MDF e. ldf e de log. Se você quiser localizar esses arquivos em outro lugar, deverá fornecer o caminho completo para os arquivos.  
  
```console
Data Source=.\\SQLExpress;Integrated Security=true;  
User Instance=true;AttachDBFilename=|DataDirectory|\InstanceDB.mdf;  
Initial Catalog=InstanceDB;  
```  
  
> [!NOTE]
>  Você também pode usar as propriedades <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder> <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.UserInstance%2A> e <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.AttachDBFilename%2A> para criar uma cadeia de conexão em tempo de execução.  
  
### <a name="using-the-124datadirectory124-substitution-string"></a>Usando a &#124;cadeia de caracteres&#124; de substituição DataDirectory  
`DataDirectory` é usado em conjunto com `AttachDbFileName` para indicar um caminho relativo para um arquivo de dados, permitindo que os desenvolvedores criem cadeias de conexão baseadas em um caminho relativo para a fonte de dados em vez de serem necessários para especificar um caminho completo.  
  
O local físico que `DataDirectory` aponta para depende do tipo de aplicativo. Neste exemplo, o arquivo Northwind. MDF a ser anexado está localizado na pasta \app_data do aplicativo.  
  
```console
Data Source=.\\SQLExpress;Integrated Security=true;  
User Instance=true;  
AttachDBFilename=|DataDirectory|\app_data\Northwind.mdf;  
Initial Catalog=Northwind;  
```  
  
Quando `DataDirectory` é usado, o caminho do arquivo resultante não pode ser maior na estrutura de diretório do que o diretório apontado pela cadeia de caracteres de substituição. Por exemplo, se a `DataDirectory` totalmente expandida for C:\AppDirectory\app_data, a cadeia de conexão de exemplo mostrada acima funcionará porque está abaixo de c:\AppDirectory. No entanto, tentar especificar `DataDirectory` como `|DataDirectory|\..\data` resultará em um erro porque \data não é um subdiretório de \AppDirectory.  
  
Se a cadeia de conexão tiver uma cadeia de caracteres de substituição formatada incorretamente, uma <xref:System.ArgumentException> será lançada.  
  
> [!NOTE]
>  <xref:Microsoft.Data.SqlClient> resolve as cadeias de caracteres de substituição em caminhos completos no sistema de arquivos do computador local. Portanto, não há suporte para nomes de caminho de servidor remoto, HTTP e UNC. Uma exceção será lançada quando a conexão for aberta se o servidor não estiver localizado no computador local.  
  
Quando o <xref:Microsoft.Data.SqlClient.SqlConnection> é aberto, ele é redirecionado da instância de SQL Server Express padrão para uma instância iniciada em tempo de execução em execução na conta do chamador.  
  
> [!NOTE]
>  Pode ser necessário aumentar o valor <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionTimeout%2A>, pois as instâncias de usuário podem levar mais tempo para carregar do que instâncias regulares.  
  
O fragmento de código a seguir abre uma nova `SqlConnection`, exibe a cadeia de conexão na janela do console e fecha a conexão ao sair do bloco de código de `using`.  
  
```csharp  
private static void OpenSqlConnection()  
{  
    // Retrieve the connection string.  
    string connectionString = GetConnectionString();  
  
    using (SqlConnection connection =   
        new SqlConnection(connectionString))  
    {  
        connection.Open();  
        Console.WriteLine("ConnectionString: {0}",   
             connection.ConnectionString);  
    }  
}  
```  
  
> [!NOTE]
>  Não há suporte para instâncias de usuário no código Common Language Runtime (CLR) em execução dentro do SQL Server. Um <xref:System.InvalidOperationException> será gerado se `Open` for chamado em um <xref:Microsoft.Data.SqlClient.SqlConnection> que tenha `User Instance=true` na cadeia de conexão.  
  
## <a name="lifetime-of-a-user-instance-connection"></a>Tempo de vida de uma conexão de instância de usuário  
Diferentemente das versões de SQL Server executadas como um serviço, SQL Server Express instâncias não precisam ser iniciadas e interrompidas manualmente. Sempre que um usuário fizer logon e se conectar a uma instância de usuário, a instância do usuário será iniciada se ainda não estiver em execução. Os bancos de dados da instância do usuário têm a opção `AutoClose` definida para que o banco de dados seja desligado automaticamente após um período de inatividade. O processo sqlservr. exe iniciado é mantido em execução por um período de tempo limite limitado após a última conexão com a instância ser fechada, portanto, não precisa ser reiniciada se outra conexão for aberta antes de o tempo limite expirar. A instância de usuário será desligada automaticamente se nenhuma nova conexão for aberta antes que esse período de tempo limite tenha expirado. Um administrador do sistema na instância pai pode definir a duração do período de tempo limite para uma instância de usuário usando **sp_configure** para alterar a opção de **tempo limite da instância do usuário** . O padrão é de 60 minutos.  
  
> [!NOTE]
>  Se `Min Pool Size` for usado na cadeia de conexão com um valor maior que zero, o pooler de conexão sempre manterá algumas conexões abertas e a instância do usuário não será desligada automaticamente.  
  
## <a name="how-user-instances-work"></a>Como as instâncias de usuário funcionam  
A primeira vez que uma instância de usuário é gerada para cada usuário, os bancos de dados do sistema **master** e **msdb** são copiados da pasta Dados de Modelo para um caminho no diretório local do repositório de dados do aplicativo do usuário para uso exclusivo pela instância de usuário. Normalmente, esse caminho é `C:\Documents and Settings\<UserName>\Local Settings\Application Data\Microsoft\Microsoft SQL Server Data\SQLEXPRESS`. Quando uma instância de usuário é iniciada, o **tempdb**, o log e os arquivos de rastreamento também são gravados neste diretório. Um nome é gerado para a instância, que tem a garantia de ser exclusivo para cada usuário.  
  
Por padrão, todos os membros do grupo Builtin\Users do Windows recebem permissões para se conectarem à instância local, bem como permissões de leitura e execução nos binários de SQL Server. Depois que as credenciais do usuário que está chamando a instância do usuário tiverem sido verificadas, esse usuário se tornará o `sysadmin` nessa instância. Somente a memória compartilhada é habilitada para instâncias de usuário, o que significa que somente as operações no computador local são possíveis.  
  
Os usuários devem receber permissões de leitura e gravação nos arquivos. MDF e. ldf especificados na cadeia de conexão.  
  
> [!NOTE]
>  Os arquivos. MDF e. ldf representam o banco de dados e os arquivos de log, respectivamente. Esses dois arquivos são um conjunto correspondente, portanto, é necessário tomar cuidado durante as operações de backup e restauração. O arquivo de banco de dados contém informações sobre a versão exata do arquivo de log e o banco de dados não será aberto se ele estiver acoplado ao arquivo de log errado.  
  
Para evitar a corrupção de dados, um banco de dado na instância do usuário é aberto com acesso exclusivo. Se duas instâncias de usuário diferentes compartilharem o mesmo banco de dados no mesmo computador, o usuário na primeira instância deverá fechar o banco de dados antes que ele possa ser aberto em uma segunda instância.  
  
## <a name="user-instance-scenarios"></a>Cenários de instância de usuário  
As instâncias de usuário fornecem aos desenvolvedores de aplicativos de banco de dados um SQL Server armazenamento que não depende de desenvolvedores com contas administrativas em seus computadores de desenvolvimento. As instâncias de usuário são baseadas no modelo de acesso/Jet, onde o aplicativo de banco de dados simplesmente se conecta a um arquivo, e o usuário tem automaticamente permissões completas em todos os objetos de banco de dados sem a necessidade de intervenção de um administrador de sistema para conceder permissões. Ele se destina a trabalhar em situações em que o usuário está executando sob uma conta de usuário com privilégios mínimos (LUA) e não tem privilégios administrativos no servidor ou no computador local, mas precisa criar objetos e aplicativos de banco de dados. As instâncias de usuário permitem que os usuários criem instâncias em tempo de execução que são executados sob o contexto de segurança do próprio usuário e não no contexto de segurança de um serviço de sistema mais privilegiado.  
  
> [!IMPORTANT]
>  As instâncias de usuário só devem ser usadas em cenários em que todos os aplicativos que o utilizam são totalmente confiáveis.  
  
Os cenários da instância do usuário incluem:  
  
- Qualquer aplicativo de usuário único em que o compartilhamento de dados não é necessário.  
  
- Implantação do ClickOnce. Se o .NET Framework 2,0 (ou posterior) ou o .NET Core 1,0 (ou posterior) e SQL Server Express já estiverem instalados no computador de destino, o pacote de instalação baixado como resultado de uma ação do ClickOnce pode ser instalado e usado por usuários que não são administradores. Observe que um administrador deve instalar SQL Server Express se isso fizer parte da instalação. Para obter mais informações, consulte [implantação do ClickOnce para Windows Forms](https://docs.microsoft.com/dotnet/framework/winforms/clickonce-deployment-for-windows-forms).
  
- Hospedagem de ASP.NET dedicada usando a autenticação do Windows. Uma única instância de SQL Server Express pode ser hospedada em uma intranet. O aplicativo se conecta usando a conta do Windows ASPNET, não usando a representação. As instâncias de usuário não devem ser usadas para cenários de Hospedagem de terceiros ou compartilhados, onde todos os aplicativos compartilharão a mesma instância de usuário e não permanecerão mais isolados uns dos outros.  
  
## <a name="next-steps"></a>Próximas etapas
- [SQL Server e ADO.NET](index.md)
