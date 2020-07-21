---
title: MSSQLSERVER_9790 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 9790 (Database Engine error)
ms.assetid: 83fd379f-5deb-4f97-8cb4-282e3d3fed94
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 89df2193a1b2c92f40d3e42dcfc6b385779e3e80
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552981"
---
# <a name="mssqlserver_9790"></a>MSSQLSERVER_9790
    
## <a name="details"></a>Detalhes  
  
|Atributo|Valor|  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|9790|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SB3_XMIT_ERROR_ENTRANCE_BROKER_SINGLE_USER|  
|Texto da mensagem|Não é possível rotear a mensagem de entrada. O banco de dados de sistema MSDB que contém informações de roteamento está no modo SINGLE USER.|  
  
## <a name="explanation"></a>Explicação  
 Ocorreu um erro ao tentar classificar uma mensagem recebida sem-cabo porque o banco de dados MSDB estava no modo usuário único.  
  
## <a name="user-action"></a>Ação do usuário  
 Altere o MSDB para o modo MULTI USER com o comando ALTER DATABASE.  
  
  
