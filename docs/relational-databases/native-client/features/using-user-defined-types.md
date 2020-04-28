---
title: Usando tipos definidos pelo usuário | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- DBPROPSET_DATASOURCEINFO property set
- UDTs [SQL Server Native Client]
- user-defined types [SQL Server], SQL Server Native Client
- SQL Server Native Client OLE DB provider, user-defined types
- DBPROPSET_SQLSERVERPARAMETER property set
- IColumnsRowset interface
- SQLNCLI, user-defined types
- SQL Server Native Client, user-defined types
- data access [SQL Server Native Client], user-defined types
- ISSCommandWithParameters interface
ms.assetid: e15d8169-3517-4323-9c9e-0f5c34aff7df
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4c6b6cf14925b7baace60a7de6c7aeaf3057de46
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303178"
---
# <a name="using-user-defined-types"></a>Usando tipos definidos pelo usuário
[!INCLUDE[appliesto-ss-asdb-xxxx-pdw-md](../../../includes/appliesto-ss-asdb-xxxx-pdw-md.md)]

  O [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] introduziu os UDTs (tipos definidos pelo usuário). Os UDTs estendem o sistema de tipos SQL, permitindo que você armazene objetos e estruturas de dados personalizadas em um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Os UDTs podem conter vários tipos de dados e ter comportamentos, o que os diferencia dos tipos de dados de alias tradicionais, que consistem em um único tipo de dado do sistema no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. UDTs são definidos usando quaisquer dos idiomas com suporte pelo .NET CRL (Common Language Runtime) que gera código verificável. Isso inclui o Microsoft Visual C#<sup>®</sup> e o Visual Basic<sup>®</sup> .net. Os dados são expostos como campos e propriedades de uma classe ou estrutura .NET e os comportamentos são definidos pelos métodos da classe ou estrutura.  
  
 Um UDT pode ser usado como definição de coluna de uma tabela, como uma variável em um lote [!INCLUDE[tsql](../../../includes/tsql-md.md)], ou como um argumento de uma função [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou um procedimento armazenado.  
  
## <a name="sql-server-native-client-ole-db-provider"></a>Provedor OLE DB do SQL Server Native Client  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo dá suporte a UDTs como tipos binários com informações de metadados, o que permite que você gerencie UDTs como objetos. As colunas UDT são expostas como DBTYPE_UDT e seus metadados são expostos pela interface principal do OLE DB **IColumnRowset** e pela nova interface [ISSCommandWithParameters](../../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md).  
  
> [!NOTE]  
>  O método **IRowsetFind::FindNextRow** não funciona com o tipo de dados UDT. DB_E_BADCOMPAREOP será retornado se o UDT for usado como um tipo de coluna de pesquisa.  
  
### <a name="data-bindings-and-coercions"></a>Coerções e associações de dados  
 A tabela a seguir descreve a associação e a coerção que ocorrem ao usar os tipos de dados listados com o UDT [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. As colunas UDT são expostas por meio do provedor de OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cliente nativo como DBTYPE_UDT. Você pode obter metadados por meio dos conjuntos de linhas de esquema apropriados de forma que possa gerenciar seus próprios tipos definidos como objetos.  
  
|Tipo de dados|Para servidor<br /><br /> **UDT**|Para servidor<br /><br /> **não UDT**|Do servidor<br /><br /> **UDT**|Do servidor<br /><br /> **não UDT**|  
|---------------|---------------------------|--------------------------------|-----------------------------|----------------------------------|  
|DBTYPE_UDT|Compatível<sup>6</sup>|Erro<sup>1</sup>|Compatível<sup>6</sup>|Erro<sup>5</sup>|  
|DBTYPE_BYTES|Compatível<sup>6</sup>|N/A<sup>2</sup>|Compatível<sup>6</sup>|N/A<sup>2</sup>|  
|DBTYPE_WSTR|Compatível<sup>3, 6</sup>|N/A<sup>2</sup>|Compatível<sup>4, 6</sup>|N/A<sup>2</sup>|  
|DBTYPE_BSTR|Compatível<sup>3, 6</sup>|N/A<sup>2</sup>|Compatível<sup>4</sup>|N/A<sup>2</sup>|  
|DBTYPE_STR|Compatível<sup>3, 6</sup>|N/A<sup>2</sup>|Compatível<sup>4, 6</sup>|N/A<sup>2</sup>|  
|DBTYPE_IUNKNOWN|Sem suporte|N/A<sup>2</sup>|Sem suporte|N/A<sup>2</sup>|  
|DBTYPE_VARIANT (VT_UI1 &#124; VT_ARRAY)|Compatível<sup>6</sup>|N/A<sup>2</sup>|Compatível<sup>4</sup>|N/A<sup>2</sup>|  
|DBTYPE_VARIANT (VT_BSTR)|Compatível<sup>3, 6</sup>|N/A<sup>2</sup>|N/D|N/A<sup>2</sup>|  
  
 <sup>1</sup>Se um tipo de servidor diferente de DBTYPE_UDT for especificado com **ICommandWithParameters::SetParameterInfo** e o tipo de acessador for DBTYPE_UDT, ocorrerá um erro quando a instrução for executada (para DB_E_ERRORSOCCURRED, o status do parâmetro é DBSTATUS_E_BADACCESSOR). Caso contrário, os dados serão enviados para o servidor, mas ele retornará um erro indicando que não há conversão implícita do UDT para o tipo de dados do parâmetro.  
  
 <sup>2</sup> Além do escopo deste tópico.  
  
 <sup>3</sup> Ocorre a conversão de dados de cadeia de caracteres hexadecimal para dados binários.  
  
 <sup>4</sup> Ocorre a conversão de dados binários para cadeia de caracteres hexadecimal.  
  
 <sup>5</sup>Pode ocorrer a validação no momento de criação do acessador ou, no momento do fetch, o erro é DB_E_ERRORSOCCURRED, o status de associação está definido como DBBINDSTATUS_UNSUPPORTEDCONVERSION.  
  
 <sup>6</sup>BY_REF pode ser usado.  
  
 DBTYPE_NULL e DBTYPE_EMPTY podem ser associados a parâmetros de entrada, mas não a parâmetros ou resultados de saída. Quando eles são associados a parâmetros de entrada, o status precisa ser definido como DBSTATUS_S_ISNULL ou DBSTATUS_S_DEFAULT.  
  
 DBTYPE_UDT pode ser convertido em DBTYPE_EMPTY e DBTYPE_NULL, porém DBTYPE_NULL e DBTYPE_EMPTY não podem ser convertidos em DBTYPE_UDT. Isso é consistente com DBTYPE_BYTES.  
  
> [!NOTE]  
>  Uma nova interface é usada para lidar com UDTs como parâmetros, **ISSCommandWithParameters**, herdada de **ICommandWithParameters**. Os aplicativos devem usar esta interface para definir pelo menos o SSPROP_PARAM_UDT_NAME da propriedade DBPROPSET_SQLSERVERPARAMETER definida para os parâmetros de UDT. Se isto não for feito, **ICommand::Execute** retornará DB_E_ERRORSOCCURRED. Esta interface e conjunto de propriedades serão descritos posteriormente neste tópico.  
  
 Se um tipo definido pelo usuário for inserido em uma coluna que não seja grande o suficiente para manter todos os dados, **ICommand::Execute** retornará S_OK com o status DB_E_ERRORSOCCURRED.  
  
 As conversões de dados fornecidas pelos serviços principais do OLE DB (**IDataConvert**) não são aplicáveis a DBTYPE_UDT. As demais associações não têm suporte.  
  
### <a name="ole-db-rowset-additions-and-changes"></a>Adições e alterações do conjunto de linhas do OLE DB  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]O Native Client adiciona novos valores ou alterações a muitos dos conjuntos de linhas de esquema de OLE DB principal.  
  
#### <a name="the-procedure_parameters-schema-rowset"></a>O conjunto de linhas do esquema PROCEDURE_PARAMETERS  
 As adições a seguir foram feitas ao conjunto de linhas de esquema de PROCEDURE_PARAMETERS.  
  
|Nome da coluna|Type|Descrição|  
|-----------------|----------|-----------------|  
|SS_UDT_CATALOGNAME|DBTYPE_WSTR|O identificador de nome de três partes.|  
|SS_UDT_SCHEMANAME|DBTYPE_WSTR|O identificador de nome de três partes.|  
|SS_UDT_NAME|DBTYPE_WSTR|O identificador de nome de três partes.|  
|SS_UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|O Nome Qualificado do Assembly, que inclui o nome de tipo e toda a identificação de assembly necessários para referência pelo CLR.|  
  
#### <a name="the-sql_assemblies-schema-rowset"></a>O conjunto de linhas do esquema SQL_ASSEMBLIES  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo expõe um novo conjunto de linhas de esquema específico de provedor que descreve os UDTs registrados. O servidor de ASSEMBLY pode ser especificado como um DBTYPE_WSTR, mas não está presente no conjunto de linhas. Se não estiver especificado, o conjunto de linhas seguirá o padrão do servidor atual. O conjunto de linhas de esquema de SQL_ASSEMBLIES é definido na tabela a seguir.  
  
|Nome da coluna|Type|Descrição|  
|-----------------|----------|-----------------|  
|ASSEMBLY_CATALOG|DBTYPE_WSTR|O nome de catálogo do assembly que contém o tipo.|  
|ASSEMBLY_SCHEMA|DBTYPE_WSTR|O nome do esquema ou nome do proprietário do assembly que contém o tipo. Embora os assemblies tenham escopo por banco de dados e não por esquema, eles ainda têm um proprietário que é refletido aqui.|  
|ASSEMBLY_NAME|DBTYPE_WSTR|O nome do assembly que contém o tipo.|  
|ASSEMBLY_ID|DBTYPE_UI4|A id do objeto do assembly que contém o tipo.|  
|PERMISSION_SET|DBTYPE_WSTR|Um valor que indica o escopo de acesso para o assembly. Valores incluem "SAFE", "EXTERNAL_ACCESS" e "UNSAFE".|  
|ASSEMBLY_BINARY|DBTYPE_BYTES|A representação binária do assembly.|  
  
#### <a name="the-sql_assemblies_-dependencies-schema-rowset"></a>O conjunto de linhas do esquema SQL_ASSEMBLIES_ DEPENDENCIES  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]O provedor de OLE DB de cliente nativo expõe um novo conjunto de linhas de esquema específico de provedor que descreve as dependências de assembly para um servidor especificado. O ASSEMBLY_SERVER pode ser especificado pelo chamador como um DBTYPE_WSTR, mas não está presente no conjunto de linhas. Se não estiver especificado, o conjunto de linhas seguirá o padrão do servidor atual. O conjunto de linhas de esquema de SQL_ASSEMBLY_DEPENDENCIES é definido na tabela a seguir.  
  
|Nome da coluna|Type|Descrição|  
|-----------------|----------|-----------------|  
|ASSEMBLY_CATALOG|DBTYPE_WSTR|O nome de catálogo do assembly que contém o tipo.|  
|ASSEMBLY_SCHEMA|DBTYPE_WSTR|O nome do esquema ou nome do proprietário do assembly que contém o tipo. Embora os assemblies tenham escopo por banco de dados e não por esquema, eles ainda têm um proprietário, que é refletido aqui.|  
|ASSEMBLY_ID|DBTYPE_UI4|A id do objeto do assembly.|  
|REFERENCED_ASSEMBLY_ID|DBTYPE_UI4|A id do objeto do assembly referenciado.|  
  
#### <a name="the-sql_user_types-schema-rowset"></a>O conjunto de linhas do esquema SQL_USER_TYPES  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]O provedor de OLE DB de cliente nativo expõe o novo conjunto de linhas de esquema, SQL_USER_TYPES, que descreve quando os UDTs registrados para um servidor especificado são adicionados. O UDT_SERVER deve ser especificado pelo chamador como um DBTYPE_WSTR, mas não está presente no conjunto de linhas. O conjunto de linhas de esquema de SQL_USER_TYPES é definido na tabela a seguir.  
  
|Nome da coluna|Type|Descrição|  
|-----------------|----------|-----------------|  
|UDT_CATALOGNAME|DBTYPE_WSTR|Para colunas de UDT esta propriedade é uma cadeia de caracteres que especifica o nome do catálogo onde o UDT é definido.|  
|UDT_SCHEMANAME|DBTYPE_WSTR|Para colunas de UDT esta propriedade é uma cadeia de caracteres que especifica o nome do esquema onde o UDT é definido.|  
|UDT_NAME|DBTYPE_WSTR|O nome do assembly que contém a classe do UDT.|  
|UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|O AQN (nome de tipo completo) inclui o nome do tipo prefixado pelo namespace, se aplicável.|  
  
#### <a name="the-columns-schema-rowset"></a>O conjunto de linhas do esquema COLUMNS  
 Adições para o conjunto de linhas de esquema de COLUMNS incluem as colunas a seguir.  
  
|Nome da coluna|Type|Descrição|  
|-----------------|----------|-----------------|  
|SS_UDT_CATALOGNAME|DBTYPE_WSTR|Para colunas de UDT esta propriedade é uma cadeia de caracteres que especifica o nome do catálogo onde o UDT é definido.|  
|SS_UDT_SCHEMANAME|DBTYPE_WSTR|Para colunas de UDT esta propriedade é uma cadeia de caracteres que especifica o nome do esquema onde o UDT é definido.|  
|SS_UDT_NAME|DBTYPE_WSTR|O nome do UDT|  
|SS_UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|O AQN (nome de tipo completo) inclui o nome do tipo prefixado pelo namespace, se aplicável.|  
  
### <a name="ole-db-property-set-additions-and-changes"></a>Adições e alterações do conjunto de propriedades do OLE DB  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]O Native Client adiciona novos valores ou alterações a muitos dos principais conjuntos de propriedades de OLE DB.  
  
#### <a name="the-dbpropset_sqlserverparameter-property-set"></a>O conjunto de propriedades de DBPROPSET_SQLSERVERPARAMETER  
 Para dar suporte a UDTs por meio de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB, o Native Client implementa o novo conjunto de propriedades de DBPROPSET_SQLSERVERPARAMETER que contém os valores a seguir.  
  
|Nome|Type|Descrição|  
|----------|----------|-----------------|  
|SSPROP_PARAM_UDT_CATALOGNAME|DBTYPE_WSTR|O identificador de nome de três partes.<br /><br /> Para parâmetros de UDT, essa propriedade é uma cadeia de caracteres que especifica o nome do catálogo onde o tipo definido pelo usuário é definido.|  
|SSPROP_PARAM_UDT_SCHEMANAME|DBTYPE_WSTR|O identificador de nome de três partes.<br /><br /> Para parâmetros de UDT, essa propriedade é uma cadeia de caracteres que especifica o nome do esquema onde o tipo definido pelo usuário é definido.|  
|SSPROP_PARAM_UDT_NAME|DBTYPE_WSTR|O identificador de nome de três partes.<br /><br /> Para colunas de UDT, essa propriedade é uma cadeia de caracteres que especifica o nome de apenas uma parte do tipo definido pelo usuário.|  
  
 SSPROP_PARAM_UDT_NAME é obrigatório. SSPROP_PARAM_UDT_CATALOGNAME e SSPROP_PARAM_UDT_SCHEMANAME são opcionais. Se alguma propriedade for especificada incorretamente, o DB_E_ERRORSINCOMMAND será retornado. Se SSPROP_PARAM_UDT_CATALOGNAME e SSPROP_PARAM_UDT_SCHEMANAME não forem especificados, então o UDT deverá ser definido no mesmo banco de dados e esquema que a tabela. Se a definição de UDT não estiver no mesmo esquema que a tabela (mas estiver no mesmo banco de dados), então SSPROP_PARAM_UDT_SCHEMANAME deverá ser especificado. Se a definição de UDT estiver em um banco de dados diferente, SSPROP_PARAM_UDT_CATALOGNAME e SSPROP_PARAM_UDT_SCHEMANAME deverão ser especificados.  
  
#### <a name="the-dbpropset_sqlservercolumn-property-set"></a>O conjunto de propriedades de DBPROPSET_SQLSERVERCOLUMN  
 Para dar suporte à criação de tabelas na interface **ITableDefinition** , [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o Native Client adiciona as três novas colunas a seguir ao conjunto de propriedades DBPROPSET_SQLSERVERCOLUMN.  
  
|Nome|Descrição|Type|Descrição|  
|----------|-----------------|----------|-----------------|  
|SSPROP_COL_UDT_CATALOGNAME|UDT_CATALOGNAME|VT_BSTR|Para colunas de tipo DBTYPE_UDT, essa propriedade é uma cadeia de caracteres que especifica o nome do catálogo onde o UDT é definido.|  
|SSPROP_COL_UDT_SCHEMANAME|UDT_SCHEMANAME|VT_BSTR|Para colunas de tipo DBTYPE_UDT, essa propriedade é uma cadeia de caracteres que especifica o nome do esquema onde o UDT é definido.|  
|SSPROP_COL_UDT_NAME|UDT_NAME|VT_BSTR|Para colunas de tipo DBTYPE_UDT, essa propriedade é uma cadeia de caracteres que especifica o nome de apenas uma parte do UDT. Para outros tipos de coluna, essa propriedade retorna uma cadeia de caracteres vazia.|  
  
> [!NOTE]  
>  Os UDTs não aparecem no conjunto de linhas de esquema de PROVIDER_TYPES. Todas as colunas têm direito de leitura e gravação.  
  
 O ADO recorrerá a estas propriedades usando a entrada correspondente na coluna Descrição.  
  
 SSPROP_COL_UDTNAME é obrigatório. SSPROP_COL_UDT_CATALOGNAME e SSPROP_COL_UDT_SCHEMANAME são opcionais. Se qualquer uma das propriedades for especificada incorretamente, **DB_E_ERRORSINCOMMAND** será retornado.  
  
 Se SSPROP_COL_UDT_CATALOGNAME nem SSPROP_COL_UDT_SCHEMANAME forem especificados, o UDT deverá ser definido no mesmo banco de dados e esquema que a tabela.  
  
 Se a definição de UDT não estiver no mesmo esquema que a tabela (mas estiver no mesmo banco de dados), então SSPROP_COL_UDT_SCHEMANAME deverá ser especificado.  
  
 Se a definição de UDT estiver em um banco de dados diferente, SSPROP_COL_UDT_CATALOGNAME e SSPROP_COL_UDT_SCHEMANAME devem ser especificados.  
  
### <a name="ole-db-interface-additions-and-changes"></a>Adições e alterações de interface do OLE DB  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]O Native Client adiciona novos valores ou alterações a muitas das principais interfaces de OLE DB.  
  
#### <a name="the-isscommandwithparameters-interface"></a>A interface ISSCommandWithParameters  
 Para dar suporte a UDTs por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] meio de OLE DB, o Native Client implementa várias alterações, incluindo a adição da interface **ISSCommandWithParameters** . Essa nova interface herda as propriedades da interface principal do OLE DB **ICommandWithParameters**. Além dos três métodos herdados de **ICommandWithParameters**; **GetParameterInfo**, **MapParameterNames**e **SetParameterInfo**; **ISSCommandWithParameters** fornece os métodos **ParameterProperties** e **ParameterProperties** que são usados para tratar tipos de dados específicos do servidor.  
  
> [!NOTE]  
>  A interface **ISSCommandWithParameters** também usa a nova estrutura SSPARAMPROPS.  
  
#### <a name="the-icolumnsrowset-interface"></a>A interface IColumnsRowset  
 Além da interface **ISSCommandWithParameters** , [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o Native Client também adiciona novos valores ao conjunto de linhas retornado da chamada do método **IColumnsRowset:: GetColumnRowset** , incluindo o seguinte.  
  
|Nome da coluna|Type|Descrição|  
|-----------------|----------|-----------------|  
|DBCOLUMN_SS_UDT_CATALOGNAME|DBTYPE_WSTR|Um identificador do nome de catálogo do UDT.|  
|DBCOLUMN_SS_UDT_SCHEMANAME|DBTYPE_WSTR|Um identificador do nome do esquema do UDT.|  
|DBCOLUMN_SS_UDT_NAME|DBTYPE_WSTR|Um identificador de nome do UDT.|  
|DBCOLUMN_SS_ASSEMBLY_TYPENAME|DBTYPE_WSTR|O nome qualificado do assembly, que inclui o nome de tipo e toda a identificação de assembly necessários para referência pelo CLR.|  
  
 É possível diferenciar uma coluna de UDT do servidor de outros tipos binários quando DBCOLUMN_TYPE for definido como DBTYPE_UDT observando os metadados de UDT adicionados especificados acima. Se esses dados estiverem parcialmente completos, o tipo de servidor será um UDT. Para tipos de servidores não UDT, essas colunas são sempre retornadas como NULL.  
  
## <a name="sql-server-native-client-odbc-driver"></a>Driver ODBC do SQL Server Native Client  
 Várias alterações foram feitas no driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client para dar suporte a UDTs. O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Native Client mapeia [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o UDT para SQL_SS_UDT identificador de tipo de dados do SQL específico do driver. São exibidas colunas de UDT como SQL_SS_UDT. Se você mapear uma coluna UDT explicitamente para outro tipo em uma instrução SQL usando os métodos **ToString** ou **ToXmlString** do UDT ou por meio da função **Cast/Convert** , o tipo da coluna no conjunto de resultados refletirá o tipo real para o qual a coluna foi convertida  
  
### <a name="sqlcolattribute-sqldescribeparam-sqlgetdescfield"></a>SQLColAttribute, SQLDescribeParam, SQLGetDescField  
 Quatro novos campos de descritor específicos de driver foram adicionados para fornecer informações adicionais para uma coluna UDT de um conjunto de resultados, ou um parâmetro UDT da consulta de procedimento armazenado/parametrizada, a ser recuperada por meio das funções [SQLColAttribute](../../../relational-databases/native-client-odbc-api/sqlcolattribute.md), [SQLDescribeParam](../../../relational-databases/native-client-odbc-api/sqldescribeparam.md)e [SQLGetDescField](../../../relational-databases/native-client-odbc-api/sqlgetdescfield.md) .  
  
 Os quatro novos campos do descritor adicionados são SQL_CA_SS_UDT_CATALOG_NAME, SQL_CA_SS_UDT_SCHEMA_NAME, SQL_CA_SS_UDT_TYPE_NAME e SQL_CA_SS_UDT_ASSEMBLY_TYPE_NAME.  
  
### <a name="sqlcolumns-sqlprocedurecolumns"></a>SQLColumns, SQLProcedureColumns  
 Além disso, três novas colunas específicas de driver são adicionadas ao conjunto de resultados retornado das funções [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md) e [SQLProcedureColumns](../../../relational-databases/native-client-odbc-api/sqlprocedurecolumns.md) para fornecer informações adicionais sobre uma coluna de conjunto de resultados UDT ou um parâmetro UDT. Essas três colunas novas são SS_UDT_CATALOG_NAME, SS_UDT_SCHEMA_NAME e SS_UDT_ASSEMBLY_TYPE_NAME.  
  
### <a name="supported-conversions"></a>Conversões com suporte  
 Na conversão de tipos de dados SQL para C, é possível converter SQL_C_WCHAR, SQL_C_BINARY e SQL_C_CHAR a SQL_SS_UDT. Porém, observe que os dados binários são convertidos a uma cadeia de caracteres hexadecimais na conversão dos tipos de dados SQL_C_WCHAR e SQL_C_CHAR SQL.  
  
 Na conversão de tipos de dados C para SQL, é possível converter SQL_C_WCHAR, SQL_C_BINARY e SQL_C_CHAR a SQL_SS_UDT. No entanto, observe que os dados binários são convertidos em uma cadeia de caracteres hexadecimal durante a conversão dos tipos de dados SQL_C_WCHAR e SQL_C_CHAR SQL.  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos de SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
