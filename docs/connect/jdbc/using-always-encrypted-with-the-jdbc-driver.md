---
title: Use sempre criptografado com o Driver JDBC | Microsoft Docs
ms.custom: 
ms.date: 12/30/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 271c0438-8af1-45e5-b96a-4b1cabe32707
caps.latest.revision: 64
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 84cf217faf0980d3ef1daf9a86a4aa362931d199
ms.contentlocale: pt-br
ms.lasthandoff: 09/27/2017

---
# <a name="using-always-encrypted-with-the-jdbc-driver"></a>Use o Always Encrypted com o Driver JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Este artigo fornece informações sobre como desenvolver aplicativos do Java usando [sempre criptografado](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_7) e o Microsoft JDBC Driver 6.0 (ou superior) para o SQL Server.

Sempre criptografado permite que os clientes criptografem dados confidenciais e nunca revelem os dados ou as chaves de criptografia do SQL Server ou banco de dados do SQL Azure. Um sempre criptografado habilitado driver, como o Microsoft JDBC Driver 6.0 (ou superior) para o SQL Server, consegue isso criptografando e descriptografando dados confidenciais no aplicativo cliente de forma transparente. O driver determina automaticamente qual consulta parâmetros correspondem a colunas de banco de dados confidenciais (protegidas com o sempre criptografado) e criptografa os valores desses parâmetros antes de passar os valores para o SQL Server ou banco de dados do SQL Azure. Da mesma forma, o driver descriptografa de modo transparente os dados recuperados das colunas de banco de dados criptografadas nos resultados da consulta. Para obter mais informações, visite [sempre criptografados (mecanismo de banco de dados)](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_7) e [sempre criptografados referência da API para o Driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).  


## <a name="prerequisites"></a>Pré-requisitos

