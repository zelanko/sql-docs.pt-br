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
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38057844"
---
# <a name="client-libraries-data-providers-used-for-analysis-services-connections"></a>Bibliotecas de cliente (provedores de dados) usadas para conexões do Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

O Analysis Services fornece três bibliotecas de cliente, também conhecido como **provedores de dados**, para acesso a dados de ferramentas e aplicativos cliente e servidor. Ferramentas como o SSMS e SSDT e aplicativos, como o Power BI Desktop e Excel se conectar ao Analysis Services usando essas bibliotecas. Duas das bibliotecas de cliente, o ADOMD.NET e o gerenciamento de objetos AMO (Analysis Services), são bibliotecas de cliente gerenciado. O provedor OLE DB do Analysis Services (MSOLAP DLL) é uma biblioteca de cliente nativo. Bibliotecas de cliente são as mesmas para o SQL Server Analysis Services e o Azure Analysis Services.
  
##  <a name="bkmk_downloadsite"></a> Onde obter as versões mais recentes  
 A versão instalada em um computador cliente deve corresponder à versão principal do servidor que fornece os dados. Se a instalação do servidor for mais recente do que a instalação dos provedores de dados existentes nas estações de trabalho da sua rede, talvez você precise instalar bibliotecas mais recentes.  

Bibliotecas de cliente incluídas em pacotes de recursos do SQL Server anteriores correspondem a essa versão do SQL; No entanto, eles não podem ser a versão mais recente. Conectar-se ao Azure Analysis Services pode exigir versões posteriores. Todas as versões são compatíveis com versões anteriores.

Para obter a versão mais recente, consulte [bibliotecas de cliente para conectar-se ao Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-data-providers). 
  
## <a name="see-also"></a>Confira também  
 [Conectar ao Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)  
  
  
