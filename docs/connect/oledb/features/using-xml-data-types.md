---
title: Usar tipos de dados XML | Microsoft Docs
description: Usar tipos de dados XML com o Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- IRowsetChange interface
- IRowsetUpdate interface
- data access [OLE DB Driver for SQL Server], xml data type
- OLE DB Driver for SQL Server schema rowsets
- PROVIDER_TYPES rowset
- IColumnsInfo interface
- IRowsetFind interface
- IColumnsRowset interface
- PROCEDURE_PARAMETERS rowset
- MSOLEDBSQL, XML
- xml data type [SQL Server], OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server, XML
- IRowset interface
- ISequentialStream interface
- ISSCommandWithParameters interface
- SS_XMLSCHEMA rowset
- OLE DB Driver for SQL Server OLE DB interfaces
- XML [SQL Server], OLE DB Driver for SQL Server
- COLUMNS rowset
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 0d3554363e4813dfb4b3f6cbeefec00214d5a2d6
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67988793"
---
# <a name="using-xml-data-types"></a>Usando tipos de dados XML
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] introduziu um tipo de dados **xml** que permite armazenar documentos e fragmentos XML em um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O tipo de dados **xml** é interno no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e tem algumas semelhanças com outros tipos internos, como **int** e **varchar**. Assim como ocorre em outros tipos internos, você pode usar o tipo de dados **xml** como um tipo de coluna ao criar uma tabela; como um tipo de variável, de parâmetro ou de retorno de função; ou em funções CAST e CONVERT.  
  
## <a name="programming-considerations"></a>Considerações sobre programação  
 O XML pode ser autodescritivo no sentido de que pode opcionalmente incluir um cabeçalho de XML que especifica a codificação do documento, por exemplo:  
  
 `<?xml version="1.0" encoding="windows-1252"?><doc/>`  
  
 O padrão XML descreve como um processador XML pode detectar a codificação usada para um documento examinando os primeiros bytes desse documento. Há riscos de a codificação especificada pelo aplicativo entrar em conflito com a especificada pelo documento. No caso de documentos passados como parâmetros associados, o XML é tratado como dados binários pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], por isso nenhuma conversão é feita e o analisador XML pode usar a codificação especificada no documento sem problemas. Entretanto, no caso de dados XML associados como WSTR, o aplicativo precisa garantir que o documento está codificado como Unicode. Esse cenário pode implicar o carregamento do documento em um DOM, a alteração da codificação para Unicode e a serialização do documento. Se essa etapa não for concluída, poderão ocorrer conversões de dados, resultando em um XML inválido ou corrompido.  
  
 Também há risco de conflitos quando o XML é especificado em literais. Por exemplo, as expressões a seguir são inválidas:  
  
 `INSERT INTO xmltable(xmlcol) VALUES('<?xml version="1.0" encoding="UTF-16"?><doc/>')`  
  
 `INSERT INTO xmltable(xmlcol) VALUES(N'<?xml version="1.0" encoding="UTF-8"?><doc/>')`  
  
## <a name="ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server 
 DBTYPE_XML é um novo tipo de dados específico ao XML no Driver do OLE DB para SQL Server. Além disso, é possível acessar dados XML pelos tipos de OLE DB existentes DBTYPE_BYTES, DBTYPE_WSTR, DBTYPE_BSTR, DBTYPE_XML, DBTYPE_STR, DBTYPE_VARIANT e DBTYPE_IUNKNOWN. Os dados armazenados em colunas do tipo XML podem ser recuperados de uma coluna em um conjunto de linhas do OLE DB Driver for SQL Server nos seguintes formatos:  
  
-   Uma cadeia de caracteres de texto  
  
-   Um **ISequentialStream**  
  
> [!NOTE]  
>  O OLE DB Driver for SQL Server não inclui um leitor SAX, mas **ISequentialStream** pode ser passado com facilidade para objetos SAX e DOM em MSXML.  
  
 **ISequentialStream** deve ser usado para recuperação de documentos XML extensos. As mesmas técnicas usadas para outros tipos de valor extenso também se aplicam ao XML. Para obter mais informações, confira [Usar tipos de valor grande](../../oledb/features/using-large-value-types.md).  
  
 Os dados armazenados em colunas do tipo XML em um conjunto de linhas também podem ser recuperados, inseridos ou atualizados por um aplicativo por meio das interfaces comuns como **IRow::GetColumns**, **IRowChange::SetColumns** e **ICommand::Execute**. De maneira semelhante ao caso da recuperação, um programa aplicativo pode passar uma cadeia de caracteres de texto ou um **ISequentialStream** para o OLE DB Driver for SQL Server.  
  