- Configure o Sempre Criptografado em seu banco de dados. Isso envolve o provisionamento de chaves do Sempre Criptografado e a configuração de criptografia de colunas de banco de dados selecionadas. Se você ainda não tiver um banco de dados com o Sempre Criptografado configurado, siga as instruções em [Getting Started with Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_5)(Introdução ao Sempre Criptografado).
- Certifique-se de que Microsoft JDBC Driver 6.0 (ou superior) para o SQL Server está instalado no computador de desenvolvimento. 
-   Baixe e instale os arquivos de política de jurisdição de força ilimitada de Java Cryptography Extension (JCE).  Certifique-se de ler o arquivo Leiame incluído no arquivo zip para instruções de instalação e detalhes pertinentes sobre problemas possíveis de importação/exportação.  
  
    -   Se usar o sqljdbc41.jar, os arquivos de política podem ser baixados do [baixar arquivos de política de jurisdição de força ilimitada do Java Cryptography Extension (JCE) 7](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)  
  
    -   Se usar o sqljdbc42.jar, os arquivos de política podem ser baixados do [baixar arquivos de política de jurisdição de força ilimitada do Java Cryptography Extension (JCE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)   
    
## <a name="enabling-always-encrypted-for-application-queries"></a>Habilitando o Always Encrypted para consultas de aplicativo  
É a maneira mais fácil de habilitar a criptografia de parâmetros e a descriptografia dos resultados de consulta de direcionamento colunas criptografadas, definindo o valor da **columnEncryptionSetting** palavra-chave de cadeia de caracteres de conexão para  **Habilitado**.

Este é um exemplo de uma cadeia de caracteres de conexão que habilita o sempre criptografado no driver JDBC:
  
```  
String connectionString = "jdbc:sqlserver://localhost;user=<user>;password=<password>;databaseName=<database>;columnEncryptionSetting=Enabled;"; 
SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionString);
     
```  
  
E, a seguir está um exemplo equivalente usando o objeto SQLServerDataSource.  
  
```  
SQLServerDataSource ds = new SQLServerDataSource();  
ds.setServerName("localhost");
ds.setUser("<user>");
ds.setPassword("<password>");
ds.setDatabaseName("<database>");
ds.setColumnEncryptionSetting("Enabled");  
SQLServerConnection con = (SQLServerConnection) ds.getConnection(); 
```    

O Sempre Criptografado também pode ser habilitado para consultas individuais. Consulte o **controlando o desempenho do impacto do sempre criptografado** seção abaixo. Observe que, habilitar o Sempre Criptografado não é suficiente para o êxito da criptografia ou descriptografia. Você também precisa garantir que:
- O aplicativo tem as permissões de banco de dados *VIEW ANY COLUMN MASTER KEY DEFINITION* e *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* , necessárias para acessar os metadados sobre as chaves do Always Encrypted no banco de dados. Para obter detalhes, veja a [seção Permissões em Always Encrypted (Mecanismo de Banco de Dados)](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_7).
- O aplicativo pode acessar a chave mestra de coluna que protege as chaves de criptografia de coluna, criptografando as colunas de banco de dados consultadas. Observe que, para usar o provedor de armazenamento de chaves Java, que você precisa fornecer credenciais adicionais na cadeia de conexão. Consulte **provedor de repositório de chaves Java usando** seção para obter mais detalhes.

### <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>Configurar como os valores são enviados ao servidor

O **sendTimeAsDatetime** propriedade de conexão é usada para configurar como o valor de Java.SQL. time será enviado para o servidor. Quando sendTimeAsDatetime = false, o tempo de valor é enviado como o tipo de hora do SQL Server e quando sendTimeAsDatetime = true, o valor é enviado como um tipo de datetime de tempo. Observe que, quando uma coluna de hora é criptografada, a propriedade sendTimeAsDatetime deve ser false como colunas criptografadas não dão suporte a conversão de tempo para datetime. Observe também que essa propriedade é true, o padrão ao usar colunas time criptografado, você precisará definido como false. Caso contrário, o driver lançará como exceção. A classe SQLServerConnection tem dois métodos, começando com a versão 6.0 do driver para configurar o valor dessa propriedade por meio de programação:
 
* setSendTimeAsDatetime public void (boolean sendTimeAsDateTimeValue)
* public boolean getSendTimeAsDatetime()

Para obter mais informações sobre essa propriedade, visite [Java.SQL. time configurando como os valores são enviados para o servidor](https://msdn.microsoft.com/library/ff427224(v=sql.110).aspx). 

### <a name="configuring-how-string-values-are-sent-to-the-server"></a>Configurar como os valores de cadeia de caracteres são enviados para o servidor

O **sendStringParametersAsUnicode** propriedade de conexão é usada para configurar como os valores de cadeia de caracteres são enviados para o SQL Server. Se definido como "true", parâmetros de cadeia de caracteres é enviado para o servidor no formato Unicode. Se definido como "falsos", parâmetros de cadeia de caracteres é enviado em formato não Unicode, como ASCII/MBCS, e Unicode. O valor padrão desta propriedade é "true". Quando sempre criptografado está habilitado e uma coluna char/varchar/varchar(max) é criptografado, o valor de **sendStringParametersAsUnicode** deve ser definida como true (ou ser deixado como o padrão). O Microsoft JDBC Driver para SQL Server lançará uma exceção ao inserir dados em uma coluna criptografada char/varchar/varchar(max) se essa propriedade for definida como false. Para obter mais informações sobre essa propriedade, visite [definindo as propriedades de Conexão](../../connect/jdbc/setting-the-connection-properties.md). 
  
## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>Recuperando e modificando dados em colunas criptografadas

Depois de habilitar o sempre criptografado para consultas de aplicativo, você pode usar APIs padrão do JDBC para recuperar ou modificar dados em colunas de banco de dados criptografado. Supondo que seu aplicativo tem as permissões de banco de dados necessários e pode acesso a chave mestra de coluna, o Microsoft JDBC Driver para SQL Server criptografará quaisquer parâmetros de consulta que se destinam a colunas criptografadas e descriptografar dados recuperados de colunas criptografadas tipos de dados retornando valores de texto sem formatação de tipos do JDBC, correspondente ao SQL Server definido para as colunas no esquema de banco de dados.
Se o Sempre Criptografado não estiver habilitado, as consultas com parâmetros que se destinam a colunas criptografadas falharão. As consultas ainda podem recuperar dados de colunas criptografadas, desde que a consulta não tenha parâmetros que se destinam a colunas criptografadas. No entanto, o Microsoft JDBC Driver para SQL Server não tentará descriptografar todos os valores recuperados de colunas criptografadas, e o aplicativo receberá dados binários criptografados (como matrizes de bytes).

A tabela abaixo resume o comportamento das consultas, dependendo se o Always Encrypted está habilitado ou não:

|Característica da consulta | O Sempre Criptografado está habilitado e o aplicativo pode acessar as chaves e os metadados da chave|O Sempre Criptografado está habilitado e o aplicativo não pode acessar as chaves nem os metadados da chave | O Sempre Criptografado está desabilitado|
|:---|:---|:---|:---|
| Consultas com parâmetros que se destinam a colunas criptografadas. | Os valores de parâmetro são criptografados de modo transparente. | Erro | Erro|
| Consultas que recuperam dados de colunas criptografadas, sem parâmetros que se destinam a colunas criptografadas.| Os resultados das colunas criptografadas são descriptografados de modo transparente. O aplicativo recebe valores de texto sem formatação dos tipos de dados JDBC correspondentes aos tipos de SQL Server configurados para as colunas criptografadas. | Erro | Os resultados das colunas criptografadas não são descriptografados. O aplicativo recebe valores criptografados como matrizes de bytes (byte[]).
      
 
### <a name="inserting-and-retrieving-encrypted-data-examples"></a>Inserir e recuperar os dados criptografados exemplos 
Os exemplos a seguir ilustram como recuperar e modificar dados em colunas criptografadas. Os exemplos pressupõem a tabela de destino com o esquema abaixo. Observe que as colunas SSN e BirthDate estão criptografadas.

```
CREATE TABLE [dbo].[Patients]([PatientId] [int] IDENTITY(1,1), 
 [SSN] [char](11) COLLATE Latin1_General_BIN2 
 ENCRYPTED WITH (ENCRYPTION_TYPE = DETERMINISTIC, 
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256', 
 COLUMN_ENCRYPTION_KEY = MyCEK) NOT NULL,
 [FirstName] [nvarchar](50) NULL,
 [LastName] [nvarchar](50) NULL, 
 [BirthDate] [date] 
 ENCRYPTED WITH (ENCRYPTION_TYPE = RANDOMIZED, 
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256', 
 COLUMN_ENCRYPTION_KEY = MyCEK) NOT NULL
 PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY])
 GO
```
 
### <a name="inserting-data-example"></a>Inserindo um exemplo de dados

Este exemplo insere uma linha na tabela Pacientes. Observe o seguinte:
- Não há nada específico de criptografia no código de exemplo. O Microsoft JDBC Driver para SQL Server detecta automaticamente e criptografa os parâmetros que se destinam a colunas criptografadas. Isso torna a criptografia transparente para o aplicativo. 
- Os valores inseridos em colunas de banco de dados, incluindo as colunas criptografadas, são passados como parâmetros usando SQLServerPreparedStatement. Embora o uso de parâmetros é opcional ao enviar valores para colunas não criptografadas (embora, é altamente recomendado, pois ajuda a prevenir a injeção de SQL), é necessário para valores que se destinam a colunas criptografadas. Se os valores inseridos em colunas criptografadas foram passados como literais inseridos na instrução de consulta, a consulta falhará porque o Microsoft JDBC Driver para SQL Server não poderá determinar os valores em colunas criptografadas de destino, portanto, não seria Criptografe os valores. Como resultado, o servidor os rejeitaria como incompatíveis com as colunas criptografadas.
- Todos os valores impressos pelo programa será em texto sem formatação, como o Microsoft JDBC Driver para SQL Server descriptografará de modo transparente os dados recuperados da colunas criptografadas.
- Se você estiver fazendo uma pesquisa usando onde cláusula, o valor usado na cláusula WHERE deve ser passado como um parâmetro, para que o Microsoft JDBC Driver para SQL Server possa transparentemente criptografá-lo antes de enviá-la para o banco de dados. No exemplo a seguir, observe que SSN é passado como um parâmetro, mas o sobrenome é passado como um literal como LastName não criptografada.
- O método setter usado para o parâmetro destina à coluna SSN é setString(), que mapeia para o tipo de dados do SQL Server char/varchar. Se, para esse parâmetro, o método setter usado foi setNString(), que é mapeada para nchar/nvarchar, a consulta falhará, pois sempre criptografado não oferece suporte a conversões de valores nchar/nvarchar criptografados em valores char/varchar criptografados.  

```
String connectionString = "jdbc:sqlserver://localhost:1433;databaseName=Clinic;user=sa;password=******;columnEncryptionSetting=Enabled;";
try  
{           
     Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
     try (Connection sourceConnection = DriverManager.getConnection(connectionString))  
     {                  
        String insertRecord="INSERT INTO [dbo].[Patients] VALUES (?, ?, ?, ?)";        
        try (PreparedStatement insertStatement = sourceConnection.prepareStatement(insertRecord))  
        {
            insertStatement.setString(1, "795-73-9838");  
            insertStatement.setString(2, "Catherine");   
            insertStatement.setString(3, "Abel");                   
            insertStatement.setDate(4, Date.valueOf("1996-09-10"));  
            insertStatement.executeUpdate();  
            System.out.println("1 record inserted.\n");  
        }         
     }  
}  
catch (Exception e)  
{  
    e.printStackTrace();  
}
```

### <a name="retrieving-plaintext-data-example"></a>Recuperando um exemplo de dados de texto sem formatação

O exemplo a seguir demonstra a filtragem de dados com base em valores criptografados e a recuperação de dados de texto sem formatação de colunas criptografadas. Observe o seguinte:
- O valor usado na cláusula WHERE para filtrar a coluna SSN precisa ser passado como um parâmetro, para que o Microsoft JDBC Driver para SQL Server pode criptografá-lo transparente antes de enviá-la para o banco de dados.
- Todos os valores impressos pelo programa será em texto sem formatação, como o Microsoft JDBC Driver para SQL Server descriptografará de modo transparente os dados recuperados das colunas SSN e BirthDate.

> [!NOTE]  
>  Consultas podem executar comparações de igualdade em colunas se forem criptografados usando a criptografia determinística. Para obter mais informações, consulte o **criptografia selecionando determinística ou aleatória** seção o [sempre criptografados (mecanismo de banco de dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) tópico.  

```
String connectionString =  "jdbc:sqlserver://localhost:1433;databaseName=Clinic;user=sa;password=******;columnEncryptionSetting=Enabled;" ;
String filterRecord="SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN = ?;";  

try (PreparedStatement selectStatement = sourceConnection.prepareStatement(filterRecord))  
{  
    selectStatement.setString(1, "795-73-9838");  
    ResultSet rs = selectStatement.executeQuery();   
    while(rs.next()) 
    {  
    System.out.println("SSN: " +rs.getString("SSN") + 
    ", FirstName: " + rs.getString("FirstName") + 
    ", LastName:"+ rs.getString("LastName")+
     ", Date of Birth: " + rs.getString("BirthDate"));  
          }  
}
catch (Exception e)  
{  
    e.printStackTrace();  
}
```
  
### <a name="retrieving-encrypted-data-example"></a>Recuperando um exemplo de dados criptografados

Se o Always Encrypted não estiver habilitado, uma consulta ainda poderá recuperar dados de colunas criptografadas, desde que a consulta não tenha parâmetros que se destinam a colunas criptografadas.

Os exemplos a seguir ilustram como recuperar dados binários criptografados de colunas criptografadas. Observe o seguinte:

- Como o Sempre Criptografado não está habilitado na cadeia de conexão, a consulta retornará valores criptografados de SSN e BirthDate como matrizes de bytes (o programa converte os valores em cadeias de caracteres).
- Uma consulta que recupera dados de colunas criptografadas com o Sempre Criptografado desabilitado pode ter parâmetros, desde que nenhum dos parâmetros se destinem a uma coluna criptografada. A consulta acima filtra por LastName, que não é criptografado no banco de dados. Se a consulta filtrar por SSN ou BirthDate, a consulta falhará.

```
String connectionString  = "jdbc:sqlserver://localhost:1433;" + "databaseName=Clinic;user=sa;password=******";

String filterRecord="SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE LastName = ?;"; 
 
try (PreparedStatement selectStatement = sourceConnection.prepareStatement(filterRecord))  
{  
    selectStatement.setString(1, "Abel");  
    ResultSet rs = selectStatement.executeQuery();   
    while(rs.next())
    {  
        System.out.println("SSN: " + rs.getString("SSN") +
         ", FirstName: " + rs.getString("FirstName") + 
        ", LastName:"+ rs.getString("LastName")+ 
        ", Date of Birth: " + rs.getString("BirthDate"));  
    } 
}  
catch (Exception e)  
{  
    e.printStackTrace();  
}
```

### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>Evitando problemas comuns ao consultar colunas criptografadas

Esta seção descreve as categorias de erros comuns ao consultar colunas criptografadas de aplicativos Java e algumas diretrizes sobre como evitá-los.

### <a name="unsupported-data-type-conversion-errors"></a>Erros de conversão de tipo de dados sem suporte

O Always Encrypted dá suporte a algumas conversões de tipos de dados criptografados. Consulte [sempre criptografados (mecanismo de banco de dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) para a lista detalhada de conversões de tipo com suporte. Isto é o que você pode fazer para evitar erros de conversão de tipo de dados, garantindo que:

- use os métodos de setter apropriado ao passar valores para parâmetros de direcionamento colunas criptografadas, para que o tipo de dados do SQL Server do parâmetro seja exatamente como o tipo de coluna de destino ou uma conversão do tipo de dados do SQL Server do parâmetro para o destino há suporte para o tipo da coluna. Observe que foram adicionados novos métodos da API para classes SQLServerPreparedStatement e SQLServerCallableStatement de SQLServerResultSet para passar parâmetros correspondentes aos tipos de dados específicos do SQL Server. Por exemplo, se uma coluna será criptografada pode usar o método setTimestamp() para passar um parâmetro para um datetime2 ou para uma coluna de data e hora. Mas, quando uma coluna é criptografada, será necessário usar o método exato que representa o tipo da coluna no banco de dados. Por exemplo, use setTimestamp() para passar valores para uma coluna criptografada datetime2 e use setDateTime() para passar valores para uma coluna de datetime criptografados. Consulte [sempre criptografados referência da API para o Driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md) para obter uma lista de novas APIs. 
- a precisão e escala dos parâmetros que se destinam a colunas dos tipos de dados decimais e numéricos do SQL Server são iguais à precisão e escala configuradas para a coluna de destino. Observe que foram adicionados novos métodos da API para classes SQLServerPreparedStatement e SQLServerCallableStatement de SQLServerResultSet para aceitar a precisão e escala juntamente com os valores de dados para parâmetros/colunas que representam os tipos de dados decimais e numéricos. Consulte [sempre criptografados referência da API para o Driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md) para obter uma lista completa das APIs novo/sobrecarregado.  
- a precisão ou escala de frações de segundo de parâmetros que se destinam a colunas datetime2, datetimeoffset ou tipos de dados do SQL Server de tempo não é maior do que para a coluna de destino, em consultas que modificam os valores da coluna de destino. Observe que foram adicionados novos métodos da API para classes SQLServerPreparedStatement e SQLServerCallableStatement de SQLServerResultSet para aceitar a precisão ou escala de frações de segundo juntamente com os valores de dados para parâmetros que representam esses tipos de dados. Consulte [sempre criptografados referência da API para o Driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md) para obter uma lista completa das APIs novo/sobrecarregado.   

### <a name="errors-due-to-incorrect-connection-properties"></a>Erros devido a propriedades de Conexão incorreta
Esta seção descreve como definir as configurações de conexão corretamente para usar dados de sempre criptografado. Como tipos de dados criptografados oferece suporte a conversões limitados, as configurações de conexão 'sendTimeAsDatetime' e 'sendStringParametersAsUnicode' precisam de configuração adequada ao usar colunas criptografadas. Verifique se: 
- [sendTimeAsDatetime](https://msdn.microsoft.com/library/ff427224(v=sql.110).aspx) configuração de conexão é definida como false quando inserindo dados em colunas de hora criptografadas. Para obter mais informações, consulte a seção 'Configurar como os valores são enviados para o servidor'.
- [sendStringParametersAsUnicode](../../connect/jdbc/setting-the-connection-properties.md) configuração de conexão está definida como true (ou será deixada como o padrão) quando inserindo dados em colunas criptografadas, char/varchar/varchar(max). Para obter mais informações, consulte a seção 'Configurar como os valores de cadeia de caracteres são enviados para o servidor'.

### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>Erros devido a passar o texto não criptografado em vez de valores criptografados

Qualquer valor que se destina a uma coluna criptografada precisa ser criptografado no aplicativo. Uma tentativa de inserir/modificar ou de filtrar por um valor de texto sem formatação em uma coluna criptografada resultará em um erro semelhante a este:


```
com.microsoft.sqlserver.jdbc.SQLServerException: Operand type clash: varchar is incompatible with varchar(8000) encrypted with (encryption_type = 'DETERMINISTIC', encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'MyCEK', column_encryption_key_database_name = 'ae') collation_name = 'SQL_Latin1_General_CP1_CI_AS'
```

Para evitar esses tipos de erros, garanta que:
- sempre criptografado está habilitado para consultas de aplicativo direcionamento colunas criptografadas (para a cadeia de caracteres de conexão ou para uma consulta específica).
- use as instruções preparadas e parâmetros para enviar dados de direcionamento a colunas criptografadas. O exemplo abaixo mostra uma consulta que filtra incorretamente por uma literal ou uma constante em uma coluna criptografada (SSN), em vez de passar a literal interna como um parâmetro. Essa consulta falhará.

```
ResultSet rs = connection.createStatement().executeQuery("SELECT * FROM Customers WHERE SSN='795-73-9838'");  
```

## <a name="working-with-column-master-key-stores"></a>Trabalhando com repositórios de chaves mestras de coluna
Para criptografar um valor de parâmetro ou descriptografar dados nos resultados da consulta, o Microsoft JDBC Driver para SQL Server precisa obter uma chave de criptografia de coluna que está configurada para a coluna de destino. Chaves de criptografia de coluna são armazenadas em formato criptografado nos metadados do banco de dados. Cada chave de criptografia de coluna tem uma chave mestra de coluna correspondente que foi usada para criptografar a chave de criptografia de coluna. Os metadados do banco de dados não armazenam as chaves mestras de coluna – eles contêm apenas as informações sobre um repositório de chaves que contém uma chave mestra de coluna específica e a localização da chave no repositório de chaves.

Para obter um valor de texto sem formatação de uma chave de criptografia de coluna, o Microsoft JDBC Driver para SQL Server primeiro obtém os metadados sobre a chave de criptografia de coluna e sua chave mestra de coluna correspondente e, em seguida, ele usa as informações nos metadados de entrar em contato com a chave repositório, que contém a chave mestra de coluna e descriptografar a chave de criptografia de coluna criptografada. O Microsoft JDBC Driver para SQL Server se comunica com um repositório de chaves usando um provedor de repositório de chaves mestras de coluna – que é uma instância de uma classe derivado de **SQLServerColumnEncryptionKeyStoreProvider** classe.


### <a name="using-built-in-column-master-key-store-providers"></a>Usando provedores internos de repositórios de chaves mestras de coluna
  
O Microsoft JDBC Driver para SQL Server vem com os seguintes provedores de armazenamento de chave mestra de coluna interna. Observe que, alguns desses provedores são pré-registrados com os nomes de provedor específico (usados para pesquisar o provedor), e alguns exigir credenciais adicionais ou registro explícito.

| Classe | Descrição | Nome (de pesquisa) do provedor |Pré-registrados?|
|:---|:---|:---|:---|
|**SQLServerColumnEncryptionAzureKeyVaultProvider**| Um provedor para um repositório de chaves para o Cofre de chaves do Azure.| AZURE_KEY_VAULT|Não|
|**SQLServerColumnEncryptionCertificateStoreProvider**| Um provedor para o repositório de certificados do Windows.|MSSQL_CERTIFICATE_STORE|Sim
|**SQLServerColumnEncryptionJavaKeyStoreProvider**| Um provedor de armazenamento de chaves Java|MSSQL_JAVA_KEYSTORE|Sim|

Para os provedores de repositório de chaves previamente registrado não é necessário fazer alterações de código do aplicativo para usar estes provedores, mas observe o seguinte:

- Você (ou seu DBA) precisa verificar se o nome do provedor, configurado nos metadados da chave mestra de coluna, está correto e se o caminho da chave mestra de coluna está em conformidade com o formato do caminho da chave válido para determinado provedor. É recomendável configurar as chaves usando ferramentas como o SQL Server Management Studio, que gera automaticamente os nomes de provedor válidos e os caminhos de chaves ao emitir a instrução CREATE COLUMN MASTER KEY (Transact-SQL).
- Você precisa garantir que seu aplicativo pode acessar a chave no repositório de chaves. Isso pode envolver a concessão de acesso para o aplicativo à chave e/ou ao repositório de chaves, dependendo do repositório de chaves, ou a execução de outras etapas de configuração específicas do repositório de chaves. Por exemplo, para usar o SQLServerColumnEncryptionJavaKeyStoreProvider você precisa fornecer o local e a senha da chave de armazenamento nas propriedades de conexão. 

Todos esses provedores de repositório de chaves são descritos em mais detalhes abaixo.
  
### <a name="using-azure-key-vault-provider"></a>Usando o Provedor do Cofre de Chaves do Azure
O Cofre de Chaves do Azure é uma opção conveniente para armazenar e gerenciar chaves mestras de coluna do Always Encrypted (especialmente se seus aplicativos estiverem hospedados no Azure). O Microsoft JDBC Driver para SQL Server inclui um provedor interno, SQLServerColumnEncryptionAzureKeyVaultProvider, para aplicativos que têm chaves armazenadas no cofre de chaves do Azure. O nome deste provedor é AZURE_KEY_VAULT. Para usar o provedor de armazenamento de Cofre de chaves do Azure, um desenvolvedor de aplicativos precisa criar o cofre e as chaves no Azure e configurar o aplicativo para acessar as chaves. Para obter mais informações sobre como configurar o Cofre de chaves e criar a chave mestra de coluna consulte [Cofre de chaves do Azure – passo a passo para obter mais informações sobre como configurar o Cofre de chaves](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/) e [Criando chaves mestras de coluna no cofre de chaves do Azure](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_2).  
  
Para usar o Cofre de chaves do Azure, os aplicativos cliente precisam instanciar o SQLServerColumnEncryptionAzureKeyVaultProvider e registrá-lo com o driver. A autenticação de representantes do driver JDBC para o aplicativo por meio de uma interface chamado SQLServerKeyVaultAuthenticationCallback que tem um método para recuperar um token de acesso do Cofre de chaves. Para instanciar o provedor de armazenamento de Cofre de chaves do Azure, o desenvolvedor do aplicativo deve fornecer uma implementação para o único método chamado **getAccessToken** que recupera o token de acesso para a chave armazenada no cofre de chaves do Azure.  
  
Aqui está um exemplo de inicialização SQLServerKeyVaultAuthenticationCallback e SQLServerColumnEncryptionAzureKeyVaultProvider:  
  
```  
// String variables clientID and clientSecret hold the client id and client secret values respectively.  
  
ExecutorService service = Executors.newFixedThreadPool(10);  
SQLServerKeyVaultAuthenticationCallback authenticationCallback = new SQLServerKeyVaultAuthenticationCallback() {  
       @Override  
    public String getAccessToken(String authority, String resource, String scope) {  
        AuthenticationResult result = null;  
        try{  
                AuthenticationContext context = new AuthenticationContext(authority, false, service);  
            ClientCredential cred = new ClientCredential(clientID, clientSecret);  
  
            Future<AuthenticationResult> future = context.acquireToken(resource, cred, null);  
            result = future.get();  
        }  
        catch(Exception e){  
            e.printStackTrace();  
        }  
        return result.getAccessToken();  
    }  
};  
  
SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(authenticationCallback, service);  
  
```

Depois que o aplicativo cria uma instância de SQLServerColumnEncryptionAzureKeyVaultProvider, o aplicativo precisa registrar a instância no Microsoft JDBC Driver para SQL Server usando o Método registercolumnencryptionkeystoreproviders (). É altamente recomendável, a instância está registrada usando o nome de pesquisa padrão, AZURE_KEY_VAULT, que pode ser obtida chamando a API SQLServerColumnEncryptionAzureKeyVaultProvider.getName(). Usando o nome padrão, permitirá que você use ferramentas, como o SQL Server Management Studio ou o PowerShell, para provisionar e gerenciar chaves Always Encrypted (ferramentas de usam o nome padrão para gerar o objeto de metadados para a chave mestra de coluna). O exemplo abaixo mostra o registro do provedor de Cofre de chaves do Azure. Para obter mais detalhes sobre o método registercolumnencryptionkeystoreproviders (), consulte [sempre criptografados referência da API para o Driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md). 

```
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();   
keyStoreMap.put(akvProvider.getName(), akvProvider);   
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);   
```
  
> [!IMPORTANT]  
>  A implementação do Cofre de chaves do Azure do driver JDBC tem dependências nessas bibliotecas (do GitHub):  
>   
>  [sdk do Azure para java](https://github.com/Azure/azure-sdk-for-java)  
>   
>  [bibliotecas do Azure Active Directory library para java](https://github.com/AzureAD/azure-activedirectory-library-for-java)  
  
### <a name="using-windows-certificate-store-provider"></a>Usando o provedor de repositório de certificados do Windows
O SQLServerColumnEncryptionCertificateStoreProvider pode ser usado para armazenar chaves mestras de coluna no repositório de certificados do Windows. Use o Assistente do SQL Server Management Studio (SSMS) sempre criptografado ou outras ferramentas com suporte para criar a chave mestra de coluna e a criptografia de coluna definições de chave no banco de dados. O mesmo assistente pode ser usado para gerar um certificado autoassinado no repositório de certificados Windows ser usada como uma chave mestra de coluna para os dados sempre criptografados. Para obter mais informações sobre a chave mestra de coluna e criptografia de coluna chave sintaxe do T-SQL visite [CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md) e [criar chave de criptografia de coluna](../../t-sql/statements/create-column-encryption-key-transact-sql.md) respectivamente.

O nome do SQLServerColumnEncryptionCertificateStoreProvider é "MSSQL_CERTIFICATE_STORE" e pode ser consultado com o API GetName do objeto de provedor. Ele é registrado automaticamente pelo driver e pode ser usado diretamente sem qualquer alteração de aplicativo.

> [!IMPORTANT]  
>  A implementação SQLServerColumnEncryptionCertificateStoreProvider do driver JDBC está disponível com sistemas operacionais somente Windows e tem uma dependência de sqljdbc_auth.dll que está disponível no pacote de driver.  Para usar esse provedor, copie o arquivo sqljdbc_auth.dll para um diretório no caminho do sistema Windows no computador onde o driver JDBC está instalado. Como alternativa, você pode definir a propriedade do sistema java.libary.path para especificar o diretório de sqljdbc_auth.dll. Se você estiver executando uma Máquina Virtual Java (JVM) de 32 bits, use o arquivo sqljdbc_auth.dll na pasta x86, mesmo se o sistema operacional for a versão x64. Se estiver executando uma JVM de 64 bits em um processador x64, use o arquivo sqljdbc_auth.dll na pasta x64. Por exemplo, se você estiver usando o JVM de 32 bits e o driver JDBC está instalado no diretório padrão, você pode especificar o local da DLL usando o seguinte argumento de máquina virtual (VM) quando o aplicativo Java for iniciado:  
`-Djava.library.path=C:\Microsoft JDBC Driver <version> for SQL Server\sqljdbc_<version>\enu\auth\x86`
        
### <a name="using-java-key-store-provider"></a>Usando o provedor de armazenamento de chaves Java  
O driver JDBC vem com uma chave criada no repositório de implementação de provedor para o repositório de chaves Java. O driver automaticamente cria e registra o provedor de armazenamento de chaves Java, se o **keyStoreAuthentication** propriedade de cadeia de caracteres de conexão está presente na cadeia de conexão e é definida como "JavaKeyStorePassword" (por favor, consulte mais detalhes abaixo). O nome do provedor de repositório de chaves Java é MSSQL_JAVA_KEYSTORE. Esse nome também pode ser consultado pela API do SQLServerColumnEncryptionJavaKeyStoreProvider.getName(). 

Três novas conexão cadeia palavras-chave são introduzidas para permitir que um aplicativo cliente especificar declarativamente as credenciais que o driver precisa para autenticar para o repositório de chaves Java. O driver deve inicializar o provedor, com base nos valores das seguintes três propriedades de cadeia de conexão, para as conexões específicas. 
  
 **keyStoreAuthentication:** identifica o repositório de chave a ser usado. Com o Microsoft JDBC Driver 6.0 para SQL Server, você pode autenticar para o repositório de chaves Java apenas através desta propriedade. Para o repositório de chaves Java, o valor dessa propriedade deve ser "JavaKeyStorePassword".   
  
 **keyStoreLocation:** o caminho para o arquivo de armazenamento de chaves Java que armazena a chave mestra de coluna. Observe que o caminho inclui o nome do arquivo de armazenamento de chaves.  
  
 **keyStoreSecret:** a segredo/senha a ser usada para o armazenamento de chaves, bem como para a chave. Observe que para usar o repositório de chave Java o armazenamento de chaves e a senha da chave deve ser o mesmo.  

Aqui está um exemplo sobre como fornecer essas credenciais na cadeia de caracteres de conexão:

    String connectionString = "jdbc:sqlserver://localhost;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path_to_the_keystore_file>;keyStoreSecret=<keystore_key_password>";
    
Essas configurações também podem ser definir/obter usando o objeto SQLServerDataSource. Consulte [sempre criptografados referência da API para o Driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md) para obter mais informações.     
  
O driver JDBC cria automaticamente o SQLServerColumnEncryptionJavaKeyStoreProvider quando essas credenciais estão presentes nas propriedades de conexão. 
  
### <a name="creating-a-column-master-key-for-the-java-key-store"></a>Criando uma chave mestra de coluna para o repositório de chaves Java
O SQLServerColumnEncryptionJavaKeyStoreProvider pode ser usado com tipos de armazenamento de chaves JKS ou PKCS12. Para criar ou importar uma chave para uso com este provedor de usar o Java [keytool](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html) utilitário. Observe que a chave deve ter a mesma senha que o armazenamento de chaves em si. Aqui está um exemplo de como criar uma chave pública e a chave privada associada usando o utilitário keytool.

    keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.jks -storepass mypassword -validity 360 -keysize 2048 -storetype jks    

Este comando cria uma chave pública e organize-os em um x. 509 certificado que é armazenado no armazenamento de chaves jks junto com chave de particular associada é autoassinado. Esta entrada no armazenamento de chaves é identificada pelo alias 'AlwaysEncryptedKey'. 

Aqui está um exemplo do mesmo usando um storetype PKCS12. 

    keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.pfx -storepass mypassword -validity 360 -keysize 2048 -storetype pkcs12 -keypass mypassword   

Observe que, se o armazenamento de chaves é do tipo PKCS12, o utilitário keytool não solicitará a senha da chave e a senha da chave deve ser fornecido com a opção - keypass conforme o SQLServerColumnEncryptionJavaKeyStoreProvider requer que o armazenamento de chaves e a chave tenham o mesma senha.

Você também pode exportar um certificado do repositório de certificados do Windows no formato. pfx e usá-lo com o SQLServerColumnEncryptionJavaKeyStoreProvider. O certificado exportado também pode ser importado para o repositório de chaves Java como um tipo de armazenamento de chaves JKS. 

Depois de criar a entrada de keytool, você precisará criar os metadados de chave mestra de coluna no banco de dados que precisa do nome do provedor de repositório de chaves e o caminho da chave. Para obter mais informações sobre como criar metadados de chave mestra de coluna visite [CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md). Para SQLServerColumnEncryptionJavaKeyStoreProvider, o caminho da chave é apenas o alias da chave. E o nome de SQLServerColumnEncryptionJavaKeyStoreProvider é 'MSSQL_JAVA_KEYSTORE'. Você também pode consultar esse nome usando a API pública GetName da classe SQLServerColumnEncryptionJavaKeyStoreProvider. 

A sintaxe do T-SQL para criar a chave mestra de coluna é:

```  
CREATE COLUMN MASTER KEY [<CMK_name>]  
WITH  
(  
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',  
    KEY_PATH = N'<key_alias>'  
)  
```  

Para o 'AlwaysEncryptedKey' criado acima, a definição da chave mestra de coluna deve ser:

```  
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'AlwaysEncryptedKey'
)
```  
    
> [!NOTE]  
>  Interna no SQL Server a funcionalidade Studio da gerenciamento não é possível criar colunas definições de chave mestra para o repositório de chaves Java para o qual você deve usar o comando T-SQL.  
  
### <a name="creating-a-column-encryption-key-for-the-java-key-store"></a>Criando uma chave de criptografia de coluna para o repositório de chaves Java
Observe que o SQL Server management Studio ou qualquer outra ferramenta não pode ser usada para criar a coluna de chaves de criptografia usando chaves mestras de coluna no repositório de chave Java. O aplicativo cliente deve criar a chave de criptografia de coluna programaticamente usando a classe SQLServerColumnEncryptionJavaKeyStoreProvider. Para obter mais detalhes, visite a seção 'Usando coluna chave mestra de provedores de armazenamento para o provisionamento programático de chave'. 

  
### <a name="implementing-a-custom-column-master-key-store-provider"></a>Implementando um provedor personalizado de repositórios de chaves mestras de coluna
Se você deseja armazenar chaves mestras de coluna em um repositório de chaves que não é suportado por um provedor existente, você pode implementar um provedor personalizado estendendo a classe SQLServerColumnEncryptionKeyStoreProvider e registrando o provedor usando o Método registercolumnencryptionkeystoreproviders ().
  
```  
public class MyCustomKeyStore extends SQLServerColumnEncryptionKeyStoreProvider{  
    private String name = "MY_CUSTOM_KEYSTORE";
    
    public void setName(String name)
    {
        this.name = name;
    }
    
    public String getName()
    {
        return name;
    }

    public byte[] encryptColumnEncryptionKey(String masterKeyPath, String encryptionAlgorithm, byte[] plainTextColumnEncryptionKey)  
    {  
        // Logic for encrypting the column encryption key  
    }  
    
    public byte[] decryptColumnEncryptionKey(String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)  
    {  
        // Logic for decrypting the column encryption key  
    }  
}  
  
```  
  
 Registre o provedor:  
  
```  
SQLServerColumnEncryptionKeyStoreProvider storeProvider = new MyCustomKeyStore();  
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();  
keyStoreMap.put(storeProvider.getName(), storeProvider);  
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);  
  
```  
  
## <a name="using-column-master-key-store-providers-for-programmatic-key-provisioning"></a>Usando provedores de repositórios de chaves mestras de coluna para o provisionamento programático de chaves

Ao acessar colunas criptografadas, o Microsoft JDBC Driver para SQL Server encontra transparente e chama o provedor de armazenamento de chave mestra de coluna da direita para descriptografar as chaves de criptografia de coluna. Normalmente, o código normal do aplicativo não chama diretamente os provedores de repositórios de chaves mestras de coluna. No entanto, é possível criar uma instância e chamar um provedor de forma explícita para provisionar de modo programático e gerenciar chaves do Sempre Criptografado: para gerar uma chave de criptografia de coluna criptografada e descriptografar uma chave de criptografia de coluna (por exemplo, como a rotação de chave mestra de coluna da parte). Para obter mais informações, consulte [Overview of Key Management for Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)(Visão geral do gerenciamento de chaves do Sempre Criptografado).
Observe que a implementação de suas próprias ferramentas de gerenciamento de chaves poderá ser necessária apenas se você usar um provedor personalizado de repositórios de chaves. Ao usar chaves armazenadas no repositório de certificados do Windows ou no cofre de chaves do Azure, você pode usar as ferramentas existentes, como o SQL Server Management Studio ou o PowerShell, para gerenciar e provisionar as chaves. Ao usar chaves armazenadas no repositório de chave Java, você precisa provisionar chaves programaticamente. O exemplo abaixo, ilustra o uso de classe SQLServerColumnEncryptionJavaKeyStoreProvider para criptografar a chave com uma chave armazenada no repositório de chave Java.

```  
import java.sql.*;
import javax.xml.bind.DatatypeConverter;
import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionJavaKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerException;

/**
 * This program demonstrates how to create a column encryption key programatically for the Java Key Store.
 */
public class AlwaysEncrypted
{
    // Alias of the key stored in the keystore.
    private static String keyAlias = "<proide key alias>";

    // Name by which the column master key will be known in the database.
    private static String columnMasterKeyName = "MyCMK";

    // Name by which the column encryption key will be known in the database.
    private static String columnEncryptionKey = "MyCEK";

    // The location of the keystore. 
    private static String keyStoreLocation = "C:\\Dev\\Always Encrypted\\keystore.jks";

    // The password of the keystore and the key.
    private static char[] keyStoreSecret = "********".toCharArray();

    /**
     * Name of the encryption algorithm used to encrypt the value of
     * the column encryption key. The algorithm for the system providers must be RSA_OAEP.
     */
    private static String algorithm = "RSA_OAEP";

    public static void main(String[] args)
    {
        String connectionString = GetConnectionString();
        try
        {
            // Note: if you are not using try-with-resources statements (as here),
            // you must remember to call close() on any Connection, Statement,
            // ResultSet objects that you create.

            // Open a connection to the database.
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
            try (Connection sourceConnection = DriverManager.getConnection(connectionString))
            {
                // Instantiate the Java Key Store provider.
                SQLServerColumnEncryptionKeyStoreProvider storeProvider = 
                        new SQLServerColumnEncryptionJavaKeyStoreProvider(
                                keyStoreLocation,
                                keyStoreSecret);

                byte [] encryptedCEK=getEncryptedCEK(storeProvider);

                /**
                 * Create column encryption key 
                 * For more details on the syntax refer: 
                 * https://msdn.microsoft.com/library/mt146372.aspx
                 * Encrypted column encryption key first needs to be converted into varbinary_literal from bytes, 
                 * for which DatatypeConverter.printHexBinary is used
                 */
                String createCEKSQL = "CREATE COLUMN ENCRYPTION KEY " 
                        + columnEncryptionKey
                        + " WITH VALUES ( "
                        + " COLUMN_MASTER_KEY = " 
                        + columnMasterKeyName
                        + " , ALGORITHM =  '" 
                        + algorithm
                        + "' , ENCRYPTED_VALUE =  0x" 
                        + DatatypeConverter.printHexBinary(encryptedCEK)
                        + " ) ";

                try (Statement cekStatement = sourceConnection.createStatement())
                {
                    cekStatement.executeUpdate(createCEKSQL);
                    System.out.println("Column encryption key created with name : " + columnEncryptionKey);
                }
            }
        }
        catch (Exception e)
        {
            // Handle any errors that may have occurred.
            e.printStackTrace();
        }
    }

    // To avoid storing the sourceConnection String in your code,
    // you can retrieve it from a configuration file.
    private static String GetConnectionString()
    {

        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://localhost:1433;" +
                "databaseName=ae2;user=sa;password=********;";

        return connectionUrl;
    }

    private static byte[] getEncryptedCEK(SQLServerColumnEncryptionKeyStoreProvider storeProvider) throws SQLServerException
    {
        /**
         * Following arguments needed by  SQLServerColumnEncryptionJavaKeyStoreProvider
         * 1) keyStoreLocation : 
         *      Path where keystore is located, including the keystore file name. 
         * 2) keyStoreSecret : 
         *      Password of the keystore and the key.  
         */
        String plainTextKey = "You need to give your plain text";

        // plainTextKey has to be 32 bytes with current algorithm supported
        byte[] plainCEK = plainTextKey.getBytes();

        // This will give us encrypted column encryption key in bytes
        byte[] encryptedCEK = storeProvider.encryptColumnEncryptionKey(
                keyAlias,
                algorithm,
                plainCEK);

        return encryptedCEK;
    }
}

```  
  
## <a name="force-encryption-on-input-parameters"></a>Forçar a criptografia em parâmetros de entrada
  
O recurso de Forçar criptografia impõe a criptografia de um parâmetro ao usar sempre criptografado. Se Forçar criptografia for usada e SQL Server informar o driver que o parâmetro não precisam ser criptografados, a consulta usando o parâmetro falhará. Essa propriedade fornece proteção adicional contra ataques de segurança que envolvem um SQL Server comprometido fornecendo metadados de criptografia incorretos ao cliente, o que pode levar à divulgação de dados. Os métodos em classes SQLServerPreparedStatement e SQLServerCallableStatement e a atualização de conjunto *\* métodos na classe SQLServerResultSet estão sobrecarregados para aceitar um argumento booliano para especificar a configuração de criptografia de força. Se o valor desse argumento for false, o driver não forçará a criptografia em parâmetros. Se Forçar criptografia for definida como true, a consulta parâmetro será enviado somente se a coluna de destino está criptografada e sempre criptografado está habilitado, a conexão ou a instrução. Isso fornece uma camada extra de segurança, garantindo que nenhum dado é por engano enviado para o SQL Server como texto sem formatação quando se espera que sejam criptografados.  
  
 Para obter mais informações sobre os métodos SQLServerPreparedStatement e SQLServerCallableStatement que estão sobrecarregados com a configuração de criptografia de força, consulte [sempre criptografados referência da API para o Driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)  

## <a name="controlling-performance-impact-of-always-encrypted"></a>Controlando o impacto no desempenho do Sempre Criptografado

Como o Sempre Criptografado é uma tecnologia de criptografia do lado do cliente, a maioria das sobrecargas devido ao desempenho é observada no lado do cliente, não no banco de dados. Além do custo das operações de criptografia e descriptografia, as outras fontes de sobrecarga devido ao desempenho no lado do cliente são:
- Viagens de ida e volta adicionais ao banco de dados para recuperar metadados dos parâmetros de consulta.
- Chamadas a um repositório de chaves mestras de coluna para acessar uma chave mestra de coluna.

Esta seção descreve as otimizações de desempenho internas no Microsoft JDBC Driver para SQL Server e como você pode controlar o impacto de dois fatores acima no desempenho.

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>Controlando as viagens de ida e volta para recuperar metadados dos parâmetros de consulta

Se o sempre criptografado está habilitado para uma conexão, por padrão, o Microsoft JDBC Driver para SQL Server chamará [sp_describe_parameter_encryption](https://msdn.microsoft.com/library/mt631693.aspx?f=255&MSPPError=-2147217396) para cada consulta parametrizada, passando a instrução de consulta (sem nenhuma valores de parâmetro) para o SQL Server. [sys. sp_describe_parameter_encryption](https://msdn.microsoft.com/library/mt631693.aspx?f=255&MSPPError=-2147217396) analisa a instrução de consulta para descobrir se os parâmetros precisam ser criptografados, e se assim, para cada um, ele retorna as informações relacionadas à criptografia que permitirão o Microsoft JDBC Driver para SQL Server para criptografar valores de parâmetro. O comportamento acima garante um alto nível de transparência para o aplicativo cliente. O aplicativo (e o desenvolvedor do aplicativo) não precisam estar ciente de quais consultas acessam colunas criptografadas, desde que os valores que se destinam a colunas criptografadas são passados para o Microsoft JDBC Driver para SQL Server como parâmetros.


#### <a name="setting-always-encrypted-at-the-query-level"></a>Configurando o Always Encrypted no nível da consulta

Para controlar o impacto no desempenho da recuperação de metadados de criptografia para consultas parametrizadas, é possível habilitar o Always Encrypted para consultas individuais, em vez de configurá-lo para a conexão. Assim, você pode garantir que sys.sp_describe_parameter_encryption é invocado apenas para consultas que você sabe que têm parâmetros que se destinam a colunas criptografadas. No entanto, observe que, ao fazer isso, você reduzirá a transparência da criptografia: se você alterar as propriedades de criptografia das colunas de banco de dados, talvez seja necessário alterar o código do aplicativo para alinhá-lo com as alterações de esquema.


Para controlar o comportamento do sempre criptografado de consultas individuais, você precisa configurar objetos de instrução individual passando um Enum, SQLServerStatementColumnEncryptionSetting, que especifica como os dados serão enviados e recebidos durante a leitura e gravação colunas criptografadas para essa instrução específica. Veja algumas diretrizes úteis:
- Se a maioria das consultas que um aplicativo cliente envia por uma conexão de banco de dados acessa colunas criptografadas:
    - Defina a palavra-chave de cadeia de caracteres do columnEncryptionSetting conexão como habilitado.
    - Defina SQLServerStatementColumnEncryptionSetting.Disabled para consultas individuais que não acessam colunas criptografadas. Isso desabilitará a chamada a sys.sp_describe_parameter_encryption, além de ser uma tentativa de descriptografar todos os valores no conjunto de resultados.
    - Defina SQLServerStatementColumnEncryptionSetting.ResultSet para consultas individuais que não têm qualquer parâmetro que exija criptografia, mas recuperam dados de colunas criptografadas. Isso desabilitará a chamada a sys.sp_describe_parameter_encryption e a criptografia de parâmetros. A consulta poderá descriptografar os resultados das colunas de criptografia.
- Se a maioria das consultas que um aplicativo cliente envia por uma conexão de banco de dados não acessa colunas criptografadas:
    - Defina a palavra chave columnEncryptionSetting da cadeia de conexão como desativado.
    - Defina SQLServerStatementColumnEncryptionSetting.Enabled para consultas individuais que têm parâmetros que precisam ser criptografados. Isso habilitará a chamada a sys.sp_describe_parameter_encryption, além da descriptografia de todos os resultados de consulta recuperados de colunas criptografadas.
    - Defina SQLServerStatementColumnEncryptionSetting.ResultSet para consultas que não têm qualquer parâmetro que exija criptografia, mas recuperam dados de colunas criptografadas. Isso desabilitará a chamada a sys.sp_describe_parameter_encryption e a criptografia de parâmetros. A consulta poderá descriptografar os resultados das colunas de criptografia.

Observe que as configurações de SQLServerStatementColumnEncryptionSetting não podem ser usadas para ignorar a criptografia e obter acesso aos dados de texto sem formatação. Para obter mais detalhes sobre como configurar a criptografia de coluna em uma instrução, consulte [sempre criptografados referência da API para o Driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).  

No exemplo abaixo, o Sempre Criptografado está desabilitado para a conexão de banco de dados. A consulta emitida pelo aplicativo tem um parâmetro que se destina à coluna LastName não criptografada. A consulta recupera dados das colunas SSN e BirthDate que são criptografadas. Nesse caso, a chamada a sys.sp_describe_parameter_encryption para recuperar os metadados de criptografia não é necessária. No entanto, a descriptografia dos resultados da consulta precisa ser habilitada, para que o aplicativo possa receber valores de texto sem formatação das duas colunas criptografadas. Configuração de SQLServerStatementColumnEncryptionSetting.ResultSet é usada para garantir que.

```
// Assumes the same table definition as in Section "Retrieving and modifying data in encrypted columns"
// where only SSN and BirthDate columns are encrypted in the database.
String connectionUrl = "jdbc:sqlserver://localhost;databaseName=ae;user=sa;password=******;"
        + "keyStoreAuthentication=JavaKeyStorePassword;"
        + "keyStoreLocation=" + keyStoreLocation + ";"
        + "keyStoreSecret=******;";
SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionString);

String filterRecord="SELECT FirstName, LastName, SSN, BirthDate FROM " + tblName + " WHERE LastName = ?";  
PreparedStatement selectStatement = connection.prepareStatement(
        filterRecord, 
        ResultSet.TYPE_FORWARD_ONLY, 
        ResultSet.CONCUR_READ_ONLY, 
        connection.getHoldability(), 
        SQLServerStatementColumnEncryptionSetting.ResultSetOnly);
selectStatement.setString(1, "Abel");  
ResultSet rs = selectStatement.executeQuery();  
while(rs.next()) {  
    System.out.println("First name: " + rs.getString("FirstName"));  
    System.out.println("Last name: " + rs.getString("LastName"));  
    System.out.println("SSN: " + rs.getString("SSN"));  
    System.out.println("Date of Birth: " + rs.getDate("BirthDate"));  
}  
rs.close();
selectStatement.close();
connection.close();
```


### <a name="column-encryption-key-caching"></a>Cache de chaves de criptografia de coluna

Para reduzir o número de chamadas para um repositório de chaves mestras de coluna para descriptografar as chaves de criptografia de coluna, o Microsoft JDBC Driver para SQL Server armazena em cache as chaves de criptografia de coluna de texto sem formatação na memória. Depois de receber o valor da chave de criptografia de coluna criptografado dos metadados do banco de dados, o driver primeiro tentará encontrar a chave de criptografia de coluna de texto sem formatação correspondente ao valor da chave criptografado. O driver chamará o repositório de chaves que contém a chave mestra de coluna apenas se não conseguir encontrar o valor da chave de criptografia de coluna criptografado no cache.

Você pode configurar um valor de tempo de vida para as entradas de chave de criptografia de coluna no cache usando a API, setColumnEncryptionKeyCacheTtl(), na classe SQLServerConnection. O valor de tempo de vida padrão para as entradas de chave de criptografia de coluna no cache é de 2 horas. Para desativar o cache de usar um valor de 0. Para definir qualquer valor de tempo de vida de uso a seguinte API:
    
    SQLServerConnection.setColumnEncryptionKeyCacheTtl (int columnEncryptionKeyCacheTTL, TimeUnit unit)
   
Por exemplo, para definir um valor de tempo de vida de 10 minutos, use
    
    SQLServerConnection.setColumnEncryptionKeyCacheTtl (10, TimeUnit.MINUTES)

Observe que, somente dias, horas, minutos ou segundos têm suporte como a unidade de tempo.  


## <a name="copying-encrypted-data-using-sqlserverbulkcopy"></a>Copiando dados criptografados usando SQLServerBulkCopy

Com SQLServerBulkCopy, você pode copiar os dados que já estão criptografados e armazenados em uma tabela para outra tabela, sem descriptografá-los. Para fazer isso:

- Verifique se a configuração de criptografia da tabela de destino é idêntica à configuração da tabela de origem. Em particular, as duas tabelas devem ter as mesmas colunas criptografadas, e as colunas devem ser criptografadas usando os mesmos tipos de criptografia e as mesmas chaves de criptografia. Observação: se uma das colunas de destino for criptografada de modo diferente da coluna de origem correspondente, você não poderá descriptografar os dados na tabela de destino após a operação de cópia. Os dados serão corrompidos.
- Configure ambas as conexões de banco de dados, à tabela de origem e à tabela de destino, com o Sempre Criptografado desabilitado. 
- Defina a opção allowEncryptedValueModifications. Consulte [usando cópia em massa com o Driver JDBC](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md) para obter mais informações.
 
Observação: Tenha cuidado ao especificar AllowEncryptedValueModifications, pois isso pode levar à corrupção de banco de dados porque o Microsoft JDBC Driver para SQL Server não verifica se os dados estão realmente criptografados ou se foram corretamente criptografado usando a mesma criptografia tipo, algoritmo e a chave como a coluna de destino.

## <a name="see-also"></a>Consulte também  
 [Always Encrypted (mecanismo de banco de dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
  
  
