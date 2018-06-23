---
title: MSSQLSERVER_3151 | Microsoft Docs
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
- 3151 (Database Engine error)
ms.assetid: a8657a91-ec75-4649-a09a-21920e0030ff
caps.latest.revision: 17
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: f5154e3ebc243c102ae49204696316cae2d6d988
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130975"
---
# <a name="mssqlserver3151"></a>MSSQLSERVER_3151
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|3151|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|LDDB_MASTER_LOAD_FAILED|  
|Texto da mensagem|Falha ao restaurar o banco de dados mestre. Desligando o SQL Server. Verifique os logs de erros e recrie o banco de dados mestre. Para obter mais informações sobre como recriar o banco de dados mestre, consulte os Manuais Online do SQL Server.|  
  
## <a name="explanation"></a>Explicação  
 Essa é uma mensagem de erro geral que indica vários problemas com o banco de dados **mestre**.  
  
## <a name="user-action"></a>Ação do usuário  
 Verifique os logs de erros para obter mais informações. Para criar um banco de dados **mestre** utilizável, execute Setup.exe com a opção REBUILDDATABASE. Para obter mais informações, consulte “Como instalar o SQL Server a partir do prompt de comando” nos Manuais Online do SQL Server.  
  
  