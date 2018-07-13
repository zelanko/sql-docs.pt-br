---
title: MSSQLSERVER_3151 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 3151 (Database Engine error)
ms.assetid: a8657a91-ec75-4649-a09a-21920e0030ff
caps.latest.revision: 17
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 16bfbb544023813698e33c0490e7ccb8d08754d3
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37418345"
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
  
  
