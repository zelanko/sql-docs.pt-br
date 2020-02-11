---
title: MSSQLSERVER_17128 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17128 (Database Engine error)
ms.assetid: 7b15a5e6-fd41-47ce-ba87-54f72acea4bb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7a73f2469c38d611b95e3446e80755687f40346e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62869704"
---
# <a name="mssqlserver_17128"></a>MSSQLSERVER_17128
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|17128|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|INIT_NOBUFSPACE|  
|Texto da mensagem|initdata: Nenhuma memória para buffers de kernel.|  
  
## <a name="explanation"></a>Explicação  
 Falha nas alocações ou reservas de memória iniciais do pool de buffers. O SQL Server foi encerrado.  
  
## <a name="user-action"></a>Ação do usuário  
 Isso geralmente ocorre ao iniciar o SQL Server em um computador extremamente pequeno (bem menor que os requisitos mínimos do sistema).  
  
  
