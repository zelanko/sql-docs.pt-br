---
title: Usar o WQL para acessar o provedor WMI
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Configuration Management, WQL
ms.assetid: 26499530-d93b-452b-bbe4-217ef1d11e68
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 53ade765b0f6b6710a12da06ae0b7470b55d9400
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73658947"
---
# <a name="access-wmi-provider-for-configuration-management-using-wql"></a>Acessar o provedor WMI para o gerenciamento de configuração usando o WQL
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Esta seção descreve como executar instruções de linguagem WQL da Instrumentação de Gerenciamento do Windows [!INCLUDE[msCoName](../../includes/msconame-md.md)] no Provedor de WMI para Gerenciamento do Computador.  
  
 O exemplo usa um editor de WQL, WBEMtest.exe, para executar consultas WQL no Provedor de WMI para enumerar serviços, protocolos de rede e aliases do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="querying-services-using-wbemtest"></a>Consultando serviços que usam WBEMtest  
  
1.  No menu **Iniciar** , clique em **executar**e, em seguida, digite **WBEMTest**.  
  
2.  A caixa de diálogo de WBEMtest.exe é exibida. Clique em **Conectar**.  
  
3.  No primeiro campo de texto, digite o namespace do Provedor de WMI para Gerenciamento do Computador: root\Microsoft\SqlServer\ComputerManagement11. Clique em **Conectar**.  
  
4.  Clique em **Consulta**. Digite uma consulta que retorne os serviços atuais em execução no computador local **: \* selecione em SqlService.** Clique em **Aplicar**.  
  
5.  Refine ainda mais a consulta adicionando **Where ServiceName = "MSSQLSERVER"**.  
  
  
