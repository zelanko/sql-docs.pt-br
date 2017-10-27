---
title: "Procurar partes de relatório e definir uma pasta padrão (construtor de relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5cf38068-65d1-4fe8-81f3-a404d8fbc663
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 645e20dbc98f831a778df0397b42eea096b71dfd
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs"></a>Procurar partes de relatório e definir uma pasta padrão (Construtor de Relatórios e SSRS)
O modo mais fácil de criar um relatório paginado do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é adicionar partes de relatório existentes, como tabelas e gráficos, ao relatório por meio da Galeria de Partes de Relatório. Quando você adiciona uma parte de relatório a seu relatório, também está adicionando tudo que ele deve ter para funcionar. Por exemplo, qualquer parte de relatório que exiba dados depende de um conjunto de dados, ou seja, uma consulta e uma conexão com uma fonte de dados. Depois que você adicionar a parte de relatório a seu relatório, poderá modificá-la tanto quanto necessário.  
  
 Você pode definir uma pasta padrão para publicar partes de relatório no servidor de relatório ou no site do SharePoint integrado a um servidor de relatório.  
  
 Para obter mais informações, consulte [Report Parts &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md).  
  
## <a name="to-browse-for-report-parts"></a>Para procurar partes de relatório  
  
1.  No menu **Inserir** , clique em **Partes de Relatório**.  
  
     Se você ainda não estiver conectado, clique em **Conectar a um servidor de relatório**e insira o nome.  
  
    > [!NOTE]  
    >  Você deve estar conectado a um servidor de relatório para procurar partes de relatório.  
  
2.  Agora você pode restringir sua pesquisa especificando detalhes sobre a parte de relatório. Digite o nome (ou parte dele) e a descrição na caixa **Pesquisar** ou clique em **Adicionar Critérios** e adicione valores a qualquer um destes campos:  
  
    -   Criado por  
  
    -   Data de criação  
  
    -   Data da última modificação  
  
    -   Última modificação feita por  
  
    -   Pasta do servidor  
  
    -   Tipo  
  
     Por exemplo, para localizar uma imagem, clique em **Adicionar Critérios**e em **Tipo**. Na caixa suspensa, marque a caixa de seleção **Imagem** , pressione ENTER e clique na lupa Pesquisar.  
  
    > [!NOTE]  
    >  Para os valores **Criado por** e **Última modificação** , é necessário procurar o nome de usuário da pessoa, conforme representado no servidor de relatório.  
  
## <a name="to-set-a-default-folder-for-report-parts"></a>Para definir uma pasta padrão para partes de relatório  
  
1.  Clique em **Construtor de Relatórios**e em **Opções**.  
  
2.  Na caixa de diálogo **Opções** , na guia **Configurações** , digite um nome de pasta na caixa de texto **Publicar partes de relatório nesta pasta por padrão** .  
  
 O Construtor de Relatórios criará essa pasta se você tiver permissões para criar pastas no servidor de relatório e se a pasta ainda não existir.  
  
 Você não precisa reiniciar o Construtor de Relatórios para que essa configuração tenha efeito.  
  
## <a name="see-also"></a>Consulte também  
 [Verificar ou desativar atualizações (Construtor de Relatórios e SSRS)](http://msdn.microsoft.com/en-us/9c69792d-d7c4-453b-ae2f-6d2d071d8606)   
 [Partes de relatório &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)   
 [Partes de relatório e conjuntos de dados no construtor de relatórios](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md)   
 [Solução de problemas de partes de relatório (Construtor de Relatórios e SSRS)](http://msdn.microsoft.com/en-us/d9fe1932-46e7-421b-a8a9-4c54d9576e94)   
 [Publicar e republicar partes de relatório &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/publish-and-republish-report-parts-report-builder-and-ssrs.md)  
  
  

