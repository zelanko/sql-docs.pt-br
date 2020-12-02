---
title: Implantando um assembly personalizado | Microsoft Docs
description: Saiba como implantar um assembly personalizado no SQL Server Reporting Services. Além disso, saiba como conceder a assemblies personalizados privilégios além das permissões de Execução.
ms.date: 11/23/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: custom-assemblies
ms.topic: reference
helpviewer_keywords:
- deploying custom assemblies [Reporting Services]
- custom assemblies [Reporting Services], deploying
- custom assemblies [Reporting Services], updating
- updating custom assemblies
ms.assetid: c6674cd8-0de7-4a5a-9e7c-12ffa49f6fd2
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2c68562c1be1817d8f7457f680b4f45169de4a1f
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96166879"
---
# <a name="deploying-a-custom-assembly"></a>Implantando um assembly personalizado
  Para implantar um assembly personalizado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], coloque o assembly nas pastas de aplicativo do Designer de Relatórios e do servidor de relatório. Por padrão, os assemblies personalizados recebem a permissão **Execução** no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para conceder privilégios aos assemblies personalizados além da permissão Executar, você precisará editar o arquivo de configuração rssrvpolicy.config do servidor de relatório e o arquivo de configuração rspreviewpolicy.config da janela de visualização do Designer de Relatórios. Como alternativa, você poderá instalar o seu assembly no GAC (cache de assembly global).  
  
> [!NOTE]  
>  Há dois modos de visualização do Designer de Relatórios: a guia Visualizar e a janela pop-up Visualizar, que é iniciada quando o Projeto de Relatório é inicializado no modo **DebugLocal**. A guia Visualizar executa todas as expressões de relatório usando o conjunto de permissões **FullTrust** e não aplica configurações de política de segurança. A janela pop-up de visualização foi desenvolvida para simular a funcionalidade do servidor de relatório e, portanto, tem um arquivo de configuração de política que você ou um administrador devem modificar para usar assemblies e extensões personalizadas no Designer de Relatórios. Essa visualização pop-up também bloqueia o assembly personalizado. Dessa forma, será preciso fechar a janela de visualização para modificar ou atualizar o seu código de assembly personalizado.  
  
## <a name="to-deploy-a-custom-assembly-in-reporting-services"></a>Para implantar um assembly personalizado no Reporting Services  
  
1.  Copie o assembly personalizado do local de compilação para a pasta bin do servidor de relatório ou para a pasta do Designer de Relatórios. 

     Colocar seu assembly personalizado na pasta bin do servidor de relatório permite que você publique relatórios que façam referência ao seu assembly personalizado. A localização padrão da pasta bin para o servidor de relatório é:

     Reporting Services 2016
     ```
     %ProgramFiles%\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer\bin
     ```
     Reporting Services 2017 e posterior
     ```
     %ProgramFiles%\Microsoft SQL Server Reporting Services\SSRS\ReportServer\bin
     ```
     Colocá-lo na pasta do Designer de Relatórios permite que você execute e depure relatórios que façam referência ao seu assembly personalizado no Designer de Relatórios. A localização padrão do Designer de Relatórios é:

     Visual Studio 2012
     ```
     C:\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE\PrivateAssemblies
     ```
     Visual Studio 2013
     ```
     C:\Program Files (x86)\Microsoft Visual Studio 12.0\Common7\IDE\PrivateAssemblies
     ```
     Visual Studio 2015
     ```
     C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\PrivateAssemblies
     ```
     Visual Studio 2017
     ```
     C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\CommonExtensions\Microsoft\SSRS
     ```
     Visual Studio 2019
     ```
     C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\CommonExtensions\Microsoft\SSRS
     ```  
