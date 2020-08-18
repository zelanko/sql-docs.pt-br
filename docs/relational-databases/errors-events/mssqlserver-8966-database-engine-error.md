---
description: MSSQLSERVER_8966
title: MSSQLSERVER_8966 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8966 (Database Engine error)
ms.assetid: 6b1150fd-9dfd-4df9-8f08-8eca237667db
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0359c734fae801d7f1c2dded751043f8d1ae5d1f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88331482"
---
# <a name="mssqlserver_8966"></a>MSSQLSERVER_8966
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|8966|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC3_FAILED_TO_READ_AND_LATCH_PAGE|  
|Texto da mensagem|Não foi possível ler e travar a página P_ID com o tipo de trava TYPE. Falha em OPERATION.|  
  
## <a name="explanation"></a>Explicação  
Houve uma falha na leitura da página ou não foi possível usar uma trava em uma página PFS ou GAM. Pode haver um tempo limite de trava ou outras mensagens acompanhantes no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="user-action"></a>Ação do usuário  
Procure essas mensagens no log de erros SQL e corrija os erros.  
  
