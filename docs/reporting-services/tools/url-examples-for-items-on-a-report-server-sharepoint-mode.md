---
title: Exemplos de URL para itens em um servidor de relatório – modo do SharePoint | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: tools
ms.topic: conceptual
ms.assetid: 54cb861a-8cec-445c-875d-599fb9bd1973
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7b787bdccdb913bd95051c8e3a4a3dd37fed5c01
ms.sourcegitcommit: 9ece10c2970a4f0812647149d3de2c6b75713e14
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51812949"
---
# <a name="url-examples-for-items-on-a-report-server---sharepoint-mode"></a>Exemplos de URL para itens em um servidor de relatório – modo do SharePoint
  Para publicar relatórios e itens relacionados em uma biblioteca do SharePoint, você pode publicar o conteúdo por meio das ferramentas de criação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , como o Designer de Relatórios ou carregar o conteúdo por meio das ações do site do SharePoint.  
  
 Os sites do SharePoint usam endereços da Web diferentes do que um servidor de relatório [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em modo nativo. A hierarquia da Web do site do SharePoint inclui o aplicativo do SharePoint Web, um site de alto nível, subsites opcionais e bibliotecas. Você deve saber criar uma URL que especifique o servidor do SharePoint, bem como o local na hierarquia do site do SharePoint em que você deseja publicar um relatório ou itens relacionados.  
  
 Os itens relacionados a um relatório incluem fontes de dados compartilhadas, sub-relatórios, relatórios detalhados e recursos como arquivos de imagem com base na Web. Um relatório que tenha sido publicado em uma biblioteca do SharePoint deve especificar esses itens relacionados por local na biblioteca do SharePoint.  
  
 Use os exemplos deste tópico para ajudar a criar URLs para relatórios e itens relacionados em suas soluções de relatório.  
  
## <a name="site-hierarchy"></a>Hierarquia do site  
 Ao configurar um servidor de relatório para ser executado no modo integrado do SharePoint, a hierarquia da Web do SharePoint é usada para direcionar os itens que serão processados e gerenciados no servidor de relatório.  
  
 Podem ser usados os seguintes elementos da hierarquia da Web para acessar e proteger o conteúdo do servidor de relatório. Outros objetos, como listas e páginas, não são usados para acessar o conteúdo do servidor de relatório e, portanto, não estão descritos na tabela seguinte.  
  
|Object|Descrição|  
|------------|-----------------|  
|Aplicativo Web do SharePoint|Um aplicativo da Web do SharePoint pode ser instalado como um servidor autônomo ou em um farm que tenha uma coleção de servidores virtuais. Um aplicativo Web tem uma URL (por exemplo, `http:*//servername*`) e pode conter vários sites.|  
|Site|Um site é um site pai de um aplicativo da Web ou um subsite.|  
|Biblioteca do SharePoint|Uma biblioteca contém documentos ou pastas. Uma biblioteca ou pasta em uma biblioteca é o único objeto do site que pode armazenar relatórios, modelos de relatório, fontes de dados compartilhadas e imagens externas.|  
|Item|Os itens do servidor de relatório que podem ser descritos em uma URL incluem uma definição de relatório para um relatório ou sub-relatório, um modelo de relatório, uma fonte de dados compartilhada ou uma imagem externa.|  
  
## <a name="url-syntax-and-rules"></a>Sintaxe de URL e regras  
 Cada item do servidor de relatório em uma biblioteca é identificado por uma URL totalmente qualificada que inclui um prefixo de protocolo, nome do servidor, biblioteca, nome do arquivo e extensão do nome do arquivo para o tipo de arquivo.  
  
### <a name="url-for-a-sharepoint-server"></a>URL para um servidor SharePoint  
 Você deve usar uma URL para o servidor SharePoint ao implantar um Servidor de Relatório ou um projeto de Modelo de Relatório do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] no servidor de relatório.  
  
 Para localizar o nome do servidor a ser usado, abra o navegador e localize a biblioteca do SharePoint onde deseja publicar um relatório. O nome do servidor é exibido imediatamente após o prefixo do protocolo, por exemplo, `http:*//servername*`.  
  
 Usando o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , o ponto de extremidade do proxy de URL não tem suporte. Um ponto de extremidade de proxy inclui um número da porta, por exemplo, `http:*//servername:8080/reportserver*`.  
  
