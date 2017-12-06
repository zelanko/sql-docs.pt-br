---
title: "Implementando uma classe Connection para uma extensão de processamento de dados | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: extensions
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- connections [Reporting Services], data processing extensions
- Connection class
- data processing extensions [Reporting Services], connections
ms.assetid: 7047d29e-a2c9-4e6f-ad02-635851a38ed7
caps.latest.revision: "42"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 8e93e40719bad391c46c4fe4521da751a4660a85
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="implementing-a-connection-class-for-a-data-processing-extension"></a>Implementando uma classe Connection para uma extensão de processamento de dados
  O objeto **Connection** representa uma conexão de banco de dados ou recurso semelhante e é o ponto de partida para usuários de uma extensão de processamento de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Ele representa as conexões com servidores de banco de dados, embora qualquer entidade com comportamento semelhante possa ser exposta como uma **Connection**.  
  
 Para implementar um objeto **Connection**, crie uma classe que implementa <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> e que, opcionalmente, implementa <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension>.  
  
 Em sua implementação, você deve garantir que uma conexão seja criada e aberta antes que comandos possam ser executados. Garanta que a sua implementação exija que os clientes abram e fechem conexões explicitamente, em vez de fazer com que ela abra e feche conexões de forma implícita para o cliente. Execute as suas verificações de segurança quando a conexão for obtida. A exigência de uma conexão existente para as outras classes da sua extensão de processamento de dados [!INCLUDE[ssRS](../../../includes/ssrs-md.md)] garantirá que essas verificações de segurança sejam sempre executadas quando você estiver trabalhando com a sua fonte de dados.  
  
 As propriedades da conexão desejada são representadas como uma cadeia de conexão. É altamente recomendável que as extensões de processamento de dados [!INCLUDE[ssRS](../../../includes/ssrs-md.md)] deem suporte à propriedade <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection.ConnectionString%2A> usando o sistema de pares de nome/valor familiar definido por OLE DB.  
  
> [!NOTE]  
>  Os objetos **Connection** costumam fazer uso intensivo de recursos para sua obtenção e, portanto, é recomendável considerar o pool de conexões ou outras técnicas para atenuar isso.  
  
 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> herda de <xref:Microsoft.ReportingServices.Interfaces.IExtension>. Você deve implementar a interface <xref:Microsoft.ReportingServices.Interfaces.IExtension> como parte da sua implementação da classe de conexão. A interface <xref:Microsoft.ReportingServices.Interfaces.IExtension> permite que uma classe implemente um nome de extensão localizado e processe informações de configuração específicas da extensão armazenadas no arquivo de configuração do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
 O objeto **Connection** contém a propriedade <xref:Microsoft.ReportingServices.Interfaces.IExtension.LocalizedName%2A> por meio de sua implementação de <xref:Microsoft.ReportingServices.Interfaces.IExtension>. É altamente recomendável que as extensões de processamento de dados do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] deem suporte à propriedade <xref:Microsoft.ReportingServices.Interfaces.IExtension.LocalizedName%2A>, para que usuários encontrem um nome familiar para a extensão em uma interface do usuário, como o Gerenciador de Relatórios.  
  
 O <xref:Microsoft.ReportingServices.Interfaces.IExtension> também permite que o objeto **Connection** recupere e processe dados de configuração personalizados armazenados no arquivo RSReportServer.config. Para obter mais informações sobre como processar dados de configuração personalizados, consulte o método <xref:Microsoft.ReportingServices.Interfaces.IExtension.SetConfiguration%2A>.  
  
 A classe que implementa <xref:Microsoft.ReportingServices.Interfaces.IExtension> não é descarregada da memória quando o resto de suas classes de extensão de processamento de dados é descarregado. Por causa disso, você pode usar a classe **Extension** para armazenar informações do estado da conexão cruzada ou armazenar dados que podem ser armazenados em cache em memória. A classe **Extension** permanece em memória enquanto o servidor de relatório estiver em execução.  
  
 Estenda a classe **Connection** para incluir suporte para credenciais no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] implementando <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension>. Quando você implementa as propriedades <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension.IntegratedSecurity%2A>, <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension.UserName%2A> e <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension.Password%2A> da interface <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension>, você habilita a caixa de seleção **Segurança Integrada** e as caixas de texto **Nome de usuário** e **Senha** da caixa de diálogo **Fonte de Dados** do Designer de Relatórios. Isto permite que o Designer de Relatórios armazene e recupere credenciais para fontes de dados que dão suporte a autenticação. As credenciais são armazenadas de forma protegida e usadas durante a renderização de relatórios em modo de visualização.  
  
> [!NOTE]  
>  A implementação de <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension> exige, implicitamente, que você implemente os membros das interfaces <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> e <xref:Microsoft.ReportingServices.Interfaces.IExtension>.  
>   
>  Para obter uma implementação de exemplo da classe **Connection**, consulte [Amostras de produto do SQL Server Reporting Services](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Consulte também  
 [Extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementando uma extensão de processamento de dados](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Biblioteca de extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
