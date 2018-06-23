---
title: Pré-requisitos do Supervisor de atualização | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- installing Upgrade Advisor
- requirements [Upgrade Advisor]
- software [Upgrade Advisor]
- system requirements [Upgrade Advisor]
- Setup [Upgrade Advisor]
- SQL Server Upgrade Advisor, prerequisites
- prerequisites [Upgrade Advisor]
- Upgrade Advisor [SQL Server], prerequisites
ms.assetid: d21a39e5-5f81-4096-a7dd-f244e4779992
caps.latest.revision: 60
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7fb8f505610607052c12c68e910185a2a5e48f16
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118037"
---
# <a name="upgrade-advisor-prerequisites"></a>Pré-requisitos do Supervisor de Atualização
  Este tópico descreve os requisitos de software do Supervisor de Atualização.  
  
## <a name="prerequisites"></a>Prerequisites  
 Os pré-requisitos para instalar e executar o Supervisor de Atualização são os seguintes:  
  
-   [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] SP1, [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] a partir do SP2, Windows 7 ou [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] R2.  
  
-   Windows Installer 4.5. Você pode instalar o Windows Installer a partir de [site do Windows Installer](http://go.microsoft.com/fwlink/?LinkId=49112).  
  
-   O [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], a partir do .NET Framework 4. O [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] está disponível na [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mídia do produto e o [site de download de SDKS, redistribuíveis e service pack](http://go.microsoft.com/fwlink/?LinkId=48882).  
  
    -   Para instalar o .NET Framework 4 a partir da mídia do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], localize a raiz da unidade de disco. Clique duas vezes nas pastas \redist e DotNetFrameworks, e execute o dotNetFx40_Full_x86_x64.exe (para sistemas operacionais de 32 e 64 bits).  
  
-   O [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] ScriptDom é um pré-requisito para instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Supervisor de atualização e não é instalado pela instalação do Supervisor de atualização. A instalação exige que você baixe e instale o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] ScriptDom a partir de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Feature Pack.  
  
## <a name="see-also"></a>Consulte também  
 [Como: instalar o Supervisor de atualização](../../../2014/sql-server/install/how-to-install-upgrade-advisor.md)  
  
  