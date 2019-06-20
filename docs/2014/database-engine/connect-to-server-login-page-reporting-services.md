---
title: Conectar ao Servidor (página Logon) Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.connecttors.login.f1
helpviewer_keywords:
- Connect to Server dialog box, Reporting Services
ms.assetid: d312c740-19d7-4931-84a2-88b805ec8439
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7369e9d37e5f706786410f8e171c89c6c38287d2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62808718"
---
# <a name="connect-to-server-login-page-reporting-services"></a>Conectar ao Servidor (página Logon) Reporting Services
  Use essa guia para exibir ou especificar as seguintes opções ao se conectar ao [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
## <a name="options"></a>Opções  
 **Tipo de servidor**  
 Ao registrar um servidor a partir do Pesquisador de Objetos, selecione o tipo de servidor ao qual se conectar: [!INCLUDE[ssDE](../includes/ssde-md.md)], Analysis Services, Reporting Services ou Integration Services. O restante da caixa de diálogo mostra somente as opções que válidas ao tipo de servidor selecionado. Ao registrar um servidor de Servidores Registrados, a caixa **Tipo de servidor** é somente leitura e corresponde ao tipo de servidor exibido no componente Servidores Registrados. Para registrar outro tipo de servidor, selecione [!INCLUDE[ssDE](../includes/ssde-md.md)], Analysis Services, Reporting Services ou Integration Services na barra de ferramentas Servidores Registrados antes de iniciar o registro de um novo servidor.  
  
 **Nome do servidor**  
 O modo de servidor da instância de servidor de relatório à qual você está se conectando determina o valor que você deve inserir.  
  
 Para um servidor de relatório executado no modo nativo, especifique a instância do servidor de relatório à qual se conectar. Se você estiver usando a instância padrão, geralmente, o nome do servidor será o nome do computador. Se você instalou uma instância nomeada, acrescente o nome da instância ao nome do servidor neste formato: \<servername >\\< InstanceName\>. O Reporting Services usa o caractere de barra invertida para delimitar o nome da instância.  
  
 Para um servidor de relatório executado no SharePoint em modo integrado, especifique um site do SharePoint. Você pode especificar qualquer site de uma coleção de sites que foi integrada ao [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. O URL que você fornecer deve incluir o HTTP ou prefixo HTTPS. Você deve ter permissão para acessar o site do SharePoint para se conectar a ele no Management Studio. O nível de permissão que foi atribuído a você determinará quais itens você pode exibir e gerenciar. Para obter mais informações, consulte [conectar-se a um servidor de relatório no Management Studio](../reporting-services/tools/connect-to-a-report-server-in-management-studio.md).  
  
 **Autenticação**  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] pode ser configurado para aceitar solicitações de Autenticação do Windows ou de Autenticação de formulários que são manipulados por uma extensão de autenticação personalizada fornecida por você. Selecione um dos seguintes modos de autenticação ao se conectar ao Reporting Services:  
  
 **Modo de Autenticação do Windows (Autenticação do Windows)**  
 Conecte-se à instância de servidor de relatório usando as credenciais do [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows.  
  
 **Autenticação Básica**  
 Conecte-se usando a **Autenticação Básica** se a instalação do Reporting Services estiver configurada para usar a Autenticação Básica.  
  
 **Autenticação de Formulários**  
 Conecte-se usando a **Autenticação de Formulários** se a instalação do Reporting Services estiver configurada para usar uma extensão de autenticação personalizada.  
  
 **Nome do Usuário**  
 Digite o nome de logon a ser usado na conexão. Essa opção estará disponível somente se você selecionou **Básica** ou **Autenticação de Formulários**.  
  
 **Senha**  
 Digite a senha para o nome de usuário. Essa opção só poderá ser editada se você selecionou **Básica** ou **Autenticação de Formulários**.  
  
 **Lembrar senha**  
 Armazene a senha que você digitou. Essa opção será exibida somente se você clicar em **Opções**e poderá ser editada apenas se você selecionou conectar-se usando **Básica** ou **Autenticação de Formulários**.  
  
 **Connect**  
 Conecte-se ao servidor selecionado.  
  
 **Opções**  
 Exiba opções de conexão de servidor adicionais, como lembrar a senha.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar uma conexão de banco de dados do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [Conectar-se a um servidor de relatório no Management Studio](../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Autenticação com o servidor de relatório](../reporting-services/security/authentication-with-the-report-server.md)  
  
  
