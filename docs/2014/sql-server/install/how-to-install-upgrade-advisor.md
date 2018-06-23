---
title: 'Como: instalar o Supervisor de atualização | Microsoft Docs'
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
- Setup [Upgrade Advisor]
- SQL Server Upgrade Advisor, installing
- Upgrade Advisor [SQL Server], installing
ms.assetid: 481b0704-ce79-4543-b141-67306128aa2b
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b98a4b134025d22ad9d13ce9fa38a7e4f2605e0b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121413"
---
# <a name="how-to-install-upgrade-advisor"></a>Como instalar o Supervisor de Atualização
  O Supervisor de Atualização dá suporte à análise remota de todos os componentes com suporte, exceto o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Se você não estiver verificando instâncias do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], você pode instalar o Supervisor de Atualização em qualquer computador que pode se conectar às suas instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O computador também deve atender aos pré-requisitos do Supervisor de Atualização. Se você estiver verificando instâncias do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], será necessário instalar o Supervisor de Atualização no servidor de relatório.  
  
 Para obter mais informações, consulte [instalando o Supervisor de atualização](../../../2014/sql-server/install/installing-upgrade-advisor.md).  
  
### <a name="to-install-upgrade-advisor"></a>Para instalar o Supervisor de Atualização  
  
1.  Inicie a instalação usando um dos seguintes métodos:  
  
    -   Se você estiver instalando a partir de [!INCLUDE[msCoName](../../includes/msconame-md.md)] site da Web, clique no **baixar** link e, em seguida, clique no **executar** botão para iniciar a instalação.  
  
    -   Se você estiver instalando da mídia do produto, abra o **redist** pasta, abra o **Supervisor de atualização** pasta e, em seguida, clique duas vezes em **SQLUA.msi**.  
  
    > [!NOTE]  
    >  O Supervisor de Atualização requer o [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 4. Caso ele não esteja instalado ou você tenha uma versão de pré-lançamento, aparecerá uma mensagem de erro. Desinstale qualquer versão anterior do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e depois instale a versão mais recente do .NET Framework 4.  
    >   
    >  O [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] ScriptDom é um pré-requisito para instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Supervisor de atualização e não é instalado pela instalação do Supervisor de atualização. A instalação exige que você baixe e instale o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] ScriptDom a partir de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Feature Pack.  
  
2.  Sobre o **bem-vindo ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] instalação do Supervisor de atualização** , clique em **próximo**.  
  
3.  Sobre o **contrato de licença** página, leia o contrato de licença. Se você concordar, selecione **aceito o contrato de licença** e, em seguida, clique em **próximo**.  
  
4.  Sobre o **informações de registro** , insira seu nome e a empresa.  
  
5.  Sobre o **seleção de recursos** , examine o **caminho de instalação** valor. Se necessário, use o **procurar** botão para alterar o local. Clique em **Avançar**.  
  
6.  Sobre o **pronto para instalar o programa** , clique em **instalar** para instalar o Supervisor de atualização.  
  
7.  Clique em **Concluir** para sair do assistente.  
  
## <a name="see-also"></a>Consulte também  
 [Pré-requisitos do Supervisor de atualização](../../../2014/sql-server/install/upgrade-advisor-prerequisites.md)  
  
  