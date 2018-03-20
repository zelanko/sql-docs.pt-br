---
title: Usando tipos de dados XML | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|features
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- IRowsetChange interface
- IRowsetUpdate interface
- data access [SQL Server Native Client], xml data type
- SQL Server Native Client OLE DB schema rowsets
- PROVIDER_TYPES rowset
- IColumnsInfo interface
- IRowsetFind interface
- IColumnsRowset interface
- PROCEDURE_PARAMETERS rowset
- SQLNCLI, XML
- xml data type [SQL Server], SQL Server Native Client
- SQL Server Native Client, XML
- IRowset interface
- ISequentialStream interface
- ISSCommandWithParameters interface
- SS_XMLSCHEMA rowset
- SQL Server Native Client OLE DB interfaces
- XML [SQL Server], SQL Server Native Client
- COLUMNS rowset
ms.assetid: a7af5b72-c5c2-418d-a636-ae4ac6270ee5
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5e6532d74b6a1a3e1859cb9fb768dcc5816c9b7a
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2018
---
# <a name="using-xml-data-types"></a>Usando tipos de dados XML
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]introduziu um **xml** tipo de dados que permite armazenar documentos XML e fragmentos em um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] banco de dados. O **xml** tipo de dados é um tipo de dados internos em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]e é em algumas semelhanças com outros tipos internos, como **int** e **varchar**. Como com outros tipos internos, você pode usar o **xml** tipo de dados como um tipo de coluna ao criar uma tabela; como um tipo de variável, um tipo de parâmetro ou um tipo de retorno de função; ou em funções CAST e CONVERT.  
  
## <a name="programming-considerations"></a>Considerações sobre programação  
 O XML pode ser autodescritivo no sentido de que pode opcionalmente incluir um cabeçalho de XML que especifica a codificação do documento, por exemplo:  
  
 `<?xml version="1.0" encoding="windows-1252"?><doc/>`  
  
 O padrão XML descreve como um processador XML pode detectar a codificação usada para um documento examinando os primeiros bytes desse documento. Há riscos de a codificação especificada pelo aplicativo entrar em conflito com a especificada pelo documento. No caso de documentos passados como parâmetros associados, o XML é tratado como dados binários pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], por isso nenhuma conversão é feita e o analisador XML pode usar a codificação especificada no documento sem problemas. Entretanto, no caso de dados XML associados como WSTR, o aplicativo precisa garantir que o documento está codificado como Unicode. Assim, talvez seja necessário carregar o documento em um DOM, alterar a codificação para Unicode e serializar o documento. Senão, poderão ocorrer conversões de dados, gerando XML inválido ou corrompido.  
  
 Também há risco de conflitos quando o XML é especificado em literais. Por exemplo, as expressões a seguir são inválidas:  
  
 `INSERT INTO xmltable(xmlcol) VALUES('<?xml version="1.0" encoding="UTF-16"?><doc/>')`  
  
 `INSERT INTO xmltable(xmlcol) VALUES(N'<?xml version="1.0" encoding="UTF-8"?><doc/>')`  
  
## <a name="sql-server-native-client-ole-db-provider"></a>Provedor OLE DB do SQL Server Native Client  
 DBTYPE_XML é um novo tipo de dados específico ao XML no provedor do OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Além disso, é possível acessar dados XML pelos tipos de OLE DB existentes DBTYPE_BYTES, DBTYPE_WSTR, DBTYPE_BSTR, DBTYPE_XML, DBTYPE_STR, DBTYPE_VARIANT e DBTYPE_IUNKNOWN. Os dados armazenados em colunas de tipo XML podem ser recuperados de uma coluna em um conjunto de linhas do provedor do OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client nos formatos a seguir:  
  
-   Uma cadeia de caracteres de texto  
  
-   Um **ISequentialStream**  
  
