---
title: Funcionalidade de cliente ADOMD.NET | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: adomd
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 792017600f15ebbfab4c0ee0e4af78c0404340d7
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="adomdnet-client-functionality"></a>Funcionalidade de cliente do ADOMD.NET
  O ADOMD.NET, assim como com outros provedores de dados do [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework, serve como uma ponte entre um aplicativo e uma fonte de dados. No entanto, ao contrário de outros provedores de dados do .NET Framework, o ADOMD.NET trabalha com dados analíticos. Para isso, o ADOMD.NET dá suporte à funcionalidade que é muito diferente de outros provedores de dados do .NET Framework. O ADOMD.NET não só permite que você recupere dados, como permite a recuperação de metadados e a alteração da estrutura do repositório de dados analíticos:  
  
 **Recuperando metadados**  
 Os aplicativos podem aprender mais sobre os dados que podem ser recuperados da fonte de dados por meio da recuperação de metadados, usando conjunto de linhas do esquema ou o modelo de objeto. As informações como os tipos de cada KPI (indicador chave de desempenho) disponíveis, as dimensões de um cubo e os parâmetros necessários aos modelos de mineração são descobríveis. Os metadados são mais importantes para *dinâmico* aplicativos que exigem entrada do usuário para determinar o tipo, a profundidade e o escopo dos dados a serem recuperados. Exemplos incluem o Analisador de Consultas, o Microsoft Excel e outras ferramentas de consulta. Metadados são menos críticos para *estático* aplicativos que executam um conjunto predefinido de ações.  
  
 Para obter mais informações: [recuperar metadados de uma fonte de dados analíticos](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md).  
  
 **Recuperando dados**  
 A recuperação de dados é a recuperação real das informações armazenadas na fonte de dados. A recuperação de dados é a principal função de aplicativos "estáticos", que conhecem a estrutura da fonte de dados. A recuperação de dados também é o resultado final dos aplicativos "dinâmicos". O valor do KPI em um determinado momento do dia, o número de bicicletas vendidas na última hora para cada loja e os fatores que governam o desempenho anual dos funcionários são exemplos de dados que podem ser recuperados. A recuperação de dados é vital para qualquer aplicativo de consulta.  
  
 Para obter mais informações: [recuperando dados de uma fonte de dados analíticos](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-from-an-analytical-data-source.md).  
  
 **Alterar a estrutura de dados analíticos**  
 O ADOMD.NET também pode ser usado para alterar a estrutura do repositório de dados analíticos. Embora normalmente isso seja feito por meio do modelo de objeto do AMO (Objetos de Gerenciamento de Análise), você pode usar o ADOMD.NET para enviar comandos ASSL (Analysis Services Scripting Language) para criar, alterar ou excluir objetos no servidor.  
  
 Para obter mais informações: [executar comandos em relação a um analíticos fonte de dados](../../analysis-services/multidimensional-models-adomd-net-client/executing-commands-against-an-analytical-data-source.md), [desenvolvendo com objetos de gerenciamento de análise &#40;AMO&#41;](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md), [script do Analysis Services Idioma &#40;ASSL para XMLA&#41;](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)  
  
 A recuperação de metadados, a recuperação de dados e a alteração da estrutura de dados podem ocorrer em um ponto específico do fluxo de trabalho de um aplicativo ADOMD.NET típico.  
  
## <a name="typical-process-flow"></a>Fluxo de processo típico  
 Os aplicativos ADOMD.NET tradicionais normalmente seguem o mesmo fluxo de trabalho ao trabalharem com um banco de dados analítico:  
  
1.  Primeiro, uma conexão é feita ao banco de dados, usando o objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>. Quando você abre a conexão, o objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> exibe metadados sobre o servidor ao qual se conectou. Em um aplicativo dinâmico, algumas dessas informações são normalmente mostradas ao usuário para que ele possa fazer uma escolha, como que cubo será consultado. A conexão criada durante esta etapa poderá ser reutilizada várias vezes pelo aplicativo, reduzindo a sobrecarga.  
  
     Para obter mais informações: [estabelecer conexões no ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net.md)  
  
2.  Depois que uma conexão foi estabelecida, um aplicativo dinâmico consulta o servidor para obter metadados mais específicos. Para um aplicativo estático, o programador sabe com antecedência que objetos serão consultados pelo aplicativo e não precisará recuperar esses metadados. Os metadados recuperados podem ser usados pelo aplicativo e pelo usuário na próxima etapa.  
  
     Para obter mais informações: [recuperar metadados de uma fonte de dados analíticos](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md)  
  
3.  Em seguida, o aplicativo executa um comando no servidor. Esse comando pode ser para fins de recuperação de metadados adicionais, para recuperação de dados ou para a modificação da estrutura do banco de dados. Para qualquer uma dessas tarefas, o aplicativo poderia usar uma consulta determinada previamente ou utilizar metadados recém-recuperados para criar consultas adicionais.  
  
     Para obter mais informações: [recuperar metadados de uma fonte de dados analíticos](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md), [recuperando dados de uma fonte de dados analíticos](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-from-an-analytical-data-source.md), [executar comandos em relação a um analíticos fonte de dados](../../analysis-services/multidimensional-models-adomd-net-client/executing-commands-against-an-analytical-data-source.md)  
  
4.  Depois que o comando é enviado ao servidor, o servidor começa a retornar os metadados ou os dados para o cliente. Essas informações podem ser exibidas usando um <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> objeto, um <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> objeto, ou um **System.XmlReader** objeto.  
  
 Para ilustrar esse fluxo de trabalho tradicional, o exemplo a seguir contém um método que abre uma conexão ao banco de dados, executa um comando em um cubo conhecido e recupera os resultados em um conjunto de células. O conjunto de células retorna uma cadeia de caracteres delimitada por tabulações que contém cabeçalhos de coluna, cabeçalhos de linha e dados de célula.  
  
 [!code-cs[Adomd.NetClient#ReturnCommandUsingCellSet](../../analysis-services/multidimensional-models-adomd-net-client/codesnippet/csharp/adomd-net-client-functio_1.cs)]  
  
## <a name="see-also"></a>Consulte também  
 [Programação do cliente no ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)  
  
  
