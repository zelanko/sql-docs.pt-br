---
title: Instalar o Reporting Services e os Serviços de Informações da Internet lado a lado | Microsoft Docs
ms.custom: ''
ms.date: 07/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: ''
ms.component: install-windows
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- deploying [Reporting Services], IIS
ms.assetid: 9b651fa5-f582-4f18-a77d-0dde95d9d211
caps.latest.revision: 40
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 7645b04a492c182283c79c814be0c59baa23fbc6
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="install-reporting-and-internet-information-services-side-by-side"></a>Instalar o Reporting Services e os Serviços de Informações da Internet lado a lado

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Você pode instalar e executar o SSRS (SQL Server Reporting Services) e o IIS (Serviços de Informações da Internet) no mesmo computador. A versão do IIS utilizada determina os problemas de interoperabilidade a serem resolvidos.  
  
|Versão do IIS|Problemas|Description|  
|-----------------|------------|-----------------|  
|8.0, 8.5|As solicitações dirigidas a um aplicativo são aceitas por um aplicativo diferente.<br /><br /> O HTTP.SYS impõe as regras de precedência a reservas de URL. As solicitações enviadas a aplicativos com o mesmo nome de diretório virtual e que, ao mesmo tempo, monitoram a porta 80 podem não alcançar o destino pretendido se a reserva de URL for fraca, em relação à reserva de URL de outro aplicativo.|Em determinadas condições, um ponto de extremidade registrado que substitui outro ponto de extremidade de URL no esquema de reserva de URL pode receber solicitações HTTP destinadas a outro aplicativo.<br /><br /> Se você usar nomes do diretório virtual exclusivos para o serviço Web Servidor de Relatórios e o [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] , esse conflito será evitado.<br /><br /> Informações detalhadas sobre esse cenário são fornecidas neste tópico.|  
  
## <a name="precedence-rules-for-url-reservations"></a>Regras de precedência para reservas de URL  
 Antes de tratar de problemas de interoperabilidade entre o IIS e o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], você deve entender as regras de precedência de reserva de URL. As regras de precedência podem ser generalizadas na seguinte instrução: uma reserva de URL tem valores definidos mais explicitamente é a primeira a receber solicitações que correspondam à URL.  
  
-   Uma reserva de URL que especifica um diretório virtual é mais explícita que uma que omite um diretório virtual.  
  
-   Uma reserva de URL que especifica um único endereço (por meio de um endereço IP, um nome de domínio totalmente qualificado, um nome de computador de rede ou um nome do host) é mais explícita que um curinga.  
  
-   Uma reserva de URL que especifica um curinga forte é mais explícita que um curinga fraco.  
  
 Os seguintes exemplos mostram um intervalo de reservas de URL, ordenado do mais explícito ao menos explícito:  
  
|Exemplo|Solicitação|  
|-------------|-------------|  
|`http://123.234.345.456:80/reports`|Recebe todas as solicitações enviadas a `http://123.234.345.456/reports` ou `http://\<computername>/reports` se um serviço de nomes de domínio pode resolver o endereço IP para o nome do host.|  
|`http://+:80/reports`|Recebe todas as solicitações enviadas a qualquer endereço IP ou nome do host válido para esse computador desde que a URL contenha o nome do diretório virtual “reports”.|  
|`http://123.234.345.456:80`|Recebe qualquer solicitação que especifica `http://123.234.345.456` ou `http://\<computername>` se um serviço de nomes de domínio pode resolver o endereço IP para esse nome do host.|  
|`http://+:80`|Recebe solicitações que ainda não foram recebidas por outros aplicativos, para todos os pontos de extremidade do aplicativo mapeado como **Todos Atribuídos**.|  
|`http://*:80`|Recebe solicitações que ainda não foram recebidas por outros aplicativos, para todos os pontos de extremidade do aplicativo mapeado como **Todos Não Atribuídos**.|  
  
 Uma indicação de um conflito de porta é que você verá a seguinte mensagem de erro: 'System.IO.FileLoadException: O processo não pode acessar o arquivo porque está sendo usado por outro processo. (Exceção de HRESULT: 0x80070020).'  
  
