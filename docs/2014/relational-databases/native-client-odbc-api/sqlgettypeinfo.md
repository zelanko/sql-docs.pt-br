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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 60c4c4d364f9c07e9ca241dd357535f7f7acb42d
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53373668"
---
# <a name="sqlgettypeinfo"></a>SQLGetTypeInfo
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] relatórios de driver ODBC do Native Client a coluna adicional USERTYPE no resultado do conjunto de `SQLGetTypeInfo`. USERTYPE informa a definição do tipo de dados da biblioteca do banco de dados, sendo útil para desenvolvedores que estejam portando aplicativos existentes da biblioteca para ODBC.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trata identidade como um atributo, ao passo que o ODBC a trata como um tipo de dados. Para resolver essa incompatibilidade `SQLGetTypeInfo` retorna os tipos de dados: **intidentity**, **smallintidentity**, **tinyintidentity**, **decimalidentity** , e **numericidentity**. O `SQLGetTypeInfo` coluna AUTO_UNIQUE_VALUE do conjunto de resultados informa o valor TRUE para esses tipos de dados.  
  
 Para **varchar**, **nvarchar** e **varbinary**, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client continua a relatar 8000, 4000 e 8000 respectivamente para o COLUMN_SIZE valor, mesmo que ele é, na verdade, ilimitado. Isso é para assegurar a compatibilidade com versões anteriores.  
  
 Para o **xml** tipo de dados, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client informa SQL_SS_LENGTH_UNLIMITED para COLUMN_SIZE indicar tamanho ilimitado.  
  
## <a name="sqlgettypeinfo-and-table-valued-parameters"></a>SQLGetTypeInfo e parâmetros com valor de tabela  
 O tipo de tabela para parâmetros com valor de tabela é efetivamente um meta-tipo-que é, um tipo usado para definir outros tipos. Portanto, não tem a ser exposta por meio de SQLGetTypeInfo. Aplicativos devem usar SQLTables, em vez de SQLGetTypeInfo, para recuperar metadados para tipos de tabela usados com parâmetros com valor de tabela.  
  
 Para obter mais informações sobre como recuperar metadados para parâmetros com valor de tabela, consulte [atributos de instrução que os parâmetros Affect Table-Valued](../native-client-odbc-table-valued-parameters/statement-attributes-that-affect-table-valued-parameters.md).  
  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros com valor de tabela &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlgettypeinfo-support-for-enhanced-date-and-time-features"></a>Suporte de SQLGetTypeInfo a recursos aprimorados de data e hora  
 Para obter os valores retornados para tipos de data/hora, consulte [Catalog Metadata](../native-client-odbc-date-time/metadata-catalog.md).  
  
 Para obter mais informações, consulte [aprimoramentos de data e hora &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlgettypeinfo-support-for-large-clr-udts"></a>Suporte de SQLGetTypeInfo a grandes UDTs do CLR  
 `SQLGetTypeInfo` dá suporte a UDTs grandes do CLR. Para obter mais informações, consulte [Large CLR User-Defined tipos &#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
 [Função SQLGetTypeInfo](https://go.microsoft.com/fwlink/?LinkId=59356)   
 [Detalhes da implementação da API do ODBC](odbc-api-implementation-details.md)  
  
  
