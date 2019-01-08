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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 14e14c23741f5473e6c9eaae46140a2f7a0668bb
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52406173"
---
# <a name="using-user-defined-types"></a>Usando tipos definidos pelo usuário
[!INCLUDE[appliesto-ss-asdb-xxxx-pdw-md](../../../includes/appliesto-ss-asdb-xxxx-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  O [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] introduziu os UDTs (tipos definidos pelo usuário). Os UDTs estendem o sistema de tipos SQL, permitindo que você armazene objetos e estruturas de dados personalizadas em um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Os UDTs podem conter vários tipos de dados e ter comportamentos, o que os diferencia dos tipos de dados de alias tradicionais, que consistem em um único tipo de dado do sistema no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. UDTs são definidos usando quaisquer dos idiomas com suporte pelo .NET CRL (Common Language Runtime) que gera código verificável. Isto inclui o Microsoft Visual C#<sup>®</sup> e Visual Basic<sup>®</sup> .NET. Os dados são expostos como campos e propriedades de uma classe ou estrutura .NET e os comportamentos são definidos pelos métodos da classe ou estrutura.  
  
 Um UDT pode ser usado como definição de coluna de uma tabela, como uma variável em um lote [!INCLUDE[tsql](../../../includes/tsql-md.md)], ou como um argumento de uma função [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou um procedimento armazenado.  
  
## <a name="sql-server-native-client-ole-db-provider"></a>Provedor OLE DB do SQL Server Native Client  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client dá suporte a UDTs como tipos binários com informações de metadados, que lhe permite gerenciar UDTs como objetos. As colunas UDT são expostas como DBTYPE_UDT e seus metadados são expostos pela interface principal do OLE DB **IColumnRowset** e pela nova interface [ISSCommandWithParameters](../../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md).  
  
> [!NOTE]  
>  O método **IRowsetFind::FindNextRow** não funciona com o tipo de dados UDT. DB_E_BADCOMPAREOP será retornado se o UDT for usado como um tipo de coluna de pesquisa.  
  
### <a name="data-bindings-and-coercions"></a>Coerções e associações de dados  
 A tabela a seguir descreve a associação e a coerção que ocorrem ao usar os tipos de dados listados com o UDT [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Colunas de UDT são expostas por meio de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client como DBTYPE_UDT. Você pode obter metadados por meio dos conjuntos de linhas de esquema apropriados de forma que possa gerenciar seus próprios tipos definidos como objetos.  
  
|Tipo de dados|Para servidor<br /><br /> **UDT**|Para servidor<br /><br /> **non-UDT**|Do servidor<br /><br /> **UDT**|Do servidor<br /><br /> **non-UDT**|  
|---------------|---------------------------|--------------------------------|-----------------------------|----------------------------------|  
|DBTYPE_UDT|Suporte para<sup>6</sup>|Erro<sup>1</sup>|Suporte para<sup>6</sup>|Erro<sup>5</sup>|  
|DBTYPE_BYTES|Suporte para<sup>6</sup>|N/D<sup>2</sup>|Suporte para<sup>6</sup>|N/D<sup>2</sup>|  
|DBTYPE_WSTR|Suporte para<sup>3,6</sup>|N/D<sup>2</sup>|Suporte para<sup>4,6</sup>|N/D<sup>2</sup>|  
|DBTYPE_BSTR|Suporte para<sup>3,6</sup>|N/D<sup>2</sup>|Suporte para<sup>4</sup>|N/D<sup>2</sup>|  
|DBTYPE_STR|Suporte para<sup>3,6</sup>|N/D<sup>2</sup>|Suporte para<sup>4,6</sup>|N/D<sup>2</sup>|  
|DBTYPE_IUNKNOWN|Sem suporte|N/D<sup>2</sup>|Sem suporte|N/D<sup>2</sup>|  
|DBTYPE_VARIANT (VT_UI1 &#124; VT_ARRAY)|Suporte para<sup>6</sup>|N/D<sup>2</sup>|Suporte para<sup>4</sup>|N/D<sup>2</sup>|  
|DBTYPE_VARIANT (VT_BSTR)|Suporte para<sup>3,6</sup>|N/D<sup>2</sup>|N/D|N/D<sup>2</sup>|  
  
 <sup>1</sup>Se um tipo de servidor diferente de DBTYPE_UDT for especificado com **ICommandWithParameters::SetParameterInfo** e o tipo de acessador for DBTYPE_UDT, ocorrerá um erro quando a instrução for executada (para DB_E_ERRORSOCCURRED, o status do parâmetro é DBSTATUS_E_BADACCESSOR). Caso contrário, os dados são enviados ao servidor, mas o servidor retornará um erro indicando que não há nenhuma conversão implícita do UDT para o tipo de dados do parâmetro.  
  
 <sup>2</sup>além do escopo deste tópico.  
  
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
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client adiciona novos valores ou alterações a muitos dos principais conjuntos de linhas de esquema OLE DB.  
  
#### <a name="the-procedureparameters-schema-rowset"></a>O conjunto de linhas do esquema PROCEDURE_PARAMETERS  
 As adições a seguir foram feitas ao conjunto de linhas de esquema de PROCEDURE_PARAMETERS.  
  
|Nome da coluna|Tipo|Descrição|  
|-----------------|----------|-----------------|  
|SS_UDT_CATALOGNAME|DBTYPE_WSTR|O identificador de nome de três partes.|  
|SS_UDT_SCHEMANAME|DBTYPE_WSTR|O identificador de nome de três partes.|  
|SS_UDT_NAME|DBTYPE_WSTR|O identificador de nome de três partes.|  
|SS_UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|O Nome Qualificado do Assembly, que inclui o nome de tipo e toda a identificação de assembly necessários para referência pelo CLR.|  
  
#### <a name="the-sqlassemblies-schema-rowset"></a>O conjunto de linhas do esquema SQL_ASSEMBLIES  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client expõe um conjunto de linhas de esquema específico provedor novo que descreve os UDTs registrados. O servidor de ASSEMBLY pode ser especificado como um DBTYPE_WSTR, mas não está presente no conjunto de linhas. Se não estiver especificado, o conjunto de linhas seguirá o padrão do servidor atual. O conjunto de linhas de esquema de SQL_ASSEMBLIES é definido na tabela a seguir.  
  
|Nome da coluna|Tipo|Descrição|  
|-----------------|----------|-----------------|  
|ASSEMBLY_CATALOG|DBTYPE_WSTR|O nome de catálogo do assembly que contém o tipo.|  
|ASSEMBLY_SCHEMA|DBTYPE_WSTR|O nome do esquema ou nome do proprietário do assembly que contém o tipo. Embora os assemblies tenham escopo por banco de dados e não por esquema, eles ainda têm um proprietário que é refletido aqui.|  
|ASSEMBLY_NAME|DBTYPE_WSTR|O nome do assembly que contém o tipo.|  
|ASSEMBLY_ID|DBTYPE_UI4|A id do objeto do assembly que contém o tipo.|  
|PERMISSION_SET|DBTYPE_WSTR|Um valor que indica o escopo de acesso para o assembly. Valores incluem "SAFE", "EXTERNAL_ACCESS" e "UNSAFE".|  
|ASSEMBLY_BINARY|DBTYPE_BYTES|A representação binária do assembly.|  
  
#### <a name="the-sqlassemblies-dependencies-schema-rowset"></a>O conjunto de linhas do esquema SQL_ASSEMBLIES_ DEPENDENCIES  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Provedor do OLE DB nativo expõe um novo conjunto de linhas específicas do provedor de esquema que descreve as dependências de assembly para um servidor especificado. O ASSEMBLY_SERVER pode ser especificado pelo chamador como um DBTYPE_WSTR, mas não está presente no conjunto de linhas. Se não estiver especificado, o conjunto de linhas seguirá o padrão do servidor atual. O conjunto de linhas de esquema de SQL_ASSEMBLY_DEPENDENCIES é definido na tabela a seguir.  
  
|Nome da coluna|Tipo|Descrição|  
|-----------------|----------|-----------------|  
|ASSEMBLY_CATALOG|DBTYPE_WSTR|O nome de catálogo do assembly que contém o tipo.|  
|ASSEMBLY_SCHEMA|DBTYPE_WSTR|O nome do esquema ou nome do proprietário do assembly que contém o tipo. Embora os assemblies tenham escopo por banco de dados e não por esquema, eles ainda têm um proprietário, que é refletido aqui.|  
|ASSEMBLY_ID|DBTYPE_UI4|A id do objeto do assembly.|  
|REFERENCED_ASSEMBLY_ID|DBTYPE_UI4|A id do objeto do assembly referenciado.|  
  
#### <a name="the-sqlusertypes-schema-rowset"></a>O conjunto de linhas do esquema SQL_USER_TYPES  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Provedor do OLE DB nativo expõe novas linhas de esquema, o SQL_USER_TYPES, que descreve quando os UDTs registrados para um servidor especificado é adicionado. O UDT_SERVER deve ser especificado pelo chamador como um DBTYPE_WSTR, mas não está presente no conjunto de linhas. O conjunto de linhas de esquema de SQL_USER_TYPES é definido na tabela a seguir.  
  
|Nome da coluna|Tipo|Descrição|  
|-----------------|----------|-----------------|  
|UDT_CATALOGNAME|DBTYPE_WSTR|Para colunas de UDT esta propriedade é uma cadeia de caracteres que especifica o nome do catálogo onde o UDT é definido.|  
|UDT_SCHEMANAME|DBTYPE_WSTR|Para colunas de UDT esta propriedade é uma cadeia de caracteres que especifica o nome do esquema onde o UDT é definido.|  
|UDT_NAME|DBTYPE_WSTR|O nome do assembly que contém a classe do UDT.|  
|UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|O AQN (nome de tipo completo) inclui o nome do tipo prefixado pelo namespace, se aplicável.|  
  
#### <a name="the-columns-schema-rowset"></a>O conjunto de linhas do esquema COLUMNS  
 Adições para o conjunto de linhas de esquema de COLUMNS incluem as colunas a seguir.  
  
|Nome da coluna|Tipo|Descrição|  
|-----------------|----------|-----------------|  
|SS_UDT_CATALOGNAME|DBTYPE_WSTR|Para colunas de UDT esta propriedade é uma cadeia de caracteres que especifica o nome do catálogo onde o UDT é definido.|  
|SS_UDT_SCHEMANAME|DBTYPE_WSTR|Para colunas de UDT esta propriedade é uma cadeia de caracteres que especifica o nome do esquema onde o UDT é definido.|  
|SS_UDT_NAME|DBTYPE_WSTR|O nome do UDT|  
|SS_UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|O AQN (nome de tipo completo) inclui o nome do tipo prefixado pelo namespace, se aplicável.|  
  
### <a name="ole-db-property-set-additions-and-changes"></a>Adições e alterações do conjunto de propriedades do OLE DB  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client adiciona novos valores ou alterações a muitos dos principais propriedade OLE DB conjuntos.  
  
#### <a name="the-dbpropsetsqlserverparameter-property-set"></a>O conjunto de propriedades de DBPROPSET_SQLSERVERPARAMETER  
 Para dar suporte a UDTs através do OLE DB, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client implementa o novo conjunto de propriedades DBPROPSET_SQLSERVERPARAMETER que contém os valores a seguir.  
  
|Nome|Tipo|Descrição|  
|----------|----------|-----------------|  
|SSPROP_PARAM_UDT_CATALOGNAME|DBTYPE_WSTR|O identificador de nome de três partes.<br /><br /> Para parâmetros de UDT, essa propriedade é uma cadeia de caracteres que especifica o nome do catálogo onde o tipo definido pelo usuário é definido.|  
|SSPROP_PARAM_UDT_SCHEMANAME|DBTYPE_WSTR|O identificador de nome de três partes.<br /><br /> Para parâmetros de UDT, essa propriedade é uma cadeia de caracteres que especifica o nome do esquema onde o tipo definido pelo usuário é definido.|  
|SSPROP_PARAM_UDT_NAME|DBTYPE_WSTR|O identificador de nome de três partes.<br /><br /> Para colunas de UDT, essa propriedade é uma cadeia de caracteres que especifica o nome de apenas uma parte do tipo definido pelo usuário.|  
  
 SSPROP_PARAM_UDT_NAME é obrigatório. SSPROP_PARAM_UDT_CATALOGNAME e SSPROP_PARAM_UDT_SCHEMANAME são opcionais. Se alguma propriedade for especificada incorretamente, o DB_E_ERRORSINCOMMAND será retornado. Se SSPROP_PARAM_UDT_CATALOGNAME e SSPROP_PARAM_UDT_SCHEMANAME não forem especificados, então o UDT deverá ser definido no mesmo banco de dados e esquema que a tabela. Se a definição de UDT não estiver no mesmo esquema que a tabela (mas estiver no mesmo banco de dados), então SSPROP_PARAM_UDT_SCHEMANAME deverá ser especificado. Se a definição de UDT estiver em um banco de dados diferente, SSPROP_PARAM_UDT_CATALOGNAME e SSPROP_PARAM_UDT_SCHEMANAME deverão ser especificados.  
  
#### <a name="the-dbpropsetsqlservercolumn-property-set"></a>O conjunto de propriedades de DBPROPSET_SQLSERVERCOLUMN  
 Para dar suporte à criação de tabelas na **ITableDefinition** interface, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client adiciona três novas colunas a seguir para propriedades de dbpropset_sqlservercolumn.  
  
|Nome|Descrição|Tipo|Descrição|  
|----------|-----------------|----------|-----------------|  
|SSPROP_COL_UDT_CATALOGNAME|UDT_CATALOGNAME|VT_BSTR|Para colunas de tipo DBTYPE_UDT, essa propriedade é uma cadeia de caracteres que especifica o nome do catálogo onde o UDT é definido.|  
|SSPROP_COL_UDT_SCHEMANAME|UDT_SCHEMANAME|VT_BSTR|Para colunas de tipo DBTYPE_UDT, essa propriedade é uma cadeia de caracteres que especifica o nome do esquema onde o UDT é definido.|  
|SSPROP_COL_UDT_NAME|UDT_NAME|VT_BSTR|Para colunas de tipo DBTYPE_UDT, essa propriedade é uma cadeia de caracteres que especifica o nome de apenas uma parte do UDT. Para outros tipos de coluna, essa propriedade retorna uma cadeia de caracteres vazia.|  
  
> [!NOTE]  
>  Os UDTs não aparecem no conjunto de linhas de esquema de PROVIDER_TYPES. Todas as colunas têm direito de leitura e gravação.  
  
 O ADO recorrerá a estas propriedades usando a entrada correspondente na coluna Descrição.  
  
 SSPROP_COL_UDTNAME é obrigatório. SSPROP_COL_UDT_CATALOGNAME e SSPROP_COL_UDT_SCHEMANAME são opcionais. Se uma das propriedades for especificada incorretamente, **DB_E_ERRORSINCOMMAND** será retornado.  
  
 Se SSPROP_COL_UDT_CATALOGNAME nem SSPROP_COL_UDT_SCHEMANAME forem especificados, o UDT deverá ser definido no mesmo banco de dados e esquema que a tabela.  
  
 Se a definição de UDT não estiver no mesmo esquema que a tabela (mas estiver no mesmo banco de dados), então SSPROP_COL_UDT_SCHEMANAME deverá ser especificado.  
  
 Se a definição de UDT estiver em um banco de dados diferente, SSPROP_COL_UDT_CATALOGNAME e SSPROP_COL_UDT_SCHEMANAME devem ser especificados.  
  
### <a name="ole-db-interface-additions-and-changes"></a>Adições e alterações de interface do OLE DB  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client adiciona novos valores ou alterações a muitos dos principais que interfaces OLE DB.  
  
#### <a name="the-isscommandwithparameters-interface"></a>A interface ISSCommandWithParameters  
 Para dar suporte a UDTs através do OLE DB, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client implementa várias alterações, incluindo a adição do **ISSCommandWithParameters** interface. Essa nova interface herda as propriedades da interface principal do OLE DB **ICommandWithParameters**. Além dos três métodos herdados de **ICommandWithParameters**; **GetParameterInfo**, **MapParameterNames**, e **SetParameterInfo**; **ISSCommandWithParameters** fornece o **GetParameterProperties** e **SetParameterProperties** métodos que são usados para lidar com o servidor específico tipos de dados.  
  
> [!NOTE]  
>  A interface **ISSCommandWithParameters** também usa a nova estrutura SSPARAMPROPS.  
  
#### <a name="the-icolumnsrowset-interface"></a>A interface IColumnsRowset  
 Além de **ISSCommandWithParameters** interface, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client adiciona novos valores no conjunto de linhas retornado ao chamar o **IColumnsRowset:: Getcolumnrowset** método incluindo o seguinte.  
  
|Nome da coluna|Tipo|Descrição|  
|-----------------|----------|-----------------|  
|DBCOLUMN_SS_UDT_CATALOGNAME|DBTYPE_WSTR|Um identificador do nome de catálogo do UDT.|  
|DBCOLUMN_SS_UDT_SCHEMANAME|DBTYPE_WSTR|Um identificador do nome do esquema do UDT.|  
|DBCOLUMN_SS_UDT_NAME|DBTYPE_WSTR|Um identificador de nome do UDT.|  
|DBCOLUMN_SS_ASSEMBLY_TYPENAME|DBTYPE_WSTR|O nome qualificado do assembly, que inclui o nome de tipo e toda a identificação de assembly necessários para referência pelo CLR.|  
  
 É possível diferenciar uma coluna de UDT do servidor de outros tipos binários quando DBCOLUMN_TYPE for definido como DBTYPE_UDT observando os metadados de UDT adicionados especificados acima. Se esses dados estiverem parcialmente completos, o tipo de servidor será um UDT. Para tipos de servidores não UDT, essas colunas são sempre retornadas como NULL.  
  
## <a name="sql-server-native-client-odbc-driver"></a>Driver ODBC do SQL Server Native Client  
 Inúmeras alterações foram feitas no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client para dar suporte a UDTs. O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mapas de driver ODBC do Native Client a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] identificador de tipo UDT para dados SQL específica do driver SQL_SS_UDT. São exibidas colunas de UDT como SQL_SS_UDT. Se você mapear uma coluna UDT explicitamente para outro tipo em uma instrução SQL usando o **ToString** ou **ToXMLString** métodos de UDT ou por meio de **CAST/CONVERT** função, o tipo da coluna no resultado do conjunto reflete o tipo real, em que a coluna foi convertida  
  
### <a name="sqlcolattribute-sqldescribeparam-sqlgetdescfield"></a>SQLColAttribute, SQLDescribeParam, SQLGetDescField  
 Quatro novos campos de descritor específicos de driver foram adicionados para fornecer informações adicionais para uma coluna UDT de um conjunto de resultados, ou um parâmetro UDT de consulta parametrizada/de procedimento, a ser recuperado por meio de [SQLColAttribute](../../../relational-databases/native-client-odbc-api/sqlcolattribute.md), [SQLDescribeParam](../../../relational-databases/native-client-odbc-api/sqldescribeparam.md), e [SQLGetDescField](../../../relational-databases/native-client-odbc-api/sqlgetdescfield.md) funções.  
  
 Os quatro novos campos do descritor adicionados são SQL_CA_SS_UDT_CATALOG_NAME, SQL_CA_SS_UDT_SCHEMA_NAME, SQL_CA_SS_UDT_TYPE_NAME e SQL_CA_SS_UDT_ASSEMBLY_TYPE_NAME.  
  
### <a name="sqlcolumns-sqlprocedurecolumns"></a>SQLColumns, SQLProcedureColumns  
 Além disso, três novas colunas específicas do driver foram adicionadas ao conjunto de resultados retornado do [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md) e [SQLProcedureColumns](../../../relational-databases/native-client-odbc-api/sqlprocedurecolumns.md) funções para fornecer mais informações sobre a resultados de UDT conjunto de colunas ou um parâmetro UDT. Essas três colunas novas são SS_UDT_CATALOG_NAME, SS_UDT_SCHEMA_NAME e SS_UDT_ASSEMBLY_TYPE_NAME.  
  
### <a name="supported-conversions"></a>Conversões com suporte  
 Na conversão de tipos de dados SQL para C, é possível converter SQL_C_WCHAR, SQL_C_BINARY e SQL_C_CHAR a SQL_SS_UDT. Porém, observe que os dados binários são convertidos a uma cadeia de caracteres hexadecimais na conversão dos tipos de dados SQL_C_WCHAR e SQL_C_CHAR SQL.  
  
 Na conversão de tipos de dados C para SQL, é possível converter SQL_C_WCHAR, SQL_C_BINARY e SQL_C_CHAR a SQL_SS_UDT. No entanto, observe que os dados binários são convertidos em uma cadeia de caracteres hexadecimal durante a conversão de tipos de dados SQL_C_WCHAR e SQL_C_CHAR SQL.  
  
## <a name="see-also"></a>Consulte também  
 [Recursos do SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
