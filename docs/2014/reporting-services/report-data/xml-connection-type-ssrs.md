---
title: Tipo de conexão do XML (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 5b55fff2-1b15-4156-83ef-15ad9cf9f509
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 4e47b2cc13c05438ce38d1b6f63bcbcb357c60d8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48211946"
---
# <a name="xml-connection-type-ssrs"></a>Tipo de conexão XML (SSRS)
  Para incluir dados em uma fonte de dados XML em seu relatório, é necessário ter um conjunto de dados baseado na fonte de dados do relatório do tipo XML. Esse tipo interno de fonte de dados é baseado na extensão de dados XML. Use esse tipo de fonte de dados para se conectar e recuperar dados de documentos XML, serviços Web ou XML inseridos na consulta.  
  
 Essa extensão de dados dá suporte a parâmetros e a credenciais gerenciados separadamente na cadeia de conexão.  
  
 Use as informações deste tópico para criar uma fonte de dados. Para obter instruções passo a passo, consulte [adicionar e verificar uma Conexão de dados ou uma fonte de dados &#40;construtor de relatórios e SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a> Cadeia de Conexão  
 A cadeia de conexão deve ser uma URL que aponta para o serviço Web, aplicativo com base na Web ou documento XML disponível no HTTP. Os documentos XML deve ter a extensão XML. Você também pode usar uma cadeia de conexão vazia para dados XML inseridos na consulta do conjunto de dados.  
  
 Os exemplos a seguir ilustram a sintaxe de cadeia de conexão para um serviço Web e documento XML, respectivamente. Não há suporte para o protocolo `file://` .  
  
|Tipo de documento XML|Exemplo de cadeia de conexão|  
|-----------------------|-------------------------------|  
|serviço Web|`http://adventure-works.com/results.aspx`|  
|Documento XML|`http://localhost/XML/Customers.xml`|  
|Documento XML inserido|*Empty (vazio)*|  
  
 Para obter mais exemplos de cadeias de conexão, consulte [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](../data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
##  <a name="Credentials"></a> Credenciais  
 As credenciais são necessárias para executar consultas, visualizar o relatório localmente e visualizá-lo no servidor de relatório.  
  
 Após a publicação do relatório, talvez seja necessário alterar as credenciais da fonte de dados para que, quando o relatório for executado no servidor de relatório, as permissões recuperadas sejam válidas.  
  
 Em um cliente de criação de relatório, as seguintes opções estão disponíveis para especificar credenciais:  
  
-   Usuário atual do Windows (também conhecido como segurança integrada).  
  
-   Nenhuma credencial é necessária. Se você não selecionar nenhuma credencial, o acesso Anônimo será usado. Verifique se você definiu a conta de execução autônoma do servidor de relatório para se conectar a uma fonte de dados externa. A extensão de processamento de dados XML não passa credenciais para a URL de destino nem para o serviço Web; a conexão não será bem-sucedida a menos que você tenha definido a conta de execução autônoma. Para obter mais informações, consulte [Configurar a conta de execução autônoma &#40;Gerenciador de Configurações do SSRS&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md) na documentação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nos [Manuais Online](http://go.microsoft.com/fwlink/?linkid=121312) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em msdn.microsoft.com.  
  
 Não há suporte para credenciais armazenadas nem solicitadas. Lembre-se de que, se você desabilitar a segurança integrada do Windows, não poderá usá-la para recuperar dados. Se você especificar as credenciais armazenadas ou solicitadas, ocorrerá um erro em tempo de execução.  
  
 Para obter mais informações, consulte [conexões de dados, fontes de dados e cadeias de caracteres de Conexão no Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) ou [especificar as credenciais no construtor de relatórios](../specify-credentials-in-report-builder.md).  
  
##  <a name="Query"></a> Consultas  
 Uma consulta especifica os dados a serem recuperados de um conjunto de dados de relatório. As colunas no conjunto de resultados para uma consulta populam a coleção de campos para um conjunto de dados. Um relatório só processa o primeiro conjunto de resultados recuperados por uma consulta.  
  
 Você deve usar o designer de consulta com base em texto para criar a consulta. A consulta deve retornar os dados XML.  
  
 Para obter mais informações sobre o designer de consultas baseado em texto, consulte [Interface do usuário do Designer de Consultas Baseado em Texto &#40;Construtor de Relatórios&#41;](text-based-query-designer-user-interface-report-builder.md).  
  
 Os valores possíveis para uma consulta de conjunto de dados de uma fonte de dados do tipo XML são mostrados abaixo.  
  
-   *Vazio*: Use uma consulta vazia para criar um conjunto de resultados padrão. A consulta padrão é criada lendo a fonte de dados e desviando a hierarquia do nó XML para a primeira coleção de folhas. O conjunto de resultados inclui todos os nós com valores de texto e todos os atributos de nó ao longo desse caminho. As colunas no conjunto de resultados são mapeadas para os campos no conjunto de dados.  
  
-   Um caminho de elemento: Especifica a sequência de nós a serem usadas ao recuperar dados XML da fonte de dados.  
  
-   Um elemento consulta XML: especificação do XML de uma consulta com os seguintes elementos opcionais:  
  
    -   **Para um serviço Web:**  
  
         Elementos XML obrigatórios:  
  
         `<Method Namespace=` *"namespace"*  `Name="MethodName" />`  
  
         `-- or --`  
  
         `<SoapAction>` *ação SOAP* `</SoapAction>`  
  
         Elementos XML opcionais:  
  
         `<ElementPath>`  *caminho do elemento*  `</ElementPath>`  
  
         `<Method Namespace=` *"namespace"*  `Name="MethodName" />`  
  
         `-- or --`  
  
         `<SoapAction>` *ação SOAP* `</SoapAction>`  
  
    -   **Para um documento XML:**  
  
         Elementos XML opcionais:  
  
         `<ElementPath>`  *caminho do elemento*  `</ElementPath>`  
  
    -   **Para um documento XML inserido:**  
  
         Elementos XML obrigatórios:  
  
         `<XmlData>` XML interno `</XmlData>`  
  
         Elementos XML opcionais:  
  
         `<ElementPath>`  *caminho do elemento*  `</ElementPath>`  
  
         `-- or --`  
  
         `<ElementPath IgnoreNamespaces="true">`  *caminho do elemento*  `</ElementPath>`  
  
 Para obter mais informações sobre sintaxe de consulta, consulte [Sintaxe de consulta XML para dados de relatório XML &#40;SSRS&#41;](report-data-ssrs.md) na documentação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nos [Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]](http://go.microsoft.com/fwlink/?linkid=121312) em msdn.microsoft.com.  
  
 Para obter exemplos, consulte [Reporting Services: Using XML and Web Service Data Sources](http://go.microsoft.com/fwlink/?LinkId=81654)[Reporting Services: usando fontes de dados XML e de serviço Web].  
  
### <a name="requirements-for-retrieving-xml-web-service-data"></a>Requisitos para recuperar os dados do serviço Web XML  
 A extensão de processamento de dados XML não detecta o esquema para você. Portanto, você deve ter alguma maneira de descobrir quais métodos SOAP recuperarão os dados desejados. Você também deve entender o namespace ou esquema de endereçamento que o serviço Web usa para seus dados.  
  
 Para um serviço Web, você pode fornecer um elemento <`Query`> que especifica um método a ser chamado ou ação SOAP. Você pode deixar a consulta em branco e usar a consulta padrão se os dados XML tiverem uma estrutura hierárquica que gera os dados que você deseja usar em seu relatório. Os atributos e valores de nó do elemento XML recuperados quando a consulta é executada são mapeados para os campos do conjunto de dados usados no seu relatório.  
  
### <a name="requirements-for-retrieving-xml-document-data"></a>Requisitos para recuperar os dados de documento XML  
 Usando o protocolo http, o servidor deve retornar dados XML ou os dados XML devem ser inseridos no elemento XML `Query`. Se você se referir a um documento XML diretamente usando o protocolo http, a extensão deverá ser .xml.  
  
 Você deve saber como criar uma consulta XML que recupere todos os dados necessários. Se você não especificara um caminho de elemento, o comportamento padrão para analisar um documento XML é selecionar o primeiro caminho disponível para uma coleção de nós folha no documento XML. Se o documento XML incluir caminhos adicionais para outras coleções de nós folha irmãs, esses nós serão ignorados a menos que você especifique um caminho em sua consulta.  
  
 Você pode fornecer um caminho de elemento usando a sintaxe XML semelhante a XQuery.  
  
 Para obter mais informações, consulte [Sintaxe caminho de elemento para dados de relatório XML &#40;SSRS&#41;](element-path-syntax-for-xml-report-data-ssrs.md) na documentação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nos [Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]](http://go.microsoft.com/fwlink/?linkid=121312) em msdn.microsoft.com.  
  
##  <a name="Parameters"></a> Parâmetros  
 A consulta não é analisada para identificar parâmetros.  
  
 Para adicionar parâmetros, você deve criá-los manualmente na página **Parâmetro** da caixa de diálogo [Propriedades do Conjunto de Dados](../dataset-properties-dialog-box-parameters-report-builder.md) .  
  
##  <a name="Remarks"></a> Comentários  
 A extensão de dados XML oferece suporte a relatórios de dados XML tabulares e não hierárquicos. Para obter mais informações, consulte [Adicionar dados de fontes de dados externas &#40;SSRS&#41;](add-data-from-external-data-sources-ssrs.md).  
  
 Não há suporte interno para recuperar documentos XML de um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
##  <a name="HowTo"></a> Tópicos de instruções  
 Esta seção contém instruções passo a passo para trabalhar com conexões de dados, fontes de dados e conjuntos de dados.  
  
 [Adicionar e verificar uma Conexão de dados ou uma fonte de dados &#40;relatórios e SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [Criar um conjunto de dados compartilhado ou um conjunto de dados inserido &#40;Construtor de Relatórios e SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [Adicionar um filtro a um conjunto de dados &#40;Construtor de Relatórios e SSRS&#41;](add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
##  <a name="Related"></a> Seções relacionadas  
 Estas seções da documentação fornecem informações conceituais detalhadas sobre dados de relatório, bem como informações de procedimentos sobre como definir, personalizar e usar partes de um relatório relacionadas aos dados.  
  
 [Adicionar dados a um relatório &#40;relatórios e SSRS&#41;](report-datasets-ssrs.md)  
 Fornece uma visão geral de como acessar dados de seu relatório.  
  
 [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
 Fornece informações sobre conexões de dados e fontes de dados.  
  
 [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Fornece informações sobre conjuntos de dados inseridos e compartilhados.  
  
 [Coleção de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)  
 Fornece informações sobre a coleção de campos de conjuntos de dados gerada pela consulta.  
  
 [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) na documentação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nos [Manuais Online](http://go.microsoft.com/fwlink/?linkid=121312) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
 Fornece informações detalhadas sobre suporte à plataforma e à versão para cada extensão de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
  
  
