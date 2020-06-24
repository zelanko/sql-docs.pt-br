---
title: Acessar o provedor WMI com WQL e scripts
description: Saiba como acessar os serviços SQL Server e as configurações de rede usando o provedor WMI usando um editor WQL ou ferramenta de consulta ou uma linguagem de script.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- queries [WMI]
- scripts [WMI]
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Configuration Management, WQL
- WMI Provider for Configuration Management, scripts
ms.assetid: c1e64905-3c2b-4974-88f4-abf17cf7e289
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: db39dfd29532f2a0fd2d61ce4a987e0aada7d6c5
ms.sourcegitcommit: bf5e9cb3a2caa25d0a37f401b3806b7baa5adea8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85295399"
---
# <a name="using-wql-and-scripting-languages-with-the-wmi-provider"></a>Usar as linguagens WQL e de scripts com o provedor WMI
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Os aplicativos de gerenciamento acessam os serviços e configurações de rede do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Provedor WMI (Instrumentação de Gerenciamento do Windows) para objetos de Gerenciamento de Configuração de duas maneiras:  
  
-   Usando um editor de WQL ou ferramenta de consulta, como o WBEMTest.exe para consultar o objeto definido com WQL (Linguagem de Instrumentação de Gerenciamento do Windows).  
  
-   Usando uma linguagem de scripts, como o VBScript.  
  
 Como alternativa, os serviços e configurações de rede do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem ser gerenciados via programação usando objetos gerenciados WMI no SMO. Para obter mais informações sobre como programar objetos gerenciados por WMI, consulte [Gerenciando serviços e configurações de rede usando o provedor WMI](../../relational-databases/server-management-objects-smo/tasks/managing-services-and-network-settings-by-using-wmi-provider.md).  
  
 O Provedor WMI para Gerenciamento de Configuração pode ser acessado usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager e o Console de Gerenciamento [!INCLUDE[msCoName](../../includes/msconame-md.md)]. Para obter mais informações sobre como acessar o provedor WMI de uma interface do usuário, consulte [Tópicos de instruções sobre como gerenciar serviços &#40;SQL Server Configuration Manager&#41;](https://msdn.microsoft.com/library/78dee169-df0c-4c95-9af7-bf033bc9fdc6).  
  
## <a name="see-also"></a>Consulte Também  
 [Acessar o provedor WMI para gerenciamento de configuração usando WQL](../../relational-databases/wmi-provider-configuration/access-wmi-provider-for-configuration-management-using-wql.md)   
 [Acessar o provedor WMI com VBScript](../../relational-databases/wmi-provider-configuration/access-wmi-provider-for-configuration-management-using-vbscript.md)  
  
  
