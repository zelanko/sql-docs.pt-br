---
title: Usando tipos definidos pelo usuário | Microsoft Docs
description: Usando tipos definidos pelo usuário com o Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 6dd1191c3bb987f99b854f2e736f86dafb9e5ed1
ms.sourcegitcommit: 354ed9c8fac7014adb0d752518a91d8c86cdce81
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/14/2018
ms.locfileid: "35612231"
---
# <a name="using-user-defined-types"></a>Usando tipos definidos pelo usuário
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] introduziu os UDTs (tipos definidos pelo usuário). Os UDTs estendem o sistema de tipos SQL, permitindo armazenar objetos e estruturas de dados personalizadas em um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] banco de dados. Os UDTs podem conter vários tipos de dados e ter comportamentos, o que os diferencia dos tipos de dados de alias tradicionais, que consistem em um único tipo de dado do sistema [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. UDTs são definidos usando quaisquer dos idiomas com suporte pelo .NET CRL (Common Language Runtime) que gera código verificável. Isso inclui o Microsoft Visual c#<sup>®</sup> e Visual Basic<sup>®</sup> .NET. Os dados são expostos como campos e propriedades de uma classe ou estrutura .NET e os comportamentos são definidos pelos métodos da classe ou estrutura.  
  
 Um UDT pode ser usado como a definição de coluna de uma tabela, como uma variável em uma [!INCLUDE[tsql](../../../includes/tsql-md.md)] em lotes, ou como um argumento de uma [!INCLUDE[tsql](../../../includes/tsql-md.md)] função ou procedimento armazenado.  
  
## <a name="ole-db-driver-for-sql-server"></a>Driver do OLE DB para SQL Server  
 O Driver OLE DB para SQL Server dá suporte a UDTs como tipos binários com informações de metadados, que permite gerenciar UDTs como objetos. Colunas UDT são expostas como DBTYPE_UDT e seus metadados são expostos por meio da interface de OLE DB core **IColumnRowset**e o novo [ISSCommandWithParameters](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md) interface.  
  
> [!NOTE]  
>  O **irowsetfind:: Findnextrow** método não funciona com o tipo de dados UDT. DB_E_BADCOMPAREOP será retornado se o UDT for usado como um tipo de coluna de pesquisa.  
  
### <a name="data-bindings-and-coercions"></a>Coerções e associações de dados  
 A tabela a seguir descreve a associação e a coerção que ocorrem ao usar os tipos de dados listados com o UDT [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Colunas UDT são expostas por meio do Driver OLE DB para SQL Server como DBTYPE_UDT. Você pode obter metadados por meio dos conjuntos de linhas de esquema apropriados de forma que possa gerenciar seus próprios tipos definidos como objetos.  
  
|Tipo de dados|Para servidor<br /><br /> **UDT**|Para servidor<br /><br /> **non-UDT**|Do servidor<br /><br /> **UDT**|Do servidor<br /><br /> **non-UDT**|  
|---------------|---------------------------|--------------------------------|-----------------------------|----------------------------------|  
|DBTYPE_UDT|Suporte para<sup>6</sup>|Erro<sup>1</sup>|Suporte para<sup>6</sup>|Erro<sup>5</sup>|  
|DBTYPE_BYTES|Suporte para<sup>6</sup>|N/D<sup>2</sup>|Suporte para<sup>6</sup>|N/D<sup>2</sup>|  
|DBTYPE_WSTR|Suporte para<sup>3,6</sup>|N/D<sup>2</sup>|Suporte para<sup>4,6</sup>|N/D<sup>2</sup>|  
|DBTYPE_BSTR|Suporte para<sup>3,6</sup>|N/D<sup>2</sup>|Suporte para<sup>4</sup>|N/D<sup>2</sup>|  
|DBTYPE_STR|Suporte para<sup>3,6</sup>|N/D<sup>2</sup>|Suporte para<sup>4,6</sup>|N/D<sup>2</sup>|  
|DBTYPE_IUNKNOWN|Sem suporte|N/D<sup>2</sup>|Sem suporte|N/D<sup>2</sup>|  
|DBTYPE_VARIANT (VT_UI1 &AMP;#124; VT_ARRAY)|Suporte para<sup>6</sup>|N/D<sup>2</sup>|Suporte para<sup>4</sup>|N/D<sup>2</sup>|  
|DBTYPE_VARIANT (VT_BSTR)|Suporte para<sup>3,6</sup>|N/D<sup>2</sup>|N/A|N/D<sup>2</sup>|  
  
 <sup>1</sup>se o tipo de um servidor diferente de DBTYPE_UDT for especificado com **ICommandWithParameters:: SetParameterInfo** e o tipo de acessador for DBTYPE_UDT, ocorrerá um erro quando a instrução é executada (DB_E_ERRORSOCCURRED; o status do parâmetro é DBSTATUS_E_BADACCESSOR). Caso contrário, os dados serão enviados para o servidor, mas ele retornará um erro indicando que não há conversão implícita do UDT para o tipo de dados do parâmetro.  
  
 <sup>2</sup>além do escopo deste artigo.  
  
 <sup>3</sup> ocorre conversão de dados de cadeia de caracteres hexadecimal para dados binários.  
  
 <sup>4</sup> ocorre conversão de dados de dados binários a cadeia de caracteres hexadecimal.  
  
 <sup>5</sup>pode ocorrer validação no momento de acessador de criação ou no momento da busca, o erro é DB_E_ERRORSOCCURRED, associando o status definido como DBBINDSTATUS_UNSUPPORTEDCONVERSION.  
  
 <sup>6</sup>BY_REF pode ser usado.  
  
 DBTYPE_NULL e DBTYPE_EMPTY podem ser associados a parâmetros de entrada, mas não a parâmetros ou resultados de saída. Quando eles são associados a parâmetros de entrada, o status precisa ser definido como DBSTATUS_S_ISNULL ou DBSTATUS_S_DEFAULT.  
  
 DBTYPE_UDT pode ser convertido em DBTYPE_EMPTY e DBTYPE_NULL, porém DBTYPE_NULL e DBTYPE_EMPTY não podem ser convertidos em DBTYPE_UDT. Isso é consistente com DBTYPE_BYTES.  
  
> [!NOTE]  
>  Uma nova interface é usada para lidar com UDTs como parâmetros, **ISSCommandWithParameters**, que herda de **ICommandWithParameters**. Os aplicativos devem usar esta interface para definir pelo menos o SSPROP_PARAM_UDT_NAME da propriedade DBPROPSET_SQLSERVERPARAMETER definida para os parâmetros de UDT. Se isso não for feito, **ICommand:: execute** retornará DB_E_ERRORSOCCURRED. Esta interface e conjunto de propriedades é descrito posteriormente neste artigo.  
  
 Se um tipo definido pelo usuário é inserido em uma coluna que não é grande o suficiente para conter todos os seus dados, **ICommand:: execute** retornará S_OK com um status de DB_E_ERRORSOCCURRED.  
  
 Conversões de dados fornecidas por serviços principais do OLE DB (**IDataConvert**) não são aplicáveis a DBTYPE_UDT. As demais associações não têm suporte.  
  
### <a name="ole-db-rowset-additions-and-changes"></a>Adições e alterações do conjunto de linhas do OLE DB  
 OLE DB Driver para SQL Server adiciona novos valores ou alterações a muitos dos principais conjuntos de linhas de esquema OLE DB.  
  
#### <a name="the-procedureparameters-schema-rowset"></a>O conjunto de linhas do esquema PROCEDURE_PARAMETERS  
 As adições a seguir foram feitas ao conjunto de linhas de esquema de PROCEDURE_PARAMETERS.  
  
|Nome da coluna|Tipo|Description|  
|-----------------|----------|-----------------|  
|SS_UDT_CATALOGNAME|DBTYPE_WSTR|O identificador de nome de três partes.|  
|SS_UDT_SCHEMANAME|DBTYPE_WSTR|O identificador de nome de três partes.|  
|SS_UDT_NAME|DBTYPE_WSTR|O identificador de nome de três partes.|  
|SS_UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|O Nome Qualificado do Assembly, que inclui o nome de tipo e toda a identificação de assembly necessários para referência pelo CLR.|  
  
#### <a name="the-sqlassemblies-schema-rowset"></a>O conjunto de linhas do esquema SQL_ASSEMBLIES  
 O Driver OLE DB para SQL Server apresenta um novo conjunto de linhas específicas do provedor de esquema que descreve os UDTs registrados. O servidor de ASSEMBLY pode ser especificado como um DBTYPE_WSTR, mas não está presente no conjunto de linhas. Se não estiver especificado, o conjunto de linhas seguirá o padrão do servidor atual. O conjunto de linhas do esquema SQL_ASSEMBLIES é definido na tabela a seguir:  
  
|Nome da coluna|Tipo|Description|  
|-----------------|----------|-----------------|  
|ASSEMBLY_CATALOG|DBTYPE_WSTR|O nome de catálogo do assembly que contém o tipo.|  
|ASSEMBLY_SCHEMA|DBTYPE_WSTR|O nome do esquema ou nome do proprietário do assembly que contém o tipo. Embora os assemblies tenham escopo por banco de dados e não por esquema, eles ainda têm um proprietário que é refletido aqui.|  
|ASSEMBLY_NAME|DBTYPE_WSTR|O nome do assembly que contém o tipo.|  
|ASSEMBLY_ID|DBTYPE_UI4|A ID de objeto do assembly que contém o tipo.|  
|PERMISSION_SET|DBTYPE_WSTR|Um valor que indica o escopo de acesso para o assembly. Valores incluem "SAFE", "EXTERNAL_ACCESS" e "UNSAFE".|  
|ASSEMBLY_BINARY|DBTYPE_BYTES|A representação binária do assembly.|  
  
#### <a name="the-sqlassemblies-dependencies-schema-rowset"></a>O conjunto de linhas do esquema SQL_ASSEMBLIES_ DEPENDENCIES  
 OLE DB Driver para SQL Server apresenta um novo conjunto de linhas específicas do provedor de esquema que descreve as dependências de assembly para um servidor especificado. O ASSEMBLY_SERVER pode ser especificado pelo chamador como um DBTYPE_WSTR, mas não está presente no conjunto de linhas. Se não estiver especificado, o conjunto de linhas seguirá o padrão do servidor atual. O conjunto de linhas do esquema SQL_ASSEMBLY_DEPENDENCIES é definido na tabela a seguir:  
  
|Nome da coluna|Tipo|Description|  
|-----------------|----------|-----------------|  
|ASSEMBLY_CATALOG|DBTYPE_WSTR|O nome de catálogo do assembly que contém o tipo.|  
|ASSEMBLY_SCHEMA|DBTYPE_WSTR|O nome do esquema ou nome do proprietário do assembly que contém o tipo. Embora os assemblies tenham escopo por banco de dados e não por esquema, eles ainda têm um proprietário, que é refletido aqui.|  
|ASSEMBLY_ID|DBTYPE_UI4|A ID de objeto do assembly.|  
|REFERENCED_ASSEMBLY_ID|DBTYPE_UI4|A ID de objeto do assembly referenciado.|  
  
#### <a name="the-sqlusertypes-schema-rowset"></a>O conjunto de linhas do esquema SQL_USER_TYPES  
 OLE DB Driver para SQL Server apresenta novas linhas de esquema, o SQL_USER_TYPES, que descreve quando os UDTs registrados para um servidor especificado são adicionados. O UDT_SERVER deve ser especificado pelo chamador como um DBTYPE_WSTR, mas não está presente no conjunto de linhas. O conjunto de linhas de esquema de SQL_USER_TYPES é definido na tabela a seguir.  
  
|Nome da coluna|Tipo|Description|  
|-----------------|----------|-----------------|  
|UDT_CATALOGNAME|DBTYPE_WSTR|Para colunas de UDT, essa propriedade é uma cadeia de caracteres especificando o nome do catálogo, onde o UDT é definido.|  
|UDT_SCHEMANAME|DBTYPE_WSTR|Para colunas de UDT, essa propriedade é uma cadeia de caracteres especificando o nome do esquema onde o UDT é definido.|  
|UDT_NAME|DBTYPE_WSTR|O nome do assembly que contém a classe do UDT.|  
|UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|O AQN (nome de tipo completo) inclui o nome do tipo prefixado pelo namespace, se aplicável.|  
  
#### <a name="the-columns-schema-rowset"></a>O conjunto de linhas do esquema COLUMNS  
 Adições ao conjunto de linhas de esquema COLUMNS incluem as seguintes colunas:  
  
|Nome da coluna|Tipo|Description|  
|-----------------|----------|-----------------|  
|SS_UDT_CATALOGNAME|DBTYPE_WSTR|Para colunas de UDT, essa propriedade é uma cadeia de caracteres especificando o nome do catálogo, onde o UDT é definido.|  
|SS_UDT_SCHEMANAME|DBTYPE_WSTR|Para colunas de UDT, essa propriedade é uma cadeia de caracteres especificando o nome do esquema onde o UDT é definido.|  
|SS_UDT_NAME|DBTYPE_WSTR|O nome do UDT|  
|SS_UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|O AQN (nome de tipo completo) inclui o nome do tipo prefixado pelo namespace, se aplicável.|  
  
### <a name="ole-db-property-set-additions-and-changes"></a>Adições e alterações do conjunto de propriedades do OLE DB  
 OLE DB Driver para SQL Server adiciona novos valores ou alterações a muitos dos principais propriedade OLE DB conjuntos.  
  
#### <a name="the-dbpropsetsqlserverparameter-property-set"></a>O conjunto de propriedades de DBPROPSET_SQLSERVERPARAMETER  
 Para dar suporte a UDTs através do OLE DB, OLE DB Driver para SQL Server implementa o novo conjunto de propriedades DBPROPSET_SQLSERVERPARAMETER, que contém os seguintes valores:  
  
|Nome|Tipo|Description|  
|----------|----------|-----------------|  
|SSPROP_PARAM_UDT_CATALOGNAME|DBTYPE_WSTR|O identificador de nome de três partes.<br /><br /> Para parâmetros de UDT, essa propriedade é uma cadeia de caracteres que especifica o nome do catálogo onde o tipo definido pelo usuário é definido.|  
|SSPROP_PARAM_UDT_SCHEMANAME|DBTYPE_WSTR|O identificador de nome de três partes.<br /><br /> Para parâmetros de UDT, essa propriedade é uma cadeia de caracteres que especifica o nome do esquema onde o tipo definido pelo usuário é definido.|  
|SSPROP_PARAM_UDT_NAME|DBTYPE_WSTR|O identificador de nome de três partes.<br /><br /> Para colunas de UDT, essa propriedade é uma cadeia de caracteres que especifica o nome de apenas uma parte do tipo definido pelo usuário.|  
  
 SSPROP_PARAM_UDT_NAME é obrigatório. SSPROP_PARAM_UDT_CATALOGNAME e SSPROP_PARAM_UDT_SCHEMANAME são opcionais. Se qualquer uma das propriedades for especificada incorretamente, o DB_E_ERRORSINCOMMAND será retornado. Se SSPROP_PARAM_UDT_CATALOGNAME e SSPROP_PARAM_UDT_SCHEMANAME não forem especificados, então o UDT deverá ser definido no mesmo banco de dados e esquema que a tabela. Se a definição de UDT não estiver no mesmo esquema que a tabela (mas estiver no mesmo banco de dados), então SSPROP_PARAM_UDT_SCHEMANAME deverá ser especificado. Se a definição de UDT estiver em um banco de dados diferente, SSPROP_PARAM_UDT_CATALOGNAME e SSPROP_PARAM_UDT_SCHEMANAME devem ser especificado.  
  
#### <a name="the-dbpropsetsqlservercolumn-property-set"></a>O conjunto de propriedades de DBPROPSET_SQLSERVERCOLUMN  
 Para dar suporte a criação de tabelas de **ITableDefinition** interface Driver OLE DB para SQL Server adiciona três novas colunas a seguir ao conjunto de propriedades DBPROPSET_SQLSERVERCOLUMN.  
  
|Nome|Description|Tipo|Description|  
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
 OLE DB Driver para SQL Server adiciona novos valores ou alterações a muitas das principais que interfaces OLE DB.  
  
#### <a name="the-isscommandwithparameters-interface"></a>A interface ISSCommandWithParameters  
 Para dar suporte a UDTs através do OLE DB, OLE DB Driver para SQL Server implementa um número de alterações, inclusive a adição do **ISSCommandWithParameters** interface. Essa nova interface herda da interface OLE DB **ICommandWithParameters**. Além dos três métodos herdados de **ICommandWithParameters**; **GetParameterInfo**, **MapParameterNames**, e **SetParameterInfo**; **ISSCommandWithParameters** fornece o **GetParameterProperties** e **SetParameterProperties** métodos que são usados para o identificador de servidor específico tipos de dados.  
  
> [!NOTE]  
>  O **ISSCommandWithParameters** interface também utiliza o SSPARAMPROPS nova estrutura.  
  
#### <a name="the-icolumnsrowset-interface"></a>A interface IColumnsRowset  
 Além de **ISSCommandWithParameters** interface Driver OLE DB para SQL Server também adiciona novos valores no conjunto de linhas retornado ao chamar o **IColumnsRowset:: Getcolumnrowset** método incluindo o seguinte.  
  
|Nome da coluna|Tipo|Description|  
|-----------------|----------|-----------------|  
|DBCOLUMN_SS_UDT_CATALOGNAME|DBTYPE_WSTR|Um identificador do nome de catálogo do UDT.|  
|DBCOLUMN_SS_UDT_SCHEMANAME|DBTYPE_WSTR|Um identificador do nome do esquema do UDT.|  
|DBCOLUMN_SS_UDT_NAME|DBTYPE_WSTR|Um identificador de nome do UDT.|  
|DBCOLUMN_SS_ASSEMBLY_TYPENAME|DBTYPE_WSTR|O nome qualificado do assembly, que inclui o nome de tipo e toda a identificação de assembly necessários para referência pelo CLR.|  
  
 Você pode diferenciar uma coluna UDT de servidor de outros tipos binários quando DBCOLUMN_TYPE for definido como DBTYPE_UDT observando os metadados UDT adicionados especificados na tabela anterior. Se esses dados estiverem parcialmente completos, o tipo de servidor será um UDT. Para tipos de servidores não UDT, essas colunas são sempre retornadas como NULL.  
 
  
## <a name="see-also"></a>Consulte também  
 [Driver do OLE DB para recursos do SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)    
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
