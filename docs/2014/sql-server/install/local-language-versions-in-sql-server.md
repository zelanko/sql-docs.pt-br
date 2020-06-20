---
title: Versões de idiomas locais no SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 20b99363-0490-4aa3-9a3d-262f827d81e8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c857b6e77e6fbf4ea7eb4d5e11b72d76708ad86a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85045134"
---
# <a name="local-language-versions-in-sql-server"></a>Versões de idiomas locais no SQL Server
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a todos os idiomas que têm suporte nos sistemas operacionais Windows.  
  
## <a name="cross-language-support"></a>Suporte entre idiomas  
  
-   Há suporte à versão no idioma inglês do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em todas as versões localizadas de sistemas operacionais.  
  
-   Também é dado suporte às versões localizadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em sistemas operacionais localizados com o idioma correspondente ou em versões em inglês de sistemas operacionais com suporte, usando as configurações do Windows MUI (Multilingual User Interface Pack). Para obter mais informações, consulte [Configure Operating System to Support Localized Versions](../../../2014/sql-server/install/local-language-versions-in-sql-server.md#BK_ConfigureOS).  
  
-   As versões localizadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] somente podem ser atualizadas para versões localizadas do mesmo idioma e não podem ser atualizadas para a versão em inglês.  
  
-   As versões localizadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também podem ser instaladas lado a lado com instâncias em inglês do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
##  <a name="configure-operating-system-to-support-localized-versions"></a><a name="BK_ConfigureOS"></a> Configure Operating System to Support Localized Versions  
 As versões localizadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] têm suporte em versões no idioma inglês de sistemas operacionais com suporte; isso ocorre com o uso de configurações MUI Pack (Multilingual User Interface Pack) do Windows.  
  
 Entretanto, você deve verificar determinadas configurações do sistema operacional antes de instalar uma versão localizada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um servidor que esteja executando um sistema operacional no idioma inglês com uma configuração de MUI não inglês. Você precisa verificar se as seguintes configurações do sistema operacional correspondem ao idioma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] localizado a ser instalado:  
  
-   A configuração de interface do usuário do sistema operacional  
  
-   A configuração de localidade do usuário do sistema operacional  
  
-   A configuração de localidade do sistema  
  
 Se as configurações não corresponderem ao idioma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] localizado a ser instalado, use os procedimentos a seguir para definir corretamente essas configurações do sistema operacional.  
  
> [!CAUTION]  
>  Não há suporte para instalações de versões de idioma diferentes de instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no mesmo computador.  
  
#### <a name="to-change-the-operating-system-user-interface-setting"></a>Para alterar a configuração da interface do usuário do sistema operacional  
  
1.  Se ainda não estiver instalado, instale o MUI do sistema operacional que corresponde à sua versão localizada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  No Painel de Controle, abra **Opções Regionais e de Idioma**.  
  
3.  Na guia **Idiomas** , para **Idioma usado em menus e caixas de diálogo**, selecione um valor da lista.  
  
     Essa configuração afetará o idioma da interface do usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], portanto deve corresponder à sua versão localizada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
4.  Clique em **Aplicar** para confirmar a alteração e em **OK** para fechar a janela.  
  
#### <a name="to-change-the-operating-system-user-locale-setting"></a>Para alterar a configuração da localidade do usuário do sistema operacional  
  
1.  Se ainda não estiver instalado, instale o MUI do sistema operacional que corresponde à sua versão localizada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  No Painel de Controle, abra **Opções Regionais e de Idioma**.  
  
3.  Na guia **Opções Regionais** , para **Selecione um item correspondente às suas preferências**, selecione um valor da lista.  
  
     Essa configuração afetará a formatação de dados específicos da cultura.  
  
4.  Clique em **Aplicar** para confirmar a alteração e em **OK** para fechar a janela.  
  
#### <a name="to-change-the-system-locale-setting"></a>Par alterar a configuração de localidade do sistema  
  
1.  Se ainda não estiver instalado, instale o MUI do sistema operacional que corresponde à sua versão localizada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  No Painel de Controle, abra **Opções Regionais e de Idioma**.  
  
3.  Na guia **Avançado** , para **Select a language to match the language version of the non-Unicode programs you want to use (Selecione um idioma correspondente à versão de idioma dos programas não Unicode que você deseja usar)** , selecione um valor da lista.  
  
     Essa configuração permitirá que a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escolha a melhor ordenação padrão para sua instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
4.  Clique em **Aplicar** para confirmar a alteração e em **OK** para fechar a janela.  
  
## <a name="see-also"></a>Consulte Também  
 [Requisitos de hardware e software para a instalação do SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md)   
 [Instalar o SQL Server 2014](../../database-engine/install-windows/install-sql-server.md)  
  
  
