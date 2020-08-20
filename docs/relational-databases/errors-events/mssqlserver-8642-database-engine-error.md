---
description: MSSQLSERVER_8642
title: MSSQLSERVER_8642 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8642 (Database Engine error)
ms.assetid: fc498059-202f-4d0b-8599-4e784b47c186
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7ab7d742d6af4b9f2ae29e8cb9cffe645a1d7f49
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460871"
---
# <a name="mssqlserver_8642"></a>MSSQLSERVER_8642
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|8642|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|EXCHNGSTART_ERR|  
|Texto da mensagem|O processador de consultas não pôde iniciar os recursos de threads necessários para execução paralela da consulta.|  
  
## <a name="explanation"></a>Explicação  
O servidor não dispõe de recursos de thread suficientes.  
  
## <a name="user-action"></a>Ação do usuário  
Reduza a carga no servidor e execute a consulta novamente.  
  
