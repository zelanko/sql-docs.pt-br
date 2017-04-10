---
title: "O caminho de conex&#227;o de dados na pasta de trabalho aponta para um arquivo na unidade local ou &#233; um URI inv&#225;lido. As seguintes conex&#245;es n&#227;o foram atualizadas: dados do Power Pivot | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: bd22e41a-0931-4d32-888a-633a3046fc5e
caps.latest.revision: 7
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# O caminho de conex&#227;o de dados na pasta de trabalho aponta para um arquivo na unidade local ou &#233; um URI inv&#225;lido. As seguintes conex&#245;es n&#227;o foram atualizadas: dados do Power Pivot
  Para pastas de trabalho do Excel que contenham dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], os Serviços do Excel retornarão este erro se não puderem se conectar a fontes de dados inseridas.  
  
## Detalhes  
  
|||  
|-|-|  
|Aplica-se a|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint|  
|Versão do Produto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|Os Serviços do Excel são configurados para permitir somente conexões de dados de arquivos .odc arquivos que estejam em uma biblioteca de conexões de dados confiável.|  
|Texto da mensagem|O caminho de conexão de dados na pasta de trabalho aponta para um arquivo na unidade local ou é um URI inválido. As conexões a seguir não foram atualizadas: dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]|  
  
## Explicação  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] As pastas de trabalho contêm conexões de dados inseridas. Para dar suporte à interação de pastas de trabalho por slicers e filtros, os Serviços do Excel devem ser configurados para permitir acesso a dados externos por informações de conexão inseridas. O acesso a dados externos é necessário para recuperar dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] carregados em servidores [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no farm.  
  
## Ação do usuário  
 Altere as definições de configuração para permitir conexões de fontes de dados inseridas.  
  
1.  Na Administração Central, em Gerenciamento de Aplicativo, clique em **Gerenciar aplicativos de serviço**.  
  
2.  Clique em **Aplicativo dos Serviços do Excel**.  
  
3.  Clique em **Local de Arquivo Confiável**.  
  
4.  Clique em **http://** ou no local que você deseja configurar.  
  
5.  Em Dados Externos, em Permitir Dados Externos, clique em **Bibliotecas de conexões de dados confiáveis e incorporadas**.  
  
6.  Clique em **OK**.  
  
 Como alternativa, você pode criar um novo local confiável para sites que contenham pastas de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e, em seguida, modificar as definições de configuração apenas para esse site. Para obter mais informações, consulte [Create a trusted location for Power Pivot sites in Central Administration](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md).  
  
  