### <a name="url-for-a-sharepoint-server-site-or-subsite"></a>URL para um site ou subsite de servidor do SharePoint  
 Ao implantar uma fonte de dados de relatório, você deve usar uma URL para um site e subsite do SharePoint, caso haja um. Na URL, o nome do site é exibido imediatamente após o nome do servidor, por exemplo, `https://*servername/site*` ou `https://*servername/site/subsite*`.  
  
 Em um aplicativo Web do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007 ou do [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] , o site e o subsite com frequência correspondem às guias no site principal. Para localizar o nome do site ou do subsite, clique em **Página Inicial**e, em seguida, **Todo Conteúdo do Site**. Role para a parte inferior e procure por **Sites e Workspaces**. A lista dos sites aparece nesta seção.  
  
### <a name="url-for-a-sharepoint-library"></a>URL para uma biblioteca do SharePoint  
 Ao implantar um relatório ou um item relacionado à biblioteca do SharePoint, você deve usar uma URL para biblioteca do SharePoint. A URL usada para uma biblioteca difere dependendo da versão do SharePoint que você está usando.  
  
 No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 3.0 ou [!INCLUDE[SPF2010](../../includes/spf2010-md.md)], a biblioteca é exibida após o nome do servidor, por exemplo, `https://*servername/*Shared Documents`.  
  
 No [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007 ou no [!INCLUDE[SPS2010](../../includes/sps2010-md.md)], a biblioteca aparece depois do site e do subsite. Por exemplo, `https://*servername/site/*Documents`.  
  
 Para localizar as informações de caminho para uma nova biblioteca do SharePoint ou para um site desconhecido, abra o navegador e localize a biblioteca do SharePoint onde deseja publicar seus relatórios. Se a biblioteca estiver vazia, carregue qualquer arquivo. Clique com o botão direito do mouse no arquivo e selecione **Propriedades** para abrir a janela **Propriedades** . O endereço do arquivo contém os valores da URL necessários para a publicação.  
  
### <a name="fully-qualified-urls-for-items-on-a-sharepoint-site"></a>URLs completamente qualificados para os itens em um site do SharePoint  
 Os itens armazenados em uma biblioteca do SharePoint são sempre endereçados por meio de uma URL totalmente qualificada que começa com o aplicativo Web (`https://*server*`) como o nó raiz e termina com o nome do arquivo que está sendo referenciado.  
  
 Os nomes de arquivo na URL devem incluir uma extensão de nome de arquivo.  
  
 Você não pode usar URLs relativas para itens dependentes nos relatórios que você publica em um site do SharePoint. Por exemplo, você não pode usar uma URL relativa para mencionar uma fonte de dados compartilhada, modelo de relatório ou sub-relatório. Você sempre tem que especificar a URL totalmente qualificada a uma biblioteca do SharePoint para cada item. Não há com prever onde um arquivo dependente pode estar localizado, pois não há uma hierarquia predefinida para os sites que você pode usar para analisar um formato de URL.  
  
 Ao publicar ou carregar um relatório que tenha itens dependentes, você deve definir as referências aos itens dependentes após o relatório ser publicado. Não há garantia de que as referências que funcionaram corretamente no modo de visualização no Designer de Relatórios funcionem após o relatório ser publicado. Para obter mais informações, consulte neste tópico [Publicando de uma ferramenta de criação para uma biblioteca do SharePoint](#publishingToDocLib) .  
  
### <a name="urls-for-external-images"></a>URLs para imagens externas  
 Uma definição de relatório pode incluir um arquivo de imagem armazenado como um arquivo externo. Você pode mencionar aquele arquivo na definição de relatório, definindo uma URL totalmente qualificada para um arquivo de imagem. Pode ser armazenado em um site do SharePoint ou em um computador remoto.  
  
> [!IMPORTANT]  
>  Se a URL externa for referente a uma imagem contida em um site do SharePoint, o ícone de imagem quebrada aparecerá quando você visualizar o relatório no Construtor de Relatórios. Quando você carregar o relatório no site do SharePoint e o renderizar no modo conectado, o ícone de imagem quebrada aparecerá se você tiver apenas as permissões **View Items** .  
  
 Independentemente do modo do servidor de relatório, as referências a um arquivo de imagem externa em um relatório devem se uma URL totalmente qualificada. Também, a referência a um arquivo de imagem externa, geralmente, exige que você configure a conta de processamento de relatório autônomo.  
  
### <a name="specifying-subreports-and-drillthrough-reports"></a>Especificando sub-relatórios e relatórios detalhados  
 Os sub-relatórios devem residir na mesma pasta que o relatório principal. Não é possível especificar uma pasta relativa.  
  
 Para especificar relatórios detalhados, inclua a URL em uma expressão. Por exemplo, para especificar o relatório denominado SalesDetails como um relatório detalhado, na caixa de texto ou no texto do espaço reservado Ação para, defina ReportName para a seguinte expressão:  
  
```  
="https://site/subsite/documentlibrary/SalesDetails.rdl"  
```  
  
### <a name="reserved-names-on-sharepoint-sites"></a>Nomes reservados nos sites do SharePoint  
 Se você está criando ou construindo uma URL para um item localizado em um site do SharePoint, saiba que ambas as palavras **Pessoal** e **Sites** são nomes reservados no site padrão.  
  
## <a name="examples-of-urls"></a>Exemplos de URLs  
 Ao publicar itens a uma biblioteca do SharePoint, você deve especificar as URLs totalmente qualificadas à biblioteca de destino. Uma URL totalmente qualificada do SharePoint inclui o aplicativo da Web do SharePoint, o site, a biblioteca, a pasta (opcional), o arquivo e a extensão de nome de arquivo. Os exemplos seguintes fornecem diversas ilustrações da sintaxe que você deve usar.  
  
|Destino|Exemplo de URL|  
|------------|-----------------|  
|Um servidor do SharePoint.|`https://TestServer`|  
|Um site ou subsite do servidor do SharePoint.|`https://TestServer/toplevelsite/subsite`|  
|O relatório de exemplo de vendas da empresa em **Documentos Compartilhados** em uma implantação do [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] ou do [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] .|`https://TestServer/TestSite/Shared%20Documents/Company%20Sales.rdl`|  
|O relatório de exemplo Company Sales na pasta **Documents/Doc** em uma instância do [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] ou do [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] .|`https://TestServer/TestSite/Documents/Doc/Company%20Sales.rdl`|  
|O relatório de exemplo de vendas da empresa na **Central de Relatórios** em uma instância do [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] ou do [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] .|`https://TestServer/TestSite/Reports/Doc/Company%20Sales.rdl`|  
  
##  <a name="publishingToDocLib"></a> Publicando de uma ferramenta de criação para uma biblioteca do SharePoint  
 Quando você usa a ferramenta de criação de relatório para publicar relatórios e arquivos relacionados em uma biblioteca, os arquivos são validados antes de serem adicionados. Se você carregar os relatórios e os arquivos relacionados, usando a ação **Carregar** na biblioteca do SharePoint, nenhuma validação ocorrerá. Você não saberá se o arquivo é válido até acessar o relatório, gerenciando, editando ou executando-o.  
  
> [!NOTE]  
>  Para publicar relatórios em um site do SharePoint pelo [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], é necessário adicionar esse site do SharePoint à lista de locais confiáveis no navegador Internet Explorer.  
  
### <a name="shared-data-sources"></a>Fontes de dados compartilhadas  
 Ao publicar um fonte de dados compartilhada a partir de uma ferramenta de criação, você define a propriedade do projeto **TargetDataSourceFolder**. A pasta de destino da fonte de dados deve ser uma URL em uma biblioteca do SharePoint. Ao contrário do modo nativo no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , não é possível especificar uma pasta relativa e caminhos relativos não são válidos. Se não existir uma pasta no caminho da Biblioteca de Documentos, será criada uma.  
  
 Ao publicar um arquivo de fonte de dados compartilhada (.rds) em um site do SharePoint, um arquivo de fonte de dados compartilhada é alterada para uma extensão de nome de arquivo .rsds. O .arquivo rsds não poderá ser salvo no local de um site do SharePoint e importado em um projeto existente [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . As fontes de dados compartilhadas com as extensões de nome de arquivo .rds e .rsds não são intercambiáveis.  
  
#### <a name="shared-data-sources-from-report-designer"></a>Fontes de dados compartilhadas do Designer de Relatórios  
 Se você estiver publicando fontes de dados compartilhadas de um projeto de Designer de Relatórios, poderá usar uma URL que especifique a biblioteca de destino ou poderá deixar a propriedade em branco. Ao contrário do modo nativo no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , não é possível especificar uma pasta relativa e caminhos relativos não são válidos. Se não existir uma pasta no caminho da Biblioteca de Documentos, será criada uma. Se você deixar em branco a pasta de destino da fonte de dados, a fonte de dados será publicada na pasta de relatório de destino.  
  
### <a name="file-names"></a>Nomes de arquivos  
 Os nomes de arquivos em uma URL para itens de relatório devem incluir uma extensão de nome de arquivo. A extensão do nome do arquivo determina o tipo de arquivo. Ao publicar itens de relatórios de uma ferramenta de criação de relatório, a extensão do nome do arquivo é incluída automaticamente. Se você carregar um item de relatório para uma biblioteca do SharePoint, deverá incluir uma extensão do nome do arquivo.  
  
 Se você não especificar uma extensão do nome do arquivo para os itens que carregou para um site do SharePoint, o erro **rsInvalidDataSourceReference** irá ocorrer. Os nomes dos arquivos não devem incluir caracteres não reconhecidos como caracteres de nome de arquivo válidos pelos aplicativos do SharePoint. Não inclua os seguintes caracteres: # % & * : < > ? / { | }.  
  
## <a name="differences-between-uploading-and-publishing"></a>Diferenças entre carregamento e publicação  
 Quando você usa o Designer de Relatórios ou o Construtor de Relatórios para publicar relatórios e arquivos relacionados em uma biblioteca, os arquivos são validados antes de serem adicionados. Se você carregar os relatórios e os arquivos relacionados, usando a ação **Carregar** na biblioteca do SharePoint, nenhuma validação ocorrerá. Você não saberá se o arquivo é válido até acessar o relatório, gerenciando, editando ou executando-o.  
  
## <a name="updating-a-published-item"></a>Atualizando um item publicado  
 Após ter publicado ou carregado um item para uma biblioteca, você deve verificar o item da biblioteca antes de atualizá-lo. Enquanto o relatório é verificado, você será o único usuário a ter permissão para alterar o relatório. Quando tiver acabado, faça o check-in do arquivo.  
  
 Se você carregar ou publicar um relatório sem verificar o documento primeiro (por exemplo, carregando um item que tenha o mesmo nome que um item existente), o servidor de relatório irá verificar para você, adicionará o relatório atualizado como uma nova versão do item existente e, em seguida, fará o check-in do documento.  
  
## <a name="external-images-as-resources"></a>Imagens externas como recursos  
 Um servidor de relatório que está sendo executado no modo nativo oferece suporte ao conceito de um recurso, o qual é definido como qualquer arquivo armazenado e protegido no servidor de relatório, mas não é processado pelo servidor de relatório. Em modo nativo, pode haver qualquer tipo de arquivo.  
  
 Quando um servidor de relatório é executado no modo integrado do SharePoint, o conceito de um recurso tem uma definição mais restrita. O servidor de relatório retém o conceito de um recurso para armazenar relatórios referentes a uma imagem externa. Isso se aplicará se o relatório for um instantâneo ou uma cópia, mantidos para uso interno.  
  
## <a name="see-also"></a>Consulte Também  
 [Publicar um relatório em uma biblioteca do SharePoint](../../reporting-services/reports/publish-a-report-to-a-sharepoint-library.md)   
 [Publicar uma fonte de dados compartilhada em uma biblioteca do SharePoint](../../reporting-services/reports/publish-a-shared-data-source-to-a-sharepoint-library.md)   
 [Caixa de diálogo Páginas de Propriedades do Projeto](../../reporting-services/tools/project-property-pages-dialog-box.md)  
  
  
