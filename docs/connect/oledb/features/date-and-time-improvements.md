---
title: Aprimoramentos de data e hora | Microsoft Docs
description: Conheça o suporte do Driver do OLE DB para SQL Server para os novos tipos de dados de data e hora adicionados ao SQL Server 2008.
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ba77a851ca8193ab3f809352d0d7804cc8189f6c
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861490"
---
# <a name="date-and-time-improvements"></a>Melhorias de data e hora
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Este tópico descreve o suporte ao Driver do OLE DB para SQL Server para os novos tipos de dados de data e hora que foram incluídos no [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)].  
  
 Para obter mais informações sobre aprimoramentos de data/hora, confira [Aprimoramentos de data e hora &#40;OLE DB&#41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md).  
  
 Para obter informações sobre aplicativos de exemplo que demonstram esse recurso, confira [Amostras de programação do SQL Server Data](https://msftdpprodsamples.codeplex.com/).  
  
## <a name="usage"></a>Uso  
 As seções a seguir descrevem vários modos de usar os novos tipos de dados date e time.  
  
### <a name="use-date-as-a-distinct-data-type"></a>Usar Date como um tipo de dados distinto  
 Do [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] em diante, o suporte avançado para tipos de data/hora torna mais eficiente o uso do tipo de OLE DB DBTYPE_DBDATE.  
  
### <a name="use-time-as-a-distinct-data-type"></a>Usar Time como um tipo de dados distinto  
 O OLE DB já tem um tipo de dados que apenas contém a hora, DBTYPE_DBTIME, que tem uma precisão de 1 segundo.
  
 O novo tipo de dados temporal do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tem segundos fracionários precisos até 100 nanossegundos. Isso requer um novo tipo no Driver do OLE DB para SQL Server: DBTYPE_DBTIME2. Os aplicativos existentes gravados para usar horas sem frações de segundos podem usar colunas time(0). O tipo DBTYPE_TIME existente do OLE DB e seus structs correspondentes devem funcionar corretamente, a menos que os aplicativos dependam do tipo retornado nos metadados.  
  
### <a name="use-time-as-a-distinct-data-type-with-extended-fractional-seconds-precision"></a>Usar Time como um tipo de dados distinto com precisão estendida de frações de segundos  
 Alguns aplicativos, como controle de processo e fabricação, requerem o recurso para controlar dados de hora com uma precisão de até 100 nanossegundos. O novo tipo para essa finalidade no OLE DB é DBTYPE_DBTIME2.  
  
### <a name="use-datetime-with-extended-fractional-seconds-precision"></a>Usar Datetime com precisão estendida de frações de segundos  
 O OLE DB já define um tipo com uma precisão de até 1 nanossegundo. Porém, este tipo já é usado por aplicativos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e tais aplicativos têm uma expectativa de apenas 1/300 de uma segunda precisão. O novo tipo **datetime2(3)** não é diretamente compatível com o tipo datetime existente. Se houver um risco que isto afetará o comportamento do aplicativo, os aplicativos deverão usar um novo sinalizador DBCOLUMN para determinar o tipo de servidor real.    
  
### <a name="use-datetime-with-extended-fractional-seconds-precision-and-timezone"></a>Usar Datetime com precisão estendida de frações de segundos e fuso horário  
 Alguns aplicativos exigem valores de datetime com informações de fuso horário. Isso é compatível com o novo tipo DBTYPE_DBTIMESTAMPOFFSET.
  
### <a name="use-datetimedatetimedatetimeoffset-data-with-client-side-conversions-consistent-with-existing-conversions"></a>Usar os dados Date/Time/Datetime/Datetimeoffset com conversões do lado do cliente consistentes com as conversões existentes  
 As conversões são estendidas de uma maneira consistente para incluir conversões entre todos os tipos de data e hora introduzidos no [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos do Driver do OLE DB para SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
