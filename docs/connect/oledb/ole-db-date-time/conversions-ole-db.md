---
title: Associações e conversões (OLE DB) | Microsoft Docs
description: Associações e conversões (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- conversions [OLE DB]
- bindings [OLE DB]
- OLE DB, bindings and conversions
author: pmasl
ms.author: pelopes
ms.openlocfilehash: dc86193f40474fc373c1b0e7dd48e579e8548821
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "68015841"
---
# <a name="conversions-ole-db"></a>Conversões (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  A seção descreve como converter valores entre os tipos **datetime** e **datetimeoffset**. As conversões descritas nesta seção já são fornecidas pelo OLE DB ou são uma extensão consistente do OLE DB.  
  
 O formato de literais e cadeias de caracteres para datas e horas no OLE DB geralmente segue a norma ISO e não depende da localidade do cliente. Uma exceção é DBTYPE_DATE, em que o padrão é Automação OLE. Entretanto, como o Driver do OLE DB para SQL Server só converte entre tipos quando os dados são transmitidos de/para o cliente, não há como um aplicativo obrigar o Driver do OLE DB para SQL Server a converter valores entre os formatos DBTYPE_DATE e cadeia de caracteres. Caso contrário, as cadeias de caracteres usam os formatos a seguir (texto entre colchetes indica um elemento opcional):  
  
-   O formato das cadeias de caracteres de **datetime** e **datetimeoffset** é:  
  
     *yyyy*-*mm*-*dd*[ *hh*:*mm*:*ss*[.*9999999*][ ± *hh*:*mm*]]  
  
-   O formato de cadeias de caracteres **time** é:  
  
     *hh*:*mm*:*ss*[.*9999999*]  
  
-   O formato das cadeias de caracteres de **date** é:  
  
     *yyyy*-*mm*-*dd*  
  
> [!NOTE]  
>  As versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e SQLOLEDB implementavam conversões OLE, caso em que conversões padrão falhavam. O Driver do OLE DB para SQL Server segue o mesmo comportamento que Cliente Nativo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Consequentemente, algumas conversões executadas pelo Driver do OLE DB para SQL Server diferem da especificação do OLE DB.  
  
 As conversões de cadeias de caracteres permitem uma flexibilidade nos espaços em branco e na largura dos campos. Para obter mais informações, confira a seção "Formatos de dados: cadeias de caracteres e literais" em [Suporte a tipo de dados para aprimoramentos de data e hora do OLE DB](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md).  
  
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
  
  
