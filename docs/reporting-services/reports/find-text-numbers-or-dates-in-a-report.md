---
title: Localizar texto, números ou datas em um relatório | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- searching reports
ms.assetid: 309dffe5-00f5-404f-bb63-9e6046253ae0
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d17541a43178f7ebe5161904266087096844b680
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47620984"
---
# <a name="find-text-numbers-or-dates-in-a-report"></a>Localizar texto, números ou datas em um relatório
  Você pode procurar conteúdo em um relatório digitando a palavra ou expressão que deseja localizar (o tamanho máximo de um termo de pesquisa é de 256 caracteres). A pesquisa é uma técnica de navegação na Internet que localiza um valor correspondente no relatório e destaca essa parte do relatório que contém o valor.  
  
 A pesquisa não diferencia maiúsculas e minúsculas, e começa na página ou seção selecionada no momento. Somente o conteúdo visível no relatório é incluído na operação de pesquisa. Se o relatório contiver áreas que podem ser expandidas ou recolhidas, os valores em uma área recolhida serão ignorados durante a pesquisa. Só é possível procurar texto, números ou datas que estejam no relatório atual. Se você estiver usando um relatório de clique gerado automaticamente para explorar dados, não poderá procurar um termo visto em um relatório gerado anteriormente nem poderá pesquisar um termo que talvez apareça em um relatório mais adiante no caminho de dados.  
  
 Ao digitar um valor de pesquisa, digite-o como espera que ele apareça no relatório. Não digite uma pergunta, por exemplo, “qual é o lucro médio deste mês”, a menos que espere que cada palavra da frase esteja no relatório.  
  
 Você só pode procurar um termo ou valor de cada vez. Não é possível usar operadores de pesquisa (por exemplo, E ou OU) ou símbolos e caracteres curinga. Você não pode realizar uma pesquisa em uma seção cruzada dos dados (por exemplo, procurando as vendas líquidas de um determinado produto em um dado mês). Para esse tipo de análise, use o Construtor de Relatórios para criar ou usar relatórios de clickthrough.  
  
 As configurações de segurança de modelo e banco de dados que restringem o acesso aos dados do relatório se aplicam às operações de pesquisa. Se você estiver procurando um valor em um relatório de clickthrough que usa um modelo como fonte de dados e não tiver acesso a uma parte do modelo, os dados apresentados por essa parte do modelo serão excluídos da pesquisa.  
  
### <a name="to-find-data-in-a-report"></a>Para localizar dados em um relatório  
  
1.  Abra o relatório.  
  
2.  Na barra de ferramentas do relatório, digite o texto, número ou a data que deseja localizar.  
  
     Se a barra de ferramentas do relatório não estiver visível, terá sido ocultada de propósito e você não poderá usar a funcionalidade que ela fornece. As propriedades na Web Part do Visualizador de Relatórios determinam se a barra de ferramentas está visível.  
  
3.  Clique em **Localizar**.  
  
4.  Para procurar ocorrências subsequentes do mesmo valor, clique em **Próximo**.  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar a Web Part do Visualizador de Relatórios a uma página da Web &#40;Reporting Services no modo integrado do SharePoint&#41;](../../reporting-services/report-server-sharepoint/add-the-report-viewer-web-part-to-a-web-page.md)  
  
  
