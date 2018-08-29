---
title: SQLColAttribute | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLColAttribute function
ms.assetid: a5387d9e-a243-4cfe-b786-7fad5842b1d6
caps.latest.revision: 52
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6f4e3ed31e590e8b3bd0ac7dc8910f38982c09ee
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43088320"
---
# <a name="sqlcolattribute"></a>SQLColAttribute
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Você pode usar **SQLColAttribute** para recuperar um atributo de uma coluna de conjunto de resultados para instruções ODBC preparadas ou executadas. Chamando **SQLColAttribute** em instruções preparadas causa uma ida e volta ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client recebe os dados de coluna do conjunto de resultados como parte da execução da instrução, por isso a chamada **SQLColAttribute** após a conclusão da **SQLExecute** ou  **SQLExecDirect** não envolve uma ida e volta do servidor.  
  
> [!NOTE]  
>  Os atributos do identificador de coluna ODBC não estão disponíveis em todos os conjuntos de resultados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Identificador de campo|Description|  
|----------------------|-----------------|  
|SQL_COLUMN_TABLE_NAME|Disponível em conjuntos de resultados recuperados de instruções que geram cursores de servidor ou em instruções SELECT executadas que contêm uma cláusula FOR BROWSE.|  
|SQL_DESC_BASE_COLUMN_NAME|Disponível em conjuntos de resultados recuperados de instruções que geram cursores de servidor ou em instruções SELECT executadas que contêm uma cláusula FOR BROWSE.|  
|SQL_DESC_BASE_TABLE_NAME|Disponível em conjuntos de resultados recuperados de instruções que geram cursores de servidor ou em instruções SELECT executadas que contêm uma cláusula FOR BROWSE.|  
|SQL_DESC_CATALOG_NAME|Nome do banco de dados. Disponível em conjuntos de resultados recuperados de instruções que geram cursores de servidor ou em instruções SELECT executadas que contêm uma cláusula FOR BROWSE.|  
|SQL_DESC_LABEL|Disponível em todos os conjuntos de resultados. O valor é idêntico ao valor do campo SQL_DESC_NAME.<br /><br /> O campo só terá comprimento zero se uma coluna for o resultado de uma expressão e a expressão não contiver uma atribuição de rótulo.|  
|SQL_DESC_NAME|Disponível em todos os conjuntos de resultados. O valor é idêntico ao valor do campo SQL_DESC_LABEL.<br /><br /> O campo só terá comprimento zero se uma coluna for o resultado de uma expressão e a expressão não contiver uma atribuição de rótulo.|  
|SQL_DESC_SCHEMA_NAME|Nome do proprietário. Disponível em conjuntos de resultados recuperados de instruções que geram cursores de servidor ou em instruções SELECT executadas que contêm uma cláusula FOR BROWSE.<br /><br /> Disponível somente se o nome do proprietário for especificado para a coluna na instrução SELECT.|  
|SQL_DESC_TABLE_NAME|Disponível em conjuntos de resultados recuperados de instruções que geram cursores de servidor ou em instruções SELECT executadas que contêm uma cláusula FOR BROWSE.|  
|SQL_DESC_UNNAMED|SQL_NAMED para todas as colunas de um conjunto de resultados, a menos que uma coluna seja o resultado de uma expressão que não contém uma atribuição de rótulo como parte da expressão. Quando SQL_DESC_UNNAMED retorna SQL_UNNAMED, todos os atributos de identificador de coluna ODBC contêm cadeias de caracteres de comprimento zero para a coluna.|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client usa a instrução SET FMTONLY para reduzir a sobrecarga de servidor quando **SQLColAttribute** é chamado para instruções preparadas mas não executadas.  
  
 Para tipos de valores grandes, **SQLColAttribute** retornará os valores a seguir:  
  
