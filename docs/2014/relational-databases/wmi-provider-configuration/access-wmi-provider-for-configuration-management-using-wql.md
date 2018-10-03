---
title: Acessar o provedor WMI para gerenciamento de configuração usando o WQL | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Configuration Management, WQL
ms.assetid: 26499530-d93b-452b-bbe4-217ef1d11e68
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 0b19bf27cdc94e70908f81523a092ba022c41601
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48157676"
---
# <a name="access-wmi-provider-for-configuration-management-using-wql"></a>Acessar o provedor WMI para o gerenciamento de configuração usando o WQL
  Esta seção descreve como executar instruções de linguagem WQL da Instrumentação de Gerenciamento do Windows [!INCLUDE[msCoName](../../includes/msconame-md.md)] no Provedor de WMI para Gerenciamento do Computador.  
  
 O exemplo usa um editor de WQL, WBEMtest.exe, para executar consultas WQL no Provedor de WMI para enumerar serviços, protocolos de rede e aliases do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="querying-services-using-wbemtest"></a>Consultando serviços que usam WBEMtest  
  
1.  Do **inicie** menu, clique em **execute**e, em seguida, insira `WBEMtest`.  
  
2.  A caixa de diálogo de WBEMtest.exe é exibida. Clique em **Conectar**.  
  
3.  No primeiro campo de texto, digite o namespace do Provedor de WMI para Gerenciamento do Computador: root\Microsoft\SqlServer\ComputerManagement11. Clique em **Conectar**.  
  
4.  Clique em **consulta**. Digite uma consulta que retorna os serviços atuais em execução no computador local: **selecionar \* de SqlService.** Clique em **Aplicar**.  
  
5.  Refine ainda mais a consulta, adicionando `WHERE ServiceName = "MSSQLSERVER"`.  
  
  
