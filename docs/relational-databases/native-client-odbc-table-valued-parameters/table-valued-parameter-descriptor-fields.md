---
title: Campos de descritor de parâmetro com valor de tabela | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), descriptor fields
ms.assetid: 4e009eff-c156-4d63-abcf-082ddd304de2
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f97d723d027cb756e7a74b5f2aa58c06d0d63acd
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85760649"
---
# <a name="table-valued-parameter-descriptor-fields"></a>Campos do descritor de parâmetro com valor de tabela
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  O suporte a parâmetros com valor de tabela inclui novos campos específicos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em APDs (descritores de parâmetro de aplicativo) e IPDs (descritores de parâmetro de implementação) ODBC.  
  
## <a name="remarks"></a>Comentários  
  
|Name|Local|Tipo|Description|  
|----------|--------------|----------|-----------------|  
|SQL_CA_SS_TYPE_NAME|IPD|SQLTCHAR*|O nome do tipo de servidor do parâmetro com valor de tabela.<br /><br /> Quando um nome de tipo de parâmetro com valor de tabela é especificado em uma chamada para SQLBindParameter, ele sempre deve ser especificado como um valor Unicode, mesmo em aplicativos criados como aplicativos ANSI. O valor usado para o parâmetro *StrLen_or_IndPtr* deve ser SQL_NTS ou o comprimento da cadeia de caracteres do nome multiplicado por sizeof (WCHAR).<br /><br /> Quando um nome de tipo de parâmetro com valor de tabela é especificado via SQLSetDescField, ele pode ser especificado usando um literal que está de acordo com a maneira como o aplicativo é compilado. O Gerenciador do Driver ODBC executará todas as conversões de Unicode necessárias.|  
|SQL_CA_SS_TYPE_CATALOG_NAME (somente leitura)|IPD|SQLTCHAR*|O catálogo onde o tipo é definido.|  
|SQL_CA_SS_TYPE_SCHEMA_NAME|IPD|SQLTCHAR*|O esquema onde o tipo é definido.|  
  
 Os aplicativos não devem ser definidos como SQL_CA_SS_TYPE_CATALOG_NAME para parâmetros com valor de tabela. Caso isso ocorra, será retornado um SQL_ERROR e será gerado um registro de diagnóstico com SQLSTATE = HY091 e a mensagem "Identificador de campo de descritor inválido".  
  
 Os seguintes atributos de instrução e campos de cabeçalho do descritor se aplicam a parâmetros com valor de tabela quando o foco do parâmetro está definido como um parâmetro com valor de tabela:  
  
|Name|Local|Tipo|Description|  
|----------|--------------|----------|-----------------|  
|SQL_ATTR_PARAMSET_SIZE<br /><br /> (É equivalente a SQL_DESC_ARRAY_SIZE no APD.)|APD|SQLUINTEGER|O tamanho das matrizes de buffers para um parâmetro com valor de tabela. Esse é o número máximo de linhas que os buffers irão conter ou o tamanho dos buffers em linhas; o próprio valor de parâmetro com valor de tabela pode ter mais ou menos linhas do que os buffers comportam. O padrão é UTF-1.<br /><br /> Observação: se SQL_SOPT_SS_PARAM_FOCUS for definido como seu valor padrão de 0, SQL_ATTR_PARAMSET_SIZE se referirá à instrução e especificará o número de conjuntos de parâmetros. Se SQL_SOPT_SS_PARAM_FOCUS for definido como o ordinal de um parâmetro com valor de tabela, ele fará referência ao parâmetro com valor de tabela e especificará o número de linhas por conjunto de parâmetros para o parâmetro com valor de tabela.|  
|SQL_ATTR_PARAM _BIND_TYPE|APD|SQLINTEGER|O padrão é SQL_PARAM_BIND_BY_COLUMN.<br /><br /> Para selecionar a associação de linha, este campo é definido como o comprimento da estrutura ou uma instância de um buffer que será associada a um conjunto de linhas de parâmetro com valor de tabela. Esse comprimento deve incluir espaço para todas as colunas associadas e qualquer preenchimento da estrutura ou do buffer. Isso garante que quando o endereço de uma coluna associada for incrementado com o comprimento especificado, o resultado apontará para o início da mesma coluna na linha seguinte. Ao usar o operador **sizeof** no ANSI C, esse comportamento é garantido.|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|APD|SQLINTEGER*|O padrão é um ponteiro nulo.<br /><br /> Se este campo for não nulo, o driver cancelará o ponteiro, adicionará o valor cancelado a cada um dos campos adiados no registro do descritor (SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, e SQL_DESC_OCTET_LENGTH_PTR) e usará os novos valores de ponteiro para acessar valores de dados.|  
  
 Esses campos só são válidos com parâmetros com valor de tabela e são ignorados para outros tipos de dados.  
  
 SQL_CA_SS_TYPE_NAME é opcional para chamadas de procedimento armazenado. Ele deve ser especificado para instruções SQL que não são chamadas de procedimento para permitir que o servidor determine o tipo do parâmetro com valor de tabela.  
  
 Se o nome do tipo for necessário e se o tipo de tabela do parâmetro com valor de tabela for definido em um esquema diferente do procedimento armazenado, SQL_CA_SS_TYPE_SCHEMA_NAME deverá ser especificado no IPD (descritor do parâmetro de implementação). Caso contrário, o servidor não poderá determinar o tipo do parâmetro com valor de tabela. Isso resultará em um erro quando você chamar SQLExecute ou SQLExecDirect. O erro terá SQLSTATE = 07006 e a mensagem "Violação do atributo de tipo de dados restrito".  
  
 As colunas de parâmetro com valor de tabela podem usar a associação de linha ou de coluna. O padrão é a associação de coluna. A associação de linha pode ser especificada definindo-se SQL_ATTR_PARAM_BIND_TYPE e SQL_ATTR_ PARAM_BIND_OFFSET_PTR. Esse procedimento é equivalente à associação de linha de colunas e parâmetros.  
  
 Também é possível usar SQL_CA_SS_TYPE_CATALOG_NAME e SQL_CA_SS_TYPE_SCHEMA_NAME para recuperar o catálogo e o esquema associados com parâmetros de tipo definido pelo usuário CLR. Essas são alternativas aos atributos existentes de esquema de catálogo específicos para esses tipos.  
  
## <a name="see-also"></a>Consulte Também  
 [Parâmetros com valor de tabela &#40;&#41;ODBC](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
