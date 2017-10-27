---
title: "Adicionar a web part do Visualizador de relatórios do SQL Server Reporting Services a uma página do SharePoint | Microsoft Docs"
ms.custom: Display a report, from SQL Server Reporting Services or Power BI Report Server, by adding a Report Viewer web part to a SharePoint page.
ms.date: 09/26/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: fbc68b6ff9f1edf5cf6ee13f6e93a3d2d1a8f834
ms.contentlocale: pt-br
ms.lasthandoff: 10/06/2017

---

# <a name="add-sql-server-reporting-services-report-viewer-web-part-to-a-sharepoint-page"></a>Adicionar a web part do Visualizador de relatórios do SQL Server Reporting Services a uma página do SharePoint

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

Exiba um relatório, do SQL Server Reporting Services ou o servidor de relatório do Power BI, adicionando uma web part do Visualizador de relatórios para uma página do SharePoint.

![Web part do Visualizador de relatórios em uma página do SharePoint](media/sharepoint-report-viewer-web-part-on-page.png)

## <a name="prerequisites"></a>Pré-requisitos

* Para relatórios carregar com êxito, o Claims to Windows Token Service (C2WTS) deve ser definida para o Kerberos a delegação restrita. Para obter mais informações sobre como configurar o C2WTS, consulte [Claims to Windows Token Service (C2WTS) e Reporting Services](../install-windows/claims-to-windows-token-service-c2wts-and-reporting-services.md).

* A web part do Visualizador de relatórios deve ser implantada em seu farm do SharePoint. Para obter informações sobre como implantar o projeto de solução da web part Visualizador de relatórios, consulte [implantar a web part do Visualizador de relatórios em um site do SharePoint](deploy-report-viewer-web-part.md).

* Para adicionar uma web part a uma página da web, você deve ter a permissão Adicionar e personalizar páginas no nível do site. Se você estiver usando as configurações de segurança padrão, essa permissão será concedida a membros do grupo **Proprietários** que tenham nível de permissão Controle Total.

## <a name="add-web-part"></a>Adicionar web part

1. No site do SharePoint, selecione o **engrenagem** ícone no canto superior esquerdo e selecione **adicionar uma página**.

    ![Adicione uma página a um site do sharepoint do ícone de engrenagem.](media/sharepoint-add-a-page.png)

2. Dê um nome e selecione à sua página **criar**.

3. No designer de página, selecione o **inserir** guia na faixa de opções. Em seguida, selecione **da web part** dentro de **partes** seção.

    ![Inserir uma web part na faixa de opções do office.](media/sharepoint-insert-web-part.png)

4. Em **categorias**, selecione * * SQL Server Reporting Services (modo nativo). Em **partes**, selecione **Visualizador de relatórios**. Em seguida, selecione **adicionar**.

    ![Adicione a web part do Visualizador de relatórios.](media/sharepoint-report-viewer-web-part.png)

    Inicialmente, isso pode parecer com um erro. O erro ocorre porque a URL do servidor de relatório padrão é definida como *http://localhost* e pode não estar disponível neste local.

## <a name="configure-the-report-viewer-web-part"></a>Configurar a web part do Visualizador de relatórios

Para configurar a web part para apontar para o relatório específico, faça o seguinte:

1. Ao editar a página do SharePoint, selecione a seta para baixo no canto superior direito da web part e selecione **Editar web part**.

    ![Editar página de web de web part da lista suspensa.](media/sharepoint-edit-web-part.png)

2. Insira o **URL do servidor de relatório** para o servidor de relatório que hospeda seu relatório. Isso deve ser semelhante ao *http://myrsserver/reportserver*.

3. Insira o caminho e o nome do relatório que você deseja exibir na web part. Isso será semelhante ao *AdventureWorks exemplo relatórios/vendas da empresa*. Neste exemplo, o relatório *vendas da empresa* em uma pasta chamada *relatórios de exemplo AdventureWorks*.

4. Se o relatório exigir parâmetros, depois que você forneceu a URL do servidor de relatório e o nome do relatório, selecione **carregar parâmetros** dentro de **parâmetros** seção.

5. Selecione **Okey** para salvar suas alterações na configuração de web part.

6. Selecione **salvar**, na faixa de opções da Office, para salvar as alterações para a página do SharePoint.

![Web part do Visualizador de relatórios em uma página do SharePoint](media/sharepoint-report-viewer-web-part-on-page.png)

## <a name="considerations-and-limitations"></a>Considerações e limitações

* A web part do Visualizador de relatórios não pode ser usada em páginas modernas no SharePoint.
* Relatórios do Power BI não podem ser usados com a web part do Visualizador de relatórios.
* Se você não vir o relatório web part do visualizador, para adicionar a uma página, verifique se você tem [implantado a web part do Visualizador de relatórios](deploy-report-viewer-web-part.md).

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)

