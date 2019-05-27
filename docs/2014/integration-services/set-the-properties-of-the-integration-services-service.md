---
title: Defina as propriedades do serviço do Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services service, configuring
- Integration Services service, properties
ms.assetid: 3a8ad546-0f58-4b31-ab56-58d6313b1098
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c40ec2d7da7dc8f46644632d29b6fb8d1101ff9b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66055635"
---
# <a name="set-the-properties-of-the-integration-services-service"></a>Definir as propriedades do serviço do Integration Services
    
> [!IMPORTANT]  
>  Esse tópico discute o serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , um serviço do Windows para o gerenciamento de pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] dá suporte ao serviço para compatibilidade de versões anteriores com versões anteriores do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. A partir do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], você pode gerenciar objetos como pacotes no servidor do Integration Services.  
  
 O serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] gerencia e monitora pacotes no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Quando você instala o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]pela primeira vez, o serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] é iniciado e o tipo de inicialização do serviço é definido como automático.  
  
 Após a instalação do serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , você pode definir as propriedades do serviço usando o SQL Server Configuration Manager ou o snap-in MMC dos Serviços.  
  
 Para configurar outros recursos importantes do serviço, incluindo os locais onde armazena e gerencia pacotes, é necessário modificar o arquivo de configuração do serviço. Para obter mais informações, consulte [Configurando o serviço Integration Services &#40; Serviço SSIS&#41;](service/integration-services-service-ssis-service.md).  
  
### <a name="to-set-properties-of-the-integration-services-service-by-using-sql-server-configuration-manager"></a>Para definir propriedades do serviço do Integration Services usando o SQL Server Configuration Manager  
  
1.  No menu **Iniciar** , aponte para **Todos os Programas**, **Microsoft SQL Server**, **Ferramentas de Configuração**e clique em **SQL Server Configuration Manager**.  
  
2.  No snap-in **SQL Server Configuration Manager** , localize **SQL Server Integration Services** na lista de serviços, clique com o botão direito do mouse em **SQL Server Integration Services**e clique em **Propriedades**.  
  
3.  Na caixa de diálogo **Propriedades do SQL Server Integration Services** , você pode fazer o seguinte:  
  
    -   Clique na guia **Fazer Logon** para exibir informações de logon, como o nome de conta.  
  
    -   Clique na guia **Serviço** para exibir informações sobre o serviço, como o nome do computador host, e para especificar o modo inicial do serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
        > [!NOTE]  
        >  A guia **Avançado** não contém nenhuma informação do serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
4.  Clique em **OK**.  
  
5.  No menu **Arquivo** , clique em **Sair** para fechar o snap-in **SQL Server Configuration Manager** .  
  
### <a name="to-set-properties-of-the-integration-services-service-by-using-services"></a>Para definir as propriedades do serviço do Integration Services usando Serviços  
  
1.  No **Painel de Controle**, se você estiver usando o Modo de exibição Clássico, clique em **Ferramentas Administrativas**ou, se estiver usando o Modo exibição de Categoria, clique em **Desempenho e Manutenção** e em **Ferramentas Administrativas**.  
  
2.  Clique em **Serviços**.  
  
3.  No snap-in **Serviços** , localize **SQL Server Integration Services** na lista de serviços, clique com o botão direito do mouse em **SQL Server Integration Services**e clique em **Propriedades**.  
  
4.  Na caixa de diálogo **Propriedades do SQL Server Integration Services** , você pode fazer o seguinte:  
  
    -   Clique na guia **Geral** . Para habilitar o serviço, selecione o tipo de inicialização automática ou manual. Para desabilitar o serviço, selecione Desabilitar na caixa **Tipo de inicialização** . A seleção de Desabilitar não interromperá o serviço se ele estiver em execução.  
  
         Se o serviço já estiver habilitado, você poderá clicar em **Parar** para interromper o serviço ou clicar em **Iniciar** para iniciar o serviço.  
  
    -   Clique na guia **Fazer Logon** para exibir ou editar as informações de logon.  
  
    -   Clique na guia **Recuperação** para exibir as respostas do computador padrão para a falha de serviço. Você pode modificar essas opções para adequar ao seu ambiente.  
  
    -   Clique na guia **Dependências** para exibir uma lista de serviços dependentes. O serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] não tem nenhuma dependência.  
  
5.  Clique em **OK**.  
  
6.  Opcionalmente, se o tipo de inicialização for Manual ou Automático, você poderá clicar com o botão direito do mouse em **SQL Server Integration Services** e clicar em **Iniciar, Parar ou Reiniciar**.  
  
7.  No menu **Arquivo** , clique em **Sair** para fechar o snap-in **Serviços** .  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar o serviço Integration Services](../../2014/integration-services/manage-the-integration-services-service.md)  
  
  
