---
title: "Parâmetros de associação | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-queries
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, parameters
- parameters [SQL Server Native Client], ODBC
- statements [ODBC], parameters
- binding parameters [SQL Server Native Client]
- parameter markers [ODBC]
- unbound parameter markers
- SQLBindParameter function
- ODBC applications, parameters
- bound parameter markers [SQL Server Native Client]
ms.assetid: d6c69739-8f89-475f-a60a-b2f6c06576e2
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eec7675fc0fa0261e877d45da86bbcd2280f0237
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="using-statement-parameters---binding-parameters"></a>Usando parâmetros de instrução - parâmetros de associação
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Para que a instrução possa ser executada, cada marcador de parâmetro em uma instrução SQL deve ser associado a uma variável no aplicativo. Isso é feito chamando a [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md) função. **SQLBindParameter** descreve a variável de programa (endereço, tipo de dados C e assim por diante) para o driver. Ela também identifica o marcador de parâmetro indicando seu valor ordinal e, em seguida, descreve as características do objeto SQL que representa (tipo de dados SQL, precisão e assim por diante).  
  
 Marcadores de parâmetro podem ser associados ou reassociados a qualquer momento, antes de uma instrução ser executada. Uma associação de parâmetro permanece em vigor até ocorrer um dos seguintes eventos:  
  
-   Uma chamada para [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) com o *opção* parâmetro definido como SQL_RESET_PARAMS libera todos os parâmetros associados ao identificador de instrução.  
  
-   Uma chamada para **SQLBindParameter** com *ParameterNumber* definido como o ordinal de um marcador de parâmetro associado automaticamente libera a associação anterior.  
  
 Um aplicativo também pode associar parâmetros a matrizes de variáveis de programa para processar uma instrução SQL em lotes. Há dois tipos de associação de matriz:  
  
-   A associação em colunas é feita quando cada um dos parâmetros é associado à sua própria matriz de variáveis.  
  
     A associação é especificada chamando [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) com *atributo* definido como SQL_ATTR_PARAM_BIND_TYPE e *ValuePtr* definido como SQL_PARAM_BIND_BY_COLUMN.  
  
-   A associação em linhas é feita quando todos os parâmetros na instrução SQL são associados como uma unidade a uma matriz de estruturas que contém cada uma das variáveis para os parâmetros.  
  
     A associação é especificada chamando **SQLSetStmtAttr** com *atributo* definido como SQL_ATTR_PARAM_BIND_TYPE e *ValuePtr* definido como o tamanho reter a estrutura de variáveis de programa.  
  
 Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client envia parâmetros de cadeia de caracteres binária ou de caractere para o servidor, ele preenche os valores para o comprimento especificado em **SQLBindParameter** *ColumnSize* parâmetro. Se um aplicativo do ODBC 2. x especificar 0 para *ColumnSize*, o driver acrescenta o valor do parâmetro para a precisão do tipo de dados. A precisão é 8000 quando houver conexão a servidores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 255 quando houver conexões a versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *ColumnSize* está em bytes para colunas variantes.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte à definição de nomes para parâmetros de procedimento armazenado. O ODBC 3.5 também introduziu o suporte a parâmetros nomeados usados ao chamar procedimentos armazenados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esse suporte pode ser usado para:  
  
-   Chamar um procedimento armazenado e fornecer valores para um subconjunto dos parâmetros definidos para o procedimento armazenado.  
  
-   Especificar os parâmetros no aplicativo em uma ordem diferente daquela especificada quando o procedimento armazenado foi criado.  
  
 Parâmetros nomeados só são suportados ao usar o [!INCLUDE[tsql](../../includes/tsql-md.md)] **EXECUTE** instrução ou a sequência de escape ODBC CALL para executar um procedimento armazenado.  
  
 Se **SQL_DESC_NAME** está definido para um parâmetro de procedimento armazenado, todos os parâmetros de procedimento armazenado na consulta também deverão definir **SQL_DESC_NAME**.  Se forem usados literais em chamadas de procedimento armazenado, onde parâmetros têm **SQL_DESC_NAME** definido, os literais deverão usar o formato *' nome*=*valor*', onde *nome* é o nome do parâmetro de procedimento armazenado (por exemplo, @p1). Para obter mais informações, consulte [associando parâmetros por nome (parâmetros nomeados)](http://go.microsoft.com/fwlink/?LinkId=167215).  
  
## <a name="see-also"></a>Consulte também  
 [Usando parâmetros de instrução](../../relational-databases/native-client-odbc-queries/using-statement-parameters.md)  
  
  
