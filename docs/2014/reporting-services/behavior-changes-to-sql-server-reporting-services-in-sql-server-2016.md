---
title: Alterações de comportamento do SQL Server Reporting Services no SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, backward compatibility
- rows [Reporting Services], heights
- leading blanks
- installing Reporting Services, behavior changes with release
- cryptography [Reporting Services]
- Setup [Reporting Services], behavior changes with release
- DefaultValueQueryBased property
- encryption [Reporting Services]
- decryption [Reporting Services]
- blank characters [SQL Server]
- initializing installations [Reporting Services]
- behavior changes [Reporting Services]
ms.assetid: 2a767f0f-84f2-4099-8784-1e37790f858e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 91fa7a66981f3e36c7e25babffbf73dc2519a0c2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109934"
---
# <a name="behavior-changes-to-sql-server-reporting-services--in-sql-server-2014"></a>Alterações de comportamento do SQL Server Reporting Services no SQL Server 2014
  Este tópico descreve as alterações no comportamento do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. As mudanças de comportamento afetam a maneira como os recursos funcionam ou interagem no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] em comparação com as versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 Neste tópico:  
  
-   [SQL Server 2014 Reporting Services alterações de comportamento](#bkmk_sql14)  
  
-   [SQL Server 2012 Reporting Services alterações de comportamento](#bkmk_rc0)  
  
-   [Alterações de comportamento de serviços de relatórios do SQL Server 2008 R2](#bkmk_kj)  
  
##  <a name="bkmk_sql14"></a> [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Alterações de comportamento do Reporting Services  
 Não há nenhuma alteração de comportamento do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
##  <a name="bkmk_rc0"></a> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Alterações de comportamento do Reporting Services  
 Esta seção descreve as alterações no comportamento do modo do SharePoint do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
### <a name="view-items-permission-will-not-download-shared-datasets-sharepoint-mode"></a>A permissão para Exibir Itens não baixará Conjuntos de Dados Compartilhados (Modo do SharePoint)  
 **Novo comportamento:** Os usuários com a permissão do SharePoint de "Exibir itens" não podem mais baixar o conteúdo de conjuntos de dados compartilhados do Reporting Services. Agora, essa alteração de comportamento é consistente com as permissões de "Exibir itens" para relatórios, fontes de dados e modelos. Os usuários com permissão de "Exibir itens" podem exibir e executar relatórios, fontes de dados e modelos, mas eles não conseguirem baixar seu conteúdo.  
  
 **Comportamento anterior:** Os usuários com a permissão do SharePoint de "Exibir itens" podem baixar o conteúdo de conjuntos de dados compartilhados do Reporting Services.  
  
 Para obter mais informações sobre os níveis de permissão do SharePoint, consulte [Permissões de usuários e níveis de permissão](https://technet.microsoft.com/library/cc721640.aspx)  
  
### <a name="report-server-trace-logs-are-in-a-new-location-for-sharepoint-mode-sharepoint-mode"></a>Logs de rastreamento de servidor de relatório estão em um novo local para o modo do SharePoint (Modo do SharePoint)  
 **Novo comportamento:** Para um servidor de relatório instalado no modo do SharePoint, os logs de rastreamento do servidor de relatório será em %Programfiles%\Common Files\Microsoft Shared\Web Server Extensions\14\Web services\reportserver\logfiles.  
  
 **Comportamento anterior:** Logs de rastreamento do servidor de relatório foram encontrados em um caminho semelhante ao seguinte: %Programfilesdir%\Microsoft SQL Server\\< RS_instance > services\logfiles.  
  
### <a name="getserverconfiginfo-soap-api-is-no-longer-supported-sharepoint-mode"></a>O GetServerConfigInfo SOAP API não tem mais suporte (Modo do SharePoint)  
 **Novo comportamento**: Use o cmdlet do PowerShell "Get-SPRSServiceApplicationServers"  
  
 **Comportamento anterior:** Os clientes podiam desenvolver o código cliente SOAP para se comunicar diretamente com o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ponto de extremidade e chamar getreportserverconfiginfo ().  
  
### <a name="report-server-configuration-and-management-tools"></a>Ferramentas de Configuração e Gerenciamento do Servidor de Relatório  
  
#### <a name="configuration-manager-is-not-used-for-sharepoint-mode"></a>O Configuration Manager não é usado para Modo do SharePoint  
 **Novo comportamento:** O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] do Configuration Manager não oferece suporte a servidores de relatório no modo do SharePoint. A configuração de modo do SharePoint [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] pode ser concluída agora usando a administração Central do SharePoint e, portanto, o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Configuration Manager não oferece mais suporte ao modo do SharePoint. O Configuration Manager é usado agora apenas para servidores de relatórios de modo nativo.  
  
#### <a name="you-cannot-change-the-server-from-one-mode-to-another"></a>Você não pode alterar o servidor de um modo para outro  
 **Novo comportamento:** Você não pode alterar modos de servidor. Se você instalar um servidor de relatório como modo nativo, não poderá alterá-lo ou reconfigurá-lo para ser modo do SharePoint. Se você instalar no modo SharePoint, poderá alterar o servidor de relatório para o modo nativo.  
  
 **Comportamento anterior:** Cliente instala um [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] servidor de relatório no modo do SharePoint. Se o cliente desejar alternar o servidor de relatório para o modo nativo, ele poderá abrir o gerenciador de configuração do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para alternar para o modo nativo, criando um novo ou se conectando a um banco de dados de modo nativo existente. O cliente também pode usar o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Configuration Manager para alternar do modo do SharePoint para o modo nativo.  
  
##  <a name="bkmk_kj"></a> Alterações de comportamento de serviços de relatórios do SQL Server 2008 R2  
 Esta seção descreve as alterações no comportamento do [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
> [!NOTE]  
>  Como o SQL Server 2008 R2 é uma atualização de versão secundária do SQL Server 2008, recomendamos que você também revise o conteúdo na seção do SQL Server 2008.  
  
### <a name="secureconnectionlevel-property-in-the-reporting-services-wmi-provider-library"></a>Propriedade SecureConnectionLevel na biblioteca do Provedor WMI do Reporting Services  
 Na biblioteca do provedor WMI do [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], o **SecureConnectionLevel** propriedade permite que os valores de `0`,`1`,`2`,`3`, com `0` indicando que o Secure Socket Layer (SSL) não é necessário para qualquer um dos métodos de serviço Web `3` indicando que o SSL é necessário para todos os métodos de serviço da Web, e `1` e `2` indicar subconjuntos de métodos de serviço Web que exigem SSL. No [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], esses valores terão apenas dois significados possíveis:  
  
-   `0` indica que o SSL não é exigido para nenhum dos métodos de serviço Web.  
  
-   Um inteiro positivo indica que o SSL é exigido para todos os métodos de serviço Web.  
  
 Essa alteração afeta como o servidor de relatório responde a chamadas de serviço Web. Por exemplo, <xref:ReportService2005.ReportingService2005.ListSecureMethods%2A> agora não retornará nada se **SecureConnectionLevel** é definido como 0 e todos os métodos em <xref:ReportService2005.ReportingService2005> se **SecureConnectionLevel** é definido como `1`, `2`, ou `3`.  
  
## <a name="see-also"></a>Consulte também  
 [O que há de novo &#40;Reporting Services&#41;](what-s-new-reporting-services.md)   
 [Recursos preteridos no SQL Server Reporting Services no SQL Server 2014](deprecated-features-in-sql-server-reporting-services-ssrs.md)   
 [Funcionalidade descontinuada do SQL Server Reporting Services no SQL Server 2014](discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)   
 [Alterações recentes no SQL Server Reporting Services no SQL Server 2014](breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md)  
  
  
