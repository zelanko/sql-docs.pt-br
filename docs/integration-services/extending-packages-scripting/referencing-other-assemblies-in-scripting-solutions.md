---
title: Referenciar outros assemblies em soluções de script | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- SSIS Script task, .NET Framework
- Script task [Integration Services], adding references
- referencing custom assemblies
- SSIS Script task, VisualBasic namespace
- assemblies [Integration Services]
- VisualBasic namespace
- Script task [Integration Services], VisualBasic namespace
- Microsoft.VisualBasic namespace
- Script task [Integration Services], .NET Framework
- .NET Framework [Integration Services]
- referencing Web services
ms.assetid: 9b655bcd-19f6-43d8-9f89-1b4d299c6380
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e3be777b41c72544d6ce4d998d39d528fc6fcc2d
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86915942"
---
# <a name="referencing-other-assemblies-in-scripting-solutions"></a>Referenciando outros assemblies em soluções de script

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  A biblioteca de classes [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] fornece ao desenvolvedor de scripts um conjunto avançado de ferramentas para implementar uma funcionalidade personalizada em pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. A tarefa Script e o componente Script também podem usar assemblies gerenciados personalizados.  
  
> [!NOTE]
>  Para permitir que seus pacotes utilizem os objetos e métodos de um serviço Web, utilize o comando **Adicionar Referência Web** disponível em VSTA ([!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications). Em versões anteriores do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], você teve que gerar uma classe proxy para usar um serviço Web.  
  
## <a name="using-a-managed-assembly"></a>Usando um assembly gerenciado  
 Para que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] localize um assembly gerenciado em tempo de design, você deve seguir as seguintes etapas:  
  
1.  Armazene o assembly gerenciado em qualquer pasta de seu computador.  
  
    > [!NOTE]  
    >  Em versões anteriores do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], só era possível adicionar uma referência a um assembly gerenciado que estivesse armazenado na pasta %windir%\Microsoft.NET\Framework\vx.x.xxxxx ou na pasta %ProgramFiles%\Microsoft SQL Server\100\SDK\Assemblies.  
  
2.  Adicione uma referência ao assembly gerenciado.  
  
     Para adicionar a referência, no VSTA, na caixa de diálogo **Adicionar Referência**, na guia **Procurar**, localize e adicione o assembly gerenciado.  
  
 Para que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] encontre o assembly gerenciado em tempo de execução, você deve seguir as seguintes etapas:  
  
1.  Assine o assembly gerenciado com um nome forte.  
  
2.  Instale o assembly no cache de assembly global do computador no qual o pacote é executado.  
  
     Para obter mais informações, consulte [Compilar, implantar e depurar objetos personalizados](../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md).  
  
## <a name="using-the-microsoft-net-framework-class-library"></a>Usando a biblioteca de classes do Microsoft .NET Framework  
 A tarefa Script e o componente Script podem levar vantagem sobre todos os outros objetos e funcionalidades expostos pela biblioteca de classes [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Por exemplo, usando o [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], você pode recuperar informações sobre seu ambiente e pode interagir com o computador que está executando o pacote.  
  
 Esta lista descreve várias das classes [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] usadas com mais frequência:  
  
-   **System.Data** Contém a arquitetura ADO.NET.  
  
-   **System.IO** Fornece uma interface para o sistema de arquivos e os fluxos.  
  
-   **System.Windows.Forms** Oferece criação de formulários.  
  
-   **System.Text.RegularExpressions** Oferece classes para trabalhar com expressões regulares.  
  
-   **System.Environment** Retorna informações sobre o computador local, o usuário atual e as configurações do computador e do usuário.  
  
-   **System.Net** Oferece comunicações de rede.  
  
-   **System.DirectoryServices** Expõe o Active Directory.  
  
-   **System.Drawing** Oferece extensas bibliotecas de manipulação de imagem.  
  
-   **System.Threading** Habilita a programação multithreaded.  
  
 Para obter mais informações sobre o [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], consulte a Biblioteca MSDN.  
  
## <a name="see-also"></a>Consulte Também  
 [Estender pacotes com scripts](../../integration-services/extending-packages-scripting/extending-packages-with-scripting.md)  
  
  
