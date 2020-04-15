---
title: SqlGetTypeInfo | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetTypeInfo function
ms.assetid: 13b982c3-ae03-4155-bc0d-e225050703ce
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 81ba57c6e66f156f13055ff5ec941fa8f0c86381
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298429"
---
# <a name="sqlgettypeinfo"></a>SQLGetTypeInfo
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver Cliente Nativo ODBC relata a coluna adicional USERTYPE no conjunto de resultados do **SQLGetTypeInfo**. USERTYPE informa a definição do tipo de dados da biblioteca do banco de dados, sendo útil para desenvolvedores que estejam portando aplicativos existentes da biblioteca para ODBC.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trata identidade como um atributo, ao passo que o ODBC a trata como um tipo de dados. Para resolver essa incompatibilidade, **o SQLGetTypeInfo** retorna os tipos de dados: **intidentity**, **smallintidentity,** **tinyintidentity,** **decimalidentity**e **numericidentity**. A coluna de conjunto de resultados **SQLGetTypeInfo** AUTO_UNIQUE_VALUE informa o valor TRUE para esses tipos de dados.  
  
 Para **varchar**, **nvarchar** e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **varbinary**, o driver Cliente Nativo ODBC continua a relatar 8000, 4000 e 8000, respectivamente, para o valor COLUMN_SIZE, embora seja realmente ilimitado. Isso é para assegurar a compatibilidade com versões anteriores.  
  
 Para o tipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados **xml,** o driver Cliente Nativo ODBC informa SQL_SS_LENGTH_UNLIMITED para COLUMN_SIZE denotar tamanho ilimitado.  
  
## <a name="sqlgettypeinfo-and-table-valued-parameters"></a>SQLGetTypeInfo e parâmetros com valor de tabela  
 O tipo de tabela para parâmetros de valor de tabela é efetivamente um metatipo-ou seja, um tipo usado para definir outros tipos. Portanto, ele não precisa ser exposto através do SQLGetTypeInfo. Os aplicativos devem usar SQLTables, em vez de SQLGetTypeInfo, para recuperar metadados para tipos de tabela usados com parâmetros de valor de tabela.  
  
 Para obter mais informações sobre a recuperação de dados metdados para parâmetros avaliados na tabela, consulte [Atributos de declaração que afetam parâmetros avaliados na tabela](../../relational-databases/native-client-odbc-table-valued-parameters/statement-attributes-that-affect-table-valued-parameters.md).  
  
 Para obter mais informações sobre parâmetros avaliados em tabela, consulte [Parâmetros valorizados em tabela &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlgettypeinfo-support-for-enhanced-date-and-time-features"></a>Suporte de SQLGetTypeInfo a recursos aprimorados de data e hora  
 Para obter os valores retornados para tipos de data/hora, consulte [Catalog Metadata](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md).  
  
 Para obter informações mais gerais, consulte [melhorias de data e hora &#40;&#41;o DBC ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlgettypeinfo-support-for-large-clr-udts"></a>Suporte de SQLGetTypeInfo a grandes UDTs do CLR  
 **O SQLGetTypeInfo** suporta grandes tipos definidos pelo usuário CLR (UDTs). Para obter mais informações, consulte [Grandes tipos definidos pelo usuário da CLR &#40;&#41;ODBC ](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLGetTypeInfo](https://go.microsoft.com/fwlink/?LinkId=59356)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
