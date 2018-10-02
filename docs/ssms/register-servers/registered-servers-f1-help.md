---
title: Ajuda F1 dos Servidores Registrados | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], Help
- Registered Servers [SQL Server], help
- SQL Server Management Studio Help [SQL Server], registered servers
ms.assetid: 59f76b28-ba78-4a1a-b5d5-8b581f30114d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ac157acea3b64b81bef5eb505b4c9b0d3525ba11
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47674935"
---
# <a name="registered-servers-f1-help"></a>Ajuda F1 dos Servidores Registrados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Essa seção contém a Ajuda F1 para o componente Servidores Registrados no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Ela descreve as várias opções disponíveis.
  
 Para saber mais sobre Servidores Registrados e obter links para saber o que fazer com eles, vá para o tópico [Registrar servidores](../../tools/sql-server-management-studio/register-servers.md) . 
 

 Clique para salvar as configurações de Servidores Registrados. 
 
 ## <a name="reporting-services-new-or-edit-server-registration-general-tab"></a>Novo Registro ou Editar Registro de Servidor (guia Geral) do Reporting Services 
  Use essa guia para especificar opções ao registrar uma instância do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 Para acessar essa página, em Servidores Registrados, clique em **Reporting Services** na barra de ferramentas **Servidores Registrados** , clique com o botão direito do mouse em qualquer grupo de servidores registrados, como **Reporting Services**, aponte para **Novo**e clique em **Registro de Servidor**.  
  
### <a name="options"></a>Opções  
 **Tipo de servidor**  
 Quando um servidor dos Servidores Registrados é registrado, a caixa **Tipo de servidor** é somente leitura e corresponde ao tipo de servidor exibido no painel **Servidores Registrados** . Para registrar um tipo de servidor diferente, clique no servidor desejado na barra de ferramentas **Servidores Registrados** antes de começar a registrar um novo servidor.  
  
 **Nome do servidor**  
 Especifique a instância do servidor de relatório para se conectar. No [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], você pode acessar um servidor de relatório por meio de seu nome de instância. Você pode ter uma instância de servidor de relatório para cada instância de SQL Server que instala. Se você estiver usando a instância padrão, digite o nome da instância do SQL Server. Caso esteja usando uma instância nomeada, especifique a instância nomeada para se conectar ao servidor de relatório no formato MSSQL$InstanceName.  
  
 **Autenticação**  
 A autenticação para um servidor de relatório é feita pelo Internet Information Services (IIS). Selecione um dos seguintes modos de autenticação ao se conectar ao Reporting Services:  
  
 **Modo de Autenticação do Windows (Autenticação do Windows)**  
 Conecte-se à instância de servidor de relatório usando as credenciais do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
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
  
> **OBSERVAÇÃO:** caso você tenha armazenado a senha e não queira mais fazê-lo, desmarque essa caixa de seleção e clique em **Salvar**.  
  
 **Nome do servidor registrado**  
 O nome que você deseja exibir em Servidores Registrados. Esse nome não precisa corresponder ao nome na caixa **Nome do servidor** .  
  
 **Descrição do servidor registrado**  
 Digite uma descrição opcional do servidor.  
  
 **Teste**  
 Clique para testar a conexão com o servidor selecionado em **Nome do servidor**.  
  
 
 ## <a name="analysis-services---multidimensional-data-new-or-edit-server-registration-general-tab"></a>Novo Registro ou Editar Registro de Servidor (guia Geral) do Analysis Services – Dados Multidimensionais
 
  Use essa guia para especificar opções ao registrar uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Para acessar esta página, em Servidores Registrados, clique em **Analysis Services** na barra de ferramentas Servidores Registrados, clique com o botão direito do mouse em qualquer grupo de servidores registrados, como **Analysis Services**, aponte para **Novo**e clique em **Registro do Servidor**.  
  
### <a name="options"></a>Opções  
 **Tipo de servidor**  
 Quando um servidor dos Servidores Registrados é registrado, a caixa **Tipo de servidor** é somente leitura e corresponde ao tipo de servidor exibido no painel Servidores Registrados. Para registrar um tipo de servidor diferente, clique no servidor desejado na barra de ferramentas **Servidores Registrados** antes de começar a registrar um novo servidor.  
  
 **Nome do servidor**  
 Selecione a instância do servidor com a qual se conectar. Por padrão, é exibida a instância de servidor usada na última conexão.  
  
 **Autenticação**  
 A Autenticação do Windows permite que um usuário se conecte usando as credenciais do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, como um usuário do Windows ou como um membro de um grupo do Windows.  
  
 **User name**  
 Essa opção não está disponível nesta versão.  
  
 **Senha**  
 Essa opção não está disponível nesta versão.  
  
 **Lembrar senha**  
 Essa opção não está disponível nesta versão.  
  
 **Nome do servidor registrado**  
 O nome que você deseja exibir em Servidores Registrados. Esse nome não precisa corresponder à caixa **Nome do servidor** .  
  
 **Descrição do servidor registrado**  
 Digite uma descrição opcional do servidor.  
  
 **Teste**  
 Clique para testar a conexão com o servidor selecionado em **Nome do servidor**. 
 
 ## <a name="ssis-new-or-edit-server-registration-general-tab"></a>Novo Registro ou Editar Registro de Servidor (guia Geral) do SSIS 
 
 Use esta guia para especificar opções ao registrar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 Para acessar essa página, em Servidores Registrados, clique em **Integration Services** na barra de ferramentas **Servidores Registrados** , clique com o botão direito do mouse em qualquer grupo de servidores registrados, aponte para **Novo**e clique em **Registro do Servidor**.  
  
### <a name="options"></a>Opções  
 **Tipo de servidor**  
 Quando um servidor é registrado em Servidores Registrados, a caixa **Tipo de servidor** é somente leitura e corresponde ao tipo de servidor exibido em Servidores Registrados. Para registrar um tipo diferente de servidor, clique em **Database Engine**, **Analysis Server**, **Reporting Services**, **SQL Server Compact** **Edition**, ou **Integration Services** na barra de ferramentas **Servidores Registrados** antes de começar a registrar um novo servidor.  
  
 **Nome do servidor**  
 Selecione o servidor ao qual se conectar. O servidor conectado da última vez é exibido por padrão.  
  
 **Autenticação**  
 O modo de Autenticação do Windows permite que um usuário se conecte por meio de uma conta de usuário do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
 **User name**  
 Essa opção não está disponível nesta versão.  
  
 **Senha**  
 Essa opção não está disponível nesta versão.  
  
 **Lembrar senha**  
 Essa opção não está disponível nesta versão.  
  
 **Nome do servidor registrado**  
 O nome que você deseja exibir em **Servidores Registrados**. Esse nome não precisa corresponder à caixa **Nome do servidor** .  
  
 **Descrição do servidor registrado**  
 Digite uma descrição opcional do servidor.  
  
 **Teste**  
 Clique para testar a conexão com o servidor selecionado em **Nome do servidor**. 
  

 
 
  
