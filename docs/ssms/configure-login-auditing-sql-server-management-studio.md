---
title: Configurar auditoria de logon (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- auditing [SQL Server]
- audits [SQL Server], logins
- logins [SQL Server], auditing
ms.assetid: 16961116-57ac-4eef-8037-791b26ade548
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 341344db9bd0e33d044ab9746bc89c8a7d648837
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2018
ms.locfileid: "42776304"
---
# <a name="configure-login-auditing-sql-server-management-studio"></a>Configurar auditoria de logon (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Este tópico descreve como configurar a auditoria de logon no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] para monitorar atividade de logon do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion_md.md)]. A auditoria de logon pode ser configurada de modo a gravar registros no log de erros ao ocorrerem os eventos abaixo.  
  
-   Logons com falha  
  
-   Logons com êxito  
  
-   Logons com falha e bem sucedidos  
  
Você deve reinicializar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para que esta opção entre em vigor.  
  
## <a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-configure-login-auditing"></a>Para configurar a auditoria de logon  
  
1.  No [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion_md.md)] com o Pesquisador de Objetos.  
  
2.  No Pesquisador de Objetos, clique com o botão direito do mouse no nome do servidor e clique em **Propriedades**.  
  
3.  Na página **Segurança** , em auditoria de **Logon** , clique na opção desejada e feche a página **Propriedades do Servidor** .  
  
4.  No Pesquisador de Objetos, clique com o botão direito do mouse no nome do servidor e clique em **Reiniciar**.  
  