> [!NOTE]  
>  Para enviar dados XML em formato de cadeia de caracteres pela interface **ISequentialStream**, você precisa obter o **ISequentialStream** especificando DBTYPE_IUNKNOWN e definir seu argumento *pObject* como nulo na associação.  
  
 Quando os dados XML recuperados estão truncados porque o buffer de consumidor é muito pequeno, a extensão poderá ser retornada como 0xffffffff, o que significará que ela é desconhecida. Esse comportamento é consistente com sua implementação como um tipo de dados transmitido ao cliente sem o envio das informações de tamanho antes dos dados reais. Em alguns casos, o tamanho real pode ser retornado quando o provedor executou o buffer do valor inteiro, como **IRowset::GetData** e quando é feita a conversão de dados.  
  
 Os dados XML enviados ao SQL Server são tratados como dados binários pelo servidor. Esse comportamento impede a ocorrência de qualquer conversão e permite que o analisador XML detecte automaticamente a codificação de XML. Além disso, permite que uma variedade mais ampla de documentos XML (por exemplo, aqueles codificados em UTF-8) seja aceita como entrada no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Se o XML de entrada estiver associado como DBTYPE_WSTR, o aplicativo deverá garantir que já tem codificação Unicode para evitar qualquer possibilidade de corrompimento por conversões de dados indesejadas.  
  
### <a name="data-bindings-and-coercions"></a>Coerções e associações de dados  
 A tabela a seguir descreve a associação e a coerção que ocorrem ao usar os tipos de dados listados com o tipo de dados **xml** do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
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
  
 <sup>2</sup>Além do escopo deste artigo.  
  
 <sup>3</sup>O formato é UTF-16, não há BOM (marca de ordem de byte), não há especificação de codificação, não há terminação nula.  
  
 <sup>4</sup>O formato é UTF-16, não há BOM, não há especificação de codificação, há terminação nula.  
  
 <sup>5</sup>O formato consiste em caracteres multibyte codificados em página de código de cliente com terminador nulo. A conversão do Unicode fornecido pelo servidor pode fazer com que os dados sejam corrompidos e, portanto, essa associação é desaconselhável.  
  
 <sup>6</sup>BY_REF pode ser usado.  
  
 <sup>7</sup>Os dados UTF-16 precisam ser iniciados com BOM. Senão, a codificação poderá não ser reconhecida corretamente pelo servidor.  
  
 <sup>8</sup>A validação pode ocorrer no momento da criação do acessador ou no momento do fetch. O erro é DB_E_ERRORSOCCURRED; status da associação definido como DBBINDSTATUS_UNSUPPORTEDCONVERSION.  
  
 <sup>9</sup>Os dados são convertidos em Unicode usando a página de código de cliente antes de serem enviados para o servidor. Se a codificação de documento não corresponder à página de código de cliente, os dados poderão ser corrompidos e, portanto, a associação é altamente desaconselhável.  
  
 <sup>10</sup>Um BOM sempre é adicionado aos dados enviados para o servidor. Se os dados já forem iniciados com um BOM, haverá dois BOMs no início do buffer. O servidor usa o primeiro BOM para reconhecer a codificação como UTF-16 e então o descarta. O segundo BOM é interpretado como um caractere de espaço incondicional de largura zero.  
  
 <sup>11</sup>O formato é UTF-16, não há especificação de codificação, um BOM é adicionado aos dados recebidos do servidor. Se uma cadeia de caracteres vazia for retornada pelo servidor, um BOM ainda será retornado para o aplicativo. Se o tamanho do buffer for um número ímpar de bytes, os dados serão truncados corretamente. Se o valor inteiro for retornado em partes, elas poderão ser concatenadas para reconstituir o valor correto.  
  
 <sup>12</sup>Se o tamanho do buffer for menor que dois caracteres – ou seja, se não houver espaço suficiente para terminação nula – um erro de estouro será relatado.  
  
