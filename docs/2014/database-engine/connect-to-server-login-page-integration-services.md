---
title: Conectar ao Servidor (página Logon) Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.connecttodtsserver.login.f1
- sql12.swb.connecttodts.login.f1
ms.assetid: 402c2de4-f4ea-40b0-909f-3ddf3bd59950
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 53a9793fc2a8770c8d926c945ba31a335bdfed3f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62808717"
---
# <a name="connect-to-server-login-page-integration-services"></a>Conectar-se ao Servidor (página Logon) Integration Services
  Use essa guia para exibir ou especificar as seguintes opções ao se conectar ao [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
## <a name="options"></a>Opções  
 **Tipo de servidor**  
 Ao registrar um servidor a partir do Pesquisador de Objetos, selecione o tipo de servidor ao qual se conectar: [!INCLUDE[ssDE](../includes/ssde-md.md)], Analysis Services, Reporting Services ou Integration Services. O restante da caixa de diálogo mostra somente as opções que válidas ao tipo de servidor selecionado. Ao registrar um servidor de Servidores Registrados, a caixa **Tipo de servidor** é somente leitura e corresponde ao tipo de servidor exibido no componente Servidores Registrados. Para registrar outro tipo de servidor, selecione [!INCLUDE[ssDE](../includes/ssde-md.md)], Analysis Services, Reporting Services ou Integration Services na barra de ferramentas Servidores Registrados antes de iniciar o registro de um novo servidor.  
  
 **Nome do servidor**  
 Selecione o servidor ao qual conectar-se. Por padrão, é exibida a instância de servidor usada na última conexão.  
  
> [!NOTE]  
>  Não use  *\<servername >*\\*\<instancename >*, pois [!INCLUDE[ssIS](../includes/ssis-md.md)] não oferece suporte a várias instâncias em um computador.  
  
 **Autenticação**  
 Somente a Autenticação do [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows está disponível para o [!INCLUDE[ssIS](../includes/ssis-md.md)]. Windows permite que um usuário conecte-se por meio de uma conta de usuário do Windows.  
  
 **Nome de usuário**  
 Essa opção não está disponível porque só a Autenticação do Windows está disponível para o [!INCLUDE[ssIS](../includes/ssis-md.md)].  
  
 **Senha**  
 Essa opção não está disponível porque só a Autenticação do Windows está disponível para o [!INCLUDE[ssIS](../includes/ssis-md.md)].  
  
 **Lembrar senha**  
 Essa opção não está disponível porque só a Autenticação do Windows está disponível para o [!INCLUDE[ssIS](../includes/ssis-md.md)].  
  
 **Connect**  
 Conecte-se com o servidor selecionado acima.  
  
 **Opções**  
 Clique para alterar a caixa de diálogo e ocultar as opções de conexão de servidor adicionais, como lembrar a senha.  
  
  
