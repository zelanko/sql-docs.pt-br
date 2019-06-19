---
title: Criar um projeto do Visual Basic SMO no Visual Studio .NET | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Visual Basic [SMO]
ms.assetid: d7a3892c-0f1c-4c4d-8480-b58dce3720bc
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 662916720b9953e0374bedb29890a36ced0cfac0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62753329"
---
# <a name="create-a-visual-basic-smo-project-in-visual-studio-net"></a>Criar um projeto SMO do Visual Basic no Visual Studio .NET
  Esta seção descreve como criar um aplicativo de console SMO simples.  
  
 Este exemplo importa namespaces que permitem ao programa referenciar tipos SMO. A importação do namespace `Agent` é opcional. Use-a quando estiver gravando um programa que usa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. O namespace `Common` é obrigatório para estabelecer uma conexão segura com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O namespace `SqlClient` é usado para processar erros de exceção do SQL.  
  
### <a name="creating-a-visual-basic-smo-project-in-visual-studionet"></a>Criando um projeto SMO do Visual Basic no Visual Studio .NET  
  
1.  Inicie o [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)] (ou [!INCLUDE[vsprvslong](../../includes/vsprvslong-md.md)]).  
  
2.  No menu **Arquivo**, clique em **NewProject.** A caixa de diálogo **Novo Projeto** será exibida.  
  
3.  Na **tipos de projeto** caixa de diálogo, selecione **Visual Basic**e, em seguida, selecione **Windows**. No [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] painel de modelos instalados, selecione **aplicativo de Console.**  
  
4.  (Opcional) No **nome** , digite o nome do novo aplicativo.  
  
5.  Clique em **Okey** para carregar o [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] modelo de aplicativo de console.  
  
6.  No menu **Projeto**, selecione **Adicionar Referência**. A caixa de diálogo **Adicionar Referência** é exibida.  
  
7.  Clique em **procurar**, localize os assemblies SMO na pasta C:\Program Files\Microsoft SQL Server\120\SDK\Assemblies e, em seguida, selecione os arquivos a seguir. Estes são os arquivos mínimos exigidos para criar um aplicativos SMO:  
  
     Microsoft.SqlServer.ConnectionInfo.dll  
  
     Microsoft.SqlServer.SqlEnum.dll  
  
     Microsoft.SqlServer.Smo.dll  
  
     Microsoft.SqlServer.Management.Sdk.Sfc  
  
    > [!NOTE]  
    >  Use a tecla `Ctrl` para selecionar mais de um arquivo.  
  
8.  Adicione os assemblies SMO necessários. Por exemplo, se estiver programando especificamente o [!INCLUDE[ssSB](../../includes/sssb-md.md)], adicione os seguintes assemblies:  
  
     Microsoft.SqlServer.ServiceBrokerEmum.dll  
  
9. Clique em **Abrir**.  
  
10. Sobre o **modo de exibição** menu, clique em **código**. - ou - selecione a janela Module1.vb para mostrar a janela de código.  
  
11. No código, antes de qualquer declaração, digite o seguinte **importações** instruções para qualificar os tipos no namespace SMO.  
  
    ```  
    Imports Microsoft.SqlServer.Management.Smo  
    Imports Microsoft.SqlServer.Management.Common  
    ```  
  
12. O SMO tem vários namespaces em Microsoft.SqlServer.Management.Smo, como o Microsoft.SqlServer.Management.Smo.Agent. Adicione esses namespaces obrigatórios.  
  
13. Agora você pode adicionar seu código SMO.  
  
  