> [!NOTE]  
>  Nenhum dado é retornado para valores de XML NULL.  
  
 O padrão XML exige que o XML codificado em UTF-16 seja iniciado com um código de caractere UTF-16 com BOM 0xFEFF. Ao trabalhar com associações WSTR e BSTR, o OLE DB Driver for SQL Server não exige nem adiciona um BOM, porque a codificação é implícita na associação. Ao trabalhar com associações BYTES, XML ou IUNKNOWN, a intenção é proporcionar simplicidade ao lidar com outros processadores XML e sistemas de armazenamento. Nesse caso, um BOM deve estar presente com o XML codificado em UTF-16, e o aplicativo não precisa verificar a codificação real, porque a maioria dos processadores XML (incluindo o SQL Server) deduz a codificação inspecionando os primeiros bytes do valor. Os dados XML recebidos do OLE DB Driver for SQL Server usando as associações BYTES, XML ou IUNKNOWN são sempre codificados em UTF-16 com um BOM e sem uma declaração de codificação inserida.  
  
 As conversões de dados fornecidas por serviços principais do OLE DB (**IDataConvert**) não são aplicáveis a DBTYPE_XML.  
  
 A validação ocorre quando os dados são enviados para o servidor. O aplicativo deverá ser responsável por lidar com as alterações de validação e codificação do lado do cliente. É recomendável que você não processe os dados XML diretamente, mas, em vez disso, use um leitor DOM ou SAX para processá-los.  
  
 DBTYPE_NULL e DBTYPE_EMPTY podem ser associados a parâmetros de entrada, mas não a parâmetros ou resultados de saída. Quando eles são associados para parâmetros de entrada, o status precisa ser definido como DBSTATUS_S_ISNULL ou DBSTATUS_S_DEFAULT.  
  
 DBTYPE_XML pode ser convertido em DBTYPE_EMPTY e DBTYPE_NULL, sendo que DBTYPE_EMPTY pode ser convertido em DBTYPE_XML, mas DBTYPE_NULL não pode ser convertido em DBTYPE_XML. Isso é condizente com DBTYPE_WSTR.  
  
 DBTYPE_IUNKNOWN é uma associação compatível (conforme mostrado na tabela anterior), mas não há nenhuma conversão entre DBTYPE_XML e DBTYPE_IUNKNOWN. DBTYPE_IUNKNOWN não pode ser usado com DBTYPE_BYREF.  
  
### <a name="ole-db-rowset-additions-and-changes"></a>Adições e alterações do conjunto de linhas do OLE DB  
 O Driver do OLE DB para SQL Server adiciona novos valores ou alterações a muitos dos conjuntos de linhas de esquema principais do OLE DB.  
  
#### <a name="the-columns-and-procedure_parameters-schema-rowsets"></a>Os conjuntos de linhas de esquema de COLUMNS e PROCEDURE_PARAMETERS  
 As adições aos conjuntos de linhas de esquema COLUMNS e PROCEDURE_PARAMETERS incluem as seguintes colunas:  
  
|Nome da coluna|Type|Descrição|  
|-----------------|----------|-----------------|  
|SS_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|O nome de um catálogo no qual uma coleção de esquema XML é definida. NULL para uma coluna não XML ou uma coluna XML não tipada.|  
|SS_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|O nome de um esquema no qual uma coleção de esquema XML é definida. NULL para uma coluna não XML ou uma coluna XML não tipada.|  
|SS_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|O nome da coleção de esquemas XML. NULL para uma coluna não XML ou uma coluna XML não tipada.|  
  
#### <a name="the-provider_types-schema-rowset"></a>O conjunto de linhas de esquema de PROVIDER_TYPES  
 No conjunto de linhas de esquema de PROVIDER_TYPES, o valor de COLUMN_SIZE é 0 para o tipo de dados **xml** e o DATA_TYPE é DBTYPE_XML.  
  
#### <a name="the-ss_xmlschema-schema-rowset"></a>O conjunto de linhas de esquema de SS_XMLSCHEMA  
 Um novo conjunto de linhas de esquema de SS_XMLSCHEMA é introduzido para que os clientes recuperem as informações de esquema XML. O conjunto de linhas de SS_XMLSCHEMA contém as seguintes colunas:  
  
|Nome da coluna|Type|Descrição|  
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
 O Driver do OLE DB para SQL Server adiciona novos valores ou alterações a muitos dos conjuntos de propriedades principais do OLE DB.  
  
#### <a name="the-dbpropset_sqlserverparameter-property-set"></a>O conjunto de propriedades de DBPROPSET_SQLSERVERPARAMETER  
 Para dar suporte ao tipo de dados **xml** por meio do OLE DB, o OLE DB Driver for SQL Server implementa o novo conjunto de propriedades DBPROPSET_SQLSERVERPARAMETER, que contém os valores a seguir.  
  
