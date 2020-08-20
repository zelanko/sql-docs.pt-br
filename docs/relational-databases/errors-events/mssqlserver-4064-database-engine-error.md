---
description: MSSQLSERVER_4064
title: MSSQLSERVER_4064 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 4064 (Database Engine error)
ms.assetid: 32112b90-0a2f-4834-a027-756811732be7
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 27f5ccbad0bd1722f8c9a4fbe1d2b7cd0fd633da
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471073"
---
# <a name="mssqlserver_4064"></a>MSSQLSERVER_4064
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|4064|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DB_UFAIL_FATAL|  
|Texto da mensagem|Não é possível abrir o banco de dados padrão do usuário. Falha no logon.|  
  
## <a name="explanation"></a>Explicação  
O logon do SQL Server não pôde se conectar devido a um problema com o banco de dados padrão. O próprio banco de dados é inválido ou o logon não tem a permissão CONNECT no banco de dados.  
  
## <a name="user-action"></a>Ação do usuário  
Use ALTER LOGIN para alterar o banco de dados padrão do logon. Conceda a permissão CONNECT para o logon.  
  
