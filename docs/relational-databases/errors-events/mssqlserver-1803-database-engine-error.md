---
description: MSSQLSERVER_1803
title: MSSQLSERVER_1803 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1803 (Database Engine error)
ms.assetid: d4315390-82f1-4c4c-8d1b-1a4989537cca
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5a1e652d3ccf32a85fc0c1299f54c00a34ea06fb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456336"
---
# <a name="mssqlserver_1803"></a>MSSQLSERVER_1803
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|1803|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|NO_SPACE|  
|Texto da mensagem|Falha em CREATE DATABASE. O arquivo primário deve ter pelo menos %d MB para acomodar uma cópia do modelo de banco de dados.|  
  
## <a name="explanation"></a>Explicação  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria um banco de dados fazendo uma cópia do banco de dados modelo. Em seguida, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] renomeia a cópia e aumenta o novo banco de dados para o tamanho solicitado. Nesse caso, o usuário tentou criar um banco de dados menor que o banco de dados modelo. A operação falhou porque a cópia do banco de dados modelo não caberia no arquivo de dados principal, já que o arquivo era menor que o banco de dados modelo.  
  
## <a name="user-action"></a>Ação do usuário  
Crie o banco de dados usando um tamanho de arquivo de banco de dados maior. Em seguida, reduza o banco de dados se desejar usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou a instrução DBCC SHRINKDATABASE.  
  
