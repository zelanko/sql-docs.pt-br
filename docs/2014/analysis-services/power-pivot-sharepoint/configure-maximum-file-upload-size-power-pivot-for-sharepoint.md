---
title: Configurar o tamanho máximo de upload de arquivo (PowerPivot para SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: ac516c63-1e79-4ae8-bca6-32d3c1a09c00
author: minewiskan
ms.author: owend
ms.openlocfilehash: d7a43ec4c52de9be2c0345e520743cc2a9fb14a7
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547549"
---
# <a name="configure-maximum-file-upload-size-powerpivot-for-sharepoint"></a>Configurar o tamanho máximo do carregamento de arquivo (PowerPivot para SharePoint)
  As pastas de trabalho PowerPivot geralmente contêm grandes quantidades de dados que resultam em arquivos que excedem o tamanho máximo de arquivo permitido para carregamentos do SharePoint. Ao tentar carregar um arquivo que excede o limite superior, você receberá o seguinte erro no SharePoint:  
  
-   "O arquivo especificado é maior que o tamanho máximo de arquivo permitido".  
  
 Para aumentar o tamanho de arquivo, inicie ajustando o Tamanho Máximo da Pasta de Trabalho para Serviços do Excel para 50 megabytes. Isso alinha os limites máximos de tamanho de arquivo para o Excel com os dos aplicativos Web do SharePoint (definidos para 50 megabytes por padrão no SharePoint 2010 e 200 no SharePoint 2013). Se seus arquivos excederem 50 megabytes em tamanho, aumente os limites de tamanho de arquivo para Serviços do Excel e para o aplicativo Web.  
  
 Você deve ser administrador do SharePoint para alterar o tamanho máximo de carregamento de arquivo.  
  
### <a name="configure-maximum-file-size-for-excel-services"></a>Configurar tamanho máximo de arquivo para Serviços do Excel  
  
1.  Na administração central, em gerenciamento de aplicativos, clique em **gerenciar aplicativos de serviço**.  
  
2.  Clique no nome do Aplicativo de Serviços do seu Excel.  
  
3.  Clique em **Locais de Arquivos Confiáveis**.  
  
4.  Clique no local para editar as propriedades. Por padrão, os Serviços do Excel consideram o aplicativo Web padrão um site de confiança. Se você estiver usando o aplicativo Web padrão, clique em **http://** abrir a página de configuração para este local.  
  
5.  Role para as **Propriedades da Pasta de Trabalho**.  
  
6.  Em Tamanho Máximo da Pasta de Trabalho, aumente o tamanho do arquivo de 10 (o valor padrão) para 50 ou um tamanho maior que acomode os arquivos em você está trabalhando.  
  
     Por padrão, 50 megabytes é o tamanho máximo de carregamento de arquivo para aplicativos Web do SharePoint. Se você definir Tamanho Máximo da Pasta de Trabalho como um número maior que 50 megabytes, siga as etapas no próximo procedimento para aumentar o Tamanho Máximo de Carregamento para o aplicativo Web do SharePoint para o mesmo valor.  
  
     O valor máximo que você pode especificar é 2 gigabytes (ou 2047 megabytes como especificado na Administração Central).  
  
7.  Clique em **OK**.  
  
### <a name="configure-maximum-file-size-for-a-sharepoint-web-application"></a>Configurar o tamanho máximo do arquivo para um aplicativo Web do SharePoint  
  
1.  Na administração central, em gerenciamento de aplicativos, clique em **gerenciar aplicativos Web**.  
  
    > [!NOTE]  
    >  Execute as etapas a seguir somente se você tiver aumentado o Tamanho Máximo da Pasta de Trabalho nos Serviços do Excel.  
  
2.  Selecione o aplicativo (por exemplo, **SharePoint - 80**).  
  
3.  Na faixa de opções de Aplicativos Web, clique na seta para baixo no botão de Configurações Gerais.  
  
4.  Clique em **configurações gerais**.  
  
5.  Role para **Tamanho Máximo do Carregamento**.  
  
6.  Defina a propriedade com o mesmo número, ou maior, que o Tamanho Máximo da Pasta de Trabalho em Serviços do Excel.  
  
7.  Clique em **OK**.  
  
  
