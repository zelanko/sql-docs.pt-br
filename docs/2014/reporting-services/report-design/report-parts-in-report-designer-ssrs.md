---
title: Partes de relatório no Designer de Relatórios (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.components.f1
ms.assetid: 0c34311d-05d6-4bd2-b452-545fa95f8e7f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2c696b87a8c8cf4688e24a0e3177948d339d7443
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66105059"
---
# <a name="report-parts-in-report-designer-ssrs"></a>Partes de relatório no Designer de Relatórios (SSRS)
  No Designer de Relatórios, depois de criar tabelas, gráficos e outros itens de relatório em um projeto, você pode publicá-los como *partes de relatório* em um servidor de relatório ou site do SharePoint integrado com um servidor de relatório de forma que você e outros usuários possam reutilizá-las em outros relatórios.  
  
 Em geral, as partes do relatório funcionam da mesma maneira no Designer de Relatórios e no Construtor de Relatórios. Para ler sobre a funcionalidade básica, consulte [partes de relatório &#40;Construtor de relatórios e SSRS&#41;](../report-parts-report-builder-and-ssrs.md) na [documentação do construtor de relatórios](https://go.microsoft.com/fwlink/?LinkId=154494) no msdn.Microsoft.com.  
  
 Há diferenças fundamentais na maneira como as partes do relatório funcionam no Designer de Relatórios. Uma diferença principal é o fluxo de trabalho. O Construtor de Relatórios permite criação colaboradora: eu crio uma parte de relatório e a publico. Você pode reutilizar, modificar e republicá-la. No Designer de Relatórios, a publicação é unidirecional: eu posso publicar uma parte de relatório no Designer de Relatórios, e você pode reutilizá-la. Mas eu não posso reutilizar uma parte de relatório existente em um relatório em Designer de Relatórios. Este tópico aborda essas diferenças, depois de uma visão geral rápida das partes de relatório.  
  
##  <a name="ComponentWorkflow"></a>Ciclo de vida da publicação de parte de relatório  
 ![rs_ComponentCreation](../media/rs-componentcreation.gif "rs_ComponentCreation")  
  
1.  No Designer de Relatórios, a Pessoa A cria um projeto que contém um relatório com um gráfico que depende de um conjunto de dados inserido.  
  
2.  A Pessoa A sinaliza o gráfico com seu conjunto de dados inserido para publicação. O Designer de Relatórios atribui uma ID exclusiva a ele. Em seguida, a Pessoa A implanta o relatório no servidor de relatório. O Designer de Relatórios publica o gráfico.  
  
3.  A Pessoa B cria um relatório em branco no Construtor de Relatórios e adiciona o gráfico a ele. O gráfico agora faz parte do relatório da Pessoa B, junto com o conjunto de dados inserido. A Pessoa B pode modificar as instâncias do gráfico e do conjunto de dados que estão no relatório. Isso não terá nenhum efeito nas instâncias do gráfico e do conjunto de dados no servidor de relatório, nem quebrará a relação entre as instâncias no relatório e no servidor de relatório.  
  
     ![rs_BIDScomponentupdate](../media/rs-bidscomponentupdate.gif "rs_BIDScomponentupdate")  
  
4.  No Designer de Relatórios, a Pessoa A modifica o gráfico no relatório original.  
  
5.  A Pessoa A reimplantar o relatório que republica o gráfico no servidor dessa forma atualizando o gráfico no servidor.  
  
6.  No Construtor de Relatórios, a Pessoa B aceita o gráfico atualizado do servidor. Isso substitui as alterações que a Pessoa B fez no gráfico no relatório da Pessoa B.  
  
##  <a name="PublishingComponents"></a>Publicando partes de relatório  
 Quando você publica uma parte de relatório, o Designer de Relatórios atribui uma ID à parte. Dali em diante, essa ID é mantida, independentemente de qualquer outra alteração. A identificação vincula o item de relatório original em seu relatório à parte de relatório. Quando outros autores de relatório reutilizam a parte de relatório no Construtor de Relatórios, a ID também vincula a parte de relatório e seu relatório à parte de relatório.  
  
 Estes são os itens de relatório que você pode publicar como partes de relatório:  
  
-   Gráficos  
  
-   Medidores  
  
-   Imagens e imagens inseridas  
  
-   Mapas  
  
-   parâmetros  
  
-   Retângulos  
  
-   Tabelas  
  
-   Matrizes  
  
-   Listas  
  
 Se você estiver publicando uma parte de relatório que exibe dados, como uma tabela, matriz ou gráfico, poderá baseá-la em um conjunto de dados compartilhado. Caso contrário, quando você publicar a parte de relatório, o conjunto de dados do qual ela depende será salvo como um conjunto de dados inserido. Conjuntos de dados inseridos podem ser baseados em fontes de dados inseridas, mas as credenciais não são armazenadas nas fontes de dados inseridas. Portanto, se sua parte de relatório depender de um conjunto de dados inserido que usa uma fonte de dados inserida, qualquer um que reutilizar essa parte de relatório precisará fornecer as credenciais para a fonte de dados inserida. Para evitar isso, baseie seus conjuntos de dados inseridos e compartilhados em fontes de dados compartilhadas com credenciais armazenadas. Para obter mais informações, consulte [partes de relatório e conjuntos de dados em Construtor de relatórios](../report-data/report-parts-and-datasets-in-report-builder.md) na [documentação do construtor de relatórios](https://go.microsoft.com/fwlink/?LinkId=154494) no msdn.Microsoft.com.  
  
 A publicação de uma parte de relatório no Designer de Relatórios é um processo de duas etapas:  
  
1.  Sinalize os itens de relatório que você deseja publicar na caixa de diálogo **Publicar Partes de Relatório** .  
  
2.  Implante o relatório.  
  
 Quando você implanta o relatório, a parte de relatório é publicada em um site do SharePoint ou servidor de relatório e outros usuários podem reutilizá-la. Para publicar uma parte de relatório, você deve ter uma conexão com um servidor de relatório do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e permissões suficientes nesse servidor ao implantar o relatório.  
  
  
##  <a name="SearchReuseComponents"></a>Reutilizando partes de relatório  
 Ao contrário do Construtor de Relatórios, você não pode pesquisar e reutilizar uma parte de relatório em um projeto diferente daquele em ela foi criada.  
  
 Os autores de relatório que trabalham com o Construtor de Relatórios podem pesquisar e reutilizar partes de relatório que você publica em relatórios que eles criam.  
  
##  <a name="RepublishingComponents"></a>Republicando partes de relatório  
 No Designer de Relatórios, você deve atualizar uma parte de relatório existente de dentro do relatório no qual você ela foi criada. No Construtor de Relatórios, os autores de relatório podem reutilizar a parte de relatório e publicá-la como uma nova parte de relatório sem substituir a parte de relatório que você publicou. Se tiverem permissões suficientes, eles também poderão atualizar a parte de relatório que você publicou. Qualquer usuário com permissões suficientes para uma pasta em um site ou servidor pode atualizar as partes de relatório armazenadas lá. A última atualização substitui atualizações anteriores.  
  
 Você pode modificar e, em seguida, republicar a parte de relatório no site ou no servidor. Os autores de relatório do Construtor de Relatórios que adicionaram essa parte de relatório a um relatório serão informados sobre a alteração na próxima vez que abrirem o relatório. Eles podem escolher aceitar ou não as alterações.  
  
 Você também pode optar por publicar como novo um relatório que já publicou. Na caixa de diálogo Publicar Partes de Relatório, clique em Publicar como uma nova parte de relatório. Essa nova parte de relatório tem uma nova identificação exclusiva e não tem nenhuma relação com a parte de relatório antiga.  
  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciando partes de relatório](managing-report-parts.md)  
  
  
