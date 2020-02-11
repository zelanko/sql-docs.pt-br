---
title: Criar um projeto do Visual C# SMO no Visual Studio .NET | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63131648"
---
# <a name="create-a-visual-c-smo-project-in-visual-studio-net"></a>Criar um projeto SMO do Visual C# no Visual Studio .NET
  Esta seção descreve como criar um aplicativo de console SMO simples.  
  
 Este exemplo importa namespaces que permitem ao programa referenciar tipos SMO. A importação do namespace `Agent` é opcional. Use-a quando estiver gravando um programa que usa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. O namespace `Common` é obrigatório para estabelecer uma conexão segura com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O namespace `SqlClient` é usado para processar erros de exceção do SQL.  
  
### <a name="creating-a-visual-c-smo-project-in-visual-studionet"></a>Criando um projeto SMO do Visual C# no Visual Studio .NET  
  
1.  Inicie o [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)] (ou [!INCLUDE[vsprvslong](../../includes/vsprvslong-md.md)]).  
  
2.  No menu **Arquivo**, clique em **NewProject.** A caixa de diálogo **Novo Projeto** aparecerá.  
  
3.  Na caixa de diálogo **tipos de projeto** , selecione **Visual C#** e, em seguida, selecione **Windows**. No painel [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] modelos instalados, selecione **aplicativo do Windows**.  
  
4.  Adicional No campo **nome** , digite o nome do novo aplicativo  
  
5.  Selecione o tipo de aplicativo do Visual C#. Para os exemplos a seguir, selecione **aplicativo de console**.  
  
6.  No menu **Projeto**, selecione **Adicionar Referência**. A caixa de diálogo **Adicionar Referência** é exibida.  
  
7.  Clique em **procurar**, localize os ASSEMBLIES do Smo [!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)] na pasta e, em seguida, selecione os arquivos a seguir. Estes são os arquivos mínimos exigidos para criar um aplicativos SMO:  
  
     Microsoft.SqlServer.ConnectionInfo.dll  
  
     Microsoft.SqlServer.Smo.dll  
  
     Microsoft.SqlServer.Management.Sdk.Sfc.dll  
  
     Microsoft.SqlServer.SqlEnum.dll  
  
    > [!NOTE]  
    >  Use a tecla `Ctrl` para selecionar mais de um arquivo.  
  
8.  Adicione os assemblies SMO necessários. Por exemplo, se estiver programando especificamente o [!INCLUDE[ssSB](../../includes/sssb-md.md)], adicione os seguintes assemblies:  
  
     Microsoft.SqlServer.ServiceBrokerEmum.dll  
  
9. Clique em **Abrir**.  
  
10. No menu **Exibir** , clique em **código**.-ou selecione as janelas Program1.cs [Design] e clique duas vezes no Windows Form para mostrar a janela de código.  
  
11. No código, antes da instrução do namespace, digite as instruções `using` a seguir para qualificar os tipos no namespace SMO:  
  
    ```  
    using Microsoft.SqlServer.Management.Smo;  
    using Microsoft.SqlServer.Management.Common;  
    ```  
  
12. O SMO tem vários namespaces em Microsoft.SqlServer.Management.Smo, como o Microsoft.SqlServer.Management.Smo.Agent. Adicione esses namespaces obrigatórios.  
  
13. Agora você pode adicionar seu código SMO.  
  
  
