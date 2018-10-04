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
ms.openlocfilehash: c03a181ee815af7b84a5019719c1ff7b532a0198
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48169246"
---
# <a name="mssqlserver17128"></a>MSSQLSERVER_17128
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|17128|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|INIT_NOBUFSPACE|  
|Texto da mensagem|initdata: Nenhuma memória para buffers de kernel.|  
  
## <a name="explanation"></a>Explicação  
 Ocorreu uma falha nas alocações ou reservas de memória iniciais do pool de buffers e o SQL Server foi encerrado.  
  
## <a name="user-action"></a>Ação do usuário  
 Isso geralmente ocorre ao iniciar o SQL Server em um computador extremamente pequeno – bem menor que os requisitos mínimos de sistema.  
  
  
