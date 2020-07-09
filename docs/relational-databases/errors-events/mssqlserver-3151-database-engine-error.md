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
ms.openlocfilehash: d0d4c51bd7f4e1eca3bf57fbcfa89aec93357fb0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85723745"
---
# <a name="mssqlserver_3151"></a>MSSQLSERVER_3151
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|3151|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|LDDB_MASTER_LOAD_FAILED|  
|Texto da mensagem|Falha ao restaurar o banco de dados mestre. Desligando o SQL Server. Verifique os logs de erros e recrie o banco de dados mestre. Para obter mais informações sobre como recriar o banco de dados mestre, consulte os Manuais Online do SQL Server.|  
  
## <a name="explanation"></a>Explicação  
Essa é uma mensagem de erro geral que indica vários problemas com o banco de dados **mestre**.  
  
## <a name="user-action"></a>Ação do usuário  
Verifique os logs de erros para obter mais informações. Para criar um banco de dados **mestre** utilizável, execute Setup.exe com a opção REBUILDDATABASE. Para saber mais, consulte "Como: instalar o SQL Server a partir do prompt de comando” nos Manuais Online do SQL Server.  
  
