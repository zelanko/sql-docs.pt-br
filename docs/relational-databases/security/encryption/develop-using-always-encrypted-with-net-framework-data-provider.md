---
title: Always Encrypted com o Provedor de Dados .NET Framework
description: Saiba como desenvolver aplicativos .NET usando o recurso Always Encrypted do SQL Server.
ms.custom: seo-lt-2019
ms.date: 10/31/2019
ms.prod: sql
ms.prod_service: security, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
ms.assetid: 827e509e-3c4f-4820-aa37-cebf0f7bbf80
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3c442568ad7764ba0f9031a02a8080499555d26f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75558031"
---
# <a name="using-always-encrypted-with-the-net-framework-data-provider-for-sql-server"></a>Usando o Always Encrypted com o Provedor de Dados .NET Framework para SQL Server
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Este artigo fornece informações sobre como desenvolver aplicativos .NET usando o [Always Encrypted](always-encrypted-database-engine.md) ou o [Always Encrypted com enclaves seguros](always-encrypted-enclaves.md) e o [Provedor de Dados do .NET Framework para SQL Server](https://msdn.microsoft.com/library/kb9s9ks0(v=vs.110).aspx).

O Always Encrypted permite que os aplicativos cliente criptografem dados confidenciais e nunca revelem os dados nem as chaves de criptografia para o SQL Server ou o Banco de Dados SQL do Azure. Um driver habilitado para Always Encrypted, como o Provedor de Dados .NET Framework para SQL Server, consegue fazer isso criptografando e descriptografando de modo transparente dados confidenciais no aplicativo cliente. O driver determina automaticamente quais parâmetros de consulta correspondem às colunas de banco de dados confidenciais (protegidas com o Always Encrypted) e criptografa os valores desses parâmetros antes de passar os dados para o SQL Server ou o Banco de Dados SQL do Azure. Da mesma forma, o driver descriptografa de modo transparente os dados recuperados das colunas de banco de dados criptografadas nos resultados da consulta. Para obter mais informações, confira [Desenvolver aplicativos usando o Always Encrypted](always-encrypted-client-development.md) e [Desenvolver aplicativos usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-client-development.md).

## <a name="prerequisites"></a>Prerequisites

- Configure o Sempre Criptografado em seu banco de dados. Isso envolve o provisionamento de chaves do Sempre Criptografado e a configuração de criptografia de colunas de banco de dados selecionadas. Se você ainda não tiver um banco de dados com o Always Encrypted configurado, siga as instruções em [Introdução ao Always Encrypted](always-encrypted-database-engine.md#getting-started-with-always-encrypted).
- Verifique se a versão 4.6.1 ou posterior do .NET Framework está instalada no computador de desenvolvimento. Para obter detalhes, confira [.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2(v=vs.110).aspx). Você também precisa verificar se a versão 4.6 ou posterior do .NET Framework está configurada como a versão de destino do .NET Framework no ambiente de desenvolvimento. Se estiver usando o Visual Studio, veja [Como: direcionar uma versão do .NET Framework](https://msdn.microsoft.com/library/bb398202.aspx). 

> [!NOTE]
> O nível de suporte para o Sempre Criptografados varia em versões específicas do .NET Framework. Veja a seção de referência de API do Always Encrypted abaixo para obter detalhes.

## <a name="enabling-always-encrypted-for-application-queries"></a>Habilitando o Always Encrypted para consultas de aplicativo
A maneira mais fácil para habilitar a criptografia de parâmetros e a descriptografia dos resultados de consulta, tendo como destino as colunas criptografadas, é definir o valor da palavra-chave da cadeia de conexão de Configuração de Criptografia de Coluna como **habilitado**.

Veja a seguir o exemplo de uma cadeia de conexão que habilita o Sempre Criptografado:

```cs
string connectionString = "Data Source=server63; Initial Catalog=Clinic; Integrated Security=true; Column Encryption Setting=enabled";
SqlConnection connection = new SqlConnection(connectionString);
```

Veja a seguir um exemplo equivalente que usa a Propriedade SqlConnectionStringBuilder.ColumnEncryptionSetting.

```cs
SqlConnectionStringBuilder strbldr = new SqlConnectionStringBuilder();
strbldr.DataSource = "server63";
strbldr.InitialCatalog = "Clinic";
strbldr.IntegratedSecurity = true;
strbldr.ColumnEncryptionSetting = SqlConnectionColumnEncryptionSetting.Enabled;
SqlConnection connection = new SqlConnection(strbldr.ConnectionString);
```

O Sempre Criptografado também pode ser habilitado para consultas individuais. Veja a seção **Controlando o impacto no desempenho do Always Encrypted** abaixo.
Habilitar Always Encrypted não é suficiente para o êxito da criptografia ou descriptografia. Você também precisa garantir que:
- O aplicativo tem as permissões de banco de dados *VIEW ANY COLUMN MASTER KEY DEFINITION* e *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* , necessárias para acessar os metadados sobre as chaves do Always Encrypted no banco de dados. Para obter detalhes, veja a [seção Permissões em Always Encrypted (Mecanismo de Banco de Dados)](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_7).
- O aplicativo pode acessar a chave mestra de coluna que protege as chaves de criptografia de coluna, criptografando as colunas de banco de dados consultadas.

## <a name="enabling-always-encrypted-with-secure-enclaves"></a>Como habilitar o Always Encrypted com enclaves seguros

Começando na versão 4.7.2 do .NET Framework, o driver dá suporte ao [Always Encrypted com enclaves seguros](always-encrypted-enclaves.md). 

Para habilitar o uso do enclave ao se conectar com o [!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)] ou posterior, você precisa configurar seu aplicativo e o Provedor de Dados do .NET Framework para SQL Server para habilitar cálculos do enclave e o atestado do enclave. 

Para obter informações gerais sobre a função do driver de cliente nos cálculos de enclave e no atestado do enclave, confira [Desenvolver aplicativos usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-client-development.md). 

Para configurar seu aplicativo:

1. Integre o pacote NuGet [Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders](https://www.nuget.org/packages/Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders) ao seu aplicativo. O NuGet é uma biblioteca de provedores de enclave, implementando a lógica do lado do cliente para os protocolos de atestado e estabelecendo um canal seguro com um enclave seguro dentro do SQL Server.  
2. Atualize a configuração do aplicativo (por exemplo, em web.config ou app.config) para definir o mapeamento entre um tipo de enclave com que sua instância de [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] foi configurada (confira [Configurar o tipo de enclave para a Opção de Configuração de Servidor Always Encrypted](../../../database-engine/configure-windows/configure-column-encryption-enclave-type.md)). [!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)] dá suporte a enclaves do VBS e ao Serviço Guardião de Host para atestado. Portanto, você precisa mapear o tipo de enclave do VBS para a classe Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders.HostGuardianServiceEnclaveProvider do pacote NuGet. 
3. Habilite cálculos de enclave para uma conexão do seu aplicativo com o banco de dados definindo a palavra-chave da URL de Atestado de Enclave na cadeia de conexão para um ponto de extremidade de atestado. O valor da palavra-chave deve ser definido como o ponto de extremidade de atestado do servidor HGS, configurado em seu ambiente. 

Para obter um tutorial passo a passo, confira [Tutorial: Desenvolver um aplicativo .NET Framework usando o Always Encrypted com enclaves seguros](../tutorial-always-encrypted-enclaves-develop-net-framework-apps.md)

## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>Recuperando e modificando dados em colunas criptografadas

Depois de habilitar o Always Encrypted para consultas de aplicativo, é possível usar APIs padrão do ADO.NET (veja [Recuperando e modificando dados no ADO.NET](https://msdn.microsoft.com/library/ms254937(v=vs.110).aspx)) ou as APIs do [Provedor de Dados do .NET Framework para SQL Server](https://msdn.microsoft.com/library/kb9s9ks0(v=vs.110).aspx) , definidas no [Namespace System.Data.SqlClient](https://msdn.microsoft.com/library/system.data.sqlclient.aspx), para recuperar ou modificar dados em colunas de banco de dados criptografadas. Supondo que seu aplicativo tenha as permissões de banco de dados necessárias e que possa acessar a chave mestra de coluna, o Provedor de Dados do .NET Framework para SQL Server criptografará quaisquer parâmetros de consulta que se destinam a colunas criptografadas. Além disso, ele descriptografará os dados recuperados das colunas criptografadas, retornando valores de texto sem formatação de tipos do .NET, correspondentes aos tipos de dados do SQL Server definidos para as colunas no esquema de banco de dados.
Se o Sempre Criptografado não estiver habilitado, as consultas com parâmetros que se destinam a colunas criptografadas falharão. As consultas ainda podem recuperar dados de colunas criptografadas, desde que a consulta não tenha parâmetros que se destinam a colunas criptografadas. No entanto, o Provedor de Dados do .NET Framework para SQL Server não tentará descriptografar nenhum valor recuperado de colunas criptografadas e o aplicativo receberá os dados binários criptografados (como matrizes de bytes).

A tabela abaixo resume o comportamento das consultas, dependendo se o Always Encrypted está habilitado ou não:

|Característica da consulta | O Always Encrypted está habilitado e o aplicativo pode acessar as chaves e os metadados da chave|O Sempre Criptografado está habilitado e o aplicativo não pode acessar as chaves nem os metadados da chave | O Sempre Criptografado está desabilitado|
|:---|:---|:---|:---|
| Consultas com parâmetros que se destinam a colunas criptografadas. | Os valores de parâmetro são criptografados de modo transparente. | Erro | Erro|
| Consultas que recuperam dados de colunas criptografadas, sem parâmetros que se destinam a colunas criptografadas.| Os resultados das colunas criptografadas são descriptografados de modo transparente. O aplicativo recebe valores de texto sem formatação dos tipos de dados do .NET correspondentes aos tipos do SQL Server configurados para as colunas criptografadas. | Erro | Os resultados das colunas criptografadas não são descriptografados. O aplicativo recebe valores criptografados como matrizes de bytes (byte[]). 

Os exemplos a seguir ilustram como recuperar e modificar dados em colunas criptografadas. Os exemplos pressupõem a tabela de destino com o esquema abaixo. As colunas SSN e BirthDate estão criptografadas.


```sql
CREATE TABLE [dbo].[Patients]([PatientId] [int] IDENTITY(1,1), 
 [SSN] [char](11) COLLATE Latin1_General_BIN2 
 ENCRYPTED WITH (ENCRYPTION_TYPE = DETERMINISTIC, 
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256', 
 COLUMN_ENCRYPTION_KEY = CEK1) NOT NULL,
 [FirstName] [nvarchar](50) NULL,
 [LastName] [nvarchar](50) NULL, 
 [BirthDate] [date] 
 ENCRYPTED WITH (ENCRYPTION_TYPE = RANDOMIZED, 
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256', 
 COLUMN_ENCRYPTION_KEY = CEK1) NOT NULL
 PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY])
 GO
```

### <a name="inserting-data-example"></a>Inserindo um exemplo de dados

Este exemplo insere uma linha na tabela Pacientes. Observe o seguinte:
- Não há nada específico de criptografia no código de exemplo. O Provedor de Dados do .NET Framework para SQL Server detecta automaticamente e criptografa os parâmetros *paramSSN* e *paramBirthdate* que se destinam a colunas criptografadas. Isso torna a criptografia transparente para o aplicativo. 
- Os valores inseridos nas colunas de banco de dados, incluindo as colunas criptografadas, são passados como objetos [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) . Embora o uso de **SqlParameter** seja opcional ao enviar valores para colunas não criptografadas (mesmo que seja altamente recomendável, pois ajuda a prevenir a injeção de SQL), ele é necessário para valores que se destinam a colunas criptografadas. Se os valores inseridos nas colunas SSN ou BirthDate fossem passados como literais inseridos na instrução da consulta, a consulta falharia, pois o Provedor de Dados do .NET Framework para SQL Server não conseguiria determinar os valores nas colunas criptografadas de destino e, portanto, não criptografaria os valores. Como resultado, o servidor os rejeitaria como incompatíveis com as colunas criptografadas.
- O tipo de dados do parâmetro que se destina à coluna SSN é definido como uma cadeia de caracteres ANSI (não Unicode), que é mapeada para o tipo de dados char/varchar do SQL Server. Se o tipo do parâmetro fosse definido como uma cadeia de caracteres Unicode (String), que é mapeada para nchar/nvarchar, a consulta falharia, já que o Always Encrypted não dá suporte a conversões de valores nchar/nvarchar criptografados em valores char/varchar criptografados. Veja [Mapeamentos de tipos de dados do SQL Server](/dotnet/framework/data/adonet/sql-server-data-type-mappings) para obter informações sobre os mapeamentos de tipos de dados.
- O tipo de dados do parâmetro inserido na coluna BirthDate é configurado explicitamente para o tipo de dados do SQL Server de destino usando a [Propriedade SqlParameter.SqlDbType](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.sqldbtype.aspx), em vez de se basear no mapeamento implícito dos tipos do .NET para os tipos de dados do SQL Server aplicados ao usar a [Propriedade SqlParameter.DbType](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.dbtype.aspx). Por padrão, a [Estrutura DateTime](https://msdn.microsoft.com/library/system.datetime.aspx) é mapeada para o tipo de dados datetime do SQL Server. Como o tipo de dados da coluna BirthDate é data e o Always Encrypted não dá suporte a uma conversão de valores de datetime criptografados em valores de data criptografados, o uso do mapeamento padrão resultará em um erro. 

```cs
string connectionString = "Data Source=server63; Initial Catalog=Clinic; Integrated Security=true; Column Encryption Setting=enabled";
using (SqlConnection connection = new SqlConnection(strbldr.ConnectionString))
{
   using (SqlCommand cmd = connection.CreateCommand())
   {
      cmd.CommandText = @"INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (@SSN, @FirstName, @LastName, @BirthDate);";

      SqlParameter paramSSN = cmd.CreateParameter();
      paramSSN.ParameterName = @"@SSN";
      paramSSN.DbType = DbType.AnsiStringFixedLength;
      paramSSN.Direction = ParameterDirection.Input;
      paramSSN.Value = "795-73-9838";
      paramSSN.Size = 11;
      cmd.Parameters.Add(paramSSN);

      SqlParameter paramFirstName = cmd.CreateParameter();
      paramFirstName.ParameterName = @"@FirstName";
      paramFirstName.DbType = DbType.String;
      paramFirstName.Direction = ParameterDirection.Input;
      paramFirstName.Value = "Catherine";
      paramFirstName.Size = 50;
      cmd.Parameters.Add(paramFirstName);

      SqlParameter paramLastName = cmd.CreateParameter();
      paramLastName.ParameterName = @"@LastName";
      paramLastName.DbType = DbType.String;
      paramLastName.Direction = ParameterDirection.Input;
      paramLastName.Value = "Abel";
      paramLastName.Size = 50;
      cmd.Parameters.Add(paramLastName);

      SqlParameter paramBirthdate = cmd.CreateParameter();
      paramBirthdate.ParameterName = @"@BirthDate";
      paramBirthdate.SqlDbType = SqlDbType.Date;
      paramBirthdate.Direction = ParameterDirection.Input;
      paramBirthdate.Value = new DateTime(1996, 09, 10);
      cmd.Parameters.Add(paramBirthdate);

      cmd.ExecuteNonQuery();
   } 
}
```

### <a name="retrieving-plaintext-data-example"></a>Recuperando um exemplo de dados de texto sem formatação

O exemplo a seguir demonstra a filtragem de dados com base em valores criptografados e a recuperação de dados de texto sem formatação de colunas criptografadas. Observe o seguinte:
- O valor usado na cláusula WHERE a ser filtrado na coluna SSN precisa ser passado com o SqlParameter, para que o Provedor de Dados do .NET Framework para SQL Server possa criptografá-lo de modo transparente antes de enviá-lo ao banco de dados.
- Todos os valores impressos pelo programa estarão em texto sem formatação, já que o Provedor de Dados do .NET Framework para SQL Server descriptografará de modo transparente os dados recuperados das colunas SSN e BirthDate.


> [!NOTE]
> Consultas podem executar comparações de igualdade em colunas se forem criptografados usando a criptografia determinística. Para obter mais informações, confira [Seleção de criptografia determinística ou aleatória](always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption).

```cs
string connectionString = "Data Source=server63; Initial Catalog=Clinic; Integrated Security=true; Column Encryption Setting=enabled";
    
using (SqlConnection connection = new SqlConnection(strbldr.ConnectionString))
 {
    using (SqlCommand cmd = connection.CreateCommand())
 {

 cmd.CommandText = @"SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN=@SSN";
 SqlParameter paramSSN = cmd.CreateParameter();
 paramSSN.ParameterName = @"@SSN";
 paramSSN.DbType = DbType.AnsiStringFixedLength;
 paramSSN.Direction = ParameterDirection.Input;
 paramSSN.Value = "795-73-9838";
 paramSSN.Size = 11;
 cmd.Parameters.Add(paramSSN);
 using (SqlDataReader reader = cmd.ExecuteReader())
 {
   if (reader.HasRows)
 {
 while (reader.Read())
 {
    Console.WriteLine(@"{0}, {1}, {2}, {3}", reader[0], reader[1], reader[2], ((DateTime)reader[3]).ToShortDateString());
 }
```

### <a name="retrieving-encrypted-data-example"></a>Recuperando um exemplo de dados criptografados

Se o Always Encrypted não estiver habilitado, uma consulta ainda poderá recuperar dados de colunas criptografadas, desde que a consulta não tenha parâmetros que se destinam a colunas criptografadas.

O exemplo a seguir demonstra como recuperar dados criptografados binários de colunas criptografadas. Observe o seguinte:

- Como o Sempre Criptografado não está habilitado na cadeia de conexão, a consulta retornará valores criptografados de SSN e BirthDate como matrizes de bytes (o programa converte os valores em cadeias de caracteres).
- Uma consulta que recupera dados de colunas criptografadas com o Sempre Criptografado desabilitado pode ter parâmetros, desde que nenhum dos parâmetros se destinem a uma coluna criptografada. A consulta acima filtra por LastName, que não é criptografado no banco de dados. Se a consulta filtrar por SSN ou BirthDate, a consulta falhará.


```cs
string connectionString = "Data Source=server63; Initial Catalog=Clinic; Integrated Security=true";
                
using (SqlConnection connection = new SqlConnection(connectionString))
{
   connection.Open();
   using (SqlCommand cmd = connection.CreateCommand())
   {
      cmd.CommandText = @"SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [LastName]=@LastName";
      SqlParameter paramLastName = cmd.CreateParameter();
      paramLastName.ParameterName = @"@LastName";
      paramLastName.DbType = DbType.String;
      paramLastName.Direction = ParameterDirection.Input;
      paramLastName.Value = "Abel";
      paramLastName.Size = 50;
      cmd.Parameters.Add(paramLastName);
      using (SqlDataReader reader = cmd.ExecuteReader())
      {
         if (reader.HasRows)
         {
            while (reader.Read())
         {
         Console.WriteLine(@"{0}, {1}, {2}, {3}", BitConverter.ToString((byte[])reader[0]), reader[1], reader[2], BitConverter.ToString((byte[])reader[3]));
      }
   }
}
```

### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>Evitando problemas comuns ao consultar colunas criptografadas

Esta seção descreve as categorias comuns de erros ao consultar colunas criptografadas de aplicativos .NET e algumas diretrizes sobre como evitá-los.

### <a name="unsupported-data-type-conversion-errors"></a>Erros de conversão de tipo de dados sem suporte

O Always Encrypted dá suporte a algumas conversões de tipos de dados criptografados. Confira [Always Encrypted](always-encrypted-database-engine.md) para obter uma lista detalhada de conversões de tipo com suporte. Faça o seguinte para evitar erros de conversão de tipo de dados:

- Defina os tipos de parâmetros que se destinam a colunas criptografadas, para que o tipo de dados do SQL Server do parâmetro seja exatamente o mesmo que o tipo da coluna de destino ou para que haja suporte para uma conversão do tipo de dados do SQL Server do parâmetro no tipo da coluna de destino. É possível impor o mapeamento desejado dos tipos de dados do .NET em tipos de dados específicos do SQL Server usando a Propriedade SqlParameter.SqlDbType.
- Verifique se a precisão e escala dos parâmetros que se destinam a colunas dos tipos de dados decimais e numéricos do SQL Server são iguais à precisão e escala configuradas para a coluna de destino.  
- Verifique se a precisão dos parâmetros que se destinam a colunas datetime2, datetimeoffset ou a tipos de dados temporais do SQL Server não é maior do que a precisão da coluna de destino (em consultas que modificam os valores na coluna de destino).  

### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>Erros devido à passagem de texto sem formatação em vez de valores criptografados

Qualquer valor que se destina a uma coluna criptografada precisa ser criptografado no aplicativo. Uma tentativa de inserir/modificar ou de filtrar por um valor de texto sem formatação em uma coluna criptografada resultará em um erro semelhante a este:


```cs
System.Data.SqlClient.SqlException (0x80131904): Operand type clash: varchar is incompatible with varchar(8000) encrypted with (encryption_type = 'DETERMINISTIC', encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'CEK_Auto1', column_encryption_key_database_name = 'Clinic') collation_name = 'SQL_Latin1_General_CP1_CI_AS'
```

Para evitar esses tipos de erros, garanta que:
- O Always Encrypted é habilitado para as consultas de aplicativo que se destinam a colunas criptografadas (na cadeia de conexão ou no objeto [SqlCommand](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.aspx) de uma consulta específica).
- SqlParameter é usado para enviar dados que se destinam a colunas criptografadas. O exemplo a seguir mostra uma consulta que é filtrada incorretamente por um literal ou uma constante em uma coluna criptografada (SSN) (em vez de passar o literal em um objeto SqlParameter). 


```cs
using (SqlCommand cmd = connection.CreateCommand())
{
   cmd.CommandText = @"SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN='795-73-9838'";
cmd.ExecuteNonQuery();
}
```

## <a name="working-with-column-master-key-stores"></a>Trabalhando com repositórios de chaves mestras de coluna

Para criptografar um valor de parâmetro ou descriptografar dados nos resultados da consulta, o Provedor de Dados do .NET Framework para SQL Server precisa obter uma chave de criptografia de coluna configurada para a coluna de destino. As chaves de criptografia de coluna são armazenadas em formato criptografado nos metadados do banco de dados. Cada chave de criptografia de coluna tem uma chave mestra de coluna correspondente que foi usada para criptografar a chave de criptografia de coluna. Os metadados do banco de dados não armazenam as chaves mestras de coluna – eles contêm apenas as informações sobre um repositório de chaves que contém uma chave mestra de coluna específica e a localização da chave no repositório de chaves.

Para obter um valor de texto sem formatação de uma chave de criptografia de coluna, o Provedor de Dados do .NET Framework para SQL Server primeiro obtém os metadados sobre a chave de criptografia de coluna e sua chave mestra de coluna correspondente e, em seguida, usa as informações nos metadados para entrar em contato com o repositório de chaves, que contém a chave mestra de coluna, e descriptografar a chave de criptografia de coluna criptografada. O Provedor de Dados .NET Framework para SQL Server se comunica com um repositório de chaves usando um provedor de repositórios de chaves mestras de coluna – que é uma instância de uma classe derivada da Classe [SqlColumnEncryptionKeyStoreProvider](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcolumnencryptionkeystoreprovider.aspx).


O processo para obter uma chave de criptografia de coluna:

1.  Se o Always Encrypted estiver habilitado em uma consulta, o Provedor de Dados .NET Framework para SQL Server chama **sys.sp_describe_parameter_encryption** de forma transparente para recuperar metadados de criptografia para parâmetros que se destinam a colunas criptografadas, caso a consulta tenha parâmetros. Para dados criptografados contidos nos resultados de uma consulta, o SQL Server anexa metadados de criptografia automaticamente. As informações sobre a chave mestra de coluna incluem:
    - O nome de um provedor de repositório de chaves que encapsula um repositório de chaves que contém a chave mestra de coluna. 
    - O caminho de chave que especifica o local da chave mestra da coluna no repositório de chaves.
    
    As informações sobre a chave de criptografia de coluna incluem:

    - O valor criptografado de uma chave de criptografia de coluna.
    - O nome do algoritmo que foi usado para criptografar a chave de criptografia de coluna.
2.  O Provedor de Dados .NET Framework para SQL Server usa o nome do provedor de repositório de chaves mestras de coluna para pesquisar o objeto de provedor (uma instância de uma classe derivada da Classe SqlColumnEncryptionKeyStoreProvider) em uma estrutura de dados interna.
3.  Para descriptografar a chave de criptografia de coluna, o Provedor de Dados .NET Framework para SQL Server chama o Método SqlColumnEncryptionKeyStoreProvider.DecryptColumnEncryptionKey, passando o caminho da chave mestra de coluna, o valor criptografado da chave de criptografia de coluna e o nome do algoritmo de criptografia, usado para gerar a chave de criptografia de coluna criptografada.




### <a name="using-built-in-column-master-key-store-providers"></a>Usando provedores internos de repositórios de chaves mestras de coluna

O Provedor de Dados do .NET Framework para SQL Server é fornecido com os provedores internos de repositórios de chaves mestras de coluna a seguir, que são pré-registrados com os nomes do provedor específico (usados para pesquisar o provedor).


| Classe | Descrição | Nome (de pesquisa) do provedor |
|:---|:---|:---|
|Classe SqlColumnEncryptionCertificateStoreProvider| Um provedor do Repositório de Certificados do Windows. | MSSQL_CERTIFICATE_STORE |
|[Classe SqlColumnEncryptionCngProvider](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcolumnencryptioncngprovider.aspx) <br><br>**Observação:** esse provedor está disponível no .NET Framework 4.6.1 e versões posteriores. |Um provedor de um repositório de chaves que dá suporte à [API de Criptografia da Microsoft: API Next Generation (CNG)](https://msdn.microsoft.com/library/windows/desktop/aa376210.aspx). Normalmente, um repositório desse tipo é um módulo de segurança de hardware – um dispositivo físico que protege e gerencia chaves digitais e fornece processamento de criptografia.  | MSSQL_CNG_STORE|
| [Classe SqlColumnEncryptionCspProvider](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcolumnencryptioncspprovider.aspx)<br><br>**Observação:** esse provedor está disponível no .NET Framework 4.6.1 ou versões posteriores.| Um provedor de um repositório de chaves que dá suporte à [CAPI (Cryptography API) da Microsoft](https://msdn.microsoft.com/library/aa266944.aspx). Normalmente, um repositório desse tipo é um módulo de segurança de hardware – um dispositivo físico que protege e gerencia chaves digitais e fornece processamento de criptografia.| MSSQL_CSP_PROVIDER |
  
Não é necessário fazer nenhuma alteração de código do aplicativo para usar esses provedores, mas observe o seguinte:

- Você (ou seu DBA) precisa verificar se o nome do provedor, configurado nos metadados da chave mestra de coluna, está correto e se o caminho da chave mestra de coluna está em conformidade com o formato do caminho da chave válido para determinado provedor. É recomendável configurar as chaves usando ferramentas como o SQL Server Management Studio, que gera automaticamente os nomes de provedor válidos e os caminhos de chaves ao emitir a instrução [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) . Para obter mais informações, consulte [Configurando o Always Encrypted usando o SQL Server Management Studio](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md) e [Configurar o Always Encrypted usando o PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md).
- Verifique se seu aplicativo pode acessar a chave no repositório de chaves. Isso pode envolver a concessão de acesso para o aplicativo à chave e/ou ao repositório de chaves, dependendo do repositório de chaves, ou a execução de outras etapas de configuração específicas do repositório de chaves. Por exemplo, para acessar um repositório de chaves que implementa o CNG ou a CAPI (por exemplo, um módulo de segurança de hardware), você precisa verificar se uma biblioteca que implementa o CNG ou a CAPI de seu repositório está instalada no computador do aplicativo. Para obter detalhes, confira [Criar e armazenar chaves mestras de coluna para Always Encrypted](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md).

### <a name="using-azure-key-vault-provider"></a>Usando o provedor do Cofre de Chaves do Azure

O Cofre de Chaves do Azure é uma opção conveniente para armazenar e gerenciar chaves mestras de coluna do Always Encrypted (especialmente se seus aplicativos estiverem hospedados no Azure). O Provedor de Dados do .NET Framework para SQL Server não inclui um provedor interno de repositórios de chaves mestras de coluna para o Cofre de Chaves do Azure, mas está disponível como um pacote Nuget, que você pode integrar ao seu aplicativo com facilidade. Para obter detalhes, veja [Always Encrypted – Proteger dados confidenciais no Banco de Dados SQL com a criptografia de dados e armazenar as chaves de criptografia no Cofre de Chaves do Azure](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted-azure-key-vault/).

### <a name="implementing-a-custom-column-master-key-store-provider"></a>Implementando um provedor personalizado de repositórios de chaves mestras de coluna

Se você quiser armazenar chaves mestras de coluna em um repositório de chaves que não tem suporte em um provedor existente, será possível implementar um provedor personalizado estendendo a [Classe SqlColumnEncryptionCngProvider](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcolumnencryptioncngprovider.aspx) e registrando o provedor usando o método [SqlConnection.RegisterColumnEncryptionKeyStoreProviders](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.registercolumnencryptionkeystoreproviders.aspx) .


```cs
public class MyCustomKeyStoreProvider : SqlColumnEncryptionKeyStoreProvider
    {
        public override byte[] EncryptColumnEncryptionKey(string masterKeyPath, string encryptionAlgorithm, byte[] columnEncryptionKey)
        {
            // Logic for encrypting a column encrypted key.
        }
        public override byte[] DecryptColumnEncryptionKey(string masterKeyPath, string encryptionAlgorithm, byte[] EncryptedColumnEncryptionKey)
        {
            // Logic for decrypting a column encrypted key.
        }
    }  
    class Program
    {
        static void Main(string[] args)
        {
            Dictionary\<string, SqlColumnEncryptionKeyStoreProvider> providers =
               new Dictionary\<string, SqlColumnEncryptionKeyStoreProvider>();
            providers.Add("MY_CUSTOM_STORE", customProvider);
            SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
            providers.Add(SqlColumnEncryptionCertificateStoreProvider.ProviderName, customProvider);
            SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers); 
       // ...
        }

    }
```
 
### <a name="using-column-master-key-store-providers-for-programmatic-key-provisioning"></a>Usando provedores de repositórios de chaves mestras de coluna para o provisionamento programático de chaves

Ao acessar colunas criptografadas, o Provedor de Dados do .NET Framework para SQL Server encontra de modo transparente e chama o provedor de repositórios de chaves mestras de coluna certo para descriptografar as chaves de criptografia de coluna. Normalmente, o código normal do aplicativo não chama diretamente os provedores de repositórios de chaves mestras de coluna. No entanto, é possível criar uma instância e chamar um provedor de forma explícita para provisionar de modo programático e gerenciar chaves do Sempre Criptografado: para gerar uma chave de criptografia de coluna criptografada e descriptografar uma chave de criptografia de coluna (por exemplo, como a rotação de chave mestra de coluna da parte). Para obter mais informações, confira [Visão geral do gerenciamento de chaves do Always Encrypted](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md).
A implementação de suas próprias ferramentas de gerenciamento de chaves poderá ser necessária apenas se você usar um provedor personalizado de repositórios de chaves. Ao usar as chaves armazenadas em repositórios de chaves, para as quais os provedores internos existem, ou no Cofre de Chaves do Azure, é possível usar as ferramentas existentes, como SQL Server Management Studio ou PowerShell, para gerenciar e provisionar as chaves.
O exemplo abaixo ilustra como gerar uma chave de criptografia de coluna e como usar a [Classe SqlColumnEncryptionCertificateStoreProvider](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcolumnencryptioncertificatestoreprovider.aspx) para criptografar a chave com um certificado.


```cs
using System.Security.Cryptography;
static void Main(string[] args)
{
    byte[] EncryptedColumnEncryptionKey = GetEncryptedColumnEncryptonKey(); 
    Console.WriteLine("0x" + BitConverter.ToString(EncryptedColumnEncryptionKey).Replace("-", "")); 
    Console.ReadKey();
}

static byte[]  GetEncryptedColumnEncryptonKey()
{
    int cekLength = 32;
    String certificateStoreLocation = "CurrentUser";
    String certificateThumbprint = "698C7F8E21B2158E9AED4978ADB147CF66574180";
    // Generate the plaintext column encryption key.
    byte[] columnEncryptionKey = new byte[cekLength];
    RNGCryptoServiceProvider rngCsp = new RNGCryptoServiceProvider();
    rngCsp.GetBytes(columnEncryptionKey);

    // Encrypt the column encryption key with a certificate.
    string keyPath = String.Format(@"{0}/My/{1}", certificateStoreLocation, certificateThumbprint);
    SqlColumnEncryptionCertificateStoreProvider provider = new SqlColumnEncryptionCertificateStoreProvider();
    return provider.EncryptColumnEncryptionKey(keyPath, @"RSA_OAEP", columnEncryptionKey); 
}
```


## <a name="controlling-performance-impact-of-always-encrypted"></a>Controlando o impacto no desempenho do Sempre Criptografado

Como o Always Encrypted é uma tecnologia de criptografia do lado do cliente, a maioria das sobrecargas devido ao desempenho é observada no lado do cliente, não no banco de dados. Além do custo das operações de criptografia e descriptografia, as outras fontes de sobrecarga devido ao desempenho no lado do cliente são:
- Viagens de ida e volta adicionais ao banco de dados para recuperar metadados dos parâmetros de consulta.
- Chamadas a um repositório de chaves mestras de coluna para acessar uma chave mestra de coluna.

Esta seção descreve as otimizações de desempenho internas do Provedor do .NET Framework para SQL Server e como você pode controlar o impacto dos dois fatores acima no desempenho.

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>Controlando as viagens de ida e volta para recuperar metadados dos parâmetros de consulta

Se o Always Encrypted estiver habilitado para uma conexão, por padrão, o Provedor de Dados .NET Framework para SQL Server chamará [sys.sp_describe_parameter_encryption](../../system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) para cada consulta parametrizada, passando a instrução de consulta (sem nenhum valor de parâmetro) para o SQL Server. O**sys.sp_describe_parameter_encryption** analisa a instrução de consulta para descobrir se os parâmetros precisam ser criptografados, e se for o caso, para cada um, retorna as informações relacionadas à criptografia que permitirão ao Provedor de Dados .NET Framework para SQL Server criptografar os valores de parâmetro. O comportamento acima garante um alto nível de transparência para o aplicativo cliente. O aplicativo (e o desenvolvedor do aplicativo) não precisa estar ciente de quais consultas acessam colunas criptografadas, desde que os valores que se destinam às colunas criptografadas sejam passados para o Provedor de Dados do .NET Framework para SQL Server em objetos SqlParameter.


### <a name="query-metadata-caching"></a>Cache de metadados de consulta

No .NET Framework 4.6.2 e posterior, o Provedor de Dados .NET Framework para SQL Server armazena em cache os resultados de **sys.sp_describe_parameter_encryption** de cada instrução de consulta. Consequentemente, se a mesma instrução de consulta for executada várias vezes, o driver chama **sys.sp_describe_parameter_encryption** apenas uma vez. O caching de metadados de criptografia para instruções de consulta reduz consideravelmente o custo de desempenho da busca de metadados do banco de dados. O caching está habilitado por padrão. É possível desabilitar o caching de metadados do parâmetro definindo a [Propriedade SqlConnection.ColumnEncryptionQueryMetadataCacheEnabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.columnencryptionquerymetadatacacheenabled.aspx) como false, mas isso não é recomendado, exceto em casos raros, como o descrito abaixo:

Considere um banco de dados que tem dois esquemas diferentes: s1 e s2. Cada esquema contém uma tabela com o mesmo nome: t. As definições das tabelas s1.t e s2.t são idênticas, exceto pelas propriedades relacionadas à criptografia: uma coluna, chamada c, em s1.t não é criptografada e é criptografada em s2.t. O banco de dados tem dois usuários: u1 e u2. O esquema padrão para os usuários u1 é s1. O esquema padrão para u2 é s2. Um aplicativo .NET abre duas conexões com o banco de dados, representando o usuário u1 em uma conexão e o usuário u2 em outra. O aplicativo envia uma consulta com um parâmetro que se destina à coluna c pela conexão do usuário u1 (a consulta não especifica o esquema e, portanto, o esquema padrão do usuário é considerado). Em seguida, o aplicativo envia a mesma consulta pela conexão do usuário u2. Se o caching de metadados de consulta estiver habilitado, após a primeira consulta, o cache será populado com metadados indicando que a coluna c, os destinos do parâmetro de consulta, não é criptografada. Como a segunda consulta tem a instrução de consulta idêntica, as informações armazenadas no cache serão usadas. Como resultado, o driver enviará a consulta sem criptografar o parâmetro (o que é incorreto, já que a coluna de destino, s2.t.c, é criptografada), causando a perda do valor de texto sem formatação do parâmetro para o servidor. O servidor detectará a incompatibilidade e forçará o driver a atualizar o cache, para que o aplicativo reenvie a consulta de forma transparente com o valor do parâmetro criptografado corretamente. Nesse caso, o caching deve ser desabilitado para prevenir a perda de valores confidenciais para o servidor. 




### <a name="setting-always-encrypted-at-the-query-level"></a>Configurando o Always Encrypted no nível da consulta

Para controlar o impacto no desempenho da recuperação de metadados de criptografia para consultas parametrizadas, é possível habilitar o Always Encrypted para consultas individuais, em vez de configurá-lo para a conexão. Assim, você pode garantir que **sys.sp_describe_parameter_encryption** é invocado apenas para consultas que você sabe que têm parâmetros que se destinam a colunas criptografadas. No entanto, observe que, ao fazer isso, você reduzirá a transparência da criptografia: se você alterar as propriedades de criptografia das colunas de banco de dados, talvez seja necessário alterar o código do aplicativo para alinhá-lo com as alterações de esquema.

> [!NOTE]
> A configuração do Always Encrypted no nível da consulta apresenta benefícios de desempenho limitados no .NET 4.6.2 e versões posteriores, que implementa o caching de metadados de criptografia do parâmetro.

Para controlar o comportamento do Always Encrypted em relação a consultas individuais, você precisa usar este construtor de [SqlCommand](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.aspx) e [SqlCommandColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommandcolumnencryptionsetting.aspx). Veja algumas diretrizes úteis:
- Se a maioria das consultas que um aplicativo cliente envia por uma conexão de banco de dados acessa colunas criptografadas:
    - Defina a palavra-chave da cadeia de conexão de **Configuração da Criptografia de Coluna** como *Habilitado*.
    - Defina **SqlCommandColumnEncryptionSetting.Disabled** para consultas individuais que não acessam nenhuma coluna criptografada. Isso desabilitará a chamada a sys.sp_describe_parameter_encryption, além de ser uma tentativa de descriptografar todos os valores no conjunto de resultados.
    - Defina **SqlCommandColumnEncryptionSetting.ResultSet** para consultas individuais que não têm parâmetros que exijam criptografia, mas que recuperam dados de colunas criptografadas. Isso desabilitará a chamada a sys.sp_describe_parameter_encryption e a criptografia de parâmetros. A consulta poderá descriptografar os resultados das colunas de criptografia.
- Se a maioria das consultas que um aplicativo cliente envia por uma conexão de banco de dados não acessa colunas criptografadas:
    - Defina a palavra-chave da cadeia de conexão de **Configuração da Criptografia de Coluna** como **Desabilitado**.
    - Defina **SqlCommandColumnEncryptionSetting.Enabled** para consultas individuais que têm parâmetros que precisam ser criptografados. Isso habilitará a chamada a sys.sp_describe_parameter_encryption, além da descriptografia de todos os resultados de consulta recuperados de colunas criptografadas.
    - Defina **SqlCommandColumnEncryptionSetting.ResultSet** para consultas que não têm parâmetros que exijam criptografia, mas que recuperam dados de colunas criptografadas. Isso desabilitará a chamada a sys.sp_describe_parameter_encryption e a criptografia de parâmetros. A consulta poderá descriptografar os resultados das colunas de criptografia.

No exemplo abaixo, o Sempre Criptografado está desabilitado para a conexão de banco de dados. A consulta emitida pelo aplicativo tem um parâmetro que se destina à coluna LastName não criptografada. A consulta recupera dados das colunas SSN e BirthDate que são criptografadas. Nesse caso, a chamada a sys.sp_describe_parameter_encryption para recuperar os metadados de criptografia não é necessária. No entanto, a descriptografia dos resultados da consulta precisa estar habilitada para que o aplicativo possa receber valores de texto não criptografado das duas colunas criptografadas. A configuração de SqlCommandColumnEncryptionSetting.ResultSet é usada para garantir isso.



```cs
string connectionString = "Data Source=server63; Initial Catalog=Clinic; Integrated Security=true";
using (SqlConnection connection = new SqlConnection(connectionString))
{
    connection.Open();
    using (SqlCommand cmd = new SqlCommand(@"SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [LastName]=@LastName",
connection, null, SqlCommandColumnEncryptionSetting.ResultSetOnly))
    {
        SqlParameter paramLastName = cmd.CreateParameter();
        paramLastName.ParameterName = @"@LastName";
        paramLastName.DbType = DbType.String;
        paramLastName.Direction = ParameterDirection.Input;
        paramLastName.Value = "Abel";
        paramLastName.Size = 50;
        cmd.Parameters.Add(paramLastName);
        using (SqlDataReader reader = cmd.ExecuteReader())
            {
               if (reader.HasRows)
               {
                  while (reader.Read())
                  {
                     Console.WriteLine(@"{0}, {1}, {2}, {3}", reader[0], reader[1], reader[2], ((DateTime)reader[3]).ToShortDateString());
                  }
               }
            }
  } 
}
```


### <a name="column-encryption-key-caching"></a>Cache de chaves de criptografia de coluna

Para reduzir o número de chamadas a um repositório de chaves mestras de coluna para descriptografar chaves de criptografia de coluna, o Provedor de Dados do .NET Framework para SQL Server armazena em cache as chaves de criptografia de coluna de texto sem formatação na memória. Depois de receber o valor da chave de criptografia de coluna criptografado dos metadados do banco de dados, o driver primeiro tentará encontrar a chave de criptografia de coluna de texto sem formatação correspondente ao valor da chave criptografado. O driver chamará o repositório de chaves que contém a chave mestra de coluna apenas se não conseguir encontrar o valor da chave de criptografia de coluna criptografado no cache.

> [!NOTE]
> No .NET Framework 4.6 e 4.6.1, as entradas de chave de criptografia de coluna no cache nunca são removidas. Isso significa que, para determinada chave de criptografia de coluna criptografada, o driver entrará em contato com o repositório de chaves apenas uma vez durante o tempo de vida do aplicativo.

No .NET Framework 4.6.2 e posterior, as entradas de cache são removidas após um intervalo de vida útil configurável por motivos de segurança. O valor de vida útil padrão é de 2 horas. Se você tiver requisitos de segurança mais estritos sobre quanto tempo as chaves de criptografia de coluna podem ser armazenadas em cache em um texto sem formatação no aplicativo, será possível alterá-las usando a [Propriedade SqlConnection.ColumnEncryptionKeyCacheTtl](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.columnencryptionkeycachettl.aspx). 


## <a name="enabling-additional-protection-for-a-compromised-sql-server"></a>Habilitando proteção adicional para um SQL Server comprometido

Por padrão, o *Provedor de Dados .NET Framework para SQL Server* depende do sistema de banco de dados (SQL Server ou Banco de Dados SQL do Azure) para fornecer metadados sobre quais colunas no banco de dados são criptografadas e como isso é feito. Os metadados de criptografia permitem ao Provedor de Dados .NET Framework para SQL Server criptografar parâmetros de consulta e descriptografar os resultados da consulta sem nenhuma entrada do aplicativo, o que reduz consideravelmente o número de alterações necessárias no aplicativo. No entanto, se o processo do SQL Server for comprometido e um invasor violar os metadados enviados pelo SQL Server para o Provedor de Dados .NET Framework para SQL Server, o invasor poderá roubar informações confidenciais. Esta seção descreve as APIs que ajudam a fornecer um nível adicional de proteção contra esse tipo de ataque, à custa da redução da transparência. 

### <a name="forcing-parameter-encryption"></a>Forçando a criptografia de parâmetro 

Antes que o Provedor de Dados .NET Framework para SQL Server envie uma consulta parametrizada para o SQL Server, ele solicita ao SQL Server (chamando [sys.sp_describe_parameter_encryption](../../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md)) para analisar a instrução de consulta e fornecer informações sobre quais parâmetros da consulta devem ser criptografados. Uma instância do SQL Server comprometida poderá confundir o Provedor de Dados .NET Framework para SQL Server enviando os metadados, indicando o parâmetro não tem como destino uma coluna criptografada, apesar do fato de que a coluna é criptografada no banco de dados. Como resultado, o Provedor de Dados .NET Framework para SQL Server não criptografará o valor do parâmetro e o enviará como texto sem formatação para a instância do SQL Server comprometida.

Para prevenir um ataque desse tipo, um aplicativo pode definir a [Propriedade SqlParameter.ForceColumnEncryption](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.forcecolumnencryption.aspx) do parâmetro como true. Isso fará com que o Provedor de Dados .NET Framework para SQL Server gere uma exceção, caso os metadados recebidos do servidor indicarem que o parâmetro não precisa ser criptografado.

Embora o uso da **Propriedade SqlParameter.ForceColumnEncryption** ajude a melhorar a segurança, ele também reduz a transparência da criptografia para o aplicativo cliente. Se você atualizar o esquema de banco de dados para alterar o conjunto de colunas criptografadas, talvez seja necessário fazer alterações no aplicativo também.

O exemplo de código a seguir ilustra o uso da **Propriedade SqlParameter.ForceColumnEncryption** para impedir que os números do seguro social sejam enviados em texto não criptografado para o banco de dados. 



```cs
SqlCommand cmd = _sqlconn.CreateCommand(); 

// Use parameterized queries to access Always Encrypted data. 
 
cmd.CommandText = @"SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN] = @SSN;"; 

SqlParameter paramSSN = cmd.CreateParameter(); 
paramSSN.ParameterName = @"@SSN"; 
paramSSN.DbType = DbType.AnsiStringFixedLength; 
paramSSN.Direction = ParameterDirection.Input; 
paramSSN.Value = ssn; 
paramSSN.Size = 11; 
paramSSN.ForceColumnEncryption = true; 
cmd.Parameters.Add(paramSSN); 

SqlDataReader reader = cmd.ExecuteReader();
```
 

### <a name="configuring-trusted-column-master-key-paths"></a>Configurando caminhos confiáveis de chave mestra de coluna 

Os metadados de criptografia, que o SQL Server retorna para parâmetros de consulta que se destinam a colunas criptografadas e para resultados recuperados das colunas de criptografia, incluem o caminho da chave mestra de coluna que identifica o repositório de chaves e o local da chave no repositório de chaves. Se a instância do SQL Server for comprometida, ela poderá enviar o caminho da chave, direcionando o Provedor de Dados .NET Framework para SQL Server para o local controlado por um invasor. Isso poderá causar a perda das credenciais do repositório de chaves, no caso do repositório de chaves que exige a autenticação do aplicativo. 

Para prevenir esses ataques, o aplicativo poderá especificar a lista de caminhos de chave confiáveis para determinado servidor usando a [Propriedade SqlConnection.ColumnEncryptionTrustedMasterKeyPaths](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.columnencryptiontrustedmasterkeypaths.aspx). Se o Provedor de Dados .NET Framework para SQL Server receber um caminho da chave que esteja fora da lista de caminhos de chave confiáveis, ele vai gerar uma exceção. 

Embora a definição de caminhos de chave confiáveis melhore a segurança do aplicativo, você precisará alterar o código e/ou a configuração do aplicativo cada vez que girar a chave mestra de coluna (sempre que o caminho da chave mestra de coluna for alterados). 

O seguinte exemplo mostra como configurar caminhos de chave mestra de coluna confiáveis:


```cs
// Configure trusted key paths to protect against fake key paths sent by a compromised SQL Server instance 
// First, create a list of trusted key paths for your server 
List<string> trustedKeyPathList = new List<string>(); 
trustedKeyPathList.Add("CurrentUser/my/425CFBB9DDDD081BB0061534CE6AB06CB5283F5Ea"); 

// Register the trusted key path list for your server 

SqlConnection.ColumnEncryptionTrustedMasterKeyPaths.Add(serverName, trustedKeyPathList);
```
 



## <a name="copying-encrypted-data-using-sqlbulkcopy"></a>Copiando dados criptografados usando SqlBulkCopy

Com SqlBulkCopy, você pode copiar dados, que já estão criptografados e armazenados em uma tabela, em outra tabela, sem descriptografá-los. Para fazer isso:

- Verifique se a configuração de criptografia da tabela de destino é idêntica à configuração da tabela de origem. Em particular, as duas tabelas devem ter as mesmas colunas criptografadas, e as colunas devem ser criptografadas usando os mesmos tipos de criptografia e as mesmas chaves de criptografia. Observação: se uma das colunas de destino for criptografada de modo diferente da coluna de origem correspondente, você não poderá descriptografar os dados na tabela de destino após a operação de cópia. Os dados serão corrompidos.
- Configure ambas as conexões de banco de dados, à tabela de origem e à tabela de destino, com o Sempre Criptografado desabilitado. 
- Defina a opção AllowEncryptedValueModifications (veja [SqlBulkCopyOptions](https://msdn.microsoft.com/library/system.data.sqlclient.sqlbulkcopyoptions.aspx)). Observação: tenha cuidado ao especificar AllowEncryptedValueModifications, pois isso pode levar à corrupção de banco de dados, já que o Provedor de Dados do .NET Framework para SQL Server não verifica se os dados estão realmente criptografados ou se estão criptografados corretamente usando o mesmo tipo de criptografia, algoritmo e chave que a coluna de destino.

A opção AllowEncryptedValueModifications está disponível no .NET Framework 4.6.1 e versões posteriores.

Aqui está um exemplo que copia dados de uma tabela em outra. Pressupõe-se que as colunas SSN e BirthDate estão criptografadas.
        

```cs
static public void CopyTablesUsingBulk(string sourceTable, string targetTable)
{
   string sourceConnectionString = "Data Source=server63; Initial Catalog=Clinic; Integrated Security=true";
   string targetConnectionString = "Data Source= server64; Initial Catalog=Clinic; Integrated Security=true";
   using (SqlConnection connSource = new SqlConnection(sourceConnectionString))
   {
      connSource.Open();
      using (SqlCommand cmd = new SqlCommand(string.Format("SELECT [PatientID], [SSN], [FirstName], [LastName], [BirthDate] FROM {0}", sourceTable), connSource))
      {
         using (SqlDataReader reader = cmd.ExecuteReader())
         {
            SqlBulkCopy copy = new SqlBulkCopy(targetConnectionString, SqlBulkCopyOptions.KeepIdentity | SqlBulkCopyOptions.AllowEncryptedValueModifications);
            copy.EnableStreaming = true;
            copy.DestinationTableName = targetTable;
            copy.WriteToServer(reader);
         }
      }
}
```


## <a name="always-encrypted-api-reference"></a>Referência de API do Always Encrypted

**Namespace:** [System.Data.SqlClient](https://msdn.microsoft.com/library/system.data.sqlclient.aspx)

**Assembly:** System.Data (em System.Data.dll)




|Nome|Descrição|Introduzido na versão do .NET
|:---|:---|:---
|[Classe SqlColumnEncryptionCertificateStoreProvider](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcolumnencryptioncertificatestoreprovider.aspx)|Um provedor de repositório de chaves para o Repositório de Certificados do Windows.|  4.6
|[Classe SqlColumnEncryptionCngProvider](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcolumnencryptioncngprovider.aspx)|Um provedor de repositório de chaves para A API de Criptografia da Microsoft: Next Generation (CNG).|  4.6.1
|[Classe SqlColumnEncryptionCspProvider](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcolumnencryptioncspprovider.aspx)|Um provedor de repositório de chaves para CSPs (Provedores de Serviços Criptográficos) baseados no Microsoft CAPI.|4.6.1  
|[SqlColumnEncryptionKeyStoreProvider](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcolumnencryptionkeystoreprovider.aspx)|Classe base dos provedores de repositório de chaves.|  4.6
|[Enumeração SqlCommandColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommandcolumnencryptionsetting.aspx)|Configurações para habilitar a criptografia e a descriptografia de uma conexão de banco de dados.|4.6  
|[Enumeração SqlConnectionColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx)|Configurações para controlar o comportamento do Always Encrypted para consultas individuais.|4.6  
| [Propriedade SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx)|Obtém e define o Always Encrypted na cadeia de conexão.|4.6|
| [Propriedade SqlConnection.ColumnEncryptionQueryMetadataCacheEnabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.columnencryptionquerymetadatacacheenabled.aspx) | Habilita e desabilita o caching de metadados de consulta de criptografia. | 4.6.2
| [Propriedade SqlConnection.ColumnEncryptionKeyCacheTtl](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.columnencryptionkeycachettl.aspx) | Obtém e define a vida útil das entradas no cache de chaves de criptografia de coluna. | 4.6.2
|[Propriedade SqlConnection.ColumnEncryptionTrustedMasterKeyPaths](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.columnencryptiontrustedmasterkeypaths.aspx)|Permite que você defina uma lista de caminhos confiáveis de chave para um servidor de banco de dados. Se durante o processamento de uma consulta de aplicativo o driver receber um caminho de chave que não esteja na lista, a consulta falhará. Esta propriedade fornece proteção adicional contra ataques de segurança que envolvem um SQL Server comprometido fornecendo falsos caminhos principais, que podem levar a vazar credenciais de repositório de chaves.|  4.6
|[Método SqlConnection.RegisterColumnEncryptionKeyStoreProviders](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.registercolumnencryptionkeystoreproviders.aspx)|Permite que você registre os provedores de repositório de chaves personalizado. É um dicionário que mapeia nomes de provedor de repositório de chaves para implementações do provedor de repositório de chaves.|  4.6
|[Construtor SqlCommand (String, SqlConnection, SqlTransaction, SqlCommandColumnEncryptionSetting)](https://msdn.microsoft.com/library/dn956511\(v=vs.110\).aspx)|Permite controlar o comportamento do Always Encrypted para consultas individuais.|  4.6
|[Propriedade SqlParameter.ForceColumnEncryption](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.forcecolumnencryption.aspx)|Impõe a criptografia de um parâmetro. Se o SQL Server informar o driver que o parâmetro não precisa ser criptografado, a consulta que estiver o parâmetro falhará. Essa propriedade fornece proteção adicional contra ataques de segurança que envolvem um SQL Server comprometido fornecendo metadados de criptografia incorretos ao cliente, o que pode levar à divulgação de dados.|4.6  
|Nova palavra-chave da [cadeia de conexão](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx) : `Column Encryption Setting=enabled`|Habilita ou desabilita a funcionalidade Always Encrypted para a conexão.| 4.6 
  

## <a name="see-also"></a>Consulte Também

- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Blog do Always Encrypted](https://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)
- [Tutorial do Banco de Dados SQL: proteger dados confidenciais com Always Encrypted](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted/)

















