---
title: "Implementando uma classe de Conexão para uma extensão de processamento de dados | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- connections [Reporting Services], data processing extensions
- Connection class
- data processing extensions [Reporting Services], connections
ms.assetid: 7047d29e-a2c9-4e6f-ad02-635851a38ed7
caps.latest.revision: 42
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 1108be24704c38f0891e623fda02803e5f8c21e5
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="implementing-a-connection-class-for-a-data-processing-extension"></a>Implementando uma classe Connection para uma extensão de processamento de dados
  O **Conexão** objeto representa uma conexão de banco de dados ou recurso semelhante e é o ponto de partida para usuários de um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] extensão de processamento de dados. Representa conexões a servidores de banco de dados, embora qualquer entidade com comportamento semelhante pode ser exposta como um **Conexão**.  
  
 Para implementar um **Conexão** de objeto, crie uma classe que implementa <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> e, opcionalmente, implemente <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension>.  
  
 Em sua implementação, você deve garantir que uma conexão seja criada e aberta antes que comandos possam ser executados. Garanta que a sua implementação exija que os clientes abram e fechem conexões explicitamente, em vez de fazer com que ela abra e feche conexões de forma implícita para o cliente. Execute as suas verificações de segurança quando a conexão for obtida. A exigência de uma conexão existente para as outras classes da sua extensão de processamento de dados [!INCLUDE[ssRS](../../../includes/ssrs-md.md)] garantirá que essas verificações de segurança sejam sempre executadas quando você estiver trabalhando com a sua fonte de dados.  
  
 As propriedades da conexão desejada são representadas como uma cadeia de conexão. É altamente recomendável que as extensões de processamento de dados [!INCLUDE[ssRS](../../../includes/ssrs-md.md)] deem suporte à propriedade <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection.ConnectionString%2A> usando o sistema de pares de nome/valor familiar definido por OLE DB.  
  
> [!NOTE]  
>  **Conexão** objetos geralmente são uso intensivo de recursos para obter, para que você talvez queira considerar o pool de conexões ou outras técnicas para mitigar isso.  
  
 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> herda de <xref:Microsoft.ReportingServices.Interfaces.IExtension>. Você deve implementar a interface <xref:Microsoft.ReportingServices.Interfaces.IExtension> como parte da sua implementação da classe de conexão. A interface <xref:Microsoft.ReportingServices.Interfaces.IExtension> permite que uma classe implemente um nome de extensão localizado e processe informações de configuração específicas da extensão armazenadas no arquivo de configuração do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
 O **Conexão** objeto contém o <xref:Microsoft.ReportingServices.Interfaces.IExtension.LocalizedName%2A> propriedade pela sua implementação de <xref:Microsoft.ReportingServices.Interfaces.IExtension>. É altamente recomendável que as extensões de processamento de dados do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] deem suporte à propriedade <xref:Microsoft.ReportingServices.Interfaces.IExtension.LocalizedName%2A>, para que usuários encontrem um nome familiar para a extensão em uma interface do usuário, como o Gerenciador de Relatórios.  
  
 <xref:Microsoft.ReportingServices.Interfaces.IExtension>também permite que seu **Conexão** objeto para recuperar e processar dados de configuração personalizados armazenados no arquivo rsreportserver. config. Para obter mais informações sobre como processar dados de configuração personalizados, consulte o método <xref:Microsoft.ReportingServices.Interfaces.IExtension.SetConfiguration%2A>.  
  
 A classe que implementa <xref:Microsoft.ReportingServices.Interfaces.IExtension> não é descarregada da memória quando o resto de suas classes de extensão de processamento de dados é descarregado. Por isso, você pode usar o **extensão** classe para armazenar informações de estado da conexão cruzada ou armazenar dados que podem ser armazenados em cache na memória. O **extensão** classe permanece na memória, desde que o servidor de relatório está em execução.  
  
 Você pode estender sua **Conexão** classe para incluir suporte para credenciais em [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] implementando <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension>. Quando você implementa o <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension.IntegratedSecurity%2A>, <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension.UserName%2A>, e <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension.Password%2A> propriedades do <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension> interface, você habilita o **segurança integrada** caixa de seleção e **Username** e **senha** caixas de texto do **fonte de dados** diálogo no Designer de relatórios. Isto permite que o Designer de Relatórios armazene e recupere credenciais para fontes de dados que dão suporte a autenticação. As credenciais são armazenadas de forma protegida e usadas durante a renderização de relatórios em modo de visualização.  
  
> [!NOTE]  
>  A implementação de <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension> exige, implicitamente, que você implemente os membros das interfaces <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> e <xref:Microsoft.ReportingServices.Interfaces.IExtension>.  
>   
>  Para obter um exemplo **Conexão** implementação da classe, consulte [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Consulte também  
 [Extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementando uma extensão de processamento de dados](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Biblioteca de extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
