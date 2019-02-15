---
title: Procurar partes de relatório e definir uma pasta padrão (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 5cf38068-65d1-4fe8-81f3-a404d8fbc663
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 5af65931e67786447b29b344e341ab6abc83050c
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56295445"
---
# <a name="browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs"></a>Procurar partes de relatório e definir uma pasta padrão (Construtor de Relatórios e SSRS)
  O modo mais fácil de criar um relatório é adicionar partes de relatório existentes, como tabelas e gráficos, ao relatório a partir da Galeria de Partes de Relatório. Quando você adiciona uma parte de relatório a seu relatório, também está adicionando tudo que ele deve ter para funcionar. Por exemplo, qualquer parte de relatório que exiba dados depende de um conjunto de dados, ou seja, uma consulta e uma conexão com uma fonte de dados. Depois que você adicionar a parte de relatório a seu relatório, poderá modificá-la tanto quanto necessário.  
  
 Você pode definir uma pasta padrão para publicar partes de relatório no servidor de relatório ou no site do SharePoint integrado a um servidor de relatório.  
  
 Para obter mais informações, consulte [Partes de relatório &#40;Construtor de Relatórios e SSRS&#41;](../report-parts-report-builder-and-ssrs.md).  
  
### <a name="to-browse-for-report-parts"></a>Para procurar partes de relatório  
  
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
  
### <a name="to-set-a-default-folder-for-report-parts"></a>Para definir uma pasta padrão para partes de relatório  
  
1.  Clique em **Construtor de Relatórios**e em **Opções**.  
  
2.  Na caixa de diálogo **Opções** , na guia **Configurações** , digite um nome de pasta na caixa de texto **Publicar partes de relatório nesta pasta por padrão** .  
  
 O Construtor de Relatórios criará essa pasta se você tiver permissões para criar pastas no servidor de relatório e se a pasta ainda não existir.  
  
 Você não precisa reiniciar o Construtor de Relatórios para que essa configuração tenha efeito.  
  
## <a name="see-also"></a>Consulte também  
 [Verificar ou desativar atualizações &#40;relatórios e SSRS&#41;](../check-for-updates-or-turn-updates-off-report-builder-and-ssrs.md)   
 [Partes de relatório &#40;Construtor de Relatórios e SSRS&#41;](../report-parts-report-builder-and-ssrs.md)   
 [Partes de relatório e conjuntos de dados no Construtor de Relatórios](../report-data/report-parts-and-datasets-in-report-builder.md)   
 [Solucionar problemas de partes de relatório &#40;relatórios e SSRS&#41;](../troubleshoot-report-parts-report-builder-and-ssrs.md)   
 [Publicar e republicar partes de relatório &#40;Construtor de Relatórios e SSRS&#41;](publish-and-republish-report-parts-report-builder-and-ssrs.md)  
  
  