2.  Abra o arquivo de configuração apropriado. A localização padrão de rssrvpolicy.config para o servidor de relatório é:

     Reporting Services 2016
     ```
     %ProgramFiles%\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer
     ```
     Reporting Services 2017 e posterior
     ```
     %ProgramFiles%\Microsoft SQL Server Reporting Services\SSRS\ReportServer
     ```
     Os arquivos a serem atualizados para o Designer de Relatórios são:

     Visual Studio 2012
     ```
     C:\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE\PrivateAssemblies\PreviewProcessingService.exe.config
     C:\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE\PrivateAssemblies\RSPreviewPolicy.config
     C:\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE\PrivateAssemblies\RSReportDesigner.config
     C:\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE\PrivateAssemblies\RSReportHost11.exe.config
     ```
     Visual Studio 2013
     ```
     C:\Program Files (x86)\Microsoft Visual Studio 12.0\Common7\IDE\PrivateAssemblies\PreviewProcessingService.exe.config
     C:\Program Files (x86)\Microsoft Visual Studio 12.0\Common7\IDE\PrivateAssemblies\RSPreviewPolicy.config
     C:\Program Files (x86)\Microsoft Visual Studio 12.0\Common7\IDE\PrivateAssemblies\RSReportDesigner.config
     C:\Program Files (x86)\Microsoft Visual Studio 12.0\Common7\IDE\PrivateAssemblies\RSReportHost.exe.config
     ```
     Visual Studio 2015
     ```
     C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\PrivateAssemblies\PreviewProcessingService.exe.config
     C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\PrivateAssemblies\RSPreviewPolicy.config
     C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\PrivateAssemblies\RSReportDesigner.config
     C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\PrivateAssemblies\RSReportHost.exe.config
     ```
     Visual Studio 2017
     ```
     C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\CommonExtensions\Microsoft\SSRS\PreviewProcessingService.exe.config
     C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\CommonExtensions\Microsoft\SSRS\RSPreviewPolicy.config
     C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\CommonExtensions\Microsoft\SSRS\RSReportDesigner.config
     C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\CommonExtensions\Microsoft\SSRS\RSReportHost.exe.config
     ```
     Visual Studio 2019
     ```
     C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\CommonExtensions\Microsoft\SSRS\PreviewProcessingService.exe.config
     C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\CommonExtensions\Microsoft\SSRS\RSPreviewPolicy.config
     C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\CommonExtensions\Microsoft\SSRS\RSReportDesigner.config
     C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\CommonExtensions\Microsoft\SSRS\RSReportHost.exe.config
     ```    
3.  Adicione um grupo de códigos ao assembly personalizado. Para obter mais informações, consulte [Desenvolvimento seguro &#40;Reporting Services&#41;](../../reporting-services/extensions/secure-development/secure-development-reporting-services.md).  
  
## <a name="updating-custom-assemblies"></a>Atualizando assemblies personalizados  
 Em algum ponto, você pode precisar atualizar uma versão de um assembly personalizado que está sendo referenciado em vários relatórios publicados. Se esse assembly já existir no diretório bin do servidor de relatório ou do Designer de Relatórios e se o número da versão do assembly for incrementado ou alterado de alguma forma, os relatórios publicados atualmente não funcionarão mais. Você precisará atualizar a versão do assembly referenciado no elemento **CodeModules** da definição do relatório e publicar os relatórios novamente. Se você souber que irá atualizar um assembly personalizado com frequência e se os seus relatórios publicados atualmente precisarem de uma referência para o novo assembly, talvez queira considerar o uso do mesmo número de versão em todas as atualizações de uma assembly em particular.  
  
 Se você não precisar que os seus relatórios publicados atualmente façam referência à nova versão do assembly, poder implantar o seu assembly personalizado no cache de assembly global. O cache de assembly global pode manter diversas versões do mesmo assembly, para que os seus relatórios atuais possam fazer referência à versão anterior do seu assembly e para que os seus relatórios recém-publicados possam fazer referência ao assembly atualizado. Outra abordagem seria definir o redirecionamento de associação do servidor de relatório para impor um redirecionamento de todas as solicitações para o assembly antigo para o novo. Você precisaria modificar os arquivos de configuração Web.config e ReportingServicesService.exe.config do servidor de relatório. A entrada poderia ser assim:  
  
```  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <dependentAssembly>  
            <assemblyIdentity name="myAssembly"  
                              publicKeyToken="32ab4ba45e0a69a1"  
                              culture="neutral" />  
            <bindingRedirect oldVersion="1.0.0.0"  
                             newVersion="2.0.0.0"/>  
         </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Usando assemblies personalizados com relatórios](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)   
 [Trabalhando com assemblies e o cache de assemblies global](https://go.microsoft.com/fwlink/?LinkId=63912)  
  
  