|Nome|Type|Descrição|  
|----------|----------|-----------------|  
|SSPROP_PARAM_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|O nome de um catálogo (banco de dados) no qual é definida uma coleção de esquemas XML. Uma parte do identificador de nome de três partes SQL.|  
|SSPROP_PARAM_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|O nome de um esquema XML em uma coleção de esquemas. Uma parte do identificador de nome de três partes SQL.|  
|SSPROP_PARAM_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|O nome da coleção de esquemas XML no catálogo. Uma parte do identificador de nome de três partes SQL.|  
  
#### <a name="the-dbpropset_sqlservercolumn-property-set"></a>O conjunto de propriedades de DBPROPSET_SQLSERVERCOLUMN  
 Para dar suporte à criação de tabelas na interface **ITableDefinition**, o OLE DB Driver for SQL Server adiciona as três novas colunas ao conjunto de propriedades DBPROPSET_SQLSERVERCOLUMN.  
  
|Nome|Type|Descrição|  
|----------|----------|-----------------|  
|SSPROP_COL_XML_SCHEMACOLLECTION_CATALOGNAME|VT_BSTR|Para colunas de XML digitadas, esta propriedade é uma cadeia de caracteres que especifica o nome do catálogo em que está armazenado o esquema XML. Para outros tipos de coluna, essa propriedade retorna uma cadeia de caracteres vazia.|  
|SSPROP_COL_XML_SCHEMACOLLECTION_SCHEMANAME|VT_BSTR|Para colunas de XML digitadas, esta propriedade é uma cadeia de caracteres que especifica o nome do esquema XML que define esta coluna.|  
|SSPROP_COL_XML_SCHEMACOLLECTIONNAME|VT_BSTR|Para colunas de XML digitadas, esta propriedade é uma cadeia de caracteres que especifica o nome da coleção de esquemas XML do esquema que define o valor.|  
  
 Assim como os valores de SSPROP_PARAM, todas essas propriedades são opcionais e o padrão é vazio. SSPROP_COL_XML_SCHEMACOLLECTION_CATALOGNAME e SSPROP_COL_XML_SCHEMACOLLECTION_SCHEMANAME só poderão ser especificados se SSPROP_COL_XML_SCHEMACOLLECTIONNAME for especificado. Na passagem do XML para o servidor, se esses valores forem incluídos, serão verificados quanto à existência (validade) com base no banco de dados atual, e os dados de instância serão verificados com base no esquema. Em todos os casos, para que sejam válidos eles ficam todos vazios ou todos preenchidos.  
  
### <a name="ole-db-interface-additions-and-changes"></a>Adições e alterações de interface do OLE DB  
 O Driver do OLE DB para SQL Server adiciona novos valores ou alterações a muitas das interfaces principais do OLE DB.  
  
#### <a name="the-isscommandwithparameters-interface"></a>A interface ISSCommandWithParameters  
 Para dar suporte ao tipo de dados **xml** por meio do OLE DB, o OLE DB Driver for SQL Server implementa várias alterações, incluindo a adição da interface [ISSCommandWithParameters](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md). Essa nova interface herda as propriedades da interface principal do OLE DB **ICommandWithParameters**. Além dos três métodos herdados de **ICommandWithParameters**; **GetParameterInfo**, **MapParameterNames** e **SetParameterInfo**; **ISSCommandWithParameters** fornece os métodos [GetParameterProperties](../../oledb/ole-db-interfaces/isscommandwithparameters-getparameterproperties-ole-db.md) e [SetParameterProperties](../../oledb/ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md) usados para manipular tipos de dados específicos de servidor.  
  
> [!NOTE]  
>  A interface **ISSCommandWithParameters** também usa a nova estrutura SSPARAMPROPS.  
  
#### <a name="the-icolumnsrowset-interface"></a>A interface IColumnsRowset  
 O OLE DB Driver for SQL Server adiciona as colunas específicas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a seguir ao conjunto de linhas retornado pelo método **IColumnRowset::GetColumnsRowset**. Estas colunas contêm o nome de três partes de uma coleção de esquemas XML. Para colunas não XML ou colunas de XML não digitadas, as três colunas assumem o valor padrão de NULL.  
  
|Nome da coluna|Type|Descrição|  
|-----------------|----------|-----------------|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|O catálogo ao qual pertence uma coleção de esquema XML;<br /><br /> NULL em caso contrário.|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|O esquema ao qual pertence uma coleção de esquemas XML. NULL em caso contrário.|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|O nome da coleção de esquemas XML para a coluna de XML digitada; ou NULL em caso contrário.|  
  
