---
title: SQLPutData | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLPutData function
ms.assetid: d39aaa5b-7fbc-4315-a7f2-5a7787e04f25
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bf27150c9e6c0da3f32cd3295c358c80da44b767
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2018
---
# <a name="sqlputdata"></a>SQLPutData
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  As seguintes restrições se aplicam ao usar SQLPutData para enviar mais de 65.535 bytes de dados (para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versão 4.21) ou 400 KB de dados (para SQL Server versão 6.0 e posterior) para um SQL_LONGVARCHAR (**texto**), SQL_WLONGVARCHAR (**ntext**) ou SQL_LONGVARBINARY (**imagem**) coluna:  
  
-   O parâmetro referenciado pode ser o *insert_value* em uma instrução INSERT.  
  
-   O parâmetro referenciado pode ser um *expressão* na cláusula SET de uma instrução UPDATE.  
  
 Cancelar uma sequência de chamadas SQLPutData que fornecem dados em blocos para um servidor executando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] faz com que uma atualização parcial de valor da coluna ao usar a versão 6.5 ou anterior. O **texto**, **ntext**, ou **imagem** coluna referenciada quando SQLCancel foi chamado é definida como um valor de espaço reservado intermediário.  
  
> [!NOTE]  
>  O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client não dá suporte à conexão ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versão 6.5 e anteriores.  
  
## <a name="diagnostics"></a>diagnóstico  
 Há um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQLSTATE específico do Native Client para SQLPutData:  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|22026|Incompatibilidade de comprimento de dados String|Se o comprimento dos dados em bytes a ser enviado tiver sido especificado por um aplicativo, por exemplo, com SQL_LEN_DATA_AT_EXEC (*n*) onde  *n*  é maior que 0, o número total de bytes fornecidas pelo aplicativo via SQLPutData devem corresponder ao comprimento especificado.|  
  
## <a name="sqlputdata-and-table-valued-parameters"></a>SQLPutData e parâmetros com valor de tabela  
 SQLPutData é usado por um aplicativo com associação de linha variável a parâmetros com valor de tabela. O *StrLen_Or_Ind* parâmetro indica que ele está pronto para o driver coletar dados para a próxima linha ou linhas de dados de parâmetro com valor de tabela, ou que não há mais linhas estão disponíveis:  
  
-   Um valor maior que 0 indica que o próximo conjunto de valores de linha está disponível.  
  
-   Um valor igual a 0 indica que não há mais linhas a serem enviadas.  
  
-   Qualquer valor menor que 0 indica um erro e resulta na geração de um registro de diagnóstico com SQLState igual a HY090 e na mensagem "Comprimento de buffer ou de cadeia de caracteres inválido".  
  
 O *DataPtr* parâmetro é ignorado, mas deve ser definido como um valor não nulo. Para obter mais informações, consulte a seção sobre associação de linha de variáveis TVP em [de associação e Data Transfer of Table-Valued parâmetros e valores de coluna](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md).  
  
 Se *StrLen_Or_Ind* tem qualquer valor diferente de SQL_DEFAULT_PARAM ou um número entre 0 e SQL_PARAMSET_SIZE (ou seja, o *ColumnSize* parâmetro de SQLBindParameter), ocorrerá um erro. Esse erro faz SQLPutData retornar SQL_ERROR: SQLSTATE=HY090, "Comprimento de buffer ou de cadeia de caracteres inválido".  
  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros com valor de tabela &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlputdata-support-for-enhanced-date-and-time-features"></a>Suporte de SQLPutData a recursos aprimorados de data e hora  
 Valores de parâmetros de tipos de data/hora são convertidos conforme descrito em [conversões do C para SQL](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md).  
  
 Para obter mais informações, consulte [data e hora melhorias &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlputdata-support-for-large-clr-udts"></a>Suporte de SQLPutData a UDTs grandes do CLR  
 **SQLPutData** oferece suporte a grandes CLR definido pelo usuário (UDTs tipos). Para obter mais informações, consulte [Large CLR User-Defined tipos &#40; ODBC &#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
 [SQLPutData Function](http://go.microsoft.com/fwlink/?LinkId=59365)   
 [Detalhes de implementação de API de ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
