---
description: Usando tipos de dados XML em SQL Server clientes nativos
title: Usar tipos de dados XML | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 76b24491df72773fb45b0513720151ed9a9c6585
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97461957"
---
# <a name="using-xml-data-types-in-sql-server-native-clients"></a>Usando tipos de dados XML em SQL Server clientes nativos
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  O [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] introduziu um tipo de dados **xml** que permite armazenar documentos e fragmentos XML em um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O tipo de dados **xml** é interno no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e tem algumas semelhanças com outros tipos internos, como **int** e **varchar**. Assim como ocorre em outros tipos internos, você pode usar o tipo de dados **xml** como um tipo de coluna ao criar uma tabela; como um tipo de variável, de parâmetro ou de retorno de função; ou em funções CAST e CONVERT.  
  
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
>  O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo não inclui um leitor SAX, mas o **ISequentialStream** pode ser facilmente passado para objetos sax e dom no MSXML.  
  
 **ISequentialStream** deve ser usado para recuperação de documentos XML grandes. As mesmas técnicas usadas para outros tipos de valor extenso também se aplicam ao XML. Para obter mais informações, confira [Usar tipos de valor grande](../../../relational-databases/native-client/features/using-large-value-types.md).  
  
 Os dados armazenados em colunas do tipo XML em um conjunto de linhas também podem ser recuperados, inseridos ou atualizados por um aplicativo por meio das interfaces comuns como **IRow::GetColumns**, **IRowChange::SetColumns** e **ICommand::Execute**. Da mesma forma que no caso de recuperação, um programa de aplicativo pode passar uma cadeia de caracteres de texto ou um **ISequentialStream** para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo.  
  
> [!NOTE]  
>  Para enviar dados XML em formato de cadeia de caracteres pela interface **ISequentialStream**, você precisa obter o **ISequentialStream** especificando DBTYPE_IUNKNOWN e definir seu argumento *pObject* como nulo na associação.  
  
 Quando os dados XML recuperados estão truncados porque o buffer de consumidor é muito pequeno, a extensão poderá ser retornada como 0xffffffff, o que significará que ela é desconhecida. Isso é condizente com sua implementação como tipo de dados transmitidos ao cliente sem enviar as informações de extensão antes dos dados reais. Em alguns casos, o comprimento real pode ser retornado quando o provedor armazena em buffer o valor inteiro, como **IRowset:: GetData** e onde a conversão de dados é executada.  
  
 Os dados XML enviados ao SQL Server são tratados como dados binários pelo servidor. Isso impede a ocorrência de qualquer conversão e permite que o analisador XML autodetecte a codificação de XML. Além disso, permite que uma variedade mais ampla de documentos XML (por exemplo, aqueles codificados em UTF-8) seja aceita como entrada no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Se o XML de entrada estiver associado como DBTYPE_WSTR, o aplicativo deverá garantir que já tem codificação Unicode para evitar qualquer possibilidade de corrompimento por conversões de dados indesejadas.  
  
### <a name="data-bindings-and-coercions"></a>Coerções e associações de dados  
 A tabela a seguir descreve a associação e a coerção que ocorrem ao usar os tipos de dados listados com o tipo de dados [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]xml **do**.  
  
