---
title: "Escolher uma fonte de dados (Assistente de Importa&#231;&#227;o e Exporta&#231;&#227;o do SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.impexpwizard.chooseadatasource.f1"
ms.assetid: ebf28a62-dfc1-4b39-9db5-df1919e5fccb
caps.latest.revision: 124
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 113
---
# Escolher uma fonte de dados (Assistente de Importa&#231;&#227;o e Exporta&#231;&#227;o do SQL Server)
  Após a página de boas-vindas, o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostra **Escolher uma fonte de dados**. Nessa página, você fornece informações sobre a fonte de dados e sobre como se conectar a ela.
  
Para obter informações sobre as fontes de dados que você pode usar, consulte [Quais fontes de dados e destinos posso usar?](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)

## <a name="screen-shot-of-the-choose-a-data-source-page"></a>Captura de tela da página Escolher uma Fonte de Dados 
A captura de tela a seguir mostra a primeira parte da página **Escolher uma Fonte de Dados** do assistente.

![Escolher fonte](../../integration-services/import-export-data/media/choose-source.png)

## <a name="choose-a-data-source"></a>Escolher uma fonte de dados
 **Fonte de dados**  
Especifique a fonte de dados selecionando um provedor de dados que pode conectar à fonte. Na maioria dos casos, o provedor de dados de que você precisa pode ser percebido com facilidade com base em seu nome, pois o nome do provedor contém o nome da origem – por exemplo, SQL Server, Oracle, arquivos simples, Excel e Access.

A lista de provedores de dados disponíveis na lista **Fonte de Dados** depende dos provedores instalados em seu computador. Também depende se você estiver executando o assistente de 32 ou 64 bits.

Pode haver mais de um provedor disponível para sua fonte de dados. Normalmente, você pode selecionar qualquer provedor que funciona com sua origem. Por exemplo, para se conectar ao Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, o Provedor de Dados .NET Framework para SQL Server ou o Provedor Microsoft OLE DB para SQL Server. 

Em alguns casos, você precisa começar escolhendo um provedor de dados genérico. Por exemplo, se você tiver um driver ODBC para sua fonte de dados, selecione o Provedor de Dados .NET Framework para ODBC.  
 