## <a name="url-reservations-for-iis-80-85-with-sql-server-reporting-services"></a>Reservas de URL para o IIS 8.0, 8.5 com o SQL Server Reporting Services  
 Dadas as regras de precedência na seção anterior, você pode começar a compreender como as reservas de URL definidas para o Reporting Services e o ISS promovem a interoperabilidade. O Reporting Services recebe solicitações que especificam explicitamente os nomes de diretório virtuais para seus aplicativos; o IIS recebe todas as solicitações restantes, que podem ser direcionadas a aplicativos executados no modelo de processo do IIS.  
  
|Aplicativo|Reserva de URL|Description|Recebimento de solicitação|  
|-----------------|---------------------|-----------------|---------------------|  
|Servidor de relatório|`http://+:80/ReportServer`|Curinga forte na porta 80, com diretório virtual de servidor de relatório.|Recebe todas as solicitações na porta 80 que especificam o diretório virtual de servidor de relatório. O serviço Web Servidor de Relatórios recebe todas as solicitações para http://\<computername>/reportserver.|  
|Portal da Web|`http://+:80/Reports`|Curinga forte na porta 80, com o diretório virtual Reports.|Recebe todas as solicitações na porta 80 que especificam o diretório virtual de relatórios. O [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] recebe todas as solicitações para http://\<computername>/reports.|  
|IIS|`http://*:80/`|Curinga fraco na porta 80.|Recebe todas as solicitações restantes na porta 80 não recebidas por outro aplicativo.|  

## <a name="side-by-side-deployments-of-sql-server-reporting-services-on-iis-80-85"></a>Implantações lado a lado do SQL Server Reporting Services no IIS 8.0 a 8.5

 Os problemas de interoperabilidade entre o ISS e o Reporting Services ocorrem quando sites do IIS têm nomes de diretório virtual idênticos aos usados pelo Reporting Services. Por exemplo, suponha que você tenha a seguinte configuração:  
  
-   Um site no IIS atribuído à porta 80 e um diretório virtual chamado "Reports".  
  
-   Uma instância do servidor de relatório instalada na configuração padrão, em que a reserva de URL também especifica a porta 80 e o aplicativo [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] também usa “Reports” como o nome do diretório virtual.  
  
 Devido a essa configuração, uma solicitação enviada para http://\<computername>:80/reports será recebida pelo [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]. O aplicativo acessado por meio do diretório virtual Reports no IIS não receberá mais solicitações depois que a instância do servidor de relatório for instalada.  
  
 Se você estiver executando implantações lado a lado de versões mais antigas e mais recentes do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], é provável que encontre o problema de roteamento descrito. Isso porque todas as versões do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usam “ReportServer” e “Reports” como nomes de diretório virtual para os aplicativos de servidor de relatório e do [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] , aumentando a probabilidade de haver um diretório virtual "reports" e "reportserver" no IIS.  
  
 Para garantir que todos os aplicativos recebam solicitações, siga estas diretrizes:  
  
-   Para instalações do Reporting Services, use nomes de diretório virtual ainda não utilizados por um site do IIS na mesma porta que o Reporting Services. Se houver conflito, instale o Reporting Services no modo “somente arquivos” (usando a instalação, mas não configurando a opção do servidor no Assistente de Instalação), para que você possa configurar os diretórios virtuais depois que a instalação for concluída. Uma indicação de que a sua configuração possui um conflito de porta é que você verá a seguinte mensagem de erro: System.IO.FileLoadException: O processo não pode acessar o arquivo porque está sendo usado por outro processo. (Exceção de HRESULT: 0x80070020).  
  
-   Para instalações configuradas manualmente, adote as convenções de nomenclatura padrão nas URLs configuradas. Se você instalar o [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] como uma instância nomeada, inclua o nome da instância ao criar um diretório virtual.  

## <a name="next-steps"></a>Próximas etapas

[Configurar as URLs do Servidor de Relatório](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
[Configurar uma URL](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
[Instalar o servidor de relatórios de modo nativo do Reporting Services](../../reporting-services/install-windows/install-reporting-services-native-mode-report-server.md)  

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
