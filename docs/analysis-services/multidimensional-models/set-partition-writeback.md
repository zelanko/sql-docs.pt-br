---
title: "Definir o write-back de partição | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- write-enabled partitions [Analysis Services]
- partitions [Analysis Services], writeback
- partitions [Analysis Services], write-enabled
- writeback [Analysis Services], partitions
ms.assetid: 38bb09cc-2652-4971-8373-0cf468cdc7a6
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c1e6971bd8c1bc228386ad5b39a498f0e0ed5d42
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2018
---
# <a name="set-partition-writeback"></a>Definir o write-back de partições
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Se você habilitar um grupo de medidas para gravação, os usuários finais poderão alterar dados de cubo enquanto procuram por ele. As alterações são salvas em uma tabela separada chamada tabela de write-back e não nos dados de cubo ou na fonte de dados. Os usuários finais que procuram uma partição habilitada para gravação observam o efeito líquido de todas as alterações na tabela de write-back da partição.  
  
 Os dados de write-back podem ser procurados ou excluídos. Também é possível converter os dados de write-back em uma partição. Em uma partição habilitada para gravação, é possível usar funções de cubo para conceder acesso de leitura/gravação a usuários e grupos de usuários e para limitar o acesso a células ou grupos de células específicos da partição.  
  
 Para ver uma breve introdução em vídeo sobre write-back, consulte [Write-back do Excel 2010 para Analysis Services](http://go.microsoft.com/fwlink/p/?LinkId=394951). Na série de postagens no blog [Building a Writeback Application with Analysis Services (blog)](http://go.microsoft.com/fwlink/?LinkId=394977)(Criando um aplicativo de write-back com o Analysis Services), você encontra uma apresentação mais detalhada deste recurso.  
  
> [!NOTE]  
>  Há suporte para write-back apenas em bancos de dados relacionais e data marts do SQL Server e somente para modelos multidimensionais do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
## <a name="how-to-write-enable-a-partition"></a>Como habilitar uma partição para gravação  
 Você pode habilitar os grupos de medidas de uma partição para gravação, habilitando a partição propriamente dita no Designer de Cubo, no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] , ou no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
-   No Designer de Cubo, na guia Partições, clique com o botão direito do mouse em uma partição e escolha **Configurações de Write-back**.  
  
-   No [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], expanda o banco de dados | cubo | grupo de medidas, clique com o botão direito do mouse em **Write-back** e escolha **Habilitar Write-back**.  
  
 O write-back só tem suporte para as medidas que usam a agregação SUM. No banco de dados de exemplo AdventureWorks, você pode usar o grupo de medidas Metas de Vendas para testar o comportamento do write-back.  
  
 Ao habilitar uma partição para gravação, especifique um nome de tabela e uma fonte de dados para armazenar a tabela de write-back. Qualquer alteração subsequente feita no grupo de medidas é registrada nessa tabela.  
  
## <a name="browse-writeback-data-in-a-partition"></a>Pesquisar dados de write-back em uma partição  
 É possível procurar o conteúdo da tabela de write-back de um cubo na caixa de diálogo **Procurar Dados** , que pode ser acessada ao clicar com o botão direito do mouse em uma partição habilitada para gravação na guia **Partições** do Designer de Cubo.  
  
## <a name="delete-writeback-data-or-disable-writeback"></a>Excluir dados de write-back ou desabilitar o write-back  
 A exclusão de dados de write-back limpa o cache; assim que esses dados são excluídos, trabalhos adicionais de write-back são executados em uma lista limpa. A desabilitação de write-back na partição de um cubo simplesmente desativa o write-back dessa partição.  
  
## <a name="convert-writeback-data-to-a-partition"></a>Converter dados de write-back para uma partição  
 É possível converter os dados da tabela de write-back em uma partição. Este procedimento faz com que a tabela de write-back se transforme na nova tabela de fatos da partição.  
  
> [!CAUTION]  
>  O uso incorreto de partições pode resultar em dados de cubo imprecisos. Para obter mais informações, consulte [Criar e gerenciar uma partição local #40;Analysis Services&#41;](../../analysis-services/multidimensional-models/create-and-manage-a-local-partition-analysis-services.md).  
  
 A conversão da tabela de dados de write-back em uma partição também desabilita a gravação da partição. Todas as políticas de leitura/gravação irrestrita e as permissões de leitura/gravação das células da partição são desabilitadas e os usuários finais não poderão alterar os dados de cubo exibidos. Os usuários finais com políticas de leitura/gravação irrestrita ou permissões de leitura/gravação desabilitadas ainda poderão procurar o cubo. As permissões de leitura e de contingente de leitura não são afetadas.  
  
 Para converter os dados de write-back em uma partição, use a caixa de diálogo **Converter em Partição**, que pode ser acessada ao clicar com o botão direito do mouse na tabela de write-back de uma partição habilitada para gravação no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Especifique um nome para a partição e se deseja projetar a agregação para a partição posteriormente ou no momento da criação. Para criar a agregação no mesmo momento em que a partição é escolhida, é necessário copiar o design de agregação de uma partição existente. Esta é, mas não necessariamente, a partição de write-back atual. Também é possível processar a partição durante sua criação.  
  
## <a name="see-also"></a>Consulte também  
 [Partições habilitadas para gravação](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions.md)   
 [Habilitando o write-back em um cubo OLAP no nível da célula no Excel 2010](http://go.microsoft.com/fwlink/p/?LinkId=394952)   
 [Habilitando e protegendo a entrada de dados com o write-back do Analysis Services](http://go.microsoft.com/fwlink/p/?LinkId=394953)  
  
  
