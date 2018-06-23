---
title: Localizar texto, números ou datas em um relatório (Reporting Services no modo integrado do SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- searching reports
ms.assetid: 309dffe5-00f5-404f-bb63-9e6046253ae0
caps.latest.revision: 11
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 6fe713a9ef49efdf6cb1a04da094f877fc614582
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019785"
---
# <a name="find-text-numbers-or-dates-in-a-report-reporting-services-in-sharepoint-integrated-mode"></a>Localizar texto, números ou datas em um relatório (Reporting Services no modo integrado do SharePoint)
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
  
## <a name="see-also"></a>Consulte também  
 [Adicionar a Web Part do Visualizador de relatórios para uma página da Web &#40;Reporting Services no SharePoint modo integrado&#41;](../report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)  
  
  