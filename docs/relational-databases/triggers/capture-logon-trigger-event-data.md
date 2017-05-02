---
title: Capturar dados de eventos do gatilho de logon | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e05b1ab4-c10b-402a-9591-f6ec1e3db8c0
caps.latest.revision: 5
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 790a086c90eeeeb606a86056f239853d805cb091
ms.lasthandoff: 04/11/2017

---
# <a name="capture-logon-trigger-event-data"></a>Capturar dados de eventos do gatilho de logon
  Para capturar dados XML sobre eventos LOGON para uso nos gatilhos de logon, use a função [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md) . O evento LOGON retorna o seguinte esquema de dados de evento:  
  
 `<EVENT_INSTANCE>`  
  
 `<EventType>event_type</EventType>`  
  
 `<PostTime>post_time</PostTime>`  
  
 `<SPID>spid</SPID>`  
  
 `<ServerName>server_name</ServerName>`  
  
 `<LoginName>login_name</LoginName>`  
  
 `<LoginType>login_type</LoginType>`  
  
 `<SID>sid</SID>`  
  
 `<ClientHost>client_host</ClientHost>`  
  
 `<IsPooled>is_pooled</IsPooled>`  
  
 `</EVENT_INSTANCE>`  
  
 `<EventType>`  
 Contém `LOGON`.  
  
 `<PostTime>`  
 Contém a hora em que foi solicitado o estabelecimento de uma sessão.  
  
 `<SID>`  
 Contém o fluxo binário codificado de base 64 do número de identificação de segurança (SID) do nome de logon especificado.  
  
 `<ClientHost>`  
 Contém o nome do host do cliente de onde é feita a conexão. O valor será '`<local_machine>`' se o nome do cliente e do servidor forem idênticos. Caso contrário, o valor é o endereço de IP do cliente.  
  
 `<IsPooled>`  
 Será `1` se a conexão for reutilizada por meio de pool de conexões. Caso contrário, o valor é `0`.  
  
  
