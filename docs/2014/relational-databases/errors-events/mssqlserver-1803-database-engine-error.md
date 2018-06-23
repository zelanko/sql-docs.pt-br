---
title: MSSQLSERVER_1803 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 1803 (Database Engine error)
ms.assetid: d4315390-82f1-4c4c-8d1b-1a4989537cca
caps.latest.revision: 17
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: ae92ac236ad8d2d5aaa97234a7624aab11e01331
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36011405"
---
# <a name="mssqlserver1803"></a>MSSQLSERVER_1803
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|1803|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|NO_SPACE|  
|Texto da mensagem|Falha em CREATE DATABASE. O arquivo primário deve ter pelo menos %d MB para acomodar uma cópia do modelo de banco de dados.|  
  
## <a name="explanation"></a>Explicação  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria um banco de dados fazendo uma cópia do banco de dados modelo. Em seguida, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] renomeia a cópia e aumenta o novo banco de dados para o tamanho solicitado. Nesse caso, o usuário tentou criar um banco de dados menor que o banco de dados modelo. A operação falhou porque a cópia do banco de dados modelo não caberia no arquivo de dados principal, já que o arquivo era menor que o banco de dados modelo.  
  
## <a name="user-action"></a>Ação do usuário  
 Crie o banco de dados usando um tamanho de arquivo de banco de dados maior. Em seguida, reduza o banco de dados se desejar usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou a instrução DBCC SHRINKDATABASE.  
  
  