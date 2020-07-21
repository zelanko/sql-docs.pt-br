---
title: MSSQLSERVER_1807 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1807 (Database Engine error)
ms.assetid: 13c1b240-098b-4d9e-89aa-21599548e074
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9cf2edc55900ceb2181d5ae0d300300376f3ecbe
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553481"
---
# <a name="mssqlserver_1807"></a>MSSQLSERVER_1807
    
## <a name="details"></a>Detalhes  
  
|Atributo|Valor|  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|1807|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|CANNOT_EX_LOCK|  
|Texto da mensagem|Não foi possível obter bloqueio exclusivo no banco de dados '%.*ls'. Tente novamente a operação mais tarde.|  
  
## <a name="explanation"></a>Explicação  
 Uma operação que exigia acesso exclusivo ao banco de dados não pôde obtê-lo.  
  
## <a name="user-action"></a>Ação do usuário  
 Desconecte todas as conexões com esse banco de dados ou tente a consulta novamente mais tarde.  
  
  
