---
title: Referência de mensagens e erros do Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- error numbers [Integration Services]
- hresults [Integration Services]
- errors [Integration Services], listed
ms.assetid: 2c825c07-5074-42ad-90ea-0dc5a588dcf7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7d55050b132a3367ecc495d0afedcad6f0d2351b
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71284431"
---
# <a name="integration-services-error-and-message-reference"></a>Referência de mensagens e erros do Integration Services

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  As tabelas a seguir listam erros, advertências e mensagens informativas do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , em ordem numérica crescente, dentro de cada categoria, acompanhados de seus códigos numéricos e nomes simbólicos. Cada um desses erros está definido como um campo da classe <xref:Microsoft.SqlServer.Dts.Runtime.Hresults> no namespace <xref:Microsoft.SqlServer.Dts.Runtime> .  
  
 Esta lista pode ser útil quando você encontrar um código de erro sem descrição. No momento, a lista não inclui informações para solução de problemas.  
  
> [!IMPORTANT]  
>  Muitas das mensagens de erro exibidas enquanto você trabalha com o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] são de outros componentes. Neste tópico, são apresentados todos os erros provocados pelos componentes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Caso você não encontre seu erro na lista, ele foi provocado por um componente fora do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Entre eles, provedores OLE DB, outros componentes de banco de dados, como o [!INCLUDE[ssDE](../includes/ssde-md.md)] e [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , ou outros serviços ou componentes, como o sistema de arquivos, servidor SMTP, MSMQ (serviço de enfileiramento de mensagens) e assim por diante. Para obter informações sobre essas mensagens externas de erro, consulte a documentação específica do componente.  
  
 Esta lista contém os seguintes grupos de mensagens:  
  
-   [Mensagens de erro (DTS_E_ *)](#msgError)  
  
-   [Mensagens de aviso (DTS_W_ *)](#msgWarning)  
  
-   [Mensagens informativas (DTS_I_ *)](#msgInfo)  
  
-   [Mensagens de evento e gerais (DTS_MSG_ *)](#msgGeneral)  
  
-   [Mensagens de êxito (DTS_S_ *)](#msgSuccess)  
  
-   [Mensagens de erro do componente de fluxo de dados (DTSBC_E_ *)](#msgPipeline)  
  
##  <a name="msgError"></a> Mensagens de erro  
 Os nomes simbólicos das mensagens de erro do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] começam com **DTS_E_** .  
  
|Código hexadecimal|Código decimal|Nome simbólico|Descrição|  
|----------------------|------------------|-------------------|-----------------|  
|0x8002F347|-2147290297|DTS_E_STOREDPROCSTASK_OVERWRITINGSPATDESTINATION|Substituição do procedimento armazenado "%1" no destino.|  
|0x8020837E|-2145352834|DTS_E_ADOSRCUNKNOWNTYPEMAPPEDTONTEXT|Não existe suporte para o tipo de dados "%1" encontrado na coluna "%2" para o %3. Essa coluna será convertida em DT_NTEXT.|  
|0x8020838C|-2145352820|DTS_E_XMLSRCSCHEMACOLUMNNOTINEXTERNALMETADATA|A coluna %1 na tabela %2 no esquema XML não tem um mapeamento nas colunas de metadados externos.|  
|0xC0000032|-1073741774|DTS_E_NOTINITIALIZED|Um objeto interno ou uma variável não foi inicializada. Esse é um erro interno de produto.  Esse erro é retornado quando uma variável deveria ter um valor válido, mas não tem.|  
|0xC0000033|-1073741773|DTS_E_EXPIRED|O período de avaliação do Integration Services expirou.|  
|0xC0000034|-1073741772|DTS_E_NEGATIVEVALUESNOTALLOWED|Um valor negativo não pode ser atribuído a essa propriedade. Esse erro ocorre quando um valor negativo é atribuído a uma propriedade que pode conter somente valores positivos, como a propriedade COUNT.|  
|0xC0000035|-1073741771|DTS_E_NEGATIVEINDEXNOTALLOWED|Índices não podem ser negativos. Esse erro ocorre quando um valor negativo é usado como índice de uma coleção.|  
|0xC00060AB|-1073717077|DTS_E_INVALIDSSISSERVERNAME|Nome do servidor inválido "%1". O serviço SSIS não dá suporte a várias múltiplas, use apenas o nome do servidor, em vez de "nome do servidor\instância".|  
|0xC0008445|-1073707963|DTS_E_SCRIPTMIGRATIONFAILED64BIT|A migração para scripts VSA não pode ser feita em plataformas de 64 bits devido à falta de ferramentas visuais para suporte ao designer de Aplicativos. Execute a migração sob WOW64 em plataformas de 64 bits.|  
|0xC000931A|-1073704166|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_ERRORSINCOMMAND|A execução de comando gerou erros.|  
|0xC000F427|-1073679321|DTS_E_SSISSTANDALONENOTINSTALLED|Para executar um pacote SSIS fora do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] , você deve instalar %1 do Integration Services ou superior.|  
|0xC0010001|-1073676287|DTS_E_VARIABLENOTFOUND|A variável não pode ser encontrada. Isso ocorre quando se tenta recuperar uma variável da coleção Variables em um contêiner durante a execução do pacote e a variável não existe. O nome da variável pode ter sido alterado ou a variável não está sendo criada.|  
|0xC0010003|-1073676285|DTS_E_VARIABLEREADONLY|Erro ao tentar gravar em uma variável somente leitura "%1".|  
|0xC0010004|-1073676284|DTS_E_MANAGEDCOMPONENTSTORENOTFOUND|Não é possível localizar os diretórios que contêm os componentes Tarefas e Tarefa de Fluxo de Dados. Verifique a integridade da sua instalação.|  
|0xC0010006|-1073676282|DTS_E_PACKAGENAMETOOLONG|O nome do pacote é muito longo. O limite é 128 caracteres. Encurte o nome do pacote.|  
|0xC0010007|-1073676281|DTS_E_PACKAGEDESCRIPTIONTOOLONG|A descrição do pacote é muito longa. O limite é 1.024 caracteres. Encurte a descrição do pacote.|  
|0xC0010008|-1073676280|DTS_E_VERCOMMENTSTOOLONG|A propriedade VersionComments é muito longa. O limite é 1.024 caracteres. Tente encurtar a propriedade VersionComments.|  
|0xC0010009|-1073676279|DTS_E_ELEMENTNOTFOUND|O elemento não pode ser encontrado em uma coleção. Esse erro ocorre quando se tenta recuperar um elemento de uma coleção em um contêiner durante a execução do pacote e o elemento não existe.|  
|0xC001000A|-1073676278|DTS_E_PACKAGENOTFOUND|Não foi possível carregar o pacote especificado a partir do banco de dados do SQL Server.|  
|0xC001000C|-1073676276|DTS_E_INVALIDVARIABLEVALUE|A atribuição de valor à variável não é válida. Esse erro ocorre quando o cliente ou uma tarefa atribui um objeto de tempo de execução a um valor de variável.|  
|0xC001000D|-1073676275|DTS_E_RESERVEDNAMESPACE|Erro ao atribuir namespace à variável. O namespace "System" é reservado para uso do sistema. Esse erro ocorre quando um componente ou uma tarefa tenta criar uma variável com um namespace de "System".|  
|0xC001000E|-1073676274|DTS_E_CONNECTIONNOTFOUND|Não foi possível encontrar a conexão "%1". Esse erro é acionado pela coleção Conexões quando o elemento específico de conexão não é encontrado.|  
|0xC001000F|-1073676273|DTS_E_64BITVARIABLERECAST|A variável "%1" é uma variável de inteiro de 64 bits, que não tem suporte neste sistema operacional. A variável foi reconvertida a um inteiro de 32 bits.|  
|0xC0010010|-1073676272|DTS_E_CANTCHANGEREADONLYATRUNTIME|Ocorreu uma tentativa de alteração para um atributo somente leitura na variável "%1". Esse erro ocorre quando se está alterando um atributo somente leitura de uma variável no tempo de execução. Os atributos somente leitura podem ser alterados apenas no tempo de design.|  
|0xC0010011|-1073676271|DTS_E_VARIABLEINVALIDCONTAINERREF|Tentativa inválida de definir uma variável para uma referência de contêiner.  As variáveis não têm permissão para referenciar contêineres.|  
|0xC0010013|-1073676269|DTS_E_INVALIDVARVALUE|Atribuição de valor ou objeto inválido à variável "%1". Esse erro ocorre quando o valor não é apropriado para variáveis.|  
|0xC0010014|-1073676268|DTS_E_GENERICERROR|Ocorreu um ou mais erros. Deve haver mais erros específicos precedentes a este que expliquem os detalhes dos erros. Essa mensagem é usada como valor de retorno de funções que encontram erros.|  
|0xC0010016|-1073676266|DTS_E_INVALIDARRAYVALUE|Erro ao adquirir ou definir um valor de matriz. O tipo "%1" não é permitido. Isso ocorre ao carregar uma matriz em uma variável.|  
|0xC0010017|-1073676265|DTS_E_UNSUPPORTEDARRAYTYPE|Tipo sem-suporte na matriz. Isso ocorre quando se salva uma matriz com tipos sem-suporte em uma variável.|  
|0xC0010018|-1073676264|DTS_E_PERSISTENCEERROR|Erro ao carregar o valor "%1" do nó "%2".|  
|0xC0010019|-1073676263|DTS_E_INVALIDNODE|O nó "%1" é inválido. Isso ocorre ao salvar falhas.|  
|0xC0010020|-1073676256|DTS_E_ERRORLOADINGTASK|Falha ao carregar a tarefa "%1", tipo "%2". As informações de contato para essa tarefa são "%3".|  
|0xC0010021|-1073676255|DTS_E_ERRORELEMENTNOTINCOLL|O elemento "%1" não existe na coleção "%2".|  
|0xC0010022|-1073676254|DTS_E_MISSINGOBJECTDATA|Falta o elemento ObjectData no bloco XML de um objeto hospedado. Isso ocorre quando o analisador XML tenta localizar o elemento de dados de um objeto e não consegue encontrá-lo.|  
|0xC0010023|-1073676253|DTS_E_VARIABLENOTFOUNDINCOLL|Não é possível encontrar a variável "%1". Esse erro ocorre quando se tenta recuperar uma variável de uma coleção de variáveis em um contêiner durante a execução do pacote e a variável não existe.  Um nome de variável pode ter sido alterado ou a variável não está sendo criada.|  
|0xC0010025|-1073676251|DTS_E_HASEMPTYTASKHOSTS|O pacote não pode ser executado por conter tarefas que falharam ao ser carregadas.|  
|0xC0010026|-1073676250|DTS_E_TASKISEMPTY|Houve falha no carregamento da tarefa. As informações de contato dessa tarefa são "%1".|  
|0xC0010027|-1073676249|DTS_E_ERRORLOADINGTASKNOCONTACT|Erro ao carregar a tarefa "%1".|  
|0xC0010028|-1073676248|DTS_E_ERRORATLOADTASK|Erro ao carregar a tarefa. Isso ocorre quando há falha no carregamento de uma tarefa do XML.|  
|0xC0010200|-1073675776|DTS_E_MULTIPLECACHEWRITES|O %1 não pode gravar em cache porque %2 já gravou nele.|  
|0xC0010201|-1073675775|DTS_E_SETCACHEFORINSERTFAILED|Falha ao preparar o cache para obter dados novos.|  
|0xC0010202|-1073675774|DTS_E_SETCACHEFORFILLFAILED|Falha ao marcar o cache como preenchido com dados.|  
|0xC0010203|-1073675773|DTS_E_READUNINITIALIZEDCACHE|O cache não foi inicializado e não pode ser lido por %1.|  
|0xC0010204|-1073675772|DTS_E_SETCACHEFORREADFAILED|Falha ao preparar o cache para fornecer dados.|  
|0xC0010205|-1073675771|DTS_E_READNOTFILLEDCACHE|O cache está sendo gravado por %1 e não pode ser lido por %2.|  
|0xC0010206|-1073675770|DTS_E_WRITEWHILECACHEINUSE|O cache está sendo lido a partir de %1 e não pode ser gravado por %2.|  
|0xC0011001|-1073672191|DTS_E_CANTLOADFROMNODE|O objeto de tempo de execução não pode ser carregado a partir do nó XML especificado.  Isso ocorre quando se tenta carregar um pacote ou outro objeto de um nó XML que não é do tipo correto, como um nó XML não SSIS.|  
|0xC0011002|-1073672190|DTS_E_OPENPACKAGEFILE|Falha ao abrir o arquivo de pacote "%1" devido ao erro 0x%2!8.8X! "%3".  Isso ocorre quando se está abrindo um pacote e o arquivo não pode ser aberto ou carregado corretamente no documento XML. Esse erro pode resultar da especificação de um nome de arquivo incorreto ao chamar LoadPackage ou de um arquivo XML no formato incorreto.|  
|0xC0011003|-1073672189|DTS_E_LOADPACKAGEXML|Falha ao carregar XML devido ao erro 0x%1!8.8X! "%2". Isso ocorre quando se está carregando um pacote e o arquivo não pode ser aberto ou carregado corretamente no documento XML.  Esse erro pode resultar da especificação de um nome de arquivo incorreto para o método LoadPackage ou de um arquivo XML no formato incorreto.|  
|0xC0011004|-1073672188|DTS_E_LOADPACKAGEXMLFILE|Falha ao carregar XML do arquivo de pacote "%1" devido ao erro 0x%2!8.8X! "%3".  Isso ocorre quando se está carregando um pacote e o arquivo não pode ser aberto ou carregado corretamente no documento XML. Esse erro pode resultar da especificação de um nome de arquivo incorreto para o método LoadPackage ou de um arquivo XML no formato incorreto.|  
|0xC0011005|-1073672187|DTS_E_OPENFILE|Falha ao abrir o arquivo de pacote. Isso ocorre quando se está carregando um pacote e o arquivo não pode ser aberto ou carregado corretamente no documento XML. Esse erro pode resultar da especificação de um nome de arquivo incorreto para o método LoadPackage ou de um arquivo XML no formato incorreto.|  
|0xC0011006|-1073672186|DTS_E_UNABLETODECODEBINARYFORMAT|Não é possível decodificar um formato binário no pacote.|  
|0xC0011007|-1073672185|DTS_E_FUNDAMENTALLOADINGERROR|Não é possível carregar o pacote como XML porque ele não tem formato XML válido. Será exibido um erro de analisador XML.|  
|0xC0011008|-1073672184|DTS_E_LOADFROMXML|Erro ao carregar do XML. Não é possível especificar nenhuma informação de erro mais detalhada para esse problema porque não foi passado nenhum objeto Eventos em que possam ser armazenadas informações detalhadas de erro.|  
|0xC0011009|-1073672183|DTS_E_XMLDOMERROR|Não é possível criar uma instância do Modelo de Objeto de Documento XML. O MSXML pode não ser registrado.|  
|0xC001100D|-1073672179|DTS_E_CANNOTLOADOLDPACKAGES|O pacote não pode ser carregado. Isso corre quando se tenta carregar um pacote de versão antiga, ou o arquivo do pacote refere-se a um objeto estruturado inválido.|  
|0xC001100E|-1073672178|DTS_E_SAVEFILE|Falha ao salvar o arquivo do pacote.|  
|0xC001100F|-1073672177|DTS_E_SAVEPACKAGEFILE|Falha ao salvar o arquivo de pacote "%1" com erro 0x%2!8.8X! "%3".|  
|0xC001200D|-1073668083|DTS_E_IDTSNAMENOTSUPPORTED|O objeto deve herdar de IDTSName100 e não herda.|  
|0xC0012018|-1073668072|DTS_E_CONFIGFORMATINVALID_PACKAGEDELIMITER|A entrada de configuração, "%1", tem um formato incorreto porque não começa com o delimitador de pacote. Não havia nenhum delimitador "\package".|  
|0xC0012019|-1073668071|DTS_E_CONFIGFORMATINVALID|A entrada de configuração "%1" tinha um formato incorreto. Isso pode ocorrer por falta de delimitador ou erros de formatação, como um delimitador inválido de matriz.|  
|0xC001201B|-1073668069|DTS_E_CONFIGFILEFAILEDEXPORT|Falha ao exportar o arquivo de configuração.|  
|0xC0012021|-1073668063|DTS_E_PROPERTIESCOLLECTIONREADONLY|A coleção Properties não pode ser modificada.|  
|0xC0012022|-1073668062|DTS_E_DTRXMLSAVEFAILURE|Não é possível salvar o arquivo de configuração. O arquivo pode ser somente leitura.|  
|0xC0012023|-1073668061|DTS_E_FAILPACKAGEONFAILURENA|A propriedade FailPackageOnFailure não é aplicável ao contêiner de pacote.|  
|0xC0012024|-1073668060|DTS_E_TASKPRODUCTLEVEL|A tarefa "%1" não pode ser executada em %2 instalado de Integration Services. É necessário %3 ou superior.|  
|0xC0012029|-1073668055|DTS_E_UNABLETOSAVETOFILE|Não é possível salvar xml em "%1". O arquivo pode ser somente leitura.|  
|0xC0012037|-1073668041|DTS_E_CONFIGTYPECONVERSIONFAILED|Falha ao converter um tipo na configuração "%1" para o caminho de pacote "%2".  Isso ocorre quando um valor de configuração não pode ser convertido de uma cadeia de caracteres em um tipo de destino apropriado. Verifique o valor de configuração para assegurar que possa ser convertido no tipo de propriedade ou variável de destino.|  
|0xC0012049|-1073668023|DTS_E_CONFIGFAILED|Falha de configuração. Este é um aviso genérico para todos os tipos de configuração. Outros avisos devem precedê-lo, com mais informações.|  
|0xC0012050|-1073668016|DTS_E_REMOTEPACKAGEVALIDATION|Falha de validação de pacote na tarefa ExecutePackage. O pacote não pode ser executado.|  
|0xC0013001|-1073663999|DTS_E_FAILTOCREATEMUTEX|Falha ao criar mutex "%1" com o erro 0x%2!8.8X!.|  
|0xC0013002|-1073663998|DTS_E_MUTEXOWNBYDIFFUSER|O mutex "%1" já existe e pertence a outro usuário.|  
|0xC0013003|-1073663997|DTS_E_WAITFORMUTEXFAILED|Falha ao adquirir mutex "%1" com o erro 0x%2!8.8X!.|  
|0xC0013004|-1073663996|DTS_E_FAILTORELEASEMUTEX|Falha ao liberar mutex "%1" com o erro 0x%2!8.8X!.|  
|0xC0014003|-1073659901|DTS_E_INVALIDTASKPOINTER|O ponteiro de tarefa dos wrappers é inválido. O wrapper possui um ponteiro inválido para uma tarefa.|  
|0xC0014004|-1073659900|DTS_E_ALREADYADDED|O executável foi adicionado à coleção Executáveis de outro contêiner. Isso ocorre quando um cliente tenta adicionar um executável a mais de uma coleção de Executáveis. É necessário remover o executável da coleção de Executáveis atual antes de tentar adicioná-lo.|  
|0xC0014005|-1073659899|DTS_E_UNKNOWNCONNECTIONMANAGERTYPE|O tipo de conexão "%1" especificado para o gerenciador de conexões "%2" não é reconhecido como um tipo de gerenciador válido. Esse erro é retornado quando se tenta criar um gerenciador de conexões para um tipo de conexão desconhecido. Verifique a ortografia no nome do tipo de conexão.|  
|0xC0014006|-1073659898|DTS_E_COLLECTIONCOULDNTADD|Um objeto foi criado, mas houve falha na tentativa de adicioná-lo a uma coleção. Isso pode ocorrer por falta de memória.|  
|0xC0014007|-1073659897|DTS_E_ODBCERRORENV|Ocorreu um erro ao criar um ambiente ODBC (Open Database Connectivity).|  
|0xC0014008|-1073659896|DTS_E_ODBCERRORDBC|Ocorreu um erro ao criar uma conexão de banco de dados ODBC.|  
|0xC0014009|-1073659895|DTS_E_ODBCERRORCONNECT|Ocorre um erro ao tentar estabelecer uma conexão ODBC com o servidor de banco de dados.|  
|0xC001400A|-1073659894|DTS_E_CONNECTIONMANAGERQUALIFIERALREADYSET|O qualificador já está definido nessa instância do gerenciador de conexões. O qualificador pode ser definido uma vez por instância.|  
|0xC001400B|-1073659893|DTS_E_CONNECTIONMANAGERQUALIFIERNOTSET|O qualificador não foi definido nessa instância do gerenciador de conexões. Para concluir a inicialização, é necessário definir o qualificador.|  
|0xC001400C|-1073659892|DTS_E_CONNECTIONMANAGERQUALIFIERNOTSUPPORTED|Este gerenciador de conexões não oferece suporte a especificação de qualificadores.|  
|0xC001400D|-1073659891|DTS_E_CANNOTCLONECONNECTIONMANAGER|Não é possível clonar o gerenciador de conexões "0x%1" para execução fora do processo.|  
|0xC001400E|-1073659890|DTS_E_NOSQLPROFILERDLL|O provedor de log para SQL Server Profiler não conseguiu carregar o pfclnt.dll. Verifique se o SQL Server Profiler foi instalado.|  
|0xC001400F|-1073659889|DTS_E_LOGFAILED|Falha na infraestrutura de log SSIS com o código de erro 0x%1!8.8X!. Este erro indica que o erro de log não se atribui a um provedor de log específico.|  
|0xC0014010|-1073659888|DTS_E_LOGPROVIDERFAILED|Falha no provedor de log SSIS com o código de erro 0x%2!8.8X! (%3).  Isso indica um erro de log que pode ser atribuído ao provedor de log especificado.|  
|0xC0014011|-1073659887|DTS_E_SAVETOSQLSERVER_OLEDB|O método SaveToSQLServer encontrou o código de erro OLE DB 0x%1!8.8X! (%2).  Houve falha na instrução SQL emitida.|  
|0xC0014012|-1073659886|DTS_E_LOADFROMSQLSERVER_OLEDB|O método LoadFromSQLServer encontrou o código de erro OLE DB 0x%1!8.8X! (%2).  Houve falha na instrução SQL emitida.|  
|0xC0014013|-1073659885|DTS_E_REMOVEFROMSQLSERVER_OLEDB|O método RemoveFromSQLServer encontrou o código de erro OLE DB 0x%1!8.8X! (%2) Falha na instrução SQL emitida.|  
|0xC0014014|-1073659884|DTS_E_EXISTSONSQLSERVER_OLEDB|O método ExistsOnSQLServer encontrou o código de erro OLE DB 0x%1!8.8X! (%2). Houve falha na instrução SQL emitida.|  
|0xC0014015|-1073659883|DTS_E_CONNECTIONSTRING|O OLE DB falhou ao realizar uma conexão de banco de dados, usando a cadeia de caracteres de conexão fornecida.|  
|0xC0014016|-1073659882|DTS_E_FROMEXECISNOTCHILD|Ao adicionar uma restrição de precedência, o executável From foi especificado não como filho deste contêiner.|  
|0xC0014017|-1073659881|DTS_E_TOEXECISNOTCHILD|Ao adicionar uma restrição de precedência, o executável To foi especificado não como filho deste contêiner.|  
|0xC0014018|-1073659880|DTS_E_ODBCTRANSACTIONENLIST|Houve erro ao tentar inscrever uma conexão ODBC em uma transação. O SQLSetConnectAttr não definiu o atributo SQL_ATTR_ENLIST_IN_DTC.|  
|0xC0014019|-1073659879|DTS_E_CONNECTIONOFFLINE|O gerenciador de conexões "%1" não adquirirá uma conexão porque a propriedade OfflineMode do pacote foi definida como TRUE. Quando a propriedade OfflineMode está definida como TRUE, não é possível adquirir conexões.|  
|0xC001401A|-1073659878|DTS_E_BEGINTRANSACTION|O Tempo de Execução de SSIS não pode iniciar a transação distribuída devido ao erro 0x%1!8.8X! "%2". A transação de DTC não iniciou. Isso pode ocorrer porque o Serviço MSDTC não está em execução.|  
|0xC001401B|-1073659877|DTS_E_SETQUALIFIERDESIGNTIMEONLY|O método SetQualifier não pode ser chamado em um gerenciador de conexões durante a execução do pacote. Esse método é usado somente no tempo de design.|  
|0xC001401C|-1073659876|DTS_E_SQLPERSISTENCEVERSION|Para armazenar ou modificar pacotes no SQL Server é necessário que o tempo de execução e o banco de dados SSIS sejam da mesma versão. Não há suporte para o armazenamento de pacotes nas versões anteriores.|  
|0xC001401D|-1073659875|DTS_E_CONNECTIONVALIDATIONFAILED|Falha de validação na conexão "%1".|  
|0xC001401E|-1073659874|DTS_E_INVALIDFILENAMEINCONNECTION|O nome de arquivo "%1" especificado na conexão não era válido.|  
|0xC001401F|-1073659873|DTS_E_MULTIPLEFILESONRETAINEDCONNECTION|Quando a propriedade Retain está definida como TRUE, não é possível especificar nomes de vários arquivos em uma conexão. Foram encontradas barras verticais na cadeia de caracteres de conexão, indicando que vários nomes de arquivo estão sendo especificados e, além disso, a propriedade Retain está definida como TRUE.|  
|0xC0014020|-1073659872|DTS_E_ODBCERROR|Erro de ODBC %1!d! ocorreu.|  
|0xC0014021|-1073659871|DTS_E_PRECEDENCECONSTRAINT|Erro na restrição de precedência entre "%1" e "%2".|  
|0xC0014022|-1073659870|DTS_E_FAILEDPOPNATIVEFEE|A coleção ForEachEnumeratorInfos não foi preenchida com ForEachEnumerators nativo e gerou o seguinte código de erro: %1.|  
|0xC0014023|-1073659869|DTS_E_GETENUMERATOR|Falha do método GetEnumerator do Enumerador ForEach com o erro 0x%1!8.8X! "%2". Isso ocorre quando o Enumerador ForEach não consegue enumerar.|  
|0xC0014024|-1073659868|DTS_E_CANTGETCERTDATA|Os dados brutos de certificado não podem ser obtidos do objeto de certificado fornecido (erro: %1). Isso ocorre quando CPackage::put_CertificateObject não consegue criar uma instância do objeto ManagedHelper, quando o objeto ManagedHelper falha, ou quando o objeto ManagedHelper retorna uma matriz malformada.|  
|0xC0014025|-1073659867|DTS_E_CANTCREATECERTCONTEXT|Falha ao criar um contexto de certificado (erro: %1). Isso ocorre em CPackage::put_CertificateObject ou CPackage::LoadFromXML quando a função CryptoAPI correspondente falha.|  
|0xC0014026|-1073659866|DTS_E_CANTOPENCERTSTORE|Falha ao abrir MEU repositório de certificados, com o erro "%1". Isso ocorre em CPackage::LoadUserCertificateByName e CPackage::LoadUserCertificateByHash.|  
|0xC0014027|-1073659865|DTS_E_CANTFINDCERTBYNAME|O certificado especificado pelo nome em MEU repositório não pode ser encontrado (erro: %1). Isso ocorre em CPackage::LoadUserCertificateByName.|  
|0xC0014028|-1073659864|DTS_E_CANTFINDCERTBYHASH|Não é possível encontrar o certificado especificado por hash em "MEU" repositório (erro: %1). Isso ocorre em CPackage::LoadUserCertificateByHash.|  
|0xC0014029|-1073659863|DTS_E_INVALIDCERTHASHFORMAT|O valor de hash não é uma matriz unidimensional de bytes (erro: %1). Isso ocorre em CPackage::LoadUserCertificateByHash.|  
|0xC001402A|-1073659862|DTS_E_CANTACCESSARRAYDATA|Os dados da matriz não podem ser acessados (erro: %1). Esse erro pode ocorrer sempre que GetDataFromSafeArray for chamado.|  
|0xC001402B|-1073659861|DTS_E_CREATEMANAGEDHELPERFAILED|Falha do objeto auxiliar gerenciado SSIS durante a criação com o erro 0x%1!8.8X! "%2". Isso ocorre sempre que há falha em CoCreateInstance CLSID_DTSManagedHelper.|  
|0xC001402C|-1073659860|DTS_E_OLEDBTRANSACTIONENLIST|Falha do Tempo de Execução SSIS em inscrever a conexão OLE DB em uma transação distribuída com o erro 0x%1!8.8X! "%2".|  
|0xC001402D|-1073659859|DTS_E_SIGNPACKAGEFAILED|Falha na assinatura do pacote com o erro 0x%1!8.8X! "%2". Isso ocorre quando o método ManagedHelper.SignDocument falha.|  
|0xC001402E|-1073659858|DTS_E_CHECKENVELOPEFAILED|Falha ao procurar o envelope de assinatura XML no pacote XML com o erro 0x%1!8.8X! "%2". Isso ocorre em CPackage::LoadFromXML.|  
|0xC001402F|-1073659857|DTS_E_GETXMLSOURCEFAILED|Falha ao obter fonte XML do objeto XML DOM com o erro 0x%1!8.8X! "%2". Isso ocorre quando há falha em IXMLDOMDocument::get_xml.|  
|0xC0014030|-1073659856|DTS_E_PACKAGEVERIFICATIONFAILED|Falha na verificação da assinatura criptográfica do pacote devido ao erro 0x%1!8.8X! "%2". Isso ocorre quando a operação de verificação de assinatura falha.|  
|0xC0014031|-1073659855|DTS_E_GETKEYFROMCERTFAILED|Falha ao obter o par de chaves criptográficas associado ao certificado especificado com o erro 0x%1!8.8X! "%2". Verifique se você tem o par de chaves para o qual o certificado foi emitido. Em geral, esse erro ocorre durante uma tentativa de assinar um documento com um certificado para o qual a pessoa não tem a chave privada.|  
|0xC0014032|-1073659854|DTS_E_INVALIDSIGNATURE|A assinatura digital não é válida. O conteúdo do pacote foi modificado.|  
|0xC0014033|-1073659853|DTS_E_UNTRUSTEDSIGNATURE|A assinatura digital é válida; porém o signatário não é de confiança e, portanto, a autenticidade não pode ser garantida.|  
|0xC0014034|-1073659852|DTS_E_TRANSACTIONENLISTNOTSUPPORTED|A conexão não oferece suporte à inscrição em transação distribuída.|  
|0xC0014035|-1073659851|DTS_E_PACKAGEPROTECT|Falha ao aplicar proteção de pacote com o erro 0x%1!8.8X! "%2". Esse erro ocorre quando se salva em Xml.|  
|0xC0014036|-1073659850|DTS_E_PACKAGEUNPROTECT|Falha ao remover a proteção de pacote com o erro 0x%1!8.8X! "%2". Isso ocorre no método CPackage::LoadFromXML.|  
|0xC0014037|-1073659849|DTS_E_PACKAGEPASSWORD|O pacote é criptografado com uma senha. A senha não foi especificada ou não está correta.|  
|0xC0014038|-1073659848|DTS_E_DUPLICATECONSTRAINT|Uma restrição de precedência já existe entre os executáveis especificados. Mais de uma restrição de precedência não é permitida.|  
|0xC0014039|-1073659847|DTS_E_PACKAGELOADFAILED|Falha no carregamento do pacote devido ao erro 0x%1!8.8X! "%2". Isso ocorre quando CPackage::LoadFromXML falha.|  
|0xC001403A|-1073659846|DTS_E_PACKAGEOBJECTNOTENVELOPED|Falha ao localizar o objeto de pacote no envelope XML assinado com o erro 0x%1!8.8X! "%2". Isso ocorre quando o XML assinado não contém um pacote SSIS, como esperado.|  
|0xC001403B|-1073659845|DTS_E_JAGGEDEVENTINFO|Os comprimentos de nomes de parâmetro, tipos e matrizes de descrições não são iguais. Os comprimentos devem ser iguais. Isso ocorre quando os comprimentos das matrizes são diferentes. Deve haver uma entrada por parâmetro em cada matriz.|  
|0xC001403C|-1073659844|DTS_E_GETPACKAGEINFOS|Erro de OLE DB 0x%1!8.8X! (%2) ocorrido ao enumerar os pacotes. Uma instrução SQL foi emitida e falhou.|  
|0xC001403D|-1073659843|DTS_E_UNKNOWNLOGPROVIDERTYPE|O tipo de provedor de log "%1" especificado para o provedor de log "%2" não é reconhecido como tipo de provedor de log válido. Esse erro ocorre quando se tenta criar um provedor de log para um tipo de provedor de log desconhecido. Verifique a ortografia do nome do tipo de provedor de log.|  
|0xC001403E|-1073659842|DTS_E_UNKNOWNLOGPROVIDERTYPENOSUBS|O tipo de provedor de log não é reconhecido como tipo de provedor de log válido. Esse erro ocorre quando se tenta criar um provedor de log para um tipo de provedor de log desconhecido. Verifique a ortografia do nome do tipo de provedor de log.|  
|0xC001403F|-1073659841|DTS_E_UNKNOWNCONNECTIONMANAGERTYPENOSUBS|O tipo de conexão especificado para o gerenciador de conexões não é um tipo de gerenciador válido. Esse erro ocorre quando se tenta criar um gerenciador de conexões para um tipo de conexão desconhecido. Verifique a ortografia do nome do tipo de conexão.|  
|0xC0014040|-1073659840|DTS_E_PACKAGEREMOVEFAILED|Erro ao tentar remover o pacote "%1" do SQL Server.|  
|0xC0014042|-1073659838|DTS_E_FOLDERADDFAILED|Erro ao tentar criar uma pasta no SQL Server de nome "%1" na pasta "%2".|  
|0xC0014043|-1073659837|DTS_E_CREATEFOLDERONSQLSERVER_OLEDB|O método CreateFolderOnSQLServer encontrou o código de erro no OLE DB 0x%1!8.8X! (%2) Falha na instrução SQL emitida.|  
|0xC0014044|-1073659836|DTS_E_FOLDERRENAMEFAILED|Erro ao renomear a pasta " %1\\\\%2" para "%1\\\\%3" no SQL Server.|  
|0xC0014045|-1073659835|DTS_E_RENAMEFOLDERONSQLSERVER_OLEDB|O método RenameFolderOnSQLServer encontrou o código de erro OLE DB 0x%1!8.8X! (%2). Houve falha na instrução SQL emitida.|  
|0xC0014046|-1073659834|DTS_E_FOLDERDELETEFAILED|Erro ao excluir a pasta "%1" do SQL Server.|  
|0xC0014047|-1073659833|DTS_E_REMOVEFOLDERFROMSQLSERVER_OLEDB|O método RemoveFolderOnSQLServer encontrou o código de erro OLE DB 0x%1!8.8X! (%2). Houve falha na instrução SQL emitida.|  
|0xC0014048|-1073659832|DTS_E_INVALIDPATHTOPACKAGE|O caminho de pacote especificado não contém um nome de pacote. Isso ocorre quando o caminho não contém pelo menos uma barra ou uma barra invertida.|  
|0xC0014049|-1073659831|DTS_E_FOLDERNOTFOUND|Não é possível encontrar a pasta "%1".|  
|0xC001404A|-1073659830|DTS_E_FINDFOLDERONSQLSERVER_OLEDB|Durante uma tentativa de encontrar uma pasta no SQL, um erro OLE DB foi encontrado com o código de erro 0x%1!8.8X! (%2).|  
|0xC001404B|-1073659829|DTS_E_OPENLOGFAILED|O provedor de log SSIS não conseguiu abrir o log. Código de erro: 0x%1!8.8X!.|  
|0xC001404C|-1073659828|DTS_E_GETCONNECTIONINFOS|Falha ao obter coleção ConnectionInfos com o erro 0x%1!8.8X! "%2". Esse erro ocorre quando a chamada ao IDTSApplication100::get_ConnectionInfos falha.|  
|0xC001404D|-1073659827|DTS_E_VARIABLEDEADLOCK|Deadlock detectado ao tentar bloquear variáveis. Os bloqueios não podem ser adquiridos depois de 16 tentativas. Os bloqueios expiraram.|  
|0xC001404E|-1073659826|DTS_E_NOTDISPENSED|A coleção Variables não foi retornada de VariableDispenser. Foi tentada uma operação permitida somente em coleções dispensadas.|  
|0xC001404F|-1073659825|DTS_E_VARIABLESALREADYUNLOCKED|Essa coleção Variables já foi desbloqueada. O método Unlock é chamado só uma vez em uma coleção Variables dispensada.|  
|0xC0014050|-1073659824|DTS_E_VARIABLEUNLOCKFAILED|Uma ou mais variáveis não foram desbloqueadas.|  
|0xC0014051|-1073659823|DTS_E_DISPENSEDREADONLY|A coleção Variables foi retornada de VariableDispenser e não pode ser modificada. Não é possível adicionar itens a coleções dispensadas ou delas remover.|  
|0xC0014052|-1073659822|DTS_E_VARIABLEALREADYONREADLIST|A variável "%1" já está na lista de leitura. Uma variável pode ser adicionada somente uma vez à lista de bloqueio de leitura ou de gravação.|  
|0xC0014053|-1073659821|DTS_E_VARIABLEALREADYONWRITELIST|A variável "%1" já está na lista de gravação. Uma variável pode ser adicionada somente uma vez à lista de bloqueio de leitura ou de gravação.|  
|0xC0014054|-1073659820|DTS_E_LOCKVARIABLEFORREAD|Falha ao bloquear a variável "%1" para acesso de leitura com o erro 0x%2!8.8X! "%3".|  
|0xC0014055|-1073659819|DTS_E_LOCKVARIABLEFORWRITE|Falha ao bloquear a variável "%1" para acesso de leitura/gravação com o erro 0x%2!8.8X! "%3".|  
|0xC0014056|-1073659818|DTS_E_CUSTOMEVENTCONFLICT|O evento personalizado "%1" já foi declarado com uma lista de parâmetro diferente. Uma tarefa está tentando declarar um evento personalizado que outra tarefa já declarou com uma lista de parâmetro diferente.|  
|0xC0014057|-1073659817|DTS_E_EVENTHANDLERNOTALLOWED|A tarefa que fornece o evento personalizado "%1" não permite o tratamento desse evento no pacote. O evento personalizado foi declarado com AllowEventHandlers = FALSE.|  
|0xC0014059|-1073659815|DTS_E_UNSAFEVARIABLESALREADYSET|O VariableDispenser recebeu uma coleção Variables insegura. Esta operação não pode ser repetida.|  
|0xC001405A|-1073659814|DTS_E_INVALIDPARENTPACKAGEPATH|GetPackagePath foi chamado no ForEachEnumerator, mas não havia nenhum caminho de pacote ForEachLoop especificado.|  
|0xC001405B|-1073659813|DTS_E_VARIABLEDEADLOCK_READ|Um deadlock foi detectado ao tentar bloquear a variável "%1" para acesso de leitura. Um bloqueio não pode ser adquirido depois de 16 tentativas e depois de expirado.|  
|0xC001405C|-1073659812|DTS_E_VARIABLEDEADLOCK_READWRITE|Um deadlock foi detectado ao tentar bloquear as variáveis "%1" para acesso de leitura/gravação. O bloqueio não pode ser adquirido depois de 16 tentativas. Os bloqueios expiraram.|  
|0xC001405D|-1073659811|DTS_E_VARIABLEDEADLOCK_BOTH|Um deadlock foi detectado ao tentar bloquear as variáveis "%1" para acesso de leitura e as variáveis "%2" para acesso de leitura/gravação. O bloqueio não pode ser adquirido depois de 16 tentativas. Os bloqueios expiraram.|  
|0xC001405E|-1073659810|DTS_E_PACKAGEPASSWORDEMPTY|O nível de proteção do pacote exige uma senha, mas a propriedade PackagePassword está em branco.|  
|0xC001405F|-1073659809|DTS_E_DECRYPTXML_PASSWORD|Falha ao decifrar um nó XML criptografado porque a senha não foi especificada ou não estava correta. A tentativa de carregar o pacote continuará sem a informação criptografada.|  
|0xC0014060|-1073659808|DTS_E_DECRYPTPACKAGE_USERKEY|Falha ao decifrar um pacote criptografado com uma chave de usuário. Talvez você não seja o usuário que criptografou este pacote ou não esteja usando a mesma máquina usada para salvar o pacote.|  
|0xC0014061|-1073659807|DTS_E_SERVERSTORAGEDISALLOWED|O nível de proteção, ServerStorage, não pode ser usado ao salvar neste destino. O sistema não conseguiu verificar se o destino oferece suporte à capacidade de armazenamento seguro.|  
|0xC0014062|-1073659806|DTS_E_LOADFROMSQLSERVER|O método LoadFromSQLServer falhou.|  
|0xC0014063|-1073659805|DTS_E_SIGNATUREPOLICYVIOLATION|O pacote não pode ser carregado porque o estado da assinatura digital viola a política de assinatura. Erro 0x%1!8.8X! "%2"|  
|0xC0014064|-1073659804|DTS_E_SIGNATURENOTPRESENT|O pacote não está assinado.|  
|0xC0014065|-1073659803|DTS_E_SQLPROFILERDLL_ONLY_X86|O provedor de log para SQL Server Profiler não pôde carregar pfclnt.dll porque só somente os sistemas de 32 bits oferecem suporte a ele.|  
|0xC0014100|-1073659648|DTS_E_NAMEALREADYADDED|O objeto não pode ser adicionado porque já existe outro com o mesmo nome na coleção. Use um nome diferente para resolver este erro.|  
|0xC0014101|-1073659647|DTS_E_NAMEALREADYEXISTS|O nome de objeto não pode ser alterado de "%1" para "%2" porque já existe outro objeto com o mesmo nome na coleção. Use um nome diferente para resolver este erro.|  
|0xC0014103|-1073659645|DTS_E_FAILEDDEPENDENCIES|Houve um erro ao enumerar as dependências de pacote. Verifique outras mensagens para obter mais informações.|  
|0xC0014104|-1073659644|DTS_E_INVALIDCHECKPOINT_TRANSACTION|Não há suporte para as configurações de pacote atuais.  Altere a propriedade SaveCheckpoints ou a propriedade TransactionOption.|  
|0xC001410E|-1073659634|DTS_E_CONNECTIONMANAGERJOINTRANSACTION|O gerenciador de conexões não conseguiu se retirar da transação.|  
|0xC0015001|-1073655807|DTS_E_BPDUPLICATE|A ID de ponto de interrupção especificada já existe. Esse erro ocorre quando uma tarefa chama CreateBreakpoint com a mesma ID várias vezes. É possível criar um ponto de interrupção com a mesma ID várias vezes se a tarefa chamar RemoveBreakpoint na primeira criação antes de criar o segundo ponto.|  
|0xC0015002|-1073655806|DTS_E_BPUNKNOWNID|A ID de ponto de interrupção especificada não existe. Esse erro ocorre quando uma tarefa referencia um ponto de interrupção inexistente.|  
|0xC0015004|-1073655804|DTS_E_CANTWRITETOFILE|O arquivo, "%1", não pôde ser aberto para gravação. O arquivo pode ser somente leitura ou você não tem as permissões corretas.|  
|0xC0015005|-1073655803|DTS_E_NOROWSETRETURNED|Nenhum conjunto de linhas de resultado está associado à execução dessa consulta. O resultado não está especificado corretamente.|  
|0xC0015105|-1073655547|DTS_E_DUMP_FAILED|Não foram gerados arquivos de despejo de depuração corretamente. O hresult é 0x%1!8.8X!.|  
|0xC0016001|-1073651711|DTS_E_INVALIDURL|A URL especificada não é válida. Isso pode ocorrer quando a URL do servidor ou do proxy é nula, ou está em formato incorreto. Um formato de URL válido está na forma de https://ServerName:Port/ResourcePath ou https://ServerName:Port/ResourcePath.|  
|0xC0016002|-1073651710|DTS_E_INVALIDSCHEME|A URL %1 não é válida. Isso pode ocorrer quando se especifica um esquema diferente de http ou https, ou quando a URL está em um formato incorreto. Um formato de URL válido está na forma de https://ServerName:Port/ResourcePath ou https://ServerName:Port/ResourcePath.|  
|0xC0016003|-1073651709|DTS_E_WINHTTPCANNOTCONNECT|Não é possível estabelecer conexão com o servidor %1. Esse erro pode ocorrer quando o servidor não existe, ou as configurações do proxy estão incorretas.|  
|0xC0016004|-1073651708|DTS_E_CONNECTIONTERMINATED|A conexão com o servidor foi redefinida ou terminada. Tente novamente depois.|  
|0xC0016005|-1073651707|DTS_E_LOGINFAILURE|Falha na tentativa de logon para "%1". Esse erro ocorre quando as credenciais de logon fornecidas estão incorretas. Verifique as credenciais de logon.|  
|0xC0016006|-1073651706|DTS_E_INVALIDSERVERNAME|O nome do servidor especificado na URL %1 não pode ser resolvido.|  
|0xC0016007|-1073651705|DTS_E_PROXYAUTH|Falha na autenticação do proxy. Esse erro ocorre quando não são fornecidas credenciais de logon, ou as credenciais estão incorretas.|  
|0xC0016008|-1073651704|DTS_E_SECUREFAILURE|A resposta do certificado SSL obtida do servidor não era válida. Não é possível processar a solicitação.|  
|0xC0016009|-1073651703|DTS_E_TIMEOUT|O tempo limite da solicitação foi atingido. Esse erro pode ocorrer quando o tempo limite especificado é muito curto ou não é possível estabelecer uma conexão com o servidor ou proxy. Verifique se a URL do servidor e a do proxy estão corretas.|  
|0xC001600A|-1073651702|DTS_E_CLIENTAUTH|Falta certificado de cliente. Esse erro ocorre quando o servidor espera um certificado de cliente SSL e o usuário fornece um certificado inválido, ou não fornece nenhum certificado. Configure um certificado de cliente para essa conexão.|  
|0xC001600B|-1073651701|DTS_E_REDIRECTFAILURE|O servidor especificado, URL %1, tem um redirecionamento e a solicitação de redirecionamento falhou.|  
|0xC001600C|-1073651700|DTS_E_SERVERAUTH|Falha na autenticação do servidor. Esse erro ocorre quando não são fornecidas credenciais de logon, ou as credenciais estão incorretas.|  
|0xC001600D|-1073651699|DTS_E_WINHTTPUNKNOWNERROR|A solicitação não pode ser processada. Tente novamente depois.|  
|0xC001600E|-1073651698|DTS_E_UNKNOWNSTATUSCODE|O servidor retornou o código de status - %1!u! : %2. Esse erro ocorre quando o servidor está com problemas.|  
|0xC001600F|-1073651697|DTS_E_WINHTTPNOTSUPPORTED|Os serviços WinHttp não dão suporte a essa plataforma.|  
|0xC0016010|-1073651696|DTS_E_INVALIDTIMEOUT|Valor de tempo limite não é válido. O tempo limite deve ficar no intervalo de %1!d! para a %2!d! (em segundos).|  
|0xC0016011|-1073651695|DTS_E_INVALIDCHUNKSIZE|O tamanho da parte não é válido. A propriedade ChunkSize deve ficar no intervalo de %1!d! para a %2!d! (em KB).|  
|0xC0016012|-1073651694|DTS_E_CERTERROR|Erro ao processar o certificado de cliente. Esse erro pode ocorrer quando o certificado de cliente fornecido não foi encontrado no Repositório de Certificados Pessoais. Verifique se o certificado de cliente é válido.|  
|0xC0016013|-1073651693|DTS_E_FORBIDDEN|O servidor retornou o código de erro "403 – Proibido". Esse erro pode ocorrer quando o recurso especificado precisa de acesso "https", mas o período de validade do certificado expirou, o certificado não é válido para o uso solicitado, ou o certificado foi revogado ou a revogação não pode ser verificada.|  
|0xC0016014|-1073651692|DTS_E_WINHTTPOPEN|Erro ao inicializar a sessão HTTP com o proxy "%1". Esse erro pode ocorrer quando um proxy inválido foi especificado. O gerenciador de conexões HTTP dá suporte somente a proxies do tipo CERN.|  
|0xC0016015|-1073651691|DTS_E_OPENCERTSTORE|Erro ao abrir o repositório de certificados.|  
|0xC0016016|-1073651690|DTS_E_UNPROTECTXMLFAILED|Falha ao descriptografar o nó XML protegido "%1" com o erro 0x%2!8.8X! "%3". Você pode não estar autorizado a acessar essas informações. Esse erro ocorre quando existe um erro criptográfico. Verifique se a chave correta está disponível.|  
|0xC0016017|-1073651689|DTS_E_UNPROTECTCONNECTIONSTRINGFAILED|Falha ao descriptografar a cadeia de conexão protegida para o servidor "%1" com o erro 0x%2!8.8X! "%3". Você pode não estar autorizado a acessar essas informações. Esse erro ocorre quando existe um erro criptográfico. Verifique se a chave correta está disponível.|  
|0xC0016018|-1073651688|DTS_E_NEGATIVEVERSION|O número de versão não pode ser negativo. Esse erro ocorre quando a propriedade VersionMajor, VersionMinor ou VersionBuild do pacote está definido como valor negativo.|  
|0xC0016019|-1073651687|DTS_E_PACKAGEMIGRATED|O pacote foi migrado para uma versão posterior ao ser carregado. Ele deve ser recarregado para completar o processo. Esse é um código de erro interno.|  
|0xC0016020|-1073651680|DTS_E_PACKAGEMIGRATIONFAILED|Migração de pacote da versão %1!d! para versão %2!d! falhou com erro 0x%3!8.8X! "%4".|  
|0xC0016021|-1073651679|DTS_E_PACKAGEMIGRATIONMODULELOAD|Falha ao carregar o módulo de migração de pacote.|  
|0xC0016022|-1073651678|DTS_E_PACKAGEMIGRATIONMODULE|Falha no módulo de migração de pacote.|  
|0xC0016023|-1073651677|DTS_E_CANTDETERMINEWHICHPROPTOPERSIST|Não é possível manter o objeto usando a persistência padrão. Esse erro ocorre quando a persistência padrão não consegue determinar quais objetos estão no objeto hospedado.|  
|0xC0016024|-1073651676|DTS_E_CANTADDREMOVEWHENEXECUTING|Um elemento não pode ser adicionado ou removido de um pacote no modo de tempo de execução. Esse erro ocorre quando se tenta adicionar ou remover um objeto de uma coleção enquanto o pacote está em execução.|  
|0xC0016025|-1073651675|DTS_E_NODENOTFOUND|O nó "%1" não pode ser encontrado na persistência padrão personalizada. Esse erro ocorre se o XML padrão salvo de um objeto extensível for alterado de forma que o objeto salvo não pode mais ser encontrado, ou se o próprio objeto extensível for alterado.|  
|0xC0016026|-1073651674|DTS_E_COLLECTIONLOCKED|Essa coleção não pode ser modificada durante a validação ou execução do pacote.|  
|0xC0016027|-1073651673|DTS_E_COLLOCKED|A coleção "%1" não pode ser modificada durante a validação ou execução do pacote. "%2" não pode ser adicionado à coleção.|  
|0xC0016029|-1073651671|DTS_E_FTPNOTCONNECTED|A conexão com o servidor FTP não foi estabelecida.|  
|0xC001602A|-1073651670|DTS_E_FTPERROR|Ocorreu um erro na operação FTP solicitada. Descrição detalhada do erro: %1.|  
|0xC001602B|-1073651669|DTS_E_FTPINVALIDRETRIES|O número de tentativas não é válido. O número de tentativas deve ficar entre %1!d! e %2!d!.|  
|0xC001602C|-1073651668|DTS_E_LOADWININET|O gerenciador de conexões FTP precisa da seguinte DLL para funcionar: %1.|  
|0xC001602D|-1073651667|DTS_E_FTPINVALIDCONNECTIONSTRING|A porta especificada na cadeia de caracteres de conexão não é válida. O formato de ConnectionString é ServerName:Port. A porta deve ser um valor inteiro entre %1!d! e %2!d!.|  
|0xC001602E|-1073651666|DTS_E_FTPCREATEFOLDER|Criando a pasta "%1" ... %2.|  
|0xC001602F|-1073651665|DTS_E_FTPDELETEFOLDER|Excluindo a pasta "%1"... %2.|  
|0xC0016030|-1073651664|DTS_E_FTPCHANGEFOLDER|Alterando o diretório atual para "%1". %2.|  
|0xC0016031|-1073651663|DTS_E_FTPFILESEMPTY|Nenhum arquivo para ser transferido. Esse erro pode ocorrer ao executar uma operação de envio ou recebimento e nenhum arquivo foi especificado para transferência.|  
|0xC0016032|-1073651662|DTS_E_FTPINVALIDLOCALPATH|O caminho local especificado não é válido. Especifique um caminho local válido. Isso pode ocorrer quando o caminho local especificado é nulo.|  
|0xC0016033|-1073651661|DTS_E_FTPNOFILESTODELETE|Nenhum arquivo especificado para ser excluído.|  
|0xC0016034|-1073651660|DTS_E_WINHTTPCERTDECODE|Ocorreu um erro interno ao carregar o certificado. Esse erro pode ocorrer quando os dados do certificado são inválidos.|  
|0xC0016035|-1073651659|DTS_E_WINHTTPCERTENCODE|Ocorreu um erro interno ao salvar os dados do certificado.|  
|0xC0016049|-1073651639|DTS_E_CHECKPOINTMISMATCH|O arquivo "%1" de ponto de verificação não corresponde a esse pacote. A ID do pacote e a ID no arquivo de ponto de verificação não coincidem.|  
|0xC001604A|-1073651638|DTS_E_CHECKPOINTFILEALREADYEXISTS|Um arquivo de ponto de verificação existente foi encontrado com conteúdo que não parece ser desse pacote, assim o arquivo não pode ser substituído para começar a salvar novos pontos de verificação. Remova o arquivo de ponto de verificação existente e tente de novo. Esse erro ocorre quando existe um arquivo de ponto de verificação, o pacote está definido para não usar arquivo de ponto de verificação, mas para salvar pontos de verificação. O arquivo de ponto de verificação existente não será substituído.|  
|0xC001604B|-1073651637|DTS_E_CHECKPOINTFILELOCKED|O arquivo de ponto de verificação "%1" está bloqueado por outro processo. Isso pode ocorrer se outra instância desse pacote estiver em execução.|  
|0xC001604C|-1073651636|DTS_E_OPENCHECKPOINTFILE|Falha ao abrir o arquivo de ponto de verificação "%1" devido ao erro 0x%2!8.8X! "%3".|  
|0xC001604D|-1073651635|DTS_E_CREATECHECKPOINTFILE|Falha do arquivo de ponto de verificação "%1" durante a criação devido ao erro 0x%2!8.8X! "%3".|  
|0xC0016050|-1073651632|DTS_E_FTPINVALIDPORT|A porta FTP contém um valor inválido. O valor da porta FTP deve ser um número inteiro entre %1!d! e %2!d!.|  
|0xC00160AA|-1073651542|DTS_E_CONNECTTOSERVERFAILED|Falha na conexão com o SSIS Service na máquina "%1":<br /><br /> %2.|  
|0xC0017002|-1073647614|DTS_E_PROPERTYEXPRESSIONSDISABLEDONVARIABLES|A propriedade Expression não dá suporte a objetos Variable. Em seu lugar, use a propriedade EvaluateAsExpression.|  
|0xC0017003|-1073647613|DTS_E_PROPERTYEXPRESSIONEVAL|A expressão "%1" na propriedade "%2" não pode ser avaliada. Modifique a expressão para ser válida.|  
|0xC0017004|-1073647612|DTS_E_PROPERTYEXPRESSIONSET|O resultado da expressão "%1" na propriedade "%2" não pode ser gravado na propriedade. A expressão foi avaliada, mas não pode ser definida na propriedade.|  
|0xC0017005|-1073647611|DTS_E_FORLOOPEVALEXPRESSIONINVALID|A expressão de avaliação para o loop não é válida. A expressão precisa ser modificada. Deve haver mensagens de erro adicionais.|  
|0xC0017006|-1073647610|DTS_E_EXPRESSIONNOTBOOLEAN|A expressão "%1" dever ser avaliada como True ou False. Altere a expressão a ser avaliada como um valor booliano.|  
|0xC0017007|-1073647609|DTS_E_FORLOOPHASNOEXPRESSION|Não há nenhuma expressão a ser avaliada para o loop. Esse erro ocorre quando a expressão em For Loop está vazia. Adicione uma expressão.|  
|0xC0017008|-1073647608|DTS_E_FORLOOPASSIGNEXPRESSIONINVALID|A expressão de atribuição para o loop não é válida e precisa ser modificada. Deve haver mensagens de erro adicionais.|  
|0xC0017009|-1073647607|DTS_E_FORLOOPINITEXPRESSIONINVALID|A expressão de inicialização para o loop não é válida e precisa ser modificada. Deve haver mensagens de erro adicionais.|  
|0xC001700A|-1073647606|DTS_E_INVALIDVERSIONNUMBER|O número da versão no pacote não é válido. O número da versão não pode ser superior que o número de versão atual.|  
|0xC001700C|-1073647604|DTS_E_INVALIDVERNUMCANTBENEGATIVE|O número da versão no pacote não é válido. O número da versão é negativo.|  
|0xC001700D|-1073647603|DTS_E_PACKAGEUPDATEDISABLED|O pacote tem uma versão de formato mais antigo, mas a atualização automática de formato de pacote está desabilitada.|  
|0xC001700E|-1073647602|DTS_E_EXPREVALTRUNCATIONASERROR|Ocorreu um truncamento durante a avaliação da expressão.|  
|0xC0019001|-1073639423|DTS_E_FAILEDSETEXECVALVARIABLE|O wrapper não conseguiu definir o valor da variável especificada na propriedade ExecutionValueVariable.|  
|0xC0019004|-1073639420|DTS_E_VARIABLEEXPRESSIONERROR|Falha na avaliação da expressão para a variável "%1". Havia um erro na expressão.|  
|0xC0019305|-1073638651|DTS_E_UNSUPPORTEDSQLVERSION|Não há suporte para essa operação com esta versão de banco de dados.|  
|0xC001A003|-1073635325|DTS_E_TXNSPECINVALID|Uma transação não pode ser especificada quando se usa uma conexão retida. Esse erro ocorre quando Retain está definido como TRUE no gerenciador de conexões, mas AcquireConnection foi chamado com um parâmetro de transação não nulo.|  
|0xC001A004|-1073635324|DTS_E_INCOMPATIBLETRANSACTIONCONTEXT|Foi especificado um contexto de transação incompatível para uma conexão retida. Essa conexão foi estabelecida sob um contexto de transação diferente. As conexões retidas podem ser usadas sob exatamente um contexto de transação.|  
|0xC001B001|-1073631231|DTS_E_NOTSUSPENDED|Falha na chamada de retomada porque o pacote não foi suspenso. Isso ocorre quando o cliente faz uma chamada de retomada, mas o pacote não foi suspenso.|  
|0xC001B002|-1073631230|DTS_E_ALREADYEXECUTING|Falha na chamada Executar porque o executável já está sendo executado. Esse erro ocorre quando o cliente faz uma chamada Executar em um contêiner que ainda está sendo executado na última chamada de execução.|  
|0xC001B003|-1073631229|DTS_E_NOTEXECUTING|Falha na chamada de suspensão ou retomada porque o executável não está sendo executado, ou não é o executável de nível superior. Isso ocorre quando o cliente faz chamadas de suspensão ou retomada em um executável que não está processando no momento uma chamada de execução.|  
|0xC001C002|-1073627134|DTS_E_INVALIDFILE|O arquivo especificado no enumerador For Each File não é válido. Verifique se o arquivo especificado no enumerador For Each File existe.|  
|0xC001C010|-1073627120|DTS_E_VALUEINDEXNOTINTEGER|O índice de valor não é um inteiro. Mapeando um número de variável For Each %1!d! para a variável "%2".|  
|0xC001C011|-1073627119|DTS_E_VALUEINDEXNEGATIVE|O índice de valor é negativo. O Mapeamento de Variável ForEach número %1!d! para variável "%2".|  
|0xC001C012|-1073627118|DTS_E_FOREACHVARIABLEMAPPING|Mapeamento de Variável ForEach número %1!d! para variável "%2" não pode ser aplicado.|  
|0xC001C013|-1073627117|DTS_E_OBJECTNOTINFOREACHLOOP|Falha ao adicionar um objeto a um ForEachPropertyMapping que não é um filho direto do contêiner ForEachLoop.|  
|0xC001F001|-1073614847|DTS_E_FAILEDSYSTEMVARIABLEREMOVE|Falha ao remover uma variável de sistema. Esse erro ocorre quando se remove uma variável que é necessária.  Variáveis necessárias são aquelas criadas pelo tempo de execução para comunicação entre tarefas e o tempo de execução.|  
|0xC001F002|-1073614846|DTS_E_CHANGESYSTEMVARIABLEREADONLYFAILED|Falha na alteração da propriedade de uma variável porque é uma variável de sistema. As variáveis de sistema são somente leitura.|  
|0xC001F003|-1073614845|DTS_E_CHANGESYSTEMVARIABLENAMEFAILED|Falha na alteração do nome de uma variável porque é uma variável de sistema. As variáveis de sistema são somente leitura.|  
|0xC001F004|-1073614844|DTS_E_CHANGESYSTEMVARIABLENAMESPACEFAILED|Falha na alteração do namespace de uma variável porque é uma variável de sistema. As variáveis de sistema são somente leitura.|  
|0xC001F006|-1073614842|DTS_E_EVENTHANDLERNAMEREADONLY|Falha na alteração de nome do manipulador de eventos. Os nomes de manipulador de eventos são somente leitura.|  
|0xC001F008|-1073614840|DTS_E_PATHUNKNOWN|Não é possível recuperar o caminho para objeto. Esse é um erro de sistema.|  
|0xC001F009|-1073614839|DTS_E_RUNTIMEVARIABLETYPECHANGE|O tipo do valor que está sendo atribuído à variável "%1" difere do tipo variável atual. O tipo das variáveis não pode ser alterado durante a execução. Os tipos de variáveis são estritos, exceto para variáveis do tipo Objeto.|  
|0xC001F010|-1073614832|DTS_E_INVALIDSTRING|Caracteres inválidos na cadeia de caracteres: "%1". Isso ocorre quando uma cadeia de caracteres fornecida a um valor de propriedade contém caracteres não imprimíveis.|  
|0xC001F011|-1073614831|DTS_E_INVALIDOBJECTNAME|Nome do objeto SSIS é inválido. Mais erros específicos teriam sido gerados, explicando o problema exato de nomeação.|  
|0xC001F021|-1073614815|DTS_E_PROPERTYREADONLY|A propriedade "%1" é somente leitura. Isso ocorre quando se tenta alterar uma propriedade somente leitura.|  
|0xC001F022|-1073614814|DTS_E_FAILEDGETTYPEINFO|O objeto não dá suporte a informações de tipo. Isso ocorre quando o tempo de execução tenta obter as informações de tipo de um objeto para popular a coleção Properties.  O objeto deve dar suporte a informações de tipo.|  
|0xC001F023|-1073614813|DTS_E_FAILEDPROPERTYGET|Erro durante a recuperação do valor da propriedade "%1". O código de erro é 0x%2!8.8X!.|  
|0xC001F024|-1073614812|DTS_E_FAILEDPROPERTYGET_ERRORINFO|Erro durante a recuperação do valor da propriedade "%1". O código de erro é 0x%2!8.8X! "%3".|  
|0xC001F025|-1073614811|DTS_E_FAILEDPROPERTYSET|Erro durante a definição do valor da propriedade "%1". O erro retornado é 0x%2!8.8X!.|  
|0xC001F026|-1073614810|DTS_E_FAILEDPROPERTYSET_ERRORINFO|Erro durante a definição do valor da propriedade "%1". O erro retornado é 0x%2!8.8X! "%3".|  
|0xC001F027|-1073614809|DTS_E_PROPERTYWRITEONLY|A propriedade "%1" é somente gravação. Esse erro ocorre quando se tenta recuperar o valor de uma propriedade por meio de um objeto de propriedade, mas a propriedade é somente gravação.|  
|0xC001F028|-1073614808|DTS_E_NODISPATCH|O objeto não implementa IDispatch. Esse erro ocorre quando um objeto de propriedade ou uma coleção de propriedades tenta acessar uma interface IDispatch em um objeto.|  
|0xC001F029|-1073614807|DTS_E_NOCONTAININGTYPELIB|Não é possível recuperar a biblioteca de tipos do objeto. Esse erro ocorre quando a coleção Properties tenta recuperar a biblioteca de tipos de um objeto pela interface IDispatch.|  
|0xC001F02A|-1073614806|DTS_E_INVALIDTASKMONIKER|Não é possível criar uma tarefa a partir do XML da tarefa "%1!s!", tipo "%2!s!" devido ao erro 0x%3!8.8X! "%4!s!".|  
|0xC001F02C|-1073614804|DTS_E_FAILEDCREATEXMLDOCUMENT|Falha ao criar um documento XML "%1".|  
|0xC001F02D|-1073614803|DTS_E_PMVARPROPTYPESDIFFERENT|Ocorreu um erro porque existe um mapeamento de propriedade de uma variável a uma propriedade com um tipo diferente. O tipo de propriedade deve corresponder ao tipo de variável.|  
|0xC001F02E|-1073614802|DTS_E_PMINVALIDPROPMAPTARGET|Tentativa de definir mapeamento de propriedade para tipo de objeto de destino sem-suporte. Esse erro ocorre ao passar um tipo de objeto sem suporte para um mapeamento de propriedade.|  
|0xC001F02F|-1073614801|DTS_E_COULDNOTRESOLVEPACKAGEPATH|Não é possível resolver um caminho de pacote para um objeto no pacote "%1".  Verifique se o caminho de pacote é válido.|  
|0xC001F030|-1073614800|DTS_E_PMNODESTPROPERTY|A propriedade de destino do mapa de propriedade está vazia. Defina o nome de propriedade de destino.|  
|0xC001F031|-1073614799|DTS_E_INVALIDPROPERTYMAPPINGSFOUND|O pacote não restaurou nenhum mapeamento de propriedade.|  
|0xC001F032|-1073614798|DTS_E_AMBIGUOUSVARIABLENAME|O nome de variável é ambíguo porque existem diversas variáveis com esse nome em namespaces diferentes. Para evitar a ambiguidade, especifique um nome qualificado de namespace.|  
|0xC001F033|-1073614797|DTS_E_DESTINATIONOBJECTPARENTLESS|O objeto de destino em um mapeamento de propriedade não tem nenhum pai. O objeto de destino não é filho de nenhum contêiner sequência. Ele pode ter sido removido do pacote.|  
|0xC001F036|-1073614794|DTS_E_INVALIDPROPERTYMAPPING|O mapeamento de propriedade não é válido. O mapeamento foi ignorado.|  
|0xC001F038|-1073614792|DTS_E_PMFAILALERTREMOVE|Falha ao alertar os mapeamentos de propriedade de que o destino está sendo removido.|  
|0xC001F03A|-1073614790|DTS_E_INVALIDFOREACHPROPERTYMAPPING|Foi encontrado um mapeamento de propriedade inválido em For Each Loop. Isso ocorre quando há falha na restauração do mapeamento de propriedade ForEach.|  
|0xC001F040|-1073614784|DTS_E_PMPROPERTYINVALID|Uma propriedade de destino foi especificada em um mapeamento de propriedade inválido. Isso ocorre quando uma propriedade é especificada em um objeto de destino não encontrado nesse objeto.|  
|0xC001F041|-1073614783|DTS_E_INVALIDTASKMONIKERNOPARAM|Não é possível criar uma tarefa a partir do XML. Isso ocorre quando o tempo de execução não consegue resolver o nome para criar uma tarefa. Verifique se o nome está correto.|  
|0xC001F080|-1073614720|DTS_E_COULDNOTREPLACECHECKPOINTFILE|O arquivo de ponto de verificação existente não pode ser substituído pelo arquivo de ponto de verificação atualizado. O ponto de verificação foi criado com êxito em um arquivo temporário, mas houve falha na substituição do arquivo existente pelo arquivo novo.|  
|0xC001F081|-1073614719|DTS_E_CHECKPOINTFILENOTSPECIFIED|O pacote está configurado para sempre reinicializar a partir de um ponto de verificação, mas o arquivo de ponto de verificação não está especificado.|  
|0xC001F082|-1073614718|DTS_E_CHECKPOINTLOADXML|Falha na tentativa de carregar o arquivo de ponto de verificação de XML "%1" com o erro 0x%2!8.8X! "%3". Verifique se o nome de arquivo especificado está correto e se o arquivo existe.|  
|0xC001F083|-1073614717|DTS_E_LOADCHECKPOINT|Houve falha no pacote durante a execução porque o arquivo de ponto de verificação não pode ser carregado. Para continuar a execução do pacote, é necessário um arquivo de ponto de verificação. Esse erro normalmente ocorre quando a propriedade CheckpointUsage é definida como ALWAYS, especificando que o pacote é sempre reinicializado.|  
|0xC001F185|-1073614459|DTS_E_NOEVALEXPRESSION|A expressão de condição de avaliação no For Loop "%1" está vazia. Deve haver uma expressão de avaliação booliana no For Loop.|  
|0xC001F186|-1073614458|DTS_E_EXPREVALASSIGNMENTTYPEMISMATCH|O resultado da expressão de atribuição "%1" não pode ser convertido em um tipo compatível com a variável à qual foi atribuído.|  
|0xC001F187|-1073614457|DTS_E_EXPREVALASSIGNMENTTOREADONLYVARIABLE|Erro ao usar uma variável somente leitura "%1" em uma expressão de atribuição. O resultado da expressão não pode ser atribuído à variável porque ela é somente leitura. Escolha uma variável na qual seja possível gravar, ou remova a expressão dessa variável.|  
|0xC001F188|-1073614456|DTS_E_EXPREVALASSIGNMENTVARIABLELOCKFORWRITEFAILED|Não é possível avaliar a expressão "%1" porque a variável "%2" não existe ou não pode ser acessada para gravação. O resultado da expressão não pode ser atribuído à variável porque ela não foi encontrada, ou pôde ser bloqueada para acesso de gravação.|  
|0xC001F189|-1073614455|DTS_E_EXPREVALRESULTTYPENOTSUPPORTED|A expressão "%1" tem um tipo de resultado "%2" que não pode ser convertido em um tipo com suporte.|  
|0xC001F18A|-1073614454|DTS_E_EXPREVALRESULTTYPECONVERSIONFAILED|Falha na conversão do resultado da expressão "%1" do tipo "%2" em um tipo com suporte com o código de erro 0x%3!8.8X!. Ocorreu um erro inesperado ao tentar converter o resultado da expressão em um tipo com suporte dado pelo mecanismo de tempo de execução, mesmo sendo uma conversão de tipo com suporte.|  
|0xC001F200|-1073614336|DTS_E_DTSNAME_NOTNULL|O nome de objeto não é válido. O nome não pode ser definido como NULL.|  
|0xC001F201|-1073614335|DTS_E_DTSNAME_NOTEMPTY|O nome de objeto não é válido. O nome não pode estar vazio.|  
|0xC001F202|-1073614334|DTS_E_DTSNAME_LEGAL|O nome de objeto "%1" não é válido. O nome não pode conter nenhum dos caracteres a seguir: / \ : [ ] . =|  
|0xC001F203|-1073614333|DTS_E_DTSNAME_PRINTABLE|O nome de objeto "%1" não é válido. O nome não pode conter caracteres de controle que o tornem não imprimíveis.|  
|0xC001F204|-1073614332|DTS_E_DTSNAME_NOLEADWHITESP|O nome de objeto "%1" não é válido. O nome não pode começar com um espaço em branco.|  
|0xC001F205|-1073614331|DTS_E_DTSNAME_NOTRAILWHITESP|O nome de objeto "%1" não é válido. Nome não pode terminar com um espaço em branco.|  
|0xC001F206|-1073614330|DTS_E_DTSNAME_BEGINSWITHALPHA|O nome de objeto "%1" não é válido. O nome deve começar com um caractere alfabético.|  
|0xC001F207|-1073614329|DTS_E_DTSNAME_BEGINSWITHALPHAUNDERBAR|O nome de objeto "%1" não é válido. O nome deve começar com um caractere alfabético ou sublinhado "_".|  
|0xC001F208|-1073614328|DTS_E_DTSNAME_ALPHADIGITUNDERBAR|O nome de objeto "%1" não é válido. O nome deve conter apenas caracteres alfanuméricos ou sublinhados "_".|  
|0xC001F209|-1073614327|DTS_E_DTSNAME_VALIDFILENAME|O nome de objeto "%1" não é válido. O nome não pode conter nenhum dos caracteres a seguir: / \ : ? " < > &#124;|  
|0xC001F420|-1073613792|DTS_E_FAILLOADINGPROPERTY|Falha ao carregar a propriedade de valor "%1" usando a persistência padrão.|  
|0xC001F422|-1073613790|DTS_E_NODELISTENUM_INVALIDCONNMGRTYPE|O gerenciador de conexões "%1" não é do tipo "%2"|  
|0xC001F423|-1073613789|DTS_E_NODELISTENUM_XPATHISEMPTY|"%1" está vazio|  
|0xC001F424|-1073613788|DTS_E_NODELISTENUM_INVALIDDATANODE|Nó de dados inválido na seção do enumerador nodelist|  
|0xC001F425|-1073613787|DTS_E_NODELISTENUM_NOENUMERATORCREATED|Nenhum enumerador pode ser criado|  
|0xC001F427|-1073613785|DTS_E_OPERATIONFAILCACHEINUSE|Falha na operação porque o cache está em uso.|  
|0xC001F428|-1073613784|DTS_E_PROPERTYCANNOTBEMODIFIED|A propriedade não pode ser modificada.|  
|0xC001F429|-1073613783|DTS_E_PACKAGEUPGRADEFAILED|Falha na atualização de pacote.|  
|0xC00220DE|-1073602338|DTS_E_TKEXECPACKAGE_UNABLETOLOADFILE|Erro 0x%1!8.8X! ao carregar o arquivo de pacote "%3". %2.|  
|0xC00220DF|-1073602337|DTS_E_TKEXECPACKAGE_UNSPECIFIEDPACKAGE|O pacote não foi especificado.|  
|0xC00220E0|-1073602336|DTS_E_TKEXECPACKAGE_UNSPECIFIEDCONNECTION|A conexão não foi especificada.|  
|0xC00220E2|-1073602334|DTS_E_TKEXECPACKAGE_INCORRECTCONNECTIONMANAGERTYPE|O gerenciador de conexões "%1" tem um tipo "%2" sem-suporte. É dado suporte apenas a gerenciadores de conexões "FILE" e "OLEDB".|  
|0xC00220E3|-1073602333|DTS_E_TKEXECPACKAGE_UNABLETOLOADXML|Erro 0x%1!8.8X! ao carregar o arquivo de pacote "%3" em um documento XML. %2.|  
|0xC00220E4|-1073602332|DTS_E_TKEXECPACKAGE_UNABLETOLOAD|Erro 0x%1!8.8X! ao preparar para carregar o pacote. %2.|  
|0xC0024102|-1073594110|DTS_E_TASKVALIDATIONFAILED|Falha do método Validate na tarefa com o código de erro 0x%1!8.8X! (%2). O método Validate deve ter êxito e indicar o resultado usando um parâmetro "out".|  
|0xC0024104|-1073594108|DTS_E_TASKEXECUTEFAILED|O método Execute na tarefa retornou o código de erro 0x%1!8.8X! (%2). O método Execute deve ter êxito e indicar o resultado usando um parâmetro "out".|  
|0xC0024105|-1073594107|DTS_E_RETRIEVINGDEPENDENCIES|Falha na tarefa "%1": 0x%2!8.8X! ao recuperar dependências. O tempo de execução estava recuperando as dependências da coleção de dependências da tarefa quando ocorreu o erro. A tarefa pode ter implementado incorretamente uma das interfaces de dependência.|  
|0xC0024107|-1073594105|DTS_E_TASKVALIDATIONERROR|Houve erros durante a validação da tarefa.|  
|0xC0024108|-1073594104|DTS_E_CONNECTIONSTRINGFORMAT|O formato de cadeia de caracteres de conexão não é válido. Ele deve consistir em um ou mais componentes do formato X=Y, separados por ponto-e-vírgulas. Esse erro ocorre quando uma cadeia de caracteres de conexão sem nenhum componente é definida em um gerenciador de conexões de banco de dados.|  
|0xC0024109|-1073594103|DTS_E_UNQUOTEDSEMICOLON|Os componentes da cadeia de caracteres de conexão não podem conter ponto-e-vírgulas sem-aspas. Se o valor tiver que conter ponto e vírgula, coloque todo esse valor entre aspas. Esse erro ocorre quando os valores na cadeia de caracteres de conexão contêm ponto-e-vírgulas sem-aspas, como na propriedade InitialCatalog.|  
|0xC002410A|-1073594102|DTS_E_LOGPROVIDERVALIDATIONFAILED|Falha na validação de um ou mais provedores de log. Não é possível executar o pacote. O pacote não pode ser executado quando um provedor de log falha.|  
|0xC002410B|-1073594101|DTS_E_INVALIDVALUEINARRAY|Valor inválido na matriz.|  
|0xC002410C|-1073594100|DTS_E_ENUMERATIONELEMENTNOTENUMERABLE|Um elemento do enumerador retornado pelo Enumerador ForEach não implementa IEnumerator, contradizendo a propriedade CollectionEnumerator do Enumerador ForEach.|  
|0xC002410D|-1073594099|DTS_E_INVALIDENUMERATORINDEX|Falha no enumerador para recuperar o elemento no índice "%1!d!".|  
|0xC0029100|-1073573632|DTS_E_AXTASK_MISSING_ENTRY_METHOD_NAME|Função não encontrada.|  
|0xC0029101|-1073573631|DTS_E_AXTASK_EMPTY_SCRIPT|Função não encontrada.|  
|0xC0029102|-1073573630|DTS_E_AXTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|A Tarefa Script do ActiveX foi iniciada com um elemento XML errado.|  
|0xC0029105|-1073573627|DTS_E_AXTASK_HANDLER_NOT_FOUND|Manipulador não encontrado.|  
|0xC0029106|-1073573626|DTS_E_AXTASKUTIL_ENUMERATE_LANGUAGES_FAILED|Ocorreu um erro durante a tentativa de recuperação das linguagens de scripts instaladas no sistema.|  
|0xC0029107|-1073573625|DTS_E_AXTASKUTIL_SCRIPTHOST_CREATE_FAILED|Ocorreu um erro durante a criação de um host de scripts ActiveX. Verifique se o host de scripts está instalado corretamente.|  
|0xC0029108|-1073573624|DTS_E_AXTASKUTIL_SCRIPTHOSTINIT_FAILED|Ocorreu um erro durante a tentativa de criação de uma instância do host de scripts para a linguagem escolhida. Verifique se a linguagem de scripts escolhida está instalada no sistema.|  
|0xC0029109|-1073573623|DTS_E_AXTASKUTIL_ADDVARIABLES_FAILED|Ocorreu um erro ao adicionar as variáveis SSIS ao namespace de host de script. Isso deve impedir a tarefa de usar variáveis SSIS no script.|  
|0xC002910A|-1073573622|DTS_E_AXTASKUTIL_SCRIPT_PARSING_FAILED|Ocorreu um erro fatal ao tentar analisar o texto do script. Verifique se o mecanismo de script para a linguagem escolhida está instalado corretamente.|  
|0xC002910B|-1073573621|DTS_E_AXTASKUTIL_MSG_BAD_FUNCTION|O nome de função digitado não é válido. Verifique se foi especificado um nome válido de função.|  
|0xC002910C|-1073573620|DTS_E_AXTASKUTIL_EXECUTION_FAILED|Ocorreu um erro durante a execução do script. Verifique se o mecanismo de script para a linguagem selecionada está instalado corretamente.|  
|0xC002910D|-1073573619|DTS_E_AXTASKUTIL_ADDTYPELIB_FAILED|Ocorreu um erro ao adicionar a biblioteca de tipos gerenciados ao host de script. Verifique se o tempo de execução DTS 2000 está instalado.|  
|0xC002910E|-1073573618|DTS_E_BITASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|A tarefa Inserção em Massa foi iniciada com um elemento XML errado.|  
|0xC002910F|-1073573617|DTS_E_BITASK_DATA_FILE_NOT_SPECIFIED|Nome de arquivo de dados não especificado.|  
|0xC0029110|-1073573616|DTS_E_BITASK_HANDLER_NOT_FOUND|Manipulador não encontrado.|  
|0xC0029111|-1073573615|DTS_E_BITASK_CANNOT_ACQUIRE_CONNECTION|Falha na aquisição da conexão especificada: "%1".|  
|0xC0029112|-1073573614|DTS_E_BITASK_NO_CONNECTION_MANAGER_SPECIFIED|Falha na tentativa de obter o Gerenciador de Conexões.|  
|0xC0029113|-1073573613|DTS_E_BITASK_INVALID_CONNECTION|A conexão não é válida.|  
|0xC0029114|-1073573612|DTS_E_BITASK_NULL_CONNECTION|A conexão é nula.|  
|0xC0029115|-1073573611|DTS_E_BITASK_EXECUTE_FAILED|Falha na execução.|  
|0xC0029116|-1073573610|DTS_E_BITASK_CANNOT_RETRIEVE_TABLES|Ocorreu um erro ao recuperar as tabelas do banco de dados.|  
|0xC0029117|-1073573609|DTS_E_BITASK_CANNOT_RETRIEVE_COLUMN_INFO|Ocorreu um erro ao recuperar as colunas da tabela.|  
|0xC0029118|-1073573608|DTS_E_BITASK_ERROR_IN_DB_OPERATION|Ocorreu um erro na operação de banco de dados.|  
|0xC0029119|-1073573607|DTS_E_BITASK_INVALIDSOURCECONNECTIONNAME|A conexão especificada "%1" não é válida ou aponta para um objeto inválido. Para continuar, especifique uma conexão válida.|  
|0xC002911A|-1073573606|DTS_E_BITASK_INVALIDDESTCONNECTIONNAME|A conexão de destino especificada não é válida. Forneça uma conexão válida para continuar.|  
|0xC002911B|-1073573605|DTS_E_BITASK_DESTINATION_TABLE_NOT_SPECIFIED|Para continuar, especifique um nome de tabela.|  
|0xC002911C|-1073573604|DTS_E_BITASK_ERROR_IN_LOAD_FROM_XML|Erro em LoadFromXML na marca "%1".|  
|0xC002911D|-1073573603|DTS_E_BITASK_ERROR_IN_SAVE_TO_XML|Erro em SaveToXML na marca "%1".|  
|0xC002911E|-1073573602|DTS_E_BITASKUNMANCONNECTION_INVALID_CONNECTION|A conexão não é válida.|  
|0xC002911F|-1073573601|DTS_E_BITASKUNMANCONNECTION_EXECUTE_FAILED|Falha na execução.|  
|0xC0029120|-1073573600|DTS_E_BITASKUNMANCONNECTION_CANNOT_RETRIEVE_TABLES|Ocorreu um erro ao recuperar as tabelas do banco de dados.|  
|0xC0029121|-1073573599|DTS_E_BITASKUNMANCONNECTION_CANNOT_RETRIEVE_COLUMN_INFO|Ocorreu um erro ao recuperar as colunas da tabela.|  
|0xC0029122|-1073573598|DTS_E_BITASKUNMANCONNECTION_CANNOT_OPEN_FILE|Ocorreu um erro ao tentar abrir o arquivo de dados.|  
|0xC0029123|-1073573597|DTS_E_BITASKUNMANCONNECTION_OEM_CONVERSION_FAILED|Não é possível converter a entrada do arquivo OEM no formato especificado.|  
|0xC0029124|-1073573596|DTS_E_BITASKUNMANCONNECTION_ERROR_IN_DB_OPERATION|Erro na operação de banco de dados.|  
|0xC0029125|-1073573595|DTS_E_DTSPROCTASK_NOCONNECTIONSPECIFIED|Nenhum gerenciador de conexões especificado.|  
|0xC0029126|-1073573594|DTS_E_DTSPROCTASK_CONNECTIONMANAGERNOTOLAP|A conexão "%1" não é uma conexão do Analysis Services.|  
|0xC0029127|-1073573593|DTS_E_DTSPROCTASK_UNABLETOLOCATECONNECTIONMANAGER|Não é possível localizar a conexão "%1".|  
|0xC0029128|-1073573592|DTS_E_DTSPROCTASK_INVALIDTASKDATANODEEXE|A tarefa Executar DDL do Analysis Services recebeu um nó de dados de tarefa inválido.|  
|0xC0029129|-1073573591|DTS_E_DTSPROCTASK_INVALIDTASKDATANODEPROC|A tarefa Processamento do Analysis Services recebeu um nó de dados de tarefa inválido.|  
|0xC002912A|-1073573590|DTS_E_DTSPROCTASK_INVALIDDDL|O DDL não é válido.|  
|0xC002912B|-1073573589|DTS_E_DTSPROCTASK_INVALIDDDLPROCESSINGCOMMANDS|O DDL encontrado em ProcessingCommands não é válido.|  
|0xC002912C|-1073573588|DTS_E_DTSPROCTASK_CANNOTWRITEINAREADONLYVARIABLE|O resultado da Execução não pode ser salvo em uma variável somente leitura.|  
|0xC002912D|-1073573587|DTS_E_DTSPROCTASK_INVALIDVARIABLE|A variável "%1" não foi definida.|  
|0xC002912E|-1073573586|DTS_E_DTSPROCTASK_CONNECTIONNOTFOUND|O Gerenciador de Conexões "%1" não foi definido.|  
|0xC002912F|-1073573585|DTS_E_DTSPROCTASK_INVALIDCONNECTION|O Gerenciador de Conexões "%1" não é um Gerenciador de Conexões FILE.|  
|0xC0029130|-1073573584|DTS_E_DTSPROCTASK_NONEXISTENTATTRIBUTE|"%1" não foi encontrado durante a desserialização.|  
|0xC0029131|-1073573583|DTS_E_DTSPROCTASK_TRACEHASBEENSTOPPED|O rastreamento foi interrompido por causa de uma exceção.|  
|0xC0029132|-1073573582|DTS_E_DTSPROCTASK_DDLEXECUTIONFAILED|Falha na execução de DDL.|  
|0xC0029133|-1073573581|DTS_E_DTSPROCTASK_FILEDOESNOTEXIST|Não existe nenhum arquivo associado à conexão "%1".|  
|0xC0029134|-1073573580|DTS_E_DTSPROCTASK_VARIABLENOTDEFINED|A variável "%1" não foi definida.|  
|0xC0029135|-1073573579|DTS_E_DTSPROCTASK_FILECONNECTIONNOTDEFINED|A conexão de arquivo "%1" não foi definida.|  
|0xC0029136|-1073573578|DTS_E_EXEC2000PKGTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|A tarefa Executar Pacote DTS 2000 foi iniciada com um elemento XML errado.|  
|0xC0029137|-1073573577|DTS_E_EXEC2000PKGTASK_HANDLER_NOT_FOUND|Manipulador não encontrado.|  
|0xC0029138|-1073573576|DTS_E_EXEC2000PKGTASK_PACKAGE_NAME_NOT_SPECIFIED|O nome do pacote não está especificado.|  
|0xC0029139|-1073573575|DTS_E_EXEC2000PKGTASK_PACKAGE_ID_NOT_SPECIFIED|A ID do pacote não está especificada.|  
|0xC002913A|-1073573574|DTS_E_EXEC2000PKGTASK_PACKAGE_VERSIONGUID_NOT_SPECIFIED|O GUID da versão do pacote não está especificado.|  
|0xC002913B|-1073573573|DTS_E_EXEC2000PKGTASK_SQLSERVER_NOT_SPECIFIED|O SQL Server não está especificado.|  
|0xC002913C|-1073573572|DTS_E_EXEC2000PKGTASK_SQL_USERNAME_NOT_SPECIFIED|O nome de usuário do SQL Server não está especificado.|  
|0xC002913D|-1073573571|DTS_E_EXEC2000PKGTASK_FILE_NAME_NOT_SPECIFIED|O nome do arquivo de armazenamento não está especificado.|  
|0xC002913E|-1073573570|DTS_E_EXEC2000PKGTASK_DTS2000CANTBEEMPTY|A propriedade do pacote DTS 2000 está vazia.|  
|0xC002913F|-1073573569|DTS_E_EXEC2000PKGTASK_ERROR_IN_PACKAGE_EXECUTE|Ocorreu um erro durante a execução do pacote DTS 2000.|  
|0xC0029140|-1073573568|DTS_E_EXEC2000PKGTASK_SQLSERVER_NOT_AVAILABLE_NETWORK|Não é possível carregar os SQL Servers disponíveis da rede. Verifique a conexão de rede.|  
|0xC0029141|-1073573567|DTS_E_EXEC2000PKGTASK_DATATYPE_NULL|O tipo de dados não pode ser nulo. Especifique o tipo de dados correto para usar na validação do valor.|  
|0xC0029142|-1073573566|DTS_E_EXEC2000PKGTASK_NULL_VALUE|Não é possível validar um valor nulo em relação a nenhum tipo de dados.|  
|0xC0029143|-1073573565|DTS_E_EXEC2000PKGTASK_NULL_VALUE_ARGUMENT|Um argumento necessário é nulo.|  
|0xC0029144|-1073573564|DTS_E_EXEC2000PKGTASK_CLS_NOT_REGISTRED_EXCEPTION|Para executar a tarefa Pacote do DTS 2000, inicie a Instalação do SQL Server e use o botão Avançado da página Componentes a Serem Instalados para selecionar Componentes Legados.|  
|0xC0029145|-1073573563|DTS_E_EXEC2000PKGTASK_NOT_PRIMITIVE_TYPE|"%1" não é um tipo de valor.|  
|0xC0029146|-1073573562|DTS_E_EXEC2000PKGTASK_CONVERT_FAILED|Não foi possível converter "%1" em "%2".|  
|0xC0029147|-1073573561|DTS_E_EXEC2000PKGTASK_ERROR_IN_VALIDATE|Não foi possível validar "%1" em relação a "%2".|  
|0xC0029148|-1073573560|DTS_E_EXEC2000PKGTASK_ERROR_IN_LOAD_FROM_XML|Erro em LoadFromXML na marca "%1".|  
|0xC0029149|-1073573559|DTS_E_EXEC2000PKGTASK_ERROR_IN_SAVE_TO_XML|Erro em SaveToXML na marca "%1".|  
|0xC002914A|-1073573558|DTS_E_EXECPROCTASK_INVALIDTIMEOUT|O valor fornecido de tempo limite não é válido. Especifique o número de segundos que a tarefa permite que o processo seja executado. O tempo limite mínimo é 0, indicando que não é usado nenhum valor de tempo limite e o processo é executado até ser concluído ou até ocorrer um erro. O tempo limite máximo é 2147483 (((2^31) - 1)/1000).|  
|0xC002914B|-1073573557|DTS_E_EXECPROCTASK_CANTREDIRECTIO|Não é possível redirecionar fluxos se o processo puder continuar em execução depois do tempo de vida da tarefa.|  
|0xC002914C|-1073573556|DTS_E_EXECPROCTASK_PROCESSHASTIMEDOUT|O processo expirou.|  
|0xC002914D|-1073573555|DTS_E_EXECPROCTASK_EXECUTABLENOTSPECIFIED|O executável não está especificado.|  
|0xC002914E|-1073573554|DTS_E_EXECPROCTASK_STDOUTVARREADONLY|O padrão fora da variável é somente leitura.|  
|0xC002914F|-1073573553|DTS_E_EXECPROCTASK_STDERRVARREADONLY|A variável de erro padrão é somente leitura.|  
|0xC0029150|-1073573552|DTS_E_EXECPROCTASK_RECEIVEDINVALIDTASKDATANODE|A tarefa Executar Processo recebeu um nó de dados de tarefa que não é válido.|  
|0xC0029151|-1073573551|DTS_E_EXECPROCTASK_PROCESSEXITCODEEXCEEDS|Executando "%2" "%3" em "%1", O código de saída de processo era "%4" enquanto o esperado era "%5".|  
|0xC0029152|-1073573550|DTS_E_EXECPROCTASK_WORKINGDIRDOESNOTEXIST|O diretório "%1" não existe.|  
|0xC0029153|-1073573549|DTS_E_EXECPROCTASK_FILEDOESNOTEXIST|O arquivo/processo "%1" não existe no diretório "%2".|  
|0xC0029154|-1073573548|DTS_E_EXECPROCTASK_FILENOTINPATH|O arquivo/processo "%1" não está no caminho.|  
|0xC0029156|-1073573546|DTS_E_EXECPROCTASK_WORKINGDIRECTORYDOESNOTEXIST|O Diretório de Trabalho "%1" não existe.|  
|0xC0029157|-1073573545|DTS_E_EXECPROCTASK_ERROREXECUTIONVALUE|O processo saiu com o código de retorno "%1". No entanto, era esperado "%2".|  
|0xC0029158|-1073573544|DTS_E_FSTASK_SYNCFAILED|Falha no objeto de sincronização.|  
|0xC0029159|-1073573543|DTS_E_FSTASK_INVALIDDATA|A tarefa Sistema de Arquivos recebeu um nó de dados de tarefa inválido.|  
|0xC002915A|-1073573542|DTS_E_FSTASK_DIRECTORYEXISTS|O Diretório já existe.|  
|0xC002915B|-1073573541|DTS_E_FSTASK_PATHNOTVALID|"%1" não é válido no tipo de operação "%2".|  
|0xC002915C|-1073573540|DTS_E_FSTASK_DESTINATIONNOTSET|A propriedade de destino da operação "%1" não foi definida.|  
|0xC002915D|-1073573539|DTS_E_FSTASK_SOURCENOTSET|A propriedade de origem da operação "%1" não foi definida.|  
|0xC002915E|-1073573538|DTS_E_FSTASK_CONNECTIONTYPENOTFILE|O Tipo de Conexão "%1" não é um arquivo.|  
|0xC002915F|-1073573537|DTS_E_FSTASK_VARIABLEDOESNTEXIST|A variável "%1" não existe.|  
|0xC0029160|-1073573536|DTS_E_FSTASK_VARIABLENOTASTRING|A variável "%1" não é uma cadeia de caracteres.|  
|0xC0029163|-1073573533|DTS_E_FSTASK_FILEDOESNOTEXIST|O arquivo ou diretório "%1" representado pela conexão "%2" não existe.|  
|0xC0029165|-1073573531|DTS_E_FSTASK_DESTCONNUSAGETYPEINVALID|O gerenciador de conexões de arquivo de destino "%1" tem um tipo de uso inválido: "%2".|  
|0xC0029166|-1073573530|DTS_E_FSTASK_SRCCONNUSAGETYPEINVALID|O gerenciador de conexões de arquivo de origem "%1" tem um tipo de uso "%2" inválido.|  
|0xC0029167|-1073573529|DTS_E_FSTASK_LOGENTRYGETTINGFILEOPERATION|FileSystemOperation|  
|0xC0029168|-1073573528|DTS_E_FSTASK_LOGENTRYGETTINGFILEOPERATIONDESC|Fornece informações relacionadas a operações do Sistema de Arquivos.|  
|0xC0029169|-1073573527|DTS_E_FSTASK_TASKDISPLAYNAME|Tarefa Sistema de Arquivos|  
|0xC002916A|-1073573526|DTS_E_FSTASK_TASKDESCRIPTION|Executa operações de sistema de arquivos, como copiar e excluir arquivos.|  
|0xC002916B|-1073573525|DTS_E_FTPTASK_SYNCOBJFAILED|Falha no objeto de sincronização.|  
|0xC002916C|-1073573524|DTS_E_FTPTASK_UNABLETOOBTAINFILELIST|Não é possível obter a lista de arquivos.|  
|0xC002916D|-1073573523|DTS_E_FTPTASK_LOCALPATHEMPTY|O caminho local está vazio.|  
|0xC002916E|-1073573522|DTS_E_FTPTASK_REMOTEPATHEMPTY|O caminho remoto está vazio.|  
|0xC002916F|-1073573521|DTS_E_FTPTASK_LOCALVARIBALEEMPTY|A variável local está vazia.|  
|0xC0029170|-1073573520|DTS_E_FTPTASK_REMOTEVARIBALEEMPTY|A variável remota está vazia.|  
|0xC0029171|-1073573519|DTS_E_FTPTASK_FTPRCVDINVLDDATANODE|A tarefa FTP recebeu um nó de dados de tarefa inválido.|  
|0xC0029172|-1073573518|DTS_E_FTPTASK_CONNECTION_NAME_NULL|A conexão está vazia. Verifique se foi fornecida uma conexão FTP válida.|  
|0xC0029173|-1073573517|DTS_E_FTPTASK_CONNECTION_NOT_FTP|A conexão especificada não é uma conexão FTP. Verifique se foi fornecida uma conexão FTP válida.|  
|0xC0029175|-1073573515|DTS_E_FTPTASK__INITIALIZATION_WITH_NULL_XML_ELEMENT|Não é possível inicializar a tarefa com um elemento XML nulo.|  
|0xC0029176|-1073573514|DTS_E_FTPTASK_SAVE_TO_NULL_XML_ELEMENT|Não é possível salvar a tarefa em um documento XML nulo.|  
|0xC0029177|-1073573513|DTS_E_FTPTASK_ERROR_IN_LOAD_FROM_XML|Erro em LoadFromXML na marca "%1".|  
|0xC0029178|-1073573512|DTS_E_FTPTASK_NOFILESATLOCATION|Não existem arquivos em "%1".|  
|0xC0029179|-1073573511|DTS_E_FTPTASK_LOCALVARIABLEISEMPTY|A variável "%1" está vazia.|  
|0xC002917A|-1073573510|DTS_E_FTPTASK_REMOTEVARIABLEISEMPTY|A variável "%1" está vazia.|  
|0xC002917B|-1073573509|DTS_E_FTPTASK_NOFILESINCONNMGR|O Arquivo "%1" não contém caminho(s) de arquivo.|  
|0xC002917C|-1073573508|DTS_E_FTPTASK_NOFILEPATHSINLOCALVAR|A variável "%1" não contém caminho(s) de arquivo.|  
|0xC002917D|-1073573507|DTS_E_FTPTASK_VARIABLENOTASTRING|A variável "%1" não é uma cadeia de caracteres.|  
|0xC002917E|-1073573506|DTS_E_FTPTASK_VARIABLENOTFOUND|A variável "%1" não existe.|  
|0xC002917F|-1073573505|DTS_E_FTPTASK_INVALIDPATHONOPERATION|Caminho inválido na operação "%1".|  
|0xC0029180|-1073573504|DTS_E_FTPTASK_DIRECTORYEXISTS|"%1" já existe.|  
|0xC0029182|-1073573502|DTS_E_FTPTASK_CONNECTIONTYPENOTFILE|O Tipo de Conexão "%1" não é um arquivo.|  
|0xC0029183|-1073573501|DTS_E_FTPTASK_FILEDOESNOTEXIST|O arquivo representado por "%1" não existe.|  
|0xC0029184|-1073573500|DTS_E_FTPTASK_INVALIDDIRECTORY|O diretório não foi especificado na variável "%1".|  
|0xC0029185|-1073573499|DTS_E_FTPTASK_NOFILESFOUND|Nenhum arquivo encontrado em "%1".|  
|0xC0029186|-1073573498|DTS_E_FTPTASK_NODIRECTORYPATHINCONMGR|O diretório não foi especificado no gerenciador de conexões de arquivo "%1".|  
|0xC0029187|-1073573497|DTS_E_FTPTASK_UNABLETODELETELOCALEFILE|Não é possível excluir o arquivo local "%1".|  
|0xC0029188|-1073573496|DTS_E_FTPTASK_UNABLETOREMOVELOCALDIRECTORY|Não é possível remover o diretório local "%1".|  
|0xC0029189|-1073573495|DTS_E_FTPTASK_UNABLETOCREATELOCALDIRECTORY|Não é possível criar o diretório local "%1".|  
|0xC002918A|-1073573494|DTS_E_FTPTASK_UNABLETORECEIVEFILES|Não é possível receber arquivos usando "%1".|  
|0xC002918B|-1073573493|DTS_E_FTPTASK_UNABLETOSENDFILES|Não é possível enviar arquivos usando "%1".|  
|0xC002918C|-1073573492|DTS_E_FTPTASK_UNABLETOMAKEDIRREMOTE|Não é possível criar diretório remoto usando "%1".|  
|0xC002918D|-1073573491|DTS_E_FTPTASK_UNABLETOREMOVEDIRREMOTE|Não é possível remover diretório remoto usando "%1".|  
|0xC002918E|-1073573490|DTS_E_FTPTASK_UNABLETODELETEREMOTEFILES|Não é possível excluir arquivos remotos usando "%1".|  
|0xC002918F|-1073573489|DTS_E_FTPTASK_UNABLETOCONNECTTOSERVER|Não é possível se conectar ao servidor FTP usando "%1".|  
|0xC0029190|-1073573488|DTS_E_FTPTASK_INVALIDVARIABLEVALUE|A variável "%1" não começa com "/".|  
|0xC0029191|-1073573487|DTS_E_FTPTASK_INVALIDREMOTEPATH|O caminho remoto "%1" não começa com "/".|  
|0xC0029192|-1073573486|DTS_E_DTS_E_FTPTASK_CANNOT_ACQUIRE_CONNECTION|Ocorreu um erro ao adquirir a conexão FTP. Verifique se foi especificado um tipo de conexão "%1" válido.|  
|0xC0029193|-1073573485|DTS_E_MSGQTASKUTIL_CERT_OPEN_STORE_FAILED|Falha ao abrir o repositório de certificados.|  
|0xC0029194|-1073573484|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_DISPLAY_NAME|Ocorreu um erro durante a recuperação do nome para exibição do certificado.|  
|0xC0029195|-1073573483|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_ISSUER_NAME|Ocorreu um erro durante a recuperação do nome do emissor do certificado.|  
|0xC0029196|-1073573482|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_FRIENDLY_NAME|Ocorreu um erro durante a recuperação do nome amigável do certificado.|  
|0xC0029197|-1073573481|DTS_E_MSMQTASK_NO_CONNECTION|O nome da conexão MSMQ não está definido.|  
|0xC0029198|-1073573480|DTS_E_MSMQTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|A tarefa foi inicializada com o elemento XML errado.|  
|0xC0029199|-1073573479|DTS_E_MSMQTASK_DATA_FILE_NAME_EMPTY|O nome do arquivo de dados está vazio.|  
|0xC002919A|-1073573478|DTS_E_MSMQTASK_DATA_FILE_SAVE_NAME_EMPTY|O nome especificado para o arquivo de dados a ser salvo está vazio.|  
|0xC002919B|-1073573477|DTS_E_MSMQTASK_DATA_FILE_SIZE_ERROR|O tamanho do arquivo deve ser menor que 4 MB.|  
|0xC002919C|-1073573476|DTS_E_MSMQTASK_DATA_FILE_SAVE_FAILED|Falha ao salvar o arquivo de dados.|  
|0xC002919D|-1073573475|DTS_E_MSMQTASK_STRING_COMPARE_VALUE_MISSING|O valor de filtro de cadeia de caracteres está vazio.|  
|0xC002919E|-1073573474|DTS_E_MSMQTASK_INVALID_QUEUE_PATH|O caminho da fila não é válido.|  
|0xC002919F|-1073573473|DTS_E_MSMQTASK_NOT_TRANSACTIONAL|A tarefa da fila de mensagens não oferece suporte à inscrição em transações distribuídas.|  
|0xC00291A0|-1073573472|DTS_E_MSMQTASK_INVALID_MESSAGE_TYPE|O tipo de mensagem não é válido.|  
|0xC00291A1|-1073573471|DTS_E_MSMQTASK_TASK_TIMEOUT|A fila de mensagens expirou. Nenhuma mensagem foi recebida.|  
|0xC00291A2|-1073573470|DTS_E_MSMQTASK_INVALID_PROPERTY_VALUE|A propriedade especificada não é válida. Verifique se o tipo de argumento está correto.|  
|0xC00291A3|-1073573469|DTS_E_MSMQTASK_MESSAGE_NON_AUTHENTICATED|A mensagem não está autenticada.|  
|0xC00291A4|-1073573468|DTS_E_MSMQTASK_INVALID_ENCRYPTION_ALGO_WRAPPER|Você está tentando definir o valor do Algoritmo de Criptografia com um objeto inválido.|  
|0xC00291A5|-1073573467|DTS_E_MSMQTASK_VARIABLE_TO_RECEIVE_STRING_MSG_EMPTY|A variável para receber a mensagem de cadeia de caracteres está vazia.|  
|0xC00291A6|-1073573466|DTS_E_MSMQTASK_RECEIVE_VARIABLE_EMPTY|A variável para receber a mensagem de variável está vazia.|  
|0xC00291A7|-1073573465|DTS_E_MSMQTASK_CONNECTIONTYPENOTMSMQ|A conexão "%1" não é do tipo MSMQ.|  
|0xC00291A8|-1073573464|DTS_E_MSMQTASK_DATAFILE_ALREADY_EXISTS|O arquivo de dados "%1" já existe no local especificado. Não é possível substituir o arquivo porque a opção Substituir está definida como falsa.|  
|0xC00291A9|-1073573463|DTS_E_MSMQTASK_STRING_MSG_TO_VARIABLE_NOT_FOUND|A variável especificada "%1" para receber a mensagem de cadeia de caracteres não foi encontrada na coleção de variáveis do pacote.|  
|0xC00291AA|-1073573462|DTS_E_MSMQTASK_CONNMNGRNULL|O gerenciador de conexões "%1" está vazio.|  
|0xC00291AB|-1073573461|DTS_E_MSMQTASK_CONNMNGRDOESNOTEXIST|O gerenciador de conexões "%1" não existe.|  
|0xC00291AC|-1073573460|DTS_E_SCRIPTTASK_COMPILEERRORMSG|Erro "%1": "%2 "\r\nLinha "%3" Coluna "%4" por "%5".|  
|0xC00291AD|-1073573459|DTS_E_SCRIPTTASK_COMPILEERRORMSG2|Erro na compilação do script: "%1".|  
|0xC00291AE|-1073573458|DTS_E_SCRIPTTASK_COMPILEERRORMSG3|Erro "%1": "%2"\r\nLinha "%3" Colunas "%4"-"%5"\r\nTexto da Linha: "%6".|  
|0xC00291AF|-1073573457|DTS_E_SCRIPTTASK_SCRIPTREPORTEDFAILURE|O script de usuário retornou um resultado de falha.|  
|0xC00291B0|-1073573456|DTS_E_SCRIPTTASK_SCRIPTFILESFAILEDTOLOAD|Falha ao carregar os arquivos de script de usuário.|  
|0xC00291B1|-1073573455|DTS_E_SCRIPTTASK_SCRIPTTHREWEXCEPTION|O script de usuário emitiu uma exceção: "%1".|  
|0xC00291B2|-1073573454|DTS_E_SCRIPTTASK_COULDNOTCREATEENTRYPOINTCLASS|Não foi possível criar uma instância de classe de ponto de entrada "%1".|  
|0xC00291B3|-1073573453|DTS_E_SCRIPTTASK_LOADFROMXMLEXCEPTION|Houve uma exceção ao carregar a Tarefa Script do XML: "%1".|  
|0xC00291B4|-1073573452|DTS_E_SCRIPTTASK_SOURCEITEMNOTFOUNDEXCEPTION|O item de origem "%1" não foi encontrado no pacote.|  
|0xC00291B5|-1073573451|DTS_E_SCRIPTTASK_BINARYITEMNOTFOUNDEXCEPTION|O item binário "%1" não foi encontrado no pacote.|  
|0xC00291B6|-1073573450|DTS_E_SCRIPTTASK_UNRECOGNIZEDSCRIPTLANGUAGEEXCEPTION|"%1" não foi reconhecido como linguagem de script válida.|  
|0xC00291B7|-1073573449|DTS_E_SCRIPTTASK_ILLEGALSCRIPTNAME|O nome de script "__" não é válido. Ele não pode conter espaços, barras, caracteres especiais, ou começar com um número.|  
|0xC00291B8|-1073573448|DTS_E_SCRIPTTASK_INVALIDSCRIPTLANGUAGE|A linguagem de script especificada não é válida.|  
|0xC00291B9|-1073573447|DTS_E_SCRIPTTASK_CANTINITNULLTASK|Não é possível inicializar para uma tarefa nula.|  
|0xC00291BA|-1073573446|DTS_E_SCRIPTTASK_MUSTINITWITHRIGHTTASK|A interface do usuário de Tarefa Script deve ser inicializada para uma Tarefa Script.|  
|0xC00291BB|-1073573445|DTS_E_SCRIPTTASK_WASNOTINITED|A interface do usuário de Tarefa Script não foi inicializada.|  
|0xC00291BC|-1073573444|DTS_E_SCRIPTTASK_HOST_NAME_CANT_EMPTY|O nome não pode estar vazio.|  
|0xC00291BD|-1073573443|DTS_E_SCRIPTTASK_INVALID_SCRIPT_NAME|O nome do projeto não é válido. Ele não pode conter espaços, barras, caracteres especiais, ou começar com um número.|  
|0xC00291BE|-1073573442|DTS_E_SCRIPTTASK_INVALID_SCRIPT_LANGUAGE|A linguagem de script especificada não é válida.|  
|0xC00291BF|-1073573441|DTS_E_SCRIPTTASK_INVALID_ENTRY_POINT|Ponto de entrada não encontrado.|  
|0xC00291C0|-1073573440|DTS_E_SCRIPTTASK_LANGUAGE_EMPTY|A linguagem de script não está especificada. Verifique se foi especificada uma linguagem de script válida.|  
|0xC00291C1|-1073573439|DTS_E_SCRIPTTASK_INITIALIZATION_WITH_NULL_TASK|Inicialização da interface de usuário: A tarefa é nula.|  
|0xC00291C2|-1073573438|DTS_E_SCRIPTTASK_UI_INITIALIZATION_WITH_WRONG_TASK|A interface do usuário de Tarefa Script foi inicializada com uma tarefa incorreta.|  
|0xC00291C3|-1073573437|DTS_E_SENDMAILTASK_RECIPIENT_EMPTY|Nenhum destinatário foi especificado.|  
|0xC00291C4|-1073573436|DTS_E_SENDMAILTASK_SMTP_SERVER_NOT_SPECIFIED|O servidor SMTP (Simple Mail Transfer Protocol) não está especificado. Forneça um nome ou endereço IP válido do servidor SMTP.|  
|0xC00291C5|-1073573435|DTS_E_SENDMAILTASK_TASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|A tarefa Enviar Email foi iniciada com um elemento XML incorreto.|  
|0xC00291CB|-1073573429|DTS_E_SENDMAILTASK_INVALIDATTACHMENT|O arquivo "%1" não existe ou você não tem permissões para acessar o arquivo.|  
|0xC00291CD|-1073573427|DTS_E_SENDMAILTASK_CHECK_VALID_SMTP_SERVER|Verifique se o servidor SMTP especificado é válido.|  
|0xC00291CE|-1073573426|DTS_E_SENDMAILTASK_CONNECTIONTYPENOTFILE|A conexão "%1" não é do tipo Arquivo.|  
|0xC00291CF|-1073573425|DTS_E_SENDMAILTASK_FILEDOESNOTEXIST|Na operação "%1", o arquivo "%2" não existe.|  
|0xC00291D0|-1073573424|DTS_E_SENDMAILTASK_VARIABLETYPEISNOTSTRING|A variável "%1" não é do tipo cadeia de caracteres.|  
|0xC00291D1|-1073573423|DTS_E_SENDMAILTASK_CONNECTIONTYPENOTSMTP|A conexão "%1" não é do tipo SMTP.|  
|0xC00291D2|-1073573422|DTS_E_SENDMAILTASK_CONNMNGRNULL|A conexão "%1" está vazia.|  
|0xC00291D3|-1073573421|DTS_E_SENDMAILTASK_NOCONNMNGR|A conexão "%1" especificada não existe.|  
|0xC00291D4|-1073573420|DTS_E_SQLTASK_NOSTATEMENTSPECIFIED|Nenhuma instrução Transact-SQL especificada.|  
|0xC00291D5|-1073573419|DTS_E_SQLTASK_NOXMLSUPPORT|A conexão não dá suporte a conjuntos de resultados do XML.|  
|0xC00291D6|-1073573418|DTS_E_SQLTASK_NOHANDLERFORCONNECTION|Não é possível localizar um manipulador para o tipo de conexão especificado.|  
|0xC00291D7|-1073573417|DTS_E_SQLTASK_NOCONNECTIONMANAGER|Nenhum gerenciador de conexões está especificado.|  
|0xC00291D8|-1073573416|DTS_E_SQLTASK_CANNOTACQUIRECONNMANAGER|Não é possível adquirir uma conexão do gerenciador de conexões.|  
|0xC00291D9|-1073573415|DTS_E_SQLTASK_NULLPARAMETERNAME|Não pode ter um nome de parâmetro nulo.|  
|0xC00291DA|-1073573414|DTS_E_SQLTASK_INVALIDPARAMETERNAME|O nome do parâmetro não é válido.|  
|0xC00291DB|-1073573413|DTS_E_SQLTASK_VALIDPARAMETERTYPES|Nomes de parâmetro válidos são do tipo Int ou String.|  
|0xC00291DC|-1073573412|DTS_E_SQLTASK_READONLYVARIABLE|A variável "%1" não pode ser usada em associação de resultados porque é somente leitura.|  
|0xC00291DD|-1073573411|DTS_E_SQLTASK_INDESNOTINCOLLECTION|O índice não está atribuído nessa coleção.|  
|0xC00291DE|-1073573410|DTS_E_SQLTASK_ROVARINOUTPARAMETER|A variável "%1" não pode ser usada como parâmetro "out" ou valor de retorno em uma associação de parâmetros porque é somente de leitura.|  
|0xC00291DF|-1073573409|DTS_E_SQLTASK_OBJECTNOTINCOLLECTION|O objeto não existe nessa coleção.|  
|0xC00291E0|-1073573408|DTS_E_SQLTASK_UNABLETOACQUIREMANAGEDCONN|Não é possível adquirir uma conexão gerenciada.|  
|0xC00291E1|-1073573407|DTS_E_UNABLETOPOPRESULT|Não é possível popular as colunas de resultado para um tipo de resultado de linha única. A consulta retornou um conjunto de resultados vazio.|  
|0xC00291E2|-1073573406|DTS_E_SQLTASK_INVALIDNUMOFRESULTBINDINGS|Existe um número inválido de associações de resultado retornadas para ResultSetType: "%1".|  
|0xC00291E3|-1073573405|DTS_E_SQLTASK_RESULTBINDTYPEFORROWSETXML|O nome da associação de resultados deve ser definida como 0 (zero) para o conjunto inteiro de resultados e para resultados XML.|  
|0xC00291E4|-1073573404|DTS_E_SQLTASK_INVALIDEPARAMDIRECTIONFALG|O sinalizador de direções de parâmetro não é válido.|  
|0xC00291E5|-1073573403|DTS_E_SQLTASK_NOSQLTASKDATAINXMLFRAGMENT|O fragmento XML não contém dados de Tarefa SQL.|  
|0xC00291E6|-1073573402|DTS_E_SQLTASK_MULTIPLERETURNVALUEPARAM|Um parâmetro com valor de retorno de tipo não é o primeiro parâmetro ou existe mais de um parâmetro de valor de retorno de tipo.|  
|0xC00291E7|-1073573401|DTS_E_SQLTASK_CONNECTIONTYPENOTFILE|A conexão "%1" não é um gerenciador de conexões de arquivo.|  
|0xC00291E8|-1073573400|DTS_E_SQLTASK_FILEDOESNOTEXIST|O arquivo representado por "%1" não existe.|  
|0xC00291E9|-1073573399|DTS_E_SQLTASK_VARIABLETYPEISNOTSTRING|O tipo de variável "%1" não é uma cadeia de caracteres.|  
|0xC00291EA|-1073573398|DTS_E_SQLTASK_VARIABLENOTFOUND|A variável "%1" não existe ou não pôde ser bloqueada.|  
|0xC00291EB|-1073573397|DTS_E_SQLTASK_CANNOTLOCATECONNMANAGER|O gerenciador de conexões "%1" não existe.|  
|0xC00291EC|-1073573396|DTS_E_SQLTASK_FAILEDTOACQUIRECONNECTION|Falha na aquisição da conexão "%1". A conexão pode não estar configurada corretamente ou você pode não ter as permissões certas nessa conexão.|  
|0xC00291ED|-1073573395|DTS_E_SQLTASK_RESULTBYNAMENOTSUPPORTED|Não existe suporte para a associação de resultados de nome "%1" para esse tipo de conexão.|  
|0xC00291EE|-1073573394|DTS_E_SQLTASKCONN_ERR_NO_ROWS|Foi especificado um tipo de conjunto de resultados de linha única, mas nenhuma linha foi retornada.|  
|0xC00291EF|-1073573393|DTS_E_SQLTASKCONN_ERR_NO_DISCONNECTED_RS|Não existe nenhum conjunto de registros desconectados disponível para a instrução Transact-SQL.|  
|0xC00291F0|-1073573392|DTS_E_SQLTASKCONN_ERR_UNSUPPORTED_TYPE|Tipo sem-suporte.|  
|0xC00291F1|-1073573391|DTS_E_SQLTASKCONN_ERR_UNKNOWN_TYPE|Tipo desconhecido.|  
|0xC00291F2|-1073573390|DTS_E_SQLTASKCONN_ERR_PARAM_DATA_TYPE|Tipo de dados sem suporte na associação de parâmetro \\"%s\\".|  
|0xC00291F3|-1073573389|DTS_E_SQLTASKCONN_ERR_PARAM_NAME_MIX|O nomes de parâmetro não podem ser uma mistura de tipos ordinais e nomeados.|  
|0xC00291F4|-1073573388|DTS_E_SQLTASKCONN_ERR_PARAM_DIR|A direção do parâmetro na associação de parâmetro \\"%s\\"não é válida.|  
|0xC00291F5|-1073573387|DTS_E_SQLTASKCONN_ERR_RESULT_DATA_TYPE|Não há suporte para o tipo de dados na associação do conjunto de resultados \\"%s\\".|  
|0xC00291F6|-1073573386|DTS_E_SQLTASKCONN_ERR_RESULT_COL_INDEX|O índice da coluna de resultados %d não é válido.|  
|0xC00291F7|-1073573385|DTS_E_SQLTASKCONN_ERR_UNKNOWN_RESULT_COL|Não é possível encontrar a coluna \\"%s\\" no conjunto de resultados.|  
|0xC00291F9|-1073573383|DTS_E_SQLTASKCONN_ERR_NOROWSET|Nenhum conjunto de linhas de resultado está associado à execução dessa consulta.|  
|0xC00291FA|-1073573382|DTS_E_SQLTASKCONN_ERR_ODBC_DISCONNECTED|Não existem conjuntos de registros desconectados disponíveis das conexões ODBC.|  
|0xC00291FB|-1073573381|DTS_E_SQLTASKCONN_ERR_RESULT_SET_DATA_TYPE|Não há suporte para o tipo de dados no conjunto de resultados, coluna %hd.|  
|0xC00291FC|-1073573380|DTS_E_SQLTASKCONN_ERR_CANT_LOAD_XML|Não é possível carregar o XML com o resultado da consulta.|  
|0xC00291FD|-1073573379|DTS_E_TTGENTASK_NOCONNORVARIABLE|É necessário especificar um nome de conexão ou nome de variável para o pacote.|  
|0xC00291FE|-1073573378|DTS_E_TTGENTASK_FAILEDCREATE|Falha na criação do pacote.|  
|0xC00291FF|-1073573377|DTS_E_TTGENTASK_BADTABLEMETADATA|O TableMetaDataNode não é um XMLNode.|  
|0xC0029200|-1073573376|DTS_E_TTGENTASK_FAILEDCREATEPIPELINE|Falha na criação do pipeline.|  
|0xC0029201|-1073573375|DTS_E_TTGENTASK_BADVARIABLETYPE|O variável não é do tipo correto.|  
|0xC0029202|-1073573374|DTS_E_TTGENTASK_NOTFILECONNECTION|O gerenciador de conexões especificado não é um gerenciador de conexões FILE.|  
|0xC0029203|-1073573373|DTS_E_TTGENTASK_BADFILENAME|Nome de arquivo inválido especificado no gerenciador de conexões "%1".|  
|0xC0029204|-1073573372|DTS_E_WEBSERVICETASK_CONNECTION_NAME_NULL|A conexão está vazia. Verifique se foi especificada uma conexão HTTP válida.|  
|0xC0029205|-1073573371|DTS_E_WEBSERVICETASK_CONNECTION_NOT_FOUND|A conexão não existe. Verifique se existe uma conexão HTTP válida especificada.|  
|0xC0029206|-1073573370|DTS_E_WEBSERVICETASK_CONNECTION_NOT_HTTP|A conexão especificada não é uma conexão HTTP. Verifique se foi especificada uma conexão HTTP válida.|  
|0xC0029207|-1073573369|DTS_E_WEBSERVICETASK_SERVICE_NULL|O nome do Serviço Web está vazio. Verifique se foi especificado um nome válido de serviço Web.|  
|0xC0029208|-1073573368|DTS_E_WEBSERVICETASK_METHODNAME_NULL|O nome do método Web está vazio. Verifique se foi especificado um método Web válido.|  
|0xC0029209|-1073573367|DTS_E_WEBSERVICETASK_WEBMETHODINFO_NULL|O método Web está vazio ou não existe. Verifique se existe um método Web para especificar.|  
|0xC002920A|-1073573366|DTS_E_WEBSERVICETASK_OUTPUTLOC_NULL|O local de saída está vazio. Verifique se foi especificada uma variável ou conexão de arquivo existente.|  
|0xC002920B|-1073573365|DTS_E_WEBSERVICETASK_VARIABLE_NOT_FOUND|A variável não pode ser encontrada. Verifique se a variável existe no pacote.|  
|0xC002920C|-1073573364|DTS_E_WEBSERVICETASK_VARIABLE_READONLY|Não é possível salvar o resultado. Verifique se a variável não é somente leitura.|  
|0xC002920D|-1073573363|DTS_E_WEBSERVICETASK_ERROR_IN_LOAD_FROM_XML|Erro em LoadFromXML na marca "%1".|  
|0xC002920E|-1073573362|DTS_E_WEBSERVICETASK_ERROR_IN_SAVE_TO_XML|Erro em SaveToXML na marca "%1".|  
|0xC002920F|-1073573361|DTS_E_WEBSERVICETASK_TASK_SAVE_TO_NULL_XML_ELEMENT|Não é possível salvar a tarefa em um documento XML nulo.|  
|0xC0029210|-1073573360|DTS_E_WEBSERVICETASK_TASK_INITIALIZATION_WITH_NULL_XML_ELEMENT|Não é possível inicializar a tarefa com um elemento XML nulo.|  
|0xC0029211|-1073573359|DTS_E_WEBSERVICETASK_TASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|A Tarefa Serviço Web foi iniciada com um elemento XML incorreto.|  
|0xC0029212|-1073573358|DTS_E_WEBSERVICETASK_UNEXPECTED_XML_ELEMENT|Foi encontrado um elemento XML inesperado.|  
|0xC0029213|-1073573357|DTS_E_WEBSERVICETASK_CANNOT_ACQUIRE_CONNECTION|Houve um erro ao adquirir a conexão HTTP. Verifique se foi especificado um tipo de conexão válido.|  
|0xC0029214|-1073573356|DTS_E_WEBSERVICETASK_FILE_CONN_NOT_FOUND|Não é possível salvar o resultado. Verifique se há uma conexão de arquivo existente.|  
|0xC0029215|-1073573355|DTS_E_WEBSERVICETASK_FILE_NOT_FOUND|Não é possível salvar o resultado. Verifique se o arquivo existe.|  
|0xC0029216|-1073573354|DTS_E_WEBSERVICETASK_FILE_NULL|Não é possível salvar o resultado. O nome do arquivo está vazio ou o arquivo está sendo usado por outro processo.|  
|0xC0029217|-1073573353|DTS_E_WEBSERVICETASK_CANNOT_ACQUIRE_FILE_CONNECTION|Houve um erro na aquisição da conexão de arquivo. Verifique se foi especificada uma conexão de arquivo válida.|  
|0xC0029218|-1073573352|DTS_E_WEBSERVICETASK_DATATYPE_NOT_SUPPORTED|Existe suporte apenas para Tipos Complexos com valores Primitivos, Matrizes Primitivas e Enumerações.|  
|0xC0029219|-1073573351|DTS_E_WEBSERVICETASK_PARAMTYPE_NOT_SUPPORTED|Existe suporte apenas para tipos Primitive, Enum, Complex, PrimitiveArray e ComplexArray.|  
|0xC002921A|-1073573350|DTS_E_WEBSERVICETASK_WSDL_VERSION_NOT_SUPPORTED|Não existe suporte para essa versão do WSDL.|  
|0xC002921B|-1073573349|DTS_E_WEBSERVICETASK_WRONG_XML_ELEMENT|Inicializado com um elemento XML incorreto.|  
|0xC002921C|-1073573348|DTS_E_WEBSERVICETASK_XML_ATTRIBUTE_NOT_FOUND|Não foi encontrado um atributo obrigatório.|  
|0xC002921D|-1073573347|DTS_E_WEBSERVICETASK_ENUM_NO_VALUES|O enum "%1" não tem nenhum valor. O WSDL está corrompido.|  
|0xC002921E|-1073573346|DTS_E_WEBSERVICETASK_CONNECTIONNOTFOUND|Não foi possível encontrar a conexão.|  
|0xC002921F|-1073573345|DTS_E_WEBSERVICETASK_CONNECTION_ALREADY_EXISTS|A conexão por esse nome já existe.|  
|0xC0029220|-1073573344|DTS_E_WEBSERVICETASK_NULL_CONNECTION|A conexão não pode ser nula ou vazia.|  
|0xC0029221|-1073573343|DTS_E_WEBSERVICETASK_NOT_HTTP_CONNECTION|A conexão especificada não é uma conexão HTTP. Verifique se foi especificada uma conexão HTTP válida.|  
|0xC0029222|-1073573342|DTS_E_WEBSERVICETASK_WSDL_NOT_FOUND|O URI (Uniform Resource Identifier) não contém um WSDL válido.|  
|0xC0029223|-1073573341|DTS_E_WEBSERVICETASK_ERROR_IN_DOWNLOAD|Não foi possível ler o arquivo WSDL. O arquivo WSDL de entrada não é válido. O leitor emitiu o erro a seguir: "%1".|  
|0xC0029224|-1073573340|DTS_E_WEBSERVICETASK_SERVICE_DESC_NULL|A Descrição do Serviço não pode ser nula.|  
|0xC0029225|-1073573339|DTS_E_WEBSERVICETASK_SERVICENULL|O nome do serviço não pode ser nulo.|  
|0xC0029226|-1073573338|DTS_E_WEBSERVICETASK_WSDL_NULL|A URL não pode ser nula.|  
|0xC0029227|-1073573337|DTS_E_WEBSERVICETASK_SERVICE_NOT_FOUND|O serviço não está atualmente disponível.|  
|0xC0029228|-1073573336|DTS_E_WEBSERVICETASK_SOAPPORT_NOT_FOUND|O serviço não está disponível na porta SOAP.|  
|0xC0029229|-1073573335|DTS_E_WEBSERVICETASK_SOAPBINDING_NOT_FOUND|Falha ao analisar WSDL (Web Services Description Language). Não é possível encontrar a Associação correspondente à porta SOAP.|  
|0xC002922A|-1073573334|DTS_E_WEBSERVICETASK_SOAPPORTTYPE_NOT_FOUND|Falha ao analisar WSDL (Web Services Description Language). Não é possível encontrar um PortType correspondente à porta SOAP.|  
|0xC002922B|-1073573333|DTS_E_WEBSERVICETASK_MSG_NOT_FOUND|Não é possível encontrar a mensagem correspondente ao método especificado.|  
|0xC002922C|-1073573332|DTS_E_WEBSERVICETASK_CANNOT_GEN_PROXY|Não foi possível gerar o proxy para o serviço Web determinado. Os erros a seguir foram encontrados durante a geração do proxy "%1".|  
|0xC002922D|-1073573331|DTS_E_WEBSERVICETASK_CANNOT_LOAD_PROXY|Não foi possível carregar o proxy para o serviço Web determinado. O erro exato é o seguinte: "%1".|  
|0xC002922E|-1073573330|DTS_E_WEBSERVICETASK_INVALID_SERVICE|Não foi possível encontrar o serviço especificado. O erro exato é o seguinte: "%1".|  
|0xC002922F|-1073573329|DTS_E_WEBSERVICETASK_WEBMETHOD_INVOKE_FAILED|O Serviço Web emitiu o seguinte erro durante a execução do método: "%1".|  
|0xC0029230|-1073573328|DTS_E_WEBSERVICETASK_INVOKE_ERR|Não foi possível executar o método Web. O erro exato é o seguinte: "%1".|  
|0xC0029231|-1073573327|DTS_E_WEBSERVICETASK_METHODINFO_NULL|MethodInfo não pode ser nulo.|  
|0xC0029232|-1073573326|DTS_E_WEBSERVICETASK_VALUE_NOT_PRIMITIVE|O WebMethodInfo especificado não está correto. O ParamValue fornecido não corresponde ao ParamType. O DTSParamValue não é do tipo PrimitiveValue.|  
|0xC0029233|-1073573325|DTS_E_WEBSERVICETASK_VALUE_NOT_ENUM|O WebMethodInfo especificado não está correto. O ParamValue fornecido não corresponde ao ParamType. O DTSParamValue encontrado não é do tipo EnumValue.|  
|0xC0029234|-1073573324|DTS_E_VALUE_WEBSERVICETASK_NOT_COMPLEX|O WebMethodInfo especificado não está correto. O ParamValue fornecido não corresponde ao ParamType. O DTSParamValue encontrado não é do tipo ComplexValue.|  
|0xC0029235|-1073573323|DTS_E_WEBSERVICETASK_VALUE_NOT_ARRAY|O WebMethodInfo especificado não está correto. O ParamValue fornecido não corresponde ao ParamType. O DTSParamValue encontrado não é do tipo ArrayValue.|  
|0xC0029236|-1073573322|DTS_E_WEBSERVICETASK_TYPE_NOT_PRIMITIVE|O WebMethodInfo especificado está errado. "%1" não é do Tipo Primitivo.|  
|0xC0029237|-1073573321|DTS_E_WEBSERVICETASK_ARRAY_VALUE_INVALID|O formato do ArrayValue não é válido. Deve haver no mínimo um elemento na matriz.|  
|0xC0029238|-1073573320|DTS_E_WEBSERVICETASK_SELECTED_VALUE_NULL|O valor da enumeração não pode ser nulo. Selecione um valor padrão para a enumeração.|  
|0xC0029239|-1073573319|DTS_E_WEBSERVICETASK_NULL_VALUE|Não é possível validar um valor nulo em relação a nenhum tipo de dados.|  
|0xC002923A|-1073573318|DTS_E_WEBSERVICETASK_ENUM_VALUE_NOT_FOUND|O Valor de enumeração não está correto.|  
|0xC002923B|-1073573317|DTS_E_WEBSERVICETASK_PROP_NOT_EXISTS|A classe especificada não contém uma propriedade pública de nome "%1".|  
|0xC002923C|-1073573316|DTS_E_WEBSERVICETASK_CONVERT_FAILED|Não foi possível converter "%1" em "%2".|  
|0xC002923D|-1073573315|DTS_E_WEBSERVICETASK_CLEANUP_FAILED|Falha na limpeza. O proxy criado para o serviço Web pode não ter sido excluído.|  
|0xC002923E|-1073573314|DTS_E_WEBSERVICETASK_CREATE_INSTANCE_FAILED|Não foi possível criar um objeto do tipo "%1". Verifique se existe o construtor padrão.|  
|0xC002923F|-1073573313|DTS_E_WEBSERVICETASK_NOT_PRIMITIVE_TYPE|"%1" não é um tipo de valor.|  
|0xC0029240|-1073573312|DTS_E_WEBSERVICETASK_ERROR_IN_VALIDATE|Não foi possível validar "%1" em relação a "%1".|  
|0xC0029241|-1073573311|DTS_E_WEBSERVICETASK_DATATYPE_NULL|O tipo de dados não pode ser nulo. Especifique o valor do tipo de dados a ser validado.|  
|0xC0029242|-1073573310|DTS_E_WEBSERVICETASK_INDEX_OUT_OF_BOUNDS|O ParamValue não pode ser inserido nessa posição. O índice especificado pode ser menor que zero ou maior que o comprimento.|  
|0xC0029243|-1073573309|DTS_E_WEBSERVICETASK_WRONG_WSDL|O arquivo WSDL de entrada não é válido.|  
|0xC0029244|-1073573308|DTS_E_WMIDRTASK_SYNCOBJECTFAILED|Falha no objeto de sincronização.|  
|0xC0029245|-1073573307|DTS_E_WMIDRTASK_MISSINGWQLQUERY|Está faltando a consulta WQL.|  
|0xC0029246|-1073573306|DTS_E_WMIDRTASK_DESTINATIONMUSTBESET|O destino deve estar definido.|  
|0xC0029247|-1073573305|DTS_E_WMIDRTASK_MISSINGCONNECTION|Não existe nenhuma conexão WMI definida.|  
|0xC0029248|-1073573304|DTS_E_WMIDRTASK_INVALIDDATANODE|A Tarefa Leitor de Dados do WMI recebeu um nó de dados de tarefa inválido.|  
|0xC0029249|-1073573303|DTS_E_WMIDRTASK_FAILEDVALIDATION|Houve falha na tarefa de validação.|  
|0xC002924A|-1073573302|DTS_E_WMIDRTASK_FILEDOESNOTEXIST|O arquivo "%1" não existe.|  
|0xC002924B|-1073573301|DTS_E_WMIDRTASK_CONNECTIONMNGRDOESNTEXIST|O gerenciador de conexões "%1" não existe.|  
|0xC002924C|-1073573300|DTS_E_WMIDRTASK_VARIABLETYPEISNOTSTRINGOROBJECT|A variável "%1" não é do tipo cadeia de caracteres ou objeto.|  
|0xC002924D|-1073573299|DTS_E_WMIDRTASK_CONNECTIONTYPENOTFILE|A conexão "%1" não é do tipo "FILE".|  
|0xC002924E|-1073573298|DTS_E_WMIDRTASK_CONNECTIONTYPENOTWMI|A conexão "%1" não é do tipo "WMI".|  
|0xC002924F|-1073573297|DTS_E_WMIDRTASK_FILEALREADYEXISTS|O arquivo "%1" já existe.|  
|0xC0029250|-1073573296|DTS_E_WMIDRTASK_CONNECTIONMANAGEREMPTY|O gerenciador de conexões "%1" está vazio.|  
|0xC0029251|-1073573295|DTS_E_WMIDRTASK_VARNOTOBJECT|A variável "%1" deve ser do tipo objeto a ser atribuído a uma tabela de dados.|  
|0xC0029252|-1073573294|DTS_E_WMIDRTASK_TASKFAILURE|Falha na tarefa por causa de uma consulta WMI inválida: "%1".|  
|0xC0029253|-1073573293|DTS_E_WMIDRTASK_CANTWRITETOVAR|Não foi possível gravar na variável "%1" porque está definida para manter seu valor original.|  
|0xC0029254|-1073573292|DTS_E_WMIEWTASK_SYNCOBJECTFAILED|Falha no objeto de sincronização.|  
|0xC0029255|-1073573291|DTS_E_WMIEWTASK_MISSINGWQLQUERY|Está faltando a consulta WQL.|  
|0xC0029256|-1073573290|DTS_E_WMIEWTASK_MISSINGCONNECTION|Está faltando a conexão WMI.|  
|0xC0029257|-1073573289|DTS_E_WMIEWTASK_QUERYFAILURE|A tarefa não executou a consulta WMI.|  
|0xC0029258|-1073573288|DTS_E_WMIEWTASK_INVALIDDATANODE|A Tarefa Detector de Eventos do WMI recebeu um nó de dados de tarefa que não é válido.|  
|0xC0029259|-1073573287|DTS_E_WMIEWTASK_CONNECTIONMNGRDOESNTEXIST|O gerenciador de conexões "%1" não existe.|  
|0xC002925A|-1073573286|DTS_E_WMIEWTASK_FILEDOESNOTEXIST|O arquivo "%1" não existe.|  
|0xC002925B|-1073573285|DTS_E_WMIEWTASK_VARIABLETYPEISNOTSTRING|A variável "%1" não é do tipo cadeia de caracteres.|  
|0xC002925C|-1073573284|DTS_E_WMIEWTASK_CONNECTIONTYPENOTFILE|A conexão "%1" não é do tipo "FILE".|  
|0xC002925D|-1073573283|DTS_E_WMIEWTASK_CONNECTIONTYPENOTWMI|A conexão "%1" não é do tipo "WMI".|  
|0xC002925E|-1073573282|DTS_E_WMIEWTASK_FILEALREADYEXISTS|O arquivo "%1" já existe.|  
|0xC002925F|-1073573281|DTS_E_WMIEWTASK_CONNECTIONMANAGEREMPTY|O gerenciador de conexões "%1" está vazio.|  
|0xC0029260|-1073573280|DTS_E_WMIEWTASK_TIMEOUTOCCURRED|O tempo limite de "%1" segundo(s) ocorreu antes do evento representado por "%2".|  
|0xC0029261|-1073573279|DTS_E_WMIEWTASK_ERRMESSAGE|A observação da consulta Wql provocou a seguinte exceção de sistema: "%1". Verifique os erros na consulta ou os direitos/permissões de acesso na conexão WMI.|  
|0xC0029262|-1073573278|DTS_E_XMLTASK_NODEFAULTOPERTION|As Operações especificadas não estão definidas.|  
|0xC0029263|-1073573277|DTS_E_XMLTASK_CONNECTIONTYPENOTFILE|O tipo de conexão não é Arquivo.|  
|0xC0029264|-1073573276|DTS_E_XMLTASK_CANTGETREADERFROMSOURCE|Não é possível obter um XmlReader do documento XML de origem.|  
|0xC0029265|-1073573275|DTS_E_XMLTASK_CANTGETREADERFROMDEST|Não é possível obter um XmlReader do documento XML alterado.|  
|0xC0029266|-1073573274|DTS_E_XMLTASK_CANTGETREADERFROMDIFFGRAM|Não é possível obter o leitor de diffgram XDL do XML do diffgram XDL.|  
|0xC0029268|-1073573272|DTS_E_XMLTASK_EMPTYNODELIST|A lista de nós está vazia.|  
|0xC0029269|-1073573271|DTS_E_XMLTASK_NOELEMENTFOUND|O elemento não foi encontrado.|  
|0xC002926A|-1073573270|DTS_E_XMLTASK_UNDEFINEDOPERATION|As Operações especificadas não estão definidas.|  
|0xC002926B|-1073573269|DTS_E_XMLTASK_XPATHNAVERROR|Item de conteúdo inesperado em XPathNavigator.|  
|0xC002926C|-1073573268|DTS_E_XMLTASK_NOSCHEMAFOUND|Não foi encontrado nenhum esquema para impor a validação.|  
|0xC002926D|-1073573267|DTS_E_XMLTASK_VALIDATIONERROR|Ocorreu um erro de validação ao validar o documento de instância.|  
|0xC002926E|-1073573266|DTS_E_XMLTASK_SYNCOBJECTFAILED|Falha no objeto de sincronização.|  
|0xC002926F|-1073573265|DTS_E_XMLTASK_ROOTNOODESNOTMATCHED|Os nós raiz não coincidem.|  
|0xC0029270|-1073573264|DTS_E_XMLTASK_INVALIDEDITSCRIPT|O tipo Operação Editar Script no Editar Script final não é válido.|  
|0xC0029271|-1073573263|DTS_E_XMLTASK_CDATANODESISSUE|Os nós CDATA devem ser adicionados com a classe DiffgramAddSubtrees.|  
|0xC0029272|-1073573262|DTS_E_XMLTASK_COMMENTSNODEISSUE|Os nós de comentários devem ser adicionados com a classe DiffgramAddSubtrees.|  
|0xC0029273|-1073573261|DTS_E_XMLTASK_TEXTNODEISSUES|Os nós de texto devem ser adicionados com a classe DiffgramAddSubtrees.|  
|0xC0029274|-1073573260|DTS_E_XMLTASK_WHITESPACEISSUE|Nós de espaços em branco significativos devem ser adicionados com a classe DiffgramAddSubtrees.|  
|0xC0029275|-1073573259|DTS_E_XMLTASK_DIFFENUMISSUE|Corrija a matriz OperationCost de forma a refletir a enumeração XmlDiffOperation.|  
|0xC0029276|-1073573258|DTS_E_XMLTASK_TASKISEMPTY|Não existe nenhuma operação na tarefa.|  
|0xC0029277|-1073573257|DTS_E_XMLTASK_DOCUMENTHASDATA|O documento já contém dados e não deve ser usado novamente.|  
|0xC0029278|-1073573256|DTS_E_XMLTASK_INVALIDENODETYPE|O tipo de nó não é válido.|  
|0xC0029279|-1073573255|DTS_E_XMLTASK_INVALIDDATANODE|A Tarefa XML recebeu um nó de dados de tarefa que não é válido.|  
|0xC002927B|-1073573253|DTS_E_XMLTASK_VARIABLETYPEISNOTSTRING|O tipo de dados da variável não é uma Cadeia de caracteres.|  
|0xC002927C|-1073573252|DTS_E_XMLTASK_COULDNOTGETENCODINGFROMDOCUMENT|Não é possível obter a codificação do XML.|  
|0xC002927D|-1073573251|DTS_E_XMLTASK_MISSINGSOURCE|A origem não está especificada.|  
|0xC002927E|-1073573250|DTS_E_XMLTASK_MISSINGSECONDOPERAND|O segundo operando não está especificado.|  
|0xC002927F|-1073573249|DTS_E_XMLTASK_INVALIDPATHDESCRIPTOR|Diffgram XDL inválido. "%1" é um descritor de caminho inválido.|  
|0xC0029280|-1073573248|DTS_E_XMLTASK_NOMATCHINGNODE|Diffgram XDL inválido. Nenhum nó corresponde ao descritor de caminho "%1".|  
|0xC0029281|-1073573247|DTS_E_XMLTASK_EXPECTINGDIFFGRAMELEMENT|Diffgram XDL inválido. Esperando xd:xmldiff como elemento raiz com URI de namespace "%1".|  
|0xC0029282|-1073573246|DTS_E_XMLTASK_MISSINGSRCDOCATTRIBUTE|O diffgram XDL não é válido. Está faltando o atributo srcDocHash no elemento xd:xmldiff.|  
|0xC0029283|-1073573245|DTS_E_XMLTASK_MISSINGOPTIONSATTRIBUTE|O diffgram XDL não é válido. Está faltando o atributo de opções no elemento xd:xmldiff.|  
|0xC0029284|-1073573244|DTS_E_XMLTASK_INVALIDSRCDOCATTRIBUTE|O diffgram XDL não é válido. O atributo srcDocHash tem um valor inválido.|  
|0xC0029285|-1073573243|DTS_E_XMLTASK_INVALIDOPTIONSATTRIBUTE|O diffgram XDL não é válido. O atributo de opções tem um valor inválido.|  
|0xC0029286|-1073573242|DTS_E_XMLTASK_SRCDOCMISMATCH|O diffgram XDL não é aplicável a esse documento XML. O valor rcDocHash não coincide.|  
|0xC0029287|-1073573241|DTS_E_XMLTASK_MORETHANONENODEMATCHED|Diffgram XDL inválido; mais de um nó corresponde ao descritor de caminho "%1" no elemento xd:node ou xd:change.|  
|0xC0029288|-1073573240|DTS_E_XMLTASK_XMLDECLMISMATCH|O diffgram XDL não é aplicável a esse documento XML. Uma declaração XML nova não pode ser adicionada.|  
|0xC0029289|-1073573239|DTS_E_XMLTASK_INTERNALERRORMORETHANONENODEINLIST|Erro Interno. XmlDiffPathSingleNodeList pode conter apenas um nó.|  
|0xC002928A|-1073573238|DTS_E_XMLTASK_INTERNALERRORMORETHANONENODELEFT|Erro Interno. "%1" nós restantes depois do patch, esperando 1.|  
|0xC002928B|-1073573237|DTS_E_XMLTASK_XSLTRESULTFILEISNOTXML|O Arquivo/Texto Produzido pelo XSLT não é um XmlDocument válido, portanto não pode ser definido como resultado da operação: "%1".|  
|0xC002928E|-1073573234|DTS_E_XMLTASK_FILEDOESNOTEXIST|Não existe nenhum arquivo associado à conexão "%1".|  
|0xC002928F|-1073573233|DTS_E_XMLTASK_XMLTEXTEMPTY|A propriedade "%1" não tem nenhum texto Xml de origem; o Texto Xml é uma cadeia de caracteres inválida, nula ou vazia.|  
|0xC0029290|-1073573232|DTS_E_XMLTASK_FILEALREADYEXISTS|O arquivo "%1" já existe.|  
|0xC0029293|-1073573229|DTS_E_TRANSFERTASKS_SRCCONNECTIONREQUIRED|É necessário especificar uma conexão de origem.|  
|0xC0029294|-1073573228|DTS_E_TRANSFERTASKS_DESTCONNECTIONREQUIRED|É necessário especificar uma conexão de destino.|  
|0xC0029295|-1073573227|DTS_E_TRANSFERTASKS_CONNECTIONNOTFOUND|Não foi possível encontrar a conexão "%1" no pacote.|  
|0xC0029296|-1073573226|DTS_E_TRANSFERTASKS_SERVERVERSIONNOTALLOWED|A conexão "%1" especifica uma instância do SQL Server com uma versão sem-suporte para transferência.  Há suporte apenas para as versões 7, 2000 e 2005.|  
|0xC0029297|-1073573225|DTS_E_TRANSFERTASKS_SRCSERVERLESSEQUALDESTSERVER|A conexão de origem "%1" deve especificar uma instância do SQL Server com uma versão inferior ou igual à conexão de destino "%2".|  
|0xC0029298|-1073573224|DTS_E_TRANSFERTASKS_SRCDBREQUIRED|É necessário especificar um banco de dados de origem.|  
|0xC0029299|-1073573223|DTS_E_TRANSFERTASKS_SRCDBMUSTEXIST|O banco de dados de origem "%1" deve existir no servidor de origem.|  
|0xC002929A|-1073573222|DTS_E_TRANSFERTASKS_DESTDBREQUIRED|É necessário especificar um banco de dados de destino.|  
|0xC002929B|-1073573221|DTS_E_TRANSFERTASKS_SRCDBANDDESTDBTHESAME|O banco de dados de origem e o banco de dados de destino não podem ser o mesmo.|  
|0xC002929C|-1073573220|DTS_E_TRANSFERDBTASK_FILENAMEREQUIRED|Nome de arquivo ausente nas informações do arquivo de transferência %1.|  
|0xC002929D|-1073573219|DTS_E_TRANSFERDBTASK_FOLDERREQUIRED|Parte da pasta ausente nas informações do arquivo de transferência %1.|  
|0xC002929E|-1073573218|DTS_E_TRANSFERTASKS_NETSHAREREQUIRED|Parte de compartilhamento de rede ausente nas informações do arquivo de transferência %1.|  
|0xC002929F|-1073573217|DTS_E_TRANSFERTASKS_FILELISTSCOUNTMISMATCH|O número de arquivos de transferência de origem e o número de arquivos de transferência de destino devem ser o mesmo.|  
|0xC00292A0|-1073573216|DTS_E_DOESNOTSUPPORTTRANSACTIONS|Não há suporte para inscrição em transações.|  
|0xC00292A1|-1073573215|DTS_E_TRANSFERDBTASK_OFFLINEERROR|Ocorreu a seguinte exceção durante uma transferência de banco de dados offline: %1.|  
|0xC00292A2|-1073573214|DTS_E_TRANSFERDBTASK_NETSHAREDOESNOTEXIST|Não foi possível encontrar o compartilhamento de rede "%1".|  
|0xC00292A3|-1073573213|DTS_E_TRANSFERDBTASK_NETSHARENOACCESS|Não foi possível acessar o compartilhamento de rede "%1".  O erro foi: %2.|  
|0xC00292A4|-1073573212|DTS_E_TRANSFERDBTASK_USERMUSTBEDBOORSYSADMIN|O usuário "%1" deve ser DBO ou sysadmin de "%2" para executar uma transferência de banco de dados online.|  
|0xC00292A5|-1073573211|DTS_E_TRANSFERDBTASK_USERMUSTBESYSADMIN|O usuário "%1" deve ser sysadmin em "%2" para executar uma transferência de banco de dados offline.|  
|0xC00292A6|-1073573210|DTS_E_TRANSFERDBTASK_FTCATALOGSOFFLINEYUKONONLY|Catálogos de texto completo podem ser incluídos apenas durante a execução de uma transferência de banco de dados offline entre dois servidores SQL Server 2005.|  
|0xC00292A7|-1073573209|DTS_E_TRANSFERDBTASK_NOOVERWRITEDB|O banco de dados "%1" já existe no servidor de destino "%2".|  
|0xC00292A8|-1073573208|DTS_E_TRANSFERDBTASK_MUSTHAVESOURCEFILES|É necessário especificar pelo menos um arquivo de origem.|  
|0xC00292A9|-1073573207|DTS_E_TRANSFERDBTASKS_SRCFILENOTFOUND|Não foi possível encontrar o arquivo "%1" no banco de dados de origem "%2".|  
|0xC00292B3|-1073573197|DTS_E_MSMQTASK_FIPS1402COMPLIANCE|A operação solicitada não é permitida em sistemas em conformidade com U.S. FIPS 140-2.|  
|0xC002F210|-1073548784|DTS_E_SQLTASK_ERROREXECUTINGTHEQUERY|Falha na execução da consulta "%1", com o erro a seguir: "%2". Possíveis razões da falha: problemas com a consulta, propriedade "ResultSet" não definida corretamente, parâmetros não definidos corretamente ou conexão não estabelecida corretamente.|  
|0xC002F300|-1073548544|DTS_E_TRANSFERSPTASK_ERRORREADINGSPNAMES|Erro ao ler os nomes de procedimento armazenado do arquivo xml.|  
|0xC002F301|-1073548543|DTS_E_TRANSFERSPTASK_INVALIDDATANODE|Nó de dados inválido para a tarefa Transferir Procedimento Armazenado.|  
|0xC002F302|-1073548542|DTS_E_TRANSFERTASKS_CONNECTIONTYPEISNOTSMOSERVER|A conexão "%1" não é do tipo "SMOServer".|  
|0xC002F303|-1073548541|DTS_E_TRANSFERSPTASK_EXECUTIONFAILED|Falha na execução com o seguinte erro: "%1".|  
|0xC002F304|-1073548540|DTS_E_ERROROCCURREDWITHFOLLOWINGMESSAGE|Erro com a seguinte mensagem: "%1".|  
|0xC002F305|-1073548539|DTS_E_BITASK_EXECUTION_FAILED|Falha na execução de inserção em massa.|  
|0xC002F306|-1073548538|DTS_E_FSTASK_INVALIDDESTPATH|Caminho de destino inválido.|  
|0xC002F307|-1073548537|DTS_E_FSTASK_CANTCREATEDIR|Não é possível criar diretório. O usuário optou por falhar a tarefa se o diretório existir.|  
|0xC002F308|-1073548536|DTS_E_SQLTASK_ODBCNOSUPPORTTRANSACTION|A tarefa tem uma opção de transação de "Obrigatória" e a conexão "%1" é do tipo "ODBC". As conexões ODBC não fornecem suporte a transações.|  
|0xC002F309|-1073548535|DTS_E_SQLTASK_ERRORASSIGINGVALUETOVAR|Erro durante a atribuição de um valor à variável "%1": "%2".|  
|0xC002F30A|-1073548534|DTS_E_FSTASK_SOURCEISEMPTY|A origem está vazia.|  
|0xC002F30B|-1073548533|DTS_E_FSTASK_DESTINATIONISEMPTY|O destino está vazio.|  
|0xC002F30C|-1073548532|DTS_E_FSTASK_FILEDIRNOTFOUND|O arquivo ou diretório "%1" não existe.|  
|0xC002F30D|-1073548531|DTS_E_FSTASK_VARSRCORDESTISEMPTY|A variável "%1" é usada como origem ou destino e está vazia.|  
|0xC002F30E|-1073548530|DTS_E_FSTASK_FILEDELETED|O arquivo ou diretório "%1" foi excluído.|  
|0xC002F30F|-1073548529|DTS_E_FSTASK_DIRECTORYDELETED|O diretório "%1" foi excluído.|  
|0xC002F310|-1073548528|DTS_E_WMIDRTASK_VARIABLETYPEISNOTOBJECT|A variável "%1" deve ser do tipo objeto a ser atribuído a uma tabela de dados.|  
|0xC002F311|-1073548527|DTS_E_WMIDRTASK_VARIABLETYPEISNOTSTRING|A variável "%1" não tem um tipo de dados de cadeia de caracteres.|  
|0xC002F312|-1073548526|DTS_E_FTPTASK_CANNOTACQUIRECONNECTION|Ocorreu um erro ao adquirir a conexão FTP. Verifique se foi especificado um tipo de conexão válido em "%1".|  
|0xC002F313|-1073548525|DTS_E_FTPTASK_CONNECTIONNOTFOUND|Não é possível encontrar o gerenciador de conexões FTP "%1".|  
|0xC002F314|-1073548524|DTS_E_FTPTASK_FILEUSAGETYPEERROR|O tipo de conexão "%1" de uso de arquivo deve ser "%2" para a operação "%3".|  
|0xC002F315|-1073548523|DTS_E_TRANSFERTASKS_SOURCECANTBESAMEASDESTINATION|O servidor de origem não pode ser o mesmo que o servidor de destino.|  
|0xC002F316|-1073548522|DTS_E_ERRMSGTASK_EMPTYSOURCELIST|Não existem Mensagens de Erro para serem transferidas.|  
|0xC002F317|-1073548521|DTS_E_ERRMSGTASK_DIFFERENTMESSAGEANDLANGUAGESIZES|As listas de mensagens de erro e suas linguagens correspondentes são de tamanhos diferentes.|  
|0xC002F318|-1073548520|DTS_E_ERRMSGTASK_ERRORMESSAGEOUTOFRANGE|A ID de mensagem de erro "%1" está fora do intervalo de mensagens de erro definidas pelo usuário. As ids de mensagem de erro definida pelo usuário ficam entre 50000 e 2147483647.|  
|0xC002F319|-1073548519|DTS_E_TRANSFERTASKS_NOTRANSACTIONSUPPORT|Essa tarefa não pode fazer parte de uma transação.|  
|0xC002F320|-1073548512|DTS_E_ERRMSGTASK_FAILEDTOTRANSFERERRORMESSAGES|Falha na transferência de algumas ou todas as Mensagens de Erro.|  
|0xC002F321|-1073548511|DTS_E_ERRMSGTASK_ERRORMESSAGEALREADYEXISTS|A mensagem de erro "%1" já existe no servidor de destino.|  
|0xC002F324|-1073548508|DTS_E_ERRMSGTASK_ERRORMESSAGECANTBEFOUND|Não é possível encontrar a mensagem de erro "%1" no servidor de origem.|  
|0xC002F325|-1073548507|DTS_E_TRANSFERTASKS_EXECUTIONFAILED|Falha na execução com o seguinte erro: "%1".|  
|0xC002F327|-1073548505|DTS_E_JOBSTASK_FAILEDTOTRANSFERJOBS|Falha na transferência do(s) Trabalho(s).|  
|0xC002F330|-1073548496|DTS_E_JOBSTASK_EMPTYSOURCELIST|Não existem Trabalhos para serem transferidos.|  
|0xC002F331|-1073548495|DTS_E_JOBSTASK_JOBEXISTSATDEST|O trabalho "%1" já existe no servidor de destino.|  
|0xC002F334|-1073548492|DTS_E_JOBSTASK_JOBCANTBEFOUND|Não é possível encontrar o trabalho "%1" no servidor de origem.|  
|0xC002F337|-1073548489|DTS_E_LOGINSTASK_EMPTYLIST|A lista de "Logins" a ser transferida está vazia.|  
|0xC002F338|-1073548488|DTS_E_LOGINSTASK_CANTGETLOGINSNAMELIST|Não é possível obter a lista de "Logins" do servidor de origem.|  
|0xC002F340|-1073548480|DTS_E_LOGINSTASK_ERRORLOGINEXISTS|O logon "%1" já existe no servidor de destino.|  
|0xC002F342|-1073548478|DTS_E_LOGINSTASK_LOGINNOTFOUND|O logon "%1" não existe na origem.|  
|0xC002F344|-1073548476|DTS_E_LOGINSTASK_FAILEDTOTRANSFERLOGINS|Falha na transferência de alguns ou todos os logons.|  
|0xC002F345|-1073548475|DTS_E_STOREDPROCSTASK_FAILEDTOTRANSFERSPS|Falha na transferência de procedimento(s) armazenado(s). Um erro mais informativo deve ter sido gerado.|  
|0xC002F346|-1073548474|DTS_E_STOREDPROCSTASK_STOREDPROCNOTFOUND|Não foi possível encontrar o Procedimento Armazenado "%1" na origem.|  
|0xC002F349|-1073548471|DTS_E_STOREDPROCSTASK_ERRORSTOREDPROCEDUREEXISTS|O procedimento armazenado "%1" já existe no servidor de destino.|  
|0xC002F350|-1073548464|DTS_E_STOREDPROCSTASK_EMPTYSOURCELIST|Não existem procedimentos armazenados para serem transferidos.|  
|0xC002F353|-1073548461|DTS_E_TRANSOBJECTSTASK_FAILEDTOTRANSFEROBJECTS|Falha na transferência do(s) objeto(s).|  
|0xC002F354|-1073548460|DTS_E_TRANSOBJECTSTASK_EMPTYLIST|A lista de "Objetos" a ser transferida está vazia.|  
|0xC002F355|-1073548459|DTS_E_TRANSOBJECTSTASK_NOSPATSOURCE|O procedimento armazenado "%1" não existe na origem.|  
|0xC002F356|-1073548458|DTS_E_TRANSOBJECTSTASK_SPALREADYATDEST|O procedimento armazenado "%1" já existe no destino.|  
|0xC002F357|-1073548457|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSPS|Erro durante a tentativa de definição da lista de Procedimentos Armazenados a ser transferida: "%1".|  
|0xC002F359|-1073548455|DTS_E_TRANSOBJECTSTASK_NORULEATSOURCE|A regra "%1" não existe na origem.|  
|0xC002F360|-1073548448|DTS_E_TRANSOBJECTSTASK_RULEALREADYATDEST|A regra "%1" já existe no destino.|  
|0xC002F361|-1073548447|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGRULES|Erro durante a tentativa de definição da lista de Regras a ser transferida: "%1".|  
|0xC002F363|-1073548445|DTS_E_TRANSOBJECTSTASK_NOTABLEATSOURCE|A tabela "%1" não existe na origem.|  
|0xC002F364|-1073548444|DTS_E_TRANSOBJECTSTASK_TABLEALREADYATDEST|A tabela "%1" já existe no destino.|  
|0xC002F365|-1073548443|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGTABLES|Erro durante a tentativa de definição da lista de Tabelas a ser transferida: "%1".|  
|0xC002F367|-1073548441|DTS_E_TRANSOBJECTSTASK_NOVIEWATSOURCE|A exibição "%1" não existe na origem.|  
|0xC002F368|-1073548440|DTS_E_TRANSOBJECTSTASK_VIEWALREADYATDEST|A exibição "%1" já existe no destino.|  
|0xC002F369|-1073548439|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGVIEWS|Erro durante a tentativa de definição da lista de Exibições a ser transferida: "%1".|  
|0xC002F371|-1073548431|DTS_E_TRANSOBJECTSTASK_NOUDFATSOURCE|A Função Definida pelo Usuário "%1" não existe na origem.|  
|0xC002F372|-1073548430|DTS_E_TRANSOBJECTSTASK_UDFALREADYATDEST|A Função Definida pelo Usuário "%1" já existe no destino.|  
|0xC002F373|-1073548429|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUDFS|Erro durante a tentativa de definição da lista de Funções Definidas pelo Usuário a ser transferida: "%1".|  
|0xC002F375|-1073548427|DTS_E_TRANSOBJECTSTASK_NODEFAULTATSOURCE|O padrão "%1" não existe na origem.|  
|0xC002F376|-1073548426|DTS_E_TRANSOBJECTSTASK_DEFAULTALREADYATDEST|O padrão "%1" já existe no destino.|  
|0xC002F377|-1073548425|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGDEFAULTS|Erro durante a tentativa de definição da lista de Padrões a ser transferida: "%1".|  
|0xC002F379|-1073548423|DTS_E_TRANSOBJECTSTASK_NOUDDTATSOURCE|O Tipo de Dados Definido pelo Usuário "%1" não existe na origem.|  
|0xC002F380|-1073548416|DTS_E_TRANSOBJECTSTASK_UDDTALREADYATDEST|O Tipo de Dados Definido pelo Usuário "%1" já existe no destino.|  
|0xC002F381|-1073548415|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUDDTS|Erro durante a tentativa de definição da lista de Tipos de Dados Definidos pelo Usuário a ser transferida: "%1".|  
|0xC002F383|-1073548413|DTS_E_TRANSOBJECTSTASK_NOPFATSOURCE|A Função de Partição "%1" não existe na origem.|  
|0xC002F384|-1073548412|DTS_E_TRANSOBJECTSTASK_PFALREADYATDEST|A Função de Partição "%1" já existe no destino.|  
|0xC002F385|-1073548411|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGPFS|Erro durante a tentativa de definição da lista de Funções de Partição a ser transferida: "%1".|  
|0xC002F387|-1073548409|DTS_E_TRANSOBJECTSTASK_NOPSATSOURCE|O Esquema de Partição "%1" não existe na origem.|  
|0xC002F388|-1073548408|DTS_E_TRANSOBJECTSTASK_PSALREADYATDEST|O Esquema de Partição "%1" já existe no destino.|  
|0xC002F389|-1073548407|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGPSS|Ocorreu um erro durante a tentativa de definição da lista de Esquemas de Partição a ser transferida: "%1".|  
|0xC002F391|-1073548399|DTS_E_TRANSOBJECTSTASK_NOSCHEMAATSOURCE|O Esquema "%1" não existe na origem.|  
|0xC002F392|-1073548398|DTS_E_TRANSOBJECTSTASK_SCHEMAALREADYATDEST|O Esquema "%1" já existe no destino.|  
|0xC002F393|-1073548397|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSCHEMAS|Erro durante a tentativa de definição da lista de Esquemas a ser transferida: "%1".|  
|0xC002F395|-1073548395|DTS_E_TRANSOBJECTSTASK_NOSQLASSEMBLYATSOURCE|O SqlAssembly "%1" não existe na origem.|  
|0xC002F396|-1073548394|DTS_E_TRANSOBJECTSTASK_SQLASSEMBLYALREADYATDEST|O SqlAssembly "%1" já existe no destino.|  
|0xC002F397|-1073548393|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSQLASSEMBLIES|Erro durante a tentativa de definição da lista de SqlAssemblies a ser transferida: "%1".|  
|0xC002F399|-1073548391|DTS_E_TRANSOBJECTSTASK_NOAGGREGATEATSOURCE|A Agregação Definida pelo Usuário "%1" não existe na origem.|  
|0xC002F400|-1073548288|DTS_E_TRANSOBJECTSTASK_AGGREGATEALREADYATDEST|A Agregação Definida pelo Usuário "%1" já existe no destino.|  
|0xC002F401|-1073548287|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGAGGREGATES|Erro durante a tentativa de definição da lista de Agregações Definidas pelo Usuário a ser transferida: "%1".|  
|0xC002F403|-1073548285|DTS_E_TRANSOBJECTSTASK_NOTYPEATSOURCE|O Tipo Definido pelo Usuário "%1" não existe na origem.|  
|0xC002F404|-1073548284|DTS_E_TRANSOBJECTSTASK_TYPEALREADYATDEST|O Tipo Definido pelo Usuário "%1" já existe no destino.|  
|0xC002F405|-1073548283|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGTYPES|Erro durante a tentativa de definição da lista de Tipos Definidos pelo Usuário a ser transferida: "%1".|  
|0xC002F407|-1073548281|DTS_E_TRANSOBJECTSTASK_NOXMLSCHEMACOLLECTIONATSOURCE|O XmlSchemaCollection "%1" não existe na origem.|  
|0xC002F408|-1073548280|DTS_E_TRANSOBJECTSTASK_XMLSCHEMACOLLECTIONALREADYATDEST|O XmlSchemaCollection "%1" já existe no destino.|  
|0xC002F409|-1073548279|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGXMLSCHEMACOLLECTIONS|Erro durante a tentativa de definição da lista de XmlSchemaCollections a ser transferida: "%1".|  
|0xC002F411|-1073548271|DTS_E_TRANSOBJECTSTASK_SUPPORTEDONYUKONONLY|Há suporte para objetos do tipo "%1" apenas entre servidores SQL Server 2005 ou servidores mais recentes.|  
|0xC002F413|-1073548269|DTS_E_LOGINSTASK_EMPTYDATABASELIST|A lista de bancos de dados está vazia.|  
|0xC002F414|-1073548268|DTS_E_TRANSOBJECTSTASK_NOLOGINATSOURCE|O logon "%1" não existe na origem.|  
|0xC002F416|-1073548266|DTS_E_TRANSOBJECTSTASK_LOGINALREADYATDEST|O logon "%1" já existe no destino.|  
|0xC002F417|-1073548265|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGLOGINS|Erro durante a tentativa de definição da lista de Logons a ser transferida: "%1".|  
|0xC002F419|-1073548263|DTS_E_TRANSOBJECTSTASK_NOUSERATSOURCE|O usuário "%1" não existe na origem.|  
|0xC002F41B|-1073548261|DTS_E_TRANSOBJECTSTASK_USERALREADYATDEST|O usuário "%1" já existe no destino.|  
|0xC002F41C|-1073548260|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUSERS|Erro durante a tentativa de definição da lista de Usuários a ser transferida: "%1".|  
|0xC002F41F|-1073548257|DTS_E_BITASK_CANNOTRETAINCONNINTRANSACTION|A tarefa não pode ter um gerenciador de conexões retido em uma transação.|  
|0xC002F421|-1073548255|DTS_E_SQLTASKOUTPUTENCODINGNOTSUPPORTED|Não é possível obter dados XML do SQL Server como Unicode porque o provedor não fornece suporte à propriedade OUTPUTENCODING.|  
|0xC002F426|-1073548250|DTS_E_FTPTASK_FILECONNECTIONNOTFOUND|Para a operação FTP "%1", não é possível encontrar o gerenciador de conexões FILE "%2".|  
|0xC002F428|-1073548248|DTS_E_TRANSOBJECTSTASK_CANNOTDROPOBJECTS|"Logons" são objetos no nível do servidor e não podem ser descartados primeiro porque a origem e o destino são o mesmo servidor. Se os objetos forem descartados primeiro os logons também serão removidos da origem.|  
|0xC002F429|-1073548247|DTS_E_SQLTASK_PARAMSIZEERROR|O parâmetro "%1" não pode ser negativo. Para o valor padrão, usa-se (-1).|  
|0xC0040019|-1073479655|DTS_E_UNREGISTEREDPIPELINEXML_LOAD|Não é possível carregar objetos Data Flow. Verifique se o Microsoft.SqlServer.PipelineXml.dll está corretamente registrado.|  
|0xC0040020|-1073479648|DTS_E_UNREGISTEREDPIPELINEXML_SAVE|Não é possível salvar objetos Data Flow. Verifique se o Microsoft.SqlServer.PipelineXml.dll está corretamente registrado.|  
|0xC0040040|-1073479616|DTS_E_PIPELINE_SAVE|Falha ao salvar objetos do Fluxo de Dados.|  
|0xC0040041|-1073479615|DTS_E_PIPELINE_LOAD|Falha ao carregar objetos do Fluxo de Dados|  
|0xC0040042|-1073479614|DTS_E_SAVE_PERSTFORMAT|Falha ao salvar objetos do Fluxo de Dados. Não há suporte ao formato especificado.|  
|0xC0040043|-1073479613|DTS_E_LOAD_PERSTFORMAT|Falha ao carregar objetos do Fluxo de Dados. Não há suporte ao formato especificado.|  
|0xC0040044|-1073479612|DTS_E_SETPERSIST_PROPEVENTS|Falha ao definir a propriedade de eventos de persistência XML para os objetos de Fluxo de Dados.|  
|0xC0040045|-1073479611|DTS_E_SETPERSIST_XMLDOM|Falha ao definir a propriedade DOM XML de persistência para os objetos de Fluxo de Dados.|  
|0xC0040046|-1073479610|DTS_E_SETPERSIST_XMLNODE|Falha ao definir a propriedade ELEMENT XML de persistência para os objetos de Fluxo de Dados.|  
|0xC0040047|-1073479609|DTS_E_SETPERSISTPROP_FAILED|Falha ao definir as propriedades de persistência XML para os objetos de Fluxo de Dados.|  
|0xC0040048|-1073479608|DTS_E_NOCUSTOMPROPCOL|Falha ao obter a coleção da propriedade personalizada para os componentes de Fluxo de Dados.|  
|0xC0047000|-1073451008|DTS_E_CYCLEINEXECUTIONTREE|Uma árvore de execução contém um ciclo.|  
|0xC0047001|-1073451007|DTS_E_DISCONNECTEDOBJECT|O objeto %1 "%2" (%3!d!) foi desconectado do layout.|  
|0xC0047002|-1073451006|DTS_E_INVALIDOBJECTID|A ID do objeto de layout não é válida.|  
|0xC0047003|-1073451005|DTS_E_INPUTWITHOUTPATHS|Um objeto de entrada necessário não está conectado a um objeto de caminho.|  
|0xC0047005|-1073451003|DTS_E_INVALIDSYNCHRONOUSINPUT|%1 tem uma identificação de entrada síncrona inválida %2!d!.|  
|0xC0047006|-1073451002|DTS_E_INVALIDOUTPUTLINEAGEID|%1 tem uma identificação de linhagem %2!d!, mas deveria ter %3!d!.|  
|0xC0047008|-1073451000|DTS_E_DUPLICATENAMESINCOLLECTION|O pacote contém dois objetos com nome duplicado de "%1" e "%2".|  
|0xC0047009|-1073450999|DTS_E_INVALIDEXCLUSIONGROUP|O "%1" e o "%2" estão no mesmo grupo de exclusão, mas eles não têm a mesma entrada síncrona.|  
|0xC004700A|-1073450998|DTS_E_DUPLICATELINEAGEIDSINCOLLECTION|Dois objetos na mesma coleção têm a identificação de linhagem duplicada %1!d!. Os objetos são %2 e %3.|  
|0xC004700B|-1073450997|DTS_E_VALIDATIONFAILEDONLAYOUT|Houve falha na validação do layout.|  
|0xC004700C|-1073450996|DTS_E_VALIDATIONFAILEDONCOMPONENTS|Houve falha na validação de um ou mais componentes.|  
|0xC004700D|-1073450995|DTS_E_VALIDATIONFAILED|Houve falha de validação no layout e em um ou mais componentes.|  
|0xC004700E|-1073450994|DTS_E_THREADSTARTUPFAILED|Houve falha na inicialização do mecanismo da tarefa Fluxo de Dados porque ele não pode criar um ou mais threads.|  
|0xC004700F|-1073450993|DTS_E_CANTGETMUTEX|Um thread não criou um mutex na inicialização.|  
|0xC0047010|-1073450992|DTS_E_CANTGETSEMAPHORE|Um thread não criou um semáforo na inicialização.|  
|0xC0047011|-1073450991|DTS_E_BUFFERFAILUREDETAILS|O sistema relata %1!d! porcentagem de carga de memória. Existem %2 bytes de memória física com %3 bytes livres. Existem %4 bytes de memória virtual com %5 bytes livres. O arquivo de paginação tem %6 bytes com %7 bytes livres.|  
|0xC0047012|-1073450990|DTS_E_BUFFERALLOCFAILED|Falha em um buffer durante a alocação de %1!d! bytes.|  
|0xC0047013|-1073450989|DTS_E_CANTCREATEBUFFERMANAGER|Não foi possível criar o Gerenciador de Buffer.|  
|0xC0047015|-1073450987|DTS_E_BUFFERBADSIZE|Tipo de buffer %1!d! tinha um tamanho de %2!I64d! bytes.|  
|0xC0047016|-1073450986|DTS_E_DANGLINGWITHPATH|%1 está marcado como pendente, mas tem um caminho anexado.|  
|0xC0047017|-1073450985|DTS_E_INDIVIDUALVALIDATIONFAILED|Falha na validação de %1 com o código de erro 0x%2!8.8X!.|  
|0xC0047018|-1073450984|DTS_E_INDIVIDUALPOSTEXECUTEFAILED|Falha de %1 na fase pós-execução com o código de erro 0x%2!8.8X!.|  
|0xC0047019|-1073450983|DTS_E_INDIVIDUALPREPAREFAILED|Falha de %1 na fase de preparação com o código de erro 0x%2!8.8X!.|  
|0xC004701A|-1073450982|DTS_E_INDIVIDUALPREEXECUTEFAILED|Falha de %1 na fase pré-execução com o código de erro 0x%2!8.8X!.|  
|0xC004701B|-1073450981|DTS_E_INDIVIDUALCLEANUPFAILED|Falha de %1 na fase de limpeza com o código de erro 0x%2!8.8X!.|  
|0xC004701C|-1073450980|DTS_E_INVALIDINPUTLINEAGEID|%1 tem identificação de linhagem %2!d! que não foi usada anteriormente na tarefa de Fluxo de Dados.|  
|0xC004701E|-1073450978|DTS_E_EXECUTIONTREECYCLE|Não é possível conectar %1 a %2 porque um ciclo seria criado.|  
|0xC004701F|-1073450977|DTS_E_CANTCOMPARE|Não é possível comparar o tipo de dados "%1". Não há suporte para comparação desse tipo de dados, assim ele não pode classificado ou usado como chave.|  
|0xC0047020|-1073450976|DTS_E_REFUSEDFORSHUTDOWN|Esse thread foi desligado e não está aceitando entrada de buffers.|  
|0xC0047021|-1073450975|DTS_E_THREADFAILED|Código de Erro SSIS DTS_E_THREADFAILED.  O Thread "%1" foi encerrado com o código de erro 0x%2!8.8X!.  Pode haver mensagens de erro geradas antes dessa, contendo mais informações justificando por que o thread foi encerrado.|  
|0xC0047022|-1073450974|DTS_E_PROCESSINPUTFAILED|Código de Erro SSIS DTS_E_PROCESSINPUTFAILED.  Falha do método ProcessInput no componente "%1" (%2!d!) com o código de erro 0x%3!8.8X! ao processar a entrada "%4 (%5!d!). O componente identificado retornou um erro do método ProcessInput. Esse erro é específico do componente, mas é fatal e fará com que a execução da tarefa de Fluxo de Dados seja interrompida.  Pode haver mensagens de erro geradas antes dessa, contendo mais informações sobre a falha.|  
|0xC0047023|-1073450973|DTS_E_CANTREALIZEVIRTUALBUFFERS|Não é possível realizar um conjunto de buffers virtuais.|  
|0xC0047024|-1073450972|DTS_E_PIPELINETOOCOMPLEX|O número de threads necessários para este pipeline é %1!d!, o que é mais do que o limite do sistema de %2!d!. O pipeline necessita de muitos threads como configurado. Há muitas saídas assíncronas ou a propriedade EngineThreads foi definida com um valor muito alto. Divida o pipeline em vários pacotes, ou reduza o valor da propriedade EngineThreads.|  
|0xC0047028|-1073450968|DTS_E_SCHEDULERCOULDNOTCOUNTSOURCES|O agendador do mecanismo de Fluxo de Dados não pode obter uma contagem das origens no layout.|  
|0xC0047029|-1073450967|DTS_E_SCHEDULERCOULDNOTCOUNTDESTINATIONS|O agendador do mecanismo de Fluxo de Dados não pode obter uma contagem dos destinos no layout.|  
|0xC004702A|-1073450966|DTS_E_COMPONENTVIEWISUNAVAILABLE|A exibição do componente está indisponível. Certifique-se de que a exibição do componente foi criada.|  
|0xC004702B|-1073450965|DTS_E_INCORRECTCOMPONENTVIEWID|A ID de exibição do componente está incorreta. A exibição do componente pode estar fora de sincronização. Tente liberar a exibição do componente e recriá-la.|  
|0xC004702C|-1073450964|DTS_E_BUFFERNOTLOCKED|Esse buffer não está bloqueado e não pode ser manipulado.|  
|0xC004702D|-1073450963|DTS_E_CANTBUILDBUFFERTYPE|A tarefa Fluxo de Dados não pode alocar memória para criar uma definição de buffer. A definição do buffer tinha %1!d! colunas.|  
|0xC004702E|-1073450962|DTS_E_CANTREGISTERBUFFERTYPE|A tarefa Fluxo de Dados não pode registrar um tipo de buffer. O tipo tinha %1!d! colunas e era para árvore de execução %2!d!.|  
|0xC004702F|-1073450961|DTS_E_INVALIDUSESDISPOSITIONSVALUE|A propriedade UsesDispositions não pode ser alterada do seu valor inicial. Isso ocorre quando o XML é editado e o valor de UsesDispositions é modificado. Esse valor é definido pelo componente quando é adicionado ao pacote e não pode ser alterado.|  
|0xC0047030|-1073450960|DTS_E_THREADFAILEDINITIALIZE|A tarefa Fluxo de Dados não inicializou um thread necessário e não pode começar a execução. O thread informou anteriormente um erro específico.|  
|0xC0047031|-1073450959|DTS_E_THREADFAILEDCREATE|A tarefa Fluxo de Dados não criou um thread necessário e não pode começar a execução. Isso normalmente ocorre quando existe um estado de falta de memória.|  
|0xC0047032|-1073450958|DTS_E_EXECUTIONTREECYCLEADDINGSYNCHRONOUSINPUT|A entrada síncrona de "%1" não pode ser definida como "%2" porque um ciclo seria criado.|  
|0xC0047033|-1073450957|DTS_E_INVALIDCUSTOMPROPERTYNAME|Uma propriedade personalizada de nome "%1" é inválida porque existe uma propriedade de estoque com esse nome. Uma propriedade personalizada não pode ter o mesmo nome de uma propriedade de estoque no mesmo objeto.|  
|0xC0047035|-1073450955|DTS_E_BUFFERLOCKUNDERFLOW|O buffer já foi desbloqueado.|  
|0xC0047036|-1073450954|DTS_E_INDIVIDUALCACHEINTERFACESFAILED|Falha na inicialização de %1 com o código de erro 0x%2!8.8X!.|  
|0xC0047037|-1073450953|DTS_E_INDIVIDUALRELEASEINTERFACESFAILED|Falha de %1 durante o desligamento com o código de erro 0x%2!8.8X!. Um componente não liberou suas interfaces.|  
|0xC0047038|-1073450952|DTS_E_PRIMEOUTPUTFAILED|Código de Erro SSIS DTS_E_PRIMEOUTPUTFAILED.  O método PrimeOutput em %1 retornou o código de erro 0x%2!8.8X!.  O componente retornou um código de falha quando o mecanismo do pipeline chamou PrimeOutput (). O significado do código de falha é definido pelo componente, mas o erro é fatal e a execução do pipeline foi interrompida.  Pode haver mensagens de erro geradas antes dessa, contendo mais informações sobre a falha.|  
|0xC0047039|-1073450951|DTS_E_THREADCANCELLED|Código de Erro SSIS DTS_E_THREADCANCELLED.  O thread "%1" recebeu um sinal de desligamento e está sendo encerrado. O usuário solicitou um desligamento, ou um erro em outro thread está provocando o desligamento do pipeline.  Pode haver mensagens de erro geradas antes dessa, contendo mais informações justificando por que o thread foi cancelado.|  
|0xC004703A|-1073450950|DTS_E_DISTRIBUTORCANTSETPROPERTY|O distribuidor do thread "%1" não pôde inicializar a propriedade "%2" no componente "%3" devido ao erro 0x%8.8X. O distribuidor não pôde inicializar a propriedade do componente e não pode continuar executando.|  
|0xC004703B|-1073450949|DTS_E_CANTREGISTERVIEWBUFFERTYPE|A tarefa Fluxo de Dados não pode registrar um tipo de buffer de exibição. O tipo tinha %1!d! colunas e era para identificação de entrada %2!d!.|  
|0xC004703F|-1073450945|DTS_E_CANTCREATEEXECUTIONTREE|Não há memória suficiente para criar uma árvore de execução.|  
|0xC0047040|-1073450944|DTS_E_CANTINSERTINTOHASHTABLE|Não há memória suficiente para inserir um objeto na tabela de hash.|  
|0xC0047041|-1073450943|DTS_E_OBJECTNOTINHASHTABLE|O objeto não está na tabela de hash.|  
|0xC0047043|-1073450941|DTS_E_CANTCREATECOMPONENTVIEW|Não é possível criar uma exibição de componente porque já existe outra. Pode existir apenas uma exibição de componente de cada vez.|  
|0xC0047046|-1073450938|DTS_E_LAYOUTCANTSETUSAGETYPE|Na entrada "%1" (%2!d!), a coleção de colunas de entrada virtual não contém uma coluna de entrada virtual com a identificação de linhagem %3!d!.|  
|0xC0047047|-1073450937|DTS_E_WRONGOBJECTTYPE|O objeto solicitado tem o tipo de objeto incorreto.|  
|0xC0047048|-1073450936|DTS_E_CANTCREATESPOOLFILE|O gerenciador de buffer não pode criar um arquivo de armazenamento temporário em nenhum caminho na propriedade BufferTempStoragePath. Há um nome de arquivo incorreto ou não há permissão ou os caminhos estão completos.|  
|0xC0047049|-1073450935|DTS_E_SEEKFAILED|O gerenciador de buffer não pôde buscar o deslocamento %1!d! no arquivo "%2". O arquivo está danificado.|  
|0xC004704A|-1073450934|DTS_E_EXTENDFAILED|O gerenciador de buffer não pode estender o arquivo "%1" para o comprimento %2!lu! bytes.  Não havia espaço suficiente no disco.|  
|0xC004704B|-1073450933|DTS_E_FILEWRITEFAILED|O gerenciador de buffer não pode gravar %1!d! bytes no arquivo "%2". Não havia cota ou espaço suficiente no disco.|  
|0xC004704C|-1073450932|DTS_E_FILEREADFAILED|O gerenciador de buffer não pode ler %1!d! bytes do arquivo "%2". O arquivo está danificado.|  
|0xC004704D|-1073450931|DTS_E_VIRTUALNOTSEQUENTIAL|ID de buffer %1!d! fornece suporte a outros buffers virtuais e não pode ser colocada em modo sequencial. IDTSBuffer100.SetSequentialMode foi chamado em um buffer com suporte para buffers virtuais.|  
|0xC004704E|-1073450930|DTS_E_BUFFERISREADONLY|Não foi possível executar essa operação porque o buffer está em modo somente leitura. Um buffer somente leitura não pode ser modificado.|  
|0xC004704F|-1073450929|DTS_E_EXECUTIONTREECYCLESETTINGID|A ID %1 não pode ser definida como %2!d! porque um ciclo seria criado.|  
|0xC0047050|-1073450928|DTS_E_NOMOREBUFFERTYPES|O gerenciador de buffer ficou sem memória durante a tentativa de estender a tabela de tipos de buffer. Isso foi provocado por falta de memória.|  
|0xC0047051|-1073450927|DTS_E_CANTCREATENEWTYPE|O gerenciador de buffer não criou um novo tipo de buffer.|  
|0xC0047053|-1073450925|DTS_E_SCHEDULERBADTREE|O agendador do mecanismo de Fluxo de Dados não recuperou a árvore de execução com o índice %1!d! do layout. O agendador recebeu uma contagem contendo mais árvores de execução que as efetivamente existentes.|  
|0xC0047056|-1073450922|DTS_E_CANTCREATEPRIMEOUTPUTBUFFER|Falha na tarefa de Fluxo de Dados ao criar um buffer para chamar PrimeOutput para saída "%3" (%4!d!) no componente "%1" (%2!d!). Esse erro normalmente ocorre por falta de memória.|  
|0xC0047057|-1073450921|DTS_E_SCHEDULERTHREADMEMORY|O agendador do mecanismo de Fluxo de Dados não criou um objeto de thread porque não há memória suficiente disponível. Isso foi provocado por falta de memória.|  
|0xC004705A|-1073450918|DTS_E_SCHEDULEROBJECT|O agendador do mecanismo de Fluxo de Dados não pode recuperar o objeto com ID %1!d! do layout. O agendador do mecanismo de Fluxo de Dados localizou antes um objeto que agora não está mais disponível.|  
|0xC004705B|-1073450917|DTS_E_PREPARETREENODEFAILED|Falha na tarefa de Fluxo de Dados ao preparar buffers para o nó da árvore de execução que começa na saída "%1" (%2!d!).|  
|0xC004705C|-1073450916|DTS_E_CANTCREATEVIRTUALBUFFER|A tarefa Fluxo de Dados não pode criar um buffer virtual para preparar para execução.|  
|0xC004705E|-1073450914|DTS_E_NOMOREIDS|A ID máxima foi atingida. Não existem mais IDs disponíveis para serem atribuídos a objetos.|  
|0xC004705F|-1073450913|DTS_E_ALREADYATTACHED|O %1 já está anexado e não pode ser anexado novamente.  Desanexe e tente novamente.|  
|0xC0047060|-1073450912|DTS_E_OUTPUTCOLUMNNAMECONFLICT|O nome de coluna "%1" na saída "%2" não pode ser usado porque está em conflito com uma coluna de mesmo nome na entrada síncrona "%3".|  
|0xC0047061|-1073450911|DTS_E_EOFANNOUNCEMENTFAILED|A tarefa Fluxo de Dados não pode criar um buffer para marcar o final do conjunto de linhas.|  
|0xC0047062|-1073450910|DTS_E_USERCOMPONENTEXCEPTION|Um componente de usuário gerenciado gerou a exceção "%1".|  
|0xC0047063|-1073450909|DTS_E_SCHEDULERMEMORY|O agendador do mecanismo de Fluxo de Dados não pode alocar memória suficiente para as estruturas de execução. O sistema tinha pouca memória antes de começar a execução.|  
|0xC0047064|-1073450908|DTS_E_BUFFERNOOBJECTMEMORY|A falta de memória impediu a criação do objeto de buffer.|  
|0xC0047065|-1073450907|DTS_E_BUFFERNOMAPMEMORY|A falta de memória impede o mapeamento de IDs de linhagem de um buffer para índices DTP_HCOL.|  
|0xC0047066|-1073450906|DTS_E_INDIVIDUALPUTVARIABLESFAILED|"%1!s!" não pode armazenar em cache a coleção de Variáveis e retornou o código de erro 0x%2!8.8X.|  
|0xC0047067|-1073450905|DTS_E_INDIVIDUALPUTCOMPONENTMETADATAFAILED|"%1" não pôde armazenar em cache o objeto de metadados do componente e retornou o código de erro 0x%2!8.8X!.|  
|0xC0047068|-1073450904|DTS_E_SORTEDOUTPUTHASINVALIDSORTKEYPOSITION|"%1" tem SortKeyPosition diferente de zero, mas seu valor (%2!ld!) é muito grande. O valor deve ser menor que ou igual ao número de colunas.|  
|0xC004706A|-1073450902|DTS_E_SORTEDOUTPUTHASINVALIDSORTKEYPOSITIONS|A propriedade IsSorted de %1 está definida como TRUE, mas os valores absolutos de SortKeyPositions da coluna de saída diferentes de zero não formam uma sequência que aumenta de forma monotônica, começando com um.|  
|0xC004706B|-1073450901|DTS_E_INDIVIDUALVALIDATIONSTATUSFAILED|Falha em "%1" na validação e retornou o status de validação "%2".|  
|0xC004706C|-1073450900|DTS_E_CANTCREATECOMPONENT|O componente "%1!s!" não pôde ser criado e retornou o código de erro 0x%2!8.8X! "%3!s!". Certifique-se de que o componente esteja registrado corretamente.|  
|0xC004706D|-1073450899|DTS_E_COMPONENTNOTREGISTERED|O módulo contendo "%1" não está registrado ou instalado corretamente.|  
|0xC004706E|-1073450898|DTS_E_COMPONENTNOTFOUND|O módulo contendo "%1" não pode ser localizado, embora esteja registrado.|  
|0xC004706F|-1073450897|DTS_E_BINARYCODENOTFOUND|O componente de script está configurado para pré-compilar o script, mas o código binário não foi encontrado. Visite o IDE em Editor de Componentes de Script, clicando no botão Script de Design para gerar o código binário.|  
|0xC0047070|-1073450896|DTS_E_CANTCREATEBLOBFILE|O gerenciador de buffer não pode criar um arquivo para colocar um objeto longo em spool nos diretórios nomeados na propriedade BLOBTempStoragePath.  Ou um nome de arquivo incorreto foi fornecido ou não há permissões ou os caminhos estão completos.|  
|0xC0047071|-1073450895|DTS_E_SYNCHRONOUSIDMISMATCH|A propriedade SynchronousInputID em "%1" era %2!d! e %3!d! era esperado.|  
|0xC0047072|-1073450894|DTS_E_OBJECTIDNOTFOUND|Não há nenhum objeto com a identificação %1!d!.|  
|0xC0047073|-1073450893|DTS_E_OBJECTIDLOOKUPFAILED|Incapaz de localizar um objeto com ID %1!d! devido ao código de erro 0x%2!8.8X!.|  
|0xC0047074|-1073450892|DTS_E_INVALIDCODEPAGE|A página de código %1!d! especificada na coluna de saída "%2" (%3!d!) não é válida. Selecione uma página de código diferente para a coluna de saída "%2".|  
|0xC0047075|-1073450891|DTS_E_INDIVIDUALPUTEVENTINFOSFAILED|A coleção EventInfos não pôde ser armazenada em cache por "%1" e retornou o código de erro 0x%2!8.8X!.|  
|0xC0047077|-1073450889|DTS_E_DUPLICATEOUTPUTCOLUMNNAMES|O nome de "%1" está duplicado.  Todos os nomes devem ser exclusivos.|  
|0xC0047078|-1073450888|DTS_E_NOOUTPUTCOLUMNFORINPUTCOLUMN|Não há coluna de saída associada à coluna de entrada "%1" (%2!d!).|  
|0xC0047079|-1073450887|DTS_E_EXCLGRPNOSYNCINP|"%1" tem um buffer virtual estendido a partir de uma origem raiz. Existe um grupo de exclusão diferente de zero com uma entrada síncrona igual a zero.|  
|0xC004707A|-1073450886|DTS_E_ERROROUTCANTBEONSYNCNONEXCLUSIVEOUTPUT|"%1" não pode ser uma saída de erro porque saídas de erro não podem ser colocadas em saídas síncronas não exclusivas.|  
|0xC004707B|-1073450885|DTS_E_EXPREVALDIVBYZERO|Ocorreu um erro a ser dividido por zero. O operando à direita é avaliado como zero na expressão "%1".|  
|0xC004707C|-1073450884|DTS_E_EXPREVALLITERALOVERFLOW|O "%1" literal é muito grande para o tipo %2. A magnitude do valor literal estoura o tipo.|  
|0xC004707D|-1073450883|DTS_E_EXPREVALBINARYOPNUMERICOVERFLOW|O resultado da operação binária "%1" nos tipos de dados %2 e %3 excede o tamanho máximo para tipos numéricos. Não foi possível converter implicitamente os tipos de operando em um resultado numérico (DT_NUMERIC) sem perda de precisão ou escala. Para executar essa operação, um ou ambos os operandos precisam ser convertidos explicitamente com um operador de conversão.|  
|0xC004707E|-1073450882|DTS_E_EXPREVALBINARYOPOVERFLOW|O resultado da operação binária "%1" excede o tamanho máximo para o tipo de dados de resultado "%2". A magnitude do resultado da operação estoura o tipo do resultado.|  
|0xC004707F|-1073450881|DTS_E_EXPREVALFUNCTIONOVERFLOW|O resultado da chamada de função "%1" é muito grande para o tipo "%2". A magnitude do resultado da chamada de função estoura o tipo do operando. Pode ser necessária uma conversão explícita para um tipo maior.|  
|0xC0047080|-1073450880|DTS_E_EXPREVALBINARYTYPEMISMATCH|Os tipos de dados "%1" e "%2" são incompatíveis para o operador binário "%3". Não foi possível converter de forma implícita os tipos de operando em tipos compatíveis para a operação. Para executar essa operação, um ou ambos os operandos precisam ser convertidos explicitamente com um operador de conversão.|  
|0xC0047081|-1073450879|DTS_E_EXPREVALUNSUPPORTEDBINARYTYPE|O tipo de dados "%1" não pode ser usado com o operador binário "%2". Não existe suporte para a operação com o tipo de um ou ambos os operandos. Para executar essa operação, um ou ambos os operandos precisam ser convertidos explicitamente com um operador de conversão.|  
|0xC0047082|-1073450878|DTS_E_EXPREVALBINARYSIGNMISMATCH|Existe uma incompatibilidade de sinais para o operador binário bit a bit "%1" na operação "%2". Ambos os operandos desse operador devem ser positivos ou negativos.|  
|0xC0047083|-1073450877|DTS_E_EXPREVALBINARYOPERATIONFAILED|Falha na operação binária "%1" com o código de erro 0x%2!8.8X!. Ocorreu um erro interno, ou há falta de memória.|  
|0xC0047084|-1073450876|DTS_E_EXPREVALBINARYOPERATIONSETTYPEFAILED|Falha na tentativa de definir o tipo de resultado da operação binária "%1" com o código de erro 0x%2!8.8X!.|  
|0xC0047085|-1073450875|DTS_E_EXPREVALSTRINGCOMPARISONFAILED|Falha na comparação entre "%1" e a cadeia de caracteres "%2".|  
|0xC0047086|-1073450874|DTS_E_EXPREVALUNSUPPORTEDUNNARYTYPE|O tipo de dados "%1" não pode ser usado com o operador unário "%2". Não existe suporte para a operação com esse tipo de operando. Para executar essa operação, o operando precisa ser convertido explicitamente com um operador de conversão.|  
|0xC0047087|-1073450873|DTS_E_EXPREVALUNARYOPERATIONFAILED|Falha na operação unária "%1" com o código de erro 0x%2!8.8X!. Ocorreu um erro interno, ou há falta de memória.|  
|0xC0047088|-1073450872|DTS_E_EXPREVALUNARYOPERATIONSETTYPEFAILED|Falha na tentativa de definir o tipo de resultado da operação unária "%1" com o código de erro 0x%2!8.8X!.|  
|0xC0047089|-1073450871|DTS_E_EXPREVALPARAMTYPEMISMATCH|A função "%1" não oferece suporte ao tipo de dados "%2" para o número de parâmetro %3!d!. Não foi possível converter de forma implícita o tipo do parâmetro em um tipo compatível para a função. Para executar essa operação, o operando precisa ser convertido explicitamente com um operador de conversão.|  
|0xC004708A|-1073450870|DTS_E_EXPREVALINVALIDFUNCTION|A função "%1" não foi reconhecida. O nome da função está incorreto ou não existe.|  
|0xC004708B|-1073450869|DTS_E_EXPREVALFNSUBSTRINGINVALIDLENGTH|O comprimento %1!d! não é válido para a função "%2". O parâmetro de comprimento não pode ser negativo. Altere o parâmetro de comprimento para zero ou um valor positivo.|  
|0xC004708C|-1073450868|DTS_E_EXPREVALFNSUBSTRINGINVALIDSTARTINDEX|O índice inicial %1!d! não é válido para a função "%2". O valor de índice inicial deve ser um número inteiro maior que zero. A base do índice inicial é 1, e não 0.|  
|0xC004708E|-1073450866|DTS_E_EXPREVALCHARMAPPINGFAILED|A função "%1" não pode executar o mapeamento de caractere na cadeia de caracteres "%2".|  
|0xC004708F|-1073450865|DTS_E_EXPREVALINVALIDDATEPART|"%1" não é uma parte de data válida para a função "%2".|  
|0xC0047090|-1073450864|DTS_E_EXPREVALINVALIDNULLPARAM|Número de parâmetro %1!d! da função NULL com tipo de dados "%2" não é válido. Os parâmetros de NULL() devem ser estáticos e não podem conter elementos dinâmicos, como colunas de entrada.|  
|0xC0047091|-1073450863|DTS_E_EXPREVALINVALIDNULLPARAMTYPE|Número de parâmetro %1!d! da função NULL com tipo de dados "%2" não é um inteiro. Um parâmetro de NULL() deve ser um número inteiro ou um tipo que possa ser convertido em inteiro.|  
|0xC0047092|-1073450862|DTS_E_EXPREVALFUNCTIONPARAMNOTSTATIC|Número de parâmetro %1!d! da função "%2" não é estático. Esse parâmetro deve ser estático e não pode conter elementos dinâmicos, como colunas de entrada.|  
|0xC0047093|-1073450861|DTS_E_EXPREVALINVALIDCASTPARAM|Número de parâmetro %1!d! da conversão para tipo de dados "%2" não é válido. Os parâmetros de operadores de conversão devem ser estáticos e não podem conter elementos dinâmicos, como colunas de entrada.|  
|0xC0047094|-1073450860|DTS_E_EXPREVALINVALIDCASTPARAMTYPE|Número de parâmetro %1!d! da conversão para tipo de dados "%2" não é inteiro. Um parâmetro de operador de conversão deve ser um número inteiro ou um tipo que possa ser convertido em inteiro.|  
|0xC0047095|-1073450859|DTS_E_EXPREVALINVALIDCAST|Não é possível converter a expressão "%1" do tipo de dados "%2" em tipo de dados "%3". Não existe suporte para a conversão solicitada.|  
|0xC0047096|-1073450858|DTS_E_EXPREVALINVALIDTOKEN|Falha na tentativa de análise da expressão "%1".  O token "%2" no número de linha "%3", número de caractere "%4" não foi reconhecido. A expressão não pode ser analisada porque contém elementos inválidos no local especificado.|  
|0xC0047097|-1073450857|DTS_E_EXPREVALUNEXPECTEDPARSEERROR|Erro durante a análise da expressão "%1". A expressão não foi analisada por motivo desconhecido.|  
|0xC0047098|-1073450856|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSIONWITHHR|Falha na tentativa de analisar a expressão "%1" com o código de erro 0x%2!8.8X!. A expressão não pode ser analisada. Ela pode conter elementos inválidos ou não estar bem formada. Pode haver também um erro por falta de memória.|  
|0xC0047099|-1073450855|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSION|A expressão "%1" não é válida e não pode ser analisada. A expressão pode conter elementos inválidos ou não estar bem formada.|  
|0xC004709A|-1073450854|DTS_E_EXPREVALEXPRESSIONEMPTY|Não havia nenhuma expressão para ser computada. Houve uma tentativa de computar ou obter a cadeia de caracteres de uma expressão vazia.|  
|0xC004709B|-1073450853|DTS_E_EXPREVALCOMPUTEFAILED|Falha na tentativa de computar a expressão "%1" com o código de erro 0x%2!8.8X!.|  
|0xC004709C|-1073450852|DTS_E_EXPREVALBUILDSTRINGFAILED|Falha na tentativa de gerar uma representação de cadeia de caracteres da expressão com o código de erro 0x%1!8.8X!. A falha ocorreu ao tentar gerar uma cadeia de caracteres exibível que representa a expressão.|  
|0xC004709D|-1073450851|DTS_E_EXPREVALCANNOTCONVERTRESULT|Não é possível converter o tipo de dados de resultado da expressão "%1" em tipo de dados de coluna "%2". O resultado da expressão deve ser gravado em uma coluna de entrada/saída, mas o tipo de dados da expressão não pode ser convertido em tipo de dados da coluna.|  
|0xC004709E|-1073450850|DTS_E_EXPREVALCONDITIONALOPINVALIDCONDITIONTYPE|A expressão condicional "%1" do operador condicional tem um tipo de dados inválido de "%2". A expressão condicional do operador condicional deve retornar um booliano que seja do tipo DT_BOOL.|  
|0xC004709F|-1073450849|DTS_E_EXPREVALCONDITIONALOPTYPEMISMATCH|Os tipos de dados "%1" e "%2" são incompatíveis para o operador condicional. Não é possível converter de forma implícita os tipos de operando em tipos compatíveis para a operação condicional. Para executar essa operação, um ou ambos os operandos precisam ser convertidos explicitamente com um operador de conversão.|  
|0xC00470A0|-1073450848|DTS_E_EXPREVALCONDITIONALOPSETTYPEFAILED|Falha na tentativa de definir o tipo de resultado da operação condicional "%1" com o código de erro 0x%2!8.8X!.|  
|0xC00470A1|-1073450847|DTS_E_BUFFERORPHANED|Esse buffer ficou órfão. O gerenciador de buffer foi desligado, deixando um buffer pendente, e nenhuma limpeza será feita no buffer. Existe possibilidade de vazamento de memória e outros problemas.|  
|0xC00470A2|-1073450846|DTS_E_EXPREVALINPUTCOLUMNNAMENOTFOUND|Falha na tentativa de encontrar a coluna de entrada denominada "%1" com o código de erro 0x%2!8.8X!. A coluna de entrada especificada não foi encontrada na coleção de colunas de entrada.|  
|0xC00470A3|-1073450845|DTS_E_EXPREVALINPUTCOLUMNIDNOTFOUND|Falha na tentativa de encontrar a coluna de entrada com a ID de linhagem %1!d! com código de erro 0x%2!8.8X!. A coluna de entrada não foi encontrada na coleção de colunas de entrada.|  
|0xC00470A4|-1073450844|DTS_E_EXPREVALNOINPUTCOLUMNCOLLECTIONFORCOLUMNNAME|A expressão contém token "%1" não reconhecido. Se "%1" for uma variável, ela deverá ser expressa como "\@%1". O token especificado não é válido. Se a intenção é que o token seja um nome de variável, deve ter como prefixo o símbolo \@.|  
|0xC00470A5|-1073450843|DTS_E_EXPREVALNOINPUTCOLUMNCOLLECTIONFORCOLUMNID|A expressão contém o token não reconhecido "#%1!d!".|  
|0xC00470A6|-1073450842|DTS_E_EXPREVALVARIABLENOTFOUND|A variável "%1" não foi encontrada na coleção Variables. A variável pode não existir no escopo correto.|  
|0xC00470A7|-1073450841|DTS_E_EXPREVALINVALIDTOKENSTATE|Falha na tentativa de análise da expressão "%1". A expressão pode conter um token inválido, um token incompleto ou um elemento inválido. Ela pode não estar bem formada, ou pode estar faltando um elemento necessário, como um parêntese.|  
|0xC00470A8|-1073450840|DTS_E_BLANKOUTPUTCOLUMNNAME|O nome para "%1" está em branco, e nomes não podem estar em branco.|  
|0xC00470A9|-1073450839|DTS_E_HASSIDEEFFECTSWITHSYNCINP|O "%1" tem a propriedade HasSideEffects definida como TRUE, mas "%1" é síncrono e não pode ter efeitos colaterais. Defina a propriedade HasSideEffects como FALSE.|  
|0xC00470AA|-1073450838|DTS_E_EXPREVALINVALIDCASTCODEPAGE|O valor %1!d!, especificado para o parâmetro de página de código da conversão em tipo de dados "%2", não é válido. A página de código não está instalada na máquina.|  
|0xC00470AB|-1073450837|DTS_E_EXPREVALINVALIDCASTPRECISION|O valor é %1!d! especificado para o parâmetro de precisão da conversão em tipo de dados "%2" não é válido. A precisão deve ficar no intervalo de %3!d! a %4!d! e o valor de precisão está fora da faixa para a conversão de tipos.|  
|0xC00470AC|-1073450836|DTS_E_EXPREVALINVALIDCASTSCALE|O valor é %1!d! especificado para o parâmetro de escala da conversão em tipo de dados "%2" não é válido. A escala deve ficar no intervalo de %3!d! a %4!d! e o valor da escala está fora da faixa para a conversão de tipos. A escala não deve exceder a precisão e deve ser positivo.|  
|0xC00470AD|-1073450835|DTS_E_NONSORTEDOUTPUTHASSORTKEYPOSITIONS|A propriedade IsSorted para "%1" é falsa, mas %2!lu! de SortKeyPositions das colunas de saída não são zero.|  
|0xC00470AF|-1073450833|DTS_E_EXPREVALCONDITIONALOPCODEPAGEMISMATCH|As páginas de código devem corresponder para os operandos de operação condicional "%1" para o tipo %2. A página de código do operando à esquerda não corresponde à página de código do operando à direita. Para o operador condicional no tipo especificado, as páginas de código devem ser as mesmas.|  
|0xC00470B1|-1073450831|DTS_E_REFERENCEDMETADATABADCOUNT|A entrada "%1" (%2!d!) referencia a entrada"%3" (%4!d!), mas elas não têm o mesmo número de colunas. A entrada %5!d! tem %6!d! colunas, enquanto a entrada %7!d! tem %8!d! colunas.|  
|0xC00470B2|-1073450830|DTS_E_OBJECTLINEAGEIDNOTFOUND|Não existe nenhum objeto com a identificação de linhagem %1!d!.|  
|0xC00470B3|-1073450829|DTS_E_FILENAMEOUTPUTCOLUMNOTFOUND|A coluna de saída para o nome de arquivo não pode ser encontrada.|  
|0xC00470B4|-1073450828|DTS_E_FILENAMEOUTPUTCOLUMNINVALIDDATATYPE|A coluna de saída para o nome de arquivo não é uma cadeia de caracteres Unicode terminada em caractere nulo, que é um tipo de dados DT_WSTR.|  
|0xC00470B5|-1073450827|DTS_E_DISTRIBUTORADDFAILED|Um distribuidor não pôde atribuir um buffer ao thread "%1" devido ao erro 0x%2!8.8X!. O thread de destino está provavelmente sendo desligado.|  
|0xC00470B6|-1073450826|DTS_E_LOCALENOTINSTALLED|A LocaleID %1!ld! não está instalada nesse sistema.|  
|0xC00470B7|-1073450825|DTS_E_EXPREVALILLEGALHEXESCAPEINSTRINGLITERAL|O "%1" literal da cadeia de caracteres contém uma sequência de escape hexadecimal ilegal de "\x%2". A sequência de escape não tem suporte em valores literais da cadeia de caracteres no avaliador de expressões. As sequências de escape hexadecimais devem ser do formato \xhhhh onde h seja um dígito hexadecimal válido.|  
|0xC00470B8|-1073450824|DTS_E_EXPREVALILLEGALESCAPEINSTRINGLITERAL|O literal da cadeia de caracteres "%1" contém uma sequência de escape ilegal de "\\%2!c!". A sequência de escape não tem suporte em valores literais da cadeia de caracteres no avaliador de expressões. Se uma cadeia de caracteres requer uma barra invertida, use duas barras invertidas, "\\\\".|  
|0xC00470B9|-1073450823|DTS_E_NOOUTPUTCOLUMNS|"%1" não contém nenhuma coluna de saída. Uma saída assíncrona deve conter colunas de saída.|  
|0xC00470BA|-1073450822|DTS_E_LOBDATATYPENOTSUPPORTED|O "%1" tem um tipo de dados de objeto longo de DT_TEXT, DT_NTEXT ou DT_IMAGE, sem-suporte.|  
|0xC00470BB|-1073450821|DTS_E_OUTPUTWITHMULTIPLEERRORS|Falha na ID de saída %1!d! foram atribuídos vários erros de configuração de saída. Primeiro %2!d! e %3!d!, depois %4!d! e %5!d!.|  
|0xC00470BC|-1073450820|DTS_E_FAILEDDURINGOLEDBDATATYPECONVERSIONCHECK|Falha no provedor OLE DB durante a verificação da conversão de tipo de dados para "%1".|  
|0xC00470BD|-1073450819|DTS_E_BUFFERISEOR|Esse buffer representa o final do conjunto de linhas, e sua contagem de linhas não pode ser alterada.  Foi feita uma tentativa de chamar AddRow ou RemoveRow em um buffer que tem o final do sinalizador de conjunto de linhas.|  
|0xC00470BE|-1073450818|DTS_E_EXPREVALUNSUPPORTEDTYPE|Não existe suporte para o tipo de dados "%1" em uma expressão. Não existe suporte para o tipo especificado, ou o tipo não é válido.|  
|0xC00470BF|-1073450817|DTS_E_PRIMEOUTPUTNOEOR|O método PrimeOutput em "%1" retornou com êxito, mas não informou um final do conjunto de linhas. Existe um erro no componente. Ele deveria ter reportado um final de linha. A execução do pipeline será desligada para evitar resultados imprevisíveis.|  
|0xC00470C0|-1073450816|DTS_E_EXPREVALDATACONVERSIONOVERFLOW|Ocorreu um estouro durante a conversão do tipo de dados "%1" em tipo de dados "%2". O tipo de origem é muito grande para o tipo de destino.|  
|0xC00470C1|-1073450815|DTS_E_EXPREVALDATACONVERSIONNOTSUPPORTED|Existe suporte para a conversão do tipo de dados "%1" em tipo de dados "%2". O tipo de origem não pode ser convertido no tipo de destino.|  
|0xC00470C2|-1073450814|DTS_E_EXPREVALDATACONVERSIONFAILED|Código de erro 0x%1!8.8X! durante tentativa de conversão de tipo de dados %2 em tipo de dados %3.|  
|0xC00470C3|-1073450813|DTS_E_EXPREVALCONDITIONALOPERATIONFAILED|Falha da operação condicional "%1" com o código de erro 0x%2!8.8X!. Houve um erro interno ou de falta de memória.|  
|0xC00470C4|-1073450812|DTS_E_EXPREVALCASTFAILED|Falha na conversão da expressão "%1" do tipo de dados "%2" no tipo de dados "%3" com o código de erro 0x%4!8.8X!.|  
|0xC00470C5|-1073450811|DTS_E_EXPREVALFUNCTIONCOMPUTEFAILED|Falha na função de avaliação "%1" com o código de erro 0x%2!8.8X!.|  
|0xC00470C6|-1073450810|DTS_E_EXPREVALFUNCTIONCONVERTPARAMTOMEMBERFAILED|Número de parâmetro %1!d! da função "%2" não pode ser convertido em valor estático.|  
|0xC00470C7|-1073450809|DTS_E_REDIRECTROWUNAVAILABLEWITHFASTLOADANDZEROMAXINSERTCOMMITSIZE|A disposição da linha de erro em "%1" não pode ser definida para redirecionar a linha quando a opção de carga rápida está ativada, e o tamanho máximo de confirmação da inserção está definido como zero.|  
|0xC00470CE|-1073450802|DTS_E_EXPREVALBINARYOPERATORCODEPAGEMISMATCH|As páginas de código para operandos do operador binário "%1" para o tipo "%2" devem ser correspondentes. No momento, a página de código do operando à esquerda não corresponde à página de código do operando à direita. Para o operador binário especificado no tipo especificado, as páginas de código devem ser as mesmas.|  
|0xC00470CF|-1073450801|DTS_E_EXPREVALVARIABLECOMPUTEFAILED|Falha na recuperação do valor da Variável "%1" com o código de erro 0x%2!8.8X!.|  
|0xC00470D0|-1073450800|DTS_E_EXPREVALVARIABLETYPENOTSUPPORTED|Não existe suporte para o tipo de dados da variável "%1" em uma expressão.|  
|0xC00470D1|-1073450799|DTS_E_EXPREVALCASTCODEPAGEMISMATCH|Não é possível converter a expressão "%1" do tipo de dados "%2" no tipo de dados "%3" porque a página de código do valor sendo convertido (%4!d!) não corresponde à página de código de resultado solicitada (%5!d!). A página de código da origem deve corresponder à página de código de destino solicitada.|  
|0xC00470D2|-1073450798|DTS_E_BUFFERSIZEOUTOFRANGE|O tamanho de buffer padrão deve estar entre %1!d! e %2!d! bytes. Falha ao tentar definir a propriedade DefaultBufferSize para um valor pequeno ou grande demais.|  
|0xC00470D3|-1073450797|DTS_E_BUFFERMAXROWSIZEOUTOFRANGE|O número máximo de linhas do buffer padrão deve ser maior que %1!d! linhas. Foi feita uma tentativa de definir a propriedade DefaultBufferMaxRows para um valor pequeno demais.|  
|0xC00470D4|-1073450796|DTS_E_EXTERNALCOLUMNMETADATACODEPAGEMISMATCH|A página de código em %1 é %2!d! e deve ser %3!d!.|  
|0xC00470D5|-1073450795|DTS_E_THREADCOUNTOUTOFRANGE|Falha ao atribuir %3!d! à propriedade EngineThreads da tarefa de Fluxo de Dados. O valor deve estar entre %1!d! e %2!d!.|  
|0xC00470D6|-1073450794|DTS_E_EXPREVALINVALIDTOKENSINGLEQUOTE|Falha na análise da expressão "%1". A aspa simples no número da linha "%2", número do caractere "%3", não era esperada.|  
|0xC00470D7|-1073450793|DTS_E_EXPREVALINVALIDTOKENSINGLEEQUAL|Falha na análise da expressão "%1". O sinal de igualdade (=) no número da linha "%2", número do caractere "%3", não era esperado. Podem ser necessários dois sinais de igualdade (==) no local especificado.|  
|0xC00470DA|-1073450790|DTS_E_INDIVIDUALPUTREFTRACKERFAILED|O componente "%1" não pôde armazenar em cache a coleção de controladores de referência de objeto de tempo de execução e retornou o código de erro 0x%2!8.8X!.|  
|0xC00470DB|-1073450789|DTS_E_EXPREVALAMBIGUOUSINPUTCOLUMNNAME|Existem várias colunas de entrada com o nome "%1". A coluna de entrada desejada deve ser especificada de forma exclusiva como [Nome do Componente]. [%2] ou referenciada por ID de linhagem. No momento, a coluna de entrada especificada existe em mais de um componente.|  
|0xC00470DC|-1073450788|DTS_E_EXPREVALDOTTEDINPUTCOLUMNNAMENOTFOUND|Falha na localização da coluna de entrada denominada "[%1].[%2]" com o código de erro 0x%3!8.8X!. A coluna de entrada não foi encontrada na coleção de colunas de entrada.|  
|0xC00470DD|-1073450787|DTS_E_EXPREVALAMBIGUOUSVARIABLENNAME|Existem diversas variáveis com o nome "%1". A variável desejada deve ser especificada de forma exclusiva como \@[Namespace::%2]. A variável existe em mais de um namespace.|  
|0xC00470DE|-1073450786|DTS_E_REDUCTIONFAILED|O agendador do mecanismo de Fluxo de Dados não reduziu o plano de execução para o pipeline. Defina a propriedade OptimizedMode como falsa.|  
|0xC00470DF|-1073450785|DTS_E_EXPREVALSQRTINVALIDPARAM|A função SQRT não pode operar com valores negativos, e foi passado um valor negativo à função SQRT.|  
|0xC00470E0|-1073450784|DTS_E_EXPREVALLNINVALIDPARAM|A função LN não pode operar com zero ou valores negativos, e foi passado um zero ou um valor negativo à função LN.|  
|0xC00470E1|-1073450783|DTS_E_EXPREVALLOGINVALIDPARAM|A função LOG não pode operar com zero ou valores negativos, e foi passado um zero ou um valor negativo à função LOG.|  
|0xC00470E2|-1073450782|DTS_E_EXPREVALPOWERINVALIDPARAM|Os parâmetros passados à função POWER não podem ser avaliados e podem gerar um resultado indeterminado.|  
|0xC00470E3|-1073450781|DTS_E_NOCANCELEVENT|O tempo de execução não pode fornecer um evento de cancelamento devido ao erro 0x%1!8.8X!.|  
|0xC00470E4|-1073450780|DTS_E_CANCELRECEIVED|O pipeline recebeu uma solicitação de cancelamento e está sendo desligado.|  
|0xC00470E5|-1073450779|DTS_E_EXPREVALUNARYOPOVERFLOW|O resultado da operação de subtração (negação) unária "%1" excede o tamanho máximo para tipo de dados de resultado "%2". A magnitude do resultado da operação estoura o tipo do resultado.|  
|0xC00470E6|-1073450778|DTS_E_EXPREVALPLACEHOLDERINEXPRESSION|O espaço reservado "%1" foi encontrado em uma expressão. Ele deve ser substituído por um operando ou parâmetro real.|  
|0xC00470E7|-1073450777|DTS_E_EXPREVALFNRIGHTINVALIDLENGTH|O comprimento %1!d! especificado para a função "%2" é negativo e não é válido. O parâmetro de comprimento deve ser positivo.|  
|0xC00470E8|-1073450776|DTS_E_EXPREVALFNREPLICATEINVALIDREPEATCOUNT|A contagem de repetições %1!d! é negativa e não é válida para a função "%2". O parâmetro de contagem de repetições não pode ser negativo.|  
|0xC00470EA|-1073450774|DTS_E_EXPREVALVARIABLECOULDNOTBEREAD|Falha na leitura da variável "%1" com o código de erro 0x%2!8.8X!.|  
|0xC00470EC|-1073450772|DTS_E_EXPREVALBINARYOPDTSTRNOTSUPPORTED|Para operandos de uma operação binária, existe suporte apenas para colunas de entrada e operações de conversão de tipo de dados DT_STR. A expressão "%1" tem um operando DT_STR que não é uma coluna de entrada ou o resultado de uma conversão e não pode ser usada em uma operação binária. Para executar essa operação, o operando precisa ser convertido explicitamente com um operador de conversão.|  
|0xC00470ED|-1073450771|DTS_E_EXPREVALCONDITIONALOPDTSTRNOTSUPPORTED|Para operandos de um operador condicional, existe suporte apenas para colunas de entrada e operações de conversão de tipo de dados DT_STR. A expressão "%1" tem um operando DT_STR que não é uma coluna de entrada ou o resultado de uma conversão e não pode ser usada em uma operação condicional. Para executar essa operação, o operando precisa ser convertido explicitamente com um operador de conversão.|  
|0xC00470EE|-1073450770|DTS_E_EXPREVALFNFINDSTRINGINVALIDOCCURRENCECOUNT|A contagem de ocorrências %1!d! não é válido para a função "%2". Esse parâmetro deve ser maior que zero.|  
|0xC00470EF|-1073450769|DTS_E_INDIVIDUALPUTLOGENTRYINFOS|"%1" não pôde armazenar em cache a coleção LogEntryInfos e retornou o código de erro 0x%2!8.8X!.|  
|0xC00470F0|-1073450768|DTS_E_EXPREVALINVALIDDATEPARTNODE|O parâmetro da parte de data especificado para a função "%1" não é válido. Ele deve ser uma cadeia de caracteres estática.  O parâmetro da parte de data não pode conter elementos dinâmicos, como colunas de entrada, e deve ser do tipo DT_WSTR.|  
|0xC00470F1|-1073450767|DTS_E_EXPREVALINVALIDCASTLENGTH|O valor é %1!d! especificado como parâmetro de comprimento da conversão em tipo de dados %2 é negativo e inválido. O comprimento deve ser positivo.|  
|0xC00470F2|-1073450766|DTS_E_EXPREVALINVALIDNULLCODEPAGE|O valor é %1!d! especificado como parâmetro de página de código da função NULL com o tipo de dados "%2" não é válido. A página de código não está instalada no computador.|  
|0xC00470F3|-1073450765|DTS_E_EXPREVALINVALIDNULLPRECISION|O valor é %1!d! especificado como parâmetro de precisão da função NULL com o tipo de dados "%2" está fora do intervalo. A precisão deve ficar no intervalo de %3!d! a %4!d!.|  
|0xC00470F4|-1073450764|DTS_E_EXPREVALINVALIDNULLSCALE|O valor é %1!d! especificado como parâmetro de escala da função NULL com o tipo de dados %2 está fora do intervalo. A escala deve ficar no intervalo de %3!d! a %4!d!. A escala não deve exceder a precisão e não deve ser negativa.|  
|0xC00470F5|-1073450763|DTS_E_EXPREVALINVALIDNULLLENGTH|O valor é %1!d! especificado como parâmetro de comprimento da função "NULL" com o tipo de dados %2 é negativo e inválido. O comprimento deve ser positivo.|  
|0xC00470F6|-1073450762|DTS_E_NEGATIVESNOTALLOWED|Não pode ser atribuído valor negativo a %1.|  
|0xC00470F7|-1073450761|DTS_E_FASTPARSENOTALLOWED|A propriedade personalizada "%1" para "%2" não pode ser definida como verdadeira.  O tipo de dados de coluna deve ser um destes:  DT_I1, DT_I2, DT_I4, DT_I8, DT_UI1, DT_UI2, DT_UI4, DT_UI8, DT_DBTIMESTAMP, DT_DBTIMESTAMP2, DT_DBTIMESTAMPOFFSET, DT_DATE, DT_DBDATE, DT_DBTIME, DT_DBTIME2 ou DT_FILETIME.|  
|0xC00470F8|-1073450760|DTS_E_CANNOTREATTACHPATH|Não é possível reanexar "%1". Exclua o caminho, adicione um novo e anexe.|  
|0xC00470F9|-1073450759|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSPLURALSINGULAR|A função "%1" requer %2!d! parâmeros, não %3!d! parâmetro. O nome da função foi reconhecido, mas o número de parâmetros não é válido.|  
|0xC00470FA|-1073450758|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSSINGULARPLURAL|A função "%1" requer %2!d! parâmetro, não %3!d! parâmetros. O nome da função foi reconhecido, mas o número de parâmetros não é válido.|  
|0xC00470FB|-1073450757|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSPLURALPLURAL|A função "%1" requer %2!d! parâmeros, não %3!d! parâmetros. O nome da função foi reconhecido, mas o número de parâmetros não é válido.|  
|0xC00470FC|-1073450756|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSIONOUTOFMEMORY|Falha na tentativa de analisar a expressão "%1" porque houve um erro de falta de memória.|  
|0xC00470FD|-1073450755|DTS_E_INDIVIDUALCHECKPRODUCTLEVELFAILED|%1 não pôde executar sua verificação de nível de produto necessária e retornou o código de erro 0x%2!8.8X!.|  
|0xC00470FE|-1073450754|DTS_E_PRODUCTLEVELTOLOW|Código de Erro SSIS DTS_E_PRODUCTLEVELTOLOW.  O %1 não pode ser executado em %2 instalado de Integration Services. É necessário %3 ou superior.|  
|0xC00470FF|-1073450753|DTS_E_EXPREVALSTRINGLITERALTOOLONG|Um valor literal da cadeia de caracteres na expressão excede o comprimento máximo permitido de %1!d! caracteres.|  
|0xC0047100|-1073450752|DTS_E_EXPREVALSTRINGVARIABLETOOLONG|A variável %1 contém uma cadeia de caracteres que excede o comprimento máximo permitido de %2!d! caracteres.|  
|0xC0047101|-1073450751|DTS_E_COMPONENT_NOINTERFACE|O %1 foi localizado, mas não oferece suporte a uma interface de Serviços de Integração exigida (IDTSRuntimeComponent100).  Obtenha uma versão atualizada deste componente do provedor de componente.|  
|0xC0048000|-1073446912|DTS_E_CANNOTOPENREGISTRYKEY|A chave do registro "%1" não pode ser aberta.|  
|0xC0048001|-1073446911|DTS_E_INVALIDCOMPONENTFILENAME|Não é possível obter o nome de arquivo para o componente com CLSID de "%1". Verifique se o componente está registrado corretamente ou se o CLSID fornecido está correto.|  
|0xC0048002|-1073446910|DTS_E_UNKNOWNCOMPONENTHASINVALIDCLSID|O CLSID para um dos componentes não é válido. Verifique se todos os componentes no pipeline têm CLSIDs válidos.|  
|0xC0048003|-1073446909|DTS_E_COMPONENTHASINVALIDCLSID|O CLSID para um dos componentes com ID %1!d! não é válido.|  
|0xC0048004|-1073446908|DTS_E_INVALIDINDEX|O índice não é válido.|  
|0xC0048005|-1073446907|DTS_E_CANNOTACCESSDTSAPPLICATIONOBJECT|O objeto Aplicativo não pode ser acessado. Verifique se o SSIS está instalado corretamente.|  
|0xC0048006|-1073446906|DTS_E_ERROROCCURREDWHILERETRIEVINGFILENAME|Falha na recuperação do nome de arquivo para um componente com o código de erro 0x%1!8.8X!.|  
|0xC0048007|-1073446905|DTS_E_CANNOTRETRIEVEPROPERTYFORCOMPONENT|Não é possível recuperar a propriedade "%1" do componente com a identificação %2!d!.|  
|0xC0048008|-1073446904|DTS_E_DUPLICATEIDFOUND|Tentando usar a ID %1!d! mais de uma vez na Tarefa de Fluxo de Dados.|  
|0xC0048009|-1073446903|DTS_E_CANNOTRETRIEVEBYLINEAGE|Não é possível recuperar um item por ID de linhagem de uma coleção que não contém colunas.|  
|0xC004800B|-1073446901|DTS_E_CANNOTMAPRUNTIMECONNECTIONMANAGER|Não é possível encontrar o gerenciador de conexões com a identificação "%1" na coleção de gerenciadores de conexão devido ao código de erro 0x%2!8.8X!. "%3" necessita desse gerenciador de conexões na coleção de gerenciadores de conexões de "%4". Verifique se um gerenciador de conexões na coleção de gerenciadores de conexões, Connections, foi criado com aquela ID.|  
|0xC004800E|-1073446898|DTS_E_INPUTNOTKNOWN|O thread "%1" recebeu um buffer para a entrada %2!d!, mas esse thread não é responsável por essa entrada. Ocorreu um erro, e o agendador do mecanismo Fluxo de Dados criou um plano de execução ruim.|  
|0xC004800F|-1073446897|DTS_E_GETRTINTERFACEFAILED|O componente "%1" (%2!d!) Não pode fornecer uma interface IDTSRuntimeComponent100.|  
|0xC0048011|-1073446895|DTS_E_CANTGIVEAWAYBUFFER|O mecanismo da tarefa Fluxo de Dados tentou copiar um buffer para atribuir a outro thread, mas falhou.|  
|0xC0048012|-1073446894|DTS_E_CANTCREATEVIEWBUFFER|O mecanismo da tarefa de Fluxo de Dados não criou um buffer de exibição do tipo %1!d! obre o tipo %2!d! para o buffer %3!d.|  
|0xC0048013|-1073446893|DTS_E_UNUSABLETEMPORARYPATH|O gerenciador de buffer não criou um arquivo temporário no caminho "%1". O caminho não será considerado novamente para armazenamento temporário.|  
|0xC0048014|-1073446892|DTS_E_DIRECTTONONERROROUTPUT|O gerenciador de buffer tentou forçar uma linha de erro em uma saída não registrada como saída de erro. Houve uma chamada para DirectErrorRow em uma saída cuja propriedade IsErrorOut não está definida como TRUE.|  
|0xC0048015|-1073446891|DTS_E_BUFFERISPRIVATE|Foi feita uma chamada para um método de buffer em um buffer privado, mas não existe suporte para esse tipo de operação em buffers privados.|  
|0xC0048016|-1073446890|DTS_E_BUFFERISFLAT|Não existe suporte para essa operação em buffers de modo privado.|  
|0xC0048017|-1073446889|DTS_E_BUFFERISPRIMEOUTPUT|Essa operação não pode ser chamada em um buffer passado para PrimeOutput. Foi feita uma chamada para um método de buffer durante PrimeOutput, mas essa chamada não é permitida durante PrimeOutput.|  
|0xC0048018|-1073446888|DTS_E_BUFFERISPROCESSINPUT|Essa operação não pode ser chamada em um buffer passado para ProcessInput. Foi feita uma chamada para um método de buffer durante ProcessInput, mas essa chamada não é permitida durante ProcessInput.|  
|0xC0048019|-1073446887|DTS_E_BUFFERGETTEMPFILENAME|O gerenciador de buffer não pôde adquirir um nome de arquivo temporário.|  
|0xC004801A|-1073446886|DTS_E_REFERENCECOLUMNTOOWIDE|O código encontrou uma coluna larga demais.|  
|0xC004801B|-1073446885|DTS_E_CANNOTGETRUNTIMECONNECTIONMANAGERID|Não é possível obter a identificação do gerenciador de conexões de tempo de execução especificado por "%1" na coleção de gerenciadores de conexões, Collections, de "%2", devido ao código de erro 0x%3!8.8X!. Verifique se a propriedade ConnectionManager.ID do objeto de conexão de tempo de execução foi definida para o componente.|  
|0xC004801C|-1073446884|DTS_E_EMPTYRUNTIMECONNECTIONMANAGERID|O "%1" na coleção de gerenciadores de conexões, Connections, de "%2" não tem um valor de propriedade de ID. Verifique se a propriedade ConnectionManagerID do objeto de conexão de tempo de execução foi definida para o componente.|  
|0xC004801D|-1073446883|DTS_E_METADATAREADONLY|Metadados não podem ser alterados durante a execução.|  
|0xC004801F|-1073446881|DTS_E_UPGRADEFAILED|Os metadados de componente para "%1" não pôde ser atualizado para a versão mais recente do componente. Houve falha no método PerformUpgrade.|  
|0xC0048020|-1073446880|DTS_E_COMPONENTVERSIONMISMATCH|A versão de %1 não é compatível com essa versão do DataFlow.|  
|0xC0048021|-1073446879|DTS_E_ERRORCOMPONENT|O componente está faltando, não está registrado, não é atualizável ou não possui as interfaces necessárias. As informações de contato desse componente são "%1".|  
|0xC0048022|-1073446878|DTS_E_BUFFERISNOTPRIMEOUTPUT|O método foi chamado no buffer errado. Não existe suporte para essa operação em buffers que não são usados para saída de componente.|  
|0xC0049014|-1073442796|DTS_E_EXPREVALSTATIC_COMPUTATIONFAILED|Ocorreu um erro durante a computação da expressão.|  
|0xC0049030|-1073442768|DTS_E_EXPREVALSTATIC_DIVBYZERO|Ocorreu uma divisão por zero na expressão.|  
|0xC0049031|-1073442767|DTS_E_EXPREVALSTATIC_LITERALOVERFLOW|A magnitude do valor literal era muito grande para o tipo solicitado.|  
|0xC0049032|-1073442766|DTS_E_EXPREVALSTATIC_BINARYOPNUMERICOVERFLOW|O resultado de uma operação binária era muito grande para o tamanho de máximo de tipos numéricos. Não foi possível converter implicitamente os tipos de operando em um resultado numérico (DT_NUMERIC) sem perda de precisão ou escala. Para executar essa operação, um ou ambos os operandos precisam ser convertidos explicitamente com um operador de conversão.|  
|0xC0049033|-1073442765|DTS_E_EXPREVALSTATIC_BINARYOPOVERFLOW|A magnitude do resultado de uma operação binária estoura o tamanho de máximo para tipo de dados de resultado.|  
|0xC0049034|-1073442764|DTS_E_EXPREVALSTATIC_FUNCTIONOVERFLOW|A magnitude do resultado de uma chamada de função era muito grande para o tipo de resultado e estourou o tipo do operando. Pode ser necessária uma conversão explícita para um tipo maior.|  
|0xC0049035|-1073442763|DTS_E_EXPREVALSTATIC_BINARYTYPEMISMATCH|Tipos de dados incompatíveis foram usados com um operador binário. Não foi possível converter de forma implícita os tipos de operando em tipos compatíveis para a operação. Para executar essa operação, um ou ambos os operandos precisam ser convertidos explicitamente com um operador de conversão.|  
|0xC0049036|-1073442762|DTS_E_EXPREVALSTATIC_UNSUPPORTEDBINARYTYPE|Um tipo de dados sem-suporte foi usado com um operador binário. Não existe suporte para a operação com o tipo de um ou ambos os operandos. Para executar essa operação, um ou ambos os operandos precisam ser convertidos explicitamente com um operador de conversão.|  
|0xC0049037|-1073442761|DTS_E_EXPREVALSTATIC_BINARYSIGNMISMATCH|Existe uma incompatibilidade de sinais para o operador binário bit a bit. Os operandos desse operador devem ser ambos positivos ou negativos.|  
|0xC0049038|-1073442760|DTS_E_EXPREVALSTATIC_BINARYOPERATIONFAILED|Falha em uma operação binária. Houve falta de memória, ou ocorreu um erro interno.|  
|0xC0049039|-1073442759|DTS_E_EXPREVALSTATIC_BINARYOPERATIONSETTYPEFAILED|Falha na definição do tipo de resultado de uma operação binária.|  
|0xC004903A|-1073442758|DTS_E_EXPREVALSTATIC_STRINGCOMPARISONFAILED|Não é possível comparar duas cadeias de caracteres.|  
|0xC004903B|-1073442757|DTS_E_EXPREVALSTATIC_UNSUPPORTEDUNNARYTYPE|Um tipo de dados sem-suporte foi usado com um operador unário. Não existe suporte para a operação com esse tipo de operando. Para executar essa operação, o operando precisa ser convertido explicitamente com um operador de conversão.|  
|0xC004903C|-1073442756|DTS_E_EXPREVALSTATIC_UNARYOPERATIONFAILED|Falha em uma operação unária. Houve falta de memória, ou ocorreu um erro interno.|  
|0xC004903D|-1073442755|DTS_E_EXPREVALSTATIC_UNARYOPERATIONSETTYPEFAILED|Falha na definição do tipo de resultado de uma operação unária.|  
|0xC004903E|-1073442754|DTS_E_EXPREVALSTATIC_PARAMTYPEMISMATCH|Uma função tem um parâmetro com um tipo de dados sem-suporte. Não é possível converter de forma implícita o tipo do parâmetro em um tipo compatível para a função. Para executar essa operação, o operando precisa ser convertido explicitamente com um operador de conversão.|  
|0xC004903F|-1073442753|DTS_E_EXPREVALSTATIC_INVALIDFUNCTION|Um nome de função inválido foi exibido na expressão. Verifique se o nome da função está correto e se realmente existe.|  
|0xC0049040|-1073442752|DTS_E_EXPREVALSTATIC_FNSUBSTRINGINVALIDLENGTH|O parâmetro de comprimento não era válido para a função SUBSTRING. O parâmetro de comprimento não pode ser negativo.|  
|0xC0049041|-1073442751|DTS_E_EXPREVALSTATIC_FNSUBSTRINGINVALIDSTARTINDEX|O índice inicial não era válido para a função SUBSTRING. O valor de índice inicial deve ser um número inteiro maior que zero. A base do índice inicial é 1, e não 0.|  
|0xC0049042|-1073442750|DTS_E_EXPREVALSTATIC_INVALIDNUMBEROFPARAMS|Um número incorreto de parâmetros foi atribuído a uma função. O nome da função foi reconhecido, mas o número de parâmetros não estava correto.|  
|0xC0049043|-1073442749|DTS_E_EXPREVALSTATIC_CHARMAPPINGFAILED|Falha em uma função de mapeamento de caracteres.|  
|0xC0049044|-1073442748|DTS_E_EXPREVALSTATIC_INVALIDDATEPART|Um parâmetro não reconhecido da parte de data foi especificado para uma função de data.|  
|0xC0049045|-1073442747|DTS_E_EXPREVALSTATIC_INVALIDNULLPARAM|Um parâmetro inválido foi atribuído à função NULL. Os parâmetros de NULL devem ser estáticos e não podem conter elementos dinâmicos, como colunas de entrada.|  
|0xC0049046|-1073442746|DTS_E_EXPREVALSTATIC_INVALIDNULLPARAMTYPE|Um parâmetro inválido foi atribuído à função NULL. Um parâmetro de NULL deve ser um número inteiro ou um tipo que possa ser convertido em inteiro.|  
|0xC0049047|-1073442745|DTS_E_EXPREVALSTATIC_FUNCTIONPARAMNOTSTATIC|Um parâmetro inválido foi atribuído a uma função. Esse parâmetro deve ser estático e não pode conter elementos dinâmicos, como colunas de entrada.|  
|0xC0049048|-1073442744|DTS_E_EXPREVALSTATIC_INVALIDCASTPARAM|Um parâmetro inválido foi atribuído a uma operação de conversão. Parâmetros de operadores de conversão devem ser estáticos e não podem conter elementos dinâmicos, como colunas de entrada.|  
|0xC0049049|-1073442743|DTS_E_EXPREVALSTATIC_INVALIDCASTPARAMTYPE|Um parâmetro inválido foi atribuído a uma operação de conversão. Um parâmetro de operador de conversão deve ser um número inteiro ou um tipo que possa ser convertido em inteiro.|  
|0xC004904A|-1073442742|DTS_E_EXPREVALSTATIC_INVALIDCAST|A expressão continha uma conversão de tipo sem-suporte.|  
|0xC004904B|-1073442741|DTS_E_EXPREVALSTATIC_INVALIDTOKEN|A expressão continha um token que não foi reconhecido. A expressão não pôde ser analisada porque contém elementos inválidos.|  
|0xC004904C|-1073442740|DTS_E_EXPREVALSTATIC_FAILEDTOPARSEEXPRESSION|A expressão não é válida e não pôde ser analisada. Ela pode conter elementos inválidos ou não estar bem formada.|  
|0xC004904D|-1073442739|DTS_E_EXPREVALSTATIC_UNARYOPOVERFLOW|O resultado de uma operação de subtração (negação) unária excedeu o tamanho máximo para tipo de dados de resultado. A magnitude do resultado da operação estoura o tipo do resultado.|  
|0xC004904E|-1073442738|DTS_E_EXPREVALSTATIC_COMPUTEFAILED|Falha na tentativa de computar a expressão.|  
|0xC004904F|-1073442737|DTS_E_EXPREVALSTATIC_BUILDSTRINGFAILED|Falha na tentativa de gerar uma representação de cadeia de caracteres da expressão.|  
|0xC0049050|-1073442736|DTS_E_EXPREVALSTATIC_CANNOTCONVERTRESULT|Não é possível converter o tipo de dados de resultado da expressão em tipo de dados de coluna. O resultado da expressão deve ser gravado em uma coluna de entrada/saída, mas o tipo de dados da expressão não pode ser convertido em tipo de dados da coluna.|  
|0xC0049051|-1073442735|DTS_E_EXPREVALSTATIC_CONDITIONALOPINVALIDCONDITIONTYPE|A expressão condicional do operador condicional tem um tipo de dados inválido. A expressão condicional deve ser do tipo DT_BOOL.|  
|0xC0049052|-1073442734|DTS_E_EXPREVALSTATIC_CONDITIONALOPTYPEMISMATCH|Os tipos de dados dos operandos do operador condicional eram incompatíveis. Não foi possível converter implicitamente os tipos de operandos em tipos compatíveis para a operação condicional. Para executar essa operação, um ou ambos os operandos precisam ser convertidos explicitamente com um operador de conversão.|  
|0xC0049053|-1073442733|DTS_E_EXPREVALSTATIC_CONDITIONALOPSETTYPEFAILED|Falha na definição do tipo de resultado de uma operação condicional.|  
|0xC0049054|-1073442732|DTS_E_EXPREVALSTATIC_INPUTCOLUMNNAMENOTFOUND|A coluna de entrada especificada não foi encontrada na coleção de colunas de entrada.|  
|0xC0049055|-1073442731|DTS_E_EXPREVALSTATIC_INPUTCOLUMNIDNOTFOUND|Falha na tentativa de encontrar uma coluna de entrada por ID de linhagem. A coluna de entrada não foi encontrada na coleção de colunas de entrada.|  
|0xC0049056|-1073442730|DTS_E_EXPREVALSTATIC_NOINPUTCOLUMNCOLLECTION|A expressão contém um token não reconhecido que parece ser uma referência de coluna de entrada, mas a coleção de colunas de entrada não está disponível para processar colunas de entrada. A coleção de colunas de entrada não foi fornecida ao avaliador de expressão, mas uma coluna de entrada foi incluída na expressão.|  
|0xC0049057|-1073442729|DTS_E_EXPREVALSTATIC_VARIABLENOTFOUND|Uma variável especificada não foi encontrada na coleção. A variável pode não existir no escopo correto. Verifique se a variável existe e se escopo está correto.|  
|0xC0049058|-1073442728|DTS_E_EXPREVALSTATIC_INVALIDTOKENSTATE|Falha na tentativa de análise da expressão. A expressão contém um token inválido ou incompleto. Ela pode conter elementos inválidos, não ter parte de um elemento necessário, como fechar parênteses, ou não estar bem formada.|  
|0xC0049059|-1073442727|DTS_E_EXPREVALSTATIC_INVALIDCASTCODEPAGE|O valor especificado para o parâmetro de página de código da conversão em tipo de dados DT_STR ou DT_TEXT não é válido. A página de código especificada não está instalada no computador.|  
|0xC004905A|-1073442726|DTS_E_EXPREVALSTATIC_INVALIDCASTPRECISION|O valor especificado para o parâmetro de precisão de uma operação de conversão está fora do intervalo para conversão de tipos.|  
|0xC004905B|-1073442725|DTS_E_EXPREVALSTATIC_INVALIDCASTSCALE|O valor especificado para o parâmetro de escala de uma operação de conversão está fora do intervalo para conversão de tipos. A escala não deve exceder a precisão e não deve ser negativa.|  
|0xC004905C|-1073442724|DTS_E_EXPREVALSTATIC_CONDITIONALOPCODEPAGEMISMATCH|As páginas de código não correspondem em uma operação condicional. A página de código do operando à esquerda não corresponde à página de código do operando à direita. Para o operador condicional desse tipo, as páginas de código devem ser as mesmas.|  
|0xC004905D|-1073442723|DTS_E_EXPREVALSTATIC_ILLEGALHEXESCAPEINSTRINGLITERAL|Um valor literal da cadeia de caracteres contém uma sequência de escape hexadecimal ilegal. A sequência de escape não tem suporte em valores literais da cadeia de caracteres no avaliador de expressões. As sequências de escape hexadecimais devem ser do formato \xhhhh onde h seja um dígito hexadecimal válido.|  
|0xC004905E|-1073442722|DTS_E_EXPREVALSTATIC_ILLEGALESCAPEINSTRINGLITERAL|O valor literal da cadeia de caracteres contém uma sequência de escape ilegal. A sequência de escape não tem suporte em valores literais da cadeia de caracteres no avaliador de expressões. Se uma cadeia de caracteres requer uma barra invertida, formate-a com duas barras, "\\\\".|  
|0xC004905F|-1073442721|DTS_E_EXPREVALSTATIC_UNSUPPORTEDTYPE|Um tipo de dados sem-suporte ou não reconhecido foi usado na expressão.|  
|0xC0049060|-1073442720|DTS_E_EXPREVALSTATIC_DATACONVERSIONOVERFLOW|Ocorreu um estouro durante a conversão entre tipos de dados. O tipo de origem é muito grande para o tipo de destino.|  
|0xC0049061|-1073442719|DTS_E_EXPREVALSTATIC_DATACONVERSIONNOTSUPPORTED|A expressão contém uma conversão de tipo de dados sem-suporte. O tipo de origem não pode ser convertido no tipo de destino.|  
|0xC0049062|-1073442718|DTS_E_EXPREVALSTATIC_DATACONVERSIONFAILED|Ocorreu um erro durante a tentativa de conversão de dados. O tipo de origem não pôde ser convertido no tipo de destino.|  
|0xC0049063|-1073442717|DTS_E_EXPREVALSTATIC_CONDITIONALOPERATIONFAILED|Falha na operação condicional.|  
|0xC0049064|-1073442716|DTS_E_EXPREVALSTATIC_CASTFAILED|Ocorreu um erro durante uma tentativa de conversão de tipo.|  
|0xC0049065|-1073442715|DTS_E_EXPREVALFAILEDTOCONVERTSTRCOLUMNTOWSTR|Falha na conversão de "%1" do tipo DT_STR no tipo DT_WSTR com o código de erro 0x%2!8.8X!. Ocorreu um erro durante a conversão implícita na coluna de entrada.|  
|0xC0049066|-1073442714|DTS_E_EXPREVALSTATIC_FAILEDTOCONVERTSTRCOLUMNTOWSTR|Falha na conversão de uma coluna de entrada do tipo DT_STR em tipo DT_WSTR. Ocorreu um erro durante a conversão implícita na coluna de entrada.|  
|0xC0049067|-1073442713|DTS_E_EXPREVALSTATIC_FUNCTIONCOMPUTEFAILED|Ocorreu um erro durante a avaliação da função.|  
|0xC0049068|-1073442712|DTS_E_EXPREVALSTATIC_FUNCTIONCONVERTPARAMTOMEMBERFAILED|Um parâmetro de função não pode ser convertido em valor estático. O parâmetro deve ser estático e não pode conter elementos dinâmicos, como colunas de entrada.|  
|0xC0049088|-1073442680|DTS_E_EXPREVALSTATIC_FNRIGHTINVALIDLENGTH|O parâmetro de comprimento não é válido para a função RIGHT. O parâmetro de comprimento não pode ser negativo.|  
|0xC0049089|-1073442679|DTS_E_EXPREVALSTATIC_FNREPLICATEINVALIDREPEATCOUNT|O parâmetro de contagem de repetições não é válido para a função REPLICATE. Esse parâmetro não pode ser negativo.|  
|0xC0049096|-1073442666|DTS_E_EXPREVALSTATIC_BINARYOPERATORCODEPAGEMISMATCH|As páginas de código não correspondem em uma operação binária. A página de código do operando à esquerda não corresponde à página de código do operando à direita. Para essa operação binária, as páginas de código devem ser a mesma.|  
|0xC0049097|-1073442665|DTS_E_EXPREVALSTATIC_VARIABLECOMPUTEFAILED|Falha na recuperação do valor para uma variável.|  
|0xC0049098|-1073442664|DTS_E_EXPREVALSTATIC_VARIABLETYPENOTSUPPORTED|A expressão contém uma variável com um tipo de dados sem-suporte.|  
|0xC004909B|-1073442661|DTS_E_EXPREVALSTATIC_CASTCODEPAGEMISMATCH|Não é possível converter a expressão porque a página de código do valor que está sendo convertido não corresponde à página solicitada de código de resultado. A página de código da origem deve corresponder à página de código de destino solicitada.|  
|0xC004909C|-1073442660|DTS_E_EXPREVALSTATIC_INVALIDTOKENSINGLEQUOTE|A expressão contém uma aspa simples inesperada. Podem ser necessárias aspas duplas.|  
|0xC004909D|-1073442659|DTS_E_EXPREVALSTATIC_INVALIDTOKENSINGLEEQUAL|A expressão contém um sinal de igualdade (=) inesperado. Esse erro normalmente ocorre quando são necessários dois sinais de igualdade (==).|  
|0xC00490AA|-1073442646|DTS_E_EXPREVALSTATIC_AMBIGUOUSINPUTCOLUMNNAME|Foi especificado um nome ambíguo de coluna de entrada.  A coluna deve ser qualificada como [Nome do Componente].[Nome da Coluna] ou referenciada por ID de linhagem. Esse erro ocorre quando a coluna de entrada existe em mais de um componente e deve ser diferenciada adicionando o nome do componente ou usando a ID de linhagem.|  
|0xC00490AB|-1073442645|DTS_E_EXPREVALSTATIC_PLACEHOLDERINEXPRESSION|Foi encontrado um parâmetro de função de espaço reservado ou um operando em uma expressão. Ele deve ser substituído por um operando ou parâmetro real.|  
|0xC00490AC|-1073442644|DTS_E_EXPREVALSTATIC_AMBIGUOUSVARIABLENNAME|Um nome ambíguo de variável foi especificado. A variável desejada deve ser qualificada como \@ [Namespace::Variable]. Esse erro ocorre quando a variável existe em mais de um namespace.|  
|0xC00490D3|-1073442605|DTS_E_EXPREVALSTATIC_BINARYOPDTSTRNOTSUPPORTED|Para operandos de operação binária, existe suporte apenas para colunas de entrada e operações de conversão de tipo de dados DT_STR. Um operando DT_STR que não é uma coluna de entrada ou o resultado de uma conversão não pode ser usado com uma operação binária. Para executar essa operação, o operando precisa ser convertido explicitamente com um operador de conversão.|  
|0xC00490D4|-1073442604|DTS_E_EXPREVALSTATIC_CONDITIONALOPDTSTRNOTSUPPORTED|Para operandos de um operador condicional, existe suporte apenas para colunas de entrada e operações de conversão de tipo de dados DT_STR. Um operando DT_STR que não é uma coluna de entrada ou o resultado de uma conversão não pode ser usado com a operação condicional. Para executar essa operação, o operando precisa ser convertido explicitamente com um operador de conversão.|  
|0xC00490D5|-1073442603|DTS_E_EXPREVALSTATIC_FNFINDSTRINGINVALIDOCCURRENCECOUNT|O parâmetro de contagem de ocorrências não é válido para função FINDSTRING. Esse parâmetro deve ser maior que zero.|  
|0xC00490DD|-1073442595|DTS_E_EXPREVALSTATIC_INVALIDDATEPARTNODE|O parâmetro "parte de data" especificado para uma função de data não é válido. Os parâmetros "parte de data" devem ser cadeias de caracteres estáticas e não podem conter elementos dinâmicos como colunas de entrada. Eles devem ser do tipo DT_WSTR.|  
|0xC00490DE|-1073442594|DTS_E_EXPREVALSTATIC_INVALIDCASTLENGTH|O valor especificado para o parâmetro de comprimento de uma operação de conversão não é válido. O comprimento deve ser positivo. O comprimento especificado para a conversão de tipo é negativo. Altere para um valor positivo.|  
|0xC00490DF|-1073442593|DTS_E_EXPREVALSTATIC_INVALIDNULLLENGTH|O valor especificado para parâmetro de comprimento de uma função NULL não é válido. O comprimento deve ser positivo. O comprimento especificado para a NULL função é negativo. Altere para um valor positivo.|  
|0xC00490E0|-1073442592|DTS_E_EXPREVALSTATIC_INVALIDNULLCODEPAGE|O valor especificado para o parâmetro de página de código da função NULL com o tipo de dados DT_STR ou DT_TEXT não é válido. A página de código especificada não foi instalada no computador. Altere a página de código que está especificada ou instale a página de código no computador.|  
|0xC00490E1|-1073442591|DTS_E_EXPREVALSTATIC_INVALIDNULLPRECISION|O valor especificado para o parâmetro de precisão de uma função NULL não é válido. A precisão especificada está fora do intervalo para a função NULL.|  
|0xC00490E2|-1073442590|DTS_E_EXPREVALSTATIC_INVALIDNULLSCALE|O valor especificado para o parâmetro de escala de uma função NULL não é válido. A escala especificada está fora do intervalo da função NULL. A escala não deve exceder a precisão e deve ser positivo.|  
|0xC00490E8|-1073442584|DTS_E_XMLSRCERRORSETTINGERROROUTPUTCOLUMNDATA|Falha em %1 no ao tentar gravar dados em %2 em %3. %4|  
|0xC00490F5|-1073442571|DTS_E_TXLOOKUP_CANCEL_REQUESTED|A transformação da pesquisa recebeu do usuário uma solicitação de cancelamento.|  
|0xC00490F6|-1073442570|DTS_E_LOBLENGTHLIMITEXCEEDED|O processamento de dados de caractere ou de LOB (objeto binário grande) foi interrompido porque o limite de 4 GB foi alcançado.|  
|0xC00490F7|-1073442569|DTS_E_CANNOTLOADCOMPONENT|O componente de pipeline gerenciado "%1" não pôde ser carregado.  A exceção foi %2.|  
|0xC00F9304|-1072721148|DTS_E_OLEDB_EXCEL_NOT_SUPPORTED|Código de erro SSIS DTS_E_OLEDB_EXCEL_NOT_SUPPORTED: não há suporte para o Gerenciador de conexões do Excel nas versões de 64 bits do SSIS, pois não há um provedor OLE DB disponível.|  
|0xC00F9310|-1072721136|DTS_E_CACHEBADHEADER|O arquivo de cache está danificado ou não foi criado usando o gerenciador de conexões do Cache.  Forneça um arquivo de cache válido.|  
|0xC0202001|-1071636479|DTS_E_MISSINGSQLCOMMAND|O comando SQL não foi definido corretamente. Verifique a propriedade SQLCommand.|  
|0xC0202002|-1071636478|DTS_E_COMERROR|Estão disponíveis informações de objeto de erro COM.  Origem: "%1" código de erro: 0x%2!8.8X!  Descrição: "%3".|  
|0xC0202003|-1071636477|DTS_E_ACQUIREDCONNECTIONUNAVAILABLE|Não é possível acessar as conexões adquiridas.|  
|0xC0202004|-1071636476|DTS_E_INCORRECTCOLUMNCOUNT|O número de colunas está incorreto.|  
|0xC0202005|-1071636475|DTS_E_COLUMNNOTFOUND|Não é possível encontrar a coluna "%1" na fonte de dados.|  
|0xC0202007|-1071636473|DTS_E_OLEDBRECORD|Está disponível um registro OLE DB.  Origem: "%1"  Hresult: 0x%2!8.8X!  Descrição: "%3".|  
|0xC0202009|-1071636471|DTS_E_OLEDBERROR|Código de Erro SSIS DTS_E_OLEDBERROR.  Ocorreu um erro OLE DB. Código de erro: 0x%1!8.8X!.|  
|0xC020200A|-1071636470|DTS_E_ALREADYCONNECTED|O componente já está conectado. O componente precisa ser desconectado antes de tentar conectá-lo.|  
|0xC020200B|-1071636469|DTS_E_INCORRECTSTOCKPROPERTYVALUE|O valor da propriedade "%1" está incorreto.|  
|0xC020200E|-1071636466|DTS_E_CANNOTOPENDATAFILE|Não é possível abrir o arquivo de dados "%1".|  
|0xC0202010|-1071636464|DTS_E_DESTINATIONFLATFILEREQUIRED|Não foi fornecido nenhum nome de arquivo simples de destino. Certifique-se de que o gerenciador de conexões de arquivos simples esteja configurado com uma cadeia de caracteres de conexão. Se o gerenciador de conexões de arquivos simples for usado por vários componentes, verifique se a cadeia de caracteres de conexão contém nomes de arquivo suficientes.|  
|0xC0202011|-1071636463|DTS_E_TEXTQUALIFIERNOTFOUND|Não é possível encontrar o qualificador de texto para a coluna "%1".|  
|0xC0202014|-1071636460|DTS_E_CANNOTCONVERTTYPES|Não há suporte para conversão de "%1" para "%2".|  
|0xC0202015|-1071636459|DTS_E_PROBLEMDETECTINGTYPECOMPATIBILITY|O código de erro 0x%1!8.8X! foi retornado ao validar a conversão de tipo de %2 em %3.|  
|0xC0202016|-1071636458|DTS_E_CANNOTMAPINPUTCOLUMNTOOUTPUTCOLUMN|Não é possível encontrar a coluna de entrada com a ID de linhagem "%1!d!" que é necessária para "%2". Verifique a propriedade personalizada SourceInputColumnLineageID da coluna de saída.|  
|0xC0202017|-1071636457|DTS_E_INCORRECTMINIMUMNUMBEROFOUTPUTS|O número de saídas está incorreto. É necessário haver pelo menos %1!d! saídas.|  
|0xC0202018|-1071636456|DTS_E_INCORRECTEXACTNUMBEROFOUTPUTS|O número de saídas está incorreto. É necessário haver exatamente %1!d! saída(s).|  
|0xC0202019|-1071636455|DTS_E_STRINGCONVERSIONTOOLONG|Uma cadeia de caracteres era muito longa para ser convertida.|  
|0xC020201A|-1071636454|DTS_E_INCORRECTEXACTNUMBEROFINPUTS|O número de entradas está incorreto. É necessário haver exatamente %1!d! entradas.|  
|0xC020201B|-1071636453|DTS_E_CANNOTHAVEZEROINPUTCOLUMNS|O número de colunas de entrada para %1 não pode ser zero.|  
|0xC020201C|-1071636452|DTS_E_CANNOTHAVEINPUTS|Este componente tem %1!d! entradas.  Nenhuma entrada é permitida nesse componente.|  
|0xC020201D|-1071636451|DTS_E_PROCESSINPUTCALLEDWITHINVALIDINPUTID|ProcessInput foi chamado com uma identificação de entrada inválida de %1!d!.|  
|0xC020201F|-1071636449|DTS_E_INCORRECTCUSTOMPROPERTYTYPE|A propriedade personalizada "%1" precisa ser do tipo %2.|  
|0xC0202020|-1071636448|DTS_E_INVALIDBUFFERTYPE|O tipo de buffer não é válido. Verifique se o layout do Pipeline e de todos os componentes foram validados.|  
|0xC0202021|-1071636447|DTS_E_INCORRECTCUSTOMPROPERTYVALUE|O valor da propriedade personalizada "%1" está incorreto.|  
|0xC0202022|-1071636446|DTS_E_CONNECTIONREQUIREDFORMETADATA|Ocorreu um erro por causa da falta de conexão. É necessária uma conexão quando se solicitam metadados. Se você estiver trabalhando offline, desmarque a opção Trabalhar Offline no menu SSIS para habilitar a conexão.|  
|0xC0202023|-1071636445|DTS_E_CANTCREATECUSTOMPROPERTY|Não é possível criar a propriedade personalizada "%1".|  
|0xC0202024|-1071636444|DTS_E_CANTGETCUSTOMPROPERTYCOLLECTION|Não é possível recuperar a coleção de propriedades personalizadas para inicialização.|  
|0xC0202025|-1071636443|DTS_E_CANNOTCREATEACCESSOR|Não é possível criar um acessador OLE DB. Verifique se os metadados da coluna são válidos.|  
|0xC0202026|-1071636442|DTS_E_PRIMEOUTPUTCALLEDWITHINVALIDOUTPUTID|PrimeOutput foi chamado com uma identificação de saída inválida de %1!d!.|  
|0xC0202027|-1071636441|DTS_E_INCORRECTSTOCKPROPERTY|O valor da propriedade "%1" em "%2" não é válido.|  
|0xC0202028|-1071636440|DTS_E_CONNECTIONREQUIREDFORREAD|É necessária uma conexão para ler dados.|  
|0xC020202C|-1071636436|DTS_E_ERRORWHILEREADINGHEADERROWS|Ocorreu um erro durante a leitura das linhas de cabeçalho.|  
|0xC020202D|-1071636435|DTS_E_DUPLICATECOLUMNNAME|Nome de coluna "%1" duplicado.|  
|0xC0202030|-1071636432|DTS_E_CANNOTGETCOLUMNNAME|Não é possível obter o nome da coluna com a identificação %1!d!.|  
|0xC0202031|-1071636431|DTS_E_CANTDIRECTROW|Falha no direcionamento da linha para a saída "%1" (%2!d!).|  
|0xC020203A|-1071636422|DTS_E_CANNOTCREATEBULKINSERTHREAD|Não é possível criar o thread de inserção em massa por causa do erro "%1".|  
|0xC020203B|-1071636421|DTS_E_BULKINSERTHREADINITIALIZATIONFAILED|Falha na inicialização do thread para a tarefa Inserção em Massa do SSIS.|  
|0xC020203E|-1071636418|DTS_E_BULKINSERTTHREADALREADYRUNNING|O thread para a tarefa Inserção em Massa do SSIS já está em execução.|  
|0xC020203F|-1071636417|DTS_E_BULKINSERTTHREADABNORMALCOMPLETION|O thread para a tarefa Inserção em Massa do SSIS foi encerrado com erros ou avisos.|  
|0xC0202040|-1071636416|DTS_E_CANNOTGETIROWSETFASTLOAD|Falha ao abrir um conjunto de linhas de carregamento rápido para "%1". Verifique se o objeto existe no banco de dados.|  
|0xC0202041|-1071636415|DTS_E_CONNECTREQUIREDFORMETADATAVALIDATION|Erro devido à falta de conexão. É necessária uma conexão antes de a validação de metadados prosseguir.|  
|0xC0202042|-1071636414|DTS_E_DESTINATIONTABLENAMENOTPROVIDED|Não foi fornecido um nome de tabela de destino.|  
|0xC0202043|-1071636413|DTS_E_ICONVERTTYPEUNAVAILABLE|O provedor OLE DB usado pelo adaptador OLE DB não fornece suporte a IConvertType. Defina a propriedade ValidateColumnMetaData do adaptador como FALSE.|  
|0xC0202044|-1071636412|DTS_E_OLEDBPROVIDERDATATYPECONVERSIONUNSUPPORTED|O provedor OLE DB usado pelo adaptador OLE DB não faz conversão entre os tipos "%1" e "%2" para "%3".|  
|0xC0202045|-1071636411|DTS_E_VALIDATECOLUMNMETADATAFAILED|Falha na validação de metadados de coluna.|  
|0xC0202047|-1071636409|DTS_E_ATTEMPTINGTOINSERTINTOAROWIDCOLUMN|"%1" é uma coluna de ID de linha e não pode ser incluída em uma operação de inserção de dados.|  
|0xC0202048|-1071636408|DTS_E_ATTEMPTINGTOINSERTINTOAROWVERCOLUMN|Tentando inserir na coluna de versão de linha "%1". Não é possível inserir em uma coluna de versão de linha.|  
|0xC0202049|-1071636407|DTS_E_ATTEMPTINGTOINSERTINTOAREADONLYCOLUMN|Falha ao inserir na coluna somente leitura "%1".|  
|0xC020204A|-1071636406|DTS_E_UNABLETORETRIEVECOLUMNINFO|Não é possível recuperar as informações de coluna da fonte de dados. Certifique-se de que sua tabela de destino no banco de dados esteja disponível.|  
|0xC020204B|-1071636405|DTS_E_CANTLOCKBUFFER|Não foi possível bloquear um buffer. O sistema está sem memória ou o gerenciador de buffer atingiu sua cota.|  
|0xC020204C|-1071636404|DTS_E_INVALIDCOMPARISONFLAGS|O %1 tem uma propriedade ComparisonFlags que inclui sinalizadores extras com o valor %2!d!.|  
|0xC020204D|-1071636403|DTS_E_COLUMNMETADATAUNAVAILABLEFORVALIDATION|Os metadados de coluna não estavam disponíveis para validação.|  
|0xC0202053|-1071636397|DTS_E_CANNOTWRITETODATAFILE|Não é possível gravar no arquivo de dados.|  
|0xC0202055|-1071636395|DTS_E_COLUMNDELIMITERNOTFOUND|O delimitador de colunas para a coluna "%1" não foi encontrado.|  
|0xC0202058|-1071636392|DTS_E_COLUMNPARSEFAILED|Falha ao analisar a coluna "%1" no arquivo de dados.|  
|0xC020205A|-1071636390|DTS_E_RAWFILENAMEREQUIRED|O nome de arquivo não está especificado corretamente.  Forneça o caminho e o nome para o arquivo bruto diretamente na propriedade FileName ou especificando uma variável na propriedade FileNameVariable.|  
|0xC020205B|-1071636389|DTS_E_RAWFILECANTOPEN|O arquivo "%1" não pode ser aberto para gravação. O erro pode ocorrer quando não há privilégios de arquivo ou o disco está cheio.|  
|0xC020205C|-1071636388|DTS_E_RAWFILECANTBUFFER|Um buffer de E/S não pode ser criado para o arquivo de saída. O erro pode ocorrer quando não há privilégios de arquivo ou o disco está cheio.|  
|0xC020205D|-1071636387|DTS_E_RAWCANTWRITE|Não é possível gravar %1!d! bytes no arquivo "%2". Para obter detalhes, consulte as mensagens de erro anteriores.|  
|0xC020205E|-1071636386|DTS_E_RAWBADHEADER|Foram encontrados metadados inválidos no cabeçalho do arquivo. O arquivo está danificado ou não é arquivo de dados brutos produzidos pelo SSIS.|  
|0xC020205F|-1071636385|DTS_E_RAWEXISTSCREATEONCE|O erro ocorreu porque o arquivo de saída já existe e WriteOption está definido como Criar Uma Vez. Defina a propriedade WriteOption como Criar Sempre, ou exclua o arquivo.|  
|0xC0202060|-1071636384|DTS_E_RAWCANTAPPENDTRUNCATE|Erro causado por configurações de propriedade conflitantes. A propriedade AllowAppend e ForceTruncate estão definidas como TRUE. Ambas as propriedades não podem ser definidas como TRUE. Defina uma das duas propriedades como FALSE.|  
|0xC0202061|-1071636383|DTS_E_RAWBADVERSION|O arquivo continha informações inválidas de sinalizadores e versão. O arquivo está danificado ou não é arquivo de dados brutos produzidos pelo SSIS.|  
|0xC0202062|-1071636382|DTS_E_RAWVERSIONINCOMPATIBLEAPPEND|O arquivo de saída foi gravado por uma versão incompatível e não pode ser anexado. O arquivo pode ser de um formato antigo não mais usado.|  
|0xC0202064|-1071636380|DTS_E_RAWMETADATAMISMATCH|Não é possível anexar o arquivo de saída porque nenhuma coluna no arquivo existente corresponde à coluna "%1" da entrada. Os metadados do arquivo artigo não coincidem.|  
|0xC0202065|-1071636379|DTS_E_RAWMETADATACOUNTMISMATCH|Não é possível anexar o arquivo de saída porque o número de colunas no arquivo de saída não corresponde ao número de colunas nesse destino. Os metadados do arquivo antigo não coincidem.|  
|0xC0202067|-1071636377|DTS_E_ERRORRETRIEVINGCOLUMNCODEPAGE|Houve um erro durante a recuperação das informações de página de código de coluna.|  
|0xC0202068|-1071636376|DTS_E_RAWCANTREAD|Não é possível ler %1!d! bytes do arquivo "%2". A causa da falha deve ter sido informada anteriormente.|  
|0xC0202069|-1071636375|DTS_E_RAWUNEXPECTEDEOF|Encontrado um fim de arquivo inesperado durante a leitura de %1!d! bytes do arquivo "%2". O arquivo foi terminado prematuramente por causa de um formato de arquivo inválido.|  
|0xC020206A|-1071636374|DTS_E_RAWNOLONGTYPES|A coluna %1 não pode ser usada. Os adaptadores brutos não fornecem suporte a imagem, texto ou dados ntext.|  
|0xC020206B|-1071636373|DTS_E_RAWUNEXPECTEDTYPE|O adaptador encontrou um tipo de dados não reconhecido de %1!d!. Isso pode ser causado por um arquivo de entrada danificado (origem) ou por um tipo de buffer inválido (destino).|  
|0xC020206C|-1071636372|DTS_E_RAWSTRINGTOOLONG|A cadeia de caracteres é muito longa. O adaptador leu uma cadeia de caracteres que era %1!d! bytes e esperava uma cadeia de caracteres com não mais de %2!d! bytes, no deslocamento %3!d!. Isso pode indicar um arquivo de entrada danificado. O arquivo mostra um comprimento da cadeia de caracteres muito longo para a coluna de buffer.|  
|0xC020206E|-1071636370|DTS_E_RAWSKIPFAILED|O adaptador bruto tentou ignorar %1!d! bytes no arquivo de entrada para a coluna não referenciada "%2" com a ID de linhagem %3, mas houve erro. O erro retornado pelo sistema operacional pode ter sido previamente informado.|  
|0xC020206F|-1071636369|DTS_E_RAWREADFAILED|O adaptador bruto tentou ler %1!d! bytes no arquivo de entrada para a coluna "%2" com a ID de linhagem %3, mas houve erro. O erro retornado pelo sistema operacional pode ter sido previamente informado.|  
|0xC0202070|-1071636368|DTS_E_RAWFILENAMEINVALID|A propriedade de nome de arquivo não é válida. O nome de arquivo é um dispositivo ou contém caracteres inválidos.|  
|0xC0202071|-1071636367|DTS_E_BULKINSERTAPIPREPARATIONFAILED|Não é possível preparar a inserção em massa do SSIS para inserção de dados.|  
|0xC0202072|-1071636366|DTS_E_INVALIDDATABASEOBJECTNAME|O nome de objeto "%1" do banco de dados não é válido.|  
|0xC0202073|-1071636365|DTS_E_INVALIDORDERCLAUSE|A cláusula de ordem não é válida.|  
|0xC0202074|-1071636364|DTS_E_RAWFILECANTOPENREAD|O arquivo "%1" não pode ser aberto para leitura. O erro pode ocorrer quando não há privilégios ou o arquivo não é encontrado. A causa exata é informada em mensagem prévia de erro.|  
|0xC0202075|-1071636363|DTS_E_TIMEGENCANTCREATE|Não é possível criar o Microsoft.AnalysisServices.TimeDimGenerator.TimeDimGenerator.|  
|0xC0202076|-1071636362|DTS_E_TIMEGENCANTCONFIGURE|Não é possível configurar o Microsoft.AnalysisServices.TimeDimGenerator.|  
|0xC0202077|-1071636361|DTS_E_TIMEGENCANTCONVERT|Tipo de dados sem-suporte para a coluna %1!d!.|  
|0xC0202079|-1071636359|DTS_E_TIMEGENCANTREAD|Falha na tentativa de leitura de Microsoft.AnalysisServices.TimeDimGenerator com o código de erro 0x%1!8.8X!.|  
|0xC020207A|-1071636358|DTS_E_TIMEGENCANTREADCOLUMN|Falha com código de erro 0x%2!8.8X! ao tentar ler a coluna "%2!d!" do Microsoft.AnalysisServices.TimeDimGenerator.|  
|0xC020207B|-1071636357|DTS_E_RSTDESTBADVARIABLENAME|A propriedade VariableName não está definida como o nome de uma variável válida. É necessária uma variável de tempo de execução para permitir a gravação.|  
|0xC020207C|-1071636356|DTS_E_RSTDESTRSTCONFIGPROBLEM|Não é possível criar ou configurar o objeto ADODB.Recordset.|  
|0xC020207D|-1071636355|DTS_E_RSTDESTRSTWRITEPROBLEM|Erro durante a gravação no objeto ADODB.Recordset.|  
|0xC020207E|-1071636354|DTS_E_FILENAMEINVALID|O nome de arquivo não é válido. O nome de arquivo é um dispositivo ou contém caracteres inválidos.|  
|0xC020207F|-1071636353|DTS_E_FILENAMEINVALIDWITHPARAM|O nome de arquivo "%1" não é válido. O nome de arquivo é um dispositivo ou contém caracteres inválidos.|  
|0xC0202080|-1071636352|DTS_E_CMDDESTNOPARAMS|Não é possível recuperar as descrições da coluna de destino dos parâmetros do comando SQL.|  
|0xC0202081|-1071636351|DTS_E_CMDDESTNOTBOUND|Os parâmetros não estão associados. Todos os parâmetros no comando SQL devem ser associados às colunas de entrada.|  
|0xC0202082|-1071636350|DTS_E_TXPIVOTBADUSAGE|O valor de PivotUsage para a coluna de entrada "%1" (%2!d!) não é válido.|  
|0xC0202083|-1071636349|DTS_E_TXPIVOTTOOMANYPIVOTKEYS|Foram encontradas Chaves Dinâmicas em excesso. Apenas uma coluna de entrada pode ser usada como Chave Dinâmica.|  
|0xC0202084|-1071636348|DTS_E_TXPIVOTNOPIVOTKEY|Não foi encontrada nenhuma Chave Dinâmica. Uma coluna de entrada deve ser usada como Chave Dinâmica.|  
|0xC0202085|-1071636347|DTS_E_TXPIVOTINPUTALREADYMAPPED|Mais de uma coluna de saída (como "%1" (%2!d!)) mapeada para a coluna de entrada "%3" (%4!d!).|  
|0xC0202086|-1071636346|DTS_E_TXPIVOTCANTMAPPIVOTKEY|Não é possível mapear a coluna de saída "%1" (%2!d!) para a coluna de entrada PivotKey.|  
|0xC0202087|-1071636345|DTS_E_TXPIVOTCANTMAPPINGNOTFOUND|A coluna de saída "%1" (%2!d!) tem um SourceColumn %3!d! que não é uma identificação de linhagem de coluna de entrada válida.|  
|0xC0202088|-1071636344|DTS_E_TXPIVOTEMPTYPIVOTKEYVALUE|A coluna de saída "%1" (%2!d!) está mapeada para uma coluna de entrada de Valor Dinâmico, mas o valor da sua propriedade PivotKeyValue está faltando.|  
|0xC0202089|-1071636343|DTS_E_TXPIVOTDUPLICATEPIVOTKEYVALUE|A coluna de saída "%1" (%2!d!) está mapeada para uma coluna de entrada de Valor Dinâmico com um valor de propriedade PivotKeyValue não exclusivo.|  
|0xC020208A|-1071636342|DTS_E_TXPIVOTOUTPUTNOTMAPPED|A coluna de entrada "%1" (%2!d!) não está mapeada para nenhuma coluna de saída.|  
|0xC020208B|-1071636341|DTS_E_TXPIVOTCANTCOMPARESETKEYS|Ocorreu uma falha durante a comparação de valores para as chaves definidas.|  
|0xC020208D|-1071636339|DTS_E_TXPIVOTNOBLOB|Não é possível usar a coluna de Entrada "%1" (%2!d!) como Set Key, Pivot Key ou Pivot Value porque ela contém dados long.|  
|0xC020208E|-1071636338|DTS_E_TXPIVOTBADOUTPUTTYPE|Tipo de saída incorreto. A coluna de saída "%1" (%2!d!) deve ter o mesmo tipo de dados e metadados que a coluna de entrada para a qual está mapeada.|  
|0xC020208F|-1071636337|DTS_E_TXPIVOTPROCESSERROR|Falha durante a tentativa de dinamizar os registros de origem.|  
|0xC0202090|-1071636336|DTS_E_TXPIVOTBADPIVOTKEYVALUE|O valor de chave dinâmica "%1" não é válido.|  
|0xC0202091|-1071636335|DTS_E_ERRORWHILESKIPPINGDATAROWS|Ocorreu um erro ao ignorar as linhas de dados.|  
|0xC0202092|-1071636334|DTS_E_ERRORWHILEREADINGDATAROWS|Erro ao processar o arquivo "%1" na linha de dados %2!I64d!.|  
|0xC0202093|-1071636333|DTS_E_FAILEDTOINITIALIZEFLATFILEPARSER|Ocorreu um erro durante a inicialização do analisador de arquivo simples.|  
|0xC0202094|-1071636332|DTS_E_UNABLETORETRIEVECOLUMNINFOFROMFLATFILECONNECTIONMANAGER|Não é possível recuperar as informações de coluna do gerenciador de conexões de arquivos simples.|  
|0xC0202095|-1071636331|DTS_E_FAILEDTOWRITEOUTCOLUMNNAME|Falha ao gravar o nome para a coluna "%1".|  
|0xC0202096|-1071636330|DTS_E_INVALIDFLATFILECOLUMNTYPE|O tipo da coluna "%1" está incorreto. É do tipo "%2". Só pode ser "%3" ou "%4".|  
|0xC0202097|-1071636329|DTS_E_DISKIOBUFFEROVERFLOW|Falha na tentativa de gravar dados de %1!d! bytes no disco de E/S. O buffer de E/S do disco tem %2!d! bytes livres.|  
|0xC0202098|-1071636328|DTS_E_FAILEDTOWRITEOUTHEADER|Ocorreu um erro durante a gravação do cabeçalho de arquivo.|  
|0xC0202099|-1071636327|DTS_E_FAILEDTOGETFILESIZE|Erro ao obter o tamanho para o arquivo "%1".|  
|0xC020209A|-1071636326|DTS_E_FAILEDTOSETFILEPOINTER|Erro durante a definição do ponteiro para o arquivo "%1".|  
|0xC020209B|-1071636325|DTS_E_UNABLETOSETUPDISKIOBUFFER|Ocorreu um erro durante a configuração do buffer de E/S de disco.|  
|0xC020209C|-1071636324|DTS_E_COLUMNDATAOVERFLOWDISKIOBUFFER|Os dados para a coluna "%1" estouraram o buffer de E/S de disco.|  
|0xC020209D|-1071636323|DTS_E_DISKIOFAILED|Ocorreu um erro inesperado de E/S de disco durante a leitura do arquivo.|  
|0xC020209E|-1071636322|DTS_E_DISKIOTIMEDOUT|A E/S de disco expirou durante a leitura do arquivo.|  
|0xC020209F|-1071636321|DTS_E_INPUTSNOTREADONLY|O Tipo de Uso especificado das colunas de entrada para essa transformação não pode ser leitura/gravação. Altere o Tipo de Uso para ser somente leitura.|  
|0xC02020A0|-1071636320|DTS_E_CANNOTCOPYORCONVERTFLATFILEDATA|Não é possível copiar nem converter os dados do arquivo simples para a coluna "%1".|  
|0xC02020A1|-1071636319|DTS_E_FAILEDCOLUMNDATACONVERSIONSTATUS|Falha na conversão de dados. A conversão de dados para a coluna "%1" retornou valor de status %2!d! e texto de status "%3".|  
|0xC02020A2|-1071636318|DTS_E_VARIABLESCOLLECTIONUNAVAILABLE|A coleção Variables não está disponível.|  
|0xC02020A3|-1071636317|DTS_E_TXUNPIVOTDUPLICATEPIVOTKEYVALUE|PivotKeyValue duplicado. A coluna de entrada "%1" (%2!d!) está mapeada para uma coluna de saída de Valor Dinâmico e tem PivotKeyValue não exclusivo.|  
|0xC02020A4|-1071636316|DTS_E_TXUNPIVOTNOUNPIVOTDESTINATION|Não foi encontrado nenhum destino não dinâmico. Pelo menos uma coluna de entrada deve ser mapeada com um PivotKeyValue para um DestinationColumn na saída.|  
|0xC02020A5|-1071636315|DTS_E_TXUNPIVOTBADKEYLIST|PivotKeyValue não é válido. Em uma transformação não dinâmica com mais de um DestinationColumn não dinamizado, o conjunto de PivotKeyValues por destino deve corresponder de forma exata.|  
|0xC02020A6|-1071636314|DTS_E_TXUNPIVOTBADUNPIVOTMETADATA|Metadados Não Dinâmicos incorretos. Em uma transformação não dinâmica, todas as colunas de entrada com um PivotKeyValue definido e que estejam apontando para a mesma DestinationColumn, devem ter metadados que correspondam exatamente a DestinationColumn.|  
|0xC02020A7|-1071636313|DTS_E_TXPIVOTBADPIVOTKEYCONVERT|Não é possível converter o valor "%1" da chave dinâmica no tipo de dados da coluna de chave dinâmica.|  
|0xC02020A8|-1071636312|DTS_E_TXUNPIVOTTOOMANYPIVOTKEYS|Há Chaves Dinâmicas, em excesso, especificadas. Só uma coluna de saída pode ser usada como Chave Dinâmica.|  
|0xC02020A9|-1071636311|DTS_E_TXUNPIVOTUNMAPPEDOUTPUT|A coluna de saída "%1" (%2!d!) não foi mapeada pela propriedade DestinationColumn de nenhuma coluna de entrada.|  
|0xC02020AA|-1071636310|DTS_E_TXUNPIVOTNOPIVOT|Nenhuma coluna de saída está marcada como PivotKey.|  
|0xC02020AB|-1071636309|DTS_E_TXUNPIVOTNOTINPUTMAP|A coluna de entrada "%1" (%2!d!) tem um valor de propriedade DestinationColumn que não se refere a um LineageID válido de coluna de saída.|  
|0xC02020AC|-1071636308|DTS_E_TXUNPIVOTDUPLICATEDESTINATION|Erro de destino duplicado. Mais de uma coluna de entrada não dinâmica é mapeada para a mesma coluna de saída de destino.|  
|0xC02020AD|-1071636307|DTS_E_TOTALINPUTCOLSCANNOTBEZERO|Não foi encontrada nenhuma coluna de entrada. Pelo menos uma coluna de entrada deve ser mapeada para uma coluna de saída.|  
|0xC02020AE|-1071636306|DTS_E_TXMERGEJOINMUSTHAVESAMENUMBEROFINPUTANDOUTPUTCOLS|O número de colunas de entrada e saída não é igual. O número total de colunas de entrada em todas as entradas deve ser igual ao número total de colunas de saída.|  
|0xC02020AF|-1071636305|DTS_E_INPUTMUSTBESORTED|A entrada não está classificada. A "%1" deve ser classificada.|  
|0xC02020B0|-1071636304|DTS_E_TXMERGEJOININVALIDJOINTYPE|A propriedade personalizada JoinType para %1 contém um valor de %2!ld!, que não é válido. Valores válidos são 0 (cheio), 1 (esquerda) ou 2 (interno).|  
|0xC02020B1|-1071636303|DTS_E_TXMERGEJOININVALIDNUMKEYCOLS|O valor NumKeyColumns não é válido. Em %1, o valor da propriedade personalizada NumKeyColumns deve ficar entre 1 e %2!lu!.|  
|0xC02020B2|-1071636302|DTS_E_NOKEYCOLS|Não foi encontrada nenhuma coluna de chave. O %1 deve ter pelo menos uma coluna com SortKeyPosition diferente de zero.|  
|0xC02020B3|-1071636301|DTS_E_TXMERGEJOINNOTENOUGHKEYCOLS|Não existem colunas de chave suficientes. O %1 deve ter pelo menos %2!ld! colunas com valores de SortKeyPosition diferentes de zero.|  
|0xC02020B4|-1071636300|DTS_E_TXMERGEJOINDATATYPEMISMATCH|Houve incompatibilidade de tipo de dados. Os tipos de dados para as colunas com valor SortKeyPosition %1!ld! não coincidem.|  
|0xC02020B5|-1071636299|DTS_E_TXMERGEJOININVALIDSORTKEYPOS|A coluna com o valor SortKeyPosition de %1!ld! não é válido. Esse valor deveria ser %2!ld!.|  
|0xC02020B6|-1071636298|DTS_E_TXMERGEJOINSORTDIRECTIONMISMATCH|Incompatibilidade de direção de classificação. As direções de classificação para as colunas com valor SortKeyPosition %1!ld! não coincidem.|  
|0xC02020B7|-1071636297|DTS_E_TXMERGEJOINOUTPUTCOLMUSTHAVEASSOCIATEDINPUTCOL|Falta uma coluna. O %1 deve ter uma coluna de entrada associada.|  
|0xC02020B8|-1071636296|DTS_E_TXMERGEJOINREADONLYINPUTCOLSWITHNOOUTPUTCOL|As colunas de entrada devem ter colunas de saída. Existem colunas de entrada com um tipo de uso somente leitura sem colunas de saída associadas.|  
|0xC02020B9|-1071636295|DTS_E_TXMERGEJOINNONSTRINGCOMPARISONFLAGSNOTZERO|Os sinalizadores de comparação são diferentes de zero. Os sinalizadores de comparação para colunas que não sejam de cadeia de caracteres devem ser zero.|  
|0xC02020BA|-1071636294|DTS_E_TXMERGEJOINCOMPARISONFLAGSMISMATCH|Os sinalizadores de comparação para as colunas com o valor SortKeyPosition %1!ld! não coincidem.|  
|0xC02020BB|-1071636293|DTS_E_TXPIVOTBADPIVOTKEYVALUENOSTRING|Valor de chave dinâmica não reconhecido.|  
|0xC02020BC|-1071636292|DTS_E_TXLINEAGEINVALIDLINEAGEITEM|O valor do item de linhagem %1!ld! não é válido. O intervalo válido fica entre %2!ld! e %3!ld!.|  
|0xC02020BD|-1071636291|DTS_E_CANNOTHAVEANYINPUTCOLUMNS|Colunas de entrada não permitidas. O número de colunas de entrada deve ser zero.|  
|0xC02020BE|-1071636290|DTS_E_TXLINEAGEDATATYPEMISMATCH|O tipo de dados "%1" não é válido para o item de linhagem especificado.|  
|0xC02020BF|-1071636289|DTS_E_TXLINEAGEINVALIDLENGTH|O comprimento para "%1" não é válido para o item de linhagem especificado.|  
|0xC02020C1|-1071636287|DTS_E_METADATAMISMATCHWITHOUTPUTCOLUMN|Os metadados para "%1" não correspondem aos metadados para a coluna de saída associada.|  
|0xC02020C3|-1071636285|DTS_E_TXMERGESORTKEYPOSMISMATCH|Existem colunas de saída com valores SortKeyPosition que não correspondem a SortKeyPosition das colunas de entrada associadas.|  
|0xC02020C4|-1071636284|DTS_E_ADDROWTOBUFFERFAILED|Falha na tentativa de adicionar uma linha ao buffer de tarefa de Fluxo de Dados com o código de erro 0x%1!8.8X!.|  
|0xC02020C5|-1071636283|DTS_E_DATACONVERSIONFAILED|Falha na conversão de dados durante a conversão da coluna "%1" (%2!d!) na coluna "%3" (%4!d!).  A conversão retornou valor de status %5!d! e texto de status "%6".|  
|0xC02020C6|-1071636282|DTS_E_FAILEDTOALLOCATEROWHANDLEBUFFER|Falha na tentativa de alocar um buffer de manipuladores de linha com o código de erro 0x%1!8.8X!.|  
|0xC02020C7|-1071636281|DTS_E_FAILEDTOSENDROWTOSQLSERVER|Falha na tentativa de envio de uma linha para um SQL Server com o código de erro 0x%1!8.8X!.|  
|0xC02020C8|-1071636280|DTS_E_FAILEDTOPREPAREBUFFERSTATUS|Falha na tentativa de preparação do status de buffer com o código de erro 0x%1!8.8X!.|  
|0xC02020C9|-1071636279|DTS_E_FAILEDTOBUFFERROWSTARTS|Falha na tentativa de recuperação do início da linha de buffer com o código de erro 0x%1!8.8X!.|  
|0xC02020CA|-1071636278|DTS_E_BULKINSERTTHREADTERMINATED|O thread para a Inserção em Massa do SSIS não está mais executando.  Não pode ser inserida mais nenhuma linha. A tentativa de aumentar o thread de inserção em massa expirou.|  
|0xC02020CB|-1071636277|DTS_E_RAWTOOMANYCOLUMNS|O nome de origem não é válido. O arquivo de origem está retornando uma contagem de mais de 131.072 colunas. Isso normalmente ocorre quando o arquivo de origem não é produzido pelo destino do arquivo bruto.|  
|0xC02020CC|-1071636276|DTS_E_TXUNIONALL_EXTRADANGLINGINPUT|O %1 é uma entrada extra desanexada e será removido.|  
|0xC02020CD|-1071636275|DTS_E_TXUNIONALL_NONDANGLINGUNATTACHEDINPUT|O %1 não está anexado, mas não está marcado como pendente.  Ele será marcado como pendente.|  
|0xC02020CF|-1071636273|DTS_E_TXPIVOTRUNTIMEDUPLICATEPIVOTKEYVALUE|Valor de chave dinâmica duplicado "%1".|  
|0xC02020D0|-1071636272|DTS_E_TXPIVOTRUNTIMEDUPLICATEPIVOTKEYVALUENOSTRING|Valor de chave dinâmica duplicado.|  
|0xC02020D1|-1071636271|DTS_E_FAILEDTOGETCOMPONENTLOCALEID|Falha na recuperação da identificação de localidade do componente. Código de erro 0x%1!8.8X!.|  
|0xC02020D2|-1071636270|DTS_E_MISMATCHCOMPONENTCONNECTIONMANAGERLOCALEID|Identificações de localidade incompatíveis. A identificação de local de componente (%1!d!) não corresponde à identificação de localidade do gerenciador de conexões (%2!d!).|  
|0xC02020D3|-1071636269|DTS_E_LOCALEIDNOTSET|A identificação de localidade do componente não foi definida. Os adaptadores de arquivo simples precisam ter a identificação de localidade definida no gerenciador de conexões de arquivos simples.|  
|0xC02020D4|-1071636268|DTS_E_RAWBYTESTOOLONG|O campo binário é muito grande. O adaptador tentou ler um campo binário com %1!d! bytes de comprimento, mas esperava-se um campo com não mais de %2!d! bytes, no deslocamento %3!d!. Isso normalmente ocorre quando o arquivo de entrada não é válido. O arquivo contém um comprimento da cadeia de caracteres muito longo para a coluna de buffer.|  
|0xC02020D5|-1071636267|DTS_E_TXSAMPLINGINVALIDPCT|A porcentagem %2!ld! não é válida para a propriedade "%1". Deve estar entre 0 e 100.|  
|0xC02020D6|-1071636266|DTS_E_TXSAMPLINGINVALIDROWS|O número de linhas %2!ld! não é válido para a propriedade "%1". Ele deve ser maior que 0.|  
|0xC02020D7|-1071636265|DTS_E_RAWSTRINGINPUTTOOLONG|O adaptador foi solicitado a gravar uma cadeia de caracteres com %1!I64d! bytes de comprimento, mas todos os dados devem ter menos de 4294967295 bytes de comprimento.|  
|0xC02020D9|-1071636263|DTS_E_ATLEASTONEINPUTMUSTBEMAPPEDTOOUTPUT|Nenhuma entrada foi mapeada para uma saída. O "%1" deve ter pelo menos uma coluna de entrada mapeada para uma coluna de saída.|  
|0xC02020DB|-1071636261|DTS_E_CANNOTCONVERTDATATYPESWITHDIFFERENTCODEPAGES|Conversão de "%1" com página de código %2!d! para "%3" com página de código %4!d! sem-suporte.|  
|0xC02020DC|-1071636260|DTS_E_COLUMNNOTMAPPEDTOEXTERNALMETADATACOLUMN|O mapeamento de coluna de metadados externos para %1 não é válido.  A identificação da coluna de metadados externos não pode ser zero.|  
|0xC02020DD|-1071636259|DTS_E_COLUMNMAPPEDTONONEXISTENTEXTERNALMETADATACOLUMN|O %1 está mapeado para uma coluna de metadados externos que não existe.|  
|0xC02020E5|-1071636251|DTS_E_UNABLETOWRITELOBDATATOBUFFER|Falha na gravação dos dados de objeto longo do tipo DT_TEXT, DT_NTEXT ou DT_IMAGE no buffer da tarefa de Fluxo de Dados para a coluna "%1".|  
|0xC02020E8|-1071636248|DTS_E_CANNOTGETIROWSET|Falha ao abrir um conjunto de linhas para "%1". Verifique se o objeto existe no banco de dados.|  
|0xC02020E9|-1071636247|DTS_E_VARIABLEACCESSFAILED|Falha no acesso à variável "%1" com o código de erro 0x%2!8.8X!.|  
|0xC02020EA|-1071636246|DTS_E_CONNECTIONMANAGERNOTFOUND|O gerenciador de conexões "%1" não foi encontrado. Um componente não encontrou o gerenciador de conexões na coleção Connections.|  
|0xC02020EB|-1071636245|DTS_E_VERSIONUPGRADEFAILED|Falha na atualização da versão "%1" para a versão %2!d! .|  
|0xC02020EC|-1071636244|DTS_E_RSTDESTBIGBLOB|Um valor em uma coluna de entrada é muito grande para ser armazenado no objeto ADODB.Recordset.|  
|0xC02020ED|-1071636243|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMNS|Não é possível converter as colunas "%1" e "%2" entre tipos de dados de cadeias de caracteres unicode e não unicode.|  
|0xC02020EE|-1071636242|DTS_E_ROWCOUNTBADVARIABLENAME|A variável "%1" especificada pela propriedade VariableName não é uma variável válida. É necessário um nome de variável válido para permitir a gravação.|  
|0xC02020EF|-1071636241|DTS_E_ROWCOUNTBADVARIABLETYPE|A variável "%1" especificada pela propriedade VariableName não é um número inteiro. Altere a variável para ser do tipo VT_I4, VT_UI4, VT_I8 ou VT_UI8.|  
|0xC02020F0|-1071636240|DTS_E_NOCOLUMNADVANCETHROUGHFILE|Nenhuma coluna foi especificada para permitir que o componente avance pelo arquivo.|  
|0xC02020F1|-1071636239|DTS_E_MERGEJOINSORTEDOUTPUTHASNOSORTKEYPOSITIONS|O "%1" tem IsSorted definido como TRUE, mas o SortKeyPosition em todas as colunas de saída é zero. Altere o IsSorted para FALSE, ou selecione pelo menos uma coluna de saída para conter um SortKeyPosition diferente de zero.|  
|0xC02020F2|-1071636238|DTS_E_METADATAMISMATCHWITHINPUTCOLUMN|Os metadados de "%1" não correspondem aos metadados da coluna de entrada.|  
|0xC02020F3|-1071636237|DTS_E_RSTDESTBADVARIABLE|O valor da variável especificada não pode ser localizado, bloqueado ou definido.|  
|0xC02020F4|-1071636236|DTS_E_CANTPROCESSCOLUMNTYPECODEPAGE|A coluna "%1" não pode ser processada porque mais de uma página de código (%2!d! e %3!d!) está especificada para ela.|  
|0xC02020F5|-1071636235|DTS_E_CANTINSERTCOLUMNTYPE|A coluna "%1" não pode ser inserida porque não existe suporte para a conversão entre tipos %2 e %3.|  
|0xC02020F6|-1071636234|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMN|Não é possível converter a coluna "%1" entre tipos de dados de cadeias de caracteres unicode e não unicode.|  
|0xC02020F8|-1071636232|DTS_E_COULDNOTFINDINPUTBUFFERCOLUMNBYLINEAGE|O %1 não pode localizar a coluna com LineageID %2!ld! em seu buffer de entrada.|  
|0xC02020F9|-1071636231|DTS_E_COULDNOTGETCOLUMNINFOFORINPUTBUFFER|O %1 não pode obter as informações de coluna para a coluna %2!lu! de seu buffer de entrada.|  
|0xC02020FA|-1071636230|DTS_E_COULDNOTGETCOLUMNINFOFORCOPYBUFFER|O %1 não pode obter as informações de coluna para a coluna %2!lu! de seu buffer de cópia.|  
|0xC02020FB|-1071636229|DTS_E_COULDNOTREGISTERCOPYBUFFER|O %1 não pode registrar um tipo de buffer para seu buffer de cópia.|  
|0xC02020FC|-1071636228|DTS_E_COULDNOTCREATECOPYBUFFER|O %1 não pode criar um buffer para copiar seus dados para serem classificados.|  
|0xC02020FD|-1071636227|DTS_E_DATAREADERDESTREADFAILED|O cliente DataReader não chamou Leitura ou fechou o DataReader.|  
|0xC02020FE|-1071636226|DTS_E_NOSCHEMAINFOFOUND|Nenhuma informação de coluna foi retornada pelo comando SQL.|  
|0xC02020FF|-1071636225|DTS_E_GETSCHEMATABLEFAILED|O %1 não pôde recuperar informações de coluna pelo comando SQL. O seguinte erro ocorreu: %2|  
|0xC0202100|-1071636224|DTS_E_SOURCETABLENAMENOTPROVIDED|Não foi fornecido um nome de tabela de origem.|  
|0xC0203110|-1071632112|DTS_E_CACHE_INVALID_INDEXPOS|A posição do índice do cache, %1!d!, não é válida. Para colunas sem índice, a posição do índice deve ser 0. Para colunas de índice, a posição de índice deve ser um número sequencial, positivo.|  
|0xC0203111|-1071632111|DTS_E_CACHE_DUPLICATE_INDEXPOS|A posição do índice, %1!d!, é uma duplicata. Para colunas sem índice, a posição do índice deve ser 0. Para colunas de índice, a posição de índice deve ser um número sequencial, positivo.|  
|0xC0203112|-1071632110|DTS_E_CACHE_TOO_FEW_INDEX_COLUMNS|Pelo menos uma coluna de índice deve ser especificada para o gerenciador de conexões do Cache. Para especificar uma coluna de índice, defina a propriedade Index Position da coluna de cache.|  
|0xC0203113|-1071632109|DTS_E_CACHE_INDEXPOS_NOT_CONTINUOUS|Posições de índice de cache devem ser contíguas. Para colunas sem índice, a posição do índice deve ser 0. Para colunas de índice, a posição de índice deve ser um número sequencial, positivo.|  
|0xC0204000|-1071628288|DTS_E_PROPERTYNOTSUPPORTED|A propriedade "%1" não pode ser definida como "%2". Não existe suporte para a propriedade que está sendo definida no objeto especificado. Verifique o nome, as maiúsculas e minúsculas e a ortografia da propriedade.|  
|0xC0204002|-1071628286|DTS_E_CANTCHANGEPROPERTYTYPE|O tipo de propriedade não pode ser alterado do tipo definido pelo componente.|  
|0xC0204003|-1071628285|DTS_E_CANTADDOUTPUTID|Falha na ID de saída %1!d! durante a inserção. Não foi criada nova saída.|  
|0xC0204004|-1071628284|DTS_E_CANTDELETEOUTPUTID|Não é possível excluir a ID de saída %1!d! da coleção de saída.  A identificação pode não ser válida ou pode ter sido a saída de erro ou padrão.|  
|0xC0204006|-1071628282|DTS_E_FAILEDTOSETPROPERTY|Falha ao definir a propriedade "%1" em "%2".|  
|0xC0204007|-1071628281|DTS_E_FAILEDTOSETOUTPUTCOLUMNTYPE|Falha ao definir o tipo de %1 como o tipo: "%2", comprimento: %3!d!, precisão: %4!d!, escala: %5!d!, página de código: %6!d!.|  
|0xC0204008|-1071628280|DTS_E_MORETHANONEERROROUTPUTFOUND|Mais de uma saída de erro foi encontrada no componente e pode haver somente um.|  
|0xC020400A|-1071628278|DTS_E_CANTSETOUTPUTCOLUMNPROPERTY|A propriedade em uma coluna de saída não pode ser definida.|  
|0xC020400B|-1071628277|DTS_E_CANTMODIFYERROROUTPUTCOLUMNDATATYPE|O tipo de dados para "%1" não pode ser modificado no erro "%2".|  
|0xC020400E|-1071628274|DTS_E_CANONLYSETISSORTEDONSOURCE|O "%1" não pode ter sua propriedade IsSorted definida como TRUE porque não é uma saída de origem. Uma saída de origem tem um valor SynchronousInputID de zero.|  
|0xC020400F|-1071628273|DTS_E_CANONLYSETSORTKEYONSOURCE|O "%1" não podem ter uma propriedade SortKeyPosition definida como diferente de zero porque "%2" não é uma saída de origem. O coluna de saída "colname" (ID) não pode ter sua propriedade SortKeyPosition definida como diferente de zero porque sua saída "outputname" (ID) não é uma saída de origem.|  
|0xC0204010|-1071628272|DTS_E_CANONLYSETCOMPFLAGSONSOURCE|A propriedade ComparisonFlags não pode ser definida como um valor diferente de zero para "%1" porque o "%2" não é saída de origem. A coluna de saída "colname" (ID) não pode ter uma propriedade ComparisonFlags definida como diferente de zero porque sua saída "outputname" (ID) não é saída de origem.|  
|0xC0204011|-1071628271|DTS_E_NONSTRINGCOMPARISONFLAGSNOTZERO|Os sinalizadores de comparação para "%1" devem ser zero porque seu tipo não é de cadeia de caracteres. ComparisonFlags só pode ser diferente de zero para colunas do tipo cadeia de caracteres.|  
|0xC0204012|-1071628270|DTS_E_COMPFLAGSONLYONSORTCOL|O "%1" não pode ter uma propriedade ComparisonFlags definida como diferente de zero porque seu SortKeyPosition está definido como zero. ComparisonFlags de uma coluna de saída só pode ser diferente de zero se seu SortKeyPosition também for diferente de zero.|  
|0xC0204013|-1071628269|DTS_E_READONLYSTOCKPROPERTY|A propriedade é somente leitura.|  
|0xC0204014|-1071628268|DTS_E_INVALIDDATATYPE|O %1 tinha um valor de tipo de dados inválido (%2!ld!) definido.|  
|0xC0204015|-1071628267|DTS_E_CODEPAGEREQUIRED|O "%1" necessita de uma página de código para ser definido, mas o valor passado foi zero.|  
|0xC0204016|-1071628266|DTS_E_INVALIDSTRINGLENGTH|O "%1" tem um comprimento que não é válido. O comprimento deve ficar entre %2!ld! e %3!ld!.|  
|0xC0204017|-1071628265|DTS_E_INVALIDSCALE|O "%1" tem uma escala que não é válida. A escala deve ficar entre %2!ld! e %3!ld!.|  
|0xC0204018|-1071628264|DTS_E_INVALIDPRECISION|O "%1" tem uma precisão que não é válida. A precisão deve ficar entre %2!ld! e %3!ld!.|  
|0xC0204019|-1071628263|DTS_E_PROPVALUEIGNORED|O "%1" tem um valor diferente de zero definido para comprimento, precisão, escala ou página de código, mas o tipo de dados exige que o valor seja zero.|  
|0xC020401A|-1071628262|DTS_E_CANTSETOUTPUTCOLUMNDATATYPEPROPERTIES|O %1 não permite a configuração das propriedades de tipos de dados de coluna de saída.|  
|0xC020401B|-1071628261|DTS_E_INVALIDDATATYPEFORERRORCOLUMNS|O "%1" contém um tipo de dados inválido. "%1" é uma coluna de erro especial, e o único tipo de dados válido é DT_I4.|  
|0xC020401C|-1071628260|DTS_E_NOERRORDESCFORCOMPONENT|O componente não fornece descrições de código de erro.|  
|0xC020401D|-1071628259|DTS_E_UNRECOGNIZEDERRORCODE|O código de erro especificado não está associado a esse componente.|  
|0xC020401F|-1071628257|DTS_E_TRUNCATIONTRIGGEREDREDIRECTION|Um truncamento provocou o redirecionamento de uma linha, com base nas configurações de disposição de truncamento.|  
|0xC0204020|-1071628256|DTS_E_CANTSETUSAGETYPETOREADWRITE|O "%1" não pode criar a coluna com leitura/gravação de ID de linhagem %2!d! porque aquele tipo de uso não é permitido nesta coluna. Foi feita uma tentativa de alterar o tipo de uso de uma coluna de entrada para tipo, UT_READWRITE, para o qual esse componente não fornece suporte.|  
|0xC0204023|-1071628253|DTS_E_CANTSETUSAGETYPE|O %1 proibiu o uso solicitado da coluna de entrada com a identificação de linhagem %2!d!.|  
|0xC0204024|-1071628252|DTS_E_FAILEDTOSETUSAGETYPE|"%1" não pôde realizar a alteração solicitada na coluna de entrada com a identificação de linhagem %2!d!. Falha na solicitação com o código de erro 0x%3!8.8X!. O erro especificado ocorreu na tentativa de definir o tipo de uso de uma coluna de entrada.|  
|0xC0204025|-1071628251|DTS_E_FAILEDTOSETOUTPUTCOLUMNDATATYPEPROPERTIES|Falha na tentativa de definição das propriedades de tipo de dados em "%1" com o código de erro 0x%2!8.8X!. O erro ocorreu na tentativa de definir uma ou mais propriedades do tipo de dados da coluna de saída.|  
|0xC0204026|-1071628250|DTS_E_UNABLETORETRIEVEMETADATA|Não é possível recuperar os metadados para "%1". Certifique-se de que o nome de objeto esteja correto e o objeto exista.|  
|0xC0204027|-1071628249|DTS_E_CANNOTMAPOUTPUTCOLUMN|A coluna de saída não pode ser mapeada para uma coluna de metadados externos.|  
|0xC0204028|-1071628248|DTS_E_UNSUPPORTEDVARIABLETYPE|A variável %1 deve ser do tipo "%2".|  
|0xC020402A|-1071628246|DTS_E_CANTSETEXTERNALMETADATACOLUMNDATATYPEPROPERTIES|O %1 não permite a configuração das propriedades do tipo de dados da coluna de metadados externos.|  
|0xC020402B|-1071628245|DTS_E_IDNOTINPUTNOROUTPUT|A identificação %1!lu! não é uma identificação de entrada nem de saída. A ID especificada deve ser de entrada ou saída à qual está associada a coleção de metadados externos.|  
|0xC020402C|-1071628244|DTS_E_METADATACOLLECTIONNOTUSED|A coleção de metadados externos em "%1" está marcada como não usada, assim nenhuma operação pode ser executada nela.|  
|0xC020402D|-1071628243|DTS_E_NOBUFFERTYPEONSYNCOUTPUT|O %1 é uma saída síncrona e o tipo de buffer não pode ser recuperado para uma saída síncrona.|  
|0xC0207000|-1071616000|DTS_E_INPUTCOLUMNUSAGETYPENOTREADONLY|A coluna de entrada "%1" deve ser somente leitura. A coluna de entrada tem um tipo de uso diferente de somente leitura, o que não é permitido.|  
|0xC0207001|-1071615999|DTS_E_MISSINGCUSTOMPROPERTY|O "%1" não tem a propriedade necessária "%2". O objeto deve ter a propriedade personalizada especificada.|  
|0xC0207002|-1071615998|DTS_E_ILLEGALCUSTOMOUTPUTPROPERTY|A saída %1 não pode ter propriedade "%2", mas atualmente tem essa propriedade atribuída.|  
|0xC0207003|-1071615997|DTS_E_INVALIDOUTPUTEXCLUSIONGROUP|O %1 deve estar no grupo de exclusão %2!d!. Todas as saídas devem estar no grupo de exclusão especificado.|  
|0xC0207004|-1071615996|DTS_E_PROPERTYISEMPTY|A propriedade "%1" está vazia. A propriedade não pode estar vazia.|  
|0xC0207005|-1071615995|DTS_E_CREATEEXPRESSIONOBJECTFAILED|A memória não pode ser alocada para a expressão "%1". Erro por falta de memória durante a criação de um objeto para manter a expressão.|  
|0xC0207006|-1071615994|DTS_E_EXPRESSIONPARSEFAILED|Não é possível analisar a expressão "%1". A expressão não era válida ou há falta de memória.|  
|0xC0207007|-1071615993|DTS_E_EXPRESSIONCOMPUTEFAILED|Falha na computação da expressão "%1" com o código de erro 0x%2!8.8X!. A expressão pode ter erros, como divisão por zero, que não podem ser detectados no momento da análise, ou pode haver falta de memória.|  
|0xC0207008|-1071615992|DTS_E_FAILEDTOCREATEEXPRESSIONARRAY|A memória não pode ser alocada para os objetos Expressão. Houve falta de memória durante a criação da matriz dos ponteiros do objeto Expressão.|  
|0xC020700A|-1071615990|DTS_E_FAILEDTOCREATEEXPRESSIONMANANGER|Falha em %1 com o código de erro 0x%2!8.8X! ao criar o Gerenciador de Expressões.|  
|0xC020700B|-1071615989|DTS_E_SPLITEXPRESSIONNOTBOOLEAN|A expressão "%1" não é booliana. O tipo de resultado da expressão deve ser booliano.|  
|0xC020700C|-1071615988|DTS_E_EXPRESSIONVALIDATIONFAILED|A expressão "%1" em "%2" não é válida.|  
|0xC020700E|-1071615986|DTS_E_COLUMNNOTMATCHED|Não é possível corresponder a coluna "%1" (%2!d!) a nenhuma coluna de arquivo de entrada. Não foi possível encontrar no arquivo o nome da coluna de saída ou nome da coluna de entrada.|  
|0xC020700F|-1071615985|DTS_E_SETRESULTCOLUMNFAILED|Falha na tentativa de definir a coluna de resultado para a expressão "%1" em %2 com o código de erro 0x%3!8.8X!. A coluna de entrada ou saída que deveria receber o resultado da expressão não pode ser determinada, ou o resultado da expressão não pode ser convertido no tipo da coluna.|  
|0xC0207011|-1071615983|DTS_E_FAILEDTOGETLOCALEIDFROMPACKAGE|O %1 não obteve a ID de localidade do pacote.|  
|0xC0207012|-1071615982|DTS_E_INCORRECTPARAMETERMAPPINGFORMAT|A cadeia de caracteres de mapeamento do parâmetro não está no formato correto.|  
|0xC0207013|-1071615981|DTS_E_NOTENOUGHPARAMETERSPROVIDED|O comando SQL requer %1!d! parâmetros, mas o mapeamento de parâmetro tem apenas %2!d! parâmetros.|  
|0xC0207014|-1071615980|DTS_E_PARAMETERNOTFOUNDINMAPPING|O comando SQL necessita de um parâmetro de nome "%1", que não é encontrado no mapeamento do parâmetro.|  
|0xC0207015|-1071615979|DTS_E_DUPLICATEDATASOURCECOLUMNNAME|Existe mais de uma coluna de fonte de dados com o nome "%1".  Os nomes da coluna de fonte de dados devem ser iguais.|  
|0xC0207016|-1071615978|DTS_E_DATASOURCECOLUMNWITHNONAMEFOUND|Existe uma coluna de fonte de dados sem-nome.  Cada coluna de fonte de dados deve ter um nome.|  
|0xC0208001|-1071611903|DTS_E_DISCONNECTEDCOMPONENT|Um componente está desconectado do plano.|  
|0xC0208002|-1071611902|DTS_E_INVALIDCOMPONENTID|A ID de um componente de layout não é válida.|  
|0xC0208003|-1071611901|DTS_E_INVALIDINPUTCOUNT|Um componente tem um número inválido de entradas.|  
|0xC0208004|-1071611900|DTS_E_INVALIDOUTPUTCOUNT|Um componente tem um número inválido de saídas.|  
|0xC0208005|-1071611899|DTS_E_NOINPUTSOROUTPUTS|Um componente não tem qualquer entrada ou saída.|  
|0xC0208007|-1071611897|DTS_E_CANTALLOCATECOLUMNINFO|Não havia memória suficiente para alocar uma lista de colunas que estão sendo tratadas por este componente.|  
|0xC0208008|-1071611896|DTS_E_OUTPUTCOLUMNNOTININPUT|A coluna de saída "%1" (%2!d!) referencia a coluna de entrada com a identificação de linhagem %3!d!, mas não foi possível encontrar nenhuma entrada com essa identificação de linhagem.|  
|0xC0208009|-1071611895|DTS_E_SORTNEEDSONEKEY|Pelo menos uma coluna de entrada deve estar marcada como chave de classificação, mas nenhuma chave foi encontrada.|  
|0xC020800A|-1071611894|DTS_E_SORTDUPLICATEKEYWEIGHT|As colunas "%1" (%2!d!) e "%3" (%4!d!) foram marcadas com peso de chave de classificação %5!d!.|  
|0xC020800D|-1071611891|DTS_E_CANTMODIFYINVALID|O componente não pode executar a alteração de metadados solicitada até que o problema de validação seja resolvido.|  
|0xC020800E|-1071611890|DTS_E_CANTADDINPUT|Uma entrada não pode ser adicionada à coleção de entradas.|  
|0xC020800F|-1071611889|DTS_E_CANTADDOUTPUT|Uma saída não pode ser adicionada à coleção de saídas.|  
|0xC0208010|-1071611888|DTS_E_CANTDELETEINPUT|Uma entrada não pode ser excluída da coleção de entradas.|  
|0xC0208011|-1071611887|DTS_E_CANTDELETEOUTPUT|Uma saída não pode ser removida da coleção de saídas.|  
|0xC0208014|-1071611884|DTS_E_CANTCHANGEUSAGETYPE|O tipo de uso da coluna não pode ser alterado.|  
|0xC0208016|-1071611882|DTS_E_INVALIDUSAGETYPEFORCUSTOMPROPERTY|O %1 deve ser leitura/gravação para ter a propriedade personalizada "%2". A coluna de entrada ou saída tem a propriedade personalizada especificada, mas não é leitura/gravação. Remova a propriedade ou torne a coluna de leitura/gravação.|  
|0xC0208017|-1071611881|DTS_E_READWRITECOLUMNMISSINGREQUIREDCUSTOMPROPERTY|O %1 é de leitura/gravação e deve ter a propriedade personalizada "%2". Adicione a propriedade ou remova o atributo de leitura/gravação da coluna.|  
|0xC0208018|-1071611880|DTS_E_CANTDELETECOLUMN|A coluna não pode ser excluída. O componente não permite excluir colunas dessa entrada ou saída.|  
|0xC0208019|-1071611879|DTS_E_CANTADDCOLUMN|O componente não permite adicionar colunas a essa entrada ou saída.|  
|0xC020801A|-1071611878|DTS_E_CANNOTTFINDRUNTIMECONNECTIONOBJECT|Não foi possível encontrar a conexão "%1". Verifique se o gerenciador de conexões tem uma conexão com esse nome.|  
|0xC020801B|-1071611877|DTS_E_CANNOTFINDRUNTIMECONNECTIONMANAGER|Não é possível encontrar o gerenciador de conexões de tempo de execução com a ID "%1". Verifique se a coleção de gerenciadores de conexões tem um gerenciador de conexões com essa ID.|  
|0xC020801C|-1071611876|DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER|Código de Erro SSIS DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER.  Falha da chamada do método AcquireConnection para o gerenciador de conexões "%1" com o código de erro 0x%2!8.8X!.  Pode haver mensagens de erro geradas antes dessa, com mais informações sobre as razões da falha na chamada do método AcquireConnection.|  
|0xC020801D|-1071611875|DTS_E_ACQUIREDCONNECTIONISINVALID|A conexão adquirida do gerenciador de conexões "%1" não é válida.|  
|0xC020801E|-1071611874|DTS_E_INCORRECTCONNECTIONMANAGERTYPE|O gerenciador de conexões "%1" é de um tipo incorreto.  O tipo necessário é "%2". O tipo disponível para componente é "%3".|  
|0xC020801F|-1071611873|DTS_E_CANNOTACQUIREMANAGEDCONNECTIONFROMCONNECTIONMANAGER|Não é possível adquirir uma conexão gerenciada do gerenciador de conexões de tempo de execução.|  
|0xC0208020|-1071611872|DTS_E_CANTINITINPUT|Não é possível criar uma entrada para inicializar a coleção de entradas.|  
|0xC0208021|-1071611871|DTS_E_CANTINITOUTPUT|Não é possível criar uma saída para inicializar a coleção de saídas.|  
|0xC0208023|-1071611869|DTS_E_EXTRACTORCANTWRITE|Falha na gravação no arquivo "%1" com o código de erro 0x%2!8.8X!.|  
|0xC0208024|-1071611868|DTS_E_INCORRECTCONNECTIONOBJECTTYPE|O gerenciador de conexões "%1" retornou um objeto de tipo incorreto do método AcquireConnection.|  
|0xC0208025|-1071611867|DTS_E_INPUTCOLPROPERTYNOTFOUND|A propriedade "%3" é necessária na coluna de entrada "%1" (%2!d!), mas não foi encontrada. Deve ser adicionada a propriedade que está faltando.|  
|0xC0208026|-1071611866|DTS_E_EXTRACTORUNREFERENCED|O "%1" está marcado como somente leitura, mas não é referenciado por nenhuma outra coluna. Não são permitidas colunas não referenciadas.|  
|0xC0208027|-1071611865|DTS_E_EXTRACTORREFERENCEDCOLUMNNOTFOUND|%1 referencia a identificação de coluna %2!d! e essa coluna não foi encontrada na entrada. Uma referência aponta para uma coluna inexistente.|  
|0xC0208028|-1071611864|DTS_E_EXTRACTORDATACOLUMNNOTBLOB|O "%1" faz referência a "%2", e essa coluna não é do tipo BLOB.|  
|0xC0208029|-1071611863|DTS_E_INSERTERREFERENCEDCOLUMNNOTFOUND|"%1" referencia a identificação de coluna de saída %2!d! e essa coluna não foi encontrada na saída.|  
|0xC020802A|-1071611862|DTS_E_INSERTERCANTREAD|Falha na leitura do arquivo "%1" com o código de erro 0x%2!8.8X!.|  
|0xC020802B|-1071611861|DTS_E_TXSCD_NOTYPEDCOLUMNSATINPUT|Deve haver pelo menos uma coluna do tipo Fixo, Alteração ou Histórico na entrada de uma transformação Dimensão de Alteração Lenta. Verifique se pelo menos uma coluna é FixedAttribute, ChangingAttribute ou HistoricalAttribute.|  
|0xC020802C|-1071611860|DTS_E_TXSCD_INVALIDINPUTCOLUMNTYPE|A propriedade ColumnType de "%1" não é válida. O valor atual está fora do intervalo de valores aceitáveis.|  
|0xC020802D|-1071611859|DTS_E_TXSCD_CANNOTMAPDIFFERENTTYPES|A coluna de entrada "%1" não pode ser mapeada para a coluna externa "%2" porque elas têm tipos de dados diferentes. A transformação Dimensão de Alteração Lenta não permite o mapeamento entre colunas de tipos diferentes, exceto para tipos DT_STR e DT_WSTR.|  
|0xC020802E|-1071611858|DTS_E_NTEXTDATATYPENOTSUPPORTEDWITHANSIFILES|O tipo de dados para "%1" é DT_NTEXT, que não tem suporte com arquivos de ANSI. Em vez desse tipo de dados, use DT_TEXT e converta os dados em DT_NTEXT usando o componente de conversão de dados.|  
|0xC020802F|-1071611857|DTS_E_TEXTDATATYPENOTSUPPORTEDWITHUNICODEFILES|O tipo de dados para "%1" é DT_TEXT, que não tem suporte com arquivos Unicode. Em vez desse tipo de dados, use DT_NTEXT e converta os dados em DT_TEXT usando o componente de conversão de dados.|  
|0xC0208030|-1071611856|DTS_E_IMAGEDATATYPENOTSUPPORTED|O tipo de dados para "%1" é DT_IMAGE, que não tem suporte. Em vez desse tipo de dados, use DT_TEXT ou DT_NTEXT e converta os dados de ou em DT_IMAGE usando o componente de conversão de dados.|  
|0xC0208031|-1071611855|DTS_E_FLATFILEFORMATNOTSUPPORTED|O Gerenciador de Conexões de Arquivos Simples não fornece suporte ao formato "%1". Os formatos com suporte são Delimited, FixedWidth, RaggedRight e Mixed.|  
|0xC0208032|-1071611854|DTS_E_EXTRACTORFILENAMECOLUMNNOTSTRING|O "%1" deveria conter um nome de arquivo, mas não é do tipo Cadeia de caracteres.|  
|0xC0208033|-1071611853|DTS_E_EXTRACTORCANTAPPENDTRUNCATE|Erro causado por configurações de propriedade conflitantes. O "%1" tem as propriedades AllowAppend e ForceTruncate definidas como TRUE. Ambas as propriedades não podem ser definidas como TRUE. Defina uma das duas propriedades como FALSE.|  
|0xC0208034|-1071611852|DTS_E_EXTRACTORCOLUMNALREADYREFERENCED|%1 referencia a identificação de coluna %2!d!, mas essa coluna já foi referenciada por %3. Remova uma das duas referências à coluna.|  
|0xC0208035|-1071611851|DTS_E_CONNECTIONMANANGERNOTASSIGNED|O gerenciador de conexões não foi atribuído ao %1.|  
|0xC0208036|-1071611850|DTS_E_INSERTERCOLUMNALREADYREFERENCED|%1 referencia a coluna de saída com a identificação %2!d!, mas essa coluna já foi referenciada por %3.|  
|0xC0208037|-1071611849|DTS_E_INSERTERCOLUMNNOTREFERENCED|O "%1" não é referenciado por nenhuma coluna de entrada. Cada coluna de saída deve ser referenciada por exatamente uma coluna de entrada.|  
|0xC0208038|-1071611848|DTS_E_INSERTERDATACOLUMNNOTBLOB|O "%1" faz referência a "%2", e essa coluna não é do tipo correto. Deve ser DT_TEXT, DT_NTEXT ou DT_IMAGE. Uma referência aponta para uma coluna que deve ser BLOB.|  
|0xC0208039|-1071611847|DTS_E_INSERTERFILENAMECOLUMNNOTSTRING|O "%1" deveria conter um nome de arquivo, mas não é do tipo Cadeia de caracteres.|  
|0xC020803A|-1071611846|DTS_E_INSERTEREXPECTBOMINVALIDTYPE|O "%1" tem a propriedade ExpectBOM definida como TRUE para %2, mas a coluna não é NT_NTEXT. A propriedade ExpectBOM especifica que a transformação Importar Coluna deve esperar por uma marca de ordem de byte (BOM). Defina a propriedade ExpectBOM como falsa ou altere o tipo de dados da coluna de saída para DT_NTEXT.|  
|0xC020803B|-1071611845|DTS_E_INSERTERINVALIDDATACOLUMNSETTYPE|As colunas de saída de dados devem ser DT_TEXT, DT_NTEXT ou DT_IMAGE. A coluna de saída de dados só pode ser definida como um tipo BLOB.|  
|0xC020803C|-1071611844|DTS_E_TXSCD_FIXEDATTRIBUTECHANGE|Se a propriedade FailOnFixedAttributeChange for definida como TRUE, a transformação falhará quando uma alteração de atributo fixo for detectada. Para enviar linhas para a saída Atributo Fixo, defina a propriedade FailOnFixedAttributeChange como FALSE.|  
|0xC020803D|-1071611843|DTS_E_TXSCD_LOOKUPFAILURE|A transformação Pesquisa não recuperou nenhuma linha. A transformação falha quando FailOnLookupFailure está definido como TRUE e nenhuma linha é recuperada.|  
|0xC020803E|-1071611842|DTS_E_TXSCD_INVALIDNUMBERSOFPARAMETERS|Deve haver pelo menos um tipo de coluna de Chave na entrada de uma transformação Dimensão de Alteração Lenta. Defina pelo menos um tipo de coluna como Chave.|  
|0xC020803F|-1071611841|DTS_E_TXSCD_CANNOTFINDEXTERNALCOLUMN|Não é possível encontrar coluna externa com o nome "%1".|  
|0xC0208040|-1071611840|DTS_E_TXSCD_INFFEREDINDICATORNOTBOOL|A coluna "%1" de indicador inferido deve ser do tipo DT_BOOL.|  
|0xC0208107|-1071611641|DTS_E_ERRORROWDISPMUSTBENOTUSED|O %1 deve ter seu valor de disposição de linha de erro definido como RD_NotUsed.|  
|0xC0208108|-1071611640|DTS_E_TRUNCROWDISPMUSTBENOTUSED|O %1 deve ter seu valor de disposição de linha de truncamento definido como RD_NotUsed.|  
|0xC0208201|-1071611391|DTS_E_TXAGG_INPUTNOTFOUNDFOROUTPUT|Não é possível encontrar a coluna de entrada com a ID de linhagem %1!d! exigida pela coluna de saída com ID %2!d!.|  
|0xC0208202|-1071611390|DTS_E_TXAGG_INVALIDOUTPUTDATATYPEFORAGGREGATE|Tipo de dados de saída inválido para o tipo de agregação especificado na identificação da coluna de saída %1!d!.|  
|0xC0208203|-1071611389|DTS_E_TXAGG_INVALIDINPUTDATATYPEFORAGGREGATE|Tipo de dados de entrada inválido para %1 usado para a agregação especificada em %2.|  
|0xC0208204|-1071611388|DTS_E_TXAGG_INPUTOUTPUTDATATYPEMISMATCH|Os tipos de dados de identificação de linhagem da coluna de entrada %1!d! e a identificação da coluna de saída %2!d! não coincidem.|  
|0xC0208205|-1071611387|DTS_E_UNABLETOGETINPUTBUFFERHANDLE|Não é possível obter a identificação de buffer de entrada para a identificação de entrada %1!d!.|  
|0xC0208206|-1071611386|DTS_E_UNABLETOGETOUTPUTBUFFERHANDLE|Não é possível obter a identificação do buffer de saída para a identificação de saída %1!d!.|  
|0xC0208207|-1071611385|DTS_E_UNABLETOFINDCOLUMNHANDLEINOUTPUTBUFFER|Não é possível localizar a coluna com identificação de linhagem %1!d! no buffer de saída.|  
|0xC0208208|-1071611384|DTS_E_UNABLETOFINDCOLUMNHANDLEININPUTBUFFER|Não é possível localizar a coluna com identificação de linhagem %1!d! no buffer de entrada.|  
|0xC0208209|-1071611383|DTS_E_CANNOTHAVEZEROOUTPUTCOLUMNS|O número de colunas de saída para %1 não pode ser zero.|  
|0xC020820A|-1071611382|DTS_E_CONNECTIONMANAGERCOLUMNCOUNTMISMATCH|O número de colunas no gerenciador de conexões de arquivos simples deve ser igual ao número de colunas do adaptador de arquivos simples. O número de colunas para o gerenciador de conexões de arquivo simples é %1!d!, enquanto o número de colunas para o adaptador de arquivo simples é %2!d!.|  
|0xC020820B|-1071611381|DTS_E_MISMATCHCONNECTIONMANAGERCOLUMN|A coluna "%1" no índice %2!d! no gerenciador de conexões de arquivo simples não foi localizado no índice %3!d! na coleção de coluna do adaptador de arquivo simples.|  
|0xC020820D|-1071611379|DTS_E_EXTERNALMETADATACOLUMNISALREADYMAPPED|A coluna de metadados externa com identificação %1!d! já foi mapeada para %2.|  
|0xC020820E|-1071611378|DTS_E_TXAGG_STRING_TOO_LONG|A transformação encontrou uma coluna de chave com mais de %1!u! caracteres.|  
|0xC020820F|-1071611377|DTS_E_DERIVEDRESULT_TOO_LONG|A transformação encontrou um valor de resultado com mais de %1!u! bytes.|  
|0xC0208210|-1071611376|DTS_E_TXAGG_MEMALLOCERROUTPUTDESCRIPTORS|Não é possível alocar memória.|  
|0xC0208211|-1071611375|DTS_E_TXAGG_MEMALLOCERRWORKSPACEDESCRIPTORS|Não é possível alocar memória.|  
|0xC0208212|-1071611374|DTS_E_TXAGG_MEMALLOCERRSORTORDERDESCRIPTORS|Não é possível alocar memória.|  
|0xC0208213|-1071611373|DTS_E_TXAGG_MEMALLOCERRNUMERICDESCRIPTORS|Não é possível alocar memória.|  
|0xC0208214|-1071611372|DTS_E_TXAGG_MEMALLOCERRCOUNTDISTINCTDESCRIPTOR|Não é possível alocar memória.|  
|0xC0208215|-1071611371|DTS_E_TXAGG_MEMALLOCERRWORKSPACESORTORDERDESCRIPTORS|Não é possível alocar memória.|  
|0xC0208216|-1071611370|DTS_E_TXAGG_MEMALLOCERRWORKSPACENUMERICDESCRIPTORS|Não é possível alocar memória.|  
|0xC0208217|-1071611369|DTS_E_TXAGG_MEMALLOCERRWORKSPACEBUFFCOLS|Não é possível alocar memória.|  
|0xC0208218|-1071611368|DTS_E_UNREFERENCEDINPUTCOLUMN|A coluna de entrada "%1" não foi referenciada.|  
|0xC0208219|-1071611367|DTS_E_CANTBUILDTHREADPOOL|A transformação Classificação não pôde criar um pool de threads com %1!d! threads. Não existe memória suficiente.|  
|0xC020821A|-1071611366|DTS_E_QUEUEWORKITEMFAILED|A Classificar transformação não pode fazer fila um item de trabalho a sua piscina de thread. Não há memória suficiente.|  
|0xC020821B|-1071611365|DTS_E_SORTTHREADSTOPPED|Um thread de trabalho na transformação Classificação foi interrompido com o código de erro 0x%1!8.8X!. Foi encontrado um erro catastrófico durante a classificação de um buffer.|  
|0xC020821E|-1071611362|DTS_E_SORTBADTHREADCOUNT|MaxThreads era %1!ld! e deveria ficar entre 1 e %2!ld!, inclusive, ou -1 para assumir como padrão o número de CPUs.|  
|0xC020821F|-1071611361|DTS_E_DTPXMLLOADFAILURE|Não é possível carregar do XML.|  
|0xC0208220|-1071611360|DTS_E_DTPXMLSAVEFAILURE|Não é possível salvar em XML.|  
|0xC0208221|-1071611359|DTS_E_DTPXMLINT32CONVERTERR|Não é possível converter o valor "%1" em inteiro.|  
|0xC0208222|-1071611358|DTS_E_DTPXMLBOOLCONVERTERR|Não é possível converter o valor "%1" em booliano.|  
|0xC0208223|-1071611357|DTS_E_DTPXMLPARSEERRORNEARID|Erro de carregamento próximo ao objeto com a identificação %1!d!.|  
|0xC0208226|-1071611354|DTS_E_DTPXMLPROPERTYTYPEERR|O valor "%1" não é válido para o atributo "%2".|  
|0xC0208228|-1071611352|DTS_E_DTPXMLSETUSAGETYPEERR|O valor "%1" não é válido para o atributo "%2".|  
|0xC0208229|-1071611351|DTS_E_DTPXMLDATATYPEERR|O valor "%1" não é válido para o atributo "%2".|  
|0xC020822A|-1071611350|DTS_E_UNMAPPEDINPUTCOLUMN|O %1 não é mapeado para uma coluna de saída.|  
|0xC020822B|-1071611349|DTS_E_INPUTCOLUMNBADMAP|O %1 tem um mapeamento inválido.  Uma coluna de saída com uma identificação de %2!ld! não existe neste componente.|  
|0xC020822D|-1071611347|DTS_E_MULTIPLYMAPPEDOUTCOL|O %1 é mapeado para uma coluna de saída que já tem um mapeamento nessa entrada.|  
|0xC020822E|-1071611346|DTS_E_TXAGG_STRINGPROMOTIONFAILED|Não foi possível converter a coluna de entrada com identificação de linhagem %1!ld! para DT_WSTR devido ao erro 0x%2!8.8X!.|  
|0xC0208230|-1071611344|DTS_E_DTPXMLIDLOOKUPERR|Objeto referenciado com ID %1!d! não encontrado no pacote.|  
|0xC0208231|-1071611343|DTS_E_DTPXMLINVALIDXMLPERSISTPROPERTY|Não é possível ler uma propriedade de persistência necessária para o módulo pipelinexml. A propriedade não foi fornecida pelo pipeline.|  
|0xC0208232|-1071611342|DTS_E_DTPXMLPROPERTYSTATEERR|O valor "%1" não é válido para o atributo "%2".|  
|0xC0208233|-1071611341|DTS_E_CANTGETCUSTOMPROPERTY|Não é possível recuperar a propriedade personalizada "%1".|  
|0xC0208234|-1071611340|DTS_E_UNABLETOLOCATEINPUTCOLUMNID|Uma coluna de entrada com a identificação de linhagem %1!d!, referenciada na propriedade personalizada ParameterMap com o parâmetro na posição número %2!d!, não pode ser encontrada na coleção de colunas de entrada.|  
|0xC0208235|-1071611339|DTS_E_TXLOOKUP_UNABLETOLOCATEREFCOLUMN|Não é possível localizar a coluna de referência "%1".|  
|0xC0208236|-1071611338|DTS_E_TXLOOKUP_INCOMPATIBLEDATATYPES|%1 e a coluna de referência de nome "%2" têm tipos de dados incompatíveis.|  
|0xC0208237|-1071611337|DTS_E_TXLOOKUP_PARAMMETADATAMISMATCH|A instrução SQL com parâmetros gera metadados que não correspondem à instrução SQL principal.|  
|0xC0208238|-1071611336|DTS_E_TXLOOKUP_INCORRECTNUMOFPARAMETERS|A instrução SQL com parâmetros contém um número incorreto de parâmetros. Esperado: %1!d!. Encontrado: %2!d!.|  
|0xC0208239|-1071611335|DTS_E_TXLOOKUP_INVALIDJOINTYPE|%1 tem um tipo de dados que não pode ser unido.|  
|0xC020823A|-1071611334|DTS_E_TXLOOKUP_INVALIDCOPYTYPE|%1 tem um tipo de dados que não pode ser copiado.|  
|0xC020823B|-1071611333|DTS_E_INSERTERINVALIDCOLUMNDATATYPE|O %1 tem um tipo de dados sem-suporte. Deve ser DT_STR ou DT_WSTR.|  
|0xC020823C|-1071611332|DTS_E_EXTRACTORINVALIDCOLUMNDATATYPE|O %1 tem um tipo de dados sem-suporte. Deve ser DT_STR, DT_WSTR, DT_TEXT, DT_NTEXT ou DT_IMAGE.|  
|0xC020823D|-1071611331|DTS_E_TXCHARMAPINVALIDCOLUMNDATATYPE|O %1 tem um tipo de dados sem-suporte. Deve ser DT_STR, DT_WSTR, DT_TEXT ou DT_NTEXT.|  
|0xC020823E|-1071611330|DTS_E_SORTCANTCREATEEVENT|A transformação Classificação não pode criar um evento para comunicar com seus threads de trabalho. Não há manipuladores de sistema suficientes para a transformação Classificação.|  
|0xC020823F|-1071611329|DTS_E_SORTCANTCREATETHREAD|A transformação Classificação não pode criar um thread de trabalho. Não há memória suficiente para a transformação Classificação.|  
|0xC0208240|-1071611328|DTS_E_SORTCANTCOMPARE|A transformação de Classificação não comparou a linha %1!d! a ID de buffer %2!d! com a linha %3!d! na identificação de buffer %4!d!.|  
|0xC0208242|-1071611326|DTS_E_TXLOOKUP_TOOFEWREFERENCECOLUMNS|Os metadados de referência da transformação Pesquisa contêm poucas colunas. Verifique a propriedade SQLCommand. A instrução SELECT deve retornar pelo menos uma coluna.|  
|0xC0208243|-1071611325|DTS_E_TXLOOKUP_MALLOCERR_REFERENCECOLUMNINFO|Não é possível alocar memória para uma matriz de estruturas ColumnInfo.|  
|0xC0208244|-1071611324|DTS_E_TXLOOKUP_MALLOCERR_REFERENCECOLUMNPAIR|Não foi possível alocar memória para uma matriz de estruturas ColumnPair.|  
|0xC0208245|-1071611323|DTS_E_TXLOOKUP_MALLOCERR_BUFFCOL|Não é possível alocar memória para uma matriz de estruturas BUFFCOL para a criação de um workspace principal.|  
|0xC0208246|-1071611322|DTS_E_TXLOOKUP_MAINWORKSPACE_CREATEERR|Não é possível criar um buffer de workspace principal.|  
|0xC0208247|-1071611321|DTS_E_TXLOOKUP_HASHTABLE_MALLOCERR|Não é possível alocar memória para uma tabela de hash.|  
|0xC0208248|-1071611320|DTS_E_TXLOOKUP_HASHNODEHEAP_CREATEERR|Não é possível alocar memória para criar um heap para nós de hash.|  
|0xC0208249|-1071611319|DTS_E_TXLOOKUP_HASHNODEHEAP_MALLOCERR|Não é possível alocar memória para um heap de nó de hash.|  
|0xC020824A|-1071611318|DTS_E_TXLOOKUP_LRUNODEHEAP_CREATEERR|Não é possível criar um heap para nós LRU. Houve falta de memória.|  
|0xC020824B|-1071611317|DTS_E_TXLOOKUP_LRUNODEHEAP_MALLOCERR|Não é possível alocar memória para um heap de nó LRU. Houve falta de memória.|  
|0xC020824C|-1071611316|DTS_E_TXLOOKUP_OLEDBERR_LOADCOLUMNMETADATA|Ocorreu um erro OLE DB ao carregar os metadados da coluna. Verifique as propriedades SQLCommand e SqlCommandParam.|  
|0xC020824D|-1071611315|DTS_E_TXLOOKUP_OLEDBERR_GETIROWSET|Ocorreu um erro OLE DB ao buscar um conjunto de linhas. Verifique as propriedades SQLCommand e SqlCommandParam.|  
|0xC020824E|-1071611314|DTS_E_TXLOOKUP_OLEDBERR_FILLBUFFER|Ocorreu um erro OLE DB ao popular o cache interno. Verifique as propriedades SQLCommand e SqlCommandParam.|  
|0xC020824F|-1071611313|DTS_E_TXLOOKUP_OLEDBERR_BINDPARAMETERS|Ocorreu um erro OLE DB ao associar os parâmetros. Verifique as propriedades SQLCommand e SqlCommandParam.|  
|0xC0208250|-1071611312|DTS_E_TXLOOKUP_OLEDBERR_CREATEBINDING|Ocorreu um erro OLE DB ao criar associações. Verifique as propriedades SQLCommand e SqlCommandParam.|  
|0xC0208251|-1071611311|DTS_E_TXLOOKUP_INVALID_CASE|Encontrado um caso inválido em uma instrução switch durante o tempo de execução.|  
|0xC0208252|-1071611310|DTS_E_TXLOOKUP_MAINWORKSPACE_MALLOCERR|Não é possível alocar memória para uma linha nova do buffer de workspace principal. Houve falta de memória.|  
|0xC0208253|-1071611309|DTS_E_TXLOOKUP_OLEDBERR_GETPARAMIROWSET|Ocorreu um erro OLE DB ao buscar um conjunto de linhas com parâmetros. Verifique as propriedades SQLCommand e SqlCommandParam.|  
|0xC0208254|-1071611308|DTS_E_TXLOOKUP_OLEDBERR_GETPARAMSINGLEROW|Ocorreu um erro OLE DB ao buscar uma linha com parâmetros. Verifique as propriedades SQLCommand e SqlCommandParam.|  
|0xC0208255|-1071611307|DTS_E_TXAGG_MAINWORKSPACE_MALLOCERR|Não é possível alocar memória para uma linha nova do buffer de workspace principal. Houve falta de memória.|  
|0xC0208256|-1071611306|DTS_E_TXAGG_MAINWORKSPACE_CREATEERR|Não é possível criar um buffer de workspace principal.|  
|0xC0208257|-1071611305|DTS_E_TXAGG_HASHTABLE_MALLOCERR|Não é possível alocar memória para a tabela de hash.|  
|0xC0208258|-1071611304|DTS_E_TXAGG_HASHNODEHEAP_CREATEERR|Não é possível alocar memória para criar um heap para os nós de hash.|  
|0xC0208259|-1071611303|DTS_E_TXAGG_HASHNODEHEAP_MALLOCERR|Não é possível alocar memória para o heap de nó de hash.|  
|0xC020825A|-1071611302|DTS_E_TXAGG_CDNODEHEAP_CREATEERR|Não é possível alocar memória para criar um heap para nós CountDistinct.|  
|0xC020825B|-1071611301|DTS_E_TXAGG_CDNODEHEAP_MALLOCERR|Não é possível alocar memória para heap de nó CountDistinct.|  
|0xC020825C|-1071611300|DTS_E_TXAGG_CDCHAINHEAP_CREATEERR|Não é possível alocar memória para criar um heap para cadeias CountDistinct.|  
|0xC020825D|-1071611299|DTS_E_TXAGG_CDHASHTABLE_CREATEERR|Não é possível alocar memória para a tabela de hash CountDistinct.|  
|0xC020825E|-1071611298|DTS_E_TXAGG_CDWORKSPACE_MALLOCERR|Não é possível alocar memória para uma linha nova do buffer de workspace CountDistinct.|  
|0xC020825F|-1071611297|DTS_E_TXAGG_CDWORKSPACE_CREATEERR|Não é possível criar um buffer de workspace CountDistinct.|  
|0xC0208260|-1071611296|DTS_E_TXAGG_CDCOLLASSEARRAY_MALLOCERR|Não é possível alocar memória para uma matriz CountDistinct Collapse.|  
|0xC0208261|-1071611295|DTS_E_TXAGG_CDCHAINHEAP_MALLOCERR|Não é possível alocar memória para cadeias CountDistinct.|  
|0xC0208262|-1071611294|DTS_E_TXCOPYMAP_MISMATCHED_COLUMN_METADATA|As colunas com identificações de linhagem %1!d! e %2!d! possuem metadados que não coincidem. A coluna de entrada mapeada para uma coluna de saída para copymap não tem os mesmos metadados (tipo de dados, precisão, escala, comprimento ou página de código).|  
|0xC0208263|-1071611293|DTS_E_TXCOPYMAP_INCORRECT_OUTPUT_COLUMN_MAPPING|A coluna de saída com ID de linhagem "%1!d!" está mapeada incorretamente a uma coluna de entrada. A propriedade CopyColumnId da coluna de saída não está correta.|  
|0xC0208265|-1071611291|DTS_E_CANTGETBLOBDATA|Falha ao recuperar os dados long para a coluna "%1".|  
|0xC0208266|-1071611290|DTS_E_CANTADDBLOBDATA|Dados long foram recuperados para uma coluna, mas não podem ser adicionados ao buffer da tarefa Fluxo de Dados.|  
|0xC0208267|-1071611289|DTS_E_MCASTOUTPUTCOLUMNS|A saída "%1" (%2!d!) em colunas de saída, mas saídas multicast não declaram colunas. O pacote está danificado.|  
|0xC0208273|-1071611277|DTS_E_UNABLETOGETLOCALIZEDRESOURCE|Não é possível carregar uma identificação de recurso localizada %1!d!. Verifique se existe o arquivo RLL.|  
|0xC0208274|-1071611276|DTS_E_DTPXMLEVENTSCACHEERR|Não é possível adquirir Interface de Eventos. Uma Interface de Eventos inválida foi passada para o módulo de fluxo de dados para persistir no XML.|  
|0xC0208275|-1071611275|DTS_E_DTPXMLPATHLOADERR|Ocorreu um erro durante a configuração de um objeto de caminho ao carregar o XML.|  
|0xC0208276|-1071611274|DTS_E_DTPXMLINPUTLOADERR|Erro de configuração do objeto de entrada ao carregar o XML.|  
|0xC0208277|-1071611273|DTS_E_DTPXMLOUTPUTLOADERR|Erro de configuração do objeto de saída ao carregar o XML.|  
|0xC0208278|-1071611272|DTS_E_DTPXMLINPUTCOLUMNLOADERR|Erro de configuração do objeto de coluna de entrada ao carregar o XML.|  
|0xC0208279|-1071611271|DTS_E_DTPXMLOUTPUTCOLUMNLOADERR|Erro de configuração do objeto de coluna de saída ao carregar o XML.|  
|0xC0208280|-1071611264|DTS_E_DTPXMLPROPERTYLOADERR|Erro de configuração do objeto de propriedade ao carregar o XML.|  
|0xC0208281|-1071611263|DTS_E_DTPXMLCONNECTIONLOADERR|Erro de configuração do objeto de conexão ao carregar o XML.|  
|0xC0208282|-1071611262|DTS_E_FG_MISSING_OUTPUT_COLUMNS|Estão faltando colunas especiais de transformação específica ou seus tipos estão incorretos.|  
|0xC0208283|-1071611261|DTS_E_FG_PREPARE_TABLES_AND_ACCESSORS|Falha na transformação Agrupamento Difuso ao criar as tabelas e os acessadores necessários.|  
|0xC0208284|-1071611260|DTS_E_FG_COPY_INPUT|Falha na transformação Agrupamento Difuso ao copiar a entrada.|  
|0xC0208285|-1071611259|DTS_E_FG_GENERATE_GROUPS|Falha na transformação Agrupamento Difuso ao gerar grupos.|  
|0xC0208286|-1071611258|DTS_E_FG_LEADING_TRAILING|Erro inesperado em Agrupamento Difuso ao aplicar as configurações da propriedade '%1'.|  
|0xC0208287|-1071611257|DTS_E_FG_PICK_CANONICAL|Falha na transformação Agrupamento Difuso ao escolher uma linha canônica de dados para usar na padronização dos dados.|  
|0xC0208288|-1071611256|DTS_E_FG_NOBLOBS|Não existe suporte para colunas de entrada do tipo IMAGE, TEXT ou NTEXT no Agrupamento Difuso.|  
|0xC0208289|-1071611255|DTS_E_FG_FUZZY_MATCH_ON_NONSTRING|Uma correspondência difusa foi especificada na coluna "%1" (%2!d!) que não é um tipo de dados DT_STR ou DT_WSTR.|  
|0xC020828A|-1071611254|DTS_E_FUZZYGROUPINGINTERNALPIPELINEERROR|Erro de pipeline de transformação Agrupamento Difuso com o código de erro 0x%1!8.8X!: "%2".|  
|0xC020828B|-1071611253|DTS_E_CODE_PAGE_NOT_SUPPORTED|A página de código %1!d! especificada na coluna de saída "%2" (%3!d!) não é suportada.  Primeiro, converta essa coluna em DT_WSTR, inserindo uma Transformação de Conversão de Dados antes desta.|  
|0xC0208294|-1071611244|DTS_E_SETEODFAILED|Falha ao definir o final do sinalizador de dados para o buffer que orienta a saída "%1" (%2!d!).|  
|0xC0208296|-1071611242|DTS_E_CANTCLONE|Não foi possível clonar o buffer de entrada. Houve falta de memória, ou ocorreu um erro interno.|  
|0xC02082F9|-1071611143|DTS_E_TXCHARMAP_CANTKATAKANAHIRAGANA|A coluna "%1" solicita que os caracteres Katakana e Hiragana sejam produzidos ao mesmo tempo.|  
|0xC02082FA|-1071611142|DTS_E_TXCHARMAP_CANTSIMPLECOMPLEX|A coluna "%1" solicita que os caracteres simples e tradicionais em chinês sejam produzidos ao mesmo tempo.|  
|0xC02082FB|-1071611141|DTS_E_TXCHARMAP_CANTFULLHALF|A coluna "%1" solicita operações para gerar caracteres de meia largura e de largura inteira.|  
|0xC02082FC|-1071611140|DTS_E_TXCHARMAP_CANTCHINAJAPAN|A coluna "%1" combina operações em caracteres japoneses com operações para caracteres chineses.|  
|0xC02082FD|-1071611139|DTS_E_TXCHARMAP_CANTCASECHINESE|A coluna "%1" combina operações em caracteres chineses com operações em caracteres maiúsculos e minúsculos.|  
|0xC02082FE|-1071611138|DTS_E_TXCHARMAP_CANTCASEJAPANESE|A coluna "%1" combina operações em caracteres japoneses com operações em caracteres maiúsculos e minúsculos.|  
|0xC02082FF|-1071611137|DTS_E_TXCHARMAP_CANTBOTHCASE|A coluna "%1" mapeia a coluna para letras maiúsculas e minúsculas.|  
|0xC0208300|-1071611136|DTS_E_TXCHARMAP_CANTLINGUISTIC|A coluna "%1" combina sinalizadores sem letras maiúsculas e minúsculas com a operação de uso linguístico de maiúsculas e minúsculas.|  
|0xC0208301|-1071611135|DTS_E_TXCHARMAP_INVALIDMAPFLAGANDDATATYPE|O tipo de dados da coluna "%1" não pode ser mapeado como especificado.|  
|0xC0208302|-1071611134|DTS_E_TXFUZZYLOOKUP_UNSUPPORTED_MATCH_INDEX_VERSION|Não existe suporte para a versão (%1) do índice de correspondência pré-existente "%2". A versão esperada é "%3". Esse erro ocorre se a versão persistente nos metadados de índice não corresponde à versão para a qual o código atual foi criado. Corrija o erro, recriando o índice com a versão atual do código.|  
|0xC0208303|-1071611133|DTS_E_TXFUZZYLOOKUP_INVALID_MATCH_INDEX|A tabela "%1" parece não ser um índice válido de correspondência pré-criado. Esse erro ocorre quando o registro de metadados não pode ser carregado do índice especificado pré-criado.|  
|0xC0208304|-1071611132|DTS_E_TXFUZZYLOOKUP_UNABLE_TO_READ_MATCH_INDEX|Não é possível ler o índice de correspondência "%1" especificado e pré-criado.  Código de erro OLEDB: 0x%2!8.8X!.|  
|0xC0208305|-1071611131|DTS_E_TXFUZZYLOOKUP_NO_JOIN_COLUMNS|Não havia nenhuma coluna de entrada com uma junção válida para uma coluna da tabela de referência.  Verifique se existe pelo menos uma junção definida, usando as propriedades JoinToReferenceColumn e JoinType da coluna de entrada.|  
|0xC0208306|-1071611130|DTS_E_TXFUZZYLOOKUP_INDEX_DOES_NOT_CONTAIN_COLUMN|O índice de correspondência "%1" pré-existente especificado não foi criado originalmente com informações de correspondência difusa para a coluna "%2".  Ele deve ser recriado para incluir essas informações. Esse erro ocorre quando o índice foi criado com uma coluna que não era de junção difusa.|  
|0xC0208307|-1071611129|DTS_E_TXFUZZYLOOKUP_IDENTIFIER_PROPERTY|O nome "%1" atribuído à propriedade "%2" não é um nome válido de identificador SQL. Esse erro ocorre se o nome da propriedade não estiver de acordo com as especificações de um nome de identificador SQL.|  
|0xC0208309|-1071611127|DTS_E_TXFUZZYLOOKUP_MINSIMILARITY_INVALID|O valor da propriedade de limite MinSimilarity na transformação Pesquisa Difusa deve ser maior que ou igual a 0.0, mas menor que 1.0.|  
|0xC020830A|-1071611126|DTS_E_TXFUZZYLOOKUP_INVALID_PROPERTY_VALUE|O valor "%1" da propriedade "%2" não é válido.|  
|0xC020830B|-1071611125|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_FUZZY_JOIN_DATATYPES|A pesquisa difusa especificada entre a coluna de entrada "%1" e a coluna de referência "%2" não é válida porque existe suporte somente para junções difusas entre colunas de cadeia de caracteres do tipo DT_STR e DT_WSTR.|  
|0xC020830C|-1071611124|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_EXACT_JOIN_DATATYPES|As colunas de pesquisa exata, "%1" e "%2", não têm tipos de dados iguais ou não são de tipos de cadeia de caracteres comparáveis. Existe suporte para junções exatas entre colunas com tipos de dados iguais ou com uma combinação de DT_STR e DT_WSTR.|  
|0xC020830D|-1071611123|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_COPYCOLUMN_DATATYPES|As colunas de cópia, "%1" e "%2", não têm tipos de dados iguais ou não são de tipos de cadeia de caracteres facilmente conversíveis. Isso ocorre porque existe suporte para copiar da referência para a saída entre colunas com tipos de dados iguais, ou com uma combinação de DT_STR e DT_WSTR, mas não para outros tipos.|  
|0xC020830E|-1071611122|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_PASSTHRUCOLUMN_DATATYPES|As colunas de passagem, "%1" e "%2", não têm tipos de dados iguais. Existe suporte somente para colunas com tipos de dados iguais como colunas de passagem da entrada para a saída.|  
|0xC020830F|-1071611121|DTS_E_TXFUZZYLOOKUP_UNABLETOLOCATEREFCOLUMN|Não é possível localizar a coluna de referência "%1".|  
|0xC0208311|-1071611119|DTS_E_TXFUZZYLOOKUP_OUTPUT_COLUMN_MUST_BE_PASSTHRU_COLUMN_OR_A_COPY_COLUMN|Uma coluna de saída deve ter exatamente uma propriedade CopyColumn ou PassThruColumn especificada. Esse erro ocorre se nem a propriedade CopyColumn nem a PassThruColumn, ou se ambas as propriedades, CopyColumn e PassThruColumn, estiverem definidas como valores não vazios.|  
|0xC0208312|-1071611118|DTS_E_TXFUZZYLOOKUP_PASSTHRU_COLUMN_NOT_FOUND|A ID da linhagem de origem '%1!d!' especificada para a propriedade '%2' na coluna de saída '%3' não foi encontrada na coleção de colunas de entrada. Isso ocorre quando a identificação da coluna de entrada especificada em uma coluna de saída como coluna de passagem não é encontrada no conjunto de entradas.|  
|0xC0208313|-1071611117|DTS_E_TXFUZZYLOOKUP_INDEXED_COLUMN_NOT_FOUND_IN_REF_TABLE|A coluna "%1" no índice "%2" criado previamente não foi encontrada na consulta/tabela de referência. Isso ocorre se o esquema/consulta da tabela de referência foi alterado desde a criação do índice de correspondência pré-existente.|  
|0xC0208314|-1071611116|DTS_E_TXFUZZYLOOKUP_TOKEN_TOO_LONG|O componente encontrou um token maior que 2147483647 caracteres.|  
|0xC0208315|-1071611115|DTS_E_RAWMETADATAMISMATCHTYPE|O arquivo de saída não pode ser anexado. A coluna "%1" faz a correspondência por nome, mas a coluna do arquivo tem tipo %2 e a coluna de entrada tem tipo %3. Os metadados da coluna não correspondem em tipo de dados.|  
|0xC0208316|-1071611114|DTS_E_RAWMETADATAMISMATCHSIZE|O arquivo de saída não pode ser anexado. A coluna "%1" faz a correspondência por nome, mas a coluna no arquivo tem o comprimento máximo de %2!d! e a coluna de entrada tem comprimento máximo de %3!d!. Os metadados da coluna não correspondem em comprimento.|  
|0xC0208317|-1071611113|DTS_E_RAWMETADATAMISMATCHCODEPAGE|O arquivo de saída não pode ser anexado. A coluna "%1" faz a correspondência por nome, mas a coluna do arquivo tem a página de código %2!d! e a coluna de entrada tem página de código %3!d!. Os metadados da coluna nomeada não correspondem em página de código.|  
|0xC0208318|-1071611112|DTS_E_RAWMETADATAMISMATCHPRECISION|O arquivo de saída não pode ser anexado. A coluna "%1" faz a correspondência por nome, mas a coluna no arquivo tem a precisão %2!d! e a coluna de entrada tem precisão %3!d!. Os metadados da coluna nomeada não correspondem em precisão.|  
|0xC0208319|-1071611111|DTS_E_RAWMETADATAMISMATCHSCALE|O arquivo de saída não pode ser anexado. A coluna "%1" faz a correspondência por nome, mas a coluna no arquivo tem a escala %2!d! e a coluna de entrada tem escala %3!d!.  Os metadados da coluna nomeada não correspondem em escala.|  
|0xC020831A|-1071611110|DTS_E_COULD_NOT_DETERMINE_DATASOURCE_DBMSNAME|Não é possível determinar a versão e o nome DBMS em "%1". Isso ocorre se IDBProperties na conexão não retorna as informações necessárias para verificar a versão e o nome DBMS.|  
|0xC020831B|-1071611109|DTS_E_INCORRECT_SQL_SERVER_VERSION|Não existe suporte para o tipo ou a versão DBMS do "%1".  É necessária uma conexão para versão 8.0 ou posterior do Microsoft SQL Server. Isso ocorre se IDBProperties na conexão não retornar uma versão correta.|  
|0xC020831D|-1071611107|DTS_E_CANTDELETEERRORCOLUMNS|O %1 é uma coluna de saída de erro especial e não pode ser excluído.|  
|0xC020831E|-1071611106|DTS_E_UNEXPECTEDCOLUMNDATATYPE|O tipo de dados especificado para a coluna "%1" não é do tipo "%2" esperado.|  
|0xC020831F|-1071611105|DTS_E_INPUTCOLUMNNOTFOUND|A ID de linhagem de coluna "%1" referenciada pela propriedade "%2" na coluna de saída "%3" não foi localizada na coleção de colunas de entrada.|  
|0xC0208320|-1071611104|DTS_E_TXGROUPDUPS_INPUTCOLUMNNOTJOINED|A coluna de entrada "%1" referenciada pela propriedade "%2" na coluna de saída "%3" deve ter a propriedade ToBeCleaned=True e ter um valor válido da propriedade ExactFuzzy.|  
|0xC0208322|-1071611102|DTS_E_TXFUZZYLOOKUP_REF_TABLE_MISSING_IDENTITY_INDEX|A tabela de referência '%1' não tem um índice clusterizado em uma coluna de identidade de número inteiro, necessário se a propriedade 'CopyRefTable' estiver definida como FALSE. Se CopyRefTable for falso, a tabela de referência deve ter um índice clusterizado em uma coluna de identidade de número inteiro.|  
|0xC0208323|-1071611101|DTS_E_TXFUZZYLOOKUP_REF_CONTAINS_NON_INTEGER_IDENT_COLUMN|A tabela de referência '%1' contém uma coluna de identidade de tipo de número não inteiro, que não tem suporte. Use uma exibição da tabela sem a coluna '%2'.  Esse erro ocorre porque quando é feita uma cópia da tabela de referência, é adicionada uma coluna de identidade de número inteiro, e é permitida somente uma coluna de identidade por tabela.|  
|0xC0208324|-1071611100|DTS_E_TXFUZZY_MATCHCONTRIBUTION_AND_HIERARCHY_SPECIFIED|As informações MatchContribution e de hierarquia não podem ser especificadas ao mesmo tempo. Isso não é permitido porque essas duas propriedades são fatores de ponderação para pontuação.|  
|0xC0208325|-1071611099|DTS_E_TXFUZZY_HIERARCHY_INCORRECT|Os níveis na hierarquia devem ser números exclusivos. Um nível válido em valores de hierarquia são números inteiros maiores ou iguais a 1. Quanto menor for o número, mais baixa será a hierarquia da coluna. O valor padrão é 0, indicando que a coluna não faz parte de uma hierarquia. Não são permitidas sobreposições e lacunas.|  
|0xC0208326|-1071611098|DTS_E_TXFUZZYGROUPING_INSUFFICIENT_FUZZY_JOIN_COLUMNS|Não foi definida nenhuma coluna para agrupamento difuso.  Deve haver pelo menos uma coluna de entrada com propriedades de coluna ToBeCleaned=true e ExactFuzzy=2.|  
|0xC0208329|-1071611095|DTS_E_TXFUZZYLOOKUP_COLUMNINVALID|A coluna com a ID %1!d! é inválida por um motivo indeterminado.|  
|0xC020832A|-1071611094|DTS_E_TXFUZZYLOOKUP_UNSUPPORTEDDATATYPE|Não existe suporte para o tipo de dados da coluna '%1'.|  
|0xC020832C|-1071611092|DTS_E_TXFUZZYLOOKUP_OUTPUTLENGTHMISMATCH|O comprimento da coluna de saída '%1' é menor que o da sua coluna de origem '%2'.|  
|0xC020832F|-1071611089|DTS_E_TERMEXTRACTION_INCORRECTEXACTNUMBEROFINPUTCOLUMNS|Deveria haver só uma coluna de entrada.|  
|0xC0208330|-1071611088|DTS_E_TERMEXTRACTION_INCORRECTEXACTNUMBEROFOUTPUTCOLUMNS|Deveria haver exatamente duas colunas de saída.|  
|0xC0208331|-1071611087|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFINPUTCOLUMN|A coluna de entrada só pode ter tipos de dados DT_WSTR ou DT_NTEXT.|  
|0xC0208332|-1071611086|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFOUTPUTCOLUMN|A coluna de saída [%1!d!] só pode ter '%2' como seu tipo de dados.|  
|0xC0208333|-1071611085|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFREFERENCECOLUMN|A coluna de referência só pode ter tipos de dados DT_STR ou DT_WSTR.|  
|0xC0208334|-1071611084|DTS_E_TERMEXTRACTION_UNABLETOLOCATEREFCOLUMN|Erro durante a localização da coluna de referência '%1'.|  
|0xC0208335|-1071611083|DTS_E_TERMEXTRACTION_INCORRECTTERMTYPE|O Tipo de Termo da transformação só pode ser WordOnly, PhraseOnly ou WordPhrase.|  
|0xC0208336|-1071611082|DTS_E_TERMEXTRACTION_INCORRECTFREQUENCYTHRESHOLD|O valor de Limite de Frequência não deve ser inferior a '%1!d!'.|  
|0xC0208337|-1071611081|DTS_E_TERMEXTRACTION_INCORRECTMAXLENOFTERM|O valor de Comprimento Máximo do Termo não deve ser inferior a '%1!d!'.|  
|0xC0208338|-1071611080|DTS_E_TERMEXTRACTION_TOOFEWREFERENCECOLUMNS|Os metadados de referência de Extração de Termo contêm poucas colunas.|  
|0xC0208339|-1071611079|DTS_E_TERMEXTRACTION_MALLOCERR_REFERENCECOLUMNINFO|Ocorreu um erro durante a alocação de memória.|  
|0xC020833A|-1071611078|DTS_E_TERMEXTRACTION_MAINWORKSPACE_CREATEERR|Ocorreu um erro durante a criação de um buffer de workspace.|  
|0xC020833B|-1071611077|DTS_E_TERMEXTRACTION_OLEDBERR_CREATEBINDING|Ocorreu um erro OLEDB durante a criação de associações.|  
|0xC020833C|-1071611076|DTS_E_TERMEXTRACTION_OLEDBERR_GETIROWSET|Ocorreu um erro OLEDB durante a busca em conjuntos de linhas.|  
|0xC020833D|-1071611075|DTS_E_TERMEXTRACTION_OLEDBERR_FILLBUFFER|Ocorreu um erro OLE DB ao popular o cache interno.|  
|0xC020833E|-1071611074|DTS_E_TERMEXTRACTION_PROCESSERR|Erro ao extrair os termos na linha %1!ld!, coluna %2!ld!. O código de erro retornado foi 0x%3!8.8X!. Remova-o da entrada como solução.|  
|0xC020833F|-1071611073|DTS_E_TERMEXTRACTIONORLOOKUP_PROCESSERR_DEPOSITFULL|O número de candidatos a termo excede seu limite, 4G.|  
|0xC0208340|-1071611072|DTS_E_TERMEXTRACTION_INVALIDOUTTERMTABLEORCOLUMN|A tabela, exibição ou coluna de referência usada para Termos de Exclusão não é válida.|  
|0xC0208341|-1071611071|DTS_E_TXFUZZYLOOKUP_STRINGCOLUMNTOOLONG|O comprimento da coluna de cadeia de caracteres '%1' excede 4.000 caracteres.  É necessária uma conversão de DT_STR para DT_WSTR, assim ocorreria um truncamento.  Reduza a largura da coluna ou use somente tipos de coluna DT_WSTR.|  
|0xC0208342|-1071611070|DTS_E_TERMEXTRACTION_OUTTERMTABLEANDCOLUMNNOTSET|A tabela, exibição ou coluna de referência a ser usada para Termos de Exclusão não foi definida.|  
|0xC0208343|-1071611069|DTS_E_TERMLOOKUP_TOOFEWOUTPUTCOLUMNS|A Pesquisa de Termos contém poucas colunas de saída.|  
|0xC0208344|-1071611068|DTS_E_TERMLOOKUP_INCORRECTDATATYPEOFREFERENCECOLUMN|A coluna de referência só pode ter tipos de dados DT_STR ou DT_WSTR.|  
|0xC0208345|-1071611067|DTS_E_TERMLOOKUP_UNABLETOLOCATEREFCOLUMN|Erro durante a localização da coluna de referência '%1'.|  
|0xC0208346|-1071611066|DTS_E_TERMLOOKUP_TOOFEWREFERENCECOLUMNS|Os metadados de referência de Pesquisa de Termo contêm poucas colunas.|  
|0xC0208347|-1071611065|DTS_E_TERMEXTRACTIONORLOOKUP_TESTOFFSETERROR|Ocorreu um erro durante a normalização das palavras.|  
|0xC0208348|-1071611064|DTS_E_TERMLOOKUP_MAINWORKSPACE_CREATEERR|Ocorreu um erro durante a criação de um buffer de workspace.|  
|0xC0208349|-1071611063|DTS_E_TERMLOOKUP_OLEDBERR_CREATEBINDING|Ocorreu um erro OLEDB durante a criação de associações.|  
|0xC020834A|-1071611062|DTS_E_TERMLOOKUP_OLEDBERR_GETIROWSET|Ocorreu um erro OLEDB durante a busca em conjuntos de linhas.|  
|0xC020834B|-1071611061|DTS_E_TERMLOOKUP_OLEDBERR_FILLBUFFER|Ocorreu um erro OLE DB ao popular o cache interno.|  
|0xC020834C|-1071611060|DTS_E_TERMLOOKUP_PROCESSERR|Erro ao pesquisar os termos na linha %1!ld!, coluna %2!ld!. O código de erro retornado foi 0x%3!8.8X!. Remova-o da entrada como solução.|  
|0xC020834D|-1071611059|DTS_E_TERMLOOKUP_TEXTIDINPUTCOLUMNNOTMAPPEDWITHOUTPUTCOLUMN|Pelo menos uma coluna Passagem não é mapeada para uma coluna de saída.|  
|0xC020834E|-1071611058|DTS_E_TERMLOOKUP_INCORRECTEXACTNUMBEROFTEXTCOLUMNS|Deve haver exatamente uma coluna de entrada mapeada para uma coluna de referência.|  
|0xC020834F|-1071611057|DTS_E_TERMLOOKUP_TEXTINPUTCOLUMNHAVEINCORRECTDATATYPE|A coluna de entrada mapeada para uma coluna de referência só pode ter tipo de dados DT_NTXT ou DT_WSTR.|  
|0xC0208354|-1071611052|DTS_E_TXFUZZYLOOKUP_INVALID_MATCH_INDEX_NAME|O nome "%1" da tabela de referência não é um identificador SQL válido. Esse erro ocorre quando o nome da tabela não pode ser analisado a partir da cadeia de caracteres de entrada. Pode haver espaços sem aspas no nome. Verifique se as aspas estão corretas no nome.|  
|0xC0208355|-1071611051|DTS_E_TERMEXTRACTION_TERMFILTERSTARTITERATIONERROR|Ocorreu um erro quando o Filtro de Termo estava começando sua iteração.|  
|0xC0208356|-1071611050|DTS_E_TERMEXTRACTION_EMPTYTERMRESULTERROR|Ocorreu um erro ao recuperar o buffer usado para os termos armazenados em cache. O código de erro retornado foi 0x%1!8.8X!.|  
|0xC0208357|-1071611049|DTS_E_TERMEXTRACTION_STDLENGTHERROR|Ocorreu um std::length_error dos contêineres STL.|  
|0xC0208358|-1071611048|DTS_E_TERMLOOKUP_SAVEWORDWITHPUNCTERROR|Ocorreu um erro ao salvar as palavras com caracteres de pontuação. O código de erro retornado foi 0x%1!8.8X!.|  
|0xC0208359|-1071611047|DTS_E_TERMLOOKUP_ADDREFERENCETERM|Erro ao processar o termo de referência %1!ld!th. O código de erro retornado foi 0x%2!8.8X!. Remova o termo de referência de sua tabela de referência como solução.|  
|0xC020835A|-1071611046|DTS_E_TERMLOOKUP_SORREFERENCETERM|Ocorreu um erro durante a classificação dos termos de referência. O código de erro retornado foi 0x%1!8.8X!.|  
|0xC020835B|-1071611045|DTS_E_TERMLOOKUP_COUNTTERM|Ocorreu um erro durante a contagem dos candidatos a termo. O código de erro retornado foi 0x%1!8.8X!.|  
|0xC020835C|-1071611044|DTS_E_FUZZYLOOKUP_REFERENCECACHEFULL|A Pesquisa Difusa não conseguiu carregar toda a tabela de referência na memória principal, como deve ocorrer quando a propriedade Exhaustive está habilitada.  Houve um erro de memória insuficiente do sistema ou um limite foi especificado para MaxMemoryUsage que não foi suficiente para o carregamento da tabela de referência.  Defina MaxMemoryUsage como 0 ou aumente significativamente.  Como alternativa, desabilite Exhaustive.|  
|0xC020835D|-1071611043|DTS_E_TERMLOOKUP_INITIALIZE|Erro durante a inicialização do mecanismo de Pesquisa de Termo. O código de erro retornado foi 0x%1!8.8X!.|  
|0xC020835E|-1071611042|DTS_E_TERMLOOKUP_PROCESSSENTENCE|Ocorreu um erro durante o processamento das sentenças. O código de erro retornado foi 0x%1!8.8X!.|  
|0xC020835F|-1071611041|DTS_E_TEXTMININGBASE_APPENDTOTEMPBUFFER|Ocorreu um erro durante a adição de cadeias de caracteres a um buffer interno. O código de erro retornado foi 0x%1!8.8X!.|  
|0xC0208360|-1071611040|DTS_E_TERMEXTRACTION_SAVEPOSTAG|Ocorreu um erro ao salvar as marcas da parte de fala de um buffer interno. O código de erro retornado foi 0x%1!8.8X!.|  
|0xC0208361|-1071611039|DTS_E_TERMEXTRACTION_COUNTTERM|Ocorreu um erro durante a contagem dos candidatos a termo. O código de erro retornado foi 0x%1!8.8X!.|  
|0xC0208362|-1071611038|DTS_E_TERMEXTRACTION_INITPOSPROCESSOR|Ocorreu um erro durante a inicialização do processador da parte de fala. O código de erro retornado foi 0x%1!8.8X!.|  
|0xC0208363|-1071611037|DTS_E_TERMEXTRACTION_INITFSA|Ocorreu um erro ao carregar automações de estado finito. O código de erro retornado foi 0x%1!8.8X!.|  
|0xC0208364|-1071611036|DTS_E_TERMEXTRACTION_INITIALIZE|Erro durante a inicialização do mecanismo de Extração de Termo. O código de erro retornado foi 0x%1!8.8X!.|  
|0xC0208365|-1071611035|DTS_E_TERMEXTRACTION_PROCESSSENTENCE|Ocorreu um erro durante o processamento dentro de uma sentença. O código de erro retornado foi 0x%1!8.8X!.|  
|0xC0208366|-1071611034|DTS_E_TERMEXTRACTION_INITPOSTAGVECTOR|Ocorreu um erro durante a inicialização do processador da parte de fala. O código de erro retornado foi 0x%1!8.8X!.|  
|0xC0208367|-1071611033|DTS_E_TERMEXTRACTION_SAVEPTRSTRING|Ocorreu um erro durante a adição de cadeias de caracteres a um buffer interno. O código de erro retornado foi 0x%1!8.8X!.|  
|0xC0208368|-1071611032|DTS_E_TERMEXTRACTION_ADDWORDTODECODER|Ocorreu um erro durante a adição de palavras a um decodificador de estatística. O código de erro retornado foi 0x%1!8.8X!.|  
|0xC0208369|-1071611031|DTS_E_TERMEXTRACTION_DECODE|Erro durante a decodificação de uma sentença. O código de erro retornado foi 0x%1!8.8X!.|  
|0xC020836A|-1071611030|DTS_E_TERMEXTRACTION_SETEXCLUDEDTERM|Ocorreu um erro durante a configuração de termos de exclusão. O código de erro retornado foi 0x%1!8.8X!.|  
|0xC020836B|-1071611029|DTS_E_TERMEXTRACTION_PROCESSDOCUMENT|Ocorreu um erro durante o processamento de um documento na entrada. O código de erro retornado foi 0x%1!8.8X!.|  
|0xC020836C|-1071611028|DTS_E_TEXTMININGBASE_TESTPERIOD|Ocorreu um erro ao testar se um ponto fazia parte de um acrônimo. O código de erro retornado foi 0x%1!8.8X!.|  
|0xC020836D|-1071611027|DTS_E_TERMLOOKUP_ENGINEADDREFERENCETERM|Ocorreu um erro durante a definição dos termos de referência. O código de erro retornado foi 0x%1!8.8X!.|  
|0xC020836E|-1071611026|DTS_E_TERMLOOKUP_PROCESSDOCUMENT|Ocorreu um erro durante o processamento de um documento na entrada. O código de erro retornado foi 0x%1!8.8X!.|  
|0xC020836F|-1071611025|DTS_E_INVALIDBULKINSERTPROPERTYVALUE|O valor da propriedade %1 é %2!d!, o que não é permitido.  O valor deve ser maior ou igual a %3!d!.|  
|0xC0208370|-1071611024|DTS_E_INVALIDBULKINSERTFIRSTROWLASTROWVALUES|O valor para a propriedade %1 é %2!d!, que deve ser menor que ou igual ao valor de __ para a propriedade %3!d! para propriedade %4.|  
|0xC0208371|-1071611023|DTS_E_FUZZYLOOKUPUNABLETODELETEEXISTINGMATCHINDEX|Foi encontrado um erro ao tentar excluir o índice de correspondência difusa existente de nome "%1". Talvez essa tabela não foi criada pela Pesquisa Difusa (ou por essa versão de Pesquisa Difusa), foi danificada ou existe outro problema. Tente excluir manualmente a tabela de nome "%2" ou especifique um nome diferente para a propriedade MatchIndexName.|  
|0xC0208372|-1071611022|DTS_E_TERMEXTRACTION_INCORRECTSCORETYPE|O Tipo de Pontuação da transformação só pode ser Frequência ou TFIDF.|  
|0xC0208373|-1071611021|DTS_E_FUZZYLOOKUPREFTABLETOOBIG|A tabela de referência especificada tem muitas linhas. A Pesquisa Difusa trabalha somente com tabelas de referência com menos de 1 bilhão de linhas. Experimente usar uma exibição menor da sua tabela de referência.|  
|0xC0208374|-1071611020|DTS_E_FUZZYLOOKUPUNABLETODETERMINEREFERENCETABLESIZE|Não é possível determinar o tamanho da tabela de referência '%1'.  Talvez esse objeto seja uma exibição e não uma tabela.  A pesquisa difusa não dá suporte a exibições quando CopyReferentaceTable=false.  Verifique se a tabela realmente existe e se CopyReferenceTable=true.|  
|0xC0208377|-1071611017|DTS_E_XMLSRCOUTPUTCOLUMNDATATYPENOTSUPPORTED|Não existe suporte para o tipo de dados "%1" da Tarefa de Fluxo de Dados do SSIS no %2 para o %3.|  
|0xC0208378|-1071611016|DTS_E_XMLSRCCANNOTFINDCOLUMNTOSETDATATYPE|Não é possível definir as propriedades de tipo de dados para a coluna de saída com ID %1!d! na saída com ID %2!d!. A saída ou a coluna não foi encontrada.|  
|0xC0208379|-1071611015|DTS_E_CUSTOMPROPERTYISREADONLY|O valor da propriedade personalizada "%1" no %2 não pode ser alterado.|  
|0xC020837A|-1071611014|DTS_E_OUTPUTCOLUMNHASNOERRORCOLUMN|O %1 na saída de erro não tem nenhuma coluna de saída correspondente na saída de não erro.|  
|0xC020837B|-1071611013|DTS_E_ERRORCOLUMNHASNOOUTPUTCOLUMN|O %1 na saída de erro não tem nenhuma coluna de saída correspondente na saída de não erro.|  
|0xC020837C|-1071611012|DTS_E_ERRORCOLUMNHASINCORRECTPROPERTIES|O %1 na saída de erro tem propriedades que não correspondem às propriedades de sua coluna de fonte de dados correspondente.|  
|0xC020837D|-1071611011|DTS_E_ADOSRCOUTPUTCOLUMNDATATYPECANNOTBECHANGED|O tipo de dados de colunas de saída no %1 não pode ser alterado, com exceção das colunas DT_WSTR e DT_NTEXT.|  
|0xC020837F|-1071611009|DTS_E_ADOSRCDATATYPEMISMATCH|O tipo de dados de "%1" não corresponde ao tipo de dados "%2" da coluna de origem "%3".|  
|0xC0208380|-1071611008|DTS_E_ADOSRCCOLUMNNOTINSCHEMAROWSET|O %1 não tem uma coluna de origem correspondente no esquema.|  
|0xC0208381|-1071611007|DTS_E_TERMLOOKUP_INVALIDREFERENCETERMTABLEORCOLUMN|A tabela/exibição ou coluna de referência usada para os termos de referência é inválida.|  
|0xC0208382|-1071611006|DTS_E_TERMLOOKUP_REFERENCETERMTABLEANDCOLUMNNOTSET|A tabela/exibição ou coluna de referência usada para os termos de referência não foi definida.|  
|0xC0208383|-1071611005|DTS_E_COLUMNMAPPEDTOALREADYMAPPEDEXTERNALMETADATACOLUMN|%1 está mapeado para a coluna de metadados externos com a identificação %2!ld!, que já foi mapeada para outra coluna.|  
|0xC0208384|-1071611004|DTS_E_TXFUZZYLOOKUP_TOOMANYPREFIXES|O nome de objeto do SQL '%1' especificado para a propriedade '%2' contém mais que o número máximo de prefixos.  O máximo é 2.|  
|0xC0208385|-1071611003|DTS_E_MGDSRCSTATIC_OVERFLOW|O valor era muito grande para a coluna.|  
|0xC0208386|-1071611002|DTS_E_DATAREADERDESTREADERISCLOSED|O IDataReader do SSIS está fechado.|  
|0xC0208387|-1071611001|DTS_E_DATAREADERDESTREADERISATEND|O IDataReader do SSIS ultrapassou o final do conjunto de resultados.|  
|0xC0208388|-1071611000|DTS_E_DATAREADERDESTINVALIDCOLUMNORDINAL|A posição ordinal da coluna não é válida.|  
|0xC0208389|-1071610999|DTS_E_DATAREADERDESTCANNOTCONVERT|Não é possível converter o %1 de tipo de dados "%2" em tipo de dados "%3".|  
|0xC020838A|-1071610998|DTS_E_DATAREADERDESTINVALIDCODEPAGE|A página de código de %1, %2!d!, não tem suporte.|  
|0xC020838B|-1071610997|DTS_E_XMLSRCEXTERNALMETADATACOLUMNNOTINSCHEMA|O %1 não tem nenhum mapeamento para o esquema XML.|  
|0xC020838D|-1071610995|DTS_E_TXTERMLOOKUP_MISMATCHED_COLUMN_METADATA|As colunas com identificações de linhagem %1!d! e %2!d! possuem metadados que não coincidem. A coluna de entrada mapeada para uma coluna de saída não tem os mesmos metadados (tipo de dados, precisão, escala, comprimento ou página de código).|  
|0xC020838E|-1071610994|DTS_E_DATAREADERDESTREADERTIMEOUT|O IDataReader do SSIS está fechado. O tempo limite de leitura expirou.|  
|0xC020838F|-1071610993|DTS_E_ADOSRCINVALIDSQLCOMMAND|Erro ao executar o comando SQL fornecido: "%1". %2|  
|0xC0208390|-1071610992|DTS_E_JOINTYPEDOESNTMATCHETI|A propriedade JoinType especificada da coluna de entrada '%1' difere da propriedade JoinType especificada para a coluna de tabela de referência correspondente quando o Índice de Correspondência foi criado inicialmente.  Recrie o Índice de Correspondência com o JoinType fornecido ou altere o JoinType para corresponder ao tipo usado quando o Índice de Correspondência foi criado.|  
|0xC0208392|-1071610990|DTS_E_SQLCEDESTDATATYPENOTSUPPORTED|Não existe suporte para o tipo de dados "%1" encontrado na coluna "%2" para o %3.|  
|0xC0208393|-1071610989|DTS_E_DATAREADERDESTDATATYPENOTSUPPORTED|Não existe suporte para o tipo de dados "%1" encontrado na coluna %2 para o %3.|  
|0xC0208394|-1071610988|DTS_E_RECORDSETDESTDATATYPENOTSUPPORTED|O tipo de dados de %1 não tem suporte para o %2.|  
|0xC0208446|-1071610810|DTS_E_TXSCRIPTMIGRATIONCOULDNOTADDREFERENCE|Falha na adição da referência de projeto "%1" durante a migração de %2. Talvez seja necessário completar a migração manualmente.|  
|0xC0208447|-1071610809|DTS_E_TXSCRIPTMIGRATIONMULTIPLEENTRYPOINTSFOUND|Foram encontrados vários pontos de entrada com o nome "%1" durante a migração de %2. Talvez seja necessário completar a migração manualmente.|  
|0xC0208448|-1071610808|DTS_E_TXSCRIPTMIGRATIONNOENTRYPOINTFOUND|Não foi encontrado nenhum ponto de entrada durante a migração de %1. Talvez seja necessário completar a migração manualmente.|  
|0xC020844B|-1071610805|DTS_E_ADODESTINSERTIONFAILURE|Exceção durante a inserção de dados, a mensagem retornada do provedor foi: %1|  
|0xC020844C|-1071610804|DTS_E_ADODESTCONNECTIONTYPENOTSUPPORTED|Falha ao recuperar o nome invariável do provedor de %1, para o qual não há atualmente suporte no componente de destino do ADO NET|  
|0xC020844D|-1071610803|DTS_E_ADODESTARGUMENTEXCEPTION|Ocorreu uma exceção de argumento quando o provedor de dados tentou inserir dados no destino. Mensagem retornada: %1|  
|0xC020844E|-1071610802|DTS_E_ADODESTWRONGBATCHSIZE|A propriedade BatchSize deve ser um inteiro não negativo|  
|0xC020844F|-1071610801|DTS_E_ADODESTERRORUPDATEROW|Erro durante o envio desta linha para a fonte de dados de destino.|  
|0xC0208450|-1071610800|DTS_E_ADODESTEXECUTEREADEREXCEPTION|A execução do comando tSQL gerou uma exceção, a mensagem foi: %1|  
|0xC0208451|-1071610799|DTS_E_ADODESTDATATYPENOTSUPPORTED|Não existe suporte para o tipo de dados "%1" encontrado na coluna "%2" para o %3.|  
|0xC0208452|-1071610798|DTS_E_ADODESTFAILEDTOACQUIRECONNECTION|O destino ADO NET não adquiriu a conexão %1. A conexão pode ter sido corrompida.|  
|0xC0208453|-1071610797|DTS_E_ADODESTNOTMANAGEDCONNECTION|A conexão %1 especificada não é gerenciada, use conexão gerenciada para o destino ADO NET.|  
|0xC0208454|-1071610796|DTS_E_ADODESTNOERROROUTPUT|O componente de destino não tem uma saída de erro. Pode ter sido corrompida.|  
|0xC0208455|-1071610795|DTS_E_ADODESTNOLINEAGEID|O %1 de lineageID associado com a coluna externa %2 não existe no tempo de execução.|  
|0xC0208456|-1071610794|DTS_E_ADODESTEXTERNALCOLNOTEXIST|O %1 não existe no banco de dados. Ele pode ter sido removido ou renomeado.|  
|0xC0208457|-1071610793|DTS_E_ADODESTGETSCHEMATABLEFAILED|Falha ao obter as propriedades de colunas externas. O nome da tabela inserido pode não existir ou você não tem permissão SELECT no objeto de tabela e uma tentativa alternativa para obter as propriedades da coluna através da conexão falhou. As mensagens de erro detalhadas são: %1|  
|0xC0208458|-1071610792|DTS_E_ADODESTCOLUMNERRORDISPNOTSUPPORTED|A disposição de erro de coluna de entrada não tem suporte no componente de destino do ADO NET.|  
|0xC0208459|-1071610791|DTS_E_ADODESTCOLUMNTRUNDISPNOTSUPPORTED|A disposição de truncamento de coluna de entrada não tem suporte no componente de destino do ADO NET.|  
|0xC020845A|-1071610790|DTS_E_ADODESTINPUTTRUNDISPNOTSUPPORTED|A disposição de linha de truncamento de entrada não tem suporte no componente de destino do ADO NET.|  
|0xC020845B|-1071610789|DTS_E_ADODESTTABLENAMEERROR|O nome da Tabela ou Exibição não é esperado. \n\t Se estiver colocando aspas no nome da tabela, use o prefixo %1 e o sufixo %2 do seu provedor de dados selecionado para as aspas. \n\t Se você estiver usando um nome de várias partes, use no máximo três partes para o nome de tabela.|  
|0xC0209001|-1071607807|DTS_E_FAILEDTOFINDCOLUMNINBUFFER|Falha ao localizar a coluna "%1" com ID de linhagem %2!d! no buffer. O gerenciador de buffer retornou o código de erro 0x%3!8.8X!.|  
|0xC0209002|-1071607806|DTS_E_FAILEDTOGETCOLUMNINFOFROMBUFFER|Falha ao obter informações para a coluna "%1" (%2!d!) do buffer. O código de erro retornado foi 0x%3!8.8X!.|  
|0xC0209011|-1071607791|DTS_E_TXAGG_ARITHMETICOVERFLOW|Estouro aritmético encontrado ao agregar "%1".|  
|0xC0209012|-1071607790|DTS_E_FAILEDTOGETCOLINFO|Falha ao obter informações para a linha %1!ld!, coluna %2!ld! do buffer. O código de erro retornado foi 0x%3!8.8X!.|  
|0xC0209013|-1071607789|DTS_E_FAILEDTOSETCOLINFO|Falha ao definir informações para a linha %1!ld!, coluna %2!ld! no buffer. O código de erro retornado foi 0x%3!8.8X!.|  
|0xC0209015|-1071607787|DTS_E_REQUIREDBUFFERISNOTAVAILBLE|Um buffer necessário não está disponível.|  
|0xC0209016|-1071607786|DTS_E_FAILEDTOGETBUFFERBOUNDARYINFO|Falha na tentativa de obtenção de informações de limite de buffer com o código de erro 0x%1!8.8X!.|  
|0xC0209017|-1071607785|DTS_E_FAILEDTOSETBUFFERENDOFROWSET|Falha na definição do fim do conjunto de linhas para o buffer com o código de erro 0x%1!8.8X!.|  
|0xC0209018|-1071607784|DTS_E_FAILEDTOGETDATAFORERROROUTPUTBUFFER|Falha na obtenção dos dados para o buffer de saída de erro.|  
|0xC0209019|-1071607783|DTS_E_FAILEDTOREMOVEROWFROMBUFFER|Falha na remoção de uma linha do buffer com o código de erro 0x%1!8.8X!.|  
|0xC020901B|-1071607781|DTS_E_FAILEDTOSETBUFFERERRORINFO|Falha na tentativa de definição de informações de erro de buffer com o código de erro 0x%1!8.8X!.|  
|0xC020901C|-1071607780|DTS_E_COLUMNSTATUSERROR|Havia um erro com %1 em %2. O status da coluna retornado foi: "%3".|  
|0xC020901D|-1071607779|DTS_E_TXLOOKUP_METADATAXMLCACHEERR|Não é possível armazenar em cache os metadados de referência.|  
|0xC020901E|-1071607778|DTS_E_TXLOOKUP_ROWLOOKUPERROR|A linha não gerou correspondência durante a pesquisa.|  
|0xC020901F|-1071607777|DTS_E_INVALIDERRORDISPOSITION|O %1 tem uma disposição de linha de truncamento ou de erro inválido.|  
|0xC0209022|-1071607774|DTS_E_FAILEDTODIRECTERRORROW|Falha no direcionamento da linha para a saída de erro com o código de erro 0x%1!8.8X!.|  
|0xC0209023|-1071607773|DTS_E_FAILEDTOPREPARECOLUMNSTATUSESFORINSERT|Falha na preparação de status de coluna para inserção com o código de erro 0x%1!8.8X!.|  
|0xC0209024|-1071607772|DTS_E_FAILEDTOFINDCOLUMNBYLINEAGEID|Falha na tentativa de localizar %1 com ID de linhagem %2!d! no buffer da Tarefa do Fluxo de Dados com o código de erro 0x%3!8.8X!.|  
|0xC0209025|-1071607771|DTS_E_FAILEDTOFINDNONSPECIALERRORCOLUMN|Falha ao encontrar qualquer coluna de erro não especial em %1.|  
|0xC0209029|-1071607767|DTS_E_INDUCEDTRANSFORMFAILUREONERROR|Código de Erro SSIS DTS_E_INDUCEDTRANSFORMFAILUREONERROR.  Falha em "%1" devido ao código de erro 0x%2!8.8X! e a disposição de linha de erro em "%3" especifica falha em erro. Ocorreu um erro no objeto especificado do componente especificado.  Pode haver mensagens de erro geradas antes dessa, contendo mais informações sobre a falha.|  
|0xC020902A|-1071607766|DTS_E_INDUCEDTRANSFORMFAILUREONTRUNCATION|Falha no "%1" provocada por truncamento, e a disposição da linha de truncamento em "%2" e em "%3" especifica a falha no truncamento. Ocorreu um erro de truncamento no objeto especificado do componente especificado.|  
|0xC020902B|-1071607765|DTS_E_TXSPLITEXPRESSIONEVALUATEDTONULL|A expressão "%1" em "%2" foi avaliada como NULL, mas o "%3" requer resultados boolianos. Modifique a disposição da linha de erro na saída para tratar esse resultado como False (Ignore Failure) ou para redirecionar essa linha para a saída de erro (Redirect Row).  Os resultados da expressão devem ser boolianos para uma Divisão Condicional.  O resultado de uma expressão NULL é um erro.|  
|0xC020902C|-1071607764|DTS_E_TXSPLITSTATIC_EXPRESSIONEVALUATEDTONULL|A expressão foi avaliada como NULL, mas o resultado deve ser booliano. Modifique a disposição da linha de erro na saída para tratar esse resultado como False (Ignore Failure) ou para redirecionar essa linha para a saída de erro (Redirect Row). Os resultados da expressão devem ser boolianos para uma Divisão Condicional.  O resultado de uma expressão NULL é um erro.|  
|0xC020902D|-1071607763|DTS_E_UTF16BIGENDIANFORMATNOTSUPPORTED|Não existe suporte para o formato de arquivo de UTF-16 big endian.  Existe suporte somente para formato de arquivo UTF-16 little endian.|  
|0xC020902E|-1071607762|DTS_E_UTF8FORMATNOTSUPPORTEDASUNICODE|Não existe suporte para o formato de arquivo de UTF-8 como Unicode.|  
|0xC020902F|-1071607761|DTS_E_DTPXMLCANTREADIDATTR|Não é possível ler o atributo da ID.|  
|0xC020903E|-1071607746|DTS_E_TXLOOKUP_INDEXCOLUMNREUSED|A coluna de índice de cache %1 é referenciada por mais de uma coluna de entrada de pesquisa.|  
|0xC020903F|-1071607745|DTS_E_TXLOOKUP_INDEXCOLUMNSMISMATCH|Pesquisa não faz referência a todas as colunas de índice de gerenciador de conexões de cache. Número de colunas unidas na pesquisa: %1!d!. Número de colunas de índice: %2!d!.|  
|0xC0209069|-1071607703|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_CANTCONVERTVALUE|O valor dos dados não pode ser convertido por outros motivos que não a incompatibilidade de sinais ou o estouro de dados.|  
|0xC020906A|-1071607702|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_SCHEMAVIOLATION|O valor dos dados violou a restrição do esquema.|  
|0xC020906B|-1071607701|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_TRUNCATED|Os dados foram truncados.|  
|0xC020906C|-1071607700|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_SIGNMISMATCH|Falha na conversão porque o valor dos dados tinha sinais e o tipo usado pelo provedor não.|  
|0xC020906D|-1071607699|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_DATAOVERFLOW|Falha na conversão porque o valor dos dados estourou o tipo usado pelo provedor.|  
|0xC020906E|-1071607698|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_UNAVAILABLE|Nenhum status disponível.|  
|0xC020906F|-1071607697|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_PERMISSIONDENIED|O usuário não tinha as permissões corretas para gravar na coluna.|  
|0xC0209070|-1071607696|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_INTEGRITYVIOLATION|O valor dos dados violou as restrições de integridade para a coluna.|  
|0xC0209071|-1071607695|DTS_E_OLEDBSOURCEADAPTERSTATIC_UNAVAILABLE|Nenhum status disponível.|  
|0xC0209072|-1071607694|DTS_E_OLEDBSOURCEADAPTERSTATIC_CANTCONVERTVALUE|O valor dos dados não pode ser convertido por outros motivos que não a incompatibilidade de sinais ou o estouro de dados.|  
|0xC0209073|-1071607693|DTS_E_OLEDBSOURCEADAPTERSTATIC_TRUNCATED|Os dados foram truncados.|  
|0xC0209074|-1071607692|DTS_E_OLEDBSOURCEADAPTERSTATIC_SIGNMISMATCH|Falha na conversão porque o valor dos dados tinha sinais e o tipo usado pelo provedor não.|  
|0xC0209075|-1071607691|DTS_E_OLEDBSOURCEADAPTERSTATIC_DATAOVERFLOW|Falha na conversão porque o valor dos dados estourou o tipo usado pelo provedor.|  
|0xC0209076|-1071607690|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_SCHEMAVIOLATION|O valor dos dados violou a restrição do esquema.|  
|0xC0209077|-1071607689|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_CANTCONVERTVALUE|O valor dos dados não pode ser convertido por outros motivos que não a incompatibilidade de sinais ou o estouro de dados.|  
|0xC0209078|-1071607688|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_TRUNCATED|Os dados foram truncados.|  
|0xC0209079|-1071607687|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_SIGNMISMATCH|Falha na conversão porque o valor dos dados tinha sinais e o tipo usado pelo provedor não.|  
|0xC020907A|-1071607686|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_DATAOVERFLOW|Falha na conversão porque o valor dos dados estourou o tipo usado pelo provedor.|  
|0xC020907B|-1071607685|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_UNAVAILABLE|Nenhum status disponível.|  
|0xC020907C|-1071607684|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_PERMISSIONDENIED|O usuário não tinha as permissões corretas para gravar na coluna.|  
|0xC020907D|-1071607683|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_INTEGRITYVIOLATION|O valor dos dados viola as restrições de integridade.|  
|0xC020907F|-1071607681|DTS_E_TXDATACONVERTSTATIC_CANTCONVERTVALUE|O valor dos dados não pode ser convertido por outros motivos que não a incompatibilidade de sinais ou o estouro de dados.|  
|0xC0209080|-1071607680|DTS_E_TXDATACONVERTSTATIC_TRUNCATED|Os dados foram truncados.|  
|0xC0209081|-1071607679|DTS_E_TXDATACONVERTSTATIC_SIGNMISMATCH|Falha na conversão porque o valor dos dados tinha sinais e o tipo usado pelo provedor não.|  
|0xC0209082|-1071607678|DTS_E_TXDATACONVERTSTATIC_DATAOVERFLOW|Falha na conversão porque o valor dos dados estourou o tipo usado pela transformação de conversão de dados.|  
|0xC0209083|-1071607677|DTS_E_FLATFILESOURCEADAPTERSTATIC_UNAVAILABLE|Nenhum status disponível.|  
|0xC0209084|-1071607676|DTS_E_FLATFILESOURCEADAPTERSTATIC_CANTCONVERTVALUE|O valor dos dados não pode ser convertido por outros motivos que não a incompatibilidade de sinais ou o estouro de dados.|  
|0xC0209085|-1071607675|DTS_E_FLATFILESOURCEADAPTERSTATIC_TRUNCATED|Os dados foram truncados.|  
|0xC0209086|-1071607674|DTS_E_FLATFILESOURCEADAPTERSTATIC_SIGNMISMATCH|Falha na conversão porque o valor dos dados estava assinado e o tipo usado pelo adaptador de fonte de arquivo simples não.|  
|0xC0209087|-1071607673|DTS_E_FLATFILESOURCEADAPTERSTATIC_DATAOVERFLOW|Falha na conversão porque o valor dos dados estourou o tipo usado pelo adaptador de fonte de arquivo simples.|  
|0xC020908E|-1071607666|DTS_E_TXDATACONVERTSTATIC_UNAVAILABLE|Nenhum status disponível.|  
|0xC0209090|-1071607664|DTS_E_FILEOPENERR_FORREAD|Falha na abertura do arquivo "%1" para leitura com o código de erro 0x%2!8.8X!.|  
|0xC0209091|-1071607663|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD|Falha na abertura do arquivo para leitura.|  
|0xC0209092|-1071607662|DTS_E_FILEOPENERR_FORWRITE|Falha na abertura do arquivo "%1" para gravação com o código de erro 0x%2!8.8X!.|  
|0xC0209093|-1071607661|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE|Falha na abertura do arquivo para gravação.|  
|0xC0209094|-1071607660|DTS_E_TXFILEINSERTERSTATIC_INSERTERCANTREAD|Falha na leitura do arquivo.|  
|0xC0209095|-1071607659|DTS_E_TXFILEEXTRACTORSTATIC_EXTRACTORCANTWRITE|Falha na gravação no arquivo.|  
|0xC0209099|-1071607655|DTS_E_DTPXMLINVALIDPROPERTYARRAYTOOMANYVALUES|Foram encontrados muitos elementos da matriz ao analisar uma propriedade da matriz de tipo. O elementCount é menor que o número de elementos da matriz encontrados.|  
|0xC020909A|-1071607654|DTS_E_DTPXMLINVALIDPROPERTYARRAYNOTENOUGHVALUES|Foram encontrados muito poucos elementos da matriz ao analisar uma propriedade da matriz de tipo. O elementCount é maior que o número de elementos da matriz encontrados.|  
|0xC020909E|-1071607650|DTS_E_FILEOPENERR_FORWRITE_FILENOTFOUND|Falha ao abrir o arquivo "%1" para gravação. Não é possível encontrar o arquivo.|  
|0xC020909F|-1071607649|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_FILENOTFOUND|Falha ao abrir o arquivo para gravação. Não é possível encontrar o arquivo.|  
|0xC02090A0|-1071607648|DTS_E_FILEOPENERR_FORWRITE_PATHNOTFOUND|Falha ao abrir o arquivo "%1" para gravação. Não é possível encontrar o caminho.|  
|0xC02090A1|-1071607647|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_PATHNOTFOUND|Falha ao abrir o arquivo para gravação. Não é possível encontrar o caminho.|  
|0xC02090A2|-1071607646|DTS_E_FILEOPENERR_FORWRITE_TOOMANYOPENFILES|Falha ao abrir o arquivo "%1" para gravação. Há muitos arquivos abertos.|  
|0xC02090A3|-1071607645|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_TOOMANYOPENFILES|Falha ao abrir o arquivo para gravação. Há muitos arquivos abertos.|  
|0xC02090A4|-1071607644|DTS_E_FILEOPENERR_FORWRITE_ACCESSDENIED|Falha ao abrir o arquivo "%1" para gravação. Você não tem as permissões corretas.|  
|0xC02090A5|-1071607643|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_ACCESSDENIED|Falha ao abrir o arquivo para gravação. Você não tem as permissões corretas.|  
|0xC02090A6|-1071607642|DTS_E_FILEOPENERR_FORWRITE_FILEEXISTS|Falha ao abrir o arquivo "%1" para gravação. O arquivo existe e não pode ser substituído. Se a propriedade AllowAppend for FALSE e a propriedade ForceTruncate estiver definida como FALSE, a existência do arquivo provocará essa falha.|  
|0xC02090A7|-1071607641|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_FILEEXISTS|Falha ao abrir um arquivo para gravação. O arquivo já existe e não pode ser substituído. Se a propriedade AllowAppend e a propriedade ForceTruncate estiverem definidas como FALSE, a existência do arquivo provocará essa falha.|  
|0xC02090A8|-1071607640|DTS_E_INCORRECTCUSTOMPROPERTYVALUEFOROBJECT|O valor da propriedade personalizada "%1" em %2 está incorreto.|  
|0xC02090A9|-1071607639|DTS_E_COLUMNSHAVEINCOMPATIBLEMETADATA|As colunas "%1" e "%2" têm metadados incompatíveis.|  
|0xC02090AD|-1071607635|DTS_E_FILEWRITEERR_DISKFULL|Falha na abertura do arquivo "%1" para gravação porque o disco está cheio. Não há espaço de disco suficiente para salvar esse arquivo.|  
|0xC02090AE|-1071607634|DTS_E_TXFILEEXTRACTORSTATIC_FILEWRITEERR_DISKFULL|Falha na tentativa de abrir o arquivo para gravação porque o disco está cheio.|  
|0xC02090B9|-1071607623|DTS_E_TXAGG_SORTKEYGENFAILED|Falha na geração de uma chave de classificação com o erro 0x%1!8.8X!. Os ComparisonFlags estão habilitados, e houve falha na geração de uma chave de classificação com LCMapString.|  
|0xC02090BA|-1071607622|DTS_E_TXCHARMAPLCMAPFAILED|A transformação não pôde mapear a cadeia de caracteres e retornou o erro 0x%1!8.8X!. Falha no LCMapString.|  
|0xC02090BB|-1071607621|DTS_E_FILEOPENERR_FORREAD_FILENOTFOUND|Falha ao abrir o arquivo "%1" para leitura. O arquivo não foi encontrado.|  
|0xC02090BC|-1071607620|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_FILENOTFOUND|Falha ao abrir um arquivo para leitura. O arquivo não foi encontrado.|  
|0xC02090BD|-1071607619|DTS_E_FILEOPENERR_FORREAD_PATHNOTFOUND|Falha ao abrir o arquivo "%1" para leitura. Não é possível encontrar o caminho.|  
|0xC02090BE|-1071607618|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_PATHNOTFOUND|Falha ao abrir um arquivo para leitura. O caminho não foi encontrado.|  
|0xC02090BF|-1071607617|DTS_E_FILEOPENERR_FORREAD_TOOMANYOPENFILES|Falha ao abrir o arquivo "%1" para leitura. Há muitos arquivos abertos.|  
|0xC02090C0|-1071607616|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_TOOMANYOPENFILES|Falha ao abrir o arquivo para leitura. Há muitos arquivos abertos.|  
|0xC02090C1|-1071607615|DTS_E_FILEOPENERR_FORREAD_ACCESSDENIED|Falha na tentativa de abrir o arquivo "%1" para leitura. Acesso negado.|  
|0xC02090C2|-1071607614|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_ACCESSDENIED|Falha ao abrir o arquivo para leitura. Você não tem as permissões corretas.|  
|0xC02090C3|-1071607613|DTS_E_INSERTERINVALIDBOM|O valor de BOM (marca de ordem de byte) do arquivo "%1" é 0x%2!4.4X!, mas o valor esperado é 0x%3!4.4X!. A propriedade ExpectBOM foi definida para esse arquivo, mas o valor de BOM está faltando no arquivo ou não é válido.|  
|0xC02090C4|-1071607612|DTS_E_TXFILEINSERTERSTATIC_INSERTERINVALIDBOM|O valor de BOM (marca de ordem de byte) para o arquivo não é válido. A propriedade ExpectBOM foi definida para esse arquivo, mas o valor de BOM está faltando no arquivo ou não é válido.|  
|0xC02090C5|-1071607611|DTS_E_NOCOMPONENTATTACHED|O %1 não está anexado a um componente.  É necessário ter um componente anexado.|  
|0xC02090C9|-1071607607|DTS_E_TXLOOKUP_INVALIDMAXMEMORYPROP|O valor da propriedade personalizada %1 está incorreto.  Deveria ser um número entre %2!d! e %3!I64d!.|  
|0xC02090CA|-1071607606|DTS_E_TXAGG_COMPFLAGS_BADAGGREGATIONTYPE|A propriedade personalizada "%1" não pode ser especificada para o tipo de agregação selecionado para essa coluna. A propriedade personalizada dos sinalizadores de comparação só pode especificada para tipos de agregação agrupar por e distinção de contagem.|  
|0xC02090CB|-1071607605|DTS_E_TXAGG_COMPFLAGS_BADDATATYPE|A propriedade personalizada dos sinalizadores de comparação "%1" só pode ser especificada para colunas com tipos de dados DT_STR ou DT_WSTR.|  
|0xC02090CD|-1071607603|DTS_E_TXAGG_AGGREGATION_FAILURE|Falha na agregação em %1 com o código de erro 0x%2!8.8X!.|  
|0xC02090CF|-1071607601|DTS_E_MAPPINGSETUPERROR|Houve um erro durante a configuração do mapeamento. %1|  
|0xC02090D0|-1071607600|DTS_E_XMLSRCUNABLETOREADXMLDATA|O %1 não pôde ler os dados XML.|  
|0xC02090D1|-1071607599|DTS_E_XMLSRCUNABLETOGETXMLDATAVARIABLE|O %1 não pôde obter a variável especificada pela propriedade "%2".|  
|0xC02090D2|-1071607598|DTS_E_NODATATABLEMATCHROWID|O %1 contém um RowsetID com um valor de %2 que não faz referência a uma tabela de dados no esquema.|  
|0xC02090D6|-1071607594|DTS_E_TXAGG_BADKEYSVALUE|A propriedade %1 deve ficar vazia ou ter um número entre %2!u! e %3!u!. A propriedade Keys ou CountDistinctKeys tem um valor inválido. A propriedade deveria ser um número entre 0 e ULONG_MAX, inclusive, ou não deveria ser definida.|  
|0xC02090D7|-1071607593|DTS_E_TXAGG_TOOMANYKEYS|O componente de agregação encontrou muitas combinações de chave distintas. Ele não pode acomodar mais que %1!u! valores de chave distintos. Existem mais valores de chave distintos que ULONG_MAX no workspace principal.|  
|0xC02090D8|-1071607592|DTS_E_TXAGG_TOOMANYCOUNTDISTINCTVALUES|O componente de agregação encontrou muitos valores distintos ao calcular a agregação de distinção de contagem. Ele não pode acomodar mais que %1!u! valores distintos. Existiam mais valores distintos que ULONG_MAX durante o cálculo da agregação de distinção de contagem.|  
|0xC02090D9|-1071607591|DTS_E_FAILEDTOWRITETOTHEFILENAMECOLUMN|Falha na tentativa de gravar na coluna de nome do arquivo com o código de erro 0x%1!8.8X!.|  
|0xC02090DC|-1071607588|DTS_E_FAILEDTOFINDERRORCOLUMN|Ocorreu um erro, mas não é possível determinar a coluna que causou o erro.|  
|0xC02090E3|-1071607581|DTS_E_TXLOOKUP_FAILEDUPGRADE_BAD_VERSION|Não é possível atualizar os metadados de pesquisa da versão %1!d! a %2!d!. A transformação Pesquisa não atualizou os metadados do número de versão existente em uma chamada para PerformUpgrade ().|  
|0xC02090E5|-1071607579|DTS_E_TERMEXTRACTIONORLOOKUP_NTEXTSPLITED|Falha na localização do limite final de uma sentença.|  
|0xC02090E6|-1071607578|DTS_E_TERMEXTRACTION_EXCEED_MAXWORDNUM|A transformação Extração de Termo não pode processar o texto de entrada porque ele tem uma sentença muito longa. A sentença está segmentada em diversas sentenças.|  
|0xC02090E7|-1071607577|DTS_E_XMLSRCFAILEDTOCREATEREADER|O %1 não pôde ler os dados XML. %2|  
|0xC02090F0|-1071607568|DTS_E_TXLOOKUP_REINITMETADATAFAILED|Falha na chamada para o método de transformação Pesquisa, ReinitializeMetadata.|  
|0xC02090F1|-1071607567|DTS_E_TXLOOKUP_NOJOINS|A transformação de pesquisa deve conter pelo menos uma coluna de entrada unida a uma coluna de referência, mas nenhuma foi especificada. Especifique pelo menos uma coluna de junção.|  
|0xC02090F2|-1071607566|DTS_E_MANAGEDERR_BADFORMATSPECIFICATION|A cadeia de caracteres da mensagem sendo gerada pela infraestrutura de erro gerenciada contém uma especificação inválida de formato. Esse é um erro interno.|  
|0xC02090F3|-1071607565|DTS_E_MANAGEDERR_UNSUPPORTEDTYPE|Durante a formatação da cadeia de caracteres da mensagem, usando a infraestrutura de erro gerenciada, havia um tipo de variante sem-suporte para formatação. Esse é um erro interno.|  
|0xC02090F5|-1071607563|DTS_E_DATAREADERSRCUNABLETOPROCESSDATA|O %1 não pôde processar os dados. %2|  
|0xC02090F6|-1071607562|DTS_E_XMLSRCEMPTYPROPERTY|A propriedade "%1" no %2 estava vazia.|  
|0xC02090F7|-1071607561|DTS_E_XMLSRCINVALIDOUTPUTNAME|Falha na tentativa de criar uma saída com o nome "%1" para a tabela XML com o caminho "%2" porque o nome é inválido.|  
|0xC02090F8|-1071607560|DTS_E_MGDSRC_OVERFLOW|O valor era muito grande para o %1.|  
|0xC02090F9|-1071607559|DTS_E_DATAREADERDESTUNABLETOPROCESSDATA|O %1 não pôde processar os dados.|  
|0xC02090FA|-1071607558|DTS_E_XMLSRC_INDUCEDTRANSFORMFAILUREONTRUNCATION|Falha no "%1" provocada por truncamento, e a disposição da linha de truncamento em "%2" em "%3" especifica a falha no truncamento. Ocorreu um erro de truncamento no objeto especificado do componente especificado.|  
|0xC02090FB|-1071607557|DTS_E_XMLSRC_INDUCEDTRANSFORMFAILUREONERROR|Falha em "%1" devido ao código de erro 0x%2!8.8X! e a disposição de linha de erro em "%3" em "%4" especifica falha em erro. Ocorreu um erro no objeto especificado do componente especificado.|  
|0xC0209291|-1071607151|DTS_E_SQLCEDESTSTATIC_FAILEDTOSETVALUES|O destino SQLCE não definiu os valores de coluna para a linha.|  
|0xC0209292|-1071607150|DTS_E_SQLCEDESTSTATIC_FAILEDTOINSERT|O destino SQLCE não inseriu a linha.|  
|0xC0209293|-1071607149|DTS_E_TXFUZZYLOOKUP_OLEDBERR_LOADCOLUMNMETADATA|Foi encontrado um erro OLE DB ao carregar os metadados da coluna.|  
|0xC0209294|-1071607148|DTS_E_TXFUZZYLOOKUP_TOOFEWREFERENCECOLUMNS|Os metadados de referência de pesquisa contêm poucas colunas.|  
|0xC0209295|-1071607147|DTS_E_TXSCD_OLEDBERR_LOADCOLUMNMETADATA|Foi encontrado um erro OLE DB ao carregar os metadados da coluna.|  
|0xC0209296|-1071607146|DTS_E_TXSCD_TOOFEWREFERENCECOLUMNS|Os metadados de referência de pesquisa contêm poucas colunas.|  
|0xC0209297|-1071607145|DTS_E_TXSCD_MALLOCERR_REFERENCECOLUMNINFO|Não é possível alocar memória.|  
|0xC0209298|-1071607144|DTS_E_TXSCD_MALLOCERR_BUFFCOL|Não é possível alocar memória.|  
|0xC0209299|-1071607143|DTS_E_TXSCD_MAINWORKSPACE_CREATEERR|Não é possível criar um buffer de workspace.|  
|0xC020929A|-1071607142|DTS_E_DTPXMLDOMCREATEERROR|Não é possível criar uma instância de documento XML DOM, verifique se os binários MSXML estão instalados e registrados corretamente.|  
|0xC020929B|-1071607141|DTS_E_DTPXMLDOMLOADERROR|Não é possível carregar os dados XML em um DOM local para processamento.|  
|0xC020929C|-1071607140|DTS_E_RSTDESTBADVARIABLETYPE|O tipo da variável de tempo de execução "%1" está incorreto. O tipo da variável de tempo de execução deve ser Object.|  
|0xC020929E|-1071607138|DTS_E_XMLDATAREADERMULTIPLEINLINEXMLSCHEMASNOTSUPPORTED|O Adaptador de Origem XML não processou os dados XML. Não existe suporte para vários esquemas embutidos.|  
|0xC020929F|-1071607137|DTS_E_XMLDATAREADERANYTYPENOTSUPPORTED|O Adaptador de Origem XML não processou os dados XML. O conteúdo de um elemento não pode ser declarado como anyType.|  
|0xC02092A0|-1071607136|DTS_E_XMLDATAREADERGROUPREFNOTSUPPORTED|O Adaptador de Origem XML não processou os dados XML. O conteúdo de um elemento não pode conter uma referência (ref) a um grupo.|  
|0xC02092A1|-1071607135|DTS_E_XMLDATAREADERMIXEDCONTENTFORCOMPLEXTYPESNOTSUPPORTED|O Adaptador de Origem XML não fornece suporte a modelos de conteúdo misto em Tipos Complexos.|  
|0xC02092A2|-1071607134|DTS_E_XMLDATAREADERINLINESCHEMAFOUNDINSOURCEXML|O Adaptador de Origem XML não processou os dados XML. Um esquema embutido deve ser o primeiro nó filho na origem Xml.|  
|0xC02092A3|-1071607133|DTS_E_XMLDATAREADERNOINLINESCHEMAFOUND|O Adaptador de Origem XML não processou os dados XML. Não foi encontrado nenhum esquema embutido na origem XML, mas a propriedade "UseInlineSchema" estava definida como verdadeira.|  
|0xC02092A4|-1071607132|DTS_E_CONNECTIONMANAGERTRANSACTEDANDRETAINEDINBULKINSERT|O componente não pode usar um gerenciador de conexões que retenha sua conexão em uma transação com inserção em massa ou de carga rápida.|  
|0xC02092A5|-1071607131|DTS_E_OUTPUTREDIRECTINTRANSACTIONNOTALLOWED|O %1 não pode ser definido para redirecionar em caso de erro, usando uma conexão em uma transação.|  
|0xC02092A6|-1071607130|DTS_E_FOUNDORPHANEDEXTERNALMETADATACOLUMN|O %1 não tem uma entrada nem uma coluna de saída correspondente.|  
|0xC02092A9|-1071607127|DTS_E_RAWDESTNOINPUTCOLUMNS|Não existe nenhuma coluna selecionada para ser gravada no arquivo.|  
|0xC02092AA|-1071607126|DTS_E_RAWDESTBLOBDATATYPE|O %1 contém um tipo de dados inválido. As colunas com tipos de dados DT_IMAGE, DT_TEXT e DT_NTEXT não podem ser gravados em arquivos brutos.|  
|0xC02092AB|-1071607125|DTS_E_RAWDESTWRONGEXTERNALMETADATAUSAGE|Esse componente usou a coleção de metadados externos de forma incorreta. O componente deveria usar metadados externos ao anexar ou truncar um arquivo existente. Do contrário, não são necessários metadados externos.|  
|0xC02092AC|-1071607124|DTS_E_RAWDESTMAPPEDINPUTCOLUMN|%1 está mapeado para uma coluna de metadados externos com a identificação %2!d!. As colunas de entrada não devem ser mapeadas para colunas de metadados externos quando o valor Opção de Gravação selecionado for Criar Sempre.|  
|0xC02092AD|-1071607123|DTS_E_RAWFILECANTOPENFORMETADATA|O arquivo não pode ser aberto para leitura de metadados. Se o arquivo não existir e o componente já definiu os metadados externos, defina a propriedade "ValidateExternalMetadata" como "false", e o arquivo será criado no tempo de execução.|  
|0xC02092AE|-1071607122|DTS_E_FAILEDTOACCESSLOBCOLUMN|Falha ao acessar dados de LOB do buffer de fluxo de dados para a coluna de origem de dados "%1" com o código de erro 0x%2!8.8X!.|  
|0xC02092AF|-1071607121|DTS_E_XMLSRCUNABLETOPROCESSXMLDATA|O %1 não pôde processar os dados XML. %2|  
|0xC02092B0|-1071607120|DTS_E_XMLSRCSTATIC_UNABLETOPROCESSXMLDATA|O Adaptador de Origem XML não processou os dados XML.|  
|0xC02092B1|-1071607119|DTS_E_RAWINVALIDACCESSMODE|O valor é %1!d! não é reconhecido como modo de acesso válido.|  
|0xC02092B2|-1071607118|DTS_E_INCOMPLETEDATASOURCECOLUMNFOUND|Não estão disponíveis informações completas dos metadados para a coluna de fonte de dados "%1".  Certifique-se de que a coluna esteja corretamente definida na fonte dos dados.|  
|0xC02092B3|-1071607117|DTS_E_TXAUDIT_ONLYSTRINGLENGTHCHANGEALLOWED|Somente os comprimentos das colunas Nome do Usuário, Nome do Pacote, Nome da Tarefa e Nome da Máquina podem ser alterados.  Todas as demais informações de tipo de dados da coluna de auditoria são somente leitura.|  
|0xC02092B4|-1071607116|DTS_E_ROWSETUNAVAILABLE|Um conjunto de linhas baseado no comando SQL não foi retornado pelo provedor OLE DB.|  
|0xC02092B5|-1071607115|DTS_E_COMMITFAILED|Falha em uma confirmação.|  
|0xC02092B6|-1071607114|DTS_E_USEBINARYFORMATREQUIRESANSIFILE|A propriedade personalizada "%1" em %2 só pode ser usada com arquivos ANSI.|  
|0xC02092B7|-1071607113|DTS_E_USEBINARYFORMATREQUIRESBYTES|A propriedade personalizada "%1" em %2 só pode ser usada com DT_BYTES.|  
|0xC0209302|-1071607038|DTS_E_OLEDB_NOPROVIDER_ERROR|Código de erro SSIS DTS_E_OLEDB_NOPROVIDER_ERROR.  O provedor OLE DB %2 solicitado não está registrado. Código de erro: 0x%1!8.8X!.|  
|0xC0209303|-1071607037|DTS_E_OLEDB_NOPROVIDER_64BIT_ERROR|Código de erro SSIS DTS_E_OLEDB_NOPROVIDER_64BIT_ERROR.  O provedor OLE DB solicitado %2 não está registrado--talvez nenhum provedor de 64 bits esteja disponível.  Código de erro: 0x%1!8.8X!.|  
|0xC0209306|-1071607034|DTS_E_MULTICACHECOLMAPPINGS|A coluna de cache, "%1", está mapeada para mais de uma coluna. Remova os mapeamentos de coluna duplicados.|  
|0xC0209307|-1071607033|DTS_E_COLNOTMAPPEDTOCACHECOL|%1 não é mapeada para uma coluna de cache válida.|  
|0xC0209308|-1071607032|DTS_E_CACHECOLDATATYPEINCOMPAT|Não é possível mapear a coluna de entrada, "%1", e a coluna de cache, "%2", porque os tipos de dados não coincidem.|  
|0xC0209309|-1071607031|DTS_E_INCORRECTINPUTCACHECOLCOUNT|O número de colunas de entrada não corresponde ao número de colunas de cache.|  
|0xC020930A|-1071607030|DTS_E_INVALIDCACHEFILENAME|O nome do arquivo de cache não foi fornecido ou não é válido. Forneça um nome de arquivo de cache válido.|  
|0xC020930B|-1071607029|DTS_E_CACHECOLINDEXPOSMISMATCH|A posição de índice da coluna, "%1", é diferente da posição de índice da coluna do gerenciador de conexões de Cache, "%2".|  
|0xC020930C|-1071607028|DTS_E_FAILEDTOLOADCACHE|Falha ao carregar o cache do arquivo, "%1".|  
|0xC020930D|-1071607027|DTS_E_TXLOOKUP_REFCOLUMNISNOTINDEX|A coluna de entrada de pesquisa %1 faz referência à coluna de cache sem-índice %2.|  
|0xC020930E|-1071607026|DTS_E_FAILEDTOGETCONNECTIONSTRING|Falha ao obter a cadeia de conexão.|  
|0xC020930F|-1071607025|DTS_E_CACHECOLDATATYPEPROPINCOMPAT|Não é possível mapear a coluna de entrada, "%1", e a coluna de cache, "%2", porque uma ou mais propriedades de tipo de dados não coincidem.|  
|0xC0209311|-1071607023|DTS_E_CACHECOLUMNOTFOUND|Coluna de cache "%1" não foi encontrada no cache.|  
|0xC0209312|-1071607022|DTS_E_CACHECOLUMNMAPPINGFAILED|Falha ao mapear %1 para uma coluna de cache. O hresult é 0x%2!8.8X!.|  
|0xC0209313|-1071607021|DTS_E_CACHELOADEDFROMFILE|O %1 não pode gravar no cache porque o cache foi carregado de um arquivo por %2.|  
|0xC0209314|-1071607020|DTS_E_CACHERELOADEDDIFFERENTFILES|O %1 não pode carregar o cache do arquivo "%2" porque o cache foi carregado do arquivo "%3".|  
|0xC0209316|-1071607018|DTS_E_OUTPUTNOTUSED|A saída com ID %1!d! do componente de agregação não é usada por nenhum componente. Remova ou associe-o com uma entrada de algum componente.|  
|0xC0209317|-1071607017|DTS_E_CACHEFILEWRITEFAILED|Falha em %1 ao gravar o cache no arquivo "%2". O hresult é 0x%3!8.8X!.|  
|0xC0209318|-1071607016|DTS_E_XMLDATATYPECHANGED|As informações de tipo de dados de esquema XML para "%1" no elemento "%2" foram alteradas.  Reinicialize os metadados para esse componente e revise os mapeamentos de coluna.|  
|0xC0209319|-1071607015|DTS_E_TXLOOKUP_UNUSEDINPUTCOLUMN|%1 não usado em junção ou cópia. Remova a coluna não usada da lista de colunas de entrada.|  
|0xC020931A|-1071607014|DTS_E_SORTSTACKOVERFLOW|Falha na classificação devido a um estouro de pilha ao classificar um buffer de entrada.  Reduza a propriedade DefaultBufferMaxRows na Tarefa de Fluxo de Dados.|  
|0xC020F42A|-1071582166|DTS_E_OLEDB_OLDPROVIDER_ERROR|Considere alterar o PROVIDER na cadeia de conexão para %1 ou acesse https://www.microsoft.com/downloads para localizar e instalar o suporte para %2.|  
|||DTS_E_INITTASKOBJECTFAILED|Falha ao inicializar o objeto de tarefa para a tarefa "%1!s!", tipo "%2!s!" devido ao erro 0x%3!8.8X! "%4!s!".|  
|||DTS_E_GETCATMANAGERFAILED|Falha ao criar o Gerenciador de Categorias de Componentes COM devido ao erro 0x%1!8.8X! "%2!s!".|  
|||DTS_E_COMPONENTINITFAILED|O componente %1!s! não inicializou devido ao erro 0x%2!8.8X! "%3!s!".|  
  
##  <a name="msgWarning"></a> Mensagens de aviso  
 Os nomes simbólicos das mensagens de aviso do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] começam com **DTS_W_** .  
  
|Código hexadecimal|Código decimal|Nome simbólico|Descrição|  
|----------------------|------------------|-------------------|-----------------|  
|0x80000036|-2147483594|DTS_W_COUNTDOWN|Restam %1!lu! dias de avaliação. Quando ela expirar, os pacotes não poderão ser executados.|  
|0x80010015|-2147418091|DTS_W_GENERICWARNING|Aviso(s) gerado(s). Deve haver mais avisos específicos precedentes a este que expliquem as especificidades do(s) aviso(s).|  
|0x80012010|-2147409904|DTS_W_FAILEDXMLDOCCREATION|Não é possível criar uma instância do objeto de documento XML. Verifique se o MSXML está instalado e registrado corretamente.|  
|0x80012011|-2147409903|DTS_W_FAILEDCONFIGLOAD|Não é possível carregar o arquivo de configuração XML. O arquivo de configuração XML pode estar danificado ou ser inválido.|  
|0x80012012|-2147409902|DTS_W_CONFIGFILENAMEINVALID|O nome do arquivo de configuração "%1" não é válido. Verifique o nome do arquivo de configuração.|  
|0x80012013|-2147409901|DTS_W_CONFIGFILEINVALID|O arquivo de configuração foi carregado, mas não é válido. O arquivo não está formatado corretamente, pode estar faltando um elemento, ou pode estar danificado.|  
|0x80012014|-2147409900|DTS_W_CONFIGFILENOTFOUND|Não é possível encontrar o arquivo de configuração "%1". Verifique o diretório e o nome do arquivo.|  
|0x80012015|-2147409899|DTS_W_CONFIGKEYNOTFOUND|Não foi encontrada a chave do Registro de configuração "%1". Uma entrada de configuração especifica uma chave do Registro que não está disponível. Verifique no registro se a chave realmente existe.|  
|0x80012016|-2147409898|DTS_W_CONFIGTYPEINVALID|O tipo de configuração em uma das entradas de configuração não era válido. Os tipos válidos estão listados na enumeração DTSConfigurationType.|  
|0x80012017|-2147409897|DTS_W_CANNOTFINDOBJECT|O caminho do pacote referiu-se a um objeto que não pode ser encontrado: "%1". Isso ocorre quando se tenta resolver um caminho de pacote para um objeto que não pode ser encontrado.|  
|0x80012018|-2147409896|DTS_W_CONFIGFORMATINVALID_PACKAGEDELIMITER|A entrada de configuração, "%1", tem um formato incorreto porque não começa com o delimitador de pacote. Insira "\package" antes do caminho do pacote.|  
|0x80012019|-2147409895|DTS_W_CONFIGFORMATINVALID|A entrada de configuração "%1" tinha um formato incorreto. Isso pode ocorrer por falta de delimitador ou erros de formatação, como um delimitador inválido de matriz.|  
|0x8001201A|-2147409894|DTS_W_NOPARENTVARIABLES|A configuração não ocorreu a partir de uma variável pai "%1" porque não existia nenhuma coleção de variáveis pai.|  
|0x8001201B|-2147409893|DTS_W_CONFIGFILEFAILEDIMPORT|Falha ao importar o arquivo de configuração: "%1".|  
|0x8001201C|-2147409892|DTS_W_PARENTVARIABLENOTFOUND|A configuração não ocorreu a partir de uma variável pai "%1" porque não existia nenhuma coleção de variáveis pai. Código de erro: 0x%2!8.8X!.|  
|0x8001201D|-2147409891|DTS_W_CONFIGFILEEMPTY|O arquivo de configuração estava vazio e não continha nenhuma entrada de configuração.|  
|0x80012023|-2147409885|DTS_W_INVALIDCONFIGURATIONTYPE|O tipo para a configuração "%1" não é válido. Isso pode ocorrer quando se tenta definir a propriedade de tipo de um objeto de configuração como um tipo inválido.|  
|0x80012025|-2147409883|DTS_W_REGISTRYCONFIGURATIONTYPENOTFOUND|O tipo de configuração para a configuração de registro não foi encontrado na chave "%1". Adicione um valor chamado ConfigType à chave do registro e atribua a ela um valor de cadeia de caracteres de "Variable", "Property", "ConnectionManager", "LoggingProvider" ou "ForEachEnumerator".|  
|0x80012026|-2147409882|DTS_W_REGISTRYCONFIGURATIONVALUENOTFOUND|O valor de configuração para a configuração de registro não foi encontrado na chave "%1". Adicione um valor chamado Value à chave do Registro do tipo DWORD ou String.|  
|0x80012028|-2147409880|DTS_W_PROCESSCONFIGURATIONFAILEDSET|Falha na configuração do processo ao definir o destino no caminho de pacote do "%1". Isso ocorre quando se tenta definir a propriedade de destino ou falhas de variável. Verifique a propriedade de destino ou a variável.|  
|0x80012032|-2147409870|DTS_W_CONFIGUREDVALUESECTIONEMPTY|Falha ao recuperar o valor do arquivo .ini. A seção ConfiguredValue está vazia ou não existe: "%1".|  
|0x80012033|-2147409869|DTS_W_CONFIGUREDTYPESECTIONEMPTY|Falha ao recuperar o valor do arquivo .ini. A seção ConfiguredType está vazia ou não existe: "%1".|  
|0x80012034|-2147409868|DTS_W_PACKAGEPATHSECTIONEMPTY|Falha ao recuperar o valor do arquivo .ini. A seção PackagePath está vazia ou não existe: "%1".|  
|0x80012035|-2147409867|DTS_W_CONFIGUREDVALUETYPE|Falha ao recuperar o valor do arquivo .ini. A seção ConfiguredValueType está vazia ou não existe: "%1".|  
|0x80012051|-2147409839|DTS_W_SQLSERVERFAILEDIMPORT|A configuração não foi importada com êxito do SQL Server: "%1".|  
|0x80012052|-2147409838|DTS_W_INICONFIGURATIONPROBLEM|O arquivo de configuração .ini não é válido porque está vazio ou faltam campos.|  
|0x80012054|-2147409836|DTS_W_NORECORDSFOUNDINTABLE|A tabela "%1" não tem nenhum registro para configuração. Isso ocorre quando se está configurando a partir de uma tabela do SQL Server que não contém registros para a configuração.|  
|0x80012055|-2147409835|DTS_W_DUPLICATECUSTOMEVENT|Erro ao usar o mesmo nome para eventos personalizados diferentes. O evento personalizado "%1" foi definido de forma diferente por filhos diferentes desse contêiner. Pode haver um erro ao executar o manipulador de eventos.|  
|0x80012057|-2147409833|DTS_W_CONFIGREADONLYVARIABLE|A configuração tentou alterar uma variável somente leitura. A variável está no caminho de pacote "%1".|  
|0x80012058|-2147409832|DTS_W_CONFIGPROCESSCONFIGURATIONFAILED|Falha ao chamar ProcessConfiguration no pacote. A configuração tentou alterar a propriedade no caminho de pacote "%1".|  
|0x80012059|-2147409831|DTS_W_ONEORMORECONFIGLOADFAILED|Falha ao carregar pelo menos uma das entradas de configuração para o pacote. Verifique as entradas de configurações para "%1" e os avisos anteriores para ver as descrições da configuração em que houve falha.|  
|0x8001205A|-2147409830|DTS_W_CONFIGNODEINVALID|A entrada de configuração "%1" no arquivo de configuração não era válida ou houve falha na configuração da variável.  O nome indica a entrada em que ocorreu a falha. Em alguns casos, o nome não estará disponível.|  
|0x80014058|-2147401640|DTS_W_FAILURENOTRESTARTABLE|Falha nessa tarefa ou nesse contêiner, mas como a propriedade FailPackageOnFailure é FALSE, o pacote continuará. Esse aviso é gerado quando a propriedade SaveCheckpoints do pacote está definida como TRUE e ocorre falha na tarefa ou no contêiner.|  
|0x80017101|-2147389183|DTS_W_EMPTYPATH|O caminho está vazio.|  
|0x80019002|-2147381246|DTS_W_MAXIMUMERRORCOUNTREACHED|Código de Aviso SSIS DTS_W_MAXIMUMERRORCOUNTREACHED.  O método Execution foi bem-sucedido, mas o número de erros aumentou (%1!d!) e alcançou o máximo permitido (%2!d!); resultando em falha. Isso ocorre quando o número de erros atinge aquele especificado em MaximumErrorCount. Altere o MaximumErrorCount ou corrija os erros.|  
|0x80019003|-2147381245|DTS_W_CONFIGENVVARNOTFOUND|Uma variável do ambiente de configuração não foi encontrada.  A variável de ambiente era: "%1". Isso ocorre quando um pacote especifica uma variável de ambiente para um parâmetro de configuração, mas ela não é encontrada. Verifique a coleção de configurações no pacote e se a variável de ambiente especificada está disponível e é válida.|  
|0x80019316|-2147380458|DTS_W_CONNECTIONPROVIDERCHANGE|O nome do provedor para o gerenciador de conexões "%1" foi alterado de "%2" para "%3".|  
|0x80019317|-2147380457|DTS_W_READEXTMAPFAILED|Exceção ao ler os arquivos de mapeamento de atualização. A exceção é "%1".|  
|0x80019318|-2147380456|DTS_W_DUPLICATEMAPPINGKEY|Há um mapeamento duplicado no arquivo, "%1". A marca é "%2" e a chave é "%3".|  
|0x80019319|-2147380455|DTS_W_IMPLICITUPGRADEMAPPING|A extensão, "%1", foi atualizada implicitamente para "%2". Adicione um mapeamento para essa extensão ao diretório UpgradeMappings.|  
|0x8001931A|-2147380454|DTS_W_INVALIDEXTENSIONMAPPING|Um mapeamento no arquivo, "%1", não é válido. Os valores não podem ser nulos nem vazios. A marca é "%2", a chave é "%3" e o valor é "%4".|  
|0x8001931C|-2147380452|DTS_W_ADOCONNECTIONDATATYPECOMPATCHANGE|A propriedade DataTypeCompatibility do gerenciador de conexões de tipo ADO "%1" foi definido a 80 por razões de compatibilidade com versões anteriores.|  
|0x8001C004|-2147368956|DTS_W_FILEENUMEMPTY|O enumerador For Each File está vazio. O enumerador For Each File não encontrou nenhum arquivo que corresponda ao padrão de arquivo, ou o diretório especificado estava vazio.|  
|0x8001F02F|-2147356625|DTS_W_COULDNOTRESOLVEPACKAGEPATH|Não é possível resolver um caminho de pacote para um objeto no pacote "%1". Verifique se o caminho de pacote é válido.|  
|0x8001F203|-2147356157|DTS_W_ITERATIONEXPRESSIONISNOTASSIGNMENT|A expressão de iteração não é uma expressão de atribuição: "%1". Esse erro normalmente ocorre quando a expressão existente na expressão de atribuição no ForLoop não é uma expressão de atribuição.|  
|0x8001F204|-2147356156|DTS_W_INITIALIZATIONEXPRESSIONISNOTASSIGNMENT|A expressão de inicialização não é uma expressão de atribuição: "%1". Esse erro normalmente ocorre quando a expressão existente na expressão de iteração no ForLoop não é uma expressão de atribuição.|  
|0x8001F205|-2147356155|DTS_W_LOGPROVIDERNOTDEFINED|O executável "%1" foi colado com sucesso. No entanto, um provedor de log que estava associado ao executável não foi encontrado na coleção "LogProviders".  O executável foi colado sem as informações do provedor de log.|  
|0x8001F300|-2147355904|DTS_W_PACKAGEUPGRADED|Atualização do pacote bem-sucedida.|  
|0x8001F42B|-2147355605|DTS_W_LEGACYPROGID|A ProgID "%1" foi preterida. A nova ProgID deste componente "%2" deve ser usada.|  
|0x80020918|-2147350248|DTS_W_FTPTASK_OPERATIONFAILURE|Falha na operação "%1".|  
|0x800283A5|-2147318875|DTS_W_MSMQTASK_USE_WEAK_ENCRYPTION|O algoritmo de criptografia "%1" usa criptografia fraca.|  
|0x80029164|-2147315356|DTS_W_FSTASK_OPERATIONFAILURE|Falha na tarefa ao executar a operação "%1".|  
|0x80029185|-2147315323|DTS_W_EXECPROCTASK_FILENOTINPATH|O arquivo/processo "%1" não está no caminho.|  
|0x800291C6|-2147315258|DTS_W_SENDMAILTASK_SUBJECT_MISSING|O assunto está vazio.|  
|0x800291C7|-2147315257|DTS_W_SENDMAILTASK_ERROR_IN_TO_LINE|O endereço na linha "Para" está incorreto. Ele é inválido ou o símbolo "\@" está ausente.|  
|0x800291C8|-2147315256|DTS_W_SENDMAILTASK_AT_MISSING_IN_FROM|O endereço na linha "De" está incorreto. Ele é inválido ou o símbolo "\@" está ausente.|  
|0x8002927A|-2147315078|DTS_W_XMLTASK_DIFFFAILURE|Os dois documentos XML são diferentes.|  
|0x8002928C|-2147315060|DTS_W_XMLTASK_DTDVALIDATIONWARNING|A validação DTD usará o arquivo DTD definido na linha DOCTYPE no documento XML. Não usará o que está atribuído à propriedade "%1".|  
|0x8002928D|-2147315059|DTS_W_XMLTASK_VALIDATIONFAILURE|Falha na tarefa ao validar "%1".|  
|0x80029291|-2147315055|DTS_W_TRANSFERDBTASK_ACTIONSETTOCOPY|O valor de ação de transferência era inválido.  Está sendo definido para copiar.|  
|0x80029292|-2147315054|DTS_W_TRANSFERDBTASK_METHODSETTOONLINE|O valor do método de transferência era inválido.  Está sendo definido como uma transferência online.|  
|0x8002F304|-2147290364|DTS_W_PROBLEMOCCURREDWITHFOLLOWINGMESSAGE|Ocorreu um problema com estas mensagens: "%1".|  
|0x8002F322|-2147290334|DTS_W_ERRMSGTASK_ERRORMESSAGEALREADYEXISTS|A mensagem de erro "%1" já existe no servidor de destino.|  
|0x8002F331|-2147290319|DTS_W_JOBSTASK_JOBEXISTSATDEST|O trabalho "%1" já existe no servidor de destino.|  
|0x8002F332|-2147290318|DTS_W_JOBSTASK_SKIPPINGJOBEXISTSATDEST|Ignorando a transferência do trabalho "%1" porque ela já existe no destino.|  
|0x8002F333|-2147290317|DTS_W_JOBSTASK_OVERWRITINGJOB|Substituindo o trabalho "%1" no servidor de destino.|  
|0x8002F339|-2147290311|DTS_W_LOGINSTASK_ENUMVALUEINCORRECT|O valor de enumeração persistente da propriedade "FailIfExists" foi alterado e tornou-se inválido. Redefinindo para o padrão.|  
|0x8002F343|-2147290301|DTS_W_LOGINSTASK_OVERWRITINGLOGINATDEST|Substituindo Logon "%1" no destino.|  
|0x8002F356|-2147290282|DTS_W_TRANSOBJECTSTASK_SPALREADYATDEST|O procedimento armazenado "%1" já existe no destino.|  
|0x8002F360|-2147290272|DTS_W_TRANSOBJECTSTASK_RULEALREADYATDEST|A regra "%1" já existe no destino.|  
|0x8002F364|-2147290268|DTS_W_TRANSOBJECTSTASK_TABLEALREADYATDEST|A tabela "%1" já existe no destino.|  
|0x8002F368|-2147290264|DTS_W_TRANSOBJECTSTASK_VIEWALREADYATDEST|A exibição "%1" já existe no destino.|  
|0x8002F372|-2147290254|DTS_W_TRANSOBJECTSTASK_UDFALREADYATDEST|A Função Definida pelo Usuário "%1" já existe no destino.|  
|0x8002F376|-2147290250|DTS_W_TRANSOBJECTSTASK_DEFAULTALREADYATDEST|O padrão "%1" já existe no destino.|  
|0x8002F380|-2147290240|DTS_W_TRANSOBJECTSTASK_UDDTALREADYATDEST|O Tipo de Dados Definido pelo Usuário "%1" já existe no destino.|  
|0x8002F384|-2147290236|DTS_W_TRANSOBJECTSTASK_PFALREADYATDEST|A Função de Partição "%1" já existe no destino.|  
|0x8002F388|-2147290232|DTS_W_TRANSOBJECTSTASK_PSALREADYATDEST|O Esquema de Partição "%1" já existe no destino.|  
|0x8002F391|-2147290223|DTS_W_TRANSOBJECTSTASK_SCHEMAALREADYATDEST|O Esquema "%1" já existe no destino.|  
|0x8002F396|-2147290218|DTS_W_TRANSOBJECTSTASK_SQLASSEMBLYALREADYATDEST|O SqlAssembly "%1" já existe no destino.|  
|0x8002F400|-2147290112|DTS_W_TRANSOBJECTSTASK_AGGREGATEALREADYATDEST|A Agregação Definida pelo Usuário "%1" já existe no destino.|  
|0x8002F404|-2147290108|DTS_W_TRANSOBJECTSTASK_TYPEALREADYATDEST|O Tipo Definido pelo Usuário "%1" já existe no destino.|  
|0x8002F408|-2147290104|DTS_W_TRANSOBJECTSTASK_XMLSCHEMACOLLECTIONALREADYATDEST|O XmlSchemaCollection "%1" já existe no destino.|  
|0x8002F412|-2147290094|DTS_W_TRANSOBJECTSTASK_NOELEMENTSPECIFIEDTOTRANSFER|Não existe nenhum elemento especificado para ser transferido.|  
|0x8002F415|-2147290091|DTS_W_TRANSOBJECTSTASK_LOGINALREADYATDEST|O logon "%1" já existe no destino.|  
|0x8002F41A|-2147290086|DTS_W_TRANSOBJECTSTASK_USERALREADYATDEST|O usuário "%1" já existe no destino.|  
|0x80047007|-2147192825|DTS_W_NOLINEAGEVALIDATION|As IDs de linhagem das colunas de entrada não podem ser validadas porque as árvores de execução contêm ciclos.|  
|0x80047034|-2147192780|DTS_W_EMPTYDATAFLOW|A tarefa DataFlow não tem nenhum componente. Adicione componentes ou remova a tarefa.|  
|0x80047069|-2147192727|DTS_W_SORTEDOUTPUTHASNOSORTKEYPOSITIONS|A propriedade IsSorted do %1 está definida como TRUE, mas todos os SortKeyPositions das suas colunas de saída estão definidas como zero.|  
|0x8004706F|-2147192721|DTS_W_SOURCEREMOVED|A origem "%1" (%2!d!) não será lida porque nenhum de seus dados fica visível fora da Tarefa de Fluxo de Dados.|  
|0x80047076|-2147192714|DTS_W_UNUSEDOUTPUTDATA|A coluna de saída "%1" (%2!d!) na saída "%3" (%4!d!) e componente "%5" (%6!d!) não é usada subsequentemente na tarefa de Fluxo de Dados. A remoção dessa coluna de saída não utilizada melhora o desempenho da tarefa Fluxo de Dados.|  
|0x800470AE|-2147192658|DTS_W_COMPONENTREMOVED|O componente "%1" (%2!d!) foi removido da tarefa de Fluxo de Dados porque sua saída não foi usada e suas entradas não têm efeitos colaterais ou não estão conectadas a saídas de outros componentes. Se o componente for necessário, a propriedade HasSideEffects em pelo menos uma de suas entradas deve ser definida como verdadeira, ou sua saída de ser conectada a algum componente.|  
|0x800470B0|-2147192656|DTS_W_NOWORKTODO|Foram atribuídas linhas a um thread, mas esse thread não tem nenhum trabalho a realizar. O layout tem uma saída desconectada. Será mais rápido executar o pipeline com a propriedade RunInOptimizedMode definida como TRUE, evitando, assim, esse aviso.|  
|0x800470C8|-2147192632|DTS_W_EXTERNALMETADATACOLUMNSOUTOFSYNC|As colunas externas para %1 estão fora de sincronização com as colunas de fonte de dados. %2|  
|0x800470C9|-2147192631|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSADDITION|A coluna "%1" precisa ser adicionada às colunas externas.|  
|0x800470CA|-2147192630|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSUPDATE|A coluna externa "%1" precisa ser atualizada.|  
|0x800470CB|-2147192629|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSREMOVAL|A %1 precisa ser removida das colunas externas.|  
|0x800470D8|-2147192616|DTS_W_EXPREVALPOTENTIALSTRINGTRUNCATION|A cadeia de caracteres de resultado para a expressão "%1" poderá ser truncada se exceder o comprimento máximo de %2!d! caracteres. A expressão pode ter um valor de resultado que exceda o tamanho máximo de um DT_WSTR.|  
|0x800470E9|-2147192599|DTS_W_COMPONENTLEAKPROCESSINPUT|Uma chamada para o método ProcessInput da entrada %1!d! em %2 manteve inesperadamente uma referência ao buffer que foi transmitido. O refcount naquele buffer era %3!d! antes da chamada e %4!d! depois que a chamada retornasse.|  
|0x800470EB|-2147192597|DTS_W_EXPREVALUNREFERENCEDINPUTCOLUMN|O "%1" em "%2" tem tipo de uso READONLY, mas não é referenciado por uma expressão. Remova a coluna da lista de colunas de entrada disponíveis ou a referencie a uma expressão.|  
|0x8004801E|-2147188706|DTS_W_COULDNOTFINDCURRENTVERSION|Não é possível encontrar o valor "%1" para o componente %2. O valor de CurrentVersion para o componente não pode ser localizado. Esse erro ocorrerá se o componente não tiver definido suas informações de Registro para que contenham um valor de CurrentVersion na seção DTSInfo. Essa mensagem ocorre durante o desenvolvimento do componente, ou quando o componente é usado em um pacote, se o componente não for corretamente registrado.|  
|0x80049300|-2147183872|DTS_W_BUFFERGETTEMPFILENAME|O gerenciador de buffer não pôde adquirir um nome de arquivo temporário.|  
|0x80049301|-2147183871|DTS_W_UNUSABLETEMPORARYPATH|O gerenciador de buffer não criou um arquivo temporário no caminho "%1". O caminho não será considerado novamente para armazenamento temporário.|  
|0x80049304|-2147183868|DTS_W_DF_PERFCOUNTERS_DISABLED|Aviso: não foi possível abrir a memória compartilhada global para se comunicar com o desempenho DLL; contadores de desempenho de fluxo de dados não estão disponíveis.  Para resolver, execute este pacote como um administrador ou no console do sistema.|  
|0x8020200F|-2145378289|DTS_W_PARTIALROWFOUNDATENDOFFILE|Existe uma linha parcial no final do arquivo.|  
|0x8020202B|-2145378261|DTS_W_ENDOFFILEREACHWHILEREADINGHEADERROWS|O final do arquivo de dados foi atingido durante a leitura das linhas de cabeçalho. Verifique se o delimitador de linha de cabeçalho e o número de linhas de cabeçalho a serem ignoradas estão corretos.|  
|0x80202066|-2145378202|DTS_W_CANTRETRIEVECODEPAGEFROMOLEDBPROVIDER|Não é possível recuperar as informações da página de código de coluna do provedor OLE DB.  Se o componente fornecer suporte à propriedade "%1", a página de código dessa propriedade será usada.  Altere o valor da propriedade se os valores da página de código de cadeia de caracteres atuais estiverem incorretos.  Se o componente não fornecer suporte à propriedade, a página de código da identificação de localidade do componente será usada.|  
|0x802020F7|-2145378057|DTS_W_TXSORTSORTISTHESAME|Os dados já estão classificados conforme as especificações, portanto, a transformação pode ser removida.|  
|0x8020400D|-2145370099|DTS_W_NOPIPELINEDATATYPEMAPPINGAVAILABLE|O %1 faz referência a um tipo de dados externos que não pode ser mapeado para um tipo de dados da tarefa de Fluxo de Dados. Em seu lugar, será usado o tipo de dados DT_WSTR da tarefa Fluxo de Dados.|  
|0x802070CC|-2145357620|DTS_W_STATICTRUNCATIONINEXPRESSION|A expressão "%1" sempre resultará em truncamento de dados. A expressão contém um truncamento estático (truncamento de um valor fixo).|  
|0x8020820C|-2145353204|DTS_W_UNMAPPEDINPUTCOLUMN|A coluna de entrada "%1" com ID %2!d! no índice %3!d! não foi mapeada. A ID de linhagem para a coluna é zero.|  
|0x80208305|-2145352955|DTS_W_TXFUZZYLOOKUP_DELIMITERS_DONT_MATCH|Os delimitadores especificados não correspondem aos delimitadores usados para criar o índice de correspondência pré-existente "%1". Esse erro ocorre quando os delimitadores usados para criar tokens de campos não correspondem. Isso pode ter efeitos desconhecidos nos resultados ou no comportamento de correspondência.|  
|0x80208308|-2145352952|DTS_W_TXFUZZYLOOKUP_MAXRESULTS_IS_ZERO|A propriedade MaxOutputMatchesPerInput na transformação Pesquisa Difusa é zero. Nenhum resultado será produzido.|  
|0x80208310|-2145352944|DTS_W_TXFUZZYLOOKUP_NO_FUZZY_JOIN_COLUMNS|Não havia nenhuma coluna de entrada válida com propriedade de coluna JoinType definida como Difusa.  É possível melhorar o desempenho em junções Exatas, usando a transformação Pesquisa em lugar de Pesquisa Difusa.|  
|0x8020831C|-2145352932|DTS_W_TXFUZZYLOOKUP_TIMESTAMPCAVEAT|A coluna de referência "%1" pode ser uma coluna de carimbo de hora SQL. Quando é criado o índice de correspondência difusa e é feita uma cópia da tabela de referência, todos os carimbos da tabela de referência refletirão o estado da tabela no momento da cópia. Pode ocorrer um comportamento inesperado se CopyReferenceTable for definido como falso.|  
|0x80208321|-2145352927|DTS_W_MATCHINDEXALREADYEXISTS|Uma tabela com o nome '%1' atribuída para MatchIndexName já existe e DropExistingMatchIndex está definido como FALSE.  Não será possível executar a transformação, a menos que essa tabela seja descartada, um nome diferente seja especificado ou DropExisitingMatchIndex seja definido como TRUE.|  
|0x8020832B|-2145352917|DTS_W_TXFUZZYLOOKUP_JOINLENGTHMISMATCH|O comprimento da coluna de entrada '%1' não é igual ao comprimento da coluna de referência '%2' à qual está sendo feita a correspondência.|  
|0x8020832D|-2145352915|DTS_W_TXFUZZYLOOKUP_CODEPAGE_MISMATCH|As páginas de código da coluna de origem DT_STR "%1" e da coluna de destino DT_STR "%2" não correspondem.  Isso pode causar resultados inesperados.|  
|0x8020832E|-2145352914|DTS_W_FUZZYLOOKUP_TOOMANYEXACTMATCHCOLUMNS|Há mais de 16 junções de correspondência exata, assim o desempenho pode não ser o ideal. Reduza o número de junções de correspondência exata para melhorar o desempenho. O SQL Server tem como limite 16 colunas por índice, será usado o índice invertido para todas as pesquisas.|  
|0x80208350|-2145352880|DTS_W_FUZZYLOOKUP_MEMLIMITANDEXHAUSTIVESPECIFIED|A opção Exhaustive exige que toda a referência seja carregada na memória principal.  Considerando que foi especificado um limite de memória para a propriedade MaxMemoryUsage propriedade, é possível que a tabela de referência inteira não caiba dentro desse limite e que a operação de correspondência falhe no tempo de execução.|  
|0x80208351|-2145352879|DTS_W_FUZZYLOOKUP_EXACTMATCHCOLUMNSEXCEEDBYTELIMIT|Os comprimentos cumulativos das colunas especificadas nas junções de correspondência exata excedem o limite de 900 bytes para chaves de índice.  A Pesquisa Difusa cria um índice nas colunas de correspondência exata para melhorar o desempenho da pesquisa, e é possível que a criação desse índice falhe e a pesquisa volte a um método alternativo, talvez mais lento, de localização de correspondências. Se houver problema de desempenho, tente remover algumas colunas de junção de correspondência exata ou reduzir os comprimentos máximos das colunas de correspondência exata de comprimento variável.|  
|0x80208352|-2145352878|DTS_W_FUZZYLOOKUP_EXACTMATCHINDEXCREATIONFAILED|Falha ao criar um índice para colunas de correspondência exata. Revertendo para o método alternativo de pesquisa difusa.|  
|0x80208353|-2145352877|DTS_W_FUZZYGROUPINGINTERNALPIPELINEWARNING|O seguinte aviso de pipeline interno de Agrupamento Difuso ocorreu com o código de aviso 0x%1!8.8X!: "%2".|  
|0x80208375|-2145352843|DTS_W_XMLSRCOUTPUTCOLUMNLENGTHSETTODEFAULT|Nenhum comprimento máximo foi especificado para o %1 com o tipo de dados externos %2. O tipo de dados "%3" da tarefa de fluxo de dados do SSIS com um comprimento de %4!d! será usado.|  
|0x80208376|-2145352842|DTS_W_XMLSRCOUTPUTCOLUMNDATATYPEMAPPEDTOSTRING|O %1 faz referência a um tipo de dados externos %2, que não pode ser mapeado para um tipo de dados da tarefa de Fluxo de Dados do SSIS.  O tipo de dados da Tarefa de Fluxo de Dados DT_WSTR com um comprimento de %3!d! será usado.|  
|0x80208385|-2145352827|DTS_W_NOREDIRECTWITHATTACHEDERROROUTPUTS|Nenhuma linha será enviada à(s) saída(s) de erro. Configure as disposições de erro ou truncamento para redirecionar as linhas para a(s) saída(s) de erro, ou exclua as transformações ou os destinos de fluxo de dados que estão anexados à(s) saída(s).|  
|0x80208386|-2145352826|DTS_W_REDIRECTWITHNOATTACHEDERROROUTPUTS|As linhas enviadas à(s) saída(s) de erro serão perdidas. Adicione novas transformações ou destinos de fluxo de dados para receber linhas de erro, ou reconfigure para deixar de redirecionar as linhas à(s) saída(s) de erro.|  
|0x80208391|-2145352815|DTS_W_XMLSRCOUTPUTCOLUMNLENGTHSETTOMAXIMUM|Para %1, com o tipo de dados externo %2, o esquema XML especificou uma restrição de maxLength de %3!d!, que excede o comprimento máximo permitido para a coluna de %4!d!. O tipo de dados "%5" da Tarefa de Fluxo de Dados do SSIS com um comprimento de %6!d! será usado.|  
|0x802090E4|-2145349404|DTS_W_TXLOOKUP_DUPLICATE_KEYS|O %1 encontrou valores de chave de referência duplicados ao armazenar em cache dados de referência. Este erro ocorre apenas no modo Cache Cheio. Remova os valores de chave duplicados ou altere o modo de cache para PARTIAL ou NO_CACHE.|  
|0x802092A7|-2145348953|DTS_W_POTENTIALTRUNCATIONFROMDATAINSERTION|O truncamento pode ocorrer devido à inserção de dados da coluna de fluxo de dados "%1" com comprimento de %2!d! para a coluna de banco de dados "%3" com um comprimento de %4!d!.|  
|0x802092A8|-2145348952|DTS_W_POTENTIALTRUNCATIONFROMDATARETRIEVAL|O truncamento pode ocorrer devido à recuperação de dados da coluna do banco de dados "%1" com comprimento de %2!d! para a coluna de fluxo de dados "%3" com um comprimento de %4!d!.|  
|0x802092AA|-2145348950|DTS_W_ADODESTBATCHNOTSUPPORTEDFORERRORDISPOSITION|Não há suporte atualmente para o modo em lote quando a disposição de linha de erro for usada. A propriedade BatchSize será definida como 1.|  
|0x802092AB|-2145348949|DTS_W_ADODESTNOROWSINSERTED|Nenhuma linha foi inserida com êxito no destino. Talvez devido à falta de correspondência de tipo de dados entre colunas, ou devido ao uso de um tipo de dados que não tem suporte em seu provedor ADO.NET. Como a disposição de erro deste componente não é "Componente com falha", as mensagens de erro não são mostradas aqui; defina a disposição de erro como "Componente com falha" para ver as mensagens de erro aqui.|  
|0x802092AC|-2145348948|DTS_W_ADODESTPOTENTIALDATALOSS|Pode ocorrer perda de dados em potencial devido à inserção de dados da coluna de entrada "%1" com tipo de dados "%2" para a coluna externa "%3" com tipo de dados "%4". Se isso for pretendido, um modo alternativo para fazer a conversão será usar um componente de Conversão de dados antes do componente de destino do ADO NET.|  
|0x802092AD|-2145348947|DTS_W_ADODESTEXTERNALCOLNOTMATCHSCHEMACOL|O %1 esteve fora de sincronização com a coluna de banco de dados.  A última coluna tem %2. Use o editor avançado para atualizar as colunas de destino disponíveis se necessário.|  
|0x802092AE|-2145348946|DTS_W_ADODESTEXTERNALCOLNOTEXIST|O %1 não existe no banco de dados. Ele pode ter sido removido ou renomeado. Use o Editor Avançado para atualizar as colunas de destino disponíveis se necessário.|  
|0x802092AF|-2145348945|DTS_W_ADODESTNEWEXTCOL|Uma coluna nova com nome %1 foi adicionada à tabela de banco de dados externa. Use o editor avançado para atualizar as colunas de destino disponíveis se necessário.|  
|0x8020930C|-2145348852|DTS_W_NOMATCHOUTPUTGETSNOROWS|Nenhuma linha será enviada à saída sem-correspondência. Configure a transformação para redirecionar as linhas sem entradas correspondentes para a saída sem-correspondência, ou exclua as transformações ou os destinos de fluxo de dados que estão anexados à saída sem-correspondência.|  
|0x8020931B|-2145348837|DTS_W_ADODESTINVARIANTEXCEPTION|Exceção recebida ao enumerar os provedores ADO.NET. O invariável era "%1". A mensagem de exceção é: "%2"|  
|0xC020822C|-1071611348|DTS_W_UNMAPPEDOUTPUTCOLUMN|O %1 não tem nenhuma coluna de entrada mapeada para ele.|  
|0x930D|37645|DTS_W_EXTERNALTABLECOLSOUTOFSYNC|A tabela "%1" foi alterada. Novas colunas podem ter sido adicionadas à tabela.|  
  
##  <a name="msgInfo"></a> Mensagens informativas  
 Os nomes simbólicos das mensagens informativas do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] começam com **DTS_I_** .  
  
|Código hexadecimal|Código decimal|Nome simbólico|Descrição|  
|----------------------|------------------|-------------------|-----------------|  
|0x4001100A|1073811466|DTS_I_STARTINGTRANSACTION|Iniciando uma transação distribuída para esse contêiner.|  
|0x4001100B|1073811467|DTS_I_COMMITTINGTRANSACTION|Confirmando a transação distribuída iniciada por esse contêiner.|  
|0x4001100C|1073811468|DTS_I_ABORTINGTRANSACTION|Abortando a transação distribuída atual.|  
|0x40013501|1073820929|DTS_I_GOTMUTEXFROMWAIT|Mutex "%1" foi adquirido com êxito.|  
|0x40013502|1073820930|DTS_I_RELEASEACQUIREDMUTEX|Mutex "%1" foi liberado com êxito.|  
|0x40013503|1073820931|DTS_I_NEWMUTEXCREATED|Mutex "%1" foi criado com êxito.|  
|0x40015101|1073828097|DTS_I_DUMP_ON_ANY_ERR|Serão gerados arquivos de despejo de depuração para qualquer evento de erro.|  
|0x40015102|1073828098|DTS_I_DUMP_ON_CODES|Serão gerados arquivos de despejo de depuração para os seguintes códigos de evento: "%1"|  
|0x40015103|1073828099|DTS_I_START_DUMP|Código de evento, 0x%1!8.8X!, geração disparada de arquivos de despejo de depuração na pasta "%2".|  
|0x40015104|1073828100|DTS_I_SSIS_INFO_DUMP|Criando arquivo de despejo de informações do SSIS "%1".|  
|0x40015106|1073828102|DTS_I_FINISH_DUMP|Arquivos de despejo de depuração criados com êxito.|  
|0x40016019|1073831961|DTS_I_PACKAGEMIGRATED|O formato do pacote foi migrado com êxito da versão %1!d! para a versão %2!d!. Para reter as alterações da migração, é necessário salvar.|  
|0x4001601A|1073831962|DTS_I_SCRIPTSMIGRATED|Os scripts do pacote foram migrados. Para reter as alterações da migração, é necessário salvar o pacote.|  
|0x40016025|1073831973|DTS_I_FTPRECEIVEFILE|Recebendo o arquivo "%1".|  
|0x40016026|1073831974|DTS_I_FTPSENDFILE|Enviando o arquivo "%1".|  
|0x40016027|1073831975|DTS_I_FTPFILEEXISTS|O arquivo "%1" já existe.|  
|0x40016028|1073831976|DTS_I_FTPERRORLOADINGMSG|Não é possível obter informações extras de erro por causa de um erro interno.|  
|0x40016036|1073831990|DTS_I_FTPDELETEFILE|Falha na tentativa de excluir o arquivo "%1". Isso pode ocorrer quando o arquivo não existir, o nome do arquivo for digitado de forma incorreta, ou você não tiver permissões para excluir o arquivo.|  
|0x40016037|1073831991|DTS_I_CONFIGFROMREG|O pacote está tentando configurar a partir de uma entrada de registro usando a chave do Registro "%1".|  
|0x40016038|1073831992|DTS_I_CONFIGFROMENVVAR|O pacote está tentando configurar a partir da variável de ambiente "%1".|  
|0x40016039|1073831993|DTS_I_CONFIGFROMINIFILE|O pacote está tentando configurar a partir do arquivo .ini "%1".|  
|0x40016040|1073832000|DTS_I_CONFIGFROMSQLSERVER|O pacote está tentando configurar a partir do SQL Server usando a cadeia de caracteres de configuração "%1".|  
|0x40016041|1073832001|DTS_I_CONFIGFROMFILE|O pacote está tentando configurar a partir do arquivo XML "%1".|  
|0x40016042|1073832002|DTS_I_CONFIGFROMPARENTVARIABLE|O pacote está tentando configurar a partir da variável pai "%1".|  
|0x40016043|1073832003|DTS_I_ATTEMPTINGUPGRADEOFDTS|Tentando uma atualização do SSIS da versão "%1" para a versão "%2". O pacote está tentando para atualizar o tempo de execução.|  
|0x40016044|1073832004|DTS_I_ATTEMPTINGUPGRADEOFANEXTOBJ|Tentando atualizar "%1". O pacote está tentando atualizar um objeto extensível.|  
|0x40016045|1073832005|DTS_I_SAVECHECKPOINTSTOFILE|O pacote salvará os pontos de verificação no arquivo "%1" durante a execução. O pacote está configurado para salvar os pontos de verificação.|  
|0x40016046|1073832006|DTS_I_RESTARTFROMCHECKPOINTFILE|O pacote foi reinicializado a partir do arquivo "%1" de ponto de verificação. O pacote foi configurado para reinicializar a partir do ponto de verificação.|  
|0x40016047|1073832007|DTS_I_CHECKPOINTSAVEDTOFILE|O arquivo "%1" de ponto de verificação foi atualizado para registrar a conclusão desse contêiner.|  
|0x40016048|1073832008|DTS_I_CHECKPOINTFILEDELETED|O arquivo "%1" de ponto de verificação foi excluído depois de concluído com êxito o pacote.|  
|0x40016049|1073832009|DTS_I_CHECKPOINTSAVINGTOFILE|Iniciando a atualização do arquivo "%1" de ponto de verificação.|  
|0x40016051|1073832017|DTS_I_CHOSENMAXEXECUTABLES|Com base na configuração do sistema, o número máximo de executáveis simultâneos é definido como %1!d!.|  
|0x40016052|1073832018|DTS_I_MAXEXECUTABLES|O número máximo de executáveis simultâneos está definido como %1!d!.|  
|0x40016053|1073832019|DTS_I_PACKAGESTART|Começando a execução do pacote.|  
|0x40016054|1073832020|DTS_I_PACKAGEEND|Conclusão da execução do pacote.|  
|0x40029161|1073910113|DTS_I_FSTASK_DIRECTORYDELETED|O diretório "%1" foi excluído.|  
|0x40029162|1073910114|DTS_I_FSTASK_FILEDELETED|O arquivo ou diretório "%1" foi excluído.|  
|0x400292A8|1073910440|DTS_I_TRANSFERDBTASK_OVERWRITEDB|Substituindo o banco de dados "%1" no servidor de destino "%2".|  
|0x4002F304|1073935108|DTS_I_SOMETHINGHAPPENED|"%1".|  
|0x4002F323|1073935139|DTS_I_ERRMSGTASK_SKIPPINGERRORMESSAGEALREADYEXISTS|Ignorando a mensagem de erro "%1" porque ela já existe no servidor de destino.|  
|0x4002F326|1073935142|DTS_I_ERRMSGTASK_TRANSFEREDNERRORMESSAGES|"%1" Mensagens de Erro foram transferidas.|  
|0x4002F351|1073935185|DTS_I_STOREDPROCSTASKS_TRANSFEREDNSPS|A tarefa transferiu "%1" Procedimentos Armazenados.|  
|0x4002F352|1073935186|DTS_I_TRANSOBJECTSTASK_TRANSFEREDNOBJECTS|Foram transferidos "%1" objetos.|  
|0x4002F358|1073935192|DTS_I_TRANSOBJECTSTASK_NOSPSTOTRANSFER|Não existem Procedimentos Armazenados para serem transferidos.|  
|0x4002F362|1073935202|DTS_I_TRANSOBJECTSTASK_NORULESTOTRANSFER|Não existem Regras para serem transferidas.|  
|0x4002F366|1073935206|DTS_I_TRANSOBJECTSTASK_NOTABLESTOTRANSFER|Não existem Tabelas para serem transferidas.|  
|0x4002F370|1073935216|DTS_I_TRANSOBJECTSTASK_NOVIEWSTOTRANSFER|Não existem Exibições para serem transferidas.|  
|0x4002F374|1073935220|DTS_I_TRANSOBJECTSTASK_NOUDFSTOTRANSFER|Não existem Funções Definidas pelo Usuário para serem transferidas.|  
|0x4002F378|1073935224|DTS_I_TRANSOBJECTSTASK_NODEFAULTSTOTRANSFER|Não existem Padrões para serem transferidos.|  
|0x4002F382|1073935234|DTS_I_TRANSOBJECTSTASK_NOUDDTSTOTRANSFER|Não existem Tipos de Dados Definidos pelo Usuário para serem transferidos.|  
|0x4002F386|1073935238|DTS_I_TRANSOBJECTSTASK_NOPFSTOTRANSFER|Não existem Funções de Partição para serem transferidas.|  
|0x4002F390|1073935248|DTS_I_TRANSOBJECTSTASK_NOPSSTOTRANSFER|Não existem Esquemas de Partição para serem transferidos.|  
|0x4002F394|1073935252|DTS_I_TRANSOBJECTSTASK_NOSCHEMASTOTRANSFER|Não existem Esquemas para serem transferidos.|  
|0x4002F398|1073935256|DTS_I_TRANSOBJECTSTASK_NOSQLASSEMBLIESTOTRANSFER|Não existem SqlAssemblies para serem transferidos.|  
|0x4002F402|1073935362|DTS_I_TRANSOBJECTSTASK_NOAGGREGATESTOTRANSFER|Não existem Agregações Definidas pelo Usuário para serem transferidas.|  
|0x4002F406|1073935366|DTS_I_TRANSOBJECTSTASK_NOTYPESTOTRANSFER|Não existem Tipos Definidos pelo Usuário para serem transferidos.|  
|0x4002F410|1073935376|DTS_I_TRANSOBJECTSTASK_NOXMLSCHEMACOLLECTIONSTOTRANSFER|Não existem XmlSchemaCollections para serem transferidos.|  
|0x4002F418|1073935384|DTS_I_TRANSOBJECTSTASK_NOLOGINSTOTRANSFER|Não existem Logons para serem transferidos.|  
|0x4002F41D|1073935389|DTS_I_TRANSOBJECTSTASK_NOUSERSTOTRANSFER|Não existem Usuários para serem transferidos.|  
|0x4002F41E|1073935390|DTS_I_TRANSOBJECTSTASK_TRUNCATINGTABLE|Truncando a tabela "%1"|  
|0x40043006|1074016262|DTS_I_EXECUTIONPHASE_PREPAREFOREXECUTE|A fase de Preparação para Execução está começando.|  
|0x40043007|1074016263|DTS_I_EXECUTIONPHASE_PREEXECUTE|A fase de Pré-Execução está começando.|  
|0x40043008|1074016264|DTS_I_EXECUTIONPHASE_POSTEXECUTE|A fase de Pós-Execução está começando.|  
|0x40043009|1074016265|DTS_I_EXECUTIONPHASE_CLEANUP|A fase de Limpeza está começando.|  
|0x4004300A|1074016266|DTS_I_EXECUTIONPHASE_VALIDATE|A fase de Validação está começando.|  
|0x4004300B|1074016267|DTS_I_ROWS_WRITTEN|"%1" escreveu %2!ld! linhas.|  
|0x4004300C|1074016268|DTS_I_EXECUTIONPHASE_EXECUTE|A fase de Execução está começando.|  
|0x4004800C|1074036748|DTS_I_CANTRELIEVEPRESSURE|O gerenciador de buffer detectou que o sistema estava com pouca memória virtual, mas não conseguiu trocar de buffers. %1!d! buffers foram considerados e %2!d! foram bloqueados. Não existe memória suficiente para o pipeline porque não foi instalada memória suficiente, outros processos a estão usando, ou muitos buffers estão bloqueados.|  
|0x4004800D|1074036749|DTS_I_CANTALLOCATEMEMORYPRESSURE|O gerenciador de buffer abandonou uma chamada de alocação de memória para %3!d! bytes, mas não pôde trocar de buffer para aliviar a pressão de memória. %1!d! buffers foram considerados e %2!d! foram bloqueados. Não existe memória suficiente para o pipeline porque não foi instalada memória suficiente, outros processos a estavam usando, ou muitos buffers estavam bloqueados.|  
|0x4004800E|1074036750|DTS_I_ALLOCATEDDURINGMEMORYPRESSURE|O gerenciador de buffer alocou %1!d! bytes, embora a pressão de memória tenha sido detectada e houve falha nas várias tentativas de troca de buffer.|  
|0x400490F4|1074041076|DTS_I_TXLOOKUP_CACHE_PROGRESS|%1 armazenou em cache %2!d! linhas.|  
|0x400490F5|1074041077|DTS_I_TXLOOKUP_CACHE_FINAL|%1 armazenou em cache um total de %2!d! linhas.|  
|0x4020206D|1075847277|DTS_I_RAWSOURCENOCOLUMNS|O adaptador de origem bruto abriu um arquivo, mas o arquivo não contém nenhuma coluna. O adaptador não produzirá dados. Isso pode indicar que um arquivo está danificado, ou que não existem colunas e, portanto, não existem dados.|  
|0x402020DA|1075847386|DTS_I_OLEDBINFORMATIONALMESSAGE|Uma mensagem informativa OLE DB está disponível.|  
|0x40208327|1075872551|DTS_I_TXFUZZYLOOKUP_EXACT_MATCH_PERF_COLLATIONS_DONT_MATCH|É possível melhorar o desempenho da correspondência difusa se a junção exata FuzzyComparisonFlags na coluna de entrada "%1" for definida para corresponder com a ordenação SQL para a coluna de tabela de referência "%2".  Além disso, nenhum sinalizador de dobra pode estar definido em FuzzyComparisonFlagsEx.|  
|0x40208328|1075872552|DTS_I_TXFUZZYLOOKUP_EXACT_MATCH_PERF_INDEX_MISSING|É possível melhorar o desempenho da correspondência difusa se um índice for criado com base na tabela de referência entre todas as colunas de correspondência exata especificadas.|  
|0x40208387|1075872647|DTS_I_DISPSNOTREVIEWED|As disposições de truncamento e erro não foram revisadas. Certifique-se de que esse componente esteja configurado para redirecionar as linhas para as saídas de erro, caso queira transformar posteriormente essas linhas.|  
|0x402090DA|1075876058|DTS_I_TXAGG_WORKSPACE_REHASH|A transformação Agregação encontrou %1!d! combinações de chaves. É necessário refazer o hash dos dados porque o número de combinações de chave é superior ao esperado. O componente pode ser configurado para evitar o re-hash de dados, ajustando as propriedades Keys, KeyScale e AutoExtendFactor.|  
|0x402090DB|1075876059|DTS_I_TXAGG_COUNTDISTINCT_REHASH|A transformação Agregação encontrou %1!d! valores distintos ao executar uma agregação "distinta de contagem" em "%2". A transformação gerará novo hash dos dados porque o número de valores distintos é superior ao esperado. O componente pode ser configurado para evitar refazer o hash de dados com o ajuste das propriedades CountDistinctKeys, CountDistinctKeyScale e AutoExtendFactor.|  
|0x402090DC|1075876060|DTS_I_STARTPROCESSINGFILE|Foi iniciado o processamento do arquivo "%1".|  
|0x402090DD|1075876061|DTS_I_FINISHPROCESSINGFILE|Foi concluído o processamento do arquivo "%1".|  
|0x402090DE|1075876062|DTS_I_TOTALDATAROWSPROCESSEDFORFILE|O número total de linhas de dados processadas para o arquivo "%1" é %2!I64d!.|  
|0x402090DF|1075876063|DTS_I_FINALCOMMITSTARTED|Foi iniciada a confirmação final para a inserção de dados em "%1".|  
|0x402090E0|1075876064|DTS_I_FINALCOMMITENDED|Foi concluída a confirmação final para a inserção de dados "%1".|  
|0x402090E1|1075876065|DTS_I_BEGINHASHINGCACHE|%1!u! linhas foram adicionadas ao cache. O sistema está processando as linhas.|  
|0x402090E2|1075876066|DTS_I_SUCCEEDEDHASHINGCACHE|O %1 processou %2!u! linhas no cache. O tempo de processamento foi de %3 segundos. O cache usou %4!I64u! bytes de memória.|  
|0x402090E3|1075876067|DTS_I_FAILEDHASHINGCACHE|Falha em %1 ao processar as linhas no cache.  O tempo de processamento foi de %2 segundos.|  
|0x402090E4|1075876068|DTS_I_SUCCEEDEDPREPARINGCACHE|O %1 teve êxito ao preparar o cache. O tempo de preparação foi de %2 segundos.|  
|0x40209314|1075876628|DTS_I_TXLOOKUP_PARTIALPERF|O %1 executou as seguintes operações: foram processadas %2!I64u! linhas, foram emitidos %3!I64u! comandos de banco de dados para o banco de dados de referência e foram executadas %4!I64u! pesquisas usando o cache parcial.|  
|0x40209315|1075876629|DTS_I_TXLOOKUP_PARTIALPERF2|O %1 executou as seguintes operações: foram processadas %2!I64u! linhas, foram emitidos %3!I64u! comandos de banco de dados para o banco de dados de referência, foram executadas %4!I64u! pesquisas usando o cache parcial e %5!I64u! pesquisas usando o cache para as linhas sem-correspondência de entradas na pesquisa inicial.|  
|0x40209316|1075876630|DTS_I_CACHEFILEWRITESTARTED|O %1 está gravando o cache no arquivo "%2".|  
|0x40209317|1075876631|DTS_I_CACHEFILEWRITESUCCEEDED|O %1 gravou o cache no arquivo "%2".|  
|0x4020F42C|1075901484|DTS_I_OLEDBDESTZEROMAXCOMMITSIZE|A propriedade de tamanho máximo de confirmação de inserção do destino de OLE DB "%1" é definida como 0. Essa configuração de propriedade pode fazer com que o pacote em execução pare de responder. Para obter mais informações, consulte o tópico da Ajuda F1 do Editor de Destino de OLE DB (Página do Gerenciador de Conexões).|  
  
##  <a name="msgGeneral"></a> Mensagens de evento e gerais  
 Os nomes simbólicos das mensagens de erro do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] começam com **DTS_MSG_** .  
  
|Código hexadecimal|Código decimal|Nome simbólico|Descrição|  
|----------------------|------------------|-------------------|-----------------|  
|0x1|1|DTS_MSG_CATEGORY_SERVICE_CONTROL|Função incorreta.|  
|0x2|2|DTS_MSG_CATEGORY_RUNNING_PACKAGE_MANAGEMENT|O sistema não pôde localizar o arquivo especificado.|  
|0x100|256|DTS_MSG_SERVER_STARTING|Iniciando o Microsoft SSIS Service.<br /><br /> Versão do servidor %1|  
|0x101|257|DTS_MSG_SERVER_STARTED|O Microsoft SSIS Service foi iniciado.<br /><br /> Versão do servidor %1|  
|0x102|258|DTS_MSG_SERVER_STOPPING|A operação de espera expirou.|  
|0x103|259|DTS_MSG_SERVER_STOPPED|Não existem mais dados disponíveis.|  
|0x104|260|DTS_MSG_SERVER_START_FAILED|Falha ao iniciar o Microsoft SSIS Service.<br /><br /> Erro: %1|  
|0x105|261|DTS_MSG_SERVER_STOP_ERROR|Erro ao parar o Microsoft SSIS Service.<br /><br /> Erro: %1|  
|0x110|272|DTS_MSG_SERVER_MISSING_CONFIG|O arquivo de configuração do Microsoft SSIS Service não existe.<br /><br /> Carregando as configurações padrão.|  
|0x111|273|DTS_MSG_SERVER_BAD_CONFIG|O arquivo de configuração do Microsoft SSIS Service está incorreto.<br /><br /> Erro na leitura do arquivo de configuração: %1<br /><br /> Carregando o servidor com as configurações padrão.|  
|0x112|274|DTS_MSG_SERVER_MISSING_CONFIG_REG|Microsoft SSIS Service:<br /><br /> A configuração de registro que especifica o arquivo de configuração não existe.<br /><br /> Tentando carregar arquivo de configuração padrão.|  
|0x150|336|DTS_MSG_SERVER_STOPPING_PACKAGE|Microsoft SSIS Service: interrompendo a execução do pacote.<br /><br /> ID de instância do pacote: %1<br /><br /> ID do Pacote: %2<br /><br /> Nome do pacote: %3<br /><br /> Descrição do pacote: %4<br /><br /> Pacote iniciado por: %5.|  
|0x40013000|1073819648|DTS_MSG_PACKAGESTART|Pacote "%1" iniciado.|  
|0x40013001|1073819649|DTS_MSG_PACKAGESUCCESS|Pacote "%1" concluído com êxito.|  
|0x40013002|1073819650|DTS_MSG_PACKAGECANCEL|Pacote "%1" cancelado.|  
|0x40013003|1073819651|DTS_MSG_PACKAGEFAILURE|Falha no pacote "%1".|  
|0x40013004|1073819652|DTS_MSG_CANTDELAYLOADDLL|O módulo %1 não pode carregar a DLL %2 para o ponto de entrada de chamada %3 devido ao erro %4. O produto precisa que o DLL seja executado, mas o DLL não foi encontrado no caminho.|  
|0x40013005|1073819653|DTS_MSG_CANTDELAYLOADDLLFUNCTION|O módulo %1 carregou a DLL %2, mas não pode encontrar o ponto de entrada %3 devido ao erro %4. O DLL nomeado não foi encontrado no caminho, e o produto necessita da execução do DLL.|  
|0x40103100|1074802944|DTS_MSG_EVENTLOGENTRY|Nome do evento: %1<br /><br /> Mensagem: %9<br /><br /> Operador: %2<br /><br /> Nome da Origem: %3<br /><br /> ID da Origem: %4<br /><br /> ID de Execução: %5<br /><br /> Hora de Início: %6<br /><br /> Hora de Término: %7<br /><br /> Código de Dados: %8|  
|0x40103101|1074802945|DTS_MSG_EVENTLOGENTRY_PREEXECUTE|Nome do evento: %1<br /><br /> Mensagem: %9<br /><br /> Operador: %2<br /><br /> Nome da Origem: %3<br /><br /> ID da Origem: %4<br /><br /> ID de Execução: %5<br /><br /> Hora de Início: %6<br /><br /> Hora de Término: %7<br /><br /> Código de Dados: %8|  
|0x40103102|1074802946|DTS_MSG_EVENTLOGENTRY_POSTEXECUTE|Nome do evento: %1<br /><br /> Mensagem: %9<br /><br /> Operador: %2<br /><br /> Nome da Origem: %3<br /><br /> ID da Origem: %4<br /><br /> ID de Execução: %5<br /><br /> Hora de Início: %6<br /><br /> Hora de Término: %7<br /><br /> Código de Dados: %8|  
|0x40103103|1074802947|DTS_MSG_EVENTLOGENTRY_PREVALIDATE|Nome do evento: %1<br /><br /> Mensagem: %9<br /><br /> Operador: %2<br /><br /> Nome da Origem: %3<br /><br /> ID da Origem: %4<br /><br /> ID de Execução: %5<br /><br /> Hora de Início: %6<br /><br /> Hora de Término: %7<br /><br /> Código de Dados: %8|  
|0x40103104|1074802948|DTS_MSG_EVENTLOGENTRY_POSTVALIDATE|Nome do evento: %1<br /><br /> Mensagem: %9<br /><br /> Operador: %2<br /><br /> Nome da Origem: %3<br /><br /> ID da Origem: %4<br /><br /> ID de Execução: %5<br /><br /> Hora de Início: %6<br /><br /> Hora de Término: %7<br /><br /> Código de Dados: %8|  
|0x40103105|1074802949|DTS_MSG_EVENTLOGENTRY_WARNING|Nome do evento: %1<br /><br /> Mensagem: %9<br /><br /> Operador: %2<br /><br /> Nome da Origem: %3<br /><br /> ID da Origem: %4<br /><br /> ID de Execução: %5<br /><br /> Hora de Início: %6<br /><br /> Hora de Término: %7<br /><br /> Código de Dados: %8|  
|0x40103106|1074802950|DTS_MSG_EVENTLOGENTRY_ERROR|Nome do evento: %1<br /><br /> Mensagem: %9<br /><br /> Operador: %2<br /><br /> Nome da Origem: %3<br /><br /> ID da Origem: %4<br /><br /> ID de Execução: %5<br /><br /> Hora de Início: %6<br /><br /> Hora de Término: %7<br /><br /> Código de Dados: %8|  
|0x40103107|1074802951|DTS_MSG_EVENTLOGENTRY_TASKFAILED|Nome do evento: %1<br /><br /> Mensagem: %9<br /><br /> Operador: %2<br /><br /> Nome da Origem: %3<br /><br /> ID da Origem: %4<br /><br /> ID de Execução: %5<br /><br /> Hora de Início: %6<br /><br /> Hora de Término: %7<br /><br /> Código de Dados: %8|  
|0x40103108|1074802952|DTS_MSG_EVENTLOGENTRY_PROGRESS|Nome do evento: %1<br /><br /> Mensagem: %9<br /><br /> Operador: %2<br /><br /> Nome da Origem: %3<br /><br /> ID da Origem: %4<br /><br /> ID de Execução: %5<br /><br /> Hora de Início: %6<br /><br /> Hora de Término: %7<br /><br /> Código de Dados: %8|  
|0x40103109|1074802953|DTS_MSG_EVENTLOGENTRY_EXECSTATCHANGE|Nome do evento: %1<br /><br /> Mensagem: %9<br /><br /> Operador: %2<br /><br /> Nome da Origem: %3<br /><br /> ID da Origem: %4<br /><br /> ID de Execução: %5<br /><br /> Hora de Início: %6<br /><br /> Hora de Término: %7<br /><br /> Código de Dados: %8|  
|0x4010310A|1074802954|DTS_MSG_EVENTLOGENTRY_VARVALCHANGE|Nome do evento: %1<br /><br /> Mensagem: %9<br /><br /> Operador: %2<br /><br /> Nome da Origem: %3<br /><br /> ID da Origem: %4<br /><br /> ID de Execução: %5<br /><br /> Hora de Início: %6<br /><br /> Hora de Término: %7<br /><br /> Código de Dados: %8|  
|0x4010310B|1074802955|DTS_MSG_EVENTLOGENTRY_CUSTOMEVENT|Nome do evento: %1<br /><br /> Mensagem: %9<br /><br /> Operador: %2<br /><br /> Nome da Origem: %3<br /><br /> ID da Origem: %4<br /><br /> ID de Execução: %5<br /><br /> Hora de Início: %6<br /><br /> Hora de Término: %7<br /><br /> Código de Dados: %8|  
|0x4010310C|1074802956|DTS_MSG_EVENTLOGENTRY_PACKAGESTART|Nome do evento: %1<br /><br /> Mensagem: %9<br /><br /> Operador: %2<br /><br /> Nome da Origem: %3<br /><br /> ID da Origem: %4<br /><br /> ID de Execução: %5<br /><br /> Hora de Início: %6<br /><br /> Hora de Término: %7<br /><br /> Código de Dados: %8|  
|0x4010310D|1074802957|DTS_MSG_EVENTLOGENTRY_PACKAGEEND|Nome do evento: %1<br /><br /> Mensagem: %9<br /><br /> Operador: %2<br /><br /> Nome da Origem: %3<br /><br /> ID da Origem: %4<br /><br /> ID de Execução: %5<br /><br /> Hora de Início: %6<br /><br /> Hora de Término: %7<br /><br /> Código de Dados: %8|  
|0x4010310E|1074802958|DTS_MSG_EVENTLOGENTRY_INFORMATION|Nome do evento: %1<br /><br /> Mensagem: %9<br /><br /> Operador: %2<br /><br /> Nome da Origem: %3<br /><br /> ID da Origem: %4<br /><br /> ID de Execução: %5<br /><br /> Hora de Início: %6<br /><br /> Hora de Término: %7<br /><br /> Código de Dados: %8|  
  
##  <a name="msgSuccess"></a> Mensagens de êxito  
 Os nomes simbólicos das mensagens de êxito do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] começam com **DTS_S_** .  
  
|Código hexadecimal|Código decimal|Nome simbólico|Descrição|  
|----------------------|------------------|-------------------|-----------------|  
|0x40003|262147|DTS_S_NULLDATA|O valor é NULL.|  
|0x40005|262149|DTS_S_TRUNCATED|O valor da cadeia de caracteres foi truncado. O buffer recebeu uma cadeia de caracteres muito longa para a coluna e a truncou.|  
|0x200001|2097153|DTS_S_EXPREVALTRUNCATIONOCCURRED|Ocorreu um truncamento durante a avaliação da expressão. O truncamento ocorreu durante a avaliação, o que pode incluir qualquer momento da etapa intermediária.|  
  
##  <a name="msgPipeline"></a> Mensagens de erro do componente de fluxo de dados  
 Os nomes simbólicos das mensagens de erro do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] começam com **DTSBC_E_** , em que "BC" refere-se à classe base nativa da qual é derivada a maioria dos componentes de fluxo de dados da Microsoft.  
  
|Código hexadecimal|Código decimal|Nome simbólico|Descrição|  
|----------------------|------------------|-------------------|-----------------|  
|0xC8000002|-939524094|DTSBC_E_INCORRECTEXACTNUMBEROFTOTALOUTPUTS|O número total de saídas e saídas de erro, %1!lu!, está incorreto. Deve haver exatamente %2!lu!.|  
|0xC8000003|-939524093|DTSBC_E_FAILEDTOGETOUTPUTBYINDEX|Não é possível recuperar a saída com o índice %1!lu!.|  
|0xC8000005|-939524091|DTSBC_E_INCORRECTEXACTNUMBEROFERROROUTPUTS|O número de saídas de erro, %1!lu!, está incorreto. Deve haver exatamente %2!lu!.|  
|0xC8000006|-939524090|DTSBC_E_INVALIDVALIDATIONSTATUSVALUE|Valor de status de validação incorreto, "%1!lu! ".  Deve ser um dos valores encontrados na enumeração DTSValidationStatus.|  
|0xC8000007|-939524089|DTSBC_E_INPUTHASNOOUTPUT|A entrada "%1!lu!" não tem saída síncrona.|  
|0xC8000008|-939524088|DTSBC_E_INPUTHASNOERROROUTPUT|A entrada "%1!lu!" não tem saída de erro síncrona.|  
|0xC8000009|-939524087|DTSBC_E_INVALIDHTPIVALUE|O valor de HowToProcessInput, %1!lu!, não é válido. Deve ser um dos valores encontrados a partir da enumeração HowToProcessInput.|  
|0xC800000A|-939524086|DTSBC_E_FAILEDTOGETCOLINFO|Falha ao obter informações para a linha "%1!ld!", coluna "%2!ld!" do buffer.  O código de erro retornado foi 0x%3!8.8X!.|  
|0xC800000B|-939524085|DTSBC_E_FAILEDTOSETCOLINFO|Falha ao definir informações para a linha "%1!ld!", coluna "%2!ld!" no buffer.  O código de erro retornado foi 0x%3!8.8X!.|  
|0xC800000C|-939524084|DTSBC_E_INVALIDPROPERTY|A propriedade "%1" não é válida.|  
|0xC800000D|-939524083|DTSBC_E_PROPERTYNOTFOUND|A propriedade "%1" não foi encontrada.|  
|0xC8000010|-939524080|DTSBC_E_READONLYPROPERTY|Erro durante a atribuição de um valor à propriedade "%1" somente leitura.|  
|0xC8000011|-939524079|DTSBC_E_CANTINSERTOUTPUTCOLUMN|O %1 não permite a inserção de colunas de saída.|  
|0xC8000012|-939524078|DTSBC_E_OUTPUTCOLUMNSMETADATAMISMATCH|Os metadados das colunas de saída não correspondem aos metadados das colunas de entrada associadas.  Os metadados das colunas de saída serão atualizados.|  
|0xC8000013|-939524077|DTSBC_E_OUTPUTCOLUMNSMISSING|Existem colunas de entrada sem colunas de saída associadas. Os metadados das colunas de saída serão adicionados.|  
|0xC8000014|-939524076|DTSBC_E_TOOMANYOUTPUTCOLUMNS|Existem colunas de saída sem colunas de entrada associadas. As colunas de saída serão removidas.|  
|0xC8000015|-939524075|DTSBC_E_OUTPUTCOLUMNSMETADATAMISMATCHUNMAP|Os metadados das colunas de saída não correspondem aos metadados das colunas de entrada associadas.  As colunas de entrada serão desmapeadas.|  
|0xC8000016|-939524074|DTSBC_E_UNMAPINPUTCOLUMNS|Existem colunas de entrada sem colunas de saída associadas. As colunas de entrada serão desmapeadas.|  
|0xC8000017|-939524073|DTSBC_E_MULTIPLEINCOLSTOOUTCOL|Existe uma coluna de entrada associada a uma coluna de saída que já está associada a outra coluna de entrada na mesma entrada.|  
|0xC8000018|-939524072|DTSBC_E_CANTINSERTEXTERNALMETADATACOLUMN|O %1 não permite a inserção de colunas de metadados externos.|  
  
  
