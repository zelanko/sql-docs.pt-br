---
title: Sintaxe de cadeia de conexão
description: Saiba mais sobre a sintaxe das cadeias de conexão no Provedor de Dados Microsoft SqlClient para SQL Server. A sintaxe de cada provedor é documentada na propriedade ConnectionString.
ms.date: 11/13/2020
ms.assetid: 0977aeee-04d1-4cce-bbed-750c77fce06e
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: f61b867b70825595a012b2167d2c63b13409a8e2
ms.sourcegitcommit: 0c0e4ab90655dde3e34ebc08487493e621f25dda
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96442819"
---
# <a name="connection-string-syntax"></a>Sintaxe de cadeia de conexão

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

O <xref:Microsoft.Data.SqlClient> tem um objeto `Connection` que herda de <xref:System.Data.Common.DbConnection>, bem como uma propriedade <xref:System.Data.Common.DbConnection.ConnectionString%2A> específica do provedor. A sintaxe da cadeia de conexão específica para o provedor SqlClient está documentada na propriedade `ConnectionString`. Para obter mais informações sobre a sintaxe da cadeia de conexão, consulte <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A>.

## <a name="connection-string-builders"></a>Construtores de cadeia de conexão

 O Provedor de Dados Microsoft SqlClient para SQL Server introduziu o construtor de cadeias de conexão a seguir.

- <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder>

Os construtores de cadeia de conexão permitem que você construa cadeias de conexão sintaticamente válidas em tempo de execução, para que você não tenha que manualmente concatenar os valores de cadeia de conexão no seu código. Para obter mais informações, confira [Construtores de cadeias de conexão](connection-string-builders.md).

## <a name="windows-authentication"></a>Autenticação do Windows

Recomendamos o uso da Autenticação do Windows (às vezes chamada de *segurança integrada*) para se conectar a fontes de dados que dão suporte a ela. A tabela a seguir mostra a sintaxe da Autenticação do Windows usada com o Provedor de Dados Microsoft SqlClient para SQL Server.

|Provedor|Syntax|  
|--------------|------------|  
|`SqlClient`|`Integrated Security=true;`<br /><br /> `-- or --`<br /><br /> `Integrated Security=SSPI;`|  

## <a name="sqlclient-connection-strings"></a>Cadeias de conexão do SqlClient

A sintaxe para uma cadeia de conexão <xref:Microsoft.Data.SqlClient.SqlConnection> está documentada na propriedade <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A?displayProperty=nameWithType>. Você pode usar a propriedade <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A> para obter ou definir uma cadeia de conexão para um banco de dados do SQL Server. As palavras-chave da cadeia de conexão também são mapeadas para as propriedades no <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder>.

> [!IMPORTANT]
> A configuração padrão para a palavra-chave `Persist Security Info` é `false`. Configurá-lo como `true` ou `yes` permite informações confidenciais de segurança, incluindo a identificação de usuário e a senha, para serem obtidas da conexão depois que ela tiver sido aberta. Mantenha `Persist Security Info` definida como `false` para garantir que uma fonte não confiável não tenha acesso a informações confidenciais da cadeia de conexão.

### <a name="windows-authentication-with-sqlclient"></a>Autenticação do Windows com SqlClient

Cada uma das formas de sintaxe a seguir usa a Autenticação do Windows para se conectar ao banco de dados **AdventureWorks** em um servidor local.

```csharp  
"Persist Security Info=False;Integrated Security=true;  
    Initial Catalog=AdventureWorks;Server=MSSQL1"  
"Persist Security Info=False;Integrated Security=SSPI;  
    database=AdventureWorks;server=(local)"  
"Persist Security Info=False;Trusted_Connection=True;  
    database=AdventureWorks;server=(local)"  
```  

### <a name="sql-server-authentication-with-sqlclient"></a>Autenticação do SQL Server com SqlClient

A Autenticação do Windows é preferencial para se conectar ao SQL Server. No entanto, se a Autenticação do SQL Server for necessária, use a seguinte sintaxe para especificar um nome de usuário e uma senha. Nesse exemplo, os asteriscos são usados para representar um nome de usuário e uma senha válidos.

```csharp  
"Persist Security Info=False;User ID=*****;Password=*****;Initial Catalog=AdventureWorks;Server=MySqlServer"  
```  

Quando você se conectar ao Banco de Dados SQL do Azure ou ao Azure Synapse Analytics e fornecer um logon no formato `user@servername`, verifique se o valor `servername` no logon corresponde ao valor fornecido para `Server=`.

> [!NOTE]
> A autenticação do Windows tem precedência sobre logons do SQL Server. Se você especificar Integrated Security=true assim como um nome de usuário e uma senha, o nome de usuário e a senha serão ignorados e a autenticação do Windows será usada.

### <a name="connect-to-a-named-instance-of-sql-server"></a>Conectar-se a uma instância nomeada do SQL Server

Para se conectar a uma instância nomeada do SQL Server, use a sintaxe *server name\instance name*.

