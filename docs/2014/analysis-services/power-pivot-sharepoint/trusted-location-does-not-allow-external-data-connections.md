---
title: 'O local confiável em que a pasta de trabalho é armazenada não permite conexões de dados externas. As seguintes conexões não foram atualizadas: dados PowerPivot | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: dc0cedfd-a7d0-40ef-bdd6-ea508130640a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 70fa82ad94ed82c7cfbf809556bfde72edb90da6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48126396"
---
# <a name="the-trusted-location-where-the-workbook-is-stored-does-not-allow-external-data-connections-the-following-connections-failed-to-refresh-powerpivot-data"></a>O local confiável em que a pasta de trabalho é armazenada não permite conexões de dados externas. As seguintes conexões não foram atualizadas: Dados PowerPivot
  Para pastas de trabalho do Excel que contenham dados PowerPivot, os Serviços do Excel retornarão este erro se não for possível conectar a fontes de dados inseridas.  
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Aplica-se a|PowerPivot para SharePoint|  
|Versão do Produto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|Os Serviços do Excel são configurados para negar acesso a dados externos.|  
|Texto da mensagem|O local confiável em que a pasta de trabalho é armazenada não permite conexões de dados externas. As seguintes conexões não foram atualizadas: Dados PowerPivot|  
  
## <a name="explanation"></a>Explicação  
 As pastas de trabalho PowerPivot contêm conexões de dados inseridas. Para dar suporte à interação de pastas de trabalho por slicers e filtros, os Serviços do Excel devem ser configurados para permitir acesso a dados externos por informações de conexão inseridas. O acesso a dados externos é necessário para recuperar dados PowerPivot carregados em servidores PowerPivot no farm.  
  
## <a name="user-action"></a>Ação do usuário  
 Altere as definições de configuração para permitir fontes de dados inseridas.  
  
1.  Na Administração Central, em Gerenciamento de Aplicativo, clique em **Gerenciar aplicativos de serviço**.  
  
2.  Clique em **Aplicativo dos Serviços do Excel**.  
  
3.  Clique em **Local de Arquivo Confiável**.  
  
4.  Clique em **http://** ou no local que você deseja configurar.  
  
5.  Em Dados Externos, em Permitir Dados Externos, clique em **Bibliotecas de conexões de dados confiáveis e incorporadas**.  
  
6.  Clique em **OK**.  
  
 Também é possível criar um novo local confiável para sites que contenham pastas de trabalho PowerPivot e, em seguida, modificar os parâmetros de configuração apenas para esse site. Para obter mais informações, consulte [Create a trusted location for PowerPivot sites in Central Administration](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md).  
  
  
