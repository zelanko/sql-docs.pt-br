---
title: "Referenciando outros Assemblies em soluções de script | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
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
caps.latest.revision: 68
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3deb13c7e3aeb2e974ac6e6582555a617346a298
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="referencing-other-assemblies-in-scripting-solutions"></a>Referenciando outros assemblies em soluções de script
  O [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] biblioteca de classes fornece ao desenvolvedor de scripts com um conjunto avançado de ferramentas para implementar a funcionalidade personalizada em [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pacotes. A tarefa Script e o componente Script também podem usar assemblies gerenciados personalizados.  
  
> [!NOTE]  
>  Para habilitar seus pacotes utilizem os objetos e métodos de um serviço Web, use o **adicionar referência Web** disponível no comando [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA). Em versões anteriores do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], você teve que gerar uma classe proxy para usar um serviço Web.  
  
## <a name="using-a-managed-assembly"></a>Usando um assembly gerenciado  
 Para [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para localizar um assembly gerenciado em tempo de design, você deve fazer o seguinte:  
  
1.  Armazene o assembly gerenciado em qualquer pasta de seu computador.  
  
    > [!NOTE]  
    >  Em versões anteriores do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], só era possível adicionar uma referência a um assembly gerenciado que estivesse armazenado na pasta %windir%\Microsoft.NET\Framework\vx.x.xxxxx ou na pasta %ProgramFiles%\Microsoft SQL Server\100\SDK\Assemblies.  
  
2.  Adicione uma referência ao assembly gerenciado.  
  
     Para adicionar a referência, no VSTA, no **adicionar referência** caixa de diálogo de **procurar** guia, localize e adicione o assembly gerenciado.  
  
 Para que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] encontre o assembly gerenciado em tempo de execução, você deve seguir as seguintes etapas:  
  
1.  Assine o assembly gerenciado com um nome forte.  
  
2.  Instale o assembly no cache de assembly global do computador no qual o pacote é executado.  
  
     Para obter mais informações, consulte [compilando, implantando e Debugging Custom Objects](../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md).  
  
## <a name="using-the-microsoft-net-framework-class-library"></a>Usando a biblioteca de classes do Microsoft .NET Framework  
 A tarefa Script e o componente Script podem levar vantagem sobre todos os outros objetos e funcionalidades expostos pela biblioteca de classes [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Por exemplo, usando o [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], você pode recuperar informações sobre seu ambiente e pode interagir com o computador que está executando o pacote.  
  
 Esta lista descreve várias das classes [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] usadas com mais frequência:  
  
-   **System. Data** contém arquitetura ADO.NET.  
  
-   **System.IO** fornece uma interface para o sistema de arquivos e fluxos.  
  
-   **System** fornece a criação de formulários.  
  
-   **RegularExpressions** fornece classes para trabalhar com expressões regulares.  
  
-   **System. Environment** retorna informações sobre o computador local, o usuário atual e as configurações de computador e usuário.  
  
-   **System.Net** oferece comunicações de rede.  
  
-   **System. DirectoryServices** expõe o Active Directory.  
  
-   **System. Drawing** fornece bibliotecas de manipulação de imagens extensivos.  
  
-   **System. Threading** habilita a programação multi-threaded.  
  
 Para obter mais informações sobre o [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], consulte a Biblioteca MSDN.  
  
## <a name="see-also"></a>Consulte também  
 [Estendendo pacotes com scripts](../../integration-services/extending-packages-scripting/extending-packages-with-scripting.md)  
  
  
