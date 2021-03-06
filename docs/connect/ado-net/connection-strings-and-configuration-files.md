---
title: Cadeias de conexão e arquivos de configuração
description: Saiba como armazenar cadeias de conexão para aplicativos ADO.NET em um arquivo de configuração de aplicativo, como uma melhor prática de segurança e manutenção.
ms.date: 11/13/2020
dev_langs:
- csharp
ms.assetid: 37df2641-661e-407a-a3fb-7bf9540f01e8
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: fb290f9a795c9f64bcb2ee95c66210790a80a71d
ms.sourcegitcommit: 7a3fdd3f282f634f7382790841d2c2a06c917011
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2020
ms.locfileid: "96563112"
---
# <a name="connection-strings-and-configuration-files"></a>Cadeias de conexão e arquivos de configuração

[!INCLUDE[appliesto-netfx-netcore-xxxx-md](../../includes/appliesto-netfx-netcore-xxxx-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Inserir cadeias de conexão no código do seu aplicativo pode resultar em vulnerabilidades de segurança e problemas de manutenção. As cadeias de conexão não criptografadas compiladas no código-fonte de um aplicativo podem ser exibidas com a ferramenta [Ildasm.exe (IL Disassembler)](/dotnet/framework/tools/ildasm-exe-il-disassembler). Além disso, se a cadeia de conexão for alterada, seu aplicativo deverá ser recompilado. Por esses motivos, recomendamos armazenar cadeias de conexão em um arquivo de configuração do aplicativo.

## <a name="working-with-application-configuration-files"></a>Trabalhando com arquivos de configuração de aplicativo

Os arquivos de configuração do aplicativo contêm as configurações que são específicas para um determinado aplicativo. Por exemplo, um aplicativo ASP.NET pode ter um ou mais arquivos **web.config** e um aplicativo do Windows pode ter um arquivo **app.config** opcional. Os arquivos de configuração compartilham elementos comuns, embora o nome e o local de um arquivo de configuração variem dependendo do host do aplicativo.

### <a name="the-connectionstrings-section"></a>A seção de connectionStrings

As cadeias de conexão podem ser armazenadas como pares chave/valor na seção **connectionStrings** do elemento **configuration** de um arquivo de configuração de aplicativo. Os elementos filho incluem **add**, **clear** e **remove**.

O fragmento de arquivo de configuração a seguir demonstra o esquema e a sintaxe para armazenar uma cadeia de conexão. O atributo **name** é um nome que você fornece para identificar exclusivamente uma cadeia de conexão para que ela possa ser recuperada em tempo de execução. O **providerName** é **Microsoft.Data.SqlClient** com o Provedor de Dados Microsoft SqlClient para SQL Server.

```xml  
<?xml version='1.0' encoding='utf-8'?>  
  <configuration>  
    <connectionStrings>  
      <clear />  
      <add name="Name"
       providerName="Microsoft.Data.SqlClient"
       connectionString="Valid Connection String;" />  
    </connectionStrings>  
  </configuration>  
```  

> [!NOTE]
> Você pode salvar parte de uma cadeia de conexão em um arquivo de configuração e usar a classe <xref:System.Data.Common.DbConnectionStringBuilder> para concluí-la em tempo de execução. Isso é útil em situações onde você não conhece os elementos da cadeia de conexão com antecedência, ou quando não quer salvar informações confidenciais em um arquivo de configuração. Para obter mais informações, confira [Construtores de cadeias de conexão](connection-string-builders.md).

### <a name="using-external-configuration-files"></a>Utilizando arquivos de configuração externos

Os arquivos de configuração externos são arquivos separados que contêm um fragmento de um arquivo de configuração que consiste em uma única seção. O arquivo de configuração externo é, em seguida, referenciado pelo arquivo de configuração principal. O armazenamento da seção **connectionStrings** em um arquivo fisicamente separado é útil em situações em que as cadeias de conexão podem ser editadas após a implantação do aplicativo. Por exemplo, o comportamento padrão do ASP.NET é reiniciar o domínio de um aplicativo quando os arquivos de configuração são modificados, o que resulta em perda de informações de estado. No entanto, modificar um arquivo de configuração externo não causa uma reinicialização do aplicativo. Os arquivos de configuração externos não estão limitados ao ASP.NET; eles também podem ser usados por aplicativos do Windows. Além disso, a segurança de acesso a arquivos e as permissões podem ser usadas para restringir o acesso a arquivos de configuração externos. Trabalhar com arquivos de configuração externos em tempo de execução é transparente e não exige nenhuma codificação especial.

Para armazenar cadeias de conexão em um arquivo de configuração externo, crie um arquivo separado que contenha somente a seção **connectionStrings**. Não inclui elementos, seções ou atributos adicionais. Este exemplo mostra a sintaxe para um arquivo de configuração externo.

```xml  
<connectionStrings>  
  <add name="Name"
   providerName="Microsoft.Data.SqlClient"
   connectionString="Valid Connection String;" />  
</connectionStrings>  
```  

 No arquivo de configuração de aplicativo principal, use o atributo **configSource** para especificar o nome totalmente qualificado e o local do arquivo externo. Este exemplo refere-se a um arquivo de configuração externo chamado `connections.config`.

```xml  
<?xml version='1.0' encoding='utf-8'?>  
<configuration>  
    <connectionStrings configSource="connections.config"/>  
</configuration>  
```  

## <a name="retrieving-connection-strings-at-run-time"></a>Recuperando cadeias de conexão em tempo de execução

O .NET Framework 2.0 introduziu novas classes no namespace <xref:System.Configuration> para simplificar a recuperação de cadeias de conexão de arquivos de configuração em tempo de execução. Você pode programaticamente recuperar uma cadeia de conexão por nome ou nome do provedor.

> [!NOTE]
> O arquivo **machine.config** também contém uma seção **connectionStrings**, que contém as cadeias de conexão usadas pelo Visual Studio. Ao recuperar cadeias de conexão pelo nome do provedor do arquivo **app.config** em um aplicativo do Windows, as cadeias de conexão em **machine.config** são carregadas primeiro e, em seguida, as entradas de **app.config**. Adicionar **clear** imediatamente após o elemento **connectionStrings** remove todas as referências herdadas da estrutura de dados na memória, de modo que somente as cadeias de conexão definidas no arquivo **app.config** local serão consideradas.

### <a name="working-with-the-configuration-classes"></a>Trabalhando com as classes de configuração

A partir do .NET Framework 2.0, <xref:System.Configuration.ConfigurationManager> é usado ao trabalhar com arquivos de configuração no computador local, substituindo o <xref:System.Configuration.ConfigurationSettings> obsoleto. <xref:System.Web.Configuration.WebConfigurationManager> é usado para trabalhar com arquivos de configuração do ASP.NET. Ele foi criado para trabalhar com arquivos de configuração em um servidor Web e permite o acesso programático a seções do arquivo de configuração como **system.web**.

> [!NOTE]
> Acessar arquivos de configuração em tempo de execução exige a concessão de permissões para o chamador; as permissões necessárias dependem do tipo de aplicativo, do arquivo de configuração e do local. Para obter mais informações, confira [Usando as classes de configuração](/previous-versions/aspnet/ms228063(v=vs.100)), <xref:System.Web.Configuration.WebConfigurationManager> para aplicativos ASP.NET e <xref:System.Configuration.ConfigurationManager> para aplicativos do Windows.

Você pode usar <xref:System.Configuration.ConnectionStringSettingsCollection> para recuperar cadeias de conexão de arquivos de configuração do aplicativo. Ele contém uma coleção de objetos <xref:System.Configuration.ConnectionStringSettings>, cada um deles representando uma única entrada na seção **connectionStrings**. Suas propriedades mapeiam para atributos de cadeia de conexão, permitindo que você recupere uma cadeia de conexão especificando o nome ou o nome do provedor.

|Propriedade|Descrição|  
|--------------|-----------------|  
|<xref:System.Configuration.ConnectionStringSettings.Name%2A>|O nome da cadeia de conexão. Mapeado para o atributo **name**.|  
|<xref:System.Configuration.ConnectionStringSettings.ProviderName%2A>|O nome do provedor totalmente qualificado. Mapeado para o atributo **providerName**.|  
|<xref:System.Configuration.ConnectionStringSettings.ConnectionString%2A>|A cadeia de conexão. Mapeada para o atributo **connectionString**.|  

### <a name="example-listing-all-connection-strings"></a>Exemplo: listando todas as cadeias de conexão

Este exemplo itera por meio de <xref:System.Configuration.ConnectionStringSettingsCollection> e exibe as propriedades <xref:System.Configuration.ConnectionStringSettings.Name%2A?displayProperty=nameWithType>, <xref:System.Configuration.ConnectionStringSettings.ProviderName%2A?displayProperty=nameWithType> e <xref:System.Configuration.ConnectionStringSettings.ConnectionString%2A?displayProperty=nameWithType> na janela do console.

> [!NOTE]
> System.Configuration.dll não está incluído em todos os tipos de projeto, e você talvez precise definir uma referência para ele para usar as classes de configuração. O nome e o local de um arquivo de configuração do aplicativo específico variam pelo tipo de aplicativo e o processo de hospedagem.

[!code-csharp[DataWorks ConnectionStringSettings.RetrieveFromConfig#1](~/../SqlClient/doc/samples/ConnectionStringSettings_RetrieveFromConfig.cs#1)]

### <a name="example-retrieving-a-connection-string-by-name"></a>Exemplo: recuperando uma cadeia de conexão por nome

Este exemplo demonstra como recuperar uma cadeia de conexão de um arquivo de configuração especificando seu nome. O código cria um objeto <xref:System.Configuration.ConnectionStringSettings>, correspondendo o parâmetro de entrada fornecido com o nome de <xref:System.Configuration.ConfigurationManager.ConnectionStrings%2A>. Se nenhum nome correspondente for localizado, a função retornará `null` (`Nothing` no Visual Basic).

[!code-csharp[DataWorks ConnectionStringSettings.RetrieveFromConfigByName#1](~/../SqlClient/doc/samples/ConnectionStringSettings_RetrieveFromConfigByName.cs#1)]

### <a name="example-retrieving-a-connection-string-by-provider-name"></a>Exemplo: recuperando uma cadeia de conexão por nome de provedor

Este exemplo demonstra como recuperar uma cadeia de conexão especificando o nome do provedor no formato *Microsoft.Data.SqlClient*. O código itera por meio do <xref:System.Configuration.ConnectionStringSettingsCollection> e retorna a cadeia de conexão para o primeiro <xref:System.Configuration.ConnectionStringSettings.ProviderName%2A> encontrado. Se o nome do provedor não for localizado, a função retornará `null` (`Nothing` no Visual Basic).

[!code-csharp[DataWorks ConnectionStringSettings.RetrieveFromConfigByProvider#1](~/../SqlClient/doc/samples/ConnectionStringSettings_RetrieveFromConfigByProvider.cs#1)]

## <a name="encrypting-configuration-file-sections-using-protected-configuration"></a>Criptografando seções do arquivo de configuração usando configuração protegida

O ASP.NET 2.0 introduziu uma nova funcionalidade, chamada *configuração protegida*, que permite criptografar informações confidenciais em um arquivo de configuração. Embora tenha sido projetado principalmente para ASP.NET, a configuração protegida também pode ser usada para criptografar seções do arquivo de configuração em aplicativos do Windows. Para obter uma descrição detalhada das funcionalidades da configuração protegida, confira [Criptografando informações de configuração usando a configuração protegida](/previous-versions/aspnet/53tyfkaw(v=vs.100)).

O fragmento do arquivo de configuração a seguir mostra a seção **connectionStrings** depois de ser criptografada. O **configProtectionProvider** especifica o provedor de configuração protegida usado para criptografar e descriptografar as cadeias de conexão. A seção **EncryptedData** contém o texto de criptografia.

```xml  
<connectionStrings configProtectionProvider="DataProtectionConfigurationProvider">  
  <EncryptedData>  
    <CipherData>  
      <CipherValue>AQAAANCMnd8BFdERjHoAwE/Cl+sBAAAAH2... </CipherValue>  
    </CipherData>  
  </EncryptedData>  
</connectionStrings>  
```  

Quando a cadeia de conexão criptografada é recuperada em tempo de execução, o .NET Framework usa o provedor especificado para descriptografar **CipherValue** e disponibilizá-lo para o aplicativo. Você não precisa escrever nenhum código adicional para gerenciar o processo descriptografia.

### <a name="protected-configuration-providers"></a>Provedores de configuração protegida

Os provedores de configuração protegida são registrados na seção **configProtectedData** do arquivo **machine.config** no computador local, conforme mostrado no fragmento a seguir, que mostra os dois provedores de configuração protegida fornecidos com o .NET Framework. Os valores mostrados aqui foram truncados para facilitar a leitura.

```xml  
<configProtectedData defaultProvider="RsaProtectedConfigurationProvider">  
  <providers>  
    <add name="RsaProtectedConfigurationProvider"
      type="System.Configuration.RsaProtectedConfigurationProvider" />  
    <add name="DataProtectionConfigurationProvider"
      type="System.Configuration.DpapiProtectedConfigurationProvider" />  
  </providers>  
</configProtectedData>  
```  

Configure outros provedores de configuração protegida adicionando-os ao arquivo **machine.config**. Você também pode criar seu próprio provedor de configuração protegida por herança da classe base abstrata <xref:System.Configuration.ProtectedConfigurationProvider>. A tabela a seguir descreve os dois arquivos de configuração incluídos no .NET Framework.

|Provedor|Descrição|  
|--------------|-----------------|  
|<xref:System.Configuration.RsaProtectedConfigurationProvider>|Usa o algoritmo de criptografia RSA para criptografar e descriptografar dados. O algoritmo RSA pode ser usado para criptografia de chave pública e assinaturas digitais. Também é conhecido como “chave pública” ou criptografia assimétrica porque emprega duas chaves diferentes. Use a [Ferramenta de Registro do IIS do ASP.NET (Aspnet_regiis.exe)](/previous-versions/dotnet/netframework-3.5/k6h9cz8h(v=vs.90)) para criptografar as seções em um arquivo Web.config e gerenciar as chaves de criptografia. O ASP.NET descriptografa o arquivo de configuração quando processa o arquivo. A identidade do aplicativo do ASP.NET deve ter acesso de leitura para a chave de criptografia que é usada para criptografar e descriptografar as seções criptografadas.|  
|<xref:System.Configuration.DpapiProtectedConfigurationProvider>|Usa a API de Proteção aos Dados do Windows (DPAPI) para criptografar seções de configuração. Usa os serviços de criptografia internos do Windows e pode ser configurado para proteção específica de computador ou da conta do usuário. A proteção específica do computador é útil para vários aplicativos no mesmo servidor que precisam compartilhar informações. A proteção específica da conta do usuário pode ser usada com serviços que são executados com uma identidade de usuário específica, como um ambiente de hospedagem compartilhado. Cada aplicativo é executado sob uma identidade separada, o que restringe o acesso a recursos como arquivos e bancos de dados.|

Os dois provedores oferecem criptografia de dados forte. Entretanto, se você estiver planejando usar o mesmo arquivo de configuração criptografado em vários servidores, como uma Web farm, apenas o <xref:System.Configuration.RsaProtectedConfigurationProvider> permite que você exporte as chaves de criptografia usadas para criptografar os dados e importá-los em outro servidor. Para obter mais informações, confira [Importando e exportando contêineres de chave RSA da configuração protegida](/previous-versions/aspnet/yxw286t2(v=vs.100)).

### <a name="using-the-configuration-classes"></a>Usando as classes de configuração

O namespace <xref:System.Configuration> fornece classes para trabalhar com parâmetros de configuração programaticamente. A classe <xref:System.Configuration.ConfigurationManager> fornece acesso a arquivos de computador, aplicativo e configuração do usuário. Se você estiver criando um aplicativo ASP.NET, poderá usar a classe <xref:System.Web.Configuration.WebConfigurationManager>, que fornece a mesma funcionalidade, além de permitir o acesso às configurações que são exclusivas para os aplicativos ASP.NET, como as encontradas em **\<system.web>** .

> [!NOTE]
> O namespace <xref:System.Security.Cryptography> contém classes que oferecem opções adicionais para criptografar e descriptografar dados. Use essas classes se você precisar de serviços de criptografia que não estão disponíveis usando a configuração protegida. Algumas dessas classes são wrappers da Microsoft CryptoAPI não gerenciada, enquanto outras são implementações puramente gerenciadas. Para obter mais informações, consulte [Serviços Criptográficos](/previous-versions/visualstudio/visual-studio-2008/93bskf9z(v=vs.90)).

### <a name="appconfig-example"></a>Exemplo de App.config

Este exemplo demonstra como ativar/desativar a criptografia da seção **connectionStrings** em um arquivo **app.config** para um aplicativo do Windows. Nesse exemplo, o procedimento utiliza o nome do aplicativo como um argumento, por exemplo, “MyApplication.exe”. O arquivo **app.config** será então criptografado e copiado para a pasta que contém o executável com o nome "MyApplication.exe.config".

> [!NOTE]
> A cadeia de conexão somente pode ser descriptografada no computador no qual foi criptografada.

O código usa o método <xref:System.Configuration.ConfigurationManager.OpenExeConfiguration%2A> para abrir o arquivo **app.config** para edição, e o método <xref:System.Configuration.ConfigurationManager.GetSection%2A> retorna a seção **connectionStrings**. O código em seguida verifica a propriedade <xref:System.Configuration.SectionInformation.IsProtected%2A>, chamando <xref:System.Configuration.SectionInformation.ProtectSection%2A> para criptografar a seção se não estiver criptografada. O método <xref:System.Configuration.SectionInformation.UnprotectSection%2A> é chamado para descriptografar a seção. O método <xref:System.Configuration.Configuration.Save%2A> conclui a operação e salva as alterações.

> [!NOTE]
> Você deve definir uma referência a `System.Configuration.dll` em seu projeto para que o código seja executado.

[!code-csharp[DataWorks ConnectionStrings.Encrypt#1](~/../SqlClient/doc/samples/ConnectionStrings_Encrypt.cs#1)]

### <a name="webconfig-example"></a>Exemplo de Web.config

Esse exemplo usa o método <xref:System.Web.Configuration.WebConfigurationManager.OpenWebConfiguration%2A> do `WebConfigurationManager`. Observe que, nesse caso, você pode fornecer o caminho relativo para o arquivo **Web.config** usando um til. O código exige uma referência à classe `System.Web.Configuration`.  
  
[!code-csharp[DataWorks ConnectionStringsWeb.Encrypt#1](~/../SqlClient/doc/samples/ConnectionStringsWeb_Encrypt.cs#1)]

Para saber mais sobre como proteger aplicativos ASP.NET, confira [Proteger sites ASP.NET](/previous-versions/aspnet/91f66yxt(v=vs.100)).

## <a name="see-also"></a>Confira também

- [Construtores de cadeia de conexão](connection-string-builders.md)
- [Protegendo informações de conexão](protecting-connection-information.md)
- [Usando as classes de configuração](/previous-versions/visualstudio/visual-studio-2008/ms228063(v=vs.90))
- [Configuração de aplicativos](/dotnet/framework/configure-apps/index)
- [Administração de site ASP.NET](/previous-versions/aspnet/6hy1xzbw(v=vs.100))
