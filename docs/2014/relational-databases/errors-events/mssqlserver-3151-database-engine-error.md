---
title: MSSQLSERVER_3151 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3151 (Database Engine error)
ms.assetid: a8657a91-ec75-4649-a09a-21920e0030ff
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c34414754ea9d25ad89f6aba767197eb1dfc10d0
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85033919"
---
# <a name="mssqlserver_3151"></a>MSSQLSERVER_3151
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|3151|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|LDDB_MASTER_LOAD_FAILED|  
|Texto da mensagem|Falha ao restaurar o banco de dados mestre. Desligando o SQL Server. Verifique os logs de erros e recrie o banco de dados mestre. Para obter mais informações sobre como recriar o banco de dados mestre, consulte os Manuais Online do SQL Server.|  
  
## <a name="explanation"></a>Explicação  
 Essa é uma mensagem de erro geral que indica vários problemas com o banco de dados **mestre**.  
  
## <a name="user-action"></a>Ação do usuário  
 Verifique os logs de erros para obter mais informações. Para criar um banco de dados **mestre** utilizável, execute Setup.exe com a opção REBUILDDATABASE. Para obter mais informações, consulte “Como instalar o SQL Server a partir do prompt de comando” nos Manuais Online do SQL Server.  
  
  
