---
title: Solução de problemas de renderização de relatório do Reporting Services | Microsoft Docs
ms.date: 02/27/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
ms.assetid: 1e0fb399-4c16-438a-92cb-db3e877896d0
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3f8c5029d66a068d43ebc659592697fd2914fd2b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65574683"
---
# <a name="troubleshoot-reporting-services-report-rendering-issues"></a>Solucionar problemas de renderização de relatório do Reporting Services
Após a combinação dos dados do relatório e das informações de layout, o relatório compilado é enviado a um renderizador de relatório. Por exemplo, quando você visualiza um relatório localmente, está usando o renderizador HTML para exibir o relatório compilado. Use este tópico para ajudar a solucionar problemas específicos da renderização de relatório.   
  
## <a name="why-do-i-have-extra-white-space-including-blank-pages-in-my-report"></a>Por que tenho um espaço em branco extra, incluindo páginas em branco, no meu relatório?  
Os itens de relatório são ajustados automaticamente durante o processamento de um relatório para preservar o espaço em branco definido como parte do relatório. O espaço em branco na exibição de design de relatório é preservado. Na superfície de design do relatório, o plano de fundo branco representa o espaço em branco que será preservado quando um relatório for exibido, exportado ou impresso, dependendo da mídia de destino.  
  
### <a name="white-space-and-page-breaks-interact-during-rendering"></a>O espaço em branco e as quebras de página interagem durante a renderização  
Quando você exibe um relatório ou exporta-o para um formato de arquivo, a extensão de renderização associada processa o relatório e salva-o no formato de arquivo especificado. Cada extensão de renderização processa o espaço em branco em um relatório de acordo com as regras específicas. O espaço em branco também é afetado pelas propriedades de configuração de página, quebras de página definidas nos itens de relatório, a posição relativa dos itens de relatório colocados no corpo do relatório, a propriedade KeepTogether para certos itens de relatório e se os itens de relatório estão nos contêineres pai.   
  
Para eliminar páginas adicionais por causa da largura do relatório, arraste a borda da superfície de design do relatório para alinhar com o item de relatório externo. Para um layout de relatório da esquerda para a direita, arraste a borda da direita para alinhar com o item de relatório externo. Para obter mais informações, confira [Comportamentos de renderização](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md).  
  
### <a name="white-space-is-not-preserved-at-the-end-of-a-report"></a>O espaço em branco não é preservado ao final de um relatório  
O Reporting Services oferece uma opção que lhe permite controlar se o espaço em branco ao final de um relatório deve ser preservado ou eliminado.   
  
Para preservar o espaço em branco ao final de um relatório, selecione-o e, no painel Propriedades, vá para ConsumeContainerWhitespace e digite False.   
  
## <a name="why-do-my-reports-look-different-when-exported-to-different-formats"></a>Por que meus relatórios ficam com uma aparência diferente quando são exportados para formatos diferentes?  
Após a emissão de um relatório, você pode exportá-lo para outro formato, como Excel, Word ou PDF. Dependendo do formato para o qual você exporta o relatório, certas regras e limitações podem ser aplicadas. É possível resolver muitas limitações, considerando-as durante a criação do relatório. Você talvez precise usar um layout um pouco diferente no relatório, alinhar cuidadosamente itens dentro do relatório, confinar rodapés do relatório a uma única linha de texto e assim por diante. Além disso, é possível usar RenderFormat interno global para usar condicionalmente layouts de relatório diferentes em renderizadores distintos. Outro globals internos podem ajudar a gerenciar a paginação no formato exportado e nomear guias de planilhas no Excel. Para obter mais informações, consulte [Exportando relatórios](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md) e [Use Built-in Globals an Users Reference](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)(Usar referências de usuários e globais internas).  
  
## <a name="how-can-i-view-all-my-report-data-on-one-page"></a>Como faço para exibir todos os dados do meu relatório em uma página?  
Para obter uma experiência de exibição interativa para os relatórios que não têm quantidades excessivas de dados, talvez você queira visualizar todos os dados em uma página.   
  
Para renderizadores de quebra de página flexíveis, para exibir todos os dados em uma página, nas propriedades de Relatório, defina InteractiveHeight como 0. Em renderizadores de quebra de página flexível, as quebras existentes são ignoradas.   
  
> [!NOTE]  
> Quando um relatório não possuir quebras de página, ele deve ser inteiramente processado antes que você possa exibir a primeira página.   
  
Para obter mais informações sobre categorias de renderizadores, consulte [Comportamentos de renderização](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md).  
  
## <a name="reports-do-not-run-when-your-browser-is-configured-to-prompt-for-credentials"></a>Os relatórios não são emitidos quando seu navegador estiver configurado para solicitar credenciais  
A exibição dos seus relatórios pode falhar com uma mensagem de erro quando seu navegador estiver configurado para solicitar credenciais e sua fonte de dados estiver configurada para a autenticação integrada do Windows. Isso ocorre quando sua fonte de dados estiver em um computador separado do servidor de relatórios, quando a fonte de dados estiver configurada para usar a Autenticação do Windows e quando o navegador estiver configurado para solicitar credenciais. Veja a seguir exemplos de mensagens que você verá.  
  
Quando a fonte de dados estiver configurada para um tipo de conexão do Microsoft SQL Server:  
`An error has occurred during report processing.`  
`Cannot create a connection to data source 'localhost'.`  
`Login failed for user '(null)'. Reason: Not associated with a trusted SQL Server connection.`  
  
Quando a fonte de dados estiver configurada para uma tipo de conexão do tipo SharePoint List:  
`An error occurred during client rendering.`   
`An error has occurred during report processing.`   
`Query execution failed for dataset 'DataSet1'.`   
`The request failed with HTTP status 401: Unauthorized.`  
  
**Para contornar este problema:** modifique a fonte de dados para usar credenciais armazenadas, em vez das credenciais do Windows.  
  
**Este problema se aplica a:** navegadores configurados para solicitar credenciais.  
  
## <a name="see-also"></a>Consulte Também  
[Erros e eventos (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
[Solucionar problemas de recuperação de dados com relatórios do Reporting Services](../../reporting-services/troubleshooting/troubleshoot-data-retrieval-issues-with-reporting-services-reports.md)  
[Solucionar problemas de assinaturas e entrega do Reporting Services](../../reporting-services/troubleshooting/troubleshoot-reporting-services-subscriptions-and-delivery.md)  
  
  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

