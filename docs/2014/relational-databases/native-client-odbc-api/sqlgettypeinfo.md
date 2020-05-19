---
title: SQLGetTypeInfo | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLGetTypeInfo function
ms.assetid: 13b982c3-ae03-4155-bc0d-e225050703ce
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4237ebcc22318fdd6a93af09a79d7f8e2bea8989
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705993"
---
# <a name="sqlgettypeinfo"></a>SQLGetTypeInfo
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client relata o tipo de coluna adicional no conjunto de resultados de `SQLGetTypeInfo` . USERTYPE informa a definição do tipo de dados da biblioteca do banco de dados, sendo útil para desenvolvedores que estejam portando aplicativos existentes da biblioteca para ODBC.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trata identidade como um atributo, ao passo que o ODBC a trata como um tipo de dados. Para resolver essa incompatibilidade, `SQLGetTypeInfo` retorna os tipos de dados: **intidentity**, **smallintidentity**, **tinyintidentity**, **decimalidentity**e **NumericIdentity**. A `SQLGetTypeInfo` coluna conjunto de resultados AUTO_UNIQUE_VALUE relata o valor true para esses tipos de dados.  
  
 Para **varchar**, **nvarchar** e **varbinary**, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client continua a relatar 8000, 4000 e 8000, respectivamente, para o valor COLUMN_SIZE, mesmo que seja realmente ilimitado. Isso é para assegurar a compatibilidade com versões anteriores.  
  
 Para o tipo de dados **XML** , o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client relata SQL_SS_LENGTH_UNLIMITED para COLUMN_SIZE para denotar tamanho ilimitado.  
  
## <a name="sqlgettypeinfo-and-table-valued-parameters"></a>SQLGetTypeInfo e parâmetros com valor de tabela  
 O tipo de tabela para parâmetros com valor de tabela é efetivamente um meta-tipo, ou seja, um tipo usado para definir outros tipos. Portanto, ele não precisa ser exposto por meio do SQLGetTypeInfo. Os aplicativos devem usar SQLTables, em vez de SQLGetTypeInfo, para recuperar metadados para tipos de tabela usados com parâmetros com valor de tabela.  
  
 Para obter mais informações, sobre como recuperar metdata para parâmetros com valor de tabela, consulte [atributos de instrução que afetam os parâmetros com valor de tabela](../native-client-odbc-table-valued-parameters/statement-attributes-that-affect-table-valued-parameters.md).  
  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros com valor de tabela &#40;&#41;ODBC ](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlgettypeinfo-support-for-enhanced-date-and-time-features"></a>Suporte de SQLGetTypeInfo a recursos aprimorados de data e hora  
 Para obter os valores retornados para tipos de data/hora, consulte [Catalog Metadata](../native-client-odbc-date-time/metadata-catalog.md).  
  
 Para obter mais informações gerais, consulte [melhorias de data e hora &#40;&#41;ODBC ](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlgettypeinfo-support-for-large-clr-udts"></a>Suporte de SQLGetTypeInfo a grandes UDTs do CLR  
 `SQLGetTypeInfo` dá suporte a UDTs grandes do CLR. Para obter mais informações, consulte [tipos CLR grandes definidos pelo usuário &#40;&#41;ODBC ](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLGetTypeInfo](https://go.microsoft.com/fwlink/?LinkId=59356)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
