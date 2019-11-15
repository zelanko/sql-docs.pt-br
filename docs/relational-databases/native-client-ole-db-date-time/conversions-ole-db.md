---
title: Associações e conversões (OLE DB)
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- conversions [OLE DB]
- bindings [OLE DB]
- OLE DB, bindings and conversions
ms.assetid: c187df58-a8c8-4c74-a76f-663abbc5f0c1
author: MightyPen
ms.author: genemi
ms.custom: seo-dt-2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a1d02ef5827ff9d121c19dd055f97feea5184758
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095353"
---
# <a name="conversions-ole-db"></a>Conversões (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Esta seção discute como converter entre os valores **DateTime** e **DateTimeOffset** . As conversões descritas nesta seção já são fornecidas pelo OLE DB ou são uma extensão consistente do OLE DB.  
  
 O formato de literais e cadeias de caracteres para datas e horas no OLE DB geralmente segue a norma ISO e não depende da localidade do cliente. Uma exceção é DBTYPE_DATE, em que o padrão é Automação OLE. Entretanto, como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client só converte entre tipos quando os dados são transmitidos para ou do cliente, não há como um aplicativo obrigar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client a converter entre DBTYPE_DATE e formatos de cadeia de caracteres. Caso contrário, as cadeias de caracteres usam os formatos a seguir (texto entre colchetes indica um elemento opcional):  
  
-   O formato das cadeias de caracteres **DateTime** e **DateTimeOffset** é:  
  
     *yyyy*-*mm*-*dd*[ *hh*:*mm*:*ss*[.*9999999*][ ± *hh*:*mm*]]  
  
-   O formato de cadeias de caracteres **time** é:  
  
     *hh*:*mm*:*ss*[.*9999999*]  
  
-   O formato das cadeias de caracteres de **Data** é:  
  
     *yyyy*-*mm*-*dd*  
  
> [!NOTE]  
>  As versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client e SQLOLEDB implementavam conversões OLE, caso em que conversões padrão falhavam. Consequentemente, algumas conversões executadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 10.0 e versões posteriores diferem da especificação OLE DB.  
  
 As conversões de cadeias de caracteres permitem uma flexibilidade nos espaços em branco e na largura dos campos. Para obter mais informações, consulte a seção "formatos de dados: cadeias de caracteres e literais" em [suporte de tipo de dados para OLE DB melhorias de data e hora](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md).  
  
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
 [Conversões executadas do cliente para o servidor](../../relational-databases/native-client-ole-db-date-time/conversions-performed-from-client-to-server.md)  
 Descreve conversões de data/hora executadas entre um aplicativo cliente escrito com o OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client e o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (ou posterior).  
  
 [Conversões executadas do servidor para o cliente](../../relational-databases/native-client-ole-db-date-time/conversions-performed-from-server-to-client.md)  
 Descreve conversões de data/hora executadas entre o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (ou posterior) e um aplicativo cliente escrito com o DB OLE do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="see-also"></a>Consulte também  
 [Melhorias de data e hora &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
