---
title: Exibir o log de erros do SQL Server (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 09/29/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- viewing logs
- displaying logs
- errors [SQL Server], logs
- logs [SQL Server], SQL Server error logs
- logs [SQL Server], viewing
ms.assetid: 55f468ba-146c-4ab3-95cd-d35d051afd12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a4bbe988a6c63cb3f0acd5b5275df811335586b1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47845354"
---
# <a name="view-the-sql-server-error-log-sql-server-management-studio"></a>Exibir o log de erros do SQL Server (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
O log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contém eventos definidos pelo usuário e alguns eventos do sistema que podem ser usados para solução de problemas. 

## <a name="view-the-logs"></a>Exibir os logs

1. No SQL Server Management Studio, selecione **Pesquisador de Objetos**. Para abrir o **Pesquisador de Objetos**, selecione F8. Se preferir, no menu superior, selecione **Exibir** e selecione **Pesquisador de Objetos**:
    
    ![Object_Explorer](../../relational-databases/performance/media/object-explorer.png) 

2. No **Pesquisador de Objetos**, conecte-se a uma instância do SQL Server e expanda-a.
  
3. Encontre e expanda a seção **Gerenciamento** (supondo que você tenha permissões para vê-la).

4. Clique com o botão direito do mouse em **Logs do SQL Server**, selecione **Exibir** e escolha **Log do SQL Server**.

    ![View_SQLServer_Log_SSMS](../../relational-databases/performance/media/view-sqlserver-log-ssms.png) 
 
5. O **Visualizador do Arquivo de Log** será exibido (pode levar um minuto) com uma lista de logs a serem exibidos.
  
  ## <a name="see-also"></a>Confira também
  Para obter mais informações, consulte a postagem útil [Identify location of the SQL Server Error Log file](https://www.mssqltips.com/sqlservertip/2506/identify-location-of-the-sql-server-error-log-file/) (Identificar o local do arquivo de log de erro do SQL Server) de [MSSQLTips.com](https://www.mssqltips.com/).