```csharp  
"Data Source=MySqlServer\MSSQL1;"  
```  

Você também pode definir a propriedade <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.DataSource%2A> de `SqlConnectionStringBuilder` para o nome da instância ao criar uma cadeia de conexão. A propriedade <xref:Microsoft.Data.SqlClient.SqlConnection.DataSource%2A> de um objeto <xref:Microsoft.Data.SqlClient.SqlConnection> é somente leitura.

### <a name="type-system-version-changes"></a>Alterações de versão do sistema de tipos

A palavra-chave `Type System Version` em um <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A?displayProperty=nameWithType> especifica a representação do lado do cliente de tipos do SQL Server. Consulte <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A?displayProperty=nameWithType> para obter mais informações sobre a palavra-chave `Type System Version`.

## <a name="connecting-and-attaching-to-sql-server-express-user-instances"></a>Conectando e anexando a instâncias de usuário do SQL Server Express

As instâncias de usuário são um recurso no SQL Server Express. Elas permitem que um usuário que esteja executando uma conta local do Windows com menos privilégios anexe e execute um banco de dados do SQL Server sem exigir privilégios administrativos. Uma instância de usuário é executada com as credenciais do Windows do usuário, não como um serviço.

Para obter mais informações sobre como trabalhar com instâncias de usuário, confira [Instâncias de usuário do SQL Server Express](./sql/sql-server-express-user-instances.md).

## <a name="using-trustservercertificate"></a>Usando TrustServerCertificate

A palavra-chave `TrustServerCertificate` é válida somente ao se conectar a uma instância do SQL Server com um certificado válido. Quando `TrustServerCertificate` for definida como `true`, a camada de transporte usará TLS/SSL para criptografar o canal, deixando de passar pela cadeia de certificado para validar a confiança.

```csharp  
"TrustServerCertificate=true;"
```  

> [!NOTE]
> Se `TrustServerCertificate` estiver definido como `true` e a criptografia estiver ativada, o nível de criptografia especificado no servidor será usado mesmo que `Encrypt` esteja definido como `false` na cadeia de conexão. A conexão falhará se isso for feito de outra maneira.

### <a name="enabling-encryption"></a>Habilitando a criptografia

Para habilitar a criptografia quando um certificado não tiver sido provisionado no servidor, as opções **Forçar Criptografia de Protocolo** e **Confiar no Certificado do Servidor** devem ser definidas no SQL Server Configuration Manager. Neste caso, a criptografia usará um certificado do servidor autoassinado sem validação, se nenhum certificado verificável tiver sido provisionado no servidor.

As configurações do aplicativo não podem reduzir o nível de segurança configurado no SQL Server, mas podem opcionalmente reforçá-lo. Um aplicativo pode solicitar a criptografia definindo as palavras-chave `TrustServerCertificate` e `Encrypt` como `true`, garantindo que a criptografia ocorra mesmo quando um certificado do servidor não tiver sido provisionado e **Forçar Criptografia de Protocolo** não estiver configurado para o cliente. No entanto, se `TrustServerCertificate` não estiver ativado na configuração do cliente, um certificado do servidor provisionado ainda será necessário.

A tabela a seguir descreve todos os casos.

|Configuração do cliente Forçar Criptografia de Protocolo|Configuração do cliente Confiar em Certificado do Servidor|Criptografar/Usar criptografia para a cadeia de conexão/atributo de dados|Cadeia de conexão/atributo do Certificado do Servidor de Confiança|Result|  
|----------------------------------------------|---------------------------------------------|-------------------------------------------------------------------|-----------------------------------------------------------|------------|  
|Não|N/D|Não (padrão)|Ignored|Não ocorre criptografia.|  
|Não|N/D|Sim|Não (padrão)|A criptografia só ocorrerá se houver um certificado de servidor verificável; caso contrário, a tentativa de conexão falhará.|  
|Não|N/D|Sim|Sim|A criptografia sempre ocorre, mas pode usar um certificado do servidor autoassinado.|  
|Sim|Não|Ignored|Ignored|A criptografia só ocorrerá se houver um certificado do servidor verificável; caso contrário, a tentativa de conexão falhará.|  
|Sim|Sim|Não (padrão)|Ignored|A criptografia sempre ocorre, mas pode usar um certificado do servidor autoassinado.|  
|Sim|Sim|Sim|Não (padrão)|A criptografia só ocorrerá se houver um certificado do servidor verificável; caso contrário, a tentativa de conexão falhará.|  
|Sim|Sim|Sim|Sim|A criptografia sempre ocorre, mas pode usar um certificado do servidor autoassinado.|  

Para obter mais informações, confira [Usando criptografia sem validação](/sql/relational-databases/native-client/features/using-encryption-without-validation).

## <a name="see-also"></a>Confira também

- [Cadeias de conexão](connection-strings.md)
- [Conectar-se a fontes de dados](connecting-to-data-source.md)
