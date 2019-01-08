---
title: Partes de relatório (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10543"
ms.assetid: 957f664c-8a7a-4532-b5a6-5f859c5840bd
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6114407d959a29944f01711b2446ce375f203b83
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53366368"
---
# <a name="report-parts-report-builder-and-ssrs"></a>Partes de relatório (Construtor de Relatórios e SSRS)
  Itens de relatório como tabelas, matrizes, gráficos e imagens podem ser publicados como *partes de relatório*. Partes de relatório são itens de relatório que foram publicados separadamente em um servidor de relatório e podem ser reutilizados em outros relatórios. As partes de relatório têm uma extensão de arquivo .rsc.  
  
 Com partes de relatório, os grupos de trabalho agora podem aproveitar as diferentes forças e funções dos membros da equipe. Por exemplo, se você for responsável por criar gráficos, poderá salvá-los como partes separadas que você e seu colaboradores podem reutilizar em outros relatórios. Você pode publicar partes de relatório em um servidor de relatório ou site do SharePoint integrado com um servidor de relatório. Você pode reutilizá-los em vários relatórios e pode atualizá-los no servidor.  
  
 A parte de relatório que você adiciona ao relatório mantém uma relação com a instância da parte de relatório no site ou servidor por meio de uma identificação exclusiva. Depois de adicionar partes de relatório de um site ou servidor a um relatório, você pode modificá-los, independentemente de a parte de relatório original estar no site ou servidor. Você pode aceitar atualizações que outros fizeram à parte de relatório no site ou servidor e pode salvar a parte de relatório modificada no site ou servidor, adicionando uma nova parte de relatório ou gravando sobre o original, se você tiver permissões suficientes.  
  
 Para começar rapidamente com partes de relatório, veja os vídeos [partes de relatório de 3 de construtor de relatórios no SQL Server 2008 R2](https://technet.microsoft.com/edge/Video/ff711300) e [como: Criar partes de relatório reutilizáveis com o construtor de relatórios do SQL Server](https://technet.microsoft.com/sqlserver/ff634166.aspx).  
  
##  <a name="ComponentWorkflow"></a> Ciclo de vida de uma parte de relatório  
 ![rs_ComponentCreation](media/rs-componentcreation.gif "rs_ComponentCreation")  
  
1.  A pessoa A cria um relatório com um gráfico que depende de um conjunto de dados inserido.  
  
2.  A pessoa A deseja publicar o gráfico no servidor de relatório. O Construtor de Relatórios atribui uma identificação exclusiva ao gráfico publicado. A pessoa A não deseja compartilhar o conjunto de dados; portanto, o conjunto de dados permanece inserido no gráfico.  
  
3.  A Pessoa B cria um relatório em branco, pesquisa a Galeria de Partes de Relatório, encontra o gráfico e o adiciona ao relatório. O gráfico agora faz parte do relatório da Pessoa B, junto com o conjunto de dados inserido. A Pessoa B pode modificar as instâncias do gráfico e do conjunto de dados que estão no relatório. Isso não terá nenhum efeito nas instâncias do gráfico e do conjunto de dados no servidor de relatório, nem quebrará a relação entre as instâncias no relatório e no servidor de relatório.  
  
     ![rs_componentupdate](media/rs-componentupdate.gif "rs_componentupdate")  
  
4.  A pessoa C adiciona o gráfico a um relatório e altera este gráfico no relatório de uma barra para um gráfico de pizza.  
  
5.  A pessoa C tem permissões para substituir o gráfico no servidor e faz isso republicando-o no servidor. Isto atualiza a cópia publicada do gráfico no servidor. A pessoa C também não deseja compartilhar o conjunto de dados; portanto, ele permanece inserido no gráfico.  
  
6.  A Pessoa B aceita o gráfico atualizado a partir do servidor. Isso substitui as alterações que a Pessoa B fez no gráfico no relatório da Pessoa B.  
  
 ![Ícone de seta usado com o link Voltar ao início](../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início")[Voltar ao início](#BackToTop)  
  
##  <a name="PublishingComponents"></a> Publicando partes de relatório  
 Quando você publicar uma parte de relatório, o Construtor de Relatórios atribui a ele uma identificação exclusiva que é distinta do nome da parte de relatório. O Construtor de Relatórios mantém aquela identificação, não importa o que mais você altere sobre a parte de relatório. A identificação vincula o item de relatório original em seu relatório à parte de relatório. Quando outros autores de relatório reutilizam a parte de relatório, a ID também vincula a parte de relatório em seu relatório à parte de relatório no servidor de relatórios.  
  
 Estes são os itens de relatório que você pode publicar como partes de relatório:  
  
-   Gráficos  
  
-   Medidores  
  
-   Imagens  
  
-   Mapas  
  
-   Parâmetros  
  
-   Retângulos  
  
-   Tabelas  
  
-   Matrizes  
  
-   Listas  
  
 Quando você publicar um item de relatório que exibe dados, como uma tabela, matriz ou gráfico, o conjunto de dados do que o item de relatório depende será salvo com ele, como um conjunto de dados inserido. Você também pode salvar o conjunto de dados separadamente, como um conjunto de dados compartilhado que você e outros podem usar como uma base para outras partes de relatório. Para obter mais informações, consulte [Partes de relatório e conjuntos de dados no Construtor de Relatórios](report-data/report-parts-and-datasets-in-report-builder.md).  
  
 Algumas partes de relatório podem conter outros itens de relatório. Por exemplo, uma tabela pode conter um gráfico e um retângulo pode conter uma matriz e um gráfico. Quando você publicar um item de relatório que contém outros itens de relatório, eles serão salvos como uma unidade. Os outros itens de relatório são salvos inseridos na parte de relatório de contêiner. Você não pode atualizá-los separadamente e não pode salvar os itens no contêiner como partes de relatório separadas.  
  
 Para obter mais informações sobre a publicação de partes de relatório, consulte [Publicar e republicar partes de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-parts-report-builder-and-ssrs.md).  
  
### <a name="modifying-report-part-metadata"></a>Modificando metadados de parte de relatório  
 Você pode publicar partes de relatório com configurações padrão para uma localização padrão ou pode salvar cada parte de relatório em um local diferente e modificar os metadados, como o título e a descrição.  
  
 É conveniente dar à parte de relatório nome e descrição claros quando você o publicar, para facilitar a identificação durante a pesquisa. Você pode acabar com muitas partes de relatório com nomes semelhantes em seu site ou servidor. Use convenções de nomenclatura para ilustrar relações entre partes de relatório e os itens dependentes correspondentes.  
  
 Além disso, salve fontes de dados compartilhadas, conjuntos de dados compartilhados e as partes de relatório que dependem deles na mesma pasta.  
  
 Você também pode editar a descrição no painel Propriedades.  
  
 ![Ícone de seta usado com o link Voltar ao início](../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início")[Voltar ao início](#BackToTop)  
  
##  <a name="ReusingComponents"></a> Reutilizando partes de relatório  
 O modo mais fácil de criar um relatório é adicionar uma parte de relatório existente, como uma tabela ou gráfico, ao relatório a partir da Galeria de Partes de Relatório. Depois de adicioná-lo a seu relatório, você poderá modificá-lo o quanto precisar, ou aceitar as atualizações do servidor. Alterar o item de relatório em seu relatório não afetará a instância da parte de relatório publicada no site ou servidor, nem interromperá a relação entre a instância no relatório e no site ou servidor. Se você tiver permissões suficientes, poderá salvar a cópia atualizada no site ou servidor. Se outra pessoa modificar a cópia no site ou servidor, você poderá decidir manter sua cópia como está, ou poderá atualizá-la para ficar com a cópia no site ou servidor.  
  
### <a name="searching-for-report-parts"></a>Procurando partes de relatório  
 Você deve procurar partes de relatório para adicionar a seu relatório na Galeria de Partes de Relatório. É possível filtrar as partes de relatório por tudo ou parte do nome da parte, quem criou, quem modificou por último, quando foi a última modificação, onde está armazenada ou que tipo de parte de relatório é. Por exemplo, você pode procurar todos os gráficos criados na semana passada por um de seus colaboradores.  
  
 Você pode exibir os resultados da pesquisa como miniaturas ou como uma lista, e classificar os resultados da pesquisa por nome, data de criação e modificação, e criador. Para obter mais informações, consulte [Procurar partes de relatório e definir uma pasta padrão &#40;Construtor de Relatórios e SSRS&#41;](report-design/browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs.md).  
  
### <a name="what-comes-with-a-report-part"></a>O que vem com uma parte de relatório  
 Quando você adiciona uma parte de relatório a seu relatório, também está adicionando tudo que ele deve ter para funcionar. Por exemplo, qualquer objeto que exiba dados depende de um conjunto de dados: uma consulta e uma conexão com uma fonte de dados. Também pode ter um ou mais parâmetros. Todos os itens dos quais ele depende são suas *dependências*e todos eles, ou ponteiros para eles, serão incluídos com a parte de relatório quando você adicioná-lo ao relatório. O conjunto de dados e os parâmetros são listados no painel de dados do relatório do seu relatório.  
  
 O conjunto de dados para a parte de relatório pode ser inserido na parte de relatório, ou pode ser um conjunto de dados separado e compartilhado para o qual a parte de relatório aponta. Se for inserido na parte de relatório, você talvez possa modificá-lo. Se for um conjunto de dados compartilhado, será um objeto separado para o qual você precisaria de permissões. Para obter mais informações sobre compartilhada e conjuntos de dados inseridos, consulte [adicionar dados a um relatório &#40;construtor de relatórios e SSRS&#41;](report-data/report-datasets-ssrs.md).  
  
### <a name="resolving-naming-conflicts"></a>Resolvendo conflitos de nomenclatura  
 Quando você adiciona uma parte de relatório, o Construtor de Relatórios corrige os conflitos de nome. Por exemplo, se você já tiver um Chart1 em seu relatório e adicionar uma parte de relatório chamada Chart1, o Construtor de Relatórios renomeará automaticamente a nova parte de relatório como Chart2. Se você já tiver um Dataset1 em seu relatório e adicionar uma parte de relatório que refere-se a um conjunto de dados diferente que também é chamado Dataset1, o Construtor de Relatórios renomeará o novo conjunto de dados como Dataset2 e atualizará as referências.  
  
### <a name="adding-more-than-one-report-part"></a>Adicionando mais de uma parte de relatório  
 Você pode adicionar um número ilimitado de partes de relatório ao relatório. No entanto, você só poderá adicionar uma parte de relatório de cada vez. Você pode até mesmo adicionar várias instâncias de uma parte de relatório ao mesmo relatório. Todos eles terão nomes exclusivos, mas serão instâncias da mesma parte de relatório no servidor e terão a mesma identificação exclusiva.  
  
 Quando você adicionar outra parte de relatório que já usa um conjunto de dados idêntico a um conjunto de dados em seu relatório, o assistente não adicionará outra versão daquele conjunto de dados ao relatório; ele redirecionará as referências na parte de relatório para ir para o conjunto de dados existente. Para obter mais informações, consulte [Partes de relatório e conjuntos de dados no Construtor de Relatórios](report-data/report-parts-and-datasets-in-report-builder.md).  
  
 ![Ícone de seta usado com o link Voltar ao início](../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início")[Voltar ao início](#BackToTop)  
  
##  <a name="UpdatingComponents"></a> Atualizando partes de relatório com alterações a partir do servidor  
 Sempre que você abre um relatório, o Construtor de Relatórios verifica se as instâncias de servidor de partes de relatório nesse relatório foram atualizadas no servidor. Também procura alterações nos itens dependentes das partes de relatório, como o conjunto de dados e os parâmetros. Se as partes de relatório publicadas ou suas dependências foram atualizados no servidor, uma barra de informações no relatório exibe o número que foi atualizado. Você pode optar por exibir e aceitar ou rejeitar as atualizações ou descartar a barra de informações. Se você escolher exibir as atualizações, verá uma miniatura da parte de relatório que foi modificada por último e quando. Você poderá então aceitar um ou todos os itens atualizados.  
  
> [!NOTE]  
>  Você pode desabilitar a barra de informações e não ser informado se a parte de relatório tiver sido alterada. Você define esta opção quando adiciona a parte de relatório ao seu relatório. Mesmo que você tenha desabilitado a barra de informações, ainda poderá procurar atualizações. Para obter mais informações, consulte [verificar ou desativar atualizações &#40;construtor de relatórios e SSRS&#41;](../../2014/reporting-services/check-for-updates-or-turn-updates-off-report-builder-and-ssrs.md).  
  
 O Construtor de Relatórios verifica se há diferenças entre a data da última atualização da parte de relatório no servidor e a data da última sincronização da parte de relatório com o servidor. Ele não verifica a data que você modificou a parte de relatório em seu relatório. Portanto, a parte de relatório em seu relatório e a parte de relatório no servidor podem ser bastante diferentes, mas quando o Construtor de Relatórios verificar se há atualizações, ele não localizará nenhuma.  
  
### <a name="accepting-updates"></a>Aceitando atualizações  
 Quando você aceita uma atualização para uma parte de relatório, ela substitui completamente a cópia da parte de relatório que já está em seu relatório. Você não pode combinar recursos da parte de relatório no relatório com recursos da parte de relatório publicada no servidor. Porém, se você alterou uma das dependências da parte de relatório, como um conjunto de dados inserido, o Construtor de Relatórios não copiará sobre a dependência que já está em seu relatório. Ele baixa uma nova cópia da dependência e atualiza a parte de relatório para apontar para a nova cópia.  
  
### <a name="reverting-to-a-previous-version-of-a-report-part"></a>Revertendo a uma versão anterior de uma parte de relatório  
 Se você tiver alterado uma versão de uma parte de relatório em seu relatório e decidiu que deseja substituí-la pela versão que está no servidor, não poderá usar a caixa de diálogo **Atualizar** para fazer isso. Atualizar serve somente para partes de relatório que foram alteradas no servidor desde que você as baixou.  
  
 Para reverter para a versão no servidor, basta excluir a versão que você tem em seu relatório e adicioná-la novamente.  
  
 ![Ícone de seta usado com o link Voltar ao início](../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início")[Voltar ao início](#BackToTop)  
  
##  <a name="RepublishingComponents"></a> Atualizando partes de relatório que já estão no servidor  
 Você pode querer atualizar uma parte de relatório existente no servidor, ou publicá-la como uma nova parte de relatório sem substituir a existente. Quando você atualiza a parte de relatório no servidor, ela não modifica cópias da parte de relatório automaticamente em outros relatórios. Se outros autores de relatório adicionaram essa parte de relatório a um relatório, eles serão informados sobre a alteração na próxima vez que abrirem o relatório. Eles podem escolher aceitar ou não as alterações.  
  
 Se você desejar publicá-la como uma nova parte de relatório, o Construtor de Relatórios dará a ela uma nova identificação exclusiva e não mais a vinculará à parte de relatório original.  
  
 Se o conjunto de dados for inserido na parte de relatório, toda vez que você publicar a parte de relatório, o conjunto de dados será exibido na caixa de diálogo **Publicar Partes de Relatório** . Conjuntos de dados compartilhados não são exibidos na caixa de diálogo **Publicar Partes de Relatório** .  
  
 ![Ícone de seta usado com o link Voltar ao início](../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início")[Voltar ao início](#BackToTop)  
  
##  <a name="RptPartsRptDesigner"></a> Trabalhando com partes de relatório no Designer de Relatórios  
 O funcionamento de partes de relatório é um pouco diferente no Designer de Relatórios no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. No Designer de Relatórios, a publicação é unidirecional: você pode publicar uma parte de relatório no Designer de Relatórios, mas não pode reutilizar uma parte de relatório existente no Designer de Relatórios. Para obter mais informações, consulte [Partes de relatório no Designer de Relatórios &#40;SSRS&#41;](report-design/report-parts-in-report-designer-ssrs.md).  
  
##  <a name="HowTo"></a> Tópicos de instruções  
 [Publicar e republicar partes de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-parts-report-builder-and-ssrs.md)  
  
 [Procurar partes de relatório e definir uma pasta padrão &#40;Construtor de Relatórios e SSRS&#41;](report-design/browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs.md)  
  
 [Verificar ou desativar atualizações &#40;relatórios e SSRS&#41;](../../2014/reporting-services/check-for-updates-or-turn-updates-off-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Consulte também  
 [Partes de relatório e conjuntos de dados no Construtor de Relatórios](report-data/report-parts-and-datasets-in-report-builder.md)   
 [Solucionar problemas de partes de relatório &#40;relatórios e SSRS&#41;](../../2014/reporting-services/troubleshoot-report-parts-report-builder-and-ssrs.md)   
 [Gerenciando partes de relatório](report-design/managing-report-parts.md)   
 [Partes de relatório do construtor de relatórios 3 no SQL Server 2008 R2 (vídeo)](https://technet.microsoft.com/edge/Video/ff711300)   
 [Como faço Criar partes de relatório reutilizáveis com o construtor de relatórios do SQL Server (vídeo)](https://technet.microsoft.com/sqlserver/ff634166.aspx)  
  
  
