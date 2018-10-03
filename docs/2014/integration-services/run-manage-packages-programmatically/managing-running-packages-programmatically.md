---
title: Gerenciar pacotes em execução programaticamente | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.topic: reference
helpviewer_keywords:
- packages [Integration Services], managing
- running packages [Integration Services]
ms.assetid: 0e91f4ac-6f29-40d7-8c28-9b82e4802c35
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b6537078fed6047fa16d759635d18ec484612b12
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48070667"
---
# <a name="managing-running-packages-programmatically"></a>Gerenciando pacotes em execução programaticamente
  Ao trabalhar programaticamente com pacotes [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], determine quais pacotes estão em execução no momento. A classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> do namespace <xref:Microsoft.SqlServer.Dts.Runtime> fornece métodos e classes que atendem a esses requisitos.  
  
 Para obter mais informações sobre o monitoramento de pacotes, consulte [Gerenciamento de Pacotes &#40;Serviço SSIS&#41;](../service/package-management-ssis-service.md).  
  
 Todos os métodos discutidos neste tópico exigem uma referência ao assembly `Microsoft.SqlServer.ManagedDTS`. Após adicionar a referência em um novo projeto, importe o namespace <xref:Microsoft.SqlServer.Dts.Runtime> com uma instrução `using` ou `Imports`.  
  
> [!IMPORTANT]  
>  Os métodos da classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> para funcionar com o Repositório de Pacotes do SSIS dão suporte apenas a “.”, localhost ou ao nome do servidor local. Você não pode usar "(local)".  
  
## <a name="determining-which-packages-are-currently-running"></a>Determinando quais pacotes estão em execução atualmente  
 Para determinar quais pacotes estão em execução atualmente no servidor especificado, chame o método <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetRunningPackages%2A>. Esse método retorna uma coleção <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackages> de objetos <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage>.  
  
> [!NOTE]  
>  Administradores consultam todos os pacotes que estão em execução atualmente no computador; outros usuários só verificam os pacotes iniciados por eles.  
  
## <a name="working-with-running-packages"></a>Trabalhando com pacotes em execução  
 Depois de determinar quais pacotes estão em execução no momento, você poderá recuperar informações sobre os pacotes e solicitar que um pacote seja interrompido.  
  
### <a name="getting-information-about-a-running-package"></a>Obtendo informações sobre um pacote em execução  
 Ao iterar na coleção <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackages>, você pode utilizar as propriedades do objeto <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage> para localizar um pacote ou para obter informações adicionais sobre os pacotes em execução:  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.ExecutionDuration%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.ExecutionStartTime%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.InstanceID%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.PackageDescription%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.PackageID%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.PackageName%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.UserName%2A>  
  
### <a name="stopping-a-running-package"></a>Interrompendo um pacote em execução  
 Você pode chamar o método <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.Stop%2A> de um objeto <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage> para solicitar que o pacote seja interrompido. Pode haver um atraso entre a hora em que uma solicitação de interrupção é emitida e a hora em que o pacote é realmente interrompido.  
  
![Ícone do Integration Services (pequeno)](../media/dts-16.gif "ícone do Integration Services (pequeno)")**mantenha-se para cima até o momento com o Integration Services** <br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciamento de Pacotes &#40;Serviço SSIS&#41;](../service/package-management-ssis-service.md)   
 [Enumerar pacotes disponíveis programaticamente](../run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)  
  
  
