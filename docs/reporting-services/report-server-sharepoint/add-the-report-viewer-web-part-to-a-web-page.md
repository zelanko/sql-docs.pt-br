---
title: Adicionar a web part do Visualizador de Relatórios a uma página da Web | Microsoft Docs
ms.custom: ''
ms.date: 10/05/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-server-sharepoint
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 5d9eb107d1355a15d15c22fc3b24824cae009075
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33025163"
---
# <a name="add-the-report-viewer-web-part-to-a-web-page"></a>Adicionar a web part do Visualizador de Relatórios a uma página da Web

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

É possível usar a web part do Visualizador de Relatórios para exibir relatórios executados no servidor de relatório configurado para execução no modo integrado do SharePoint. Você pode usar a web part para exibir arquivos de definição de relatório (.rdl) criados no Construtor de Relatórios ou no Designer de Relatórios e carregados em uma biblioteca.

Você poderá adicionar a web part do Visualizador de Relatórios a uma página da Web se desejar inserir um relatório nessa página.

> [!NOTE]
> Este artigo é específico à web part do Visualizador de Relatórios fornecida com o Suplemento Reporting Services para produtos do SharePoint. A integração do Reporting Services ao SharePoint não está mais disponível após o SQL Server 2016.

Para adicionar uma web part a uma página da Web, é necessário ter a permissão Adicionar e Personalizar Páginas no nível do site. Se você estiver usando as configurações de segurança padrão, essa permissão será concedida a membros do grupo **Proprietários** que tenham nível de permissão Controle Total.

## <a name="to-embed-a-report-in-a-web-page"></a>Para inserir um relatório em uma página da Web

1.  Abra ou crie uma página ou um painel da web part.  
  
2.  Em **Ações do Site**, clique em **Editar Página**.  
  
3.  Clique em **Adicionar uma web part**.  
  
4.  Na lista de categorias de web part, selecione a categoria **Diversas** e depois selecione **Visualizador de Relatórios do SQL Server Reporting Services**.  
  
5.  Clique em **Adicionar**. A web part é adicionada à parte superior da zona. Você pode arrastá-la para um local diferente na zona.  
  
6.  No visualizador, clique em **Clique aqui abrir o painel de ferramentas**.  
  
7.  Selecione um relatório de qualquer biblioteca na coleção de sites atuais clicando no botão Procurar (**...**). Você também pode digitar a URL do relatório. Para determinar a URL de um relatório, clique com o botão direito do mouse no relatório e selecione **Propriedades**. Não clique na seta para baixo ao lado do relatório; a URL do relatório não está indicada na página Exibir Propriedades do item. Se você copiar e colar a URL da caixa de diálogo **Propriedades** , substitua a codificação de URL "%20" por um espaço (por exemplo, "Company%20Sales" deverá ser "Company Sales").  
  
    > [!NOTE]  
    >  Cada web part do Visualizador de Relatórios contém um único relatório. É necessário que a URL seja totalmente qualificada para um relatório que está no site do SharePoint atual ou em um site no mesmo aplicativo ou farm da Web. A URL deve apontar para uma biblioteca de documentos ou para uma pasta em uma biblioteca de documentos que contenha o relatório. A URL do relatório deve incluir a extensão de arquivo .rdl. Se o relatório depender de um arquivo de fonte de dados compartilhados ou de modelo, não será necessário especificar esses arquivos na URL. O relatório contém referências aos arquivos necessários.  
  
8.  Enquanto o painel de ferramentas estiver aberto, você poderá definir propriedades para modificar a aparência e o layout padrão.  
  
9. Clique em **Aplicar** na parte inferior do painel de ferramentas e clique em **OK** para fechar esse painel.  
  
## <a name="see-also"></a>Confira também

 [Web part do Visualizador de Relatórios em um Site do SharePoint](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
 [Personalizar a web part do Visualizador de Relatórios](../../reporting-services/report-server-sharepoint/customize-the-report-viewer-web-part.md)   
 [Concedendo permissões para itens do servidor de relatório em um site do SharePoint](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [Instalar ou desinstalar o suplemento Reporting Services para SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
