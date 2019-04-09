---
title: Configurar um Firewall do Windows para acesso ao serviço SSIS | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- security [Integration Services], firewalls
- Windows Firewall [Integration Services]
- unauthorized access [Integration Services]
- Integration Services service, firewalls
- firewall systems [Integration Services]
- SQL Server Integration Services, firewalls
- SSIS, firewalls
ms.assetid: 39975cf2-c351-4205-8c39-27a0fadfb010
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c40d0003211c0446982f70a9c7a00c1f189808b6
ms.sourcegitcommit: aa4f594ec6d3e85d0a1da6e69fa0c2070d42e1d8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59241878"
---
# <a name="configure-a-windows-firewall-for-access-to-the-ssis-service"></a>Configurar um Firewall do Windows para acesso ao serviço SSIS
    
> [!IMPORTANT]  
>  Esse tópico discute o serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , um serviço do Windows para o gerenciamento de pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] dá suporte ao serviço para compatibilidade de versões anteriores com versões anteriores do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. A partir do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], você pode gerenciar objetos como pacotes no servidor do Integration Services.  
  
 O sistema windowsfirewall ajuda a impedir acesso não autorizado a recursos de computador por meio de uma conexão de rede. Para acessar o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] por meio desse firewall, você precisa configurar o firewall para habilitar o acesso.  
  
> [!IMPORTANT]  
>  Para gerenciar pacotes armazenados em um servidor remoto, você não precisa conectar-se à instância do serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] naquele servidor remoto. Em vez disso, edite o arquivo de configuração do serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] de forma que o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] exiba os pacotes armazenados no servidor remoto. Para obter mais informações, consulte [Configuring the Integration Services Service &#40;SSIS Service&#41;](configuring-the-integration-services-service-ssis-service.md).  
  
 O serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] usa o protocolo DCOM. Para obter mais informações sobre como o protocolo DCOM funciona através de firewalls, consulte o artigo "[Using Distributed COM with Firewalls](https://manualzz.com/doc/19762578/using-distributed-com-with-firewalls-by-michael-nelson-in...)".  
  
 Há muitos sistemas de firewall disponíveis. Se estiver executando um firewall diferente do windowsfirewall, consulte a documentação de seu firewall para obter informações específicas sobre o sistema que você está usando.  
  
 Se o firewall oferecer suporte a filtros no nível de aplicativo, você poderá usar a interface do usuário que o Windows fornece para especificar as exceções permitidas pelo firewall, como programas e serviços. Caso contrário, você precisará configurar o DCOM para usar um conjunto limitado de portas TCP. O link do site da Microsoft fornecido anteriormente inclui informações sobre como especificar as portas TCP a serem usadas.  
  
 O serviço Integration Services usa a porta 135, e ela não pode ser alterada. Você precisa abrir a porta TCP 135 para acessar o SCM (Gerenciador de Controle de Serviços). O SCM executa tarefas como iniciar e parar os serviços [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e transmitir solicitações de controle ao serviço em execução.  
  
 As informações da seção a seguir são específicas para o windowsfirewall. Você pode configurar o sistema de windowsfirewall executando um comando no prompt de comando, ou definindo as propriedades na caixa de diálogo windowsfirewall.  
  
 Para obter mais informações sobre as configurações padrão do Firewall do Windows e uma descrição das portas TCP que afetam o Mecanismo de Banco de Dados, o Analysis Services, o Reporting Services e o Integration Services, consulte [Configurar o Firewall do Windows para permitir acesso ao SQL Server](../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
## <a name="configuring-a-windowsfirewall"></a>Configurando um windowsfirewall  
 Você pode usar os comandos a seguir para abrir a porta TCP 135, adicionar o MsDtsSrvr.exe à lista de exceções e especificar o escopo de desbloqueio para o firewall.  
  
#### <a name="to-configure-a-windowsfirewall-using-the-command-prompt-window"></a>Para configurar um windowsfirewall usando a janela do prompt de comando  
  
1.  Execute o comando: `netsh firewall add portopening protocol=TCP port=135 name="RPC (TCP/135)" mode=ENABLE scope=SUBNET`  
  
2.  Execute o comando: `netsh firewall add allowedprogram program="%ProgramFiles%\Microsoft SQL Server\100\DTS\Binn\MsDtsSrvr.exe" name="SSIS Service" scope=SUBNET`  
  
    > [!NOTE]  
    >  Para abrir o firewall em todos os computadores e, também, para os computadores na Internet, substitua scope=SUBNET por scope=ALL.  
  
 O procedimento a seguir descreve como usar a interface do usuário do Windows para abrir a porta TCP 135, adicionar o MsDtsSrvr.exe à lista de exceções e especificar o escopo de desbloqueio para o firewall.  
  
#### <a name="to-configure-a-firewall-using-the-windowsfirewall-dialog-box"></a>Para configurar um firewall usando a caixa de diálogo windowsfirewall  
  
1.  No Painel de Controle, clique duas vezes em **Firewall do Windows**.  
  
2.  Na caixa de diálogo **Firewall do Windows** , clique na guia **Exceções** e em **Adicionar Programa.**  
  
3.  Na caixa de diálogo **Adicionar um Programa** , clique em **Procurar**, navegue até a pasta Arquivos de Programas\Microsoft SQL Server\100\DTS\Binn, clique em MsDtsSrvr.exe e em **Abrir**. Clique em **OK** para fechar a caixa de diálogo **Adicionar um Programa** .  
  
4.  Na guia **Exceções** , clique em **Adicionar Porta.**  
  
5.  Na caixa de diálogo **Adicionar uma Porta** , digite **RPC (TCP/135)** ou outro nome descritivo na caixa **Nome**, digite **135** na caixa **Número da porta** e selecione o **TCP**.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] O serviço sempre usa a porta 135. Não é possível especificar uma porta diferente.  
  
6.  Na caixa de diálogo **Adicionar uma Porta** , opcionalmente, você pode clicar em **Alterar Escopo** para modificar o escopo padrão.  
  
7.  Na caixa de diálogo **Alterar Escopo** , selecione **Minha rede (somente sub-rede)** ou digite uma lista personalizada e clique em **OK**.  
  
8.  Para fechar a caixa de diálogo **Adicionar uma Porta** , clique em **OK**.  
  
9. Para fechar a caixa de diálogo **Firewall do Windows** , clique em **OK**.  
  
    > [!NOTE]  
    >  Para configurar o Firewall do Windows, este procedimento usa o item **Firewall do Windows** no Painel de Controle. O item **Firewall do Windows** configura apenas o firewall do perfil do local de rede local. No entanto, também é possível configurar o Firewall do Windows por meio da ferramenta de linha de comando **netsh** ou do snap-in MMC (Console de Gerenciamento) da [!INCLUDE[msCoName](../includes/msconame-md.md)] denominado Firewall do Windows com Segurança Avançada. Para obter mais informações sobre como fazer isso, consulte [Configurar o Firewall do Windows para permitir acesso ao SQL Server](../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
## <a name="see-also"></a>Consulte também  
 [Configurando o Serviço Integration Services &#40;Serviço SSIS#41;](service/integration-services-service-ssis-service.md)   
 [Serviço Integration Services &#40;Serviço SSIS&#41;](service/integration-services-service-ssis-service.md)  
  
  
