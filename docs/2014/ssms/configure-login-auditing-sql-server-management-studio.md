---
title: Configurar auditoria de logon (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- auditing [SQL Server]
- audits [SQL Server], logins
- logins [SQL Server], auditing
ms.assetid: 16961116-57ac-4eef-8037-791b26ade548
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b1ea23cf8d31b66d8db57e53c08ae09233908f8e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37275662"
---
# <a name="configure-login-auditing-sql-server-management-studio"></a>Configurar auditoria de logon (SQL Server Management Studio)
  Este tópico descreve como configurar a auditoria de logon no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] para monitorar atividade de logon do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]. A auditoria de logon pode ser configurada de modo a gravar registros no log de erros ao ocorrerem os eventos abaixo.  
  
-   Logons com falha  
  
-   Logons com êxito  
  
-   Logons com falha e bem sucedidos  
  
 Você deve reinicializar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para que esta opção entre em vigor.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-configure-login-auditing"></a>Para configurar a auditoria de logon  
  
1.  No [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] com o Pesquisador de Objetos.  
  
2.  No Pesquisador de Objetos, clique com o botão direito do mouse no nome do servidor e clique em **Propriedades**.  
  
3.  Na página **Segurança** , em auditoria de **Logon** , clique na opção desejada e feche a página **Propriedades do Servidor** .  
  
4.  No Pesquisador de Objetos, clique com o botão direito do mouse no nome do servidor e clique em **Reiniciar**.  
  
  