|Tipo de dados|Para servidor<br /><br /> **XML**|Para servidor<br /><br /> **Não XML**|Do servidor<br /><br /> **XML**|Do servidor<br /><br /> **Não XML**|  
|---------------|---------------------------|--------------------------------|-----------------------------|----------------------------------|  
|DBTYPE_XML|Passagem<sup>6,7</sup>|Erro<sup>1</sup>|OK<sup>11, 6</sup>|Erro<sup>8</sup>|  
|DBTYPE_BYTES|Passagem<sup>6,7</sup>|N/A<sup>2</sup>|OK <sup>11, 6</sup>|N/D <sup>2</sup>|  
|DBTYPE_WSTR|Passagem<sup>6,10</sup>|N/D <sup>2</sup>|OK<sup>4, 6, 12</sup>|N/D <sup>2</sup>|  
|DBTYPE_BSTR|Passagem<sup>6,10</sup>|N/D <sup>2</sup>|OK <sup>3</sup>|N/D <sup>2</sup>|  
|DBTYPE_STR|OK<sup>6, 9, 10</sup>|N/D <sup>2</sup>|OK<sup>5, 6, 12</sup>|N/D <sup>2</sup>|  
|DBTYPE_IUNKNOWN|Fluxo de bytes por meio de **ISequentialStream**<sup>7</sup>|N/D <sup>2</sup>|Fluxo de bytes por meio de **ISequentialStream**<sup>11</sup>|N/D <sup>2</sup>|  
|DBTYPE_VARIANT (VT_UI1 &#124; VT_ARRAY)|Passagem<sup>6,7</sup>|N/D <sup>2</sup>|N/D|N/D <sup>2</sup>|  
|DBTYPE_VARIANT (VT_BSTR)|Passagem<sup>6,10</sup>|N/D <sup>2</sup>|OK<sup>3</sup>|N/D <sup>2</sup>|  
  
 <sup>1</sup>Se um tipo de servidor diferente de DBTYPE_XML for especificado com **ICommandWithParameters::SetParameterInfo** e o tipo de acessador for DBTYPE_XML, ocorrerá um erro quando a instrução for executada (para DB_E_ERRORSOCCURRED, o status do parâmetro é DBSTATUS_E_BADACCESSOR); caso contrário, os dados serão enviados para o servidor, mas ele retornará um erro indicando que não há conversão implícita do XML para o tipo de dados do parâmetro.  
  
 <sup>2</sup> Além do escopo deste tópico.  
  
 <sup>3</sup>O formato é UTF-16, não há BOM (marca de ordem de byte), não há especificação de codificação, não há terminação nula.  
  
 <sup>4</sup>O formato é UTF-16, não há BOM, não há especificação de codificação, há terminação nula.  
  
 <sup>5</sup>O formato consiste em caracteres multibyte codificados em página de código de cliente com terminador nulo. A conversão a partir do Unicode fornecido pelo servidor pode causar corrompimento dos dados, por isso essa associação é altamente desestimulada.  
  
 <sup>6</sup>BY_REF pode ser usado.  
  
 <sup>7</sup>Os dados UTF-16 precisam ser iniciados com BOM. Senão, a codificação poderá não ser reconhecida corretamente pelo servidor.  
  
 <sup>8</sup>A validação pode ocorrer no momento da criação do acessador ou no momento do fetch. O erro é DB_E_ERRORSOCCURRED; status da associação definido como DBBINDSTATUS_UNSUPPORTEDCONVERSION.  
  
 <sup>9</sup>Os dados são convertidos em Unicode usando a página de código de cliente antes de serem enviados para o servidor. Se a codificação de documento não corresponder à página de código de cliente, poderá haver corrompimento dos dados, por isso a associação é altamente desestimulada.  
  
 <sup>10</sup>Um BOM sempre é adicionado aos dados enviados para o servidor. Se os dados já forem iniciados com um BOM, isso resultará em dois BOMs no início do buffer. O servidor usa o primeiro BOM para reconhecer a codificação como UTF-16 e então o descarta. O segundo BOM é interpretado como um caractere de espaço incondicional de largura zero.  
  
 <sup>11</sup>O formato é UTF-16, não há especificação de codificação, um BOM é adicionado aos dados recebidos do servidor. Se uma cadeia de caracteres vazia for retornada pelo servidor, um BOM ainda será retornado para o aplicativo. Se o tamanho do buffer for um número ímpar de bytes, os dados serão truncados corretamente. Se o valor inteiro for retornado em partes, elas poderão ser concatenadas para reconstituir o valor correto.  
  
 <sup>12</sup> Se o comprimento do buffer for menor que dois caracteres – ou seja, não há espaço suficiente para terminação nula, um erro de estouro será relatado.  
  
> [!NOTE]  
>  Nenhum dado é retornado para valores de XML NULL.  
  
 O padrão XML exige que o XML codificado em UTF-16 seja iniciado com um código de caractere UTF-16 com BOM 0xFEFF. Ao trabalhar com associações WSTR e BSTR, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o Native Client não exige ou adiciona uma bom, pois a codificação é implícita pela associação. Ao trabalhar com associações BYTES, XML ou IUNKNOWN, a intenção é proporcionar simplicidade ao lidar com outros processadores XML e sistemas de armazenamento. Nesse caso, um BOM deve estar presente com o XML codificado em UTF-16, e o aplicativo não precisa verificar a codificação real, porque a maioria dos processadores XML (incluindo o SQL Server) deduz a codificação inspecionando os primeiros bytes do valor. Os dados XML recebidos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cliente nativo usando associações de bytes, XML ou IUnknown são sempre codificados em UTF-16 com uma bom e sem uma declaração de codificação incorporada.  
  
 As conversões de dados fornecidas por serviços principais do OLE DB (**IDataConvert**) não são aplicáveis a DBTYPE_XML.  
  
 A validação ocorre quando os dados são enviados para o servidor. As alterações de codificação e validação do lado do cliente devem ser manipuladas pelo aplicativo, e é altamente recomendável que você não processe os dados XML diretamente, mas sim use um leitor DOM ou SAX para processá-los.  
  
 DBTYPE_NULL e DBTYPE_EMPTY podem ser associados a parâmetros de entrada, mas não a parâmetros ou resultados de saída. Quando eles são associados para parâmetros de entrada, o status precisa ser definido como DBSTATUS_S_ISNULL ou DBSTATUS_S_DEFAULT.  
  
 DBTYPE_XML pode ser convertido em DBTYPE_EMPTY e DBTYPE_NULL, sendo que DBTYPE_EMPTY pode ser convertido em DBTYPE_XML, mas DBTYPE_NULL não pode ser convertido em DBTYPE_XML. Isso é condizente com DBTYPE_WSTR.  
  
 DBTYPE_IUNKNOWN é uma associação com suporte (conforme mostrado na tabela anterior), mas não há nenhuma conversão entre DBTYPE_XML e DBTYPE_IUNKNOWN. DBTYPE_IUNKNOWN não pode ser usado com DBTYPE_BYREF.  
  
### <a name="ole-db-rowset-additions-and-changes"></a>Adições e alterações do conjunto de linhas do OLE DB  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] O Native Client adiciona novos valores ou alterações a muitos dos conjuntos de linhas de esquema de OLE DB principal.  
  
#### <a name="the-columns-and-procedure_parameters-schema-rowsets"></a>Os conjuntos de linhas de esquema de COLUMNS e PROCEDURE_PARAMETERS  
 Entre as adições aos conjuntos de linhas de esquema de COLUMNS e PROCEDURE_PARAMETERS estão as colunas a seguir.  
  
|Nome da coluna|Type|DESCRIÇÃO|  
|-----------------|----------|-----------------|  
|SS_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|O nome de um catálogo no qual uma coleção de esquema XML é definida. NULL para uma coluna não XML ou coluna de XML não digitada.|  
|SS_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|O nome de um esquema no qual uma coleção de esquema XML é definida. NULL para uma coluna não XML ou coluna de XML não digitada.|  
|SS_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|O nome da coleção de esquemas XML. NULL para uma coluna não XML ou coluna de XML não digitada.|  
  
#### <a name="the-provider_types-schema-rowset"></a>O conjunto de linhas de esquema de PROVIDER_TYPES  
 No conjunto de linhas de esquema de PROVIDER_TYPES, o valor de COLUMN_SIZE é 0 para o tipo de dados **xml** e o DATA_TYPE é DBTYPE_XML.  
  
#### <a name="the-ss_xmlschema-schema-rowset"></a>O conjunto de linhas de esquema de SS_XMLSCHEMA  
 Um novo conjunto de linhas de esquema de SS_XMLSCHEMA é introduzido para que os clientes recuperem as informações de esquema XML. O conjunto de linhas de SS_XMLSCHEMA contém as colunas a seguir.  
  
|Nome da coluna|Type|DESCRIÇÃO|  
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
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] O Native Client adiciona novos valores ou alterações a muitos dos principais conjuntos de propriedades de OLE DB.  
  
