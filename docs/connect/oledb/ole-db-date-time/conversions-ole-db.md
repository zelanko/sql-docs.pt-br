---
title: Associações e conversões (OLE DB) | Microsoft Docs
description: Associações e conversões (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- conversions [OLE DB]
- bindings [OLE DB]
- OLE DB, bindings and conversions
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 233c9e7e2aefbdae34f964e95dbeb7d10d55a63d
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2018
ms.locfileid: "39105872"
---
# <a name="conversions-ole-db"></a>Conversões (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Esta seção discute como converter entre **datetime** e **datetimeoffset** valores. As conversões descritas nesta seção já são fornecidas pelo OLE DB ou são uma extensão consistente do OLE DB.  
  
 O formato de literais e cadeias de caracteres para datas e horas no OLE DB geralmente segue a norma ISO e não depende da localidade do cliente. Uma exceção é DBTYPE_DATE, em que o padrão é Automação OLE. No entanto, porque o Driver do OLE DB para SQL Server só converte entre tipos quando os dados são transmitidos para ou do cliente, não é possível para um aplicativo forçar o Driver do OLE DB para SQL Server converter entre DBTYPE_DATE e cadeia de caracteres de formatos. Caso contrário, as cadeias de caracteres usam os formatos a seguir (texto entre colchetes indica um elemento opcional):  
  
-   O formato do **datetime** e **datetimeoffset** cadeias de caracteres é:  
  
     *aaaa*-*mm*-*dd*[ *hh*:*mm*:*ss*[. *9999999*] [± *hh*:*mm*]]  
  
-   O formato de cadeias de caracteres **time** é:  
  
     *hh*:*mm*:*ss*[.*9999999*]  
  
-   O formato do **data** cadeias de caracteres é:  
  
     *yyyy*-*mm*-*dd*  
  
> [!NOTE]  
>  As versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e SQLOLEDB implementavam conversões OLE, caso em que conversões padrão falhavam. O Driver do OLE DB para SQL Server segue o mesmo comportamento que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Como resultado, algumas conversões executadas pelo Driver do OLE DB para SQL Server diferem da especificação OLE DB.  
  
 As conversões de cadeias de caracteres permitem uma flexibilidade nos espaços em branco e na largura dos campos. Para obter mais informações, consulte a seção "Formatos de dados: cadeias de caracteres e literais" [suporte de tipo de dados para OLE DB aprimoramentos de data e hora](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md).  
  
 Seguem as regras de conversão gerais:  
  
-   Quando uma cadeia de caracteres é convertida em um tipo de data/hora, a cadeia de caracteres é analisada primeiro como um literal ISO. Se esse procedimento falhar, a cadeia de caracteres será analisada como um literal de data OLE, que tem componentes de hora.  
  
-   Se não houver uma hora mas o receptor puder armazenar horas, a hora será definida como zero. Se não houver uma data mas o receptor puder armazenar datas, a data será definida como a data atual quando conversões ISO forem usadas e como 1899-12-30 quando conversões OLE forem usadas.  
  
-   Se não houver um fuso horário no tipo de dados que o cliente está utilizando mas o servidor puder armazenar fusos horários, a data no cliente será assumida como o fuso horário do cliente.  
  
-   Se não houver nenhum fuso horário no servidor mas o cliente tiver informações de fusos horários, o fuso horário de UTC será assumido. Esse é um comportamento diferente daquele do servidor.  
  
-   Se houver uma hora mas o receptor não puder armazenar horas, o componente de hora será ignorado.  
  
-   Se houver uma data mas o receptor não puder armazenar datas, o componente de data será ignorado.  
  
-   Se ocorrer o truncamento de segundos ou segundos fracionários ao converter de cliente em servidor, DB_E_ERRORSOCCURRED será retornado e o status DBSTATUS_E_DATAOVERFLOW será definido.  
  
-   Se ocorrer o truncamento de segundos ou segundos fracionários ao converter de servidor em cliente, DBSTATUS_S_TRUNCATED será definido.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Conversões executadas do cliente para o servidor](../../oledb/ole-db-date-time/conversions-performed-from-client-to-server.md)  
 Descreve as conversões de data/hora executadas entre um aplicativo cliente escrito com o OLE DB Driver for SQL Server e o [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] (ou posterior).  
  
 [Conversões executadas do servidor para o cliente](../../oledb/ole-db-date-time/conversions-performed-from-server-to-client.md)  
 Descreve as conversões de data/hora executadas entre o [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] (ou posterior) e um aplicativo cliente escrito com o OLE DB Driver for SQL Server.  
  
## <a name="see-also"></a>Consulte Também  
 [Melhorias de data e hora &#40;OLE DB&#41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
