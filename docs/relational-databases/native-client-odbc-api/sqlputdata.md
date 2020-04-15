---
title: SQLPutData | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLPutData function
ms.assetid: d39aaa5b-7fbc-4315-a7f2-5a7787e04f25
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e063d1053d8a6e5e10a1234d33893adf27fbc3ad
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302337"
---
# <a name="sqlputdata"></a>SQLPutData
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  As seguintes restrições se aplicam ao usar o SQLPutData para enviar mais [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de 65.535 bytes de dados (para a versão 4.21a) ou 400 KB de dados (para a versão 6.0 do SQL Server e posterior) para uma coluna SQL_LONGVARCHAR **(texto),** SQL_WLONGVARCHAR **(ntext)** ou SQL_LONGVARBINARY **(imagem):**  
  
-   O parâmetro referenciado pode ser o *insert_value* em uma instrução INSERT.  
  
-   O parâmetro referenciado pode ser uma *expressão* na cláusula SET de uma declaração UPDATE.  
  
 O cancelamento de uma seqüência de chamadas SQLPutData que fornecem dados em blocos para um servidor em execução [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] causa uma atualização parcial do valor da coluna ao usar a versão 6.5 ou anterior. O **texto**, **ntext**ou coluna **de imagem** que foi referenciado quando o SQLCancel foi chamado é definido como um valor intermediário de espaço reservado.  
  
> [!NOTE]  
>  O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client não dá suporte à conexão ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versão 6.5 e anteriores.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Existe um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQLSTATE específico do Cliente Nativo para SQLPutData:  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|22026|Incompatibilidade de comprimento de dados String|Se o comprimento dos dados em bytes a serem enviados tiver sido especificado por um aplicativo, por exemplo, com*SQL_LEN_DATA_AT_EXEC(n)* onde *n* é maior que 0, o número total de bytes fornecidos pelo aplicativo via SQLPutData deve corresponder ao comprimento especificado.|  
  
## <a name="sqlputdata-and-table-valued-parameters"></a>SQLPutData e parâmetros com valor de tabela  
 SQLPutData é usado por um aplicativo ao usar a vinculação de linha variável com parâmetros de valor de tabela. O parâmetro *StrLen_Or_Ind* indica que está pronto para o motorista coletar dados para a próxima linha ou linhas de dados de parâmetros avaliados em tabela, ou que não há mais linhas disponíveis:  
  
-   Um valor maior que 0 indica que o próximo conjunto de valores de linha está disponível.  
  
-   Um valor igual a 0 indica que não há mais linhas a serem enviadas.  
  
-   Qualquer valor menor que 0 indica um erro e resulta na geração de um registro de diagnóstico com SQLState igual a HY090 e na mensagem "Comprimento de buffer ou de cadeia de caracteres inválido".  
  
 O *parâmetro DataPtr* é ignorado, mas deve ser definido como um valor não NULA. Para obter mais informações, consulte a seção na vinculação da linha TVP variável em [Vinculação e Transferência de Dados de Parâmetros e Valores de Coluna valorizados pela tabela](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md).  
  
 Se *StrLen_Or_Ind* tiver algum valor que não seja SQL_DEFAULT_PARAM ou um número entre 0 e o SQL_PARAMSET_SIZE (ou seja, o parâmetro *ColumnSize* do SQLBindParameter), é um erro. Esse erro faz SQLPutData retornar SQL_ERROR: SQLSTATE=HY090, "Comprimento de buffer ou de cadeia de caracteres inválido".  
  
 Para obter mais informações sobre parâmetros avaliados em tabela, consulte [Parâmetros valorizados em tabela &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlputdata-support-for-enhanced-date-and-time-features"></a>Suporte de SQLPutData a recursos aprimorados de data e hora  
 Os valores dos parâmetros dos tipos de data/hora são convertidos conforme descrito em [Conversões de C para SQL](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md).  
  
 Para obter mais informações, consulte [melhorias de data e hora &#40;&#41;da ODBC ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlputdata-support-for-large-clr-udts"></a>Suporte de SQLPutData a UDTs grandes do CLR  
 **O SQLPutData** suporta grandes tipos definidos pelo usuário CLR (UDTs). Para obter mais informações, consulte [Grandes tipos definidos pelo usuário da CLR &#40;&#41;ODBC ](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLPutData](https://go.microsoft.com/fwlink/?LinkId=59365)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
