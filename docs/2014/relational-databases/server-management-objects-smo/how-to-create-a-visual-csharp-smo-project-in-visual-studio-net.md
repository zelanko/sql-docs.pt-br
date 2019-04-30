---
title: Criar um projeto Visual c# SMO no Visual Studio .NET | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- Visual C# [SMO]
ms.assetid: 1e7abb16-23a0-4a18-91ad-253261e6bf84
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 371da8231138fb43e9b001808b9fb88ad09543b5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63131648"
---
# <a name="create-a-visual-c-smo-project-in-visual-studio-net"></a>Criar um projeto SMO do Visual C# no Visual Studio .NET
  Esta seção descreve como criar um aplicativo de console SMO simples.  
  
 Este exemplo importa namespaces que permitem ao programa referenciar tipos SMO. A importação do namespace `Agent` é opcional. Use-a quando estiver gravando um programa que usa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. O namespace `Common` é obrigatório para estabelecer uma conexão segura com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O namespace `SqlClient` é usado para processar erros de exceção do SQL.  
  
### <a name="creating-a-visual-c-smo-project-in-visual-studionet"></a>Criando um projeto SMO do Visual C# no Visual Studio .NET  
  
1.  Inicie o [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)] (ou [!INCLUDE[vsprvslong](../../includes/vsprvslong-md.md)]).  
  
2.  No menu **Arquivo**, clique em **NewProject.** A caixa de diálogo **Novo Projeto** será exibida.  
  
3.  Na **tipos de projeto** caixa de diálogo, selecione **Visual c#** e, em seguida, selecione **Windows**. No [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] painel de modelos instalados, selecione **aplicativo do Windows**.  
  
4.  (Opcional) No **nome** , digite o nome do novo aplicativo  
  
5.  Selecione o tipo de aplicativo do Visual C#. Para os exemplos a seguir, selecione **aplicativo de Console**.  
  
6.  No menu **Projeto**, selecione **Adicionar Referência**. A caixa de diálogo **Adicionar Referência** é exibida.  
  
7.  Clique em **navegue**, localize os assemblies SMO no [!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)] pasta e, em seguida, selecione os arquivos a seguir. Estes são os arquivos mínimos exigidos para criar um aplicativos SMO:  
  
     Microsoft.SqlServer.ConnectionInfo.dll  
  
     Microsoft.SqlServer.Smo.dll  
  
     Microsoft.SqlServer.Management.Sdk.Sfc.dll  
  
     Microsoft.SqlServer.SqlEnum.dll  
  
    > [!NOTE]  
    >  Use a tecla `Ctrl` para selecionar mais de um arquivo.  
  
8.  Adicione os assemblies SMO necessários. Por exemplo, se estiver programando especificamente o [!INCLUDE[ssSB](../../includes/sssb-md.md)], adicione os seguintes assemblies:  
  
     Microsoft.SqlServer.ServiceBrokerEmum.dll  
  
9. Clique em **Abrir**.  
  
10. Sobre o **modo de exibição** menu, clique em **código**. - ou - selecione o Program1.cs [Design] Windows e clique duas vezes no formulário do windows para mostrar a janela de código.  
  
11. No código, antes da instrução do namespace, digite as instruções `using` a seguir para qualificar os tipos no namespace SMO:  
  
    ```  
    using Microsoft.SqlServer.Management.Smo;  
    using Microsoft.SqlServer.Management.Common;  
    ```  
  
12. O SMO tem vários namespaces em Microsoft.SqlServer.Management.Smo, como o Microsoft.SqlServer.Management.Smo.Agent. Adicione esses namespaces obrigatórios.  
  
13. Agora você pode adicionar seu código SMO.  
  
  
