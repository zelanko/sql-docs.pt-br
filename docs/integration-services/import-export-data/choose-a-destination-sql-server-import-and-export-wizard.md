---
title: "Escolher um destino (Assistente de Importa&#231;&#227;o e Exporta&#231;&#227;o do SQL Server) | Microsoft Docs"
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
  - "sql13.dts.impexpwizard.chooseadestination.f1"
ms.assetid: 1898be15-3e69-42d3-8ecb-3733c9f6c8e3
caps.latest.revision: 104
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 95
---
# Escolher um destino (Assistente de Importa&#231;&#227;o e Exporta&#231;&#227;o do SQL Server)
 Depois de fornecer informações sobre a fonte de dados e sobre como se conectar a ela, o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostra a página **Escolher um Destino**. Nessa página, você fornece informações sobre o destino dos dados e sobre como se conectar a ele.
  
Para obter informações sobre os destinos de dados que você pode usar, consulte [Quais fontes de dados e destinos posso usar?](Import%20and%20Export%20Data%20with%20the%20SQL%20Server%20Import%20and%20Export%20Wizard.md\#wizardSources). 

## <a name="screen-shot-of-the-destination-page"></a>Captura de tela da página Destino
A captura de tela a seguir mostra a parte da página **Escolher um Destino** do assistente.

![Escolher destino](../../integration-services/import-export-data/media/choose-destination.png)

## <a name="choose-a-destination"></a>Escolher um destino
 **Destino**  
 Especifique o destino selecionando um provedor de dados que pode importar dados no destino. Na maioria dos casos, o provedor de dados de que você precisa pode ser percebido com facilidade com base em seu nome, pois o nome do provedor contém o nome do destino – por exemplo, SQL Server, Oracle, arquivos simples, Excel e Access.
 
A lista de provedores de dados disponíveis na lista **Destino** depende dos provedores instalados em seu computador. Também depende se você estiver executando o assistente de 32 ou 64 bits.

Pode haver mais de um provedor disponível para seu destino. Normalmente, você pode selecionar qualquer provedor que funciona com o destino. Por exemplo, para se conectar ao Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, o Provedor de Dados .NET Framework para SQL Server ou o Provedor Microsoft OLE DB para SQL Server.
 
Em alguns casos, você precisa começar escolhendo um provedor de dados genérico. Por exemplo, se você tiver um driver ODBC para o destino, selecione o Provedor de Dados .NET Framework para ODBC.

Para alguns destinos, talvez você precise baixar o provedor de dados da Microsoft ou de terceiros. Para obter informações sobre os destinos de dados que você pode usar, consulte [Quais fontes de dados e destinos posso usar?](Import%20and%20Export%20Data%20with%20the%20SQL%20Server%20Import%20and%20Export%20Wizard.md\#wizardSources).

## <a name="after-you-choose-a-destination"></a>Depois de escolher um destino
Depois de escolher um destino, o restante da propriedade da página **Escolher um Destino** apresenta opções variáveis que dependem do provedor de dados escolhido.

As seções a seguir listam as opções importantes de alguns destinos usados com frequência. Nem todos os destinos disponíveis no menu suspenso **Destino** são listados aqui. Para obter outras opções e outros provedores, consulte a documentação específica do provedor.

> [!TIP] Se o destino exigir uma cadeia de conexão, você poderá encontrar exemplos neste site de terceiros – [The Connection Strings Reference](https://www.connectionstrings.com/).  

## <a name="microsoft-sql-server"></a>Microsoft SQL Server 

Se você quiser criar um novo banco de dados SQL Server como destino, selecione o SQL Server Native Client ou o Provedor Microsoft OLE DB para SQL Server. Se você selecionar o provedor de Dados .NET Framework para SQL Server, a opção para criar um novo banco de dados não estará disponível.  

### <a name="connect-to-sql-server-with-sql-server-native-client-or-the-microsoft-ole-db-provider-for-sql-server"></a>Conectar-se ao SQL Server com o SQL Server Native Client ou o Provedor Microsoft OLE DB para SQL Server  

O SQL Server Native Client e o Provedor Microsoft OLE DB para SQL Server expõem o mesmo conjunto de opções. A captura de tela a seguir mostra as opções para o SQL Server Native Client como exemplo.

![Destino nativo do SQL](../../integration-services/import-export-data/media/sql-native-destination.png)

 **Nome do servidor**  
 Digite o nome ou o endereço IP do servidor de destino ou escolha um servidor na lista.  
  
> [!NOTE] Se você estiver em uma rede com vários servidores, poderá ser mais fácil digitar o nome do servidor. Se você clicar na lista suspensa, poderá demorar muito tempo para consultar todos os servidores disponíveis na rede e o nome do servidor poderá não estar listado nos resultados.  
 
 Para especificar uma porta TCP não padrão, digite uma vírgula após o nome do servidor ou endereço IP, em seguida digite o número da porta.
 
 **Usar Autenticação do Windows**  
 Especifique se o assistente deve usar a Autenticação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows para fazer logon no banco de dados. A Autenticação do Windows é recomendável.  
  
 **Usar Autenticação do SQL Server**  
 Especifique se o assistente deve usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para fazer logon no banco de dados. Se você usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , será preciso fornecer um nome de usuário e uma senha.  
  
 **Nome de usuário**  
 Forneça um nome de usuário para estabelecer conexão de banco de dados quando estiver usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Senha**  
 Forneça uma senha para estabelecer conexão de banco de dados quando estiver usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Banco de dados**  
 Selecione usando a lista de bancos de dados na instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Atualizar**  
 Restaure a lista de bancos de dados disponíveis clicando em **Atualizar**.  
  
### <a name="connect-to-sql-server-with-the-net-framework-data-provider-for-sql-server"></a>Conectar-se ao SQL Server com o Provedor de Dados .NET Framework para SQL Server 

Esta página apresenta uma lista agrupada de opções para o Provedor de Dados [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. As opções importantes são listadas aqui. As opções adicionais listadas ao selecionar esse provedor não são necessárias para estabelecer uma conexão bem-sucedida com o banco de dados de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 

Para obter mais informações, consulte [Provedor de Dados .NET Framework para cadeias de conexão do SQL Server](https://www.connectionstrings.com/sqlconnection/).

![Rede de destino do SQL Server](../../integration-services/import-export-data/media/sql-server-destination-net.png)
  
 **Destino**  
 Digite o nome ou o endereço IP do servidor de destino ou escolha um servidor na lista.  
  
> [!NOTE] Se você estiver em uma rede com vários servidores, poderá ser mais fácil digitar o nome do servidor. Se você clicar na lista suspensa, poderá demorar muito tempo para consultar todos os servidores disponíveis na rede e o nome do servidor poderá não estar listado nos resultados.  
 
 Para especificar uma porta TCP não padrão, digite uma vírgula após o nome do servidor ou endereço IP, em seguida digite o número da porta.
 
 **Catálogo Inicial**  
 Digite o nome do banco de dados de destino ou escolha um banco de dados na lista.  
  
 **Segurança Integrada**  
 Especifique **True** para estabelecer conexão usando a autenticação integrada do Windows (recomendado) ou **False** para estabelecer conexão usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se você especificar **False**, deverá inserir uma ID de usuário e uma senha. O valor padrão é **Falso**.  
  
 **ID de usuário**  
 Forneça um nome de usuário para estabelecer conexão de banco de dados quando estiver usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Senha**  
 Forneça uma senha para estabelecer conexão de banco de dados quando estiver usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

## <a name="oracle"></a>Oracle

Conectar-se ao Oracle usando o Provedor de Dados .NET Framework para Oracle ou o Provedor Microsoft OLE DB para Oracle. O Provedor .NET Framework para Oracle é mais fácil de configurar e é mostrado na captura de tela a seguir.

Para obter mais informações, consulte [Cadeias de conexão do Provedor de Dados .NET Framework para Oracle](https://www.connectionstrings.com/net-framework-data-provider-for-oracle/) ou [Cadeias de conexão do Provedor de Dados Microsoft OLE DB para Oracle](https://www.connectionstrings.com/microsoft-ole-db-provider-for-oracle-msdaora/).

![Destino Oracle](../../integration-services/import-export-data/media/oracle-destination.png)

## <a name="odbc-destinations"></a>Destinos ODBC

Para salvar os dados em qualquer destino que fornece um driver ODBC, selecione o Provedor de Dados .NET Framework para ODBC.

Para fornecer uma cadeia de conexão para um destino ODBC, consulte a documentação do driver ODBC que você quer usar ou procure exemplos aqui – [The Connection Strings Reference](https://www.connectionstrings.com/). 

A captura de tela a seguir mostra uma conexão ODBC com o SQL Server como exemplo. A cadeia de conexão usada no exemplo é:

    Driver={SQL Server};Server=(local);Database=TestData;Trusted_Connection=Yes;

Depois de inserir a cadeia de conexão no campo **ConnectionString**, o assistente analisa a cadeia de caracteres e exibe as propriedades individuais e seus valores na seção **Misc** da lista.

![Destino SQL de conexão ODBC](../../integration-services/import-export-data/media/odbc-connection-sql-destination.png)

 ## <a name="text-files-flat-files"></a>Arquivos de texto (arquivos simples)
 
![Destino de arquivo simples](../../integration-services/import-export-data/media/flat-file-destination.png)  

**Nome do arquivo**  
 Especifique o caminho e o nome de arquivo do arquivo no qual deseja armazenar os dados. Se preferir, clique em **Procurar** para localizar um arquivo.  
  
 **Procurar**  
 Localize um arquivo usando a caixa de diálogo **Abrir**.  
  
 **Localidade**  
 Especifique a ID de localidade (LCID) que define as ordens de classificação de caracteres e a formatação de data e hora.  
  
 **Unicode**  
 Indique se deve ser usado o Unicode. Se decidir usá-lo, não será possível especificar uma página de códigos.  
  
 **Página de código**  
 Especifique a página de códigos da linguagem que deseja usar.  
  
 **Formato**  
 Indique se será usada formatação delimitada, de largura fixa ou irregular à direita.  
  
|Value|Description|  
|-----------|-----------------|  
|Delimitado|As colunas são separadas por um delimitador.|  
|Largura fixa|As colunas têm uma largura fixa.|  
|Irregular à direita|Nos arquivos irregulares à direita, todas as colunas têm uma largura fixa, com exceção da última, que é delimitada pelo delimitador de linha.|  
  
 **Qualificador de texto**  
 Digite o qualificador de texto a ser usado. Por exemplo, você pode especificar que cada coluna de texto seja destacada com aspas.  
  
 **Nomes de coluna na primeira linha de dados**  
 Indique se você deseja exibir os nomes de coluna na primeira linha de dados.  
 
 ## <a name="microsoft-excel"></a>Microsoft Excel

>  **Vídeo**: um uso comum do assistente é exportar dados para o Excel. Assista a um vídeo de quatro minutos do YouTube que explica como fazer isso com instruções simples e claras. [Using the SQL Server Import and Export Wizard to Export to Excel](https://go.microsoft.com/fwlink/?linkid=829049) (Usando o Assistente de Importação e Exportação do SQL Server para exportar para o Excel). (O vídeo usa o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 2012.)

A captura de tela a seguir mostra uma conexão de exemplo a uma pasta de trabalho do Microsoft Excel.

![Destino do Excel](../../integration-services/import-export-data/media/excel-destination.png) 
 
 **Caminho de Arquivo do Excel**  
 Especifique o caminho e nome de arquivo da planilha para a qual os dados serão importados. Por exemplo, **C:\\MyData.xlsx** para um arquivo no computador local ou **\\\\Sales\\Database\\Northwind.xlsx** para um arquivo em um compartilhamento de rede. Se preferir, clique em **Procurar**.   
  
 **Procurar**  
 Localize a planilha usando a caixa de diálogo **Abrir**.  

> [!NOTE] O assistente não pode abrir um arquivo do Excel protegido por senha.

 **Versão do Excel**  
Selecione a versão do Excel usada pela pasta de trabalho de destino.  

Talvez seja necessário baixar e instalar arquivos adicionais para se conectar à versão do Excel selecionada. Consulte [Obter os downloads necessários para Excel e Access](Choose%20a%20Data%20Source%20\%28SQL%20Server%20Import%20and%20Export%20Wizard%29.md\#officeDownloads) nesta página para obter mais informações.

Se tiver problemas ao especificar uma versão (por exemplo, se não for possível instalar o tempo de execução do Access 2016 porque você já tem o Microsoft Office 365), tente especificar uma versão diferente, até mesmo uma versão anterior, por exemplo, 2013, em vez da 2016.

**Primeira linha tem nomes de coluna**  
Essa opção parece não ter nenhum efeito para um destino do Excel. Se o destino não tiver nomes de coluna, o driver não gerará nomes de coluna, mesmo com essa opção habilitada. Internamente, o assistente usa F1, F2 e assim por diante como títulos de coluna temporários.
 
## <a name="microsoft-access"></a>Microsoft Access  

A captura de tela a seguir mostra uma conexão de exemplo a um banco de dados do Microsoft Access.

![Destino do Access](../../integration-services/import-export-data/media/access-destination.png)

 **Nome do arquivo**  
 Especifique o caminho e o nome do arquivo de banco de dados para o qual os dados serão importados. Por exemplo, **C:\MyData.mdb, \\\Sales\Database\Northwind.mdb**. Se preferir, clique em **Procurar**.
 
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
Para usar o destino de Blob do Azure, você precisa instalar o pacote de recursos do Azure para SSIS. Para obter mais informações, consulte [Feature Pack do Azure para o Integration Services &#40;SSIS&#41;](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).  

>   [!NOTE] Para garantir que o Gerenciador de Conexões do Armazenamento do Azure e os componentes que o utilizam, incluindo o Destino do Blob, podem se conectar às contas de armazenamento de uso geral e às contas de armazenamento de blobs, verifique se você baixou a versão mais recente do Azure Feature Pack [aqui](https://www.microsoft.com/download/details.aspx?id=49492). Para obter mais informações sobre esses dois tipos de contas de armazenamento, consulte [Introdução ao Armazenamento do Microsoft Azure](https://azure.microsoft.com/en-us/documentation/articles/storage-introduction/#general-purpose-storage-accounts).

![Destino do blob do Azure](../../integration-services/import-export-data/media/azure-blob-destination.png)

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
 Depois de fornecer informações sobre o destino dos dados e sobre como se conectar a eles, a próxima página é **Especificar cópia ou consulta de tabela**. Nessa página, você especifica se quer copiar uma tabela inteira ou apenas algumas linhas. Para obter mais informações, consulte [Especificar cópia ou consulta de tabela](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md).  
