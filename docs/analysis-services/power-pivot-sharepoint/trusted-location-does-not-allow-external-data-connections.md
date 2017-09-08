---
title: "Confiável local não permite conexões de dados externas | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: dc0cedfd-a7d0-40ef-bdd6-ea508130640a
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0f774f6bc9a4d950d8f7c00e3c3e79aa3211e4cf
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="trusted-location-does-not-allow-external-data-connections"></a>Local confiável não permite conexões de dados externas
  Para pastas de trabalho do Excel que contenham dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , os Serviços do Excel retornarão este erro se não puderem se conectar a fontes de dados inseridas.  
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Aplica-se a|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint|  
|Versão do Produto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|Os Serviços do Excel são configurados para negar acesso a dados externos.|  
|Texto da mensagem|O local confiável em que a pasta de trabalho é armazenada não permite conexões de dados externas. As conexões a seguir não foram atualizadas: dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]|  
  
## <a name="explanation"></a>Explicação  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] As pastas de trabalho contêm conexões de dados inseridas. Para dar suporte à interação de pastas de trabalho por slicers e filtros, os Serviços do Excel devem ser configurados para permitir acesso a dados externos por informações de conexão inseridas. O acesso a dados externos é necessário para recuperar dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] carregados em servidores [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no farm.  
  
## <a name="user-action"></a>Ação do usuário  
 Altere as definições de configuração para permitir fontes de dados inseridas.  
  
1.  Na Administração Central, em Gerenciamento de Aplicativo, clique em **Gerenciar aplicativos de serviço**.  
  
2.  Clique em **Aplicativo dos Serviços do Excel**.  
  
3.  Clique em **Local de Arquivo Confiável**.  
  
4.  Clique em **http://** ou no local que você deseja configurar.  
  
5.  Em Dados Externos, em Permitir Dados Externos, clique em **Bibliotecas de conexões de dados confiáveis e incorporadas**.  
  
6.  Clique em **OK**.  
  
 Como alternativa, você pode criar um novo local confiável para sites que contenham pastas de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e, em seguida, modificar as definições de configuração apenas para esse site. Para obter mais informações, consulte [Create a trusted location for Power Pivot sites in Central Administration](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md).  
  
  
