---
title: Como instalar o supervisor de atualização | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
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
ms.openlocfilehash: 0de86b9690f0647803938218ce566508662da20e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66094916"
---
# <a name="how-to-install-upgrade-advisor"></a>Como instalar o Supervisor de Atualização
  O Supervisor de Atualização dá suporte à análise remota de todos os componentes com suporte, exceto o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Se você não estiver verificando instâncias do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], você pode instalar o Supervisor de Atualização em qualquer computador que pode se conectar às suas instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O computador também deve atender aos pré-requisitos do Supervisor de Atualização. Se você estiver verificando instâncias do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], será necessário instalar o Supervisor de Atualização no servidor de relatório.  
  
 Para obter mais informações, consulte [instalando o supervisor de atualização](../../../2014/sql-server/install/installing-upgrade-advisor.md).  
  
### <a name="to-install-upgrade-advisor"></a>Para instalar o Supervisor de Atualização  
  
1.  Inicie a instalação usando um dos seguintes métodos:  
  
    -   Se você estiver instalando do [!INCLUDE[msCoName](../../includes/msconame-md.md)] site, clique no link **baixar** e, em seguida, clique no botão **executar** para iniciar a instalação.  
  
    -   Se você estiver instalando a partir da mídia do produto, abra a pasta **Redist** , abra a pasta **supervisor de atualização** e clique duas vezes em **SQLUA. msi**.  
  
    > [!NOTE]  
    >  O Supervisor de Atualização requer o [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 4. Caso ele não esteja instalado ou você tenha uma versão de pré-lançamento, aparecerá uma mensagem de erro. Desinstale qualquer versão anterior do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e depois instale a versão mais recente do .NET Framework 4.  
    >   
    >  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O [!INCLUDE[tsql](../../includes/tsql-md.md)] ScriptDom é um pré-requisito para instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] o supervisor de atualização e não é instalado pela instalação do supervisor de atualização. A instalação exige que você baixe e instale o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] ScriptDom do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Feature Pack.  
  
2.  Na página **Bem-vindo [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] à instalação do supervisor de atualização** , clique em **Avançar**.  
  
3.  Na página **contrato de licença** , leia o contrato de licença. Se você concordar, selecione **aceito o contrato de licença** e clique em **Avançar**.  
  
4.  Na página **informações de registro** , insira seu nome e empresa.  
  
5.  Na página **seleção de recursos** , examine o valor do **caminho de instalação** . Se necessário, use o botão **procurar** para alterar o local. Clique em **Próximo**.  
  
6.  Na página **pronto para instalar o programa** , clique em **instalar** para instalar o supervisor de atualização.  
  
7.  Clique em **Concluir** para sair do assistente.  
  
## <a name="see-also"></a>Consulte Também  
 [Pré-requisitos do Supervisor de Atualização](../../../2014/sql-server/install/upgrade-advisor-prerequisites.md)  
  
  