|Identificador de campo|Descrição de alteração|  
|----------------------|---------------------------|  
|SQL_DESC_DISPLAY_SIZE|Esse é o número máximo de caracteres necessários para exibir dados da coluna. Para colunas de tipos de valores grandes, o valor retornado é SQL_SS_LENGTH_UNLIMITED.|  
|SQL_DESC_LENGTH|Retorna o comprimento real da coluna no conjunto de resultados. Para colunas de tipos de valores grandes, o valor retornado é SQL_SS_LENGTH_UNLIMITED.|  
|SQL_DESC_OCTET_LENGTH|Retorna o comprimento de máximo de uma coluna de tipo de valor grande. SQL_SS_LENGTH_UNLIMITED é usado para indicar tamanho ilimitado.|  
|SQL_DESC_PRECISION|Retorna o valor SQL_SS_LENGTH_UNLIMITED para colunas de tipo de valor grande.|  
|SQL_DESC_TYPE|Retorna SQL_VARCHAR, SQL_WVARCHAR e SQL_VARBINARY para tipos de valor grande.|  
|SQL_DESC_TYPE_NAME|Retorna "varchar", "varbinary", "nvarchar" para os tipos de valor grande.|  
  
 Para todas as versões, os atributos de coluna são informados somente para o primeiro conjunto de resultados quando vários conjuntos são gerados por um lote preparado de instruções SQL.  
  
 Os seguintes atributos de coluna são extensões expostas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client retorna todos os valores de *NumericAttrPtr* parâmetro. Os valores são retornados como SDWORD (signed long) com exceção de SQL_CA_SS_COMPUTE_BYLIST, que é um ponteiro para uma matriz de WORD.  
  
|Identificador de campo|Valor retornado|  
|----------------------|--------------------|  
|SQL_CA_SS_COLUMN_HIDDEN*|TRUE se a coluna referenciada fizer parte de uma chave primária oculta criada para suportar uma instrução SELECT Transact-SQL que contém FOR BROWSE.|  
|SQL_CA_SS_COLUMN_ID|Posição ordinal de uma coluna de resultados de cláusula COMPUTE na instrução SELECT Transact-SQL atual.|  
|SQL_CA_SS_COLUMN_KEY *|TRUE se a coluna referenciada fizer parte de uma chave primária para a linha e a instrução SELECT Transact-SQL contiver FOR BROWSE.|  
|SQL_CA_SS_COLUMN_OP|Inteiro que especifica o operador de agregação responsável pelo valor em uma coluna de cláusula COMPUTE. As definições dos valores inteiros estão em sqlncli.h.|  
|SQL_CA_SS_COLUMN_ORDER|Posição ordinal da coluna em uma cláusula ORDER BY da instrução SELECT Transact-SQL ou ODBC.|  
|SQL_CA_SS_COLUMN_SIZE|Comprimento máximo, em bytes, necessário para associar um valor de dados recuperado da coluna a uma variável SQL_C_BINARY.|  
|SQL_CA_SS_COLUMN_SSTYPE|Tipo de dados nativo de dados armazenados na coluna do SQL Server. As definições dos valores de tipo estão em sqlncli.h.|  
|SQL_CA_SS_COLUMN_UTYPE|Tipo de dados básico do tipo de dados definido pelo usuário da coluna do SQL Server. As definições dos valores de tipo estão em sqlncli.h.|  
|SQL_CA_SS_COLUMN_VARYLEN|TRUE se os dados da coluna puderem variar em comprimento; ou FALSE em caso contrário.|  
|SQL_CA_SS_COMPUTE_BYLIST|Ponteiro para uma matriz de WORD (unsigned short) que especifica as colunas usadas na frase BY de uma cláusula COMPUTE. Se a cláusula COMPUTE não especificar uma frase BY, um ponteiro NULL será retornado.<br /><br /> O primeiro elemento da matriz contém a contagem de colunas de lista BY. Os elementos adicionais são os ordinais da coluna.|  
|SQL_CA_SS_COMPUTE_ID|*computeid* de uma linha que é o resultado de uma cláusula COMPUTE na instrução SELECT Transact-SQL atual.|  
|SQL_CA_SS_NUM_COMPUTES|Número de cláusulas COMPUTE especificado na instrução SELECT Transact-SQL atual.|  
|SQL_CA_SS_NUM_ORDERS|Número de colunas especificado em uma cláusula ORDER BY da instrução SELECT Transact-SQL ou ODBC.|  
  
 \*   Disponível se o atributo de instrução SQL_SOPT_SS_HIDDEN_COLUMNS for definido como SQL_HC_ON.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] introduziu campos de descritor específicos de driver para fornecer informações adicionais para denotar o nome de coleção de esquemas XML, o nome do esquema e o nome do catálogo, respectivamente. Essas propriedades não exigem aspas ou um caractere de escape se eles contiverem caracteres não alfanuméricos. A tabela a seguir lista esses novos campos de descritor:  
  
