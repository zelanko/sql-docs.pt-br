---
title: Criar um projeto Visual c# SMO no Visual Studio .NET | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Visual C# [SMO]
ms.assetid: 1e7abb16-23a0-4a18-91ad-253261e6bf84
caps.latest.revision: 43
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 63c461e734c4ecb4a53b06e73199002aff64b539
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39555866"
---
# <a name="how-to-create-a-visual-c-smo-project-in-visual-studio-net"></a>Como criar um projeto SMO do Visual C# no Visual Studio .NET
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  Esta seção descreve como criar um aplicativo de console SMO simples.  
  
 Este exemplo importa namespaces que permitem ao programa referenciar tipos SMO. A importação do **agente** namespace é opcional. Use-a quando estiver gravando um programa que usa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. O **comuns** namespace é necessário para estabelecer uma conexão segura com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O **SqlClient** namespace é usado para processar erros de exceção SQL.  
  
### <a name="creating-a-visual-c-smo-project-in-visual-studionet"></a>Criando um projeto SMO do Visual C# no Visual Studio .NET  
  
1. Inicie o Visual Studio
  
2. Sobre o **arquivo** menu, clique em **New** e, em seguida, **projeto**.  A caixa de diálogo **Novo Projeto** será exibida.   
  
3. No [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **instalado** painel, navegue até **modelos**\\**Visual c#**\\**Windows** e selecione **aplicativo de Console**.  
  
4. (Opcional) No **nome** texto, digite o nome do novo aplicativo.  

5. Clique em **Okey** para carregar o modelo de aplicativo de console.  

6. Siga as instruções em [instalando o SMO](installing-smo.md) para instalar o pacote para seu projeto fazer referência.
  
7. No menu **Exibir** , clique em **Código**.
    
8. No código, antes da instrução do namespace, digite o seguinte **usando** instruções para qualificar os tipos no namespace SMO:
  
    ```  
    using Microsoft.SqlServer.Management.Smo;  
    using Microsoft.SqlServer.Management.Common;  
    ```  
  
15. O SMO tem vários namespaces em Microsoft.SqlServer.Management.Smo, como o Microsoft.SqlServer.Management.Smo.Agent. Adicione esses namespaces obrigatórios.  
  
16. Agora você pode adicionar seu código SMO.  
  
  
