---
title: Compartilhar Feeds de dados usando uma biblioteca de Feed de dados (PowerPivot para SharePoint) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: power-pivot-sharepoint
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: data feeds [Analysis Services with SharePoint]
ms.assetid: 4ec98dec-0cd2-4727-bb79-5bf6f8a865d6
caps.latest.revision: "26"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6b345b289e396d62565f9fee76a72c0cf9cb9d04
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="share-data-feeds-using-a-data-feed-library-power-pivot-for-sharepoint"></a>Compartilhar feeds de dados usando uma biblioteca de feed de dados (Power Pivot para SharePoint)
  Um feed de dados é um fluxo de dados XML que é gerado em um serviço ou aplicativo que expõe dados no formato de conexão Atom. Ele é usado cada vez mais para transportar dados entre aplicativos e para visualizadores do lado do cliente. Em uma implantação do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, os feeds de dados são usados para preencher uma fonte de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] com dados de um aplicativo ou serviço com reconhecimento do Atom.  
  
 Se já usar uma combinação de aplicativos com reconhecimento do Atom, você talvez nunca precise saber como os feeds são gerados e consumidos porque a transferência de dados é transparente entre os aplicativos. No entanto, frequentemente as organizações que usam soluções personalizadas para publicar feeds Atom precisam de uma maneira de disponibilizar os feeds para os operadores de informações. Uma maneira de fazer isso é criar e compartilhar arquivos de documento de serviço de dados (.atomsvc) que fornecem conexões às origens online que geram os feeds. Uma biblioteca com finalidade especial, chamada de biblioteca de feed de dados, dá suporte à criação e ao compartilhamento de documentos de serviço de dados em um aplicativo Web do SharePoint.  
  
 Este tópico contém as seguintes seções:  
  
 [Pré-requisitos](#prereq)  
  
 [Criar um documento de serviço de dados](#createdsdoc)  
  
 [Proteger um documento de serviço de dados](#securedsdoc)  
  
 [Modificar um documento de serviço de dados](#modifydsdoc)  
  
 [Próxima etapa: Usar um documento de serviço de dados](#usedsdoc)  
  
> [!NOTE]  
>  Embora os feeds de dados sejam usados para adicionar dados da Web a uma fonte de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] criada em um [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)], qualquer aplicativo cliente que possa ler um feed Atom pode processar um documento de serviço de dados.  
  
##  <a name="prereq"></a> Pré-requisitos  
 Você deve ter uma implantação do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint que adicione o processamento de consulta do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] a um farm do SharePoint. O suporte ao feed de dados é implantado por meio do pacote de solução [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 Você deve ter uma biblioteca do SharePoint que dê suporte ao tipo de conteúdo de documento de serviço de dados. Uma biblioteca de Feed de Dados padrão é recomendada para essa finalidade, mas você pode adicionar manualmente o tipo de conteúdo a qualquer biblioteca. Para obter mais informações, consulte [Criar ou personalizar uma biblioteca de feed de dados &#40;Power Pivot para SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/create-or-customize-a-data-feed-library-power-pivot-for-sharepoint.md).  
  
 Você deve ter um serviço de dados ou uma fonte de dados online que forneça os dados tabulares XML no formato Atom 1.0.  
  
 Você deve ter permissões de colaboração em um site do SharePoint para criar ou gerenciar um documento de serviço de dados em uma biblioteca do SharePoint.  
  
##  <a name="createdsdoc"></a> Criar um documento de serviço de dados  
 Um documento de serviço de dados é uma solicitação permanente para transmissão de dados sob solicitação de uma fonte de dados ou aplicativo online que fornece dados em um formato de feed. Ao criar um documento de serviço de dados, você especifica um ponteiro para um ou mais serviços de dados endereçáveis por URL que fornecem o XML tabular no formato Atom distribuído.  
  
 Um único documento pode especificar vários feeds de dados. Isso será útil se você desejar recuperar um conjunto de cargas de dados do mesmo serviço ou até mesmo de serviços diferentes em uma única operação de importação.  
  
1.  Em um site do SharePoint, abra a biblioteca de Feed de Dados ou outra biblioteca de documentos à qual você adicionou e configurou o tipo de conteúdo de serviço de dados. Para localizar uma biblioteca de Feed de Dados criada anteriormente, clique em **Exibir Tudo** no Início Rápido.  
  
2.  Na faixa de opções na parte superior da página, em Ferramentas de Documento, clique em **Documentos**.  
  
3.  Clique em **Novo Documento** e selecione **Documento de Serviço de Dados**.  
  
4.  Na página Novo Documento de Serviço de Dados, digite as seguintes informações:  
  
    1.  Um nome e uma descrição para o documento de serviço de dados. Forneça detalhes suficientes para que os usuários possam determinar se devem usar o feed.  
  
    2.  Em Feed de Dados, digite uma URL para um serviço de dados ou aplicativo Web que forneça dados no formato Atom 1.0.  
  
         A URL deve ser resolvida para um serviço que retorna dados estruturados ou semiestruturados em linhas e colunas. O serviço deve retornar dados anonimamente ou por meio das credenciais de segurança do usuário atual.  
  
         A URL deve ser resolvida para um serviço que dê suporte à Autenticação do Windows, à autenticação básica ou ao acesso anônimo. O usuário que importa o feed especifica qual esquema usar. Por padrão, a segurança integrada é selecionada.  
  
         A URL de um feed de dados pode incluir parâmetros. Tipos diferentes de tecnologias de serviço de dados dão suporte a esquemas avançados de endereçamento por URL que permitem selecionar precisamente os dados que você deseja usar. Por exemplo, um serviço de dados do ADO.NET fornece parâmetros de URL para especificar entidades, associações e caminhos de navegação nos dados subjacentes. Ao especificar uma URL complexa como uma origem de um feed de dados, você pode especificar precisamente o conjunto de dados que deseja usar.  
  
    3.  Para o mesmo feed de dados, digite um nome de tabela que identifique subsequentemente o conjunto de dados em um aplicativo cliente. No [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)], cada feed de dados importado é colocado em seu próprio controle de tabela em uma fonte de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Você deve especificar o nome da tabela que recebe os dados importados ao configurar o feed de dados.  
  
5.  Clique em "Adicionar outro feed de dados" para repetir as etapas anteriores para especificar feeds adicionais do mesmo serviço ou de um serviço diferente.  
  
     Cada documento de serviço de dados é processado como uma única operação. Todos os feeds de dados no documento serão gerados de forma assíncrona e retornados a um aplicativo cliente na mesma operação. Por isso, especifique os pares de tabela-URL apenas para feeds de dados que você deseja usar em conjunto.  
  
     Como os esquemas de autenticação são definidos no nível do documento de serviço de dados, cada feed de dados adicional deve originar-se do serviço ou aplicativo que dê suporte ao mesmo esquema de autenticação do primeiro feed. Todos os feeds dentro do mesmo documento de serviço de dados serão autenticados pelo mesmo método em tempo de execução.  
  
6.  Salve o documento. O documento de serviço de dados é armazenado como um arquivo físico (.atomsvc) em uma biblioteca de conteúdo configurada para esse tipo de conteúdo.  
  
 Para usar o documento de serviço de dados, você pode abrir uma pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] e escolher a opção **Do Feed de Dados** no Assistente de Importação de Dados. Quando solicitado, um usuário especificará a URL do SharePoint do documento de serviço de dados para iniciar uma operação de importação de dados. Para obter mais informações, consulte [Use feeds de dados &#40;Power Pivot para SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/use-data-feeds-power-pivot-for-sharepoint.md).  
  
##  <a name="securedsdoc"></a> Proteger um documento de serviço de dados  
 Um documento de serviço de dados herda as permissões da biblioteca que o contém. As permissões definidas no item determinarão se um usuário pode abrir, modificar ou excluir o documento de serviço de dados.  
  
 Para usar um documento de serviço de dados como uma importação de feed de dados no aplicativo cliente do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , um usuário precisa apenas de permissões de exibição no documento. As permissões de exibição são suficientes para resolver a URL no Assistente de Importação.  
  
 As permissões de exibição em um documento de serviço de dados são verificadas apenas quando uma operação de importação de feed de dados é iniciada. Depois da importação, as permissões no documento não são verificadas continuamente. Os feeds que foram adicionados a uma fonte de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] existem como dados estáticos, desconectados do documento de serviço de dados que forneceu as informações de conexão originais.  
  
 De modo semelhante, qualquer operação de atualização de dados agendada subsequentemente também exclui o documento de serviço de dados. No momento da importação, as informações de conexão de cada feed são copiadas na fonte de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para fins de atualização. Dessa forma, as permissões em um documento de serviço de dados não são verificadas para atualização de dados, porque o próprio documento nunca é referenciado em uma operação de atualização.  
  
|Tarefa|Requisitos de permissão do SharePoint|  
|----------|----------------------------------------|  
|Importe os feeds de dados para uma pasta de trabalho habilitada para [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].|Exiba as permissões para o documento de serviço de dados em uma biblioteca.|  
|No aplicativo cliente [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , atualize os dados que foram recuperados anteriormente por meio de um feed.|Não aplicável. O aplicativo cliente [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] usa informações de conexão HTTP inseridas para conectar-se diretamente aos serviços de dados e aplicativos que fornecem o feed. O aplicativo cliente [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] não usa o documento de serviço de dados.|  
|Em um farm do SharePoint, atualize dados como uma tarefa agendada, sem necessidade de nenhuma entrada do usuário.|Não aplicável. O serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] usa informações de conexão HTTP inseridas para conectar-se diretamente aos serviços de dados e aplicativos que fornecem o feed. O serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] não usa o documento de serviço de dados.|  
|Excluir um documento de serviço de dados em uma biblioteca|Permissões de colaboração na biblioteca.|  
  
##  <a name="modifydsdoc"></a> Modificar um documento de serviço de dados  
 Você pode adicionar, editar ou remover entradas individuais da tabela de URL em um documento de serviço de dados. Depois de salvar suas alterações, os usuários que selecionarem o documento de serviço em uma nova operação de importação obterão os feeds de dados que você especificou.  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que usavam uma versão anterior do documento não são afetadas por nenhuma alteração que você faça. Isso ocorre porque um documento de serviço de dados é lido apenas uma vez durante a operação de importação inicial. Durante a importação, a URL do serviço e os nomes das tabelas são copiados e armazenados internamente na pasta de trabalho. Esses valores internos são usados em operações de atualização subsequentes para obter dados atualizados.  
  
 Como não há nenhum link persistente entre um documento de serviço de dados em um site do SharePoint e a pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que contém o feed importado, a modificação de qualquer parte de um documento de serviço de dados não tem nenhum efeito em pastas de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] existentes.  
  
> [!IMPORTANT]  
>  Embora o documento de serviço de dados seja lido apenas uma vez, os serviços de dados que fornecem os dados reais podem ser acessados em intervalos regulares para obter feeds mais recentes. Para obter mais informações sobre como atualizar dados, consulte [Atualização de dados do Power Pivot](../../analysis-services/power-pivot-sharepoint/power-pivot-data-refresh.md).  
  
##  <a name="usedsdoc"></a> Próxima etapa: Usar um documento de serviço de dados  
 Para usar um documento de serviço de dados criado em uma biblioteca do SharePoint, você usa a opção de importação **De Feeds de Dados** em uma fonte de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Para obter instruções mais, confira [Usar feeds de dados &#40;Power Pivot para SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/use-data-feeds-power-pivot-for-sharepoint.md).  
  
## <a name="see-also"></a>Consulte também  
 [Feeds de dados do Power Pivot](../../analysis-services/power-pivot-sharepoint/power-pivot-data-feeds.md)  
  
  
