---
title: SQLPutData | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLPutData function
ms.assetid: d39aaa5b-7fbc-4315-a7f2-5a7787e04f25
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7e15353cd9f4c4a837fe5978d00259ad5460d50d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63046621"
---
# <a name="sqlputdata"></a>SQLPutData
  As restrições a seguir se aplicam ao usar o SQLPutData para enviar mais de 65.535 bytes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de dados (para a versão 4.21 a) ou 400 KB de dados (para SQL Server versão 6,0 e posterior`text`) para uma coluna`ntext`SQL_LONGVARCHAR (),`image`SQL_WLONGVARCHAR () ou SQL_LONGVARBINARY ():  
  
-   O parâmetro referenciado pode ser o *insert_value* em uma instrução INSERT.  
  
-   O parâmetro referenciado pode ser uma *expressão* na cláusula SET de uma instrução UPDATE.  
  
 Cancelar uma sequência de chamadas SQLPutData que fornecem dados em blocos para um servidor em execução [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] causa uma atualização parcial do valor da coluna ao usar a versão 6,5 ou anterior. A `text`coluna `ntext`,, `image` ou que foi referenciada quando SQLCancel foi chamado é definida como um valor de espaço reservado intermediário.  
  
> [!NOTE]  
>  O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client não dá suporte à conexão ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versão 6.5 e anteriores.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Há um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQLSTATE específico de cliente nativo para SQLPutData:  
  
|SQLSTATE|Erro|DESCRIÇÃO|  
|--------------|-----------|-----------------|  
|22026|Incompatibilidade de comprimento de dados String|Se o comprimento dos dados em bytes a ser enviado tiver sido especificado por um aplicativo, por exemplo, com SQL_LEN_DATA_AT_EXEC (*n*) em que *n* é maior que 0, o número total de bytes fornecidos pelo aplicativo via SQLPutData deve corresponder ao comprimento especificado.|  
  
## <a name="sqlputdata-and-table-valued-parameters"></a>SQLPutData e parâmetros com valor de tabela  
 SQLPutData é usado por um aplicativo ao usar a associação de linha variável com parâmetros com valor de tabela. O parâmetro *StrLen_or_Ind* indica que ele está pronto para o driver coletar dados para a próxima linha ou linhas de dados de parâmetro com valor de tabela, ou que não há mais linhas disponíveis:  
  
-   Um valor maior que 0 indica que o próximo conjunto de valores de linha está disponível.  
  
-   Um valor igual a 0 indica que não há mais linhas a serem enviadas.  
  
-   Qualquer valor menor que 0 indica um erro e resulta na geração de um registro de diagnóstico com SQLState igual a HY090 e na mensagem "Comprimento de buffer ou de cadeia de caracteres inválido".  
  
 O parâmetro *DataPtr* é ignorado, mas deve ser definido como um valor não nulo. Para obter mais informações, consulte a seção sobre associação de linha TVP variável em [associação e transferência de dados de parâmetros com valor de tabela e valores de coluna](../native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md).  
  
 Se *StrLen_or_Ind* tiver qualquer valor diferente de SQL_DEFAULT_PARAM ou um número entre 0 e o SQL_PARAMSET_SIZE (ou seja, o parâmetro *ColumnSize* de SQLBindParameter), será um erro. Esse erro faz SQLPutData retornar SQL_ERROR: SQLSTATE=HY090, "Comprimento de buffer ou de cadeia de caracteres inválido".  
  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros com valor de tabela &#40;&#41;ODBC ](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlputdata-support-for-enhanced-date-and-time-features"></a>Suporte de SQLPutData a recursos aprimorados de data e hora  
 Os valores de parâmetro dos tipos de data/hora são convertidos conforme descrito em [conversões de C para SQL](../native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md).  
  
 Para obter mais informações, consulte [melhorias de data e hora &#40;&#41;ODBC ](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlputdata-support-for-large-clr-udts"></a>Suporte de SQLPutData a UDTs grandes do CLR  
 
  `SQLPutData` dá suporte a UDTs grandes do CLR. Para obter mais informações, consulte [tipos CLR grandes definidos pelo usuário &#40;&#41;ODBC ](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLPutData](https://go.microsoft.com/fwlink/?LinkId=59365)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
