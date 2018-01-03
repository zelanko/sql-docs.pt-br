---
title: "Propriedades do SQL Server Agent (página Sistema de Trabalho) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.ag.agent.job.f1
ms.assetid: e171d13e-1302-4f0e-88be-67d656aec8d3
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ddaf9fe88289bb05c312539fdd60f83d55e0ca8b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="sql-server-agent-properties-job-system-page"></a>Propriedades do SQL Server Agent (página Sistema de Trabalho)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Use esta página para exibir e modificar o modo como o serviço do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent gerencia trabalhos.  
  
## <a name="options"></a>Opções  
**Intervalo de tempo limite de desligamento (em segundos)**  
Especifica o número de segundos que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent espera os trabalhos serem concluídos antes de desligar. Se o trabalho ainda estiver em execução depois do intervalo especificado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent para o trabalho à força.  
  
**Usar uma conta proxy não administrador**  
Define uma conta proxy não administrador para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent. [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)] e as versões posteriores dão suporte a vários proxies; portanto, essa opção será aplicável somente ao gerenciar versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent anteriores ao [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)].  
  
**User name**  
Digite o nome do usuário para a conta proxy não administrador. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] dá suporte a vários proxies; portanto, essa opção será aplicável somente ao gerenciar versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent anteriores ao [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)].  
  
**Senha**  
Digite a senha do usuário para a conta proxy não administrador. [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] e as versões posteriores dão suporte a vários proxies; portanto, essa opção será aplicável somente ao gerenciar versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent anteriores ao [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)].  
  
**Domínio**  
Digite o domínio do usuário para a conta proxy não administrador. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] dá suporte a vários proxies; portanto, essa opção será aplicável somente ao gerenciar versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent anteriores ao [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)].  
  
## <a name="see-also"></a>Consulte Também  
[Implementar trabalhos](../../ssms/agent/implement-jobs.md)  
  
