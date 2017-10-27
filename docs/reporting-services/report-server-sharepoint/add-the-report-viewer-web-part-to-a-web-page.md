---
title: "Adicionar a web part do Visualizador de relatórios para uma página da web | Microsoft Docs"
ms.custom: 
ms.date: 10/05/2017
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
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: 26080938c9849d6021f30d970ab2262f405df00c
ms.contentlocale: pt-br
ms.lasthandoff: 10/06/2017

---
# <a name="add-the-report-viewer-web-part-to-a-web-page"></a>Adicionar a web part do Visualizador de relatórios para uma página da web

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Você pode usar a web part do Visualizador de relatórios para exibir relatórios executados no servidor de relatório está configurado ser executado no SharePoint modo integrado. Você pode usar a web part para exibir os arquivos de definição (. RDL) do relatório que você criou no construtor de relatórios ou Designer de relatórios e carregados em uma biblioteca.

Você pode adicionar a web part do Visualizador de relatórios para uma página da web, se você quiser inserir um relatório nessa página.

> [!NOTE]
> Este artigo é específico para a web part do Visualizador de relatórios fornecido com o suplemento Reporting Services para produtos do SharePoint. Integração do Reporting Services com o SharePoint não está mais disponível após o SQL Server 2016.

Para adicionar uma web part a uma página da web, você deve ter a permissão Adicionar e personalizar páginas no nível do site. Se você estiver usando as configurações de segurança padrão, essa permissão será concedida a membros do grupo **Proprietários** que tenham nível de permissão Controle Total.

## <a name="to-embed-a-report-in-a-web-page"></a>Para inserir um relatório em uma página da web

1.  Abra ou crie a página de web part ou um painel.  
  
2.  Em **Ações do Site**, clique em **Editar Página**.  
  
3.  Clique em **adicionar uma web part**.  
  
4.  Na lista de categorias de web part, selecione a categoria **Diversas** e depois selecione **Visualizador de Relatórios do SQL Server Reporting Services**.  
  
5.  Clique em **Adicionar**. A web part será adicionada na parte superior da zona. Você pode arrastá-la para um local diferente na zona.  
  
6.  No visualizador, clique em **Clique aqui abrir o painel de ferramentas**.  
  
7.  Selecione um relatório de qualquer biblioteca na coleção de sites atuais clicando no botão Procurar (**...**). Você também pode digitar a URL do relatório. Para determinar a URL de um relatório, clique com o botão direito do mouse no relatório e selecione **Propriedades**. Não clique na seta para baixo ao lado do relatório; a URL do relatório não está indicada na página Exibir Propriedades do item. Se você copiar e colar a URL da caixa de diálogo **Propriedades** , substitua a codificação de URL "%20" por um espaço (por exemplo, "Company%20Sales" deverá ser "Company Sales").  
  
    > [!NOTE]  
    >  Cada web part do Visualizador de relatórios contém um único relatório. É necessário que a URL seja totalmente qualificada para um relatório que está no site do SharePoint atual ou em um site no mesmo aplicativo ou farm da Web. A URL deve apontar para uma biblioteca de documentos ou para uma pasta em uma biblioteca de documentos que contenha o relatório. A URL do relatório deve incluir a extensão de arquivo .rdl. Se o relatório depender de um arquivo de fonte de dados compartilhados ou de modelo, não será necessário especificar esses arquivos na URL. O relatório contém referências aos arquivos necessários.  
  
8.  Enquanto o painel de ferramentas estiver aberto, você poderá definir propriedades para modificar a aparência e o layout padrão.  
  
9. Clique em **Aplicar** na parte inferior do painel de ferramentas e clique em **OK** para fechar esse painel.  
  
## <a name="see-also"></a>Consulte também

 [Web part do Visualizador de relatórios em um Site do SharePoint](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
 [Personalizar a web part do Visualizador de relatórios](../../reporting-services/report-server-sharepoint/customize-the-report-viewer-web-part.md)   
 [Concedendo permissões para itens do servidor de relatório em um site do SharePoint](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [Instalar ou desinstalar o suplemento Reporting Services para SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  

