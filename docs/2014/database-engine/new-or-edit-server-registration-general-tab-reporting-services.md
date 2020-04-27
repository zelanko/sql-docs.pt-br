---
title: Novo ou editar registro de servidor (guia geral) (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.registerserver.general.reportserver.f1
ms.assetid: 5f899a8e-52ef-46b5-b7a9-f200ccd9f724
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e0e6d6d3ad57726c42556c9ecc2662edce102e57
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62844262"
---
# <a name="new-or-edit-server-registration-general-tab-reporting-services"></a>Novo registro ou editar registro de servidor (guia Geral) (Reporting Services)
  Use essa guia para especificar opções ao registrar uma instância do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
 Para acessar essa página, em Servidores Registrados, clique em **Reporting Services** na barra de ferramentas **Servidores Registrados** , clique com o botão direito do mouse em qualquer grupo de servidores registrados, como **Reporting Services**, aponte para **Novo**e clique em **Registro de Servidor**.  
  
## <a name="options"></a>Opções  
 **Tipo de servidor**  
 Quando um servidor é registrado a partir de servidores registrados, a caixa **tipo de servidor** é somente leitura e corresponde ao tipo de servidor exibido no painel **servidores registrados** . Para registrar um tipo de servidor diferente, clique no servidor desejado na barra de ferramentas **Servidores Registrados** antes de começar a registrar um novo servidor.  
  
 **Nome do servidor**  
 Especifique a instância do servidor de relatório para se conectar. No [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], você pode acessar um servidor de relatório por meio de seu nome de instância. Você pode ter uma instância de servidor de relatório para cada instância de SQL Server que instala. Se você estiver usando a instância padrão, digite o nome da instância do SQL Server. Caso esteja usando uma instância nomeada, especifique a instância nomeada para se conectar ao servidor de relatório no formato MSSQL$InstanceName.  
  
 **Autenticação**  
 A autenticação para um servidor de relatório é feita pelo Internet Information Services (IIS). Selecione um dos seguintes modos de autenticação ao se conectar ao Reporting Services:  
  
 **Modo de Autenticação do Windows (Autenticação do Windows)**  
 Conecte-se à instância de servidor de relatório usando as credenciais do [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows.  
  
 **Autenticação básica**  
 Conecte-se usando a **Autenticação Básica** se a instalação do Reporting Services estiver configurada para usar a Autenticação Básica.  
  
 **Autenticação de Formulários**  
 Conecte-se usando a **Autenticação de Formulários** se a instalação do Reporting Services estiver configurada para usar uma extensão de autenticação personalizada.  
  
 **Nome de usuário**  
 Digite o nome de logon a ser usado na conexão. Essa opção estará disponível somente se você selecionou **Básica** ou **Autenticação de Formulários**.  
  
 **Senha**  
 Digite a senha para o nome de usuário. Essa opção só poderá ser editada se você selecionou **Básica** ou **Autenticação de Formulários**.  
  
 **Lembrar senha**  
 Armazene a senha que você digitou. Essa opção só estará disponível se você clicou em **Básico** ou **Autenticação de Formatos**.  
  
> [!NOTE]  
>   Caso tenha armazenado a senha e não deseja mais fazê-lo, desmarque essa caixa de seleção e clique em **Salvar**.  
  
 **Nome do servidor registrado**  
 O nome que você deseja exibir em Servidores Registrados. Esse nome não precisa corresponder ao nome na caixa **Nome do servidor** .  
  
 **Descrição do servidor registrado**  
 Digite uma descrição opcional do servidor.  
  
 **Teste**  
 Clique para testar a conexão com o servidor selecionado em **Nome do servidor**.  
  
 **Salvar**  
 Clique para salvar as configurações do servidor registrado.  
  
  
