---
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
ms.openlocfilehash: ced4c9b3e690b709be9d8f500ff2656cf6b5e220
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727433"
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
  
