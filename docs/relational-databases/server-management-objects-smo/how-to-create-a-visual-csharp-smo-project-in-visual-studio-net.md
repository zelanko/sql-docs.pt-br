---
description: Como criar um projeto SMO do Visual C# no Visual Studio .NET
title: Criar um projeto SMO do Visual C# no Visual Studio .NET
ms.custom: seo-dt-2019
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- Visual C# [SMO]
ms.assetid: 1e7abb16-23a0-4a18-91ad-253261e6bf84
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 943cfd787cccff42973862b12f0f52feae24410c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467187"
---
# <a name="how-to-create-a-visual-c-smo-project-in-visual-studio-net"></a>Como criar um projeto SMO do Visual C# no Visual Studio .NET
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  Esta seção descreve como criar um aplicativo de console SMO simples.  
  
 Este exemplo importa namespaces que permitem ao programa referenciar tipos SMO. A importação do namespace do **agente** é opcional. Use-a quando estiver gravando um programa que usa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. O namespace **comum** é necessário para estabelecer uma conexão segura com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O namespace **SqlClient** é usado para processar erros de exceção do SQL.  
  
### <a name="creating-a-visual-c-smo-project-in-visual-studionet"></a>Criando um projeto SMO do Visual C# no Visual Studio .NET  
  
1. Iniciar o Visual Studio
  
2. No menu **arquivo** , clique em **novo** e em **projeto**.  A caixa de diálogo **Novo Projeto** aparecerá.   
  
3. No painel [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **instalado** , navegue até **modelos** \\ **Visual C#** \\ **Windows** e selecione **aplicativo de console**.  
  
4. Adicional Na caixa de texto **nome** , digite o nome do novo aplicativo.  

5. Clique em **OK** para carregar o modelo de aplicativo de console.  

6. Siga as instruções em [instalando o Smo](installing-smo.md) para instalar o pacote para que seu projeto faça referência.
  
7. No menu **Exibir** , clique em **Código**.
    
8. No código, antes da instrução namespace, digite as instruções **using** a seguir para qualificar os tipos no namespace SMO:
  
    ```  
    using Microsoft.SqlServer.Management.Smo;  
    using Microsoft.SqlServer.Management.Common;  
    ```  
  
15. O SMO tem vários namespaces em Microsoft.SqlServer.Management.Smo, como o Microsoft.SqlServer.Management.Smo.Agent. Adicione esses namespaces obrigatórios.  
  
16. Agora você pode adicionar seu código SMO.  

