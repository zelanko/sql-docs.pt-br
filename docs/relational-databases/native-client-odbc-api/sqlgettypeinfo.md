---
title: SQLGetTypeInfo | Microsoft Docs
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
helpviewer_keywords: SQLGetTypeInfo function
ms.assetid: 13b982c3-ae03-4155-bc0d-e225050703ce
caps.latest.revision: "47"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 27e02520cffa658b9c7a59b1848ee349eed698f5
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="sqlgettypeinfo"></a>SQLGetTypeInfo
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] relatórios de driver ODBC Native Client a coluna adicional USERTYPE no resultado do conjunto de **SQLGetTypeInfo**. USERTYPE informa a definição do tipo de dados da biblioteca do banco de dados, sendo útil para desenvolvedores que estejam portando aplicativos existentes da biblioteca para ODBC.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trata identidade como um atributo, ao passo que o ODBC a trata como um tipo de dados. Para resolver essa incompatibilidade, **SQLGetTypeInfo** retorna os tipos de dados: **intidentity**, **smallintidentity**, **tinyintidentity**, **decimalidentity**, e **numericidentity**. O **SQLGetTypeInfo** coluna AUTO_UNIQUE_VALUE do conjunto de resultados informa o valor TRUE para esses tipos de dados.  
  
 Para **varchar**, **nvarchar** e **varbinary**, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client continua a relatar 8000, 4000 e 8000 respectivamente para o COLUMN_SIZE o valor, mesmo que ele é, na verdade, ilimitado. Isso é para assegurar a compatibilidade com versões anteriores.  
  
 Para o **xml** tipo de dados, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client informa SQL_SS_LENGTH_UNLIMITED para COLUMN_SIZE a fim de indicar tamanho ilimitado.  
  
## <a name="sqlgettypeinfo-and-table-valued-parameters"></a>SQLGetTypeInfo e parâmetros com valor de tabela  
 O tipo de tabela para parâmetros com valor de tabela é, na verdade, metatipo, ou seja, um tipo usado para definir outros tipos. Portanto, ele não tem a serem expostas por meio de SQLGetTypeInfo. Aplicativos devem usar SQLTables, em vez de SQLGetTypeInfo, para recuperar metadados para tipos de tabela usados com parâmetros com valor de tabela.  
  
 Para obter mais informações sobre como recuperar metadados para parâmetros com valor de tabela, consulte [atributos de instrução que parâmetros Affect Table-Valued](../../relational-databases/native-client-odbc-table-valued-parameters/statement-attributes-that-affect-table-valued-parameters.md).  
  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros com valor de tabela &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlgettypeinfo-support-for-enhanced-date-and-time-features"></a>Suporte de SQLGetTypeInfo a recursos aprimorados de data e hora  
 Para os valores retornados para tipos de data/hora, consulte [metadados de catálogo](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md).  
  
 Para obter mais informações, consulte [data e hora melhorias &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlgettypeinfo-support-for-large-clr-udts"></a>Suporte de SQLGetTypeInfo a grandes UDTs do CLR  
 **SQLGetTypeInfo** oferece suporte a grandes CLR definido pelo usuário (UDTs tipos). Para obter mais informações, consulte [Large CLR User-Defined tipos &#40; ODBC &#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLGetTypeInfo](http://go.microsoft.com/fwlink/?LinkId=59356)   
 [Detalhes da implementação da API do ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
