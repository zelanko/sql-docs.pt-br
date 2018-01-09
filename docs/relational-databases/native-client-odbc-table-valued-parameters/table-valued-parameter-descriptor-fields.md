---
title: "Campos de descritor de parâmetro com valor de tabela | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-table-valued-parameters
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: table-valued parameters (ODBC), descriptor fields
ms.assetid: 4e009eff-c156-4d63-abcf-082ddd304de2
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 60db5e1eed36ab731c982d7171ca186b3012aacc
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="table-valued-parameter-descriptor-fields"></a>Campos do descritor de parâmetro com valor de tabela
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O suporte a parâmetros com valor de tabela inclui novos campos específicos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em APDs (descritores de parâmetro de aplicativo) e IPDs (descritores de parâmetro de implementação) ODBC.  
  
## <a name="remarks"></a>Remarks  
  
|Nome|Local|Tipo|Description|  
|----------|--------------|----------|-----------------|  
|SQL_CA_SS_TYPE_NAME|IPD|SQLTCHAR*|O nome do tipo de servidor do parâmetro com valor de tabela.<br /><br /> Quando um nome de tipo de parâmetro com valor de tabela é especificado em uma chamada para SQLBindParameter, ele sempre deve ser especificado como um valor Unicode, mesmo em aplicativos que são criados como aplicativos ANSI. O valor usado para o parâmetro *StrLen_or_IndPtr* deve ser SQL_NTS ou o comprimento da cadeia de caracteres do nome multiplicado por sizeof (WCHAR).<br /><br /> Quando um nome de tipo de parâmetro com valor de tabela é especificado por meio de SQLSetDescField, ele pode ser especificado usando um literal que está de acordo com a maneira como o aplicativo é compilado. O Gerenciador do Driver ODBC executará todas as conversões de Unicode necessárias.|  
|SQL_CA_SS_TYPE_CATALOG_NAME (somente leitura)|IPD|SQLTCHAR*|O catálogo onde o tipo é definido.|  
|SQL_CA_SS_TYPE_SCHEMA_NAME|IPD|SQLTCHAR*|O esquema onde o tipo é definido.|  
  
 Os aplicativos não devem ser definidos como SQL_CA_SS_TYPE_CATALOG_NAME para parâmetros com valor de tabela. Caso isso ocorra, será retornado um SQL_ERROR e será gerado um registro de diagnóstico com SQLSTATE = HY091 e a mensagem "Identificador de campo de descritor inválido".  
  
 Os seguintes atributos de instrução e campos de cabeçalho do descritor se aplicam a parâmetros com valor de tabela quando o foco do parâmetro está definido como um parâmetro com valor de tabela:  
  
|Nome|Local|Tipo|Description|  
|----------|--------------|----------|-----------------|  
|SQL_ATTR_PARAMSET_SIZE<br /><br /> (É equivalente a SQL_DESC_ARRAY_SIZE no APD.)|APD|SQLUINTEGER|O tamanho das matrizes de buffers para um parâmetro com valor de tabela. Esse é o número máximo de linhas que os buffers irão conter ou o tamanho dos buffers em linhas; o próprio valor de parâmetro com valor de tabela pode ter mais ou menos linhas do que os buffers comportam. O padrão é 1.<br /><br /> Observação: Se SQL_SOPT_SS_PARAM_FOCUS for definido como seu valor padrão de 0, SQL_ATTR_PARAMSET_SIZE refere-se à instrução e especifica o número de conjuntos de parâmetros. Se SQL_SOPT_SS_PARAM_FOCUS for definido como o ordinal de um parâmetro com valor de tabela, ele fará referência ao parâmetro com valor de tabela e especificará o número de linhas por conjunto de parâmetros para o parâmetro com valor de tabela.|  
|SQL_ATTR_PARAM _BIND_TYPE|APD|SQLINTEGER|O padrão é SQL_PARAM_BIND_BY_COLUMN.<br /><br /> Para selecionar a associação de linha, este campo é definido como o comprimento da estrutura ou uma instância de um buffer que será associada a um conjunto de linhas de parâmetro com valor de tabela. Esse comprimento deve incluir espaço para todas as colunas associadas e qualquer preenchimento da estrutura ou do buffer. Isso garante que quando o endereço de uma coluna associada for incrementado com o comprimento especificado, o resultado apontará para o início da mesma coluna na linha seguinte. Ao usar o **sizeof** operador em ANSI C, esse comportamento é garantido.|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|APD|SQLINTEGER*|O padrão é um ponteiro nulo.<br /><br /> Se este campo for não nulo, o driver cancelará o ponteiro, adicionará o valor cancelado a cada um dos campos adiados no registro do descritor (SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, e SQL_DESC_OCTET_LENGTH_PTR) e usará os novos valores de ponteiro para acessar valores de dados.|  
  
 Esses campos só são válidos com parâmetros com valor de tabela e são ignorados para outros tipos de dados.  
  
 SQL_CA_SS_TYPE_NAME é opcional para chamadas de procedimento armazenado. Ele deve ser especificado para instruções SQL que não são chamadas de procedimento para permitir que o servidor determine o tipo do parâmetro com valor de tabela.  
  
 Se o nome do tipo for necessário e se o tipo de tabela do parâmetro com valor de tabela for definido em um esquema diferente do procedimento armazenado, SQL_CA_SS_TYPE_SCHEMA_NAME deverá ser especificado no IPD (descritor do parâmetro de implementação). Caso contrário, o servidor não poderá determinar o tipo do parâmetro com valor de tabela. Isso resultará em um erro ao chamar SQLExecute ou SQLExecDirect. O erro terá SQLSTATE = 07006 e a mensagem "Violação do atributo de tipo de dados restrito".  
  
 As colunas de parâmetro com valor de tabela podem usar a associação de linha ou de coluna. O padrão é a associação de coluna. A associação de linha pode ser especificada definindo-se SQL_ATTR_PARAM_BIND_TYPE e SQL_ATTR_ PARAM_BIND_OFFSET_PTR. Esse procedimento é equivalente à associação de linha de colunas e parâmetros.  
  
 Também é possível usar SQL_CA_SS_TYPE_CATALOG_NAME e SQL_CA_SS_TYPE_SCHEMA_NAME para recuperar o catálogo e o esquema associados com parâmetros de tipo definido pelo usuário CLR. Essas são alternativas aos atributos existentes de esquema de catálogo específicos para esses tipos.  
  
## <a name="see-also"></a>Consulte Também  
 [Com valor de tabela parâmetros &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
