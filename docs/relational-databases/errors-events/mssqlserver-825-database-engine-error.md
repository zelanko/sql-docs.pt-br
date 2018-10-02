---
title: MSSQLSERVER_825 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 825 (Database Engine error)
ms.assetid: f69f8214-5af1-4769-878b-117ad6eaff52
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c01befe93cc27c545965e3ecdd896dc7f14ca34f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47680384"
---
# <a name="mssqlserver825"></a>MSSQLSERVER_825
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|825|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|B_RETRYWORKED|  
|Texto da mensagem|Uma leitura do arquivo '%ls' no deslocamento %#016I64x teve êxito depois de falhar %d vezes com o erro: %ls. Additional messages in the SQL Server error log and system event log may provide more detail. Essa condição de erro ameaça a integridade do banco de dados e precisa ser corrigida. Faça uma verificação completa da consistência do banco de dados (DBCC CHECKDB). Esse erro pode ter sido causado por vários fatores. Para obter mais informações, consulte os Manuais Online do SQL Server.|  
  
## <a name="explanation"></a>Explicação  
Essa mensagem indica que a operação de leitura precisou ser reemitida pelo menos uma vez e indica um problema importante com o hardware de disco. Essa mensagem não indica um problema atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas o problema de disco pode causar perda de dados ou corrupção no banco de dados se não for resolvido. O log de eventos do sistema pode conter eventos relacionados que ajudem a diagnosticar o problema. Para obter mais informações sobre erros de E/S, consulte [Microsoft SQL Server I/O Basics, Chapter 2](http://go.microsoft.com/fwlink/?LinkId=69370) (Noções básicas de E/S do Microsoft SQL Server, Capítulo 2).  
  
## <a name="user-action"></a>Ação do usuário  
As seguintes ações podem ajudá-lo a identificar e resolver o problema subjacente:  
  
-   Revise o log de erros e o texto variável nesta mensagem para encontrar pistas que expliquem o problema.  
  
-   Verifique seu sistema de disco. O problema pode estar relacionado aos discos, aos controladores de disco, aos cartões de matriz ou aos drivers de disco.  
  
-   Entre em contato com o fabricante do disco para obter os utilitários mais recentes para verificar o status do sistema de disco.  
  
-   Contate o fabricante do disco para obter as mais recentes atualizações de driver.  
  