Para algumas fontes de dados, talvez você precise baixar o provedor de dados da Microsoft ou de terceiros. Para obter informações sobre as fontes de dados que você pode usar, consulte [Quais fontes de dados e destinos posso usar?](Import%20and%20Export%20Data%20with%20the%20SQL%20Server%20Import%20and%20Export%20Wizard.md\#wizardSources)

## <a name="after-you-choose-a-data-source"></a>Depois de escolher uma fonte de dados
Depois de escolher uma fonte de dados, o restante da propriedade da página **Escolher uma Fonte de Dados** apresenta opções variáveis que dependem do provedor de dados escolhido.

As seções a seguir listam as opções importantes de algumas fontes de dados usadas com frequência. Nem todas as fontes disponíveis no menu suspenso **Fonte de dados** são listadas aqui. Para obter outras opções e outros provedores, consulte a documentação específica do provedor. 
  
> [!TIP]  Se a fonte de dados exigir uma cadeia de conexão, você poderá encontrar exemplos neste site de terceiros – [The Connection Strings Reference](https://www.connectionstrings.com/).  

## <a name="microsoft-sql-server"></a>Microsoft SQL Server 

### <a name="connect-to-sql-server-with-sql-server-native-client-or-the-microsoft-ole-db-provider-for-sql-server"></a>Conectar-se ao SQL Server com o SQL Server Native Client ou o Provedor Microsoft OLE DB para SQL Server  

O SQL Server Native Client e o Provedor Microsoft OLE DB para SQL Server expõem o mesmo conjunto de opções. A captura de tela a seguir mostra as opções para o SQL Server Native Client como exemplo.

![Nativo de conexão do SQL Server](../../integration-services/import-export-data/media/sql-server-connection-native.png)

 **Nome do servidor**  
 Digite o nome ou endereço IP do servidor que contém os dados ou escolha um servidor da lista.  
  
> [!NOTE] Se você estiver em uma rede com vários servidores, poderá ser mais fácil digitar o nome do servidor. Se você clicar na lista suspensa, poderá demorar muito tempo para consultar todos os servidores disponíveis na rede e o nome do servidor poderá não estar listado nos resultados.

Para especificar uma porta TCP não padrão, digite uma vírgula após o nome do servidor ou endereço IP, em seguida digite o número da porta.
  
 **Usar Autenticação do Windows**  
 Especifique se o assistente deve usar a Autenticação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows para fazer logon no banco de dados. A Autenticação do Windows é recomendada para obter melhor segurança.  
  
 **Usar Autenticação do SQL Server**  
 Especifique se o assistente deve usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para fazer logon no banco de dados. Se você usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , será preciso fornecer um nome de usuário e uma senha.  
  
 **Nome de usuário**  
 Forneça um nome de usuário para estabelecer conexão de banco de dados quando estiver usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Senha**  
 Forneça uma senha para estabelecer conexão de banco de dados quando estiver usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Banco de dados**  
 Selecione usando a lista de bancos de dados na instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Atualizar**  
 Atualize a lista de bancos de dados disponíveis clicando em **Atualizar**.  
  
### <a name="connect-to-sql-server-with-the-net-framework-data-provider-for-sql-server"></a>Conectar-se ao SQL Server com o Provedor de Dados .NET Framework para SQL Server 

Esta página apresenta uma lista agrupada de opções para o Provedor de Dados [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. As opções importantes são listadas aqui. As opções adicionais que são listadas ao selecionar esse provedor geralmente não são necessárias para estabelecer uma conexão bem-sucedida com o banco de dados de origem do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 

Para obter mais informações, consulte [Provedor de Dados .NET Framework para cadeias de conexão do SQL Server](https://www.connectionstrings.com/sqlconnection/).

![Rede de conexão do SQL Server](../../integration-services/import-export-data/media/sql-server-connection-net.png)
  
 **Fonte de Dados**  
 Digite o nome ou endereço IP do servidor que contém os dados ou escolha um servidor da lista.  
  
> [!NOTE] Se você estiver em uma rede com vários servidores, poderá ser mais fácil digitar o nome do servidor. Se você clicar na lista suspensa, poderá demorar muito tempo para consultar todos os servidores disponíveis na rede e o nome do servidor poderá não estar listado nos resultados.  
 
 Para especificar uma porta TCP não padrão, digite uma vírgula após o nome do servidor ou endereço IP, em seguida digite o número da porta.
 
 **Catálogo Inicial**  
 Digite o nome do banco de dados de origem ou escolha um banco de dados na lista.  
  
 **Segurança Integrada**  
 Especifique **True** para estabelecer conexão usando a autenticação integrada do Windows (recomendado) ou **False** para estabelecer conexão usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se você especificar **False**, deverá inserir uma ID de usuário e uma senha. O valor padrão é **Falso**.  
  
 **ID de usuário**  
 Forneça um nome de usuário para estabelecer conexão de banco de dados quando estiver usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Senha**  
 Forneça uma senha para estabelecer conexão de banco de dados quando estiver usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

## <a name="oracle"></a>Oracle

Conectar-se ao Oracle usando o Provedor de Dados .NET Framework para Oracle ou o Provedor Microsoft OLE DB para Oracle. O Provedor .NET Framework para Oracle é mais fácil de configurar e é mostrado na captura de tela a seguir.

Para obter mais informações, consulte [Cadeias de conexão do Provedor de Dados .NET Framework para Oracle](https://www.connectionstrings.com/net-framework-data-provider-for-oracle/) ou [Cadeias de conexão do Provedor de Dados Microsoft OLE DB para Oracle](https://www.connectionstrings.com/microsoft-ole-db-provider-for-oracle-msdaora/).

![Conexão Oracle](../../integration-services/import-export-data/media/oracle-connection.png)

## <a name="odbc-data-sources"></a>fontes de dados ODBC

Para carregar os dados de qualquer fonte que fornece um driver ODBC, selecione o Provedor de Dados .NET Framework para ODBC.

Para fornecer uma cadeia de conexão para uma fonte de dados ODBC, consulte a documentação do driver ODBC que você quer usar ou procure exemplos aqui – [The Connection Strings Reference](https://www.connectionstrings.com/). 

A captura de tela a seguir mostra uma conexão ODBC com o SQL Server como exemplo. A cadeia de conexão usada no exemplo é:

    Driver={SQL Server};Server=(local);Database=TestData;Trusted_Connection=Yes;

Depois de inserir a cadeia de conexão no campo **ConnectionString**, o assistente analisa a cadeia de caracteres e exibe as propriedades individuais e seus valores na seção **Misc** da lista.

![Conexão ODBC SQL](../../integration-services/import-export-data/media/odbc-connection-sql.png)

## <a name="text-files-flat-files"></a>Arquivos de texto (arquivos simples)
 
 Há várias páginas de opções para fontes de dados de arquivo simples.
 
 ### <a name="general-page"></a>Página Geral
 Na página **Geral**, navegue para selecionar o arquivo e verifique as configurações na seção **Formato**.
 
 ![Conexão geral de arquivo simples](../../integration-services/import-export-data/media/flat-file-connection-general.png)  
   
Para obter mais informações sobre a página **Geral**, consulte a seguinte página de referência do Integration Services: [Editor do Gerenciador de Conexões de arquivos simples &#40;página Geral&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md).  

### <a name="columns-page"></a>Página Colunas

 Na página **Colunas**, verifique se a lista de colunas e os delimitadores que o assistente identificou.
 
 ![Colunas de conexões de arquivo simples](../../integration-services/import-export-data/media/flat-file-connection-columns.png)
  
Para obter mais informações sobre a página **Colunas**, consulte a seguinte página de referência do Integration Services: [Editor do Gerenciador de Conexões de arquivos simples &#40;página Colunas&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-columns-page.md).

### <a name="advanced-page"></a>Página Avançado

A página **Avançado** mostra informações detalhadas sobre cada coluna na fonte de dados, como o tipo de dados e tamanho.

Na seguinte captura de tela, observe que a coluna **id** inicialmente tem um tipo de dados de cadeia de caracteres.

![Conexão de arquivo simples avançada antes de](../../integration-services/import-export-data/media/flat-file-connection-advanced-before.png)

Clique em **Sugerir tipos** para exibir a caixa de diálogo **Sugerir tipos de coluna**. 

![Sugerir conexões de arquivo simples](../../integration-services/import-export-data/media/flat-file-connection-suggest.png)

Depois de escolher as opções na caixa de diálogo **Sugerir tipos de coluna** e clicar em **OK**, o assistente poderá alterar os tipos de dados de algumas das colunas a serem importados.

A captura de tela a seguir mostra que o assistente reconheceu que a coluna **id** na fonte de dados é, na verdade, um número e não uma cadeia de caracteres de texto e alterou o tipo de dados da coluna de uma cadeia de caracteres para um número inteiro.

![Conexão de arquivo simples avançado depois de](../../integration-services/import-export-data/media/flat-file-connection-advanced-after.png)
  
Para obter mais informações sobre a página **Avançado**, consulte a seguinte página de referência do Integration Services: [Editor do Gerenciador de Conexões de arquivos simples &#40;página Avançado&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-advanced-page.md).

### <a name="preview-page"></a>Página Visualização

Na página **Visualização**, verifique se que a lista de colunas e os dados de exemplo são os esperados.

![Visualização de conexões de arquivo simples](../../integration-services/import-export-data/media/flat-file-connection-preview.png)

Para obter mais informações sobre a página **Visualização**, consulte a seguinte página de referência do Integration Services: [Editor do Gerenciador de Conexões de arquivos simples &#40;página Visualização&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md).  
 
## <a name="microsoft-excel"></a>Microsoft Excel

A captura de tela a seguir mostra uma conexão de exemplo a uma pasta de trabalho do Microsoft Excel.

![Conexão do Excel](../../integration-services/import-export-data/media/excel-connection.png) 
 
 **Caminho de Arquivo do Excel**  
 Especifique o caminho e nome de arquivo da planilha a partir da qual os dados serão importados. Por exemplo, **C:\\MyData.xlsx** para um arquivo no computador local ou **\\\\Sales\\Database\\Northwind.xlsx** para um arquivo em um compartilhamento de rede. Se preferir, clique em **Procurar**.  
  
 **Procurar**  
 Localize a planilha usando a caixa de diálogo **Abrir**.  

> [!NOTE] O assistente não pode abrir um arquivo do Excel protegido por senha.

 **Versão do Excel**  
 Selecione a versão do Excel usada pela pasta de trabalho de origem.

Talvez seja necessário baixar e instalar arquivos adicionais para se conectar à versão do Excel selecionada. Consulte [Obter os downloads necessários para Excel e Access](Choose%20a%20Data%20Source%20\%28SQL%20Server%20Import%20and%20Export%20Wizard%29.md\#officeDownloads) nesta página para obter mais informações.

Se tiver problemas ao especificar uma versão (por exemplo, se não for possível instalar o tempo de execução do Access 2016 porque você já tem o Microsoft Office 365), tente especificar uma versão diferente, até mesmo uma versão anterior, por exemplo, 2013, em vez da 2016.

**Primeira linha tem nomes de coluna**  
Indique se a primeira linha dos dados de origem contém nomes de coluna.
-   Se os dados de origem não contiverem nomes de coluna, mas você habilitar essa opção, o assistente tratará a primeira linha dos dados de origem como os nomes de coluna.
-   Se os dados de origem contiverem nomes de coluna, mas você desabilitar essa opção, o assistente tratará a linha de nomes de coluna como a primeira linha de dados.

Se os dados de origem não tiverem os nomes de coluna, o assistente usará F1, F2 e assim por diante de maneira interna como os títulos de coluna temporários.

## <a name="microsoft-access"></a>Microsoft Access  

A captura de tela a seguir mostra uma conexão de exemplo a um banco de dados do Microsoft Access.

![Conexão Access](../../integration-services/import-export-data/media/access-connection.png)

 **Nome do arquivo**  
 Especifique o caminho e nome de arquivo do arquivo de banco de dados a partir do qual os dados serão importados. Por exemplo, **C:\MyData.mdb, \\\Sales\Database\Northwind.mdb**. Se preferir, clique em **Procurar**.
 
 >   [!NOTE] O assistente só pode se conectar a um banco de dados Access no formato de arquivo .MDB.  
  
 **Procurar**  
 Localize o arquivo de banco de dados usando a caixa de diálogo **Abrir**.  
  
 **Nome de usuário**  
Quando um arquivo de informações do grupo de trabalho estiver associado ao banco de dados, forneça um nome de usuário válido da conexão de banco de dados.  
  
 **Senha**  
Quando um arquivo de informações do grupo de trabalho estiver associado ao banco de dados, forneça a senha do usuário da conexão de banco de dados.
 
Se o banco de dados estiver protegido com uma única senha para todos os usuários, forneça este valor na caixa de diálogo **Propriedades de Vínculo de Dados**. Para abrir a caixa de diálogo **Propriedades de Vínculo de Dados**, clique em **Avançado**.  
  
 **Avançado**  
Especifique as opções avançadas, como a senha do banco de dados ou um arquivo de informações do grupo de trabalho não padrão, usando a caixa de diálogo **Propriedades de Vínculo de Dados**.  
  
## <a name="a-nameofficedownloadsaget-the-downloads-you-need-for-excel-and-access"></a><a name="officeDownloads"></a>Obter os downloads necessários para Excel e Access  
Talvez seja preciso baixar os componentes de conectividade para as fontes de dados do Microsoft Excel e do Access se eles ainda não estiverem instalados.

As versões mais recentes dos componentes podem abrir arquivos criados em versões anteriores dos programas. Em alguns casos, as versões anteriores dos componentes também podem abrir arquivos criados por versões mais recentes dos programas.  
  
Se o computador tiver uma versão de 32 bits do Office, você precisará instalar a versão de 32 bits dos componentes. Você também precisará verificar se o assistente (ou pacote do Integration Services que ele cria) é executado no modo de 32 bits.  
|Versão do Microsoft Office|Download|  
|------------------------------|--------------|  
|2007|[2007 Office System Driver: componentes de conectividade de dados](https://www.microsoft.com/download/details.aspx?id=23734)|  
|2010|[Tempo de execução do Microsoft Access 2010](https://www.microsoft.com/download/details.aspx?id=10910)|  
|2013|[Tempo de execução do Microsoft Access 2013](http://www.microsoft.com/download/details.aspx?id=39358)|  
|2016|[Tempo de execução do Microsoft Access 2016](https://www.microsoft.com/download/details.aspx?id=50040)|  
 
 
## <a name="azure-blob-storage"></a>Armazenamento de blob do Azure  
Para usar o a Fonte de Blob do Azure, você precisa instalar o Feature Pack do Azure para SSIS. Para obter mais informações, consulte [Feature Pack do Azure para o Integration Services &#40;SSIS&#41;](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).  

>   [!NOTE] Para garantir que o Gerenciador de Conexões do Armazenamento do Azure e os componentes que o utilizam, incluindo o Origem do Blob, podem se conectar às contas de armazenamento de uso geral e às contas de armazenamento de blobs, verifique se você baixou a versão mais recente do Azure Feature Pack [aqui](https://www.microsoft.com/download/details.aspx?id=49492). Para obter mais informações sobre esses dois tipos de contas de armazenamento, consulte [Introdução ao Armazenamento do Microsoft Azure](https://azure.microsoft.com/en-us/documentation/articles/storage-introduction/#general-purpose-storage-accounts).

![Conexão do armazenamento de blobs do Azure](../../integration-services/import-export-data/media/azure-blob-storage-connection.png)

 **Usar conta do Azure**  
 Especifique se uma conta online deverá ser usada.
  
 **Nome da conta de armazenamento**  
 Especifique o nome da conta de armazenamento do Azure.  
  
**Chave de conta**  
Forneça a chave da conta de armazenamento do Azure.  
  
 **Usar HTTPS**  
 Especifique se deseja usar HTTP ou HTTPS para se conectar à conta de armazenamento.  
  
 **Usar conta de desenvolvedor local**  
 Especifique se deseja usar o emulador de armazenamento no computador local.  
  
 **Nome do contêiner de Blob**  
 Selecione na lista de contêineres de armazenamento disponíveis na conta de armazenamento especificada.  
  
 **Formato de arquivo do Blob**  
 Selecione o formato de arquivo de texto ou Avro.  
  
 **Caractere delimitador de coluna**  
 Se você selecionou o formato Texto, especifique o caractere delimitador de coluna.  
  
 **Use a primeira linha como nomes de colunas**  
 Especifique se a primeira linha de dados contém nomes de coluna.  
  
## <a name="whats-next"></a>O que vem a seguir?  
 Depois de fornecer informações sobre a fonte de dados e sobre como se conectar a ela, a próxima página será **Escolher um Destino**. Nessa página, você fornece informações sobre o destino dos dados e sobre como se conectar a ele. Para obter mais informações, consulte [Escolher um destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md).  
