---
title: Provedor WMI para gerenciamento de configuração
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- WMI Provider for Configuration Management, operations supported
ms.assetid: 92323972-7943-4208-bbf4-050774fb6027
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 21ca5f7039b11b30c11a0fb707f6b6e89244bae2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73658914"
---
# <a name="understanding-the-wmi-provider-for-configuration-management"></a>Compreendendo o provedor WMI para gerenciamento de configuração
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece o provedor WMI para o gerenciamento de configuração. Isto permite que você use a WMI (Instrumentação de Gerenciamento do Windows) para gerenciar serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], configurações de rede de cliente e servidor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e aliases de servidor. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]os serviços, as configurações de rede e os aliases são representados por objetos WMI no namespace root\Microsoft\SqlServer\ComputerManagement*NN* do computador. Depois que uma conexão for estabelecida com o provedor WMI no computador especificado, os serviços, as configurações de rede e os aliases poderão ser consultados usando WQL ou uma linguagem de script.  
  
 O Provedor WMI é um provedor de instância. Ele fornece instâncias das [classes WMI](../../relational-databases/wmi-provider-configuration-classes/wmi-provider-for-configuration-management-classes.md) e oferece suporte às operações assíncronas a seguir.  
  
 Recuperação de instância  
 Recuperação de uma instância de tipo de classe específica.  
  
 Enumeração  
 Enumeração de todas as instâncias de um tipo de classe.  
  
 Modificação  
 Modificação de uma instância específica de um tipo de classe.  
  
 As classes têm métodos que permitem a modificação de suas propriedades.  
  
 Exclusão  
 Remoção de uma instância específica de um tipo de classe.  
  
 Processamento de consulta  
 Enumeração de instâncias de um tipo de classe baseado em um filtro.  
  
 Para obter exemplos de aplicativo de gerenciamento usando o provedor WMI para gerenciamento de configuração, consulte [usando WQL e linguagens de script com o provedor WMI para gerenciamento de configuração](../../relational-databases/wmi-provider-configuration/using-wql-and-scripting-languages-with-the-wmi-provider.md).  
  
 Para obter mais informações sobre como programar aplicativos de gerenciamento usando o provedor WMI, consulte a [!INCLUDE[msCoName](../../includes/msconame-md.md)] documentação do WMI no SDK do .NET Framework.  
  
## <a name="see-also"></a>Consulte Também  
 [Trabalhando com o provedor WMI para gerenciamento de configuração](../../relational-databases/wmi-provider-configuration/working-with-the-wmi-provider-for-configuration-management.md)   
 [Usando as linguagens WQL e de scripts com o provedor WMI para gerenciamento de configuração](../../relational-databases/wmi-provider-configuration/using-wql-and-scripting-languages-with-the-wmi-provider.md)  
  
  
