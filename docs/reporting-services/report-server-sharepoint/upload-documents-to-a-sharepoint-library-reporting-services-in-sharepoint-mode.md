---
title: Carregar documentos em uma biblioteca do SharePoint (Reporting Services no modo do SharePoint) | Microsoft Docs
ms.custom: 
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-server-sharepoint
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 955bdb159350ead0def109cb7909121a018dbd85
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode"></a>Carregar documentos em uma biblioteca do SharePoint (Reporting Services no modo do SharePoint)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Você pode carregar definições de relatório e modelos de relatório em uma biblioteca do SharePoint. Ao carregar um item de servidor de relatório, selecione uma biblioteca ou uma pasta em uma biblioteca. Não é possível carregar um item de servidor de relatório em uma lista ou página.  

> [!NOTE]
> A integração do Reporting Services ao SharePoint não está mais disponível após o SQL Server 2016.

 Você não pode carregar um arquivo de fonte de dados (.rds). No entanto, é possível publicar arquivos .rds de uma ferramenta de design, como Designer de Relatórios, em uma biblioteca do SharePoint. Durante a publicação, um novo arquivo .rsds é criado a partir do arquivo .rds original na solução. Também é possível criar um novo arquivo .rsds em uma biblioteca do SharePoint e, em seguida, definir propriedades de conexão de fonte de dados nos relatórios e modelos carregados para usar a nova conexão.  
  
> [!NOTE]  
>  O servidor de relatório deve ser configurado para o modo do SharePoint e a instância do produto do SharePoint deve ter o Suplemento Reporting Services que fornece arquivos de programa para armazenar e acessar itens do servidor de relatório em um site do SharePoint.  
  
 Para carregar um documento em uma biblioteca, você deve ter a permissão “Adicionar Itens” no nível do site. Se estiver usando as configurações de segurança padrão, essa permissão será concedida a membros do grupo **Proprietários** que tenham o nível de permissão Controle Total e do grupo **Membros** que tenham o nível de permissão Colaborar.  
  
## <a name="add-a-report-definition-or-report-model-to-a-library"></a>Adicionar uma definição de relatório ou um modelo de relatório a uma biblioteca
  
1.  Abra a biblioteca ou uma pasta de uma biblioteca. Se a biblioteca ainda não estiver aberta, clique no seu nome no Início Rápido. Se o nome da biblioteca não for exibido, clique em **Exibir Todo o Conteúdo do Site**e, em seguida, clique no nome da biblioteca.  
  
2.  No menu **Carregar** , clique em **Carregar documento**.  
  
3.  Para carregar um único arquivo de relatório ou modelo de relatório, selecione um arquivo de definição de relatório (.rdl) ou modelo de relatório (.smdl) e clique em **OK**.  
  
     Se a definição do relatório usar um arquivo de fonte de dados compartilhada (.rsds) para armazenar informações de conexão em uma fonte de dados externa, atualize os arquivos .rds e .rsds ao mesmo tempo. Para fazer isso, clique em **Carregar Vários Documentos**, especifique os dois arquivos e, em seguida, clique em **OK**.  
  
 Se você carregar um relatório que contém referências a fontes de dados compartilhadas, modelos de relatório ou sub-relatórios, as referências serão rompidas no relatório quando os arquivos forem carregados. Para obter mais informações sobre como redefinir as referências, consulte [Criar e gerenciar fontes de dados compartilhadas &#40;Reporting Services no modo integrado do SharePoint&#41;](http://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76).  
  
 Ao ser carregado, o relatório é executado sob demanda quando aberto, recuperando dados ao vivo da fonte de dados. Você pode configurar o relatório para recuperar dados em uma agenda ou usar dados armazenados em cache. Para obter mais informações, consulte [Definir opções de processamento &#40;Reporting Services no modo integrado do SharePoint&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md).  
  
 Um relatório pode conter parâmetros de forma que usuários podem filtrar dados. Você pode configurar os parâmetros para usar valores específicos ou alterar como eles aparecem ao usuário. Para obter mais informações, consulte [Definir parâmetros em um relatório publicado &#40;Reporting Services no modo integrado do SharePoint&#41;](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md).  
  
## <a name="see-also"></a>Consulte também

 [Publicar um relatório em uma biblioteca do SharePoint](../../reporting-services/reports/publish-a-report-to-a-sharepoint-library.md)   
 [Publicar uma fonte de dados compartilhada em uma biblioteca do SharePoint](../../reporting-services/reports/publish-a-shared-data-source-to-a-sharepoint-library.md)   
 [Conceder permissões para itens do servidor de relatório em um site do SharePoint](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
