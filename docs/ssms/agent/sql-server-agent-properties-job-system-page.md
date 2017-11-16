---
title: "Propriedades do SQL Server Agent (página Sistema de Trabalho) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
ms.openlocfilehash: ed055e6b7a9c560c0ac05c11f930c49b681de0aa
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="sql-server-agent-properties-job-system-page"></a>Propriedades do SQL Server Agent (página Sistema de Trabalho)
Use esta página para exibir e modificar o modo como o serviço do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent gerencia trabalhos.  
  
## <a name="options"></a>Opções  
**Intervalo de tempo limite de desligamento (em segundos)**  
Especifica o número de segundos que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent espera os trabalhos serem concluídos antes de desligar. Se o trabalho ainda estiver em execução depois do intervalo especificado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent para o trabalho à força.  
  
**Usar uma conta proxy não administrador**  
Define uma conta proxy não administrador para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent. [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)] e as versões posteriores dão suporte a vários proxies; portanto, essa opção será aplicável somente ao gerenciar versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent anteriores ao [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)].  
  
**Nome de usuário**  
Digite o nome do usuário para a conta proxy não administrador. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] dá suporte a vários proxies; portanto, essa opção será aplicável somente ao gerenciar versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent anteriores ao [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)].  
  
**Senha**  
Digite a senha do usuário para a conta proxy não administrador. [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] e as versões posteriores dão suporte a vários proxies; portanto, essa opção será aplicável somente ao gerenciar versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent anteriores ao [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)].  
  
**Domínio**  
Digite o domínio do usuário para a conta proxy não administrador. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] dá suporte a vários proxies; portanto, essa opção será aplicável somente ao gerenciar versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent anteriores ao [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)].  
  
## <a name="see-also"></a>Consulte também  
[Implementar trabalhos](../../ssms/agent/implement-jobs.md)  
  
