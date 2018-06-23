---
title: Novo ou editar registro de servidor (guia Geral) (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.registerserver.general.reportserver.f1
ms.assetid: 5f899a8e-52ef-46b5-b7a9-f200ccd9f724
caps.latest.revision: 26
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 17c10bb36de85a7d0ad1d9522d5d54a540d51a61
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019642"
---
# <a name="new-or-edit-server-registration-general-tab-reporting-services"></a>Novo registro ou editar registro de servidor (guia Geral) (Reporting Services)
  Use essa guia para especificar opções ao registrar uma instância do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
 Para acessar essa página, em Servidores Registrados, clique em **Reporting Services** na barra de ferramentas **Servidores Registrados** , clique com o botão direito do mouse em qualquer grupo de servidores registrados, como **Reporting Services**, aponte para **Novo**e clique em **Registro de Servidor**.  
  
## <a name="options"></a>Opções  
 **Tipo de servidor**  
 Quando um servidor dos Servidores Registrados é registrado, a caixa **Tipo de servidor** é somente leitura e corresponde ao tipo de servidor exibido no painel **Servidores Registrados** . Para registrar um tipo de servidor diferente, clique no servidor desejado na barra de ferramentas **Servidores Registrados** antes de começar a registrar um novo servidor.  
  
 **Nome do servidor**  
 Especifique a instância do servidor de relatório para se conectar. No [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], você pode acessar um servidor de relatório por meio de seu nome de instância. Você pode ter uma instância de servidor de relatório para cada instância de SQL Server que instala. Se você estiver usando a instância padrão, digite o nome da instância do SQL Server. Caso esteja usando uma instância nomeada, especifique a instância nomeada para se conectar ao servidor de relatório no formato MSSQL$InstanceName.  
  
 **Autenticação**  
 A autenticação para um servidor de relatório é feita pelo Internet Information Services (IIS). Selecione um dos seguintes modos de autenticação ao se conectar ao Reporting Services:  
  
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
 Armazene a senha que você digitou. Essa opção só estará disponível se você clicou em **Básico** ou **Autenticação de Formatos**.  
  
> [!NOTE]  
>  Caso você tenha armazenado a senha e não queira mais fazê-lo, desmarque essa caixa de seleção e clique em **Salvar**.  
  
 **Nome do servidor registrado**  
 O nome que você deseja exibir em Servidores Registrados. Esse nome não precisa corresponder ao nome na caixa **Nome do servidor** .  
  
 **Descrição do servidor registrado**  
 Digite uma descrição opcional do servidor.  
  
 **Teste**  
 Clique para testar a conexão com o servidor selecionado em **Nome do servidor**.  
  
 **Salvar**  
 Clique para salvar as configurações do servidor registrado.  
  
  