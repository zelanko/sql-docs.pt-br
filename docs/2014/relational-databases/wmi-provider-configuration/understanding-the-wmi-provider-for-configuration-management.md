---
title: Noções básicas sobre o provedor WMI para gerenciamento de configuração | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- WMI Provider for Configuration Management, operations supported
ms.assetid: 92323972-7943-4208-bbf4-050774fb6027
caps.latest.revision: 20
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: d4917968888760b0910629338eb435df41769efc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37222916"
---
# <a name="understanding-the-wmi-provider-for-configuration-management"></a>Compreendendo o provedor WMI para gerenciamento de configuração
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece o provedor WMI para gerenciamento de configuração. Isto permite que você use a WMI (Instrumentação de Gerenciamento do Windows) para gerenciar serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], configurações de rede de cliente e servidor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e aliases de servidor. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] os serviços, as configurações de rede e os aliases são representados por objetos de WMI no root\Microsoft\SqlServer\ComputerManagement*nn* espaço para nome do computador. Depois que uma conexão for estabelecida com o provedor WMI no computador especificado, os serviços, as configurações de rede e os aliases poderão ser consultados usando WQL ou uma linguagem de script.  
  
 O Provedor WMI é um provedor de instância. Ele fornece instâncias da [Classes WMI](../wmi-provider-configuration-classes/wmi-provider-for-configuration-management-classes.md) e suporta as seguintes operações assíncronas.  
  
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
  
 Para obter exemplos de aplicativo de gerenciamento usando o provedor WMI para gerenciamento de configuração, consulte [usando o WQL e linguagens de script com o provedor WMI para gerenciamento de configuração](using-wql-and-scripting-languages-with-the-wmi-provider.md).  
  
 Para obter mais informações sobre como programar aplicativos de gerenciamento usando o provedor WMI, consulte a documentação do WMI no [!INCLUDE[msCoName](../../includes/msconame-md.md)] SDK do .NET Framework.  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhando com o provedor WMI para gerenciamento de configuração](working-with-the-wmi-provider-for-configuration-management.md)   
 [Usando as linguagens WQL e de scripts com o provedor WMI para gerenciamento de configuração](using-wql-and-scripting-languages-with-the-wmi-provider.md)  
  
  
