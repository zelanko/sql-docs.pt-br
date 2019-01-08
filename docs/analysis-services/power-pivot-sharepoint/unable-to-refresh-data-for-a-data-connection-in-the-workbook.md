---
title: Não é possível atualizar os dados para uma conexão de dados na pasta de trabalho | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a5db5706af88a657b213e85d97777abe3ef4f744
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53203135"
---
# <a name="unable-to-refresh-data-for-a-data-connection-in-the-workbook"></a>Não é possível atualizar dados de uma conexão de dados na pasta de trabalho
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Para pastas de trabalho do Excel contendo dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , os serviços do Excel retornam este erro quando enviam uma solicitação de conexão a um servidor do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e a solicitação falha.  
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Aplica-se a:|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint|  
|Versão do Produto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|Veja abaixo.|  
|Texto da mensagem|Não é possível atualizar dados de uma conexão de dados na pasta de trabalho. Tente outra vez ou entre em contato com o administrador do sistema. As conexões a seguir não foram atualizadas: [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Dados|  
  
## <a name="explanation-and-resolution"></a>Explicação e resolução  
 Os serviços do Excel não podem se conectar ou carregar dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . As condições que causam esse erro incluem:  
  
 **Cenário 1: Serviço não foi iniciado**  
  
 O SQL Server Analysis Services ( [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]) instância não foi iniciada. Uma senha expirada interromperá a execução do serviço. Para obter mais informações sobre como alterar a senha, consulte [Configurar contas de serviço Power Pivot](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md) e [Iniciar ou parar um Power Pivot para SharePoint Server](../../analysis-services/power-pivot-sharepoint/start-or-stop-a-power-pivot-for-sharepoint-server.md).  
  
 **Cenário 2a: Abrindo uma versão anterior pasta de trabalho do servidor**  
  
 A pasta de trabalho que você está tentando abrir pode ter sido criada na versão SQL Server 2008 R2 do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para Excel. Muito provavelmente, o provedor de dados do Analysis Services especificado na cadeia de conexão de dados não está presente no computador que está executando a solicitação.  
  
 Se esse for o caso, você encontrará esta mensagem no log ULS: "Falha na atualização para ' [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]t dados ' na pasta de trabalho '\<URL para a pasta de trabalho >'", seguido por "Não é possível obter uma conexão".  
  
 Para determinar a versão da pasta de trabalho, abra-a no Excel e verifique o provedor de dados que está especificado na cadeia de conexão. Uma pasta de trabalho do SQL Server 2008 R2 usa MSOLAP.4 como provedor de dados.  
  
 Para resolver esse problema, você pode atualizar a pasta de trabalho. Opcionalmente, você pode instalar bibliotecas de cliente da versão do SQL Server 2008 R2 do Analysis Services nos computadores físicos executando o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint ou os serviços do Excel. Consulte: [Instalar o provedor OLE DB do Analysis Services em servidores do SharePoint](http://msdn.microsoft.com/2c62daf9-1f2d-4508-a497-af62360ee859).  
  
 **Cenário 2b: Os serviços do Excel está em execução em um servidor de aplicativo que tem a versão incorreta das bibliotecas de cliente**  
  
 Por padrão, o SharePoint Server 2010 instala a versão SQL Server 2008 do provedor OLE DB do Analysis Services em servidores de aplicativos que executam Serviços do Excel. Em um farm com suporte para o acesso a dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , todos os servidores físicos executando aplicativos que exigem dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , como os serviços do Excel e do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, deverão usar uma versão posterior do provedor de dados.  
  
 Os servidores que executam o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint obtêm o provedor de dados OLE DB atualizado automaticamente. Outros servidores, como os que executam uma instância autônoma dos Serviços do Excel sem o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint no mesmo computador, devem ser reparados para usar as bibliotecas de cliente mais recentes. Para obter mais informações, consulte [Instalar o Provedor OLE DB do Analysis Services nos Servidores SharePoint](http://msdn.microsoft.com/2c62daf9-1f2d-4508-a497-af62360ee859).  
  
 **Cenário 3: Controlador de domínio não está disponível**  
  
 A causa pode ser um controlador de domínio que não está disponível para validar a identidade do usuário. Um controlador de domínio é exigido pelas Reivindicações ao Windows Token Service para autenticar o usuário do SharePoint em cada conexão. O Claims to Windows Token Service não usa credenciais armazenadas em cache. Valida a identidade do usuário para cada conexão.  
  
 Você pode confirmar a causa desse erro exibindo o arquivo de log do SharePoint. Se os logs do SharePoint incluírem a mensagem "Falha ao obter WindowsIdentity de IClaimsIdentity", não foi possível autenticar a identidade do usuário.  
  
 Para solucionar este problema, una o computador ao mesmo domínio do servidor do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ou instale um controlador de domínio em seu computador local. A segunda solução, instalar o controlador de domínio, exigirá que você crie contas de domínio locais para todos os serviços e usuários. Você precisará configurar contas de serviço e permissões do SharePoint para as contas que definir.  
  
 Instalar um controlador de domínio em seu computador é útil se o seu objetivo for usar o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint no estado offline. Para obter instruções detalhadas sobre como usar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] offline, consulte a entrada de blog "levando seus [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] server fora da rede" no [ http://www.powerpivotgeek.com ](http://go.microsoft.com/fwlink/?LinkId=184241).  
  
 **Cenário 4: Servidor instável**  
  
 Um ou mais serviços podem estar em um estado inconsistente. Em alguns casos, executar IISRESET resolverá o problema.  
  
  
