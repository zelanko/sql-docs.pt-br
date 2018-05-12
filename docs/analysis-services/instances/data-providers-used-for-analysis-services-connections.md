---
title: Provedores de dados usados para conexões do Analysis Services | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f5ba97f90b877896d68cd62598f11d0845fb698e
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="client-libraries-data-providers-used-for-analysis-services-connections"></a>Bibliotecas de cliente (provedores de dados) usadas para conexões do Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

O Analysis Services fornece três bibliotecas de cliente, também conhecido como **provedores de dados**, para acesso a dados de ferramentas e aplicativos cliente e servidor. Ferramentas como o SSMS SSDT e aplicativos que o Power BI Desktop e Excel se conectar ao Analysis Services usando essas bibliotecas. Duas das bibliotecas de cliente ADOMD.NET e o Analysis Services Management Objects (AMO) são bibliotecas de cliente gerenciado. O provedor OLE DB do Analysis Services (MSOLAP DLL) é uma biblioteca do native client. Bibliotecas de cliente são os mesmos para o SQL Server Analysis Services e o Azure Analysis Services.
  
##  <a name="bkmk_downloadsite"></a> Onde obter versões mais recentes  
 A versão instalada em um computador cliente deve corresponder à versão principal do servidor que fornece os dados. Se a instalação do servidor for mais recente do que a instalação dos provedores de dados existentes nas estações de trabalho da sua rede, talvez você precise instalar bibliotecas mais recentes.  

Bibliotecas de cliente incluídas em pacotes de recursos do SQL Server anteriores correspondem a essa versão do SQL; No entanto, eles não podem ter a versão mais recente. Conectar-se ao Azure Analysis Services pode exigir versões posteriores. Todas as versões são compatíveis com versões anteriores.

Para obter a versão mais recente, consulte [bibliotecas de cliente para se conectar ao Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-data-providers). 
  
## <a name="see-also"></a>Consulte também  
 [Conectar ao Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)  
  
  
