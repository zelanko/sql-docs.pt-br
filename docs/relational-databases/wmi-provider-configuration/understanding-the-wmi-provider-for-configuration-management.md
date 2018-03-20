---
title: "Noções básicas sobre o provedor WMI para gerenciamento de configuração | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- WMI Provider for Configuration Management, operations supported
ms.assetid: 92323972-7943-4208-bbf4-050774fb6027
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e31118f5df632d79ae5d1d098032ed2d1bcc33e4
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2018
---
# <a name="understanding-the-wmi-provider-for-configuration-management"></a>Compreendendo o provedor WMI para gerenciamento de configuração
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece o provedor WMI para gerenciamento de configuração. Isto permite que você use a WMI (Instrumentação de Gerenciamento do Windows) para gerenciar serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], configurações de rede de cliente e servidor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e aliases de servidor. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviços, configurações de rede e os aliases são representados por objetos de WMI no root\Microsoft\SqlServer\ComputerManagement*nn* espaço para nome do computador. Depois que uma conexão for estabelecida com o provedor WMI no computador especificado, os serviços, as configurações de rede e os aliases poderão ser consultados usando WQL ou uma linguagem de script.  
  
 O Provedor WMI é um provedor de instância. Ele fornece instâncias do [Classes WMI](../../relational-databases/wmi-provider-configuration-classes/wmi-provider-for-configuration-management-classes.md) e suporta as seguintes operações assíncronas.  
  
 Recuperação de instância  
 Recuperação de uma instância de tipo de classe específica.  
  
 Enumeração  
 Enumeração de todas as instâncias de um tipo de classe.  
  
 Modification  
 Modificação de uma instância específica de um tipo de classe.  
  
 As classes têm métodos que permitem a modificação de suas propriedades.  
  
 Exclusão  
 Remoção de uma instância específica de um tipo de classe.  
  
 Processamento de consulta  
 Enumeração de instâncias de um tipo de classe baseado em um filtro.  
  
 Para obter exemplos de aplicativo de gerenciamento usando o provedor WMI para gerenciamento de configuração, consulte [usando o WQL e linguagens de script com o provedor WMI para gerenciamento de configuração](../../relational-databases/wmi-provider-configuration/using-wql-and-scripting-languages-with-the-wmi-provider.md).  
  
 Para obter mais informações sobre como programar aplicativos de gerenciamento usando o provedor WMI, consulte a documentação do WMI no [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework SDK.  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhando com o provedor WMI para gerenciamento de configuração](../../relational-databases/wmi-provider-configuration/working-with-the-wmi-provider-for-configuration-management.md)   
 [Usando o WQL e linguagens com o provedor WMI para gerenciamento de configuração de scripts](../../relational-databases/wmi-provider-configuration/using-wql-and-scripting-languages-with-the-wmi-provider.md)  
  
  
