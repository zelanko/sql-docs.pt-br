---
title: "Acessar o provedor WMI para gerenciamento de configuração usando o WQL | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Configuration Management, WQL
ms.assetid: 26499530-d93b-452b-bbe4-217ef1d11e68
caps.latest.revision: "16"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2055cb2f38ea35c3ae4123c0bf8f1f8501dcc4e1
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="access-wmi-provider-for-configuration-management-using-wql"></a>Acessar o provedor WMI para o gerenciamento de configuração usando o WQL
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]Esta seção descreve como executar [!INCLUDE[msCoName](../../includes/msconame-md.md)] instruções do Windows Management Instrumentation Query Language (WQL) em relação ao provedor WMI para gerenciamento do computador.  
  
 O exemplo usa um editor de WQL, WBEMtest.exe, para executar consultas WQL no Provedor de WMI para enumerar serviços, protocolos de rede e aliases do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="querying-services-using-wbemtest"></a>Consultando serviços que usam WBEMtest  
  
1.  Do **iniciar** menu, clique em **executar**e, em seguida, digite **WBEMtest**.  
  
2.  A caixa de diálogo de WBEMtest.exe é exibida. Clique em **Conectar**.  
  
3.  No primeiro campo de texto, digite o namespace do Provedor de WMI para Gerenciamento do Computador: root\Microsoft\SqlServer\ComputerManagement11. Clique em **Conectar**.  
  
4.  Clique em **consulta**. Digite uma consulta que retorna os serviços atuais em execução no computador local: **selecionar \* de SqlService.** Clique em **Aplicar**.  
  
5.  Refine a consulta adicionando **onde ServiceName = "MSSQLSERVER"**.  
  
  
