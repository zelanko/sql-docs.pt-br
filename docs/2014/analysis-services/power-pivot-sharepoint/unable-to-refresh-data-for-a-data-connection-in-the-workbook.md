---
title: 'Não é possível atualizar dados de uma conexão de dados na pasta de trabalho. Tente outra vez ou entre em contato com o administrador do sistema. As seguintes conexões não foram atualizadas: dados PowerPivot | Microsoft Docs'
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 0f6fd52d-ac72-43e3-aa08-05a2d2bb873d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4deeeaae2bb08d9f1e2b4c434ec262d0fb7bd679
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48077486"
---
# <a name="unable-to-refresh-data-for-a-data-connection-in-the-workbook-try-again-or-contact-your-system-administrator-the-following-connections-failed-to-refresh-powerpivot-data"></a>Não é possível atualizar dados de uma conexão de dados na pasta de trabalho. Tente outra vez ou entre em contato com o administrador do sistema. As seguintes conexões não foram atualizadas: Dados PowerPivot
  Para pastas de trabalho do Excel contendo dados PowerPivot, os Serviços do Excel retornam este erro quando submetem uma solicitação de conexão a um servidor do PowerPivot e a solicitação falha.  
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Aplica-se a:|Instalação do PowerPivot para SharePoint|  
|Versão do Produto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|Veja abaixo.|  
|Texto da mensagem|Não é possível atualizar dados de uma conexão de dados na pasta de trabalho. Tente outra vez ou entre em contato com o administrador do sistema. As seguintes conexões não foram atualizadas: Dados PowerPivot|  
  
## <a name="explanation-and-resolution"></a>Explicação e resolução  
 Os Serviços do Excel não podem se conectar a nem carregar dados PowerPivot. As condições que causam esse erro incluem:  
  
 **Cenário 1: o serviço não é iniciado**  
  
 A instância do SQL Server Analysis Services (PowerPivot) não é iniciada. Uma senha expirada interromperá a execução do serviço. Para obter mais informações sobre como alterar a senha, consulte [configurar contas de serviço PowerPivot](configure-power-pivot-service-accounts.md) e [iniciar ou parar um PowerPivot para SharePoint Server](start-or-stop-a-power-pivot-for-sharepoint-server.md).  
  
 **Cenário 2a: Abrindo uma pasta de trabalho de versão anterior no servidor**  
  
 A pasta de trabalho que você está tentando abrir pode ter sido criada na versão SQL Server 2008 R2 do PowerPivot para Excel. Muito provavelmente, o provedor de dados do Analysis Services especificado na cadeia de conexão de dados não está presente no computador que está executando a solicitação.  
  
 Se esse for o caso, você encontrará esta mensagem no log ULS: "Falha na atualização dos 'Dados PowerPivot' na pasta de trabalho '\<URL para a pasta de trabalho >'", seguido por "Não é possível obter uma conexão".  
  
 Para determinar a versão da pasta de trabalho, abra-a no Excel e verifique o provedor de dados que está especificado na cadeia de conexão. Uma pasta de trabalho do SQL Server 2008 R2 usa MSOLAP.4 como provedor de dados.  
  
 Para resolver esse problema, você pode atualizar a pasta de trabalho. Opcionalmente, você pode instalar bibliotecas de cliente da versão SQL Server 2008 R2 do Analysis Services nos computadores físicos que executam o PowerPivot para SharePoint ou Serviços do Excel:  
  
 [Instalar o Provedor Analysis Services OLE DB nos servidores do SharePoint](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)  
  
 **Cenário 2b: Serviços do Excel em execução em um servidor de aplicativos que tem a versão incorreta das bibliotecas de cliente**  
  
 Por padrão, o SharePoint Server 2010 instala a versão SQL Server 2008 do provedor OLE DB do Analysis Services em servidores de aplicativos que executam Serviços do Excel. Em um farm com suporte para o acesso a dados PowerPivot, todos os servidores físicos que executam aplicativos que exigem dados PowerPivot, como Serviços do Excel e PowerPivot para SharePoint, devem usar uma versão posterior do provedor de dados.  
  
 Os servidores que executam o PowerPivot para SharePoint obtêm o provedor de dados OLE DB atualizado automaticamente. Outros servidores, como os que executam uma instância autônoma dos Serviços do Excel sem o PowerPivot para SharePoint no mesmo computador, devem ser reparados para usar as bibliotecas de cliente mais recentes. Para obter mais informações, consulte [Instalar o Provedor OLE DB do Analysis Services nos Servidores SharePoint](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md).  
  
 **Cenário 3: o controlador de domínio está indisponível.**  
  
 A causa pode ser um controlador de domínio que não está disponível para validar a identidade do usuário. Um controlador de domínio é exigido pelas Reivindicações ao Windows Token Service para autenticar o usuário do SharePoint em cada conexão. O Claims to Windows Token Service não usa credenciais armazenadas em cache. Valida a identidade do usuário para cada conexão.  
  
 Você pode confirmar a causa desse erro exibindo o arquivo de log do SharePoint. Se os logs do SharePoint incluírem a mensagem "Falha ao obter WindowsIdentity de IClaimsIdentity", não foi possível autenticar a identidade do usuário.  
  
 Para solucionar este problema, una o computador ao mesmo domínio de servidor do PowerPivot ou instale um controlador de domínio em seu computador local. A segunda solução, instalar o controlador de domínio, exigirá que você crie contas de domínio locais para todos os serviços e usuários. Você precisará configurar contas de serviço e permissões do SharePoint para as contas que definir.  
  
 Instale um controlador de domínio em seu computador será útil se o seu objetivo for usar o PowerPivot para SharePoint no estado offline. Para obter instruções detalhadas sobre como usar o PowerPivot offline, consulte a entrada de blog "Fazendo o seu servidor PowerPivot fora da rede" [ http://www.powerpivotgeek.com ](http://go.microsoft.com/fwlink/?LinkId=184241).  
  
 **Cenário 4: servidor instável**  
  
 Um ou mais serviços podem estar em um estado inconsistente. Em alguns casos, executar IISRESET resolverá o problema.  
  
  