#### <a name="the-dbpropset_sqlserverparameter-property-set"></a>O conjunto de propriedades de DBPROPSET_SQLSERVERPARAMETER  
 Para oferecer suporte ao tipo de dados **XML** por meio do OLE DB, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o Native Client implementa o novo conjunto de propriedades DBPROPSET_SQLSERVERPARAMETER, que contém os valores a seguir.  
  
|Nome|Type|DESCRIÇÃO|  
|----------|----------|-----------------|  
|SSPROP_PARAM_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|O nome de um catálogo (banco de dados) no qual é definida uma coleção de esquemas XML. Uma parte do identificador de nome de três partes SQL.|  
|SSPROP_PARAM_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|O nome de um esquema XML em uma coleção de esquemas. Uma parte do identificador de nome de três partes SQL.|  
|SSPROP_PARAM_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|O nome da coleção de esquemas XML no catálogo. Uma parte do identificador de nome de três partes SQL.|  
  
#### <a name="the-dbpropset_sqlservercolumn-property-set"></a>O conjunto de propriedades de DBPROPSET_SQLSERVERCOLUMN  
 Para dar suporte à criação de tabelas na interface **ITableDefinition** , [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o Native Client adiciona três novas colunas ao conjunto de propriedades DBPROPSET_SQLSERVERCOLUMN.  
  
|Nome|Type|DESCRIÇÃO|  
|----------|----------|-----------------|  
|SSPROP_COL_XML_SCHEMACOLLECTION_CATALOGNAME|VT_BSTR|Para colunas de XML digitadas, esta propriedade é uma cadeia de caracteres que especifica o nome do catálogo em que está armazenado o esquema XML. Para outros tipos de coluna, esta propriedade retorna uma cadeia de caracteres vazia.|  
|SSPROP_COL_XML_SCHEMACOLLECTION_SCHEMANAME|VT_BSTR|Para colunas de XML digitadas, esta propriedade é uma cadeia de caracteres que especifica o nome do esquema XML que define esta coluna.|  
|SSPROP_COL_XML_SCHEMACOLLECTIONNAME|VT_BSTR|Para colunas de XML digitadas, esta propriedade é uma cadeia de caracteres que especifica o nome da coleção de esquemas XML do esquema que define o valor.|  
  
 Assim como os valores de SSPROP_PARAM, todas essas propriedades são opcionais e o padrão é vazio. SSPROP_COL_XML_SCHEMACOLLECTION_CATALOGNAME e SSPROP_COL_XML_SCHEMACOLLECTION_SCHEMANAME só poderão ser especificados se SSPROP_COL_XML_SCHEMACOLLECTIONNAME for especificado. Na passagem do XML para o servidor, se esses valores forem incluídos, serão verificados quanto à existência (validade) com base no banco de dados atual, e os dados de instância serão verificados com base no esquema. Em todos os casos, para que sejam válidos eles ficam todos vazios ou todos preenchidos.  
  
### <a name="ole-db-interface-additions-and-changes"></a>Adições e alterações de interface do OLE DB  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] O Native Client adiciona novos valores ou alterações a muitas das principais interfaces de OLE DB.  
  
#### <a name="the-isscommandwithparameters-interface"></a>A interface ISSCommandWithParameters  
 Para oferecer suporte ao tipo de dados **XML** por meio do OLE DB, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o Native Client implementa várias alterações, incluindo a adição da interface [ISSCommandWithParameters](../../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md) . Essa nova interface herda as propriedades da interface principal do OLE DB **ICommandWithParameters**. Além dos três métodos herdados de **ICommandWithParameters**; **GetParameterInfo**, **MapParameterNames** e **SetParameterInfo**; **ISSCommandWithParameters** fornece os métodos [ParameterProperties](../../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-getparameterproperties-ole-db.md) e [ParameterProperties](../../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md) que são usados para tratar tipos de dados específicos do servidor.  
  
> [!NOTE]  
>  A interface **ISSCommandWithParameters** também usa a nova estrutura SSPARAMPROPS.  
  
#### <a name="the-icolumnsrowset-interface"></a>A interface IColumnsRowset  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] O Native Client adiciona as seguintes [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] colunas específicas ao conjunto de linhas retornado pelo método **IColumnRowset:: GetColumnsRowset** . Estas colunas contêm o nome de três partes de uma coleção de esquemas XML. Para colunas não XML ou colunas de XML não digitadas, as três colunas assumem o valor padrão de NULL.  
  
|Nome da coluna|Type|DESCRIÇÃO|  
|-----------------|----------|-----------------|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|O catálogo ao qual pertence uma coleção de esquema XML;<br /><br /> NULL em caso contrário.|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|O esquema ao qual pertence uma coleção de esquemas XML. NULL em caso contrário.|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|O nome da coleção de esquemas XML para a coluna de XML digitada; ou NULL em caso contrário.|  
  
#### <a name="the-irowset-interface"></a>A interface IRowset  
 Uma instância XML em uma coluna XML é recuperada por meio do método **IRowset::GetData**. Dependendo da associação especificada pelo cliente, uma instância de XML pode ser recuperada como DBTYPE_BSTR, DBTYPE_WSTR, DBTYPE_VARIANT, DBTYPE_XML, DBTYPE_STR, DBTYPE_BYTES ou como uma interface via DBTYPE_IUNKNOWN. Se o consumidor especificar DBTYPE_BSTR, DBTYPE_WSTR ou DBTYPE_VARIANT, o provedor converterá a instância de XML para o tipo solicitado pelo usuário e a colocará no local especificado na associação correspondente.  
  
 Se o consumidor especificar DBTYPE_IUNKNOWN e definir o argumento *pObject* como NULL ou definir o argumento *pObject* como IID_ISequentialStream, o provedor retornará uma interface **ISequentialStream** para o consumidor, de modo que ele possa transmitir os dados XML da coluna. Em seguida, **ISequentialStream** retornará os dados XML como um fluxo de caracteres Unicode.  
  
 Ao retornar um valor XML associado a DBTYPE_IUNKNOWN, o provedor informará um valor de tamanho de `sizeof (IUnknown *)`. Observe que esse procedimento é condizente com a abordagem adotada quando uma coluna é associada como DBTYPE_IUnknown ou DBTYPE_IDISPATCH e por DBTYPE_IUNKNOWN/ISequentialStream quando não é possível determinar o tamanho exato da coluna.  
  
#### <a name="the-irowsetchange-interface"></a>A interface IRowsetChange  
 Há duas maneiras de um consumidor atualizar uma instância de XML em uma coluna. A primeira é pelo objeto de armazenamento **ISequentialStream** criado pelo provedor. O consumidor pode chamar o método **ISequentialStream::Write** para atualizar diretamente a instância de XML retornada pelo provedor.  
  
 A segunda abordagem é pelos métodos **IRowsetChange::SetData** ou **IRowsetChange::InsertRow**. Nessa abordagem, uma instância de XML no buffer do consumidor pode ser especificada em uma associação de tipo DBTYPE_BSTR, DBTYPE_WSTR, DBTYPE_VARIANT, DBTYPE_XML ou DBTYPE_IUNKNOWN.  
  
 No caso de DBTYPE_BSTR, DBTYPE_WSTR ou DBTYPE_VARIANT, o provedor armazena a instância de XML que reside no buffer do consumidor na coluna adequada.  
  
 No caso de DBTYPE_IUNKNOWN/ISequentialStream, se o consumidor não especificar nenhum objeto de armazenamento, o consumidor deverá criar um objeto **ISequentialStream** com antecedência, associar o documento XML ao objeto e, em seguida, passar o objeto para o provedor por meio do método **IRowsetChange:: SetData** . O consumidor também pode criar um objeto de armazenamento, definir o argumento pObject como IID_ISequentialStream, criar um objeto **ISequentialStream** e, em seguida, passar o objeto **ISequentialStream** para o método **IRowsetChange::SetData**. Em ambos os casos, o provedor pode recuperar o objeto XML pelo objeto **ISequentialStream** e inseri-lo em uma coluna adequada.  
  
#### <a name="the-irowsetupdate-interface"></a>A interface IRowsetUpdate  
 A interface **IRowsetUpdate** oferece funcionalidade para atualizações atrasadas. Os dados disponibilizados para os conjuntos de linhas não são disponibilizados para outras transações até que o consumidor chame o método **IRowsetUpdate: Update** .  
  
#### <a name="the-irowsetfind-interface"></a>A interface IRowsetFind  
 O método **IRowsetFind::FindNextRow** não funciona com o tipo de dados **xml**. Quando **IRowsetFind::FindNextRow** é chamado e o argumento *hAccessor* especifica uma coluna de DBTYPE_XML, DB_E_BADBINDINFO é retornado. Isso ocorre independentemente do tipo de coluna que está sendo pesquisada. Para qualquer outro tipo de associação, **FindNextRow** falha com DB_E_BADCOMPAREOP se a coluna a ser pesquisada é do tipo de dados **xml**.  
  
## <a name="sql-server-native-client-odbc-driver"></a>Driver ODBC do SQL Server Native Client  
 No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Native Client, várias alterações foram feitas em diversas funções para dar suporte ao tipo de dados **XML** .  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 A função [SQLColAttribute](../../../relational-databases/native-client-odbc-api/sqlcolattribute.md) tem três novos identificadores de campo, incluindo SQL_CA_SS_XML_SCHEMACOLLECTION_CATALOG_NAME, SQL_CA_SS_XML_SCHEMACOLLECTION_SCHEMA_NAME e SQL_CA_SS _XML_SCHEMACOLLECTION_NAME.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Native Client relata SQL_SS_LENGTH_UNLIMITED para as colunas SQL_DESC_DISPLAY_SIZE e SQL_DESC_LENGTH.  
  
### <a name="sqlcolumns"></a>SQLColumns  
 A função [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md) tem três novas colunas, incluindo SS_XML_SCHEMACOLLECTION_CATALOG_NAME, SS_XML_SCHEMACOLLECTION_SCHEMA_NAME e SS_XML_SCHEMACOLLECTION_NAME. A coluna TYPE_NAME existente é usada para indicar o nome do tipo de XM, e o DATA_TYPE para um parâmetro ou coluna de tipo de XML é SQL_SS_XML.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Native Client relata SQL_SS_LENGTH_UNLIMITED para os valores de COLUMN_SIZE e CHAR_OCTET_LENGTH.  
  
### <a name="sqldescribecol"></a>SQLDescribeCol  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Native Client relata SQL_SS_LENGTH_UNLIMITED quando o tamanho da coluna não pode ser determinado na função [SQLDescribeCol](../../../relational-databases/native-client-odbc-api/sqldescribecol.md) .  
  
### <a name="sqlgettypeinfo"></a>SQLGetTypeInfo  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Native Client relata SQL_SS_LENGTH_UNLIMITED como o COLUMN_SIZE máximo para o tipo de dados **XML** na função [SQLGetTypeInfo](../../../relational-databases/native-client-odbc-api/sqlgettypeinfo.md) .  
  
### <a name="sqlprocedurecolumns"></a>SQLProcedureColumns  
 A função [SQLProcedureColumns](../../../relational-databases/native-client-odbc-api/sqlprocedurecolumns.md) tem as mesmas inclusões de coluna que a função **SQLColumns** .  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Native Client relata SQL_SS_LENGTH_UNLIMITED como o COLUMN_SIZE máximo para o tipo de dados **XML** .  
  
### <a name="supported-conversions"></a>Conversões com suporte  
 Ao converter de tipos de dados SQL para C, é possível converter SQL_C_WCHAR, SQL_C_BINARY e SQL_C_CHAR em SQL_SS_XML, com as estipulações a seguir:  
  
-   SQL_C_WCHAR: o formato é UTF-16, não há BOM, há terminação nula.  
  
-   SQL_C_BINARY: o formato é UTF-16, não há terminação nula. Um BOM é adicionado aos dados recebidos do servidor. Se uma cadeia de caracteres vazia for retornada pelo servidor, um BOM ainda será retornado para o aplicativo. Se a extensão do buffer for um número ímpar de bytes, os dados serão truncados corretamente. Se o valor inteiro for retornado em partes, elas poderão ser concatenadas para reconstituir o valor correto.  
  
-   SQL_C_CHAR: o formato consiste em caracteres multibyte codificados em página de código de cliente com terminação nula. A conversão a partir do UTF-16 fornecido pelo servidor pode causar corrompimento dos dados, por isso essa associação é altamente desestimulada.  
  
 Ao converter de tipos de dados C para SQL, é possível converter SQL_C_WCHAR, SQL_C_BINARY e SQL_C_CHAR em SQL_SS_XML, com as estipulações a seguir:  
  
-   SQL_C_WCHAR: um BOM sempre é adicionado aos dados enviados para o servidor. Se os dados já forem iniciados com um BOM, isso resultará em dois BOMs no início do buffer. O servidor usa o primeiro BOM para reconhecer a codificação como UTF-16 e então o descarta. O segundo BOM é interpretado como um caractere de espaço incondicional de largura zero.  
  
-   SQL_C_BINARY: nenhuma conversão é executada e os dados são passados para o servidor "no estado atual". Os dados UTF-16 precisam ser iniciados com um BOM; senão, a codificação poderá não ser reconhecida corretamente pelo servidor.  
  
-   SQL_C_CHAR: os dados são convertidos em UTF-16 no cliente e enviados para o servidor da mesma maneira que SQL_C_WCHAR (inclusive a adição de um BOM). Se o XML não for codificado na página de código de cliente, isso poderá causar corrompimento dos dados.  
  
 O padrão XML exige que o XML codificado em UTF-16 seja iniciado com um código de caractere UTF-16 com BOM 0xFEFF. Ao trabalhar com uma associação de SQL_C_BINARY, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client não exige ou adiciona uma bom, pois a codificação é implícita pela associação. A intenção é proporcionar simplicidade ao lidar com outros processadores XML e sistemas de armazenamento. Nesse caso, um BOM deve estar presente com o XML codificado em UTF-16, e o aplicativo não precisa verificar a codificação real, porque a maioria dos processadores XML (incluindo o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]) deduz a codificação inspecionando os primeiros bytes do valor. Os dados XML recebidos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cliente nativo usando associações de SQL_C_BINARY são sempre codificados em UTF-16 com uma bom e sem uma declaração de codificação inserida.  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos do SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
