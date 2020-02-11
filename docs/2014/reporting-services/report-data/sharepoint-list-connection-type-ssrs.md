---
title: Tipo de conexão da lista do SharePoint (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 2c4adf2f-e9c4-4fae-bd3c-97fe64436caf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: cfa09322af5b4838ccdc2bb9dc85d13a412bc359
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66107074"
---
# <a name="sharepoint-list-connection-type-ssrs"></a>Conexões de conexão de lista do SharePoint (SSRS)
  Para incluir dados de uma lista do Microsoft SharePoint no relatório, você deve adicionar ou criar um conjunto de dados baseado em uma fonte de dados de relatório do tipo Lista do Microsoft SharePoint. Esse é um tipo de fonte de dados interna baseado na extensão de dados Lista do SharePoint do Microsoft SQL Server Reporting Services. Use esse tipo de fonte de dados para se conectar e recuperar dados de lista dos sites do [!INCLUDE[SPF2010](../../includes/spf2010-md.md)], [!INCLUDE[SPS2010](../../includes/sps2010-md.md)], do [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 3.0 e do [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007.  
  
 Use as informações deste tópico para criar uma fonte de dados. Para obter instruções detalhadas, consulte [Adicionar e verificar uma &#40;de conexão de dados ou fonte de dados Construtor de relatórios e SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a>Cadeia de conexão  
 A cadeia de conexão de uma lista do SharePoint é a URL para o site do SharePoint ou subsite, por exemplo, `http://MySharePointWeb/MySharePointSite` ou `http://MySharePointWeb/MySharePointSite/Subsite`.  
  
 O designer de consulta exibe automaticamente as listas do SharePoint às quais você tem permissões suficientes para acessar.  
  
 Para obter mais exemplos de cadeias de conexão, consulte [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](../data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
##  <a name="Credentials"></a>Fornecidas  
 As credenciais são necessárias para executar consultas, visualizar o relatório localmente e visualizá-lo no servidor de relatório. Após a publicação do relatório, talvez seja necessário alterar as credenciais da fonte de dados para que, quando o relatório for executado no servidor de relatório, as permissões recuperadas sejam válidas. Os tipos de credenciais que podem ser usados com essa extensão de dados dependem da configuração da tecnologia do SharePoint para a lista do SharePoint que você está usando como uma fonte de dados.  
  
 As tabelas a seguir esboçam o comportamento da recuperação de credenciais para a extensão de lista do SharePoint, ao conectar-se a uma lista de farm local do SharePoint e a uma lista remota do SharePoint.  
  
 A **tabela 1** é para relatórios implantados em um site herdado do Windows SharePoint. Um site herdado do Windows dá suporte apenas ao Kerberos, ao NTLM e à FBA (Autenticação Baseada em Formulários). A **tabela 2** é para relatórios implantados em um site do SharePoint baseado em declarações.  
  
 **Tabela 1**  
  
||Credenciais com suporte|Modo clássico de Autenticação do Windows|<sup>3</sup> autenticação de declarações|  
|-|---------------------------|-----------------------------------------|----------------------------------------|  
|Lista de farm local do SharePoint|Autenticação do Windows (integrada) ou token de usuário do SharePoint|Sim|Sim|  
||Armazenado, Prompt, Nenhum (com credenciais do Windows<sup>1</sup>)|Sim|Não|  
|Lista remota do SharePoint|Autenticação do Windows (integrada) ou token de usuário do SharePoint|Sim|Não<sup>2</sup>|  
||Armazenado, Prompt, Nenhum (com credenciais do Windows<sup>1</sup>)|Sim|Não<sup>2</sup>|  
  
 **Tabela 2**  
  
||Credenciais com suporte|Modo clássico de Autenticação do Windows|<sup>3</sup> autenticação de declarações|  
|-|---------------------------|-----------------------------------------|----------------------------------------|  
|Lista de farm local do SharePoint|Autenticação do Windows (integrada) ou token de usuário do SharePoint|Sim|Sim|  
||Armazenado, Prompt, Nenhum (com credenciais do Windows<sup>1</sup>)|Não|Não|  
|Lista remota do SharePoint|Autenticação do Windows (integrada) ou token de usuário do SharePoint|Sim|Não<sup>2</sup>|  
||Armazenado, Prompt, Nenhum (com credenciais do Windows<sup>1</sup>)|Não|Não<sup>2</sup>|  
  
 <sup>1</sup> não há suporte para credenciais armazenadas e de prompt com credenciais que não sejam do Windows.  
  
 <sup>2</sup> a autenticação baseada em formulários e a autenticação de declarações não têm suporte para listas remotas do SharePoint.  
  
 <sup>3</sup> a autenticação do Windows, a FBA (autenticação baseada em formulários), os tokens SAML (linguagem de marcação de aplicativo seguro), outros provedores de identidade ou uma combinação de mais de um dos provedores de autenticação mencionados acima.  
  
 **Autenticação do Windows**  
 Para uma tecnologia do SharePoint configurada para funcionar com um servidor de relatório no modo Conta Confiável, não há suporte a essa opção. Isso aplica-se apenas às versões anteriores do SQL Server 2012 Reporting Services.  
  
 Para uma tecnologia do SharePoint configurada para funcionar com um servidor de relatório no modo Windows Integrado, essa opção se aplica tanto ao usuário do Windows atual quanto ao usuário do SharePoint atual.  
  
 Para uma tecnologia do SharePoint configurada para funcionar sem um servidor de relatório (modo local), não há suporte a essa opção. Para saber mais sobre o modo local, confira relatórios em modo [local versus conectado no Visualizador de relatórios &#40;Reporting Services no modo do SharePoint&#41;](../local-vs-connected-mode-report-viewer-reporting-services-sharepoint-mode.md).  
  
 **As credenciais não são necessárias (não use credenciais):**  
 Para usar essa opção, a conta de execução autônoma deve ser configurada no servidor de relatório. Para obter mais informações, consulte [Configurar a conta de execução autônoma &#40;Configuration Manager do SSRS&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
 Para obter informações sobre o suporte à autenticação de declarações na pilha Microsoft BI, consulte [Usando a autenticação de declarações na pilha Microsoft BI](https://social.technet.microsoft.com/wiki/contents/articles/15274.using-claims-authentication-across-the-microsoft-bi-stack.aspx).  
  
 Para obter mais informações, consulte [conexões de dados, fontes de dados e cadeias de conexão em Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md), [especificar credenciais em Construtor de relatórios](../specify-credentials-in-report-builder.md)e [fontes de dados com suporte Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md).  
  
##  <a name="Query"></a>Procura  
 Para criar uma consulta, crie um novo conjunto de dados com base na fonte de dados e, em seguida, abra o designer de consulta associado. Para obter mais informações, consulte [Criar um conjunto de dados compartilhado ou um conjunto de dados inserido &#40;Construtor de Relatórios e SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md).  
  
 O designer de consulta gráfica de Lista do SharePoint exibe quatro painéis:  
  
 **Listas do SharePoint**  Exibe uma lista de todas as listas do SharePoint no site para esta fonte de dados. Selecione uma lista e os campos que você deseja na consulta. Os nomes de campos nesse painel são nomes amigáveis com o SharePoint, também conhecidos como nomes para exibição. Focalize um item para exibir as seguintes propriedades na dica de ferramenta:  
  
-   **Nome** do O nome exclusivo do campo.  
  
-   **Identificador** do O identificador exclusivo do campo.  
  
-   **Tipo de campo** O tipo de dados do campo.  
  
-   **Oculto** Especifica se o campo é exibido no modo de exibição de lista do SharePoint.  
  
 Não há suporte para a seleção de campos de várias listas. Você pode criar um conjunto de dados para cada lista e selecionar os campos de cada conjunto de dados. Se as listas tiverem um campo comum, você poderá usar a função Lookup em uma região de dados tablix que está vinculada a um conjunto de dados para recuperar um valor do outro conjunto de dados que não está vinculado à região de dados. Para obter mais informações, consulte [Função de pesquisa &#40;Construtor de Relatórios e SSRS&#41;](../report-design/report-builder-functions-lookup-function.md).  
  
-   **Campos selecionados**  Exibe os campos que você selecionou. Os nomes de campos nesse painel são nomes amigáveis especificados por um usuário do SharePoint. Quando fecha o designer de consulta, você visualiza esses nomes na coleção de campos do conjunto de dados no painel de dados do relatório. A relação entre nomes exclusivos e nomes amigáveis está disponível na página [Caixa de diálogo Propriedades do conjunto de dados, Campos &#40;Construtor de Relatórios&#41;](../dataset-properties-dialog-box-fields-report-builder.md).  
  
-   **Filtros aplicados**  Limita os dados retornados da lista do SharePoint antes que os dados sejam retornados ao relatório. Selecione o nome do campo, o operador e o valor a ser usado para limitar os dados recuperados na lista. Os operadores variam de acordo com o tipo de dados do valor selecionado.  
  
     Não é possível alterar a ordem de classificação, nem especificar grupos no designer de consulta gráfica. Para fazer isso, defina expressões de classificação no conjunto de dados do relatório e expressões de grupo nas regiões de dados no relatório. Não há suporte para os parâmetros de consulta. Para filtrar dados no relatório, use filtros de relatório ou parâmetros de relatório criados por você. Para obter mais informações, consulte [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md) e [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../report-design/report-parameters-report-builder-and-report-designer.md).  
  
-   **Resultados da consulta**  Exibe linhas de exemplo que são retornadas quando a consulta é executada. Se os valores da lista do SharePoint forem alterados com frequência no site do SharePoint, os valores que você visualiza no painel de resultados da consulta poderão ser diferentes dos valores exibidos no relatório.  
  
-   **Campos selecionados**  Exibe os campos que você selecionou. Os nomes de campos nesse painel são nomes amigáveis especificados por um usuário do SharePoint. Quando fecha o designer de consulta, você visualiza esses nomes na coleção de campos do conjunto de dados no painel de dados do relatório. A relação entre nomes exclusivos e nomes amigáveis está disponível na página [Caixa de diálogo Propriedades do conjunto de dados, Campos &#40;Construtor de Relatórios&#41;](../dataset-properties-dialog-box-fields-report-builder.md).  
  
-   **Filtros aplicados**  Limita os dados retornados da lista do SharePoint antes que os dados sejam retornados ao relatório. Selecione o nome do campo, o operador e o valor a ser usado para limitar os dados recuperados na lista. Os operadores variam de acordo com o tipo de dados do valor selecionado.  
  
     Não é possível alterar a ordem de classificação, nem especificar grupos no designer de consulta gráfica. Para fazer isso, defina expressões de classificação no conjunto de dados do relatório e expressões de grupo nas regiões de dados no relatório. Não há suporte para os parâmetros de consulta. Para filtrar dados no relatório, use filtros de relatório ou parâmetros de relatório criados por você. Para obter mais informações, consulte [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md) e [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../report-design/report-parameters-report-builder-and-report-designer.md).  
  
-   **Resultados da consulta**  Exibe linhas de exemplo que são retornadas quando a consulta é executada. Se os valores da lista do SharePoint forem alterados com frequência no site do SharePoint, os valores que você visualiza no painel de resultados da consulta poderão ser diferentes dos valores exibidos no relatório.  
  
 Para obter mais informações, consulte [Designer de consultas da lista do SharePoint &#40;Construtor de Relatórios&#41;](sharepoint-list-query-designer-report-builder.md).  
  
### <a name="query-text"></a>Texto da consulta  
 Para exibir a consulta gerada pelo designer de consulta gráfica, alterne para o designer de consulta baseado em texto. Nessa exibição, você pode visualizar o XML criado pelo designer de consulta gráfica. O XML inclui elementos para o nome da lista, a coleção de campos e o filtro.  
  
#### <a name="example-1-specified-fields-for-a-list"></a>Exemplo 1. Campos especificados para uma lista  
 O seguinte exemplo mostra uma consulta do SharePoint bem formada:  
  
```  
<RSSharePointList>  
<listName>MyList</listName>  
<viewFields>  
  <FieldRef Name="Field1"/>  
  <FieldRef Name="Field4"/>  
</viewFields>  
<Query>  
  <Where>  
    <And>  
      <Gt>  
        <FieldRef Name="Field1"/>  
        <Value Type="Integer">1</Value>  
      </Gt>  
      <IsNotNull>  
        <FieldRef Name="Field2"/>  
        <Value Type="string"/>  
      </IsNotNull>   
    </And>  
  </Where>  
</Query>  
</RSSharePointList>  
```  
  
 Você pode editar essa exibição da consulta, desde que ela permaneça como texto XML bem formado.  
  
#### <a name="example-2-all-fields-for-a-list"></a>Exemplo 2. Todos os campos de uma lista  
 Também é possível especificar somente o nome de uma lista, e todos os campos, inclusive campos ocultos, são retornados. O seguinte exemplo recupera todos os campos de uma lista denominada Tarefas:  
  
```  
<RSSharePointList>  
<listName>Tasks</listName>  
</RSSharePointList>  
```  
  
 Todos os campos da lista Tarefas são retornados nos resultados da consulta.  
  
##  <a name="Parameters"></a> Parâmetros  
 Essa extensão de dados não dá suporte a parâmetros.  
  
  
##  <a name="HowTo"></a> Tópicos de instruções  
 Esta seção contém instruções passo a passo para trabalhar com conexões de dados, fontes de dados e conjuntos de dados.  
  
 [Adicionar e verificar uma conexão de dados ou uma fonte de dados &#40;Construtor de Relatórios e SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [Criar um conjunto de um DataSet compartilhado ou um conjunto de &#40;inserido Construtor de Relatórios e SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [Adicionar um filtro a um conjunto de &#40;Construtor de Relatórios e SSRS&#41;](add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="Related"></a>Seções relacionadas  
 Estas seções da documentação fornecem informações conceituais detalhadas sobre dados de relatório, bem como informações de procedimentos sobre como definir, personalizar e usar partes de um relatório relacionadas aos dados.  
  
 [Adicionar dados a um relatório &#40;Construtor de Relatórios e SSRS&#41;](report-datasets-ssrs.md)  
 Fornece uma visão geral de como acessar dados de seu relatório.  
  
 [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
 Fornece informações sobre conexões de dados e fontes de dados.  
  
 [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Fornece informações sobre conjuntos de dados inseridos e compartilhados.  
  
 [Coleção de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)  
 Fornece informações sobre a coleção de campos de conjuntos de dados gerada pela consulta.  
  
 [Fontes de dados com suporte pelo Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) na [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] documentação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do nos [manuais online](https://go.microsoft.com/fwlink/?linkid=121312)do.  
 Fornece informações detalhadas sobre suporte à plataforma e à versão para cada extensão de dados.  
  
  
## <a name="see-also"></a>Consulte Também  
 [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
  
  
