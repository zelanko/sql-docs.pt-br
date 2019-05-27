---
title: Esta pasta de trabalho contém uma ou mais consultas que atualizam dados externos. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: aa65c992-eb41-4032-9e11-a9ba871b6a3c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 925821cba91a8a62076f0dcfa327453d035671d9
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66070964"
---
# <a name="this-workbook-contains-one-or-more-queries-that-refresh-external-data"></a>Esta pasta de trabalho contém uma ou mais consultas que atualizam dados externos.
  Para pastas de trabalho do Excel que contêm dados PowerPivot, os Serviços do Excel mostram este aviso quando detectam informações de conexão e solicitam que você habilite ou desabilite consultas para essa pasta de trabalho.  
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|PowerPivot para SharePoint|  
|Versão do Produto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|Os Serviços do Excel são configurados para avisar na atualização de dados.|  
|Texto da mensagem|Esta pasta de trabalho contém uma ou mais consultas que atualizam dados externos. Um usuário mal-intencionado pode criar uma consulta para acessar informações confidenciais e distribuí-las a outros usuários ou pode executar outras ações prejudiciais.<br /><br /> Se você confiar na origem dessa pasta de trabalho, clique em Sim para habilitar consultas a dados externos nessa pasta de trabalho. Se você não tiver certeza, clique em Não para que as alterações não sejam aplicados em sua pasta de trabalho.<br /><br /> Você deseja habilitar consultas a dados externos nesta pasta de trabalho?|  
  
## <a name="explanation"></a>Explicação  
 As pastas de trabalho PowerPivot contêm cadeias de conexão de dados incorporadas usadas pelo Excel para se comunicar com um servidor PowerPivot externo que carrega e calcula os dados. Quando o aviso na atualização de dados estiver habilitado, o Serviços do Excel detectará essa cadeia de conexão e avisará o usuário.  
  
 Para filtrar e dividir dados PowerPivot na pasta de trabalho, as consultas devem ser habilitadas. Certifique-se de habilitar consultas apenas para as pastas de trabalho PowerPivot nas que você confia.  
  
## <a name="user-action"></a>Ação do usuário  
 Clique em **Sim** para habilitar consultas.  
  
 Você também pode alterar os parâmetros de configuração para que o aviso na atualização não ocorra mais:  
  
1.  Na Administração Central, em Gerenciamento de Aplicativo, clique em **Gerenciar aplicativos de serviço**.  
  
2.  Clique em **Aplicativo dos Serviços do Excel**.  
  
3.  Clique em **Local de Arquivo Confiável**.  
  
4.  Clique em **http://** ou no local que você deseja configurar.  
  
5.  Em Dados Externos, desmarque a caixa de seleção para **Avisar na atualização de dados**.  
  
6.  Clique em **OK**.  
  
 Também é possível criar um novo local confiável para sites que contenham pastas de trabalho PowerPivot e, em seguida, modificar os parâmetros de configuração apenas para esse site. Para obter mais informações, consulte [criar um local confiável para sites do PowerPivot na Administração Central](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md).  
  
  
