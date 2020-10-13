---
title: Solucionar problemas de integridade de recursos do SQL Server (Utilitário do SQL Server) | Microsoft Docs
description: Saiba como solucionar problemas de integridade de recursos que um SQL Server UCP identifica, como CPU com utilização excessiva, espaço de arquivo ou espaço em disco alocado.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 614f07b5-f221-4013-9f8d-22964cf42270
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c6c6d499d485941d490848b68b5c8142edd0cb4b
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810671"
---
# <a name="troubleshoot-sql-server-resource-health-sql-server-utility"></a>Solucionar problemas de integridade de recursos do SQL Server (Utilitário do SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Solucionar problemas de integridade de recursos identificados por uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP pode incluir a eliminação de uma CPU sobrecarregada em um computador ou em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ou a eliminação uma CPU sobrecarregada para um aplicativo da camada de dados. Outros problemas incluem a resolução de espaço de arquivo superutilizado para arquivos de banco de dados ou a resolução de superutilização de espaço em disco alocado em um volume de armazenamento.  
  
 Note que, se um banco de dados estiver no estado de "emergência", o estado de integridade exibirá o espaço de arquivo de log superutilizado.  
  
 Para obter mais informações sobre a coleta de dados com falha que resulta em ícones de status cinza na exibição de lista da instância gerenciada em um UCP, veja [Recursos e tarefas do Utilitário do SQL Server](/previous-versions/sql/sql-server-2016/ee210592(v=sql.130)). Para obter mais informações sobre como começar a usar o Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , veja [Recursos e tarefas do Utilitário do SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  
  
 Para obter mais informações sobre como eliminar problemas de integridade de recursos específicos identificados por um UCP do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte os seguintes tópicos:  
  
-   [Como identificar sua versão de SQL Server e edição](https://go.microsoft.com/fwlink/?LinkID=178504)  
  
-   [Solucionando problemas de desempenho no SQL Server 2008](/previous-versions/sql/sql-server-2008/dd672789(v=sql.100))  
  