|Nome da coluna|Tipo|Description|  
|-----------------|----------|-----------------|  
|SQL_CA_SS_XML_SCHEMACOLLECTION_CATALOG_NAME|CharacterAttributePtr|O nome do catálogo em que é definido um nome da coleção de esquemas XML. Se não for possível localizar o nome do catálogo, essa variável conterá uma cadeia de caracteres vazia.<br /><br /> Essas informações são retornadas do campo de registro SQL_DESC_SS_XML_SCHEMACOLLECTION_CATALOG_NAME do IRD, que é um campo de leitura-gravação.|  
|SQL_CA_SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|CharacterAttributePtr|O nome do esquema no qual é definido um nome da coleção de esquemas XML. Se não for possível localizar o nome do esquema, essa variável conterá uma cadeia de caracteres vazia.<br /><br /> Essas informações são retornadas do campo de registro SQL_DESC_SS_XML_SCHEMACOLLECTION_SCHEMA_NAME do IRD, que é um campo de leitura-gravação.|  
|SQL_CA_SS_XML_SCHEMACOLLECTION_NAME|CharacterAttributePtr|O nome de uma coleção de esquemas XML. Se não for possível localizar o nome, essa variável conterá uma cadeia de caracteres vazia.<br /><br /> Essas informações são retornadas do campo de registro SQL_DESC_SS_XML_SCHEMACOLLECTION_NAME do IRD, que é um campo de leitura-gravação.|  
  
 Além disso, o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] introduziu campos de descritor específicos de driver para fornecer informações adicionais para uma coluna de UDT (tipo definido pelo usuário) de um conjunto de resultados ou um parâmetro de UDT de um procedimento armazenado ou consulta parametrizada. Essas propriedades não exigem aspas ou um caractere de escape se eles contiverem caracteres não alfanuméricos. A tabela a seguir lista esses novos campos de descritor:  
  
|Nome da coluna|Tipo|Description|  
|-----------------|----------|-----------------|  
|SQL_CA_SS_UDT_CATALOG_NAME|CharacterAttributePtr|O nome do catálogo que contém o UDT.|  
|SQL_CA_SS_UDT_SCHEMA_NAME|CharacterAttributePtr|O nome do esquema que contém o UDT.|  
|SQL_CA_SS_UDT_TYPE_NAME|CharacterAttributePtr|O nome do UDT.|  
|SQL_CA_SS_UDT_ASSEMBLY_TYPE_NAME|CharacterAttributePtr|O nome qualificado do assembly do UDT.|  
  
 O identificador do campo de descritor SQL_DESC_TYPE_NAME existente é usado para indicar o nome do UDT. O campo SQL_DESC_TYPE para uma coluna de tipo UDT é SQL_SS_UDT.  
  
## <a name="sqlcolattribute-support-for-enhanced-date-and-time-features"></a>Suporte do SQLColAttribute a recursos aprimorados de data e hora  
 Para obter os valores retornados para tipos de data/hora, consulte a seção "Informações retornadas em campos IRD" [Parameter and Result Metadata](../../relational-databases/native-client-odbc-date-time/metadata-parameter-and-result.md).  
  
 Para obter mais informações, consulte [aprimoramentos de data e hora &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlcolattribute-support-for-large-clr-udts"></a>Suporte do SQLColAttribute a UDTs CLR grandes  
 O**SQLColAttribute** suporta UDTs CLR grandes. Para obter mais informações, consulte [Large CLR User-Defined tipos &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="sqlcolattribute-support-for-sparse-columns"></a>Suporte do SQLColAttribute a colunas esparsas  
 SQLColAttribute consulta nova implementação IRD (descritor) campo de linha, SQL_CA_SS_IS_COLUMN_SET, para determinar se uma coluna é uma **column_set** coluna.  
  
 Para obter mais informações, consulte [Sparse Columns Support &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
 [Função SQLColAttribute](http://go.microsoft.com/fwlink/?LinkId=59334)   
 [Detalhes de implementação de API do ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)  
  
  
