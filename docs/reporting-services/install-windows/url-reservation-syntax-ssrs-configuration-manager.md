---
title: Sintaxe de reserva de URL (Gerenciador de Configurações do SSRS) | Microsoft Docs
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- URL reservations
ms.assetid: 30e4be2e-e65d-462c-895a-5a0a636d042f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 115035e4ab8711a251ec8d2ac253b9987b5ebe66
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62651663"
---
# <a name="url-reservation-syntax--ssrs-configuration-manager"></a>Sintaxe de reserva de URL (Gerenciador de Configurações do SSRS)
  Este tópico descreve as partes da cadeia de caracteres da URL para o serviço Web Servidor de Relatório e o Gerenciador de Relatórios. A cadeia de caracteres da URL armazenada internamente tem uma estrutura diferente de uma URL digitada na barra de Endereço de uma janela do navegador. A cadeia de caracteres de reserva de URL aparece na janela Resultados da ferramenta Configuração do Reporting Services quando você configura uma URL e no arquivo RSReportServer.config. Poderá ser útil saber como a cadeia de caracteres da URL é definida se você estiver solucionando problemas de reserva de URL ou consultando HTTP.SYS para exibir as reservas de URL internas que estão definidas em seu servidor.  
  
## <a name="url-syntax"></a>Sintaxe da URL  
 Uma URL de servidor de relatórios é armazenada no elemento **UrlString** e no elemento **VirtualDirectory** . A razão para a separação de **UrlString** e **VirtualDirectory** em elementos separados é que você pode ter várias cadeias de caracteres de URL, mas apenas um nome de diretório virtual para cada aplicativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Em HTTP.SYS, a reserva de URL inclui **UrlString** e **VirtualDirectory**. A sintaxe para uma reserva de URL tem as seguintes partes:  
  
 \<scheme>://\<hostname>:\<port>/\<virtualdirectory>  
  
 A tabela a seguir descreve cada propriedade e quais valores são válidos para cada uma.  
  
|Propriedade|Valores válidos|Descrição|  
|--------------|------------------|-----------------|  
|Esquema|http ou https|Prefixos para conexões não SSL e SSL.|  
|Nome_do_host|(+) Curinga forte, equipara-se ao valor **(Todos Atribuídos)** para o endereço IP.<br /><br /> (\*) Curinga fraco, equipara-se a um endereço IP **(Todos os Não Atribuídos)** .<br /><br /> Nome de domínio totalmente qualificado<br /><br /> Nome do computador<br /><br /> Endereço IP (IPV4)<br /><br /> Endereço IP (IPV6)|Identifica o servidor na rede.<br /><br /> (+) Curinga forte é o padrão. HTTP.SYS aceitará todas as solicitações em todos os adaptadores de rede para uma determinada combinação de porta e diretório virtual. O servidor de relatório aceitará qualquer solicitação na porta.<br /><br /> (\*) Curinga fraco. HTTP.SYS aceita todas as solicitações não tratadas por outras reservas de URL em todos os adaptadores de rede para uma determinada combinação de porta e diretório virtual.<br /><br /> Nome do computador é o nome NEBIOS do computador na rede.<br /><br /> O nome de domínio totalmente qualificado inclui o endereço do domínio e o nome do servidor, como registrado em um controlador de domínio ou em um servidor de nome de domínio público.<br /><br /> Endereço IP (IPV4) é o endereço IP de um adaptador de rede no computador no formato IPV4: *nnn.nnn.nnn.nnn*.<br /><br /> Endereço IP (IPV6) é o endereço IP de um adaptador de rede no computador no formato IPV6: \<header>:\<header>:*nnn.nnn.nnn.nnn*.|  
|Porta|80<br /><br /> 443<br /><br /> \<custom>|A porta 80 é a padrão para solicitações HTTP para e de um servidor.<br /><br /> A porta 443 é a padrão para conexões SSL.<br /><br /> Você pode usar qualquer porta que ainda não esteja reservada por outro aplicativo.|  
|VirtualDirectory|ReportServer *[_InstanceName]*<br /><br /> Reports *[_InstanceName]*<br /><br /> \<custom>|Especifica o nome do aplicativo. Esse valor é uma cadeia de caracteres. Por padrão, o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa ReportServer e Reports como os nomes de aplicativos para o serviço Web Servidor de Relatórios e Gerenciador de Relatórios. Você pode usar nomes diferentes se preferir.<br /><br /> Esse valor é necessário. Ele identifica o aplicativo.<br /><br /> Especifique apenas um diretório virtual para cada instância de aplicativo. Para criar várias URLs para o mesmo aplicativo na mesma instância, crie várias versões de **UrlString**. Para criar nomes de diretórios virtuais exclusivos para várias instâncias de aplicativo, considere a inclusão do nome da instância no nome do diretório virtual, usando o caractere sublinhado (_) para anexar o nome da instância. *InstanceName* é opcional, mas recomendado se você tiver várias instâncias no mesmo computador. Para obter mais informações sobre como definir reservas de URL para instâncias nomeadas, consulte [Reservas de URL para implantações do Servidor de Relatório com várias instâncias &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/url-reservations-for-multi-instance-report-server-deployments.md).<br /><br /> O valor do diretório virtual não diferencia maiúsculas de minúsculas. Você pode usar qualquer cadeia de caracteres, desde que não inclua caracteres separadores de URL ou codificação de URL.|  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar as URLs do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [Configurar uma URL &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
  
  
