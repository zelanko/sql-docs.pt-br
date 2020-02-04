---
title: Solução de problemas de Design de Relatório com o Reporting Services | Microsoft Docs
ms.date: 02/27/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
ms.assetid: a0d103da-5a3e-475c-a71a-9e23476095e2
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b3eb298bc6b359b0df92566f9add8d7011cdc907
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "65573851"
---
# <a name="troubleshoot-report-design-issues-with-reporting-services"></a>Solucionar problemas de Design de Relatório com o Reporting Services
Os problemas de design de relatórios podem ocorrer quando você cria o layout do relatório na exibição Design em um aplicativo de criação de relatório. Use este tópico para ajudar a solucionar esses problemas.   
  
## <a name="why-does-my-text-box-show-only-a-single-value-and-not-repeat-for-every-row"></a>Por que minha caixa de texto mostra apenas um único valor e não se repete a cada linha?  
Uma caixa de texto com uma referência de campo de conjunto de dados é renderizada apenas uma vez e exibe o primeiro valor no conjunto de dados.   
  
**A caixa de texto pai é o corpo do relatório**  
  
  
Uma caixa de texto adicionada diretamente à superfície de design só pode exibir um valor de agregação para um conjunto de dados.  
  
Para verificar o contêiner pai de uma caixa de texto, selecione-a e, no painel Propriedades, role até **Pai**.   
  
Se você quiser caixas de texto que mostrem cada valor em um conjunto de dados, use uma região de dados, como uma tabela ou matriz. Por padrão, cada célula de uma tabela ou matriz contém uma caixa de texto. Arraste os campos do conjunto de dados para cada célula.   
  
## <a name="why-cant-i-add-total-pages-to-my-report"></a>Por que não posso adicionar o total de páginas ao meu relatório?  
Os campos internos `[&PageNumber]` e `[&TotalPages]` não são válidos no corpo do relatório.   
  
PageNumber e TotalPages somente são válidos no cabeçalho e no rodapé da página.  
  
  
Os campos internos [&PageNumber] e [&TotalPages] somente são válidos no cabeçalho e no rodapé da página.   
  
Para adicionar [&PageNumber] ou [&TotalPages] a um relatório, primeiro você deve adicionar um cabeçalho ou rodapé de página. Para obter mais informações, consulte [Adicionar ou remover um cabeçalho de página](../../reporting-services/report-design/add-or-remove-a-page-header-or-footer-report-builder-and-ssrs.md).  
  
> [!NOTE]  
> A inclusão de [&TotalPages] no cabeçalho ou rodapé da página pode ter consequências para o processamento de um relatório. Para obter mais informações, consulte Solucionando problemas de relatório: relatórios exportados para um formato de arquivo específico.  
[Processamento de solução de problemas dos relatórios do Reporting Services](../../reporting-services/troubleshooting/troubleshoot-processing-of-reporting-services-reports.md).  
  
## <a name="how-do-i-design-two-tables-or-a-chart-and-a-table-to-display-side-by-side"></a>Como faço para criar duas tabelas ou um gráfico e uma tabela para exibição lado a lado?  
A criação de um relatório não é uma experiência objetiva. O processador do relatório combina dados, itens de relatório, informações de layout, como um espaço em branco, contêineres e expressões para produzir um relatório compilado que é passado a um renderizador que estabelece seu layout, para a experiência de exibição especificada: interativa para um navegador HTML ou como um formato de arquivo. Os algoritmos de layout automáticos podem produzir um layout de relatório que você deseja alterar.   
  
### <a name="rendering-rules-use-page-size-containers-peer-objects-relative-placement-and-white-space-to-determine-layout"></a>As regras de renderização usam tamanho de página, contêineres, objetos pares, posicionamento relativo e espaço em branco para determinar o layout  
Em geral, um relatório aumenta para conter seus dados e descarta outros itens de relatório.   
  
Para agrupar várias regiões de dados ou itens de relatório, coloque-os no mesmo contêiner pai. Por exemplo, coloque um gráfico e uma tabela em um contêiner de retângulo e alinhe as margens superiores para exibi-los lado a lado. Para obter mais informações, consulte [Rendering Behaviors in Report Builder](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)(Comportamentos de renderização no Construtor de Relatórios).  
  
## <a name="see-also"></a>Consulte Também  
[Solucionar problemas de recuperação de dados com relatórios do Reporting Services](../../reporting-services/troubleshooting/troubleshoot-data-retrieval-issues-with-reporting-services-reports.md)  
[Solucionar problemas de assinaturas e entrega do Reporting Services](../../reporting-services/troubleshooting/troubleshoot-reporting-services-subscriptions-and-delivery.md)  
  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

