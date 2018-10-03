---
title: Usando tipos definidos pelo usuário | Microsoft Docs
description: Usando tipos definidos pelo usuário com o Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- DBPROPSET_DATASOURCEINFO property set
- UDTs [OLE DB Driver for SQL Server]
- user-defined types [SQL Server], OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server, user-defined types
- DBPROPSET_SQLSERVERPARAMETER property set
- IColumnsRowset interface
- MSOLEDBSQL, user-defined types
- OLE DB Driver for SQL Server, user-defined types
- data access [OLE DB Driver for SQL Server], user-defined types
- ISSCommandWithParameters interface
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 8a5c362dff5b091461f7c88955dcabe309c3864a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47839544"
---
# <a name="using-user-defined-types"></a>Usando tipos definidos pelo usuário
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] introduziu os UDTs (tipos definidos pelo usuário). Os UDTs estendem o sistema de tipos SQL, permitindo que você armazene objetos e estruturas de dados personalizadas em um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Os UDTs podem conter vários tipos de dados e ter comportamentos, o que os diferencia dos tipos de dados de alias tradicionais, que consistem em um único tipo de dado do sistema [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. UDTs são definidos usando quaisquer dos idiomas com suporte pelo .NET CRL (Common Language Runtime) que gera código verificável. Isto inclui o Microsoft Visual C#<sup>®</sup> e Visual Basic<sup>®</sup> .NET. Os dados são expostos como campos e propriedades de uma classe ou estrutura .NET e os comportamentos são definidos pelos métodos da classe ou estrutura.  
  
 Um UDT pode ser usado como definição de coluna de uma tabela, como uma variável em um lote [!INCLUDE[tsql](../../../includes/tsql-md.md)], ou como um argumento de uma função [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou um procedimento armazenado.  
  
## <a name="ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server  
 O OLE DB Driver for SQL Server dá suporte a UDTs como tipos binários com informações de metadados, o que permite gerenciar UDTs como objetos. As colunas UDT são expostas como DBTYPE_UDT e seus metadados são expostos pela interface principal do OLE DB **IColumnRowset** e pela nova interface [ISSCommandWithParameters](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md).  
  
> [!NOTE]  
>  O método **IRowsetFind::FindNextRow** não funciona com o tipo de dados UDT. DB_E_BADCOMPAREOP será retornado se o UDT for usado como um tipo de coluna de pesquisa.  
  
### <a name="data-bindings-and-coercions"></a>Coerções e associações de dados  
 A tabela a seguir descreve a associação e a coerção que ocorrem ao usar os tipos de dados listados com o UDT [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Colunas de UDT são expostas por meio do Driver OLE DB para SQL Server como DBTYPE_UDT. Você pode obter metadados por meio dos conjuntos de linhas de esquema apropriados de forma que possa gerenciar seus próprios tipos definidos como objetos.  
  
|Tipo de dados|Para servidor<br /><br /> **UDT**|Para servidor<br /><br /> **não UDT**|Do servidor<br /><br /> **UDT**|Do servidor<br /><br /> **não UDT**|  
|---------------|---------------------------|--------------------------------|-----------------------------|----------------------------------|  
|DBTYPE_UDT|Suporte para<sup>6</sup>|Erro<sup>1</sup>|Suporte para<sup>6</sup>|Erro<sup>5</sup>|  
|DBTYPE_BYTES|Suporte para<sup>6</sup>|N/D<sup>2</sup>|Suporte para<sup>6</sup>|N/D<sup>2</sup>|  
|DBTYPE_WSTR|Suporte para<sup>3,6</sup>|N/D<sup>2</sup>|Suporte para<sup>4,6</sup>|N/D<sup>2</sup>|  
|DBTYPE_BSTR|Suporte para<sup>3,6</sup>|N/D<sup>2</sup>|Suporte para<sup>4</sup>|N/D<sup>2</sup>|  
|DBTYPE_STR|Suporte para<sup>3,6</sup>|N/D<sup>2</sup>|Suporte para<sup>4,6</sup>|N/D<sup>2</sup>|  
|DBTYPE_IUNKNOWN|Sem suporte|N/D<sup>2</sup>|Sem suporte|N/D<sup>2</sup>|  
|DBTYPE_VARIANT (VT_UI1 &#124; VT_ARRAY)|Suporte para<sup>6</sup>|N/D<sup>2</sup>|Suporte para<sup>4</sup>|N/D<sup>2</sup>|  
|DBTYPE_VARIANT (VT_BSTR)|Suporte para<sup>3,6</sup>|N/D<sup>2</sup>|N/A|N/D<sup>2</sup>|  
  
 <sup>1</sup>Se um tipo de servidor diferente de DBTYPE_UDT for especificado com **ICommandWithParameters::SetParameterInfo** e o tipo de acessador for DBTYPE_UDT, ocorrerá um erro quando a instrução for executada (para DB_E_ERRORSOCCURRED, o status do parâmetro é DBSTATUS_E_BADACCESSOR). Caso contrário, os dados serão enviados para o servidor, mas ele retornará um erro indicando que não há conversão implícita do UDT para o tipo de dados do parâmetro.  
  
 <sup>2</sup>Além do escopo deste artigo.  
  
 <sup>3</sup> Ocorre a conversão de dados de cadeia de caracteres hexadecimal para dados binários.  
  
 <sup>4</sup> Ocorre a conversão de dados binários para cadeia de caracteres hexadecimal.  
  
 <sup>5</sup>Pode ocorrer a validação no momento de criação do acessador ou, no momento do fetch, o erro é DB_E_ERRORSOCCURRED, o status de associação está definido como DBBINDSTATUS_UNSUPPORTEDCONVERSION.  
  
 <sup>6</sup>BY_REF pode ser usado.  
  
 DBTYPE_NULL e DBTYPE_EMPTY podem ser associados a parâmetros de entrada, mas não a parâmetros ou resultados de saída. Quando eles são associados a parâmetros de entrada, o status precisa ser definido como DBSTATUS_S_ISNULL ou DBSTATUS_S_DEFAULT.  
  
 DBTYPE_UDT pode ser convertido em DBTYPE_EMPTY e DBTYPE_NULL, porém DBTYPE_NULL e DBTYPE_EMPTY não podem ser convertidos em DBTYPE_UDT. Isso é consistente com DBTYPE_BYTES.  
  
> [!NOTE]  
>  Uma nova interface é usada para lidar com UDTs como parâmetros, **ISSCommandWithParameters**, herdada de **ICommandWithParameters**. Os aplicativos devem usar esta interface para definir pelo menos o SSPROP_PARAM_UDT_NAME da propriedade DBPROPSET_SQLSERVERPARAMETER definida para os parâmetros de UDT. Se isto não for feito, **ICommand::Execute** retornará DB_E_ERRORSOCCURRED. Essa interface e o conjunto de propriedades são descritos mais adiante neste artigo.  
  
 Se um tipo definido pelo usuário for inserido em uma coluna que não seja grande o suficiente para manter todos os dados, **ICommand::Execute** retornará S_OK com o status DB_E_ERRORSOCCURRED.  
  
 As conversões de dados fornecidas pelos serviços principais do OLE DB (**IDataConvert**) não são aplicáveis a DBTYPE_UDT. As demais associações não têm suporte.  
  
### <a name="ole-db-rowset-additions-and-changes"></a>Adições e alterações do conjunto de linhas do OLE DB  
 Driver do OLE DB para SQL Server adiciona novos valores ou alterações em muitos dos principais conjuntos de linhas de esquema OLE DB.  
  
#### <a name="the-procedureparameters-schema-rowset"></a>O conjunto de linhas do esquema PROCEDURE_PARAMETERS  
 As adições a seguir foram feitas ao conjunto de linhas de esquema de PROCEDURE_PARAMETERS.  
  
|Nome da coluna|Tipo|Descrição|  
|-----------------|----------|-----------------|  
|SS_UDT_CATALOGNAME|DBTYPE_WSTR|O identificador de nome de três partes.|  
|SS_UDT_SCHEMANAME|DBTYPE_WSTR|O identificador de nome de três partes.|  
|SS_UDT_NAME|DBTYPE_WSTR|O identificador de nome de três partes.|  
|SS_UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|O Nome Qualificado do Assembly, que inclui o nome de tipo e toda a identificação de assembly necessários para referência pelo CLR.|  
  
#### <a name="the-sqlassemblies-schema-rowset"></a>O conjunto de linhas do esquema SQL_ASSEMBLIES  
 O OLE DB Driver for SQL Server expõe um novo conjunto de linhas de esquema específico do provedor que descreve os UDTs registrados. O servidor de ASSEMBLY pode ser especificado como um DBTYPE_WSTR, mas não está presente no conjunto de linhas. Se não estiver especificado, o conjunto de linhas seguirá o padrão do servidor atual. O conjunto de linhas de esquema de SQL_ASSEMBLIES é definido na seguinte tabela:  
  
|Nome da coluna|Tipo|Descrição|  
|-----------------|----------|-----------------|  
|ASSEMBLY_CATALOG|DBTYPE_WSTR|O nome de catálogo do assembly que contém o tipo.|  
|ASSEMBLY_SCHEMA|DBTYPE_WSTR|O nome do esquema ou nome do proprietário do assembly que contém o tipo. Embora os assemblies tenham escopo por banco de dados e não por esquema, eles ainda têm um proprietário que é refletido aqui.|  
|ASSEMBLY_NAME|DBTYPE_WSTR|O nome do assembly que contém o tipo.|  
|ASSEMBLY_ID|DBTYPE_UI4|A ID de objeto do assembly que contém o tipo.|  
|PERMISSION_SET|DBTYPE_WSTR|Um valor que indica o escopo de acesso para o assembly. Valores incluem "SAFE", "EXTERNAL_ACCESS" e "UNSAFE".|  
|ASSEMBLY_BINARY|DBTYPE_BYTES|A representação binária do assembly.|  
  
#### <a name="the-sqlassemblies-dependencies-schema-rowset"></a>O conjunto de linhas do esquema SQL_ASSEMBLIES_ DEPENDENCIES  
 O OLE DB Driver for SQL Server expõe um novo conjunto de linhas de esquema específico do provedor que descreve as dependências de assembly para um servidor especificado. O ASSEMBLY_SERVER pode ser especificado pelo chamador como um DBTYPE_WSTR, mas não está presente no conjunto de linhas. Se não estiver especificado, o conjunto de linhas seguirá o padrão do servidor atual. O conjunto de linhas de esquema de SQL_ASSEMBLY_DEPENDENCIES é definido na seguinte tabela:  
  
|Nome da coluna|Tipo|Descrição|  
|-----------------|----------|-----------------|  
|ASSEMBLY_CATALOG|DBTYPE_WSTR|O nome de catálogo do assembly que contém o tipo.|  
|ASSEMBLY_SCHEMA|DBTYPE_WSTR|O nome do esquema ou nome do proprietário do assembly que contém o tipo. Embora os assemblies tenham escopo por banco de dados e não por esquema, eles ainda têm um proprietário, que é refletido aqui.|  
|ASSEMBLY_ID|DBTYPE_UI4|A ID de objeto do assembly.|  
|REFERENCED_ASSEMBLY_ID|DBTYPE_UI4|A ID de objeto do assembly referenciado.|  
  
#### <a name="the-sqlusertypes-schema-rowset"></a>O conjunto de linhas do esquema SQL_USER_TYPES  
 O OLE DB Driver for SQL Server expõe um novo conjunto de linhas de esquema, SQL_USER_TYPES, que descreve quando os UDTs registrados para um servidor especificado são adicionados. O UDT_SERVER deve ser especificado pelo chamador como um DBTYPE_WSTR, mas não está presente no conjunto de linhas. O conjunto de linhas de esquema de SQL_USER_TYPES é definido na tabela a seguir.  
  
|Nome da coluna|Tipo|Descrição|  
|-----------------|----------|-----------------|  
|UDT_CATALOGNAME|DBTYPE_WSTR|Para colunas UDT, essa propriedade é uma cadeia de caracteres que especifica o nome do catálogo em que o UDT é definido.|  
|UDT_SCHEMANAME|DBTYPE_WSTR|Para colunas UDT, essa propriedade é uma cadeia de caracteres que especifica o nome do esquema em que o UDT é definido.|  
|UDT_NAME|DBTYPE_WSTR|O nome do assembly que contém a classe do UDT.|  
|UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|O AQN (nome de tipo completo) inclui o nome do tipo prefixado pelo namespace, se aplicável.|  
  
#### <a name="the-columns-schema-rowset"></a>O conjunto de linhas do esquema COLUMNS  
 As adições ao conjunto de linhas de esquema COLUMNS incluem as seguintes colunas:  
  
|Nome da coluna|Tipo|Descrição|  
|-----------------|----------|-----------------|  
|SS_UDT_CATALOGNAME|DBTYPE_WSTR|Para colunas UDT, essa propriedade é uma cadeia de caracteres que especifica o nome do catálogo em que o UDT é definido.|  
|SS_UDT_SCHEMANAME|DBTYPE_WSTR|Para colunas UDT, essa propriedade é uma cadeia de caracteres que especifica o nome do esquema em que o UDT é definido.|  
|SS_UDT_NAME|DBTYPE_WSTR|O nome do UDT|  
|SS_UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|O AQN (nome de tipo completo) inclui o nome do tipo prefixado pelo namespace, se aplicável.|  
  
### <a name="ole-db-property-set-additions-and-changes"></a>Adições e alterações do conjunto de propriedades do OLE DB  
 Driver do OLE DB para SQL Server adiciona novos valores ou alterações a muitos dos principais propriedade OLE DB conjuntos.  
  
#### <a name="the-dbpropsetsqlserverparameter-property-set"></a>O conjunto de propriedades de DBPROPSET_SQLSERVERPARAMETER  
 Para dar suporte aos UDTs por meio do OLE DB, o OLE DB Driver for SQL Server implementa o novo conjunto de propriedades DBPROPSET_SQLSERVERPARAMETER, que contém os seguintes valores:  
  
|Nome|Tipo|Descrição|  
|----------|----------|-----------------|  
|SSPROP_PARAM_UDT_CATALOGNAME|DBTYPE_WSTR|O identificador de nome de três partes.<br /><br /> Para parâmetros de UDT, essa propriedade é uma cadeia de caracteres que especifica o nome do catálogo onde o tipo definido pelo usuário é definido.|  
|SSPROP_PARAM_UDT_SCHEMANAME|DBTYPE_WSTR|O identificador de nome de três partes.<br /><br /> Para parâmetros de UDT, essa propriedade é uma cadeia de caracteres que especifica o nome do esquema onde o tipo definido pelo usuário é definido.|  
|SSPROP_PARAM_UDT_NAME|DBTYPE_WSTR|O identificador de nome de três partes.<br /><br /> Para colunas de UDT, essa propriedade é uma cadeia de caracteres que especifica o nome de apenas uma parte do tipo definido pelo usuário.|  
  
 SSPROP_PARAM_UDT_NAME é obrigatório. SSPROP_PARAM_UDT_CATALOGNAME e SSPROP_PARAM_UDT_SCHEMANAME são opcionais. Se uma das propriedades for especificada incorretamente, DB_E_ERRORSINCOMMAND será retornado. Se SSPROP_PARAM_UDT_CATALOGNAME e SSPROP_PARAM_UDT_SCHEMANAME não forem especificados, então o UDT deverá ser definido no mesmo banco de dados e esquema que a tabela. Se a definição de UDT não estiver no mesmo esquema que a tabela (mas estiver no mesmo banco de dados), então SSPROP_PARAM_UDT_SCHEMANAME deverá ser especificado. Se a definição de UDT estiver em um banco de dados diferente, SSPROP_PARAM_UDT_CATALOGNAME e SSPROP_PARAM_UDT_SCHEMANAME precisarão ser especificados.  
  
#### <a name="the-dbpropsetsqlservercolumn-property-set"></a>O conjunto de propriedades de DBPROPSET_SQLSERVERCOLUMN  
 Para dar suporte à criação de tabelas na interface **ITableDefinition**, o OLE DB Driver for SQL Server adiciona as três novas colunas a seguir ao conjunto de propriedades DBPROPSET_SQLSERVERCOLUMN.  
  
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
 Driver do OLE DB para SQL Server adiciona novos valores ou alterações em muitos dos principais que interfaces OLE DB.  
  
#### <a name="the-isscommandwithparameters-interface"></a>A interface ISSCommandWithParameters  
 Para dar suporte aos UDTs por meio do OLE DB, o OLE DB Driver for SQL Server implementa várias alterações, incluindo a adição da interface **ISSCommandWithParameters**. Essa nova interface herda as propriedades da interface principal do OLE DB **ICommandWithParameters**. Além dos três métodos herdados de **ICommandWithParameters**; **GetParameterInfo**, **MapParameterNames** e **SetParameterInfo**; **ISSCommandWithParameters** fornece os métodos **GetParameterProperties** e **SetParameterProperties** usados para manipular tipos de dados específicos de servidor.  
  
> [!NOTE]  
>  A interface **ISSCommandWithParameters** também usa a nova estrutura SSPARAMPROPS.  
  
#### <a name="the-icolumnsrowset-interface"></a>A interface IColumnsRowset  
 Além da interface **ISSCommandWithParameters**, o OLE DB Driver for SQL Server também adiciona novos valores ao conjunto de linhas retornado da chamada ao método **IColumnsRowset::GetColumnRowset**, incluindo o mostrado a seguir.  
  
|Nome da coluna|Tipo|Descrição|  
|-----------------|----------|-----------------|  
|DBCOLUMN_SS_UDT_CATALOGNAME|DBTYPE_WSTR|Um identificador do nome de catálogo do UDT.|  
|DBCOLUMN_SS_UDT_SCHEMANAME|DBTYPE_WSTR|Um identificador do nome do esquema do UDT.|  
|DBCOLUMN_SS_UDT_NAME|DBTYPE_WSTR|Um identificador de nome do UDT.|  
|DBCOLUMN_SS_ASSEMBLY_TYPENAME|DBTYPE_WSTR|O nome qualificado do assembly, que inclui o nome de tipo e toda a identificação de assembly necessários para referência pelo CLR.|  
  
 É possível diferenciar uma coluna UDT do servidor de outros tipos binários quando DBCOLUMN_TYPE é definido como DBTYPE_UDT observando os metadados de UDT adicionados especificados na tabela anterior. Se esses dados estiverem parcialmente completos, o tipo de servidor será um UDT. Para tipos de servidores não UDT, essas colunas são sempre retornadas como NULL.  
 
  
## <a name="see-also"></a>Consulte Também  
 [Recursos do OLE DB Driver for SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)    
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
