---
title: Data e hora melhorias | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client|features
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 9b1d0d9d-1f6e-4399-8f61-e23f9a486a7a
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: e2077845a348243b8f2e68563580028f6d656354
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="date-and-time-improvements"></a>Aprimoramentos de hora e data
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Este tópico descreve o suporte ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client para os novos tipos de dados de data e hora que foram incluídos no [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)].  
  
 Para obter mais informações sobre aprimoramentos de data/hora, consulte [data e hora melhorias &#40;OLE DB&#41; ](../../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md) e [data e hora melhorias &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
 Para obter informações sobre aplicativos de exemplo que demonstram esse recurso, consulte [exemplos de programação de dados do SQL Server](http://msftdpprodsamples.codeplex.com/).  
  
## <a name="usage"></a>Uso  
 As seções a seguir descrevem vários modos de usar os novos tipos de dados date e time.  
  
### <a name="use-date-as-a-distinct-data-type"></a>Usar Date como um tipo de dados distinto  
 A partir do [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], o suporte avançado para tipos de data/hora torna-o mais eficiente para usar o tipo de ODBC SQL_TYPE_DATE (SQL_DATE para aplicativos ODBC 2.0) e o tipo de OLE DB DBTYPE_DBDATE.  
  
### <a name="use-time-as-a-distinct-data-type"></a>Usar Time como um tipo de dados distinto  
 O OLE DB já tem um tipo de dados que apenas contém a hora, DBTYPE_DBTIME, que tem uma precisão de 1 segundo. Em ODBC, o tipo equivalente é SQL_TYPE_TIME (SQL_TIME para aplicativos ODBC 2.0).  
  
 O novo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tempo ao tipo de dados tem frações de segundos precisas para 100 nanossegundos. Isto exige novos tipos em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client: DBTYPE_DBTIME2 (OLE DB) e SQL_SS_TIME2 (ODBC). Os aplicativos existentes gravados para usar horas sem frações de segundos podem usar colunas time(0). Os tipos DBTYPE_TIME do OLE DB e SQL_TYPE_TIME do ODBC e suas estruturas correspondentes devem funcionar corretamente, a menos que os aplicativos confiem no tipo retornado no metadados.  
  
### <a name="use-time-as-a-distinct-data-type-with-extended-fractional-seconds-precision"></a>Usar Time como um tipo de dados distinto com precisão estendida de frações de segundos  
 Alguns aplicativos, como controle de processo e fabricação, requerem o recurso para controlar dados de hora com uma precisão de até 100 nanossegundos. Os novos tipos para esta finalidade são DBTYPE_DBTIME2 (OLE DB) e SQL_SS_TIME2 (ODBC).  
  
### <a name="use-datetime-with-extended-fractional-seconds-precision"></a>Usar Datetime com precisão estendida de frações de segundos  
 O OLE DB já define um tipo com uma precisão de até 1 nanossegundo. Porém, este tipo já é usado por aplicativos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e tais aplicativos têm uma expectativa de apenas 1/300 de uma segunda precisão. O novo **datetime2(3)** tipo não é diretamente compatível com o tipo datetime existente. Se houver um risco que isto afetará o comportamento do aplicativo, os aplicativos deverão usar um novo sinalizador DBCOLUMN para determinar o tipo de servidor real.  
  
 O ODBC também define um tipo com uma precisão de até 1 nanossegundo. Porém, esse tipo já é usado pelos aplicativos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] existentes e tais aplicativos esperam uma precisão de apenas 3 milissegundos. O novo **datetime2(3)** tipo não é diretamente compatível com o existente **datetime** tipo. **datetime2(3)** tem uma precisão de um milissegundo e **datetime** tem uma precisão de 1/300 de segundo. No ODBC, os aplicativos podem determinar qual tipo de servidor está em uso com o campo do descritor SQL_DESC_TYPE_NAME. Portanto, o tipo existente SQL_TYPE_TIMESTAMP (SQL_TIMESTAMP para aplicativos ODBC 2.0) pode ser usado para ambos os tipos.  
  
### <a name="use-datetime-with-extended-fractional-seconds-precision-and-timezone"></a>Usar Datetime com precisão estendida de frações de segundos e fuso horário  
 Alguns aplicativos exigem valores de datetime com informações de fuso horário. Isto é aceito pelos novos tipos DBTYPE_DBTIMESTAMPOFFSET (OLE DB) e SQL_SS_TIMESTAMPOFFSET (ODBC).  
  
### <a name="use-datetimedatetimedatetimeoffset-data-with-client-side-conversions-consistent-with-existing-conversions"></a>Usar os dados Date/Time/Datetime/Datetimeoffset com conversões do lado do cliente consistentes com as conversões existentes  
 O padrão de ODBC descreve como conversões entre os tipos existentes de data, hora e carimbo de data/hora funcionam. Esses tipos são estendidos de uma maneira consistente para incluir conversões entre todos os tipos de data e hora inseridos no [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Recursos do SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
