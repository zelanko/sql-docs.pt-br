---
title: Tipo de conexão do OLE DB (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: d00cb13b-e1c2-4300-a195-3da1430a2df1
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 1cb3c7e8f9be785a93b29e453b5dfc727d747569
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53369568"
---
# <a name="ole-db-connection-type-ssrs"></a>Tipo de conexão OLE DB (SSRS)
  Para incluir dados de um provedor de dados OLE DB, é necessário ter um conjunto de dados baseado em uma fonte de dados de relatório do tipo OLE DB. Esse tipo de fonte de dados interna tem como base a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] extensão de processamento de dados OLE DB.  
  
 OLE DB é uma tecnologia de acesso a dados que permite aos clientes conectar-se a vários provedores de dados. Depois que você selecionar o tipo de fonte de dados OLE DB, deverá selecionar um provedor de dados específico. O suporte a recursos, como parâmetros e credenciais, depende do provedor de dados selecionado.  
  
 Use as informações deste tópico para criar uma fonte de dados. Para obter instruções passo a passo, consulte [adicionar e verificar uma Conexão de dados ou uma fonte de dados &#40;construtor de relatórios e SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a> Cadeia de Conexão  
 A cadeia de caracteres de conexão da extensão de processamento de dados OLE DB depende do provedor de dados desejado. Uma cadeia de caracteres de conexão típica contém pares de nome/valor que são suportados pelo provedor de dados. Por exemplo, a cadeia de caracteres de conexão a seguir especifica o provedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client e do banco de dados AdventureWorks:  
  
```  
Provider=SQLNCLI10.1;Data Source=server; Initial Catalog=AdventureWorks  
```  
  
 A cadeia de conexão utilizada depende da fonte de dados externa à qual você está se conectando. Para definir as propriedades da cadeia de caracteres de conexão específicas de um provedor de dados, na página **Geral** da caixa de diálogo **Propriedades da Fonte de Dados** , clique no botão **Construir** para abrir a caixa de diálogo **Propriedades da Conexão** . Defina propriedades de fonte de dados estendidas através da caixa de diálogo **Propriedades de Link de Dados** .  
  
 Para ver mais exemplos de cadeias de conexão, consulte [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](../data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
  
  
##  <a name="Credentials"></a> Credenciais  
 As credenciais são necessárias para executar consultas, visualizar o relatório localmente e visualizá-lo no servidor de relatório.  
  
 Após a publicação do relatório, talvez seja necessário alterar as credenciais da fonte de dados para que, quando o relatório for executado no servidor de relatório, as permissões recuperadas sejam válidas.  
  
 Para obter mais informações, consulte [conexões de dados, fontes de dados e cadeias de caracteres de Conexão no Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) ou [especificar as credenciais no construtor de relatórios](../specify-credentials-in-report-builder.md).  
  
###### <a name="special-characters-in-a-password"></a>Caracteres especiais em uma senha  
 Se você configurar a fonte de dados OLE DB para exigir uma senha ou para incluir uma senha na cadeia de conexão e um usuário inserir a senha com caracteres especiais, como sinais de pontuação, alguns drivers de fonte de dados subjacentes não conseguirão validar os caracteres especiais. Quando você processar o relatório, a mensagem "Senha inválida" poderá indicar esse problema.  
  
> [!NOTE]  
>  Não é recomendável a inclusão de informações de logon, como senhas, na cadeia de conexão. O Construtor de Relatórios fornece uma guia separada na caixa de diálogo **Fonte de Dados** que pode ser usada para inserir credenciais.  
  
  
  
##  <a name="Parameters"></a> Parâmetros  
 Alguns provedores OLE DB oferecem suporte a parâmetros não nomeados, e não a parâmetros nomeados. Os parâmetros são transmitidos por posição, através de um espaço reservado na consulta. O caractere de espaço reservado é determinado pela sintaxe suportada pelo provedor de dados.  
  
 
  
##  <a name="Remarks"></a> Comentários  
 OLEDB é uma tecnologia nativa para criação de provedores de dados para fontes de dados específicas. A tecnologia OLEDB é baseada em interfaces COM (Component Object Model). A tecnologia OLEDB é posterior à ODBC e anterior aos provedores de dados ADO.NET. Os provedores de dados OLEDB são registrados com o sistema operacional, como qualquer outro componente COM. Há provedores de dados OLEDB disponibilizados pela Microsoft e por fornecedores terceirizados. A Microsoft fornece também o MSDASQL, um provedor de dados OLEDB que faz a comunicação com drivers ODBC. Para obter mais informações, consulte [Tipo de conexão ODBC &#40;SSRS&#41;](odbc-connection-type-ssrs.md).  
  
 Para recuperar os dados desejados com êxito, é necessário fornecer uma sintaxe de consulta que seja suportada pelo provedor de dados. O suporte a parâmetros varia de acordo com o provedor de dados. Para obter mais informações, consulte os tópicos específicos do provedor de dados selecionado. Por exemplo:  
  
-   [Provedor OLE DB do Analysis Services &#40;Analysis Services – Dados Multidimensionais&#41;](../../analysis-services/dev-guide/analysis-services-ole-db-provider-analysis-services-multidimensional-data.md)  
  
-   [Usando o Provedor de Dados .NET Framework para Oracle](https://go.microsoft.com/fwlink/?LinkId=112314)  
  
-   [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
 Para obter mais informações sobre os provedores de dados específicos de OLE DB, consulte [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) na documentação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nos [Manuais Online](https://go.microsoft.com/fwlink/?linkid=121312) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
  
  
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
  
 [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) na documentação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nos [Manuais Online](https://go.microsoft.com/fwlink/?linkid=121312) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
 Fornece informações detalhadas sobre suporte à plataforma e à versão para cada extensão de dados.  
  
 
  
## <a name="see-also"></a>Consulte também  
 [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
  
  
