---
title: O que&#39;novo no SQLXML 4.0 SP1 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- SQLNCLI, SQLXML
- what's new [SQLXML]
- SQLXML, what's new
- migrating SQLXML applications
- redistributing SQLXML
- SQL Server Native Client, SQLXML
- side-by-side installations [SQLXML]
ms.assetid: 48f7720b-1705-402d-93ce-097ff1737877
caps.latest.revision: 67
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ab3336a913a5b2a34c45800858af1b0b371f0746
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37258222"
---
# <a name="what39s-new-in-sqlxml-40-sp1"></a>O que&#39;novo no SQLXML 4.0 SP1
  O [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQLXML 4.0 SP1 inclui várias atualizações e aprimoramentos. Este tópico resume as atualizações e fornece links a informações mais detalhadas. O SQLXML 4.0 SP1 tem aprimoramentos adicionais para dar suporte aos novos tipos de dados apresentados no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]. Este tópico abrange os seguintes assuntos:  
  
-   Instalação do SQLXML 4.0 SP1  
  
-   Problemas da instalação lado a lado  
  
-   SQLXML 4.0 e MSXML  
  
-   Redistribuição do SQLXML 4.0  
  
-   Suporte para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client  
  
-   Suporte para tipos de dados introduzidos no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
  
-   Alterações no XML Bulk Load para o SQLXML 4.0  
  
-   Alterações de chave de registro para o SQLXML 4.0  
  
-   Problemas de migração  
  
