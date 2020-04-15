---
title: SQLBindCol | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLBindCol function
ms.assetid: fbd7ba20-d917-4ca9-b018-018ac6af9f98
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 69457daccbc7868e58f91c71a48b4b25f15f5318
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302688"
---
# <a name="sqlbindcol"></a>SQLBindCol
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Como regra geral, considere as implicações de usar **SQLBindCol** para causar conversão de dados. As conversões de associações são processos do cliente, portanto, por exemplo, recuperar um valor de ponto flutuante associado a uma coluna de caracteres faz com que o driver execute a conversão flutuante para caractere localmente quando uma linha é buscada. A função CONVERT do [!INCLUDE[tsql](../../includes/tsql-md.md)] pode ser usada para inserir o custo da conversão de dados no servidor.  
  
 Uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode retornar vários conjuntos de linhas de resultado em uma única execução de instrução. Cada conjunto de resultados deve ser associado separadamente. Para obter mais informações sobre como associar vários conjuntos de resultados, consulte [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md).  
  
 O desenvolvedor pode vincular [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]colunas a tipos de dados C específicos usando o valor *targetType* **SQL_C_BINARY**. Colunas associadas a tipos específicos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]não são portáteis. Os tipos de dados C de ODBC definidos e específicos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]correspondem às definições de tipo para DB-Library e os desenvolvedores de DB-Library portando aplicativos podem desejar tirar proveito desse recurso.  
  
 Informar o truncamento de dados é um processo caro para o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Você pode evitar o truncamento assegurando que todos os buffers de dados associados tenham largura suficiente para retornar dados. Para dados de caracteres, a largura deve incluir espaço para um terminador da cadeia de caracteres quando o comportamento padrão do driver para a terminação da cadeia de caracteres for usado. Por exemplo, a associação de uma coluna [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **char(5)** a uma matriz de cinco caracteres resulta em truncagem para todos os valores buscados. A associação da mesma coluna a uma matriz de seis caracteres evita a truncagem, fornecendo um elemento de caractere no qual armazenar o terminador nulo. [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) pode ser usado para recuperar com eficiência dados de caracteres longos e dados binários sem truncagem.  
  
 Para tipos de dados de grande valor, se o buffer fornecido pelo usuário não for grande o suficiente para conter todo o valor da coluna, **SQL_SUCCESS_WITH_INFO** é devolvido e os "dados de seqüência; aviso de truncação direita "é emitido. O argumento **StrLen_or_IndPtr** conterá o número de chars/bytes armazenados no buffer.  
  
## <a name="sqlbindcol-support-for-enhanced-date-and-time-features"></a>Suporte de SQLBindCol a recursos aprimorados de data e hora  
 Os valores da coluna de resultados dos tipos de data/hora são convertidos conforme descrito em [Conversões de SQL para C](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md). Observe que para recuperar as colunas de data e hora definidas como suas estruturas correspondentes **(SQL_SS_TIME2_STRUCT** e **SQL_SS_TIMESTAMPOFFSET_STRUCT),** *o TargetType* deve ser especificado como **SQL_C_DEFAULT** ou **SQL_C_BINARY**.  
  
 Para obter mais informações, consulte [melhorias de data e hora &#40;&#41;da ODBC ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlbindcol-support-for-large-clr-udts"></a>Suporte de SQLBindCol para CLR UDTs grandes  
 **SQLBindCol** dá suporte a tipos de dados CLR definidos pelo usuário. Para obter mais informações, consulte [Grandes tipos definidos pelo usuário da CLR &#40;&#41;ODBC ](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLBindCol](https://go.microsoft.com/fwlink/?LinkId=59327)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
