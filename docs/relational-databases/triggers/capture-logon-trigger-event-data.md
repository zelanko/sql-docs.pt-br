---
title: Capturar dados de eventos do gatilho de logon | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e05b1ab4-c10b-402a-9591-f6ec1e3db8c0
author: rothja
ms.author: jroth
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c758e9d1e18e3f3db73a25422200ab78ffb01eb7
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43072925"
---
# <a name="capture-logon-trigger-event-data"></a>Capturar dados de eventos do gatilho de logon
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
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
  
  