#### <a name="the-irowset-interface"></a>A interface IRowset  
 Uma instância XML em uma coluna XML é recuperada por meio do método **IRowset::GetData**. Dependendo da associação especificada pelo cliente, uma instância de XML pode ser recuperada como DBTYPE_BSTR, DBTYPE_WSTR, DBTYPE_VARIANT, DBTYPE_XML, DBTYPE_STR, DBTYPE_BYTES ou como uma interface via DBTYPE_IUNKNOWN. Se o consumidor especificar DBTYPE_BSTR, DBTYPE_WSTR ou DBTYPE_VARIANT, o provedor converterá a instância de XML para o tipo solicitado pelo usuário e a colocará no local especificado na associação correspondente.  
  
 Se o consumidor especificar DBTYPE_IUNKNOWN e definir o argumento *pObject* como NULL ou definir o argumento *pObject* como IID_ISequentialStream, o provedor retornará uma interface **ISequentialStream** para o consumidor, de modo que ele possa transmitir os dados XML da coluna. Em seguida, **ISequentialStream** retornará os dados XML como um fluxo de caracteres Unicode.  
  
 Ao retornar um valor XML associado a DBTYPE_IUNKNOWN, o provedor informará um valor de tamanho de `sizeof (IUnknown *)`. Esse comportamento é consistente com a abordagem adotada quando uma coluna é associada como DBTYPE_IUnknown ou DBTYPE_IDISPATCH e por DBTYPE_IUNKNOWN/ISequentialStream quando não é possível determinar o tamanho exato da coluna.  
  
#### <a name="the-irowsetchange-interface"></a>A interface IRowsetChange  
 Há duas maneiras de um consumidor atualizar uma instância de XML em uma coluna. A primeira é pelo objeto de armazenamento **ISequentialStream** criado pelo provedor. O consumidor pode chamar o método **ISequentialStream::Write** para atualizar diretamente a instância de XML retornada pelo provedor.  
  
 A segunda abordagem é pelos métodos **IRowsetChange::SetData** ou **IRowsetChange::InsertRow**. Nessa abordagem, uma instância de XML no buffer do consumidor pode ser especificada em uma associação de tipo DBTYPE_BSTR, DBTYPE_WSTR, DBTYPE_VARIANT, DBTYPE_XML ou DBTYPE_IUNKNOWN.  
  
 Se DBTYPE_BSTR, DBTYPE_WSTR ou DBTYPE_VARIANT for especificado, o provedor armazenará a instância de XML que reside no buffer do consumidor na coluna adequada.  
  
 Se DBTYPE_IUNKNOWN/ISequentialStream for especificado, se o consumidor não especificar um objeto de armazenamento, ele precisará criar um objeto **ISequentialStream** com antecedência, associar o documento XML ao objeto e, em seguida, passar esse objeto para o provedor por meio do método **IRowsetChange::SetData**. O consumidor também pode criar um objeto de armazenamento, definir o argumento pObject como IID_ISequentialStream, criar um objeto **ISequentialStream** e, em seguida, passar o objeto **ISequentialStream** para o método **IRowsetChange::SetData**. Em ambos os casos, o provedor pode recuperar o objeto XML pelo objeto **ISequentialStream** e inseri-lo em uma coluna adequada.  
  
#### <a name="the-irowsetupdate-interface"></a>A interface IRowsetUpdate  
 A interface **IRowsetUpdate** oferece funcionalidade para atualizações atrasadas. Os dados disponibilizados aos conjuntos de linhas não ficarão disponíveis para outras transações enquanto o consumidor não chamar o método **IRowsetUpdate::Update**.  
  
#### <a name="the-irowsetfind-interface"></a>A interface IRowsetFind  
 O método **IRowsetFind::FindNextRow** não funciona com o tipo de dados **xml**. Quando **IRowsetFind::FindNextRow** é chamado e o argumento *hAccessor* especifica uma coluna de DBTYPE_XML, DB_E_BADBINDINFO é retornado. Isso ocorre independentemente do tipo de coluna que está sendo pesquisada. Para qualquer outro tipo de associação, **FindNextRow** falha com DB_E_BADCOMPAREOP se a coluna a ser pesquisada é do tipo de dados **xml**.  
 
  
## <a name="see-also"></a>Consulte Também  
 [Recursos do OLE DB Driver for SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)    
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