> [!NOTE]  
>  O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client não inclui um leitor SAX, mas o **ISequentialStream** pode ser passado facilmente para objetos SAX e DOM em MSXML.  
  
 **ISequentialStream** deve ser usado para recuperação de documentos XML extensos. As mesmas técnicas usadas para outros tipos de valor extenso também se aplicam ao XML. Para obter mais informações, consulte [usando tipos de valor grande](../../../relational-databases/native-client/features/using-large-value-types.md).  
  
 Dados armazenados em colunas do tipo XML em um conjunto de linhas também podem ser recuperados, inseridos ou atualizados por um aplicativo por meio das interfaces comuns como **IRow:: Getcolumns**, **irowchange::**, e **ICommand:: execute**. De maneira semelhante ao caso da recuperação, um programa aplicativo pode passar uma cadeia de caracteres do texto ou um **ISequentialStream** para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client.  
  
> [!NOTE]  
>  Para enviar dados XML em formato de cadeia de caracteres por meio de **ISequentialStream** interface, você deve obter **ISequentialStream** especificando DBTYPE_IUNKNOWN e definir seu *pObject* argumento nulo na associação.  
  
 Quando os dados XML recuperados estão truncados porque o buffer de consumidor é muito pequeno, a extensão poderá ser retornada como 0xffffffff, o que significará que ela é desconhecida. Isso é condizente com sua implementação como tipo de dados transmitidos ao cliente sem enviar as informações de extensão antes dos dados reais. Em alguns casos o comprimento real pode ser retornado quando o provedor de buffer do valor inteiro, como **IRowset:: GetData** e onde ocorre a conversão de dados.  
  
 Os dados XML enviados ao SQL Server são tratados como dados binários pelo servidor. Isso impede a ocorrência de qualquer conversão e permite que o analisador XML autodetecte a codificação de XML. Além disso, permite que uma variedade mais ampla de documentos XML (por exemplo, aqueles codificados em UTF-8) seja aceita como entrada no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Se o XML de entrada estiver associado como DBTYPE_WSTR, o aplicativo deverá garantir que já tem codificação Unicode para evitar qualquer possibilidade de corrompimento por conversões de dados indesejadas.  
  
### <a name="data-bindings-and-coercions"></a>Coerções e associações de dados  
 A tabela a seguir descreve a associação e coerção que ocorrem ao usar os listados tipos de dados com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **xml** tipo de dados.  
  