## <a name="installing-sqlxml-40-sp1"></a>Instalação do SQLXML 4.0 SP1  
 Antes do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], o SQLXML 4.0 era liberado com o SQL Server e fazia parte da instalação padrão de todas as versões do SQL Server com exceção do SQL Server Express. A partir do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], a última versão do SQLXML (SQLXML 4.0 SP1) não está mais incluída no SQL Server. Para instalar o SQLXML 4.0 SP1, baixe-o do [local de instalação do SQLXML 4.0 SP1](http://www.microsoft.com/download/details.aspx?id=30403).  
  
 Os arquivos do SQLXML 4.0 SP1 são instalados no seguinte local:  
  
 `%PROGRAMFILES%\SQLXML 4.0\`  
  
> [!NOTE]  
>  Todas as configurações adequadas de registro são feitas para o SQLXML 4.0 como parte do processo de instalação.  
  
 Para permitir que os aplicativos SQLXML de 32 bits sejam executados no Windows on Windows (WOW64) em sistemas operacionais Windows de 64 bits, execute o pacote SQLXML 4.0 SP1 de 64 bits, chamado sqlxml4.msi, que está disponível no Centro de download.  
  
#### <a name="uninstalling-sqlxml-40-sp1"></a>Desinstalação do SQLXML 4.0 SP1  
 Existem chaves de registro compartilhadas entre o SQLXML 3.0 SP3, o SQLXML 4.0 e o SQLXML 4.0 SP1. Se as versões posteriores do SQLXML forem desinstaladas no mesmo computador que contém o SQLXML 3.0 SP3, talvez seja necessário reinstalar o SQLXML 3.0 SP3.  
  
## <a name="side-by-side-installation-issues"></a>Problemas da instalação lado a lado  
 O processo de instalação para SQLXML 4.0 não remove os arquivos que foram instalados pelas versões anteriores do SQLXML. Portanto, você pode ter DLLs para várias instalações de versões diferentes do SQLXML em seu computador. É possível executar as instalações lado a lado. O SQLXML 4.0 inclui tanto ProgIDs dependentes de versão como independentes de versão. Todos os aplicativos de produção devem usar PROGIDs dependentes de versão.  
  
## <a name="sqlxml-40-sp1-and-msxml"></a>SQLXML 4.0 SP1 e MSXML  
 O SQLXML 4.0 não instala o MSXML. O SQLXML 4.0 usa o MSXML 6.0, que é instalado como parte da instalação do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou posterior.  
  
## <a name="redistributing-sqlxml-40-sp1"></a>Redistribuição do SQLXML 4.0 SP1  
 É possível distribuir o SQLXML 4.0 SP1 usando o pacote do instalador redistribuível. Uma maneira de instalar vários pacotes em um processo que, para o usuário, parece ser uma única instalação é usar a tecnologia de encadeador e bootstrapper. Para obter mais informações, consulte as seções sobre Criação de um pacote de bootstrapper personalizado para o Visual Studio 2005 e Adição de pré-requisitos personalizados.  
  
 Se o aplicativo foi projetado para uma plataforma diferente daquela em que foi desenvolvido, você poderá baixar as versões do sqlncli.msi para x64, Itanium e x86 do Centro de Download da Microsoft.  
  
 Também há programas de instalação de redistribuição separados o MSXML 6.0 (msxml6.msi). Eles podem ser encontrados no CD de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no seguinte local:  
  
 `%CD%\Setup\`  
  
 Esses arquivos de instalação podem ser usados para instalar o MSXML 6.0 diretamente do CD. Eles também podem ser usados, de forma independente, para redistribuir o MSXML 6.0 junto com o SQLXML 4.0 SP1 com seus próprios aplicativos personalizados.  
  
 Você também precisará redistribuir o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client se estiver usando-o como o provedor de dados com seu aplicativo. Para obter mais informações, consulte [Instalando o SQL Server Native Client](../native-client/applications/installing-sql-server-native-client.md).  
  
## <a name="support-for-sql-server-native-client"></a>Suporte para SQL Server Native Client  
 O SQLXML 4.0 dá suporte a ambos os SQLOLEDB e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedores de cliente nativo. É recomendável que você use a mesma versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor Native Client e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] porque [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client foi desenvolvido para dar suporte a qualquer tipo de dados novo fornecido no servidor, como o `Date, Time`, `DateTime2`, e `dateTimeOffset` tipos de dados no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e com suporte pelo [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Native Client.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client é uma tecnologia de acesso a dados introduzida no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Ela reúne o provedor SQLOLEDB e o driver SQLODBC em uma única DLL (dynamic link library) nativa fornecendo, ao mesmo tempo, uma nova funcionalidade separada e diferente do MDAC (Microsoft Data Access Components).  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client pode ser usado para criar novos aplicativos ou aprimorar os aplicativos existentes que precisam aproveitar os recursos introduzidos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não são suportados pelo SQLOLEDB e SQLODBC no MDAC e [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Por exemplo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client é necessário para os recursos SQLXML do lado do cliente, como FOR XML, para usar o tipo de dados `xml`. Para obter mais informações, consulte [formatação XML no lado do cliente &#40;SQLXML 4.0&#41;](formatting/client-side-xml-formatting-sqlxml-4-0.md), [usando o ADO para executar consultas do SQLXML 4.0](using-ado-to-execute-sqlxml-4-0-queries.md), e [SQL Server Native Client de programação](../native-client/sql-server-native-client-programming.md).  
  
> [!NOTE]  
>  O SQLXML 4.0 não é totalmente compatível com o SQLXML 3.0. Pelo fato de haver algumas correções de bug e outras alterações funcionais, particularmente a remoção do suporte a SQLXML ISAPI, você não pode usar diretórios virtuais IIS com o SQLXML 4.0. Embora a maioria dos aplicativos será executada com pequenas modificações, você deve testá-los antes de os colocar em produção com o SQLXML 4.0.  
  
## <a name="support-for-data-types-introduced-in-sql-server-2005-and-sql-server-2008"></a>Suporte para tipos de dados introduzidos no SQL Server 2005 e no SQL Server 2008  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] introduziu o `xml` tipo de dados e o SQLXML 4.0 dá suporte ao `xml` tipo de dados. Para obter mais informações, consulte [xml Data Type Support in SQLXML 4.0](xml-data-type-support-in-sqlxml-4-0.md).  
  
 Para obter exemplos de como usar o tipo de dados `xml` no SQLXML durante o mapeamento de exibições XML, o carregamento em massa de dados XML ou a execução de diagramas de atualização XML, consulte os exemplos fornecidos nos tópicos a seguir.  
  
-   [Mapeamento de atributos e elementos XSD para tabelas e colunas padrão](../sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)  
  
-   [Inserindo dados usando diagramas de atualização XML](../sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)  
  
-   [Exemplos de documentos XML de carregamento em massa](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)  
  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] introduziu o `Date, Time`, `DateTime2`, e **DateTimeOffset** tipos de dados. O SQLXML 4.0 SP1 habilitará esses quatro novos tipos de dados como tipos escalares internos quando usados com o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Native Client OLE DB Provider (SQLNCLI11) que é fornecido com o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="xml-bulk-load-changes-for-sqlxml-40-sp1"></a>Alterações no XML Bulk Load para o SQLXML 4.0 SP1  
  
-   Para SQLXML 4.0, o campo de estouro SchemaGen é criado usando o `xml` tipo de dados. Para obter mais informações, consulte [SQL Server XML Bulk Load Object Model](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/sql-server-xml-bulk-load-object-model-sqlxml-4-0.md).  
  
-   Se você tiver criado anteriormente aplicativos do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic e deseja usar o SQLXML 4.0, deverá recompilar o aplicativo com referência à Xblkld4.dll.  
  
-   No caso dos aplicativos do Visual Basic Scripting Edition, você deve registrar a DLL que deseja usar. No seguinte exemplo, se você especificar os ProgIDs independentes de versão, o aplicativo dependerá da última DLL registrada:  
  
    ```  
    set objBulkLoad = CreateObject("SQLXMLBulkLoad.SQLXMLBulkLoad")   
    ```  
  
    > [!NOTE]  
    >  O PROGID dependente de versão é o SQLXMLBulkLoad.SQLXMLBulkLoad.4.0.  
  
## <a name="registry-key-changes-for-sqlxml-40"></a>Alterações de chave de registro para o SQLXML 4.0  
 No SQLXML 4.0, as chaves de registro foram alteradas em relação às versões anteriores no seguinte:  
  
 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\TemplateCacheSize  
  
 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\SchemaCacheSize  
  
 Você deve alterar as configurações se quiser que essas chaves entrem em vigor no SQLXML 4.0.  
  
 Além disso, o SQLXML 4.0 introduz as seguintes chaves de registro:  
  
-   `HKEY_LOCAL_MACHINE\Software\Microsoft\MSSQLServer\Client\SQLXML4\ReportErrorsWithSQLInfo`  
  
     Por padrão, o SQLXML 4.0 retorna informações de erros nativos fornecidas pelo OLE DB e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em vez de um erro SQLXML de nível superior (como nas versões anteriores do SQLXML). Se você não quiser esse comportamento, o valor desta chave de registro de tipo Dword deverá ser definido como 0 (o padrão é 1).  
  
-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSSQLServer\Client\SQLXML4\FORXML_GenerateGUIDBraces  
  
     Por padrão, o SQLXML retorna valores GUID do SQL Server sem os colchetes. Se você deseja que o valor GUID seja retornado com os colchetes (por exemplo, {*some GUID*}), o valor dessa chave do registro deve ser definido como 1 (o padrão é 0).  
  
-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSSQLServer\Client\SQLXML4\SQL2000CompatMode  
  
     Por padrão, quando o analisador XML carrega os dados, os espaços em branco são normalizados de acordo com as regras do XML 1.0. Isso resulta na perda de alguns dos caracteres com espaço em branco em seus dados. Assim, a representação textual de seus dados pode não ser a mesma depois da análise, embora os dados sejam semanticamente os mesmos.  
  
     Essa chave é introduzida para que você possa escolher manter os caracteres com espaço em branco nos dados. Se você adicionar essa chave de registro e definir seu valor como 0, os caracteres com espaço em branco (LF, CR e tab) no XML serão retornados codificados em caso de valores de atributo. No caso de valores de elemento, somente CR é retornado codificado.  
  
     Por exemplo:  
  
    ```  
    CREATE TABLE T( Col1 int, Col2 nvarchar(100));  
    GO  
    -- Insert data with tab, line feed and carriage return).  
    INSERT INTO T VALUES (1, 'This is a tab    . This is a line feed and CR   
     more text');  
    GO  
    -- Test this query (without the registry key).  
    SELECT * FROM T   
    FOR XML AUTO;  
    -- This is the result (no encoding of special characters).  
    <?xml version="1.0" encoding="utf-8" ?>  
    <r>  
      <T Col1="1"   
         Col2="This is a tab    . This is a line feed and CR   
     more text"/>  
    </r>  
    -- Now add registry key with value 0 and execute the query again.  
    -- Note the encoding for carriage return, line-feed and tab in the attribute value.  
    <?xml version="1.0" encoding="utf-8" ?>  
    <r>  
      <T Col1="1"   
         Col2="This is a tab    . This is a line feed and CR   
     more text"/>  
    </r>  
  
    -- Update the query and specify ELEMENTS directive  
    SELECT * FROM T  
    FOR XML AUTO, ELEMENTS  
    -- Only the carriage return is returned encoded.  
    <?xml version="1.0" encoding="utf-8" ?>  
    <r>  
       <T>  
          <Col1>1</Col1>  
          <Col2>This is a tab    . This is a line feed and CR   
     more text</Col2>  
       </T>  
    </r>  
    ```  
  
## <a name="migration-issues"></a>Problemas de migração  
 A seguir, são citadas algumas questões que poderiam impactar a migração de seus aplicativos SQLXML herdados para o SQLXML 4.0.  
  
### <a name="ado-and-sqlxml-40-queries"></a>Consultas ADO e SQLXML 4.0  
 Nas versões anteriores do SQLXML, havia suporte para a execução de consultas baseadas em URL usando diretórios virtuais IIS e o filtro ISAPI SQLXML. Para aplicativos que usam SQLXML 4.0, este suporte não está mais disponível.  
  
 Em vez disso, as consultas, modelos e diagramas de atualização SQLXML podem ser executados com as extensões SQLXML para ADO (ActiveX Data Objects) introduzidas pela primeira vez no MDAC (Microsoft Data Access Components) 2.6 e versão posterior.  
  
 Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4.0](using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="supportability-for-sqlxml-30-isapi-and-data-types-introduced-in-sql-server-2005"></a>Suporte para SQLXML 3.0 ISAPI e tipos de dados introduzidos no SQL Server 2005  
 Porque o suporte a ISAPI foi removido do SQLXML 4.0, se sua solução exige a digitação de dados aprimorados recursos introduzidos no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] como o [tipo de dados xml](/sql/t-sql/xml/xml-transact-sql) ou [tipos de dados definidos pelo usuário (UDTs)](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)e acesso baseado na Web, você precisará usar outra solução, como [classes gerenciadas SQLXML](../sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-4-0-net-framework-support-managed-classes.md) ou outro tipo de manipulador HTTP, como o XML Web Services nativos para SQL Server 2005.  
  
 Como alternativa, se você não precisar dessas extensões de tipo, você pode continuar a usar o SQLXML 3.0 para se conectar ao [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] instalações. O suporte a SQLXML 3.0 ISAPI funcionará nessas versões mais recentes, mas não suporta nem reconhece o tipo de dados `xml` ou o suporte a tipos de dados UDT introduzido no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
### <a name="xml-bulk-load-security-changes-for-temporary-files"></a>Alterações de segurança do XML Bulk Load para arquivos temporários  
 Para o SQLXML 4.0 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], são concedidas permissões de arquivo do XML Bulk Load ao usuário que executa a operação de carregamento em massa. As permissões de leitura e gravação são herdadas do sistema de arquivos. Nas versões anteriores do SQLXML e SQL Server, o XML Bulk Load em SQLXML criava arquivos temporários que não eram seguros e que podiam ser lidos por qualquer pessoa.  
  
### <a name="migration-issues-for-client-side-for-xml"></a>Problemas de migração para FOR XML do lado do cliente  
 Devido a alterações no mecanismo de execução, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem retornar valores diferentes nos metadados para uma tabela base que seria retornado se a consulta FOR XML fosse executada em [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. Nesses casos, a formatação no lado do cliente dos resultados de consulta FOR XML terá uma saída diferente dependendo da versão em que a consulta estiver sendo executada.  
  
 Se uma consulta FOR XML for executada no lado do cliente com SQLXML 3.0 em uma coluna de tipo de dados `xml`, os dados resultantes serão retornados como uma cadeia de caracteres com entidade completa criada. No SQLXML 4.0, se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client (SQLNCLI11) for especificado como o provedor, os dados serão retornados como XML.  
  
  
