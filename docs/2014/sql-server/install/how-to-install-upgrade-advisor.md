---
title: 'Como: instalar o Supervisor de atualização | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- installing Upgrade Advisor
- Setup [Upgrade Advisor]
- SQL Server Upgrade Advisor, installing
- Upgrade Advisor [SQL Server], installing
ms.assetid: 481b0704-ce79-4543-b141-67306128aa2b
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 69d5be9a4514f002ebd8c9b7ffb05c6f614e2129
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48112917"
---
# <a name="how-to-install-upgrade-advisor"></a>Como instalar o Supervisor de Atualização
  O Supervisor de Atualização dá suporte à análise remota de todos os componentes com suporte, exceto o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Se você não estiver verificando instâncias do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], você pode instalar o Supervisor de Atualização em qualquer computador que pode se conectar às suas instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O computador também deve atender aos pré-requisitos do Supervisor de Atualização. Se você estiver verificando instâncias do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], será necessário instalar o Supervisor de Atualização no servidor de relatório.  
  
 Para obter mais informações, consulte [Installing Upgrade Advisor](../../../2014/sql-server/install/installing-upgrade-advisor.md).  
  
### <a name="to-install-upgrade-advisor"></a>Para instalar o Supervisor de Atualização  
  
1.  Inicie a instalação usando um dos seguintes métodos:  
  
    -   Se você estiver instalando a partir de [!INCLUDE[msCoName](../../includes/msconame-md.md)] site da Web, clique no **baixar** vincular e, em seguida, clique no **executar** botão para iniciar a instalação.  
  
    -   Se você estiver instalando da mídia do produto, abra o **redist** pasta, abra o **Supervisor de atualização** pasta e clique duas vezes em **sqlua. msi**.  
  
    > [!NOTE]  
    >  O Supervisor de Atualização requer o [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 4. Caso ele não esteja instalado ou você tenha uma versão de pré-lançamento, aparecerá uma mensagem de erro. Desinstale qualquer versão anterior do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e depois instale a versão mais recente do .NET Framework 4.  
    >   
    >  O [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] ScriptDom é um pré-requisito para instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Supervisor de atualização e não é instalado pela instalação do Supervisor de atualização. A instalação exige que você baixe e instale o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] ScriptDom no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Feature Pack.  
  
2.  Sobre o **bem-vindo ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] instalação do Supervisor de atualização** , clique em **próximo**.  
  
3.  Sobre o **contrato de licença** página, leia o contrato de licença. Se você concordar, marque **aceito o contrato de licença** e, em seguida, clique em **próxima**.  
  
4.  Sobre o **informações de registro** página, insira seu nome e a empresa.  
  
5.  Sobre o **seleção de recursos** , examine o **caminho de instalação** valor. Se necessário, use o **procurar** botão para alterar o local. Clique em **Avançar**.  
  
6.  Sobre o **pronto para instalar o programa** , clique em **instalar** para instalar o Supervisor de atualização.  
  
7.  Clique em **Concluir** para sair do assistente.  
  
## <a name="see-also"></a>Consulte também  
 [Pré-requisitos do Supervisor de Atualização](../../../2014/sql-server/install/upgrade-advisor-prerequisites.md)  
  
  
