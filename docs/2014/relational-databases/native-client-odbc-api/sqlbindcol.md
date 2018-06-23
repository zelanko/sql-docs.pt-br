---
title: SQLBindCol | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLBindCol function
ms.assetid: fbd7ba20-d917-4ca9-b018-018ac6af9f98
caps.latest.revision: 39
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 2bd30b241f36a8650408fc83142c18558951333b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121927"
---
# <a name="sqlbindcol"></a>SQLBindCol
  Como regra geral, considere as implicações de usar **SQLBindCol** para causar conversão de dados. As conversões de associações são processos do cliente, portanto, por exemplo, recuperar um valor de ponto flutuante associado a uma coluna de caracteres faz com que o driver execute a conversão flutuante para caractere localmente quando uma linha é buscada. A função CONVERT do [!INCLUDE[tsql](../../includes/tsql-md.md)] pode ser usada para inserir o custo da conversão de dados no servidor.  
  
 Uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode retornar vários conjuntos de linhas de resultado em uma única execução de instrução. Cada conjunto de resultados deve ser associado separadamente. Para obter mais informações sobre como associar vários conjuntos de resultados, consulte [SQLMoreResults](sqlmoreresults.md).  
  
 O desenvolvedor pode associar colunas a serem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-tipos de dados C específicos usando o *TargetType* valor `SQL_C_BINARY`. Colunas associadas a tipos específicos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não são portáteis. Os tipos de dados C de ODBC definidos e específicos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] correspondem às definições de tipo para DB-Library e os desenvolvedores de DB-Library portando aplicativos podem desejar tirar proveito desse recurso.  
  
 Truncamento de dados de relatórios é um processo caro para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client. Você pode evitar o truncamento assegurando que todos os buffers de dados associados tenham largura suficiente para retornar dados. Para dados de caracteres, a largura deve incluir espaço para um terminador da cadeia de caracteres quando o comportamento padrão do driver para a terminação da cadeia de caracteres for usado. Por exemplo, a associação um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **char (5)** coluna a uma matriz de cinco caracteres resulta em truncagem para todos os valores buscados. A associação da mesma coluna a uma matriz de seis caracteres evita a truncagem, fornecendo um elemento de caractere no qual armazenar o terminador nulo. [SQLGetData](sqlgetdata.md) pode ser usado para recuperar dados de caracteres longos e binários sem truncamento de maneira eficiente.  
  
 Para tipos de dados com valor grande, se o buffer fornecido do usuário não for grande o suficiente para reter todo o valor da coluna, `SQL_SUCCESS_WITH_INFO` será retornado e o aviso do tipo “dados da cadeia de caracteres; truncagem à direita” será emitido. O argumento `StrLen_or_IndPtr` conterá o número de chars/bytes armazenados no buffer.  
  
## <a name="sqlbindcol-support-for-enhanced-date-and-time-features"></a>Suporte de SQLBindCol a recursos aprimorados de data e hora  
 Valores de coluna de resultado dos tipos de data/hora são convertidos conforme descrito em [conversões de SQL para C](../native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md). Observe que para recuperar colunas hora e datetimeoffset como suas estruturas correspondentes (`SQL_SS_TIME2_STRUCT` e **SQL_SS_TIMESTAMPOFFSET_STRUCT**), *TargetType* devem ser especificados como `SQL_C_DEFAULT` ou `SQL_C_BINARY`.  
  
 Para obter mais informações, consulte [data e hora melhorias &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlbindcol-support-for-large-clr-udts"></a>Suporte de SQLBindCol para CLR UDTs grandes  
 **SQLBindCol** dá suporte a tipos de dados CLR definidos pelo usuário. Para obter mais informações, consulte [Large CLR User-Defined tipos &#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
 [Função SQLBindCol](http://go.microsoft.com/fwlink/?LinkId=59327)   
 [Detalhes da implementação da API do ODBC](odbc-api-implementation-details.md)  
  
  