---
title: MSSQLSERVER_3151 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3151 (Database Engine error)
ms.assetid: a8657a91-ec75-4649-a09a-21920e0030ff
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 068f4737a3367acdd01862cc800a4255a472c843
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68001911"
---
# <a name="mssqlserver_3151"></a>MSSQLSERVER_3151
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
