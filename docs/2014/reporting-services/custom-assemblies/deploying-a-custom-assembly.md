---
title: Implantando um assembly personalizado | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- deploying custom assemblies [Reporting Services]
- custom assemblies [Reporting Services], deploying
- custom assemblies [Reporting Services], updating
- updating custom assemblies
ms.assetid: c6674cd8-0de7-4a5a-9e7c-12ffa49f6fd2
caps.latest.revision: 46
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: db9a7f2660306b5a938041cc967d1daccc9bc97b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120973"
---
# <a name="deploying-a-custom-assembly"></a>Implantando um assembly personalizado
  Para implantar um assembly personalizado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], coloque o assembly nas pastas de aplicativo do Designer de Relatórios e do servidor de relatório. Por padrão, os assemblies personalizados recebem a permissão `Execution` no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para conceder privilégios aos assemblies personalizados além da permissão Executar, você precisará editar o arquivo de configuração rssrvpolicy.config do servidor de relatório e o arquivo de configuração rspreviewpolicy.config da janela de visualização do Designer de Relatórios. Como alternativa, você poderá instalar o seu assembly no GAC (cache de assembly global).  
  
> [!NOTE]  
>  Existem dois modos de visualização para o Designer de Relatórios: a guia Visualizar e a janela pop-up que é iniciada quando o projeto de relatório é inicializado no modo `DebugLocal`. A guia Visualizar executa todas as expressões de relatório usando o conjunto de permissões `FullTrust` e não aplica configurações de política de segurança. A janela pop-up de visualização foi desenvolvida para simular a funcionalidade do servidor de relatório e, portanto, tem um arquivo de configuração de política que você ou um administrador devem modificar para usar assemblies e extensões personalizadas no Designer de Relatórios. Essa visualização pop-up também bloqueia o assembly personalizado. Dessa forma, será preciso fechar a janela de visualização para modificar ou atualizar o seu código de assembly personalizado.  
  
###### <a name="to-deploy-a-custom-assembly-in-reporting-services"></a>Para implantar um assembly personalizado no Reporting Services  
  
1.  Copie o assembly personalizado do local de compilação para a pasta bin do servidor de relatório ou para a pasta do Designer de Relatórios. O local padrão da pasta bin do servidor de relatório é :%Arquivos de Programas%\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer\bin. O local padrão do Designer de Relatórios é %ProgramFiles%\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies.  
  
     Colocar o assembly personalizado na pasta bin do servidor de relatório permite publicar relatórios que referenciam o assembly personalizado; e colocá-lo na pasta do Designer de Relatórios permite executar e depurar relatórios que referenciam o assembly personalizado no Designer de Relatórios.  
  
     Se você precisar conceder permissões ao seu código de assembly personalizado além das permissões padrão de execução:  
  
2.  Abra o arquivo de configuração apropriado. O local padrão do arquivo rssrvpolicy.config é %ProgramFiles%\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer. O local padrão do arquivo rspreviewpolicy.config é %ProgramFiles%\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies.  
  
3.  Adicione um grupo de códigos ao assembly personalizado. Para obter mais informações, consulte [Desenvolvimento seguro &#40;Reporting Services&#41;](../extensions/secure-development/secure-development-reporting-services.md).  
  
## <a name="updating-custom-assemblies"></a>Atualizando assemblies personalizados  
 Em algum ponto, você pode precisar atualizar uma versão de um assembly personalizado que está sendo referenciado em vários relatórios publicados. Se esse assembly já existir no diretório bin do servidor de relatório ou do Designer de Relatórios e se o número da versão do assembly for incrementado ou alterado de alguma forma, os relatórios publicados atualmente não funcionarão mais. Você terá de atualizar a versão do assembly referenciado no elemento `CodeModules` da definição do relatório e republicar os relatórios. Se você souber que irá atualizar um assembly personalizado com frequência e se os seus relatórios publicados atualmente precisarem de uma referência para o novo assembly, talvez queira considerar o uso do mesmo número de versão em todas as atualizações de uma assembly em particular.  
  
 Se você não precisar que os seus relatórios publicados atualmente façam referência à nova versão do assembly, poder implantar o seu assembly personalizado no cache de assembly global. O cache de assembly global pode manter diversas versões do mesmo assembly, para que os seus relatórios atuais possam fazer referência à versão anterior do seu assembly e para que os seus relatórios recém-publicados possam fazer referência ao assembly atualizado. Outra abordagem seria definir o redirecionamento de associação do servidor de relatório para impor um redirecionamento de todas as solicitações para o assembly antigo para o novo. Você precisaria modificar os arquivos Web.config arquivo e ReportService.exe.config do servidor de relatório. A entrada poderia ser assim:  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Usando Assemblies personalizados com relatórios](using-custom-assemblies-with-reports.md)   
 [Trabalhando com assemblies e o cache de assembly global](http://go.microsoft.com/fwlink/?LinkId=63912)  
  
  