|Tipo de dados|Para servidor<br /><br /> **XML**|Para servidor<br /><br /> **Não XML**|Do servidor<br /><br /> **XML**|Do servidor<br /><br /> **Não XML**|  
|---------------|---------------------------|--------------------------------|-----------------------------|----------------------------------|  
|DBTYPE_XML|Passar<sup>6,7</sup>|Erro<sup>1</sup>|OKEY<sup>11, 6</sup>|Erro<sup>8</sup>|  
|DBTYPE_BYTES|Passar<sup>6,7</sup>|N/A<sup>2</sup>|OKEY <sup>11, 6</sup>|N/A <sup>2</sup>|  
|DBTYPE_WSTR|Passar<sup>6,10</sup>|N/A <sup>2</sup>|OKEY<sup>4, 6, 12</sup>|N/A <sup>2</sup>|  
|DBTYPE_BSTR|Passar<sup>6,10</sup>|N/A <sup>2</sup>|OK <sup>3</sup>|N/A <sup>2</sup>|  
|DBTYPE_STR|OKEY<sup>6, 9, 10</sup>|N/A <sup>2</sup>|OKEY<sup>5, 6, 12</sup>|N/A <sup>2</sup>|  
|DBTYPE_IUNKNOWN|Fluxo de bytes via **ISequentialStream**<sup>7</sup>|N/A <sup>2</sup>|Fluxo de bytes via **ISequentialStream**<sup>11</sup>|N/A <sup>2</sup>|  
|DBTYPE_VARIANT (VT_UI1 &#124; VT_ARRAY)|Passar<sup>6,7</sup>|N/A <sup>2</sup>|N/A|N/A <sup>2</sup>|  
|DBTYPE_VARIANT (VT_BSTR)|Passar<sup>6,10</sup>|N/A <sup>2</sup>|OK<sup>3</sup>|N/A <sup>2</sup>|  
  
 <sup>1</sup>se o tipo de um servidor diferente de DBTYPE_XML for especificado com **ICommandWithParameters:: SetParameterInfo** e o tipo de acessador for DBTYPE_XML, ocorrerá um erro quando a instrução é executada (DB_E_ERRORSOCCURRED, o status do parâmetro é DBSTATUS_E_BADACCESSOR); caso contrário, os dados são enviados ao servidor, mas o servidor retornará um erro indicando que não há nenhuma conversão implícita de XML para o tipo de dados do parâmetro.  
  
 <sup>2</sup>além do escopo deste tópico.  
  
 <sup>3</sup>formato é UTF-16, nenhuma marca de ordem de bye (BOM), nenhuma especificação de codificação, não há terminação nula.  
  
 <sup>4</sup>formato não é UTF-16, não há BOM, nenhuma especificação de codificação, terminação nula.  
  
 <sup>5</sup>formato é caracteres multibyte codificados em página de código de cliente com terminador nulo. A conversão a partir do Unicode fornecido pelo servidor pode causar corrompimento dos dados, por isso essa associação é altamente desestimulada.  
  
 <sup>6</sup>BY_REF pode ser usado.  
  
 <sup>7</sup>dados UTF-16 devem começar com um BOM. Senão, a codificação poderá não ser reconhecida corretamente pelo servidor.  
  
 <sup>8</sup>validação pode acontecer no momento do acessador de criação ou no tempo de busca. O erro é DB_E_ERRORSOCCURRED; status da associação definido como DBBINDSTATUS_UNSUPPORTEDCONVERSION.  
  
 <sup>9</sup>dados são convertidos em Unicode usando a página de código do cliente antes de serem enviados ao servidor. Se a codificação de documento não corresponder à página de código de cliente, poderá haver corrompimento dos dados, por isso a associação é altamente desestimulada.  
  
 <sup>10</sup>um BOM sempre é adicionado aos dados enviados ao servidor. Se os dados já forem iniciados com um BOM, isso resultará em dois BOMs no início do buffer. O servidor usa o primeiro BOM para reconhecer a codificação como UTF-16 e, em seguida, descarta-lo. O segundo BOM é interpretado como um caractere de espaço incondicional de largura zero.  
  
 <sup>11</sup>formato é UTF-16, não há especificação de codificação, um BOM é adicionado aos dados recebidos do servidor. Se uma cadeia de caracteres vazia é retornada pelo servidor, um BOM ainda será retornado para o aplicativo. Se o tamanho do buffer é um número ímpar de bytes, os dados são truncados corretamente. Se o valor inteiro for retornado em partes, elas poderão ser concatenadas para reconstituir o valor correto.  
  
 <sup>12</sup>se o tamanho do buffer é menor que dois caracteres – ou seja, não há espaço suficiente para terminação nula – é reportado um erro de estouro.  
  
> [!NOTE]  
>  Nenhum dado é retornado para valores de XML NULL.  
  
 O padrão XML exige que o XML codificado em UTF-16 seja iniciado com um código de caractere UTF-16 com BOM 0xFEFF. Ao trabalhar com associações WSTR e BSTR, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client não exige ou adiciona um BOM porque a codificação é insinuada pela associação. Ao trabalhar com associações BYTES, XML ou IUNKNOWN, a intenção é proporcionar simplicidade ao lidar com outros processadores XML e sistemas de armazenamento. Nesse caso, um BOM deve estar presente com o XML codificado em UTF-16, e o aplicativo não precisa verificar a codificação real, porque a maioria dos processadores XML (incluindo o SQL Server) deduz a codificação inspecionando os primeiros bytes do valor. Dados XML recebidos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client usando BYTES, XML ou IUNKNOWN as associações são sempre codificados em UTF-16 com um BOM e sem uma declaração de codificação inserida.  
  
 Conversões de dados fornecidas por serviços principais do OLE DB (**IDataConvert**) não são aplicáveis a DBTYPE_XML.  
  
 A validação ocorre quando os dados são enviados para o servidor. As alterações de codificação e validação do lado do cliente devem ser manipuladas pelo aplicativo, e é altamente recomendável que você não processe os dados XML diretamente, mas sim use um leitor DOM ou SAX para processá-los.  
  
 DBTYPE_NULL e DBTYPE_EMPTY podem ser associados a parâmetros de entrada, mas não a parâmetros ou resultados de saída. Quando eles são associados para parâmetros de entrada, o status precisa ser definido como DBSTATUS_S_ISNULL ou DBSTATUS_S_DEFAULT.  
  
 DBTYPE_XML pode ser convertido em DBTYPE_EMPTY e DBTYPE_NULL, sendo que DBTYPE_EMPTY pode ser convertido em DBTYPE_XML, mas DBTYPE_NULL não pode ser convertido em DBTYPE_XML. Isso é condizente com DBTYPE_WSTR.  
  
 DBTYPE_IUNKNOWN é uma associação com suporte (conforme mostrado na tabela anterior), mas não há nenhuma conversão entre DBTYPE_XML e DBTYPE_IUNKNOWN. DBTYPE_IUNKNOWN não pode ser usado com DBTYPE_BYREF.  
  
### <a name="ole-db-rowset-additions-and-changes"></a>Adições e alterações do conjunto de linhas do OLE DB  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client adiciona novos valores ou alterações a muitos dos principais conjuntos de linhas de esquema OLE DB.  
  
#### <a name="the-columns-and-procedureparameters-schema-rowsets"></a>Os conjuntos de linhas de esquema de COLUMNS e PROCEDURE_PARAMETERS  
 Entre as adições aos conjuntos de linhas de esquema de COLUMNS e PROCEDURE_PARAMETERS estão as colunas a seguir.  
  
|Nome da coluna|Tipo|Description|  
|-----------------|----------|-----------------|  
|SS_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|O nome de um catálogo no qual uma coleção de esquema XML é definida. NULL para uma coluna não XML ou coluna de XML não digitada.|  
|SS_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|O nome de um esquema no qual uma coleção de esquema XML é definida. NULL para uma coluna não XML ou coluna de XML não digitada.|  
|SS_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|O nome da coleção de esquemas XML. NULL para uma coluna não XML ou coluna de XML não digitada.|  
  
#### <a name="the-providertypes-schema-rowset"></a>O conjunto de linhas de esquema de PROVIDER_TYPES  
 O conjunto de linhas de esquema PROVIDER_TYPES, o valor COLUMN_SIZE é 0 para o **xml** tipo de dados, e o DATA_TYPE é DBTYPE_XML.  
  
#### <a name="the-ssxmlschema-schema-rowset"></a>O conjunto de linhas de esquema de SS_XMLSCHEMA  
 Um novo conjunto de linhas de esquema de SS_XMLSCHEMA é introduzido para que os clientes recuperem as informações de esquema XML. O conjunto de linhas de SS_XMLSCHEMA contém as colunas a seguir.  
  
|Nome da coluna|Tipo|Description|  
|-----------------|----------|-----------------|  
|SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|O catálogo ao qual pertence uma coleção XML.|  
|SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|O esquema ao qual pertence uma coleção XML.|  
|SCHEMACOLLECTIONNAME|DBTYPE_WSTR|O nome de uma coleção de esquemas XML para colunas de XML digitadas; ou NULL em caso contrário.|  
|TARGETNAMESPACEURI|DBTYPE_WSTR|O espaço de nome de destino de um esquema XML.|  
|SCHEMACONTENT|DBTYPE_WSTR|O conteúdo de esquema XML.|  
  
 O escopo de cada esquema XML é definido por nome de catálogo, de esquema e de coleção de esquema, além de URI (identificador de recurso uniforme) de espaço de nome de destino. Além disso, também é definido um novo GUID com o nome DBSCHEMA_XML_COLLECTIONS. O número de restrições e colunas restringidas para o conjunto de linhas de esquema de SS_XMLSCHEMA é definido da seguinte maneira.  
  
|GUID|Número de restrições|Colunas restringidas|  
|----------|----------------------------|------------------------|  
|DBSCHEMA_XML_COLLECTIONS|4|SCHEMACOLLECTION_CATALOGNAME<br /><br /> SCHEMACOLLECTION_SCHEMANAME<br /><br /> SCHEMACOLLECTIONNAME<br /><br /> TARGETNAMESPACEURI|  
  
### <a name="ole-db-property-set-additions-and-changes"></a>Adições e alterações do conjunto de propriedades do OLE DB  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client adiciona novos valores ou alterações a muitos dos principais propriedade OLE DB conjuntos.  
  
#### <a name="the-dbpropsetsqlserverparameter-property-set"></a>O conjunto de propriedades de DBPROPSET_SQLSERVERPARAMETER  
 Para oferecer suporte a **xml** tipo de dados por meio de OLE DB, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client implementa o novo conjunto de propriedades DBPROPSET_SQLSERVERPARAMETER, que contém os seguintes valores.  
  
|Nome|Tipo|Description|  
|----------|----------|-----------------|  
|SSPROP_PARAM_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|O nome de um catálogo (banco de dados) no qual é definida uma coleção de esquemas XML. Uma parte do identificador de nome de três partes SQL.|  
|SSPROP_PARAM_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|O nome de um esquema XML em uma coleção de esquemas. Uma parte do identificador de nome de três partes SQL.|  
|SSPROP_PARAM_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|O nome da coleção de esquemas XML no catálogo. Uma parte do identificador de nome de três partes SQL.|  
  
#### <a name="the-dbpropsetsqlservercolumn-property-set"></a>O conjunto de propriedades de DBPROPSET_SQLSERVERCOLUMN  
 Suporte à criação de tabelas de **ITableDefinition** interface, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client adiciona três colunas novas ao conjunto de propriedades DBPROPSET_SQLSERVERCOLUMN.  
  
|Nome|Tipo|Description|  
|----------|----------|-----------------|  
|SSPROP_COL_XML_SCHEMACOLLECTION_CATALOGNAME|VT_BSTR|Para colunas de XML digitadas, esta propriedade é uma cadeia de caracteres que especifica o nome do catálogo em que está armazenado o esquema XML. Para outros tipos de coluna, esta propriedade retorna uma cadeia de caracteres vazia.|  
|SSPROP_COL_XML_SCHEMACOLLECTION_SCHEMANAME|VT_BSTR|Para colunas de XML digitadas, esta propriedade é uma cadeia de caracteres que especifica o nome do esquema XML que define esta coluna.|  
|SSPROP_COL_XML_SCHEMACOLLECTIONNAME|VT_BSTR|Para colunas de XML digitadas, esta propriedade é uma cadeia de caracteres que especifica o nome da coleção de esquemas XML do esquema que define o valor.|  
  
 Assim como os valores de SSPROP_PARAM, todas essas propriedades são opcionais e o padrão é vazio. SSPROP_COL_XML_SCHEMACOLLECTION_CATALOGNAME e SSPROP_COL_XML_SCHEMACOLLECTION_SCHEMANAME só poderão ser especificados se SSPROP_COL_XML_SCHEMACOLLECTIONNAME for especificado. Na passagem do XML para o servidor, se esses valores forem incluídos, serão verificados quanto à existência (validade) com base no banco de dados atual, e os dados de instância serão verificados com base no esquema. Em todos os casos, para que sejam válidos eles ficam todos vazios ou todos preenchidos.  
  
### <a name="ole-db-interface-additions-and-changes"></a>Adições e alterações de interface do OLE DB  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client adiciona novos valores ou alterações a muitas das principais que interfaces OLE DB.  
  
#### <a name="the-isscommandwithparameters-interface"></a>A interface ISSCommandWithParameters  
 Para oferecer suporte a **xml** tipo de dados por meio de OLE DB, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client implementa um número de alterações, incluindo a adição do [ISSCommandWithParameters](../../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md) interface. Essa nova interface herda da interface OLE DB **ICommandWithParameters**. Além dos três métodos herdados de **ICommandWithParameters**; **GetParameterInfo**, **MapParameterNames**, e **SetParameterInfo**; **ISSCommandWithParameters** fornece o [GetParameterProperties](../../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-getparameterproperties-ole-db.md) e [SetParameterProperties](../../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md) métodos que são usados para identificar os tipos de dados específicos do servidor.  
  
> [!NOTE]  
>  O **ISSCommandWithParameters** interface também utiliza o SSPARAMPROPS nova estrutura.  
  
#### <a name="the-icolumnsrowset-interface"></a>A interface IColumnsRowset  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client adiciona as seguintes [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-colunas específicas ao conjunto de linhas retornado pelo **icolumnrowset:: Getcolumnsrowset** método. Estas colunas contêm o nome de três partes de uma coleção de esquemas XML. Para colunas não XML ou colunas de XML não digitadas, as três colunas assumem o valor padrão de NULL.  
  
|Nome da coluna|Tipo|Description|  
|-----------------|----------|-----------------|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|O catálogo ao qual pertence uma coleção de esquema XML;<br /><br /> NULL em caso contrário.|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|O esquema ao qual pertence uma coleção de esquemas XML. NULL em caso contrário.|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|O nome da coleção de esquemas XML para a coluna de XML digitada; ou NULL em caso contrário.|  
  
#### <a name="the-irowset-interface"></a>A interface IRowset  
 Uma instância XML em uma coluna XML é recuperada por meio de **IRowset:: GetData** método. Dependendo da associação especificada pelo cliente, uma instância de XML pode ser recuperada como DBTYPE_BSTR, DBTYPE_WSTR, DBTYPE_VARIANT, DBTYPE_XML, DBTYPE_STR, DBTYPE_BYTES ou como uma interface via DBTYPE_IUNKNOWN. Se o consumidor especificar DBTYPE_BSTR, DBTYPE_WSTR ou DBTYPE_VARIANT, o provedor converterá a instância de XML para o tipo solicitado pelo usuário e a colocará no local especificado na associação correspondente.  
  
 Se o consumidor especificar DBTYPE_IUNKNOWN e define o *pObject* argumento nulo ou conjuntos de *pObject* argumento como IID_ISequentialStream, o provedor retorna um **ISequentialStream** interface para o consumidor para que o consumidor pode transmitir os dados XML da coluna. **ISequentialStream** , em seguida, retorna os dados XML como um fluxo de caracteres Unicode.  
  
 Ao retornar um valor XML associado a DBTYPE_IUNKNOWN, o provedor informará um valor de tamanho de `sizeof (IUnknown *)`. Observe que esse procedimento é condizente com a abordagem adotada quando uma coluna é associada como DBTYPE_IUnknown ou DBTYPE_IDISPATCH e por DBTYPE_IUNKNOWN/ISequentialStream quando não é possível determinar o tamanho exato da coluna.  
  
#### <a name="the-irowsetchange-interface"></a>A interface IRowsetChange  
 Há duas maneiras de um consumidor atualizar uma instância de XML em uma coluna. A primeira é por meio do objeto de armazenamento **ISequentialStream** criado pelo provedor. O consumidor pode chamar o **ISequentialStream:: Write** método para atualizar diretamente a instância XML retornada pelo provedor.  
  
 A segunda abordagem é por meio de **IRowsetChange:: SetData** ou **IRowsetChange:: Insertrow** métodos. Nessa abordagem, uma instância de XML no buffer do consumidor pode ser especificada em uma associação de tipo DBTYPE_BSTR, DBTYPE_WSTR, DBTYPE_VARIANT, DBTYPE_XML ou DBTYPE_IUNKNOWN.  
  
 No caso de DBTYPE_BSTR, DBTYPE_WSTR ou DBTYPE_VARIANT, o provedor armazena a instância de XML que reside no buffer do consumidor na coluna adequada.  
  
 No caso de DBTYPE_IUNKNOWN/ISequentialStream, se o consumidor não especificar um objeto de armazenamento, o consumidor deve criar um **ISequentialStream** objeto com antecedência, associar o documento XML com o objeto e, em seguida, passar o objeto para o provedor por meio de **IRowsetChange:: SetData** método. O consumidor também pode criar um armazenamento de objeto, defina o argumento pObject como IID_ISequentialStream, criar um **ISequentialStream** de objeto e, em seguida, passar o **ISequentialStream** o objeto para o **IRowsetChange:: SetData** método. Em ambos os casos, o provedor pode recuperar o objeto XML por meio de **ISequentialStream** de objeto e inseri-lo em uma coluna adequada.  
  
#### <a name="the-irowsetupdate-interface"></a>A interface IRowsetUpdate  
 **IRowsetUpdate** interface fornece funcionalidade para atualizações atrasadas. Os dados disponíveis para os conjuntos de linhas não estarão disponíveis para outras transações até que o consumidor chama o **IRowsetUpdate: Update** método.  
  
#### <a name="the-irowsetfind-interface"></a>A interface IRowsetFind  
 O **irowsetfind:: Findnextrow** método não funciona com o **xml** tipo de dados. Quando **irowsetfind:: Findnextrow** é chamado e o *hAccessor* argumento especifica uma coluna de DBTYPE_XML, é retornado DB_E_BADBINDINFO. Isso ocorre independentemente do tipo de coluna que está sendo pesquisada. Para qualquer outro tipo de associação, o **FindNextRow** falha com DB_E_BADCOMPAREOP se a coluna a ser pesquisada for o **xml** tipo de dados.  
  
## <a name="sql-server-native-client-odbc-driver"></a>Driver ODBC do SQL Server Native Client  
 No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client, inúmeras alterações foram feitas para várias funções para oferecer suporte a **xml** tipo de dados.  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 O [SQLColAttribute](../../../relational-databases/native-client-odbc-api/sqlcolattribute.md) função tem três novos identificadores de campo, incluindo SQL_CA_SS_XML_SCHEMACOLLECTION_CATALOG_NAME, SQL_CA_SS_XML_SCHEMACOLLECTION_SCHEMA_NAME e SQL_CA_SS xml_schemacollection_name.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client informa SQL_SS_LENGTH_UNLIMITED para as colunas de colunas de SQL_DESC_DISPLAY_SIZE e SQL_DESC_LENGTH.  
  
### <a name="sqlcolumns"></a>SQLColumns  
 O [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md) função tem três colunas novas, incluindo SS_XML_SCHEMACOLLECTION_CATALOG_NAME, SS_XML_SCHEMACOLLECTION_SCHEMA_NAME e SS_XML_SCHEMACOLLECTION_NAME. A coluna TYPE_NAME existente é usada para indicar o nome do tipo de XM, e o DATA_TYPE para um parâmetro ou coluna de tipo de XML é SQL_SS_XML.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client informa SQL_SS_LENGTH_UNLIMITED para os valores de COLUMN_SIZE e CHAR_OCTET_LENGTH.  
  
### <a name="sqldescribecol"></a>SQLDescribeCol  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client informa SQL_SS_LENGTH_UNLIMITED quando o tamanho da coluna não pode ser determinado no [SQLDescribeCol](../../../relational-databases/native-client-odbc-api/sqldescribecol.md) função.  
  
### <a name="sqlgettypeinfo"></a>SQLGetTypeInfo  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client informa SQL_SS_LENGTH_UNLIMITED como o COLUMN_SIZE máximo para o **xml** no tipo de dados de [SQLGetTypeInfo](../../../relational-databases/native-client-odbc-api/sqlgettypeinfo.md) função.  
  
### <a name="sqlprocedurecolumns"></a>SQLProcedureColumns  
 O [SQLProcedureColumns](../../../relational-databases/native-client-odbc-api/sqlprocedurecolumns.md) função tem as mesmas adições de coluna como o **SQLColumns** função.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client informa SQL_SS_LENGTH_UNLIMITED como o COLUMN_SIZE máximo para o **xml** tipo de dados.  
  
### <a name="supported-conversions"></a>Conversões com suporte  
 Ao converter de tipos de dados SQL para C, é possível converter SQL_C_WCHAR, SQL_C_BINARY e SQL_C_CHAR em SQL_SS_XML, com as estipulações a seguir:  
  
-   SQL_C_WCHAR: o formato é UTF-16, não há BOM, há terminação nula.  
  
-   SQL_C_BINARY: o formato é UTF-16, não há terminação nula. Um BOM é adicionado aos dados recebidos do servidor. Se uma cadeia de caracteres vazia for retornada pelo servidor, um BOM ainda será retornado para o aplicativo. Se a extensão do buffer for um número ímpar de bytes, os dados serão truncados corretamente. Se o valor inteiro for retornado em partes, elas poderão ser concatenadas para reconstituir o valor correto.  
  
-   SQL_C_CHAR: o formato consiste em caracteres multibyte codificados em página de código de cliente com terminação nula. A conversão a partir do UTF-16 fornecido pelo servidor pode causar corrompimento dos dados, por isso essa associação é altamente desestimulada.  
  
 Ao converter de tipos de dados C para SQL, é possível converter SQL_C_WCHAR, SQL_C_BINARY e SQL_C_CHAR em SQL_SS_XML, com as estipulações a seguir:  
  
-   SQL_C_WCHAR: um BOM sempre é adicionado aos dados enviados para o servidor. Se os dados já forem iniciados com um BOM, isso resultará em dois BOMs no início do buffer. O servidor usa o primeiro BOM para reconhecer a codificação como UTF-16 e então o descarta. O segundo BOM é interpretado como um caractere de espaço incondicional de largura zero.  
  
-   SQL_C_BINARY: nenhuma conversão é executada e os dados são passados para o servidor "no estado atual". Os dados UTF-16 precisam ser iniciados com um BOM; senão, a codificação poderá não ser reconhecida corretamente pelo servidor.  
  
-   SQL_C_CHAR: os dados são convertidos em UTF-16 no cliente e enviados para o servidor da mesma maneira que SQL_C_WCHAR (inclusive a adição de um BOM). Se o XML não for codificado na página de código de cliente, isso poderá causar corrompimento dos dados.  
  
 O padrão XML exige que o XML codificado em UTF-16 seja iniciado com um código de caractere UTF-16 com BOM 0xFEFF. Ao trabalhar com uma associação SQL_C_BINARY, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client não exige ou adiciona um BOM, porque a codificação é insinuada pela associação. A intenção é proporcionar simplicidade ao lidar com outros processadores XML e sistemas de armazenamento. Nesse caso, um BOM deve estar presente com o XML codificado em UTF-16, e o aplicativo não precisa verificar a codificação real, porque a maioria dos processadores XML (incluindo o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]) deduz a codificação inspecionando os primeiros bytes do valor. Dados XML recebidos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client usando SQL_C_BINARY associações sempre são codificados em UTF-16 com um BOM e sem uma declaração de codificação inserida.  
  
## <a name="see-also"></a>Consulte também  
 [Recursos do SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [ISSCommandWithParameters &#40; OLE DB &#41;](../../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
