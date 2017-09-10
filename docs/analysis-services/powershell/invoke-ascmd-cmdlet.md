---
title: Cmdlet Invoke-ASCmd | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 2896b74a-3911-4b3f-89ab-bb375bdb34d8
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 366263980ae7ad9d5a792e6525888080a38ebbf6
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="invoke-ascmd-cmdlet"></a>Cmdlet Invoke-ASCmd

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Permite que um administrador de banco de dados execute um script XMLA, MDX (Multidimensional Expressions), instruções ou script TMSL (Tabular Model Scripting Language).  
  
 O TMSL só tem suporte para o modo de servidor Tabular em uma instância do SQL Server 2016 Analysis Services.  
  
 Se você quiser criar bancos de dados ou outros objetos, esse é o cmdlet que usaria, com um arquivo de entrada de script.  
  
## <a name="syntax"></a>Sintaxe  
 `Invoke-ASCmd –Query <string> [-Server <string>] [-Database <string>] [-Credential <PSCredential>] [-ConnectionTimeout <int>] [-QueryTimeout <int>] [-Variable <string[]>] [-TraceFile <string>] [-TraceFileFormat <TraceFileFormatOption>] [-TraceFileDelimiter <string>] [-TraceTimeout <int>] [-TraceLevel <TraceLevelOption>] [<CommonParameters>]`  
  
 `Invoke-ASCmd –InputFile <string> [-Server <string>] [-Database <string>] [-Credential <PSCredential>] [-ConnectionTimeout <int>] [-QueryTimeout <int>] [-Variable <string[]>] [-TraceFile <string>] [-TraceFileFormat <TraceFileFormatOption>] [-TraceFileDelimiter <string>] [-TraceTimeout <int>] [-TraceLevel <TraceLevelOption>] [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 O cmdlet Invoke-ASCmd pode executar consultas ou scripts que estão contidos em arquivos de entrada.  
  
 Para o XMLA, os seguintes comandos têm suporte: Alter, Backup, Batch, BeginTransaction, Cancel, ClearCache, CommitTransaction, Create, Delete, DesignAggregations, Drop, Insert, Lock, MergePartitions, NotifyTableChange, Process, Restore, RollbackTransaction, Statement (usados para executar consultas MDX e instruções DMX), Subscribe, Synchronize, Unlock, Update, UpdateCells.  
  
 Para TMSL: Alter, Create, Delete, MergePartitions, Process, Update.  
  
 Esse cmdlet oferece suporte ao parâmetro –Credential, que pode ser usado se você configurar a instância do Analysis Services para acesso HTTP. O parâmetro –Credential usa o objeto PSCredential que fornece uma identidade de usuário do Windows. O IIS representará esse usuário ao conectar-se ao Analysis Services. A identidade deve ter permissões de administrador de sistema na instância do Analysis Services para executar o script.  
  
## <a name="parameters"></a>Parâmetros  
  
### <a name="-query-string"></a>-Consulta \<cadeia de caracteres >  
 Especifica o script, consulta ou instrução atual diretamente na linha de comando em vez de em um arquivo. Você também pode especificar uma consulta como entrada do pipeline. É necessário especificar um valor para o parâmetro **–InputFile** ou **–Query** ao usar **Invoke-AsCmd**.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|True (ByValue)|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-inputfile-string"></a>-InputFile \<cadeia de caracteres >  
 Identifica o arquivo que contém o script XMLA, a consulta MDX, a instrução DMX ou o script TMSL (no JSON). É necessário especificar um valor para o parâmetro **–InputFile** ou **–Query** ao usar **Invoke-AsCmd**.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-server-string"></a>-Servidor \<cadeia de caracteres >  
 Especifica a instância do Analysis Services que o cmdlet conectará e executará. Se nenhum nome de servidor for fornecido, uma conexão será feita com o localhost. Para instâncias padrão, especifique apenas o nome do servidor. Para instâncias nomeadas, use o formato nome_do_servidor\nome_da_instância. Para conexões HTTP, use o formato http[s]://servidor[:porta]/diretório_virtual/msmdpump.dll.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão|localhost|  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-database-string"></a>-Banco de dados \<cadeia de caracteres >  
 Especifica o banco de dados em que será executada uma consulta MDX ou uma instrução DMX. O parâmetro de banco de dados é ignorado quando o cmdlet executa um script XMLA, pois o nome de banco de dados está inserido no script XMLA.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-credential-pscredential"></a>-Credential \<PSCredential >  
 Especifica um objeto –Credential que fornece um nome de usuário e senha do Windows. Especifique esse parâmetro somente se a instância do Analysis Services estiver configurada para acesso HTTP, usando a autenticação básica. Para conexões nativas que usam a segurança integrada, esse parâmetro é ignorado.  
  
 Se esse parâmetro estiver presente, as credenciais que ele fornece serão anexadas à cadeia de conexão. O IIS representará essa identidade de usuário ao conectar-se ao Analysis Services. Se nenhuma credencial for especificada, será usada a conta do Windows padrão do usuário que está executando a ferramenta.  
  
 Para usar este parâmetro, primeiro crie um objeto PSCredential usando Get-Credential para especificar o nome de usuário e a senha (por exemplo, `$Cred=Get-Credential “adventure-works\admin”`. Você pode redirecionar este objeto para o parâmetro –Credential `(-Credential:$Cred`).  
  
   Para obter mais informações sobre o acesso HTTP, consulte [Configurar o acesso HTTP ao Analysis Services no IIS &#40;(Serviços de Informações da Internet)&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md).  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|True (ByValue)|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-connectiontimeout-int"></a>-ConnectionTimeout \<int >  
 Especifica o número de segundos antes que a conexão para a instância do Analysis Services expire. O valor do tempo limite deve ser um inteiro entre 0 e 65534. Se 0 for especificado, as tentativas de conexão não atingirão o tempo limite.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão|30|  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-querytimeout-int"></a>-QueryTimeout \<int >  
 Especifica o número de segundos antes de as consultas expirarem. Se o valor de tempo limite não for especificado, as consultas não atingirão o tempo limite. O tempo limite deve ser um inteiro entre 1 e 65535.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão|30|  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-variable-string"></a>-Variável \<string [] >  
 Especifica variáveis de script adicionais. Cada variável é um par de nome-valor. Se o valor contém espaços inseridos ou caracteres de controle, ele deve estar entre aspas duplas("). Use uma matriz do PowerShell para especificar as diversas variáveis e seus valores.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-tracefile-string"></a>-TraceFile \<cadeia de caracteres >  
 Identifica um arquivo que recebe eventos de rastreamento do Analysis Services enquanto executa o script XMLA, consulta MDX ou instrução DMX. Se o arquivo já existir, será substituído automaticamente (exceto os arquivos de rastreamento criados usando as configurações de parâmetro -TraceLevel:Duration e –TraceLevel:DurationResult). Os nomes de arquivo que contêm espaços deverão estar entre aspas (" "). Se o nome do arquivo for inválido, uma mensagem de erro será gerada.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-tracefileformat-string"></a>-TraceFileFormat \<cadeia de caracteres >  
 Especifica o formato de arquivo para o parâmetro –TraceFile (quando esse parâmetro estiver especificado). As opções disponíveis são texto ou csv. O valor padrão é "csv".  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão|csv|  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-tracefiledelimiter-string"></a>-TraceFileDelimiter \<cadeia de caracteres >  
 Especifica qual caractere deve ser usado como o delimitador do arquivo de rastreamento, quando o formato de arquivo de rastreamento .csv for especificado. O padrão é | (barra vertical).  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-tracetimeout-int"></a>-TraceTimeout \<int >  
 Especifica o número de segundos que o mecanismo do Analysis Services espera antes de encerrar o rastreamento (caso o parâmetro –TraceFile seja especificado). O rastreamento será dado como encerrado se nenhuma mensagem de rastreamento for registrada durante o período de tempo especificado. O valor do tempo limite de rastreamento padrão é 5 segundos.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão|5|  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-tracelevel-traceleveloption"></a>-TraceLevel \<TraceLevelOption >  
 Especifica quais dados são coletados e registrados no arquivo de rastreamento. Os valores possíveis valores são: High, Medium, Low, Duration, DurationResult.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão|Alta|  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="commonparameters"></a>\<CommonParameters >  
 Este cmdlet oferece suporte aos parâmetros comuns: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer e -OutVariable. Para obter mais informações, consulte [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## <a name="inputs-and-outputs"></a>Entradas e saídas  
 O tipo de entrada é o tipo dos objetos que você pode transportar para o cmdlet. O tipo de retorno é o tipo dos objetos que o cmdlet retorna.  
  
|||  
|-|-|  
|Entradas|PSObject|  
|Saídas|Cadeia de caracteres|  
  
## <a name="example-1-xmla-input-file"></a>Exemplo 1 (arquivo de entrada XMLA)  
  
```  
Invoke-ASCmd –InputFile:"C:\MyFolder\DiscoverConnections.xmla"  
```  
  
 Este comando executa um script XMLA que retorna a lista de conexões ativas no servidor. O arquivo DiscoverConnections.xmla contém o script XMLA a seguir:  
  
```  
<Discover xmlns="urn:schemas-microsoft-com:xml-analysis">  
<RequestType>DISCOVER_CONNECTIONS</RequestType>  
<Restrictions />  
   <Properties>  
      <PropertyList>  
         <Content>Data</Content>  
      </PropertyList>  
   </Properties>  
</Discover>  
```  
  
## <a name="example-2-tmsl-input-file"></a>Exemplo 2 (arquivo de entrada TMSL)  
 Este exemplo é idêntico ao primeiro, exceto que o script é TMSL (JSON) e requer uma instância de tabela do SQL Server 2016. Assim, você pode executar um script TMSL no SQL Server Management Studio.  
  
 Se você tiver várias instâncias e se sua instância de tabela for uma instância nomeada, lembre-se de definir o nome do servidor:  
  
```  
Invoke-ASCmd –InputFile "C:\folder-name\T1200-NewDB.json" -Server "server-name\instance-name"  
```  
  
## <a name="example-3-query"></a>Exemplo 3 (Consulta)  
  
```  
Invoke-ASCmd -Database:"Adventure Works DW" -Query:"<Discover xmlns='urn:schemas-microsoft-com:xml analysis'><RequestType>DISCOVER_DATASOURCES</RequestType><Restrictions></Restrictions><Properties></Properties></Discover>"  
```  
  
 A consulta Discover XMLA retorna fontes de dados disponíveis para o Analysis Server e as informações necessárias para se conectar a elas. Os resultados estão em XML. Para facilitar a leitura, você pode redirecionar a saída para um arquivo XML (por exemplo, acrescente `| Out-file C:\Results\XMLAQueryOutput.xml` ao comando) e exibir os resultados em um navegador ou em outro aplicativo que dá suporte a XML estruturado.  
  
  
  
