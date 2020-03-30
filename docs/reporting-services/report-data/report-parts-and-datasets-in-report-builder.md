---
title: Partes de relatório e conjuntos de dados no Construtor de Relatórios | Microsoft Docs
ms.date: 09/16/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: 1fe86481-9c41-4535-a4b7-c7c4d780cab6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a06344a119dfba635a07d0050a61f561065a2984
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "65571193"
---
# <a name="report-parts-and-datasets-in-report-builder"></a>Partes de relatório e conjuntos de dados no Construtor de Relatórios
  No Construtor de Relatórios, a maneira mais fácil de incluir dados em um relatório é adicionando partes de relatório da Galeria de Partes de Relatório. As partes de relatório contêm os conjuntos de dados dos quais dependem, conhecidos como *conjuntos de dados dependentes*. Os conjuntos de dados dependentes se baseiam em fontes de dados compartilhadas e podem ser conjuntos de dados inseridos ou compartilhados. Leia mais sobre as [Partes do relatório](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md).  
  
 Outra forma simples de incluir dados em um relatório é usando um conjunto de dados compartilhado. Para obter mais informações, consulte [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="adding-a-report-part-with-dependent-datasets-to-your-report"></a><a name="Adding"></a> Adicionando uma parte de relatório com conjuntos de dados dependentes ao seu relatório  
 Quando você adiciona uma parte de relatório a seu relatório, os conjuntos de dados dependentes que ela contém também são adicionados ao seu relatório. Como uma parte de relatório pode incluir um retângulo que contém muitos outros itens de relatório, ela pode adicionar vários conjuntos de dados dependentes ao relatório. Cada conjunto de dados compartilhado é uma referência independente; a fonte de dados compartilhada do qual ele depende não é adicionada ao relatório. Cada conjunto de dados inserido também adiciona a fonte de dados inserida ou compartilhada do qual depende.  
  
 As credenciais de uma fonte de dados inserida não são salvas como parte da parte de relatório. Se uma fonte de dados inserida for adicionada ao relatório, você receberá uma solicitação para fornecer credenciais quando executar o relatório. Para não receber essa solicitação de credenciais, use partes de relatório que se baseiem em fontes de dados compartilhadas com credenciais armazenadas.  
  
 Após a adição de uma parte de relatório ao relatório, os conjuntos de dados adicionados não serão diferentes dos conjuntos de dados inseridos ou compartilhados criados por você. Você pode exibir conjuntos de dados adicionais no painel de Dados do Relatório. Os conjuntos de dados inseridos aparecem sob a fonte de dados compartilhada correspondente e os conjuntos de dados compartilhados aparecem sob a pasta Conjuntos de Dados Compartilhados.  
  
##  <a name="customizing-dependent-datasets"></a><a name="Customizing"></a> Personalizando conjuntos de dados dependentes  
 Depois que você adicionar partes de relatório ao relatório, poderá visualizá-lo e decidir fazer algumas alterações aos dados. Os itens que poderão ser alterados dependerão do tipo de conjunto de dados com os quais você estiver trabalhando.  
  
 Para alterar dados e opções de dados de um conjunto de dados inserido, você pode editar as propriedades do conjunto de dados, incluindo a consulta, como se você tivesse criado o próprio conjunto de dados.  
  
 Para alterar dados e opções de dados de um conjunto de dados compartilhado, você somente poderá alterar a definição de fonte de dados compartilhada no servidor de relatório se tiver permissões suficientes. Também é possível personalizar a instância do conjunto de dados personalizado no relatório adicionando filtros, adicionando campos calculados e alterando opções de dados, como distinção entre maiúsculas e minúsculas. Para obter mais informações, consulte [Conjuntos de dados inseridos e compartilhados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/embedded-and-shared-datasets-report-builder-and-ssrs.md).  
  
 Para obter mais informações sobre como alterar a definição de um conjunto de dados compartilhado ou mostrar as últimas alterações de dados de um conjunto de dados compartilhado em seu relatório, consulte [Criar um conjunto de dados compartilhado ou um conjunto de dados inserido &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md) e [Adicionar, editar e atualizar campos no painel Dados do Relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md).  
  
##  <a name="publishing-dependent-datasets-as-shared-datasets"></a><a name="Publishing"></a> Publicando conjuntos de dados dependentes como conjuntos de dados compartilhados  
 Quando publica um item de relatório que tem conjuntos de dados dependentes, você tem a opção de publicar cada conjunto de dados como um conjunto de dados compartilhado ou inserido que permanece inserido no item de relatório.  
  
 Quando você seleciona a opção de conjunto de dados compartilhado, o conjunto de dados é salvo no servidor de relatório como uma definição de conjunto de dados compartilhado. No seu relatório, cada item de relatório que usa o conjunto de dados é atualizado para apontar para o conjunto de dados compartilhado que agora está no servidor de relatório. Isso tem duas consequências:  
  
1.  Na caixa de diálogo Publicar, cada conjunto de dados compartilhado que foi publicado é removido da lista de itens disponíveis para publicação.  
  
2.  Quando você sai do Construtor de Relatórios ou inicia um novo relatório, recebe uma solicitação para salvar o relatório. Se você não salvar o relatório, na próxima vez em que abri-lo e publicar itens de relatório, poderá publicar novas cópias dos mesmos conjuntos de dados. Para não salvar várias cópias de conjuntos de dados compartilhados no servidor de relatório, é recomendável salvar o relatório.  
  
> [!IMPORTANT]  
>  Para assegurar que você e outros usuários possam continuar usando os dados de um conjunto de dados compartilhado com êxito, é necessário entender os princípios por trás da proteção de itens de relatório. Para obter mais informações, consulte [Proteger itens de conjunto de dados compartilhados](../../reporting-services/security/secure-shared-dataset-items.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Modo de exibição de Design de relatório &#40;Construtor de Relatórios&#41;](../../reporting-services/report-builder/report-design-view-report-builder.md)   
 [Segurança &#40;Construtor de Relatórios&#41;](../../reporting-services/report-builder/security-report-builder.md)   
 [Partes de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)   
 [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
