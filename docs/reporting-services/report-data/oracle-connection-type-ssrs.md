---
title: "Tipo de Conexão Oracle (SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 01/11/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9db86dd2-beda-42d8-8af7-2629d58a8e3d
caps.latest.revision: 10
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 4ce6a83437433c2254b2993f68f78e8c8c8f4375
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="oracle-connection-type-ssrs"></a>Tipo de conexão Oracle (SSRS)
Para usar dados de um banco de dados Oracle em seu relatório, é necessário ter um conjunto de dados baseado na fonte de dados do relatório do tipo Oracle. Esse tipo de fonte de dados interno usa o provedor de dados de Oracle diretamente e requer um componente de software cliente Oracle.

Para instalar as ferramentas de cliente Oracle, você pode fazer o seguinte.
 
1.  Vá para [site de download da Oracle](http://www.oracle.com/us/products/tools/index-090165.html)
2.  Baixe o ODAC 12c versão 4 (12.1.0.2.4) para Windows (64 bits para o servidor, 32 bits para ferramentas)
3.  Instalar o provedor de dados para o .NET 4
  
 Use as informações deste tópico para criar uma fonte de dados. Para obter instruções passo a passo, consulte [Adicionar e verificar uma conexão de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a> Cadeia de Conexão  
 Contate o administrador do banco de dados para obter informações sobre a conexão e as credenciais que devem ser usadas para se conectar à fonte de dados. O exemplo de cadeia de conexão a seguir especifica um banco de dados Oracle no servidor chamado “Oracle9” com Unicode. O nome do servidor deve coincidir com o que está definido no arquivo de configuração Tnsnames.ora como o nome da instância do servidor Oracle.  
  
```  
Data Source="Oracle"; Unicode="True"  
```  
  
 Para obter mais informações sobre exemplos de cadeias de conexão, consulte [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34).  
  
##  <a name="Credentials"></a> Credenciais  
 As credenciais são necessárias para executar consultas, visualizar o relatório localmente e visualizá-lo no servidor de relatório.  
  
 Após a publicação do relatório, talvez seja necessário alterar as credenciais da fonte de dados para que, quando o relatório for executado no servidor de relatório, as permissões recuperadas sejam válidas.  
  
 Para obter mais informações, consulte [Conexões de dados, fontes de dados e cadeias de conexão &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) ou [Especificar as credenciais no Construtor de Relatórios](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53).  
  
  
##  <a name="Query"></a> Consultas  
 Para criar um conjunto de dados, você pode selecionar um procedimento armazenado na lista suspensa ou criar uma consulta SQL. Para criar uma consulta, use o designer de consulta baseado em texto. Para obter mais informações, consulte [Interface de usuário de Designer de consulta baseado em texto &#40; Construtor de relatórios &#41; ](../../reporting-services/report-data/text-based-query-designer-user-interface-report-builder.md).  
  
 É possível especificar procedimentos armazenados que retornem apenas um conjunto de resultados. Não há suporte para o uso de consultas com base no cursor.  
  
##  <a name="Parameters"></a> Parâmetros  
 Se a consulta incluir variáveis de consulta, os parâmetros de relatório correspondentes serão gerados automaticamente. Essa extensão dá suporte a parâmetros nomeados. Para o Oracle versão 9 ou posterior, há suporte para parâmetros de vários valores.  
  
 Os parâmetros de relatório são criados com valores de propriedade padrão que talvez precisem ser modificados. Por exemplo, cada parâmetro de relatório é do tipo de dados **Texto**. Depois que os parâmetros de relatório forem criados, talvez seja necessário alterar os valores padrão. Para obter mais informações, consulte [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
  
##  <a name="Remarks"></a> Comentários  
 Para que você possa se conectar a uma fonte de dados Oracle, o administrador do sistema deve ter instalado a versão do .NET Data Provider for Oracle que dê suporte à recuperação de dados do banco de dados Oracle. O provedor de dados deve ser instalado no mesmo computador que o Construtor de Relatórios e também no servidor de relatório.  
  
 Para obter mais informações, consulte o seguinte:  
  
-   [Usando o Provedor de Dados .NET Framework para Oracle](http://go.microsoft.com/fwlink/?LinkId=112314) no msdn.microsoft.com  
  
-   [Como usar o Reporting Services para configurar e acessar uma fonte de dados Oracle](http://support.microsoft.com/kb/834305)  
  
-   [Como adicionar permissões à entidade de segurança de NETWORK SERVICE](http://support.microsoft.com/kb/870668)  
  
###### <a name="alternate-data-extensions"></a>Extensões de dados alternativas  
 Você também pode recuperar dados de um banco de dados Oracle com o uso de um tipo de fonte de dados OLE DB. Para obter mais informações, consulte [Tipo de conexão OLE DB &#40;SSRS&#41;](../../reporting-services/report-data/ole-db-connection-type-ssrs.md).  
  
###### <a name="report-models"></a>Modelos de relatório  
 Também é possível criar modelos com base em um banco de dados Oracle.  
  
###### <a name="platform-and-version-information"></a>Informações sobre plataforma e versão  
 Para obter mais informações sobre o suporte de plataforma e à versão, consulte [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md) na documentação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nos [Manuais Online](http://go.microsoft.com/fwlink/?linkid=121312) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
  
##  <a name="HowTo"></a> Tópicos de instruções  
 Esta seção contém instruções passo a passo para trabalhar com conexões de dados, fontes de dados e conjuntos de dados.  
  
 [Adicionar e verificar uma conexão de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [Criar um conjunto de dados compartilhado ou um conjunto de dados inserido &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [Adicionar um filtro a um conjunto de dados e &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="Related"></a> Seções relacionadas  
 Estas seções da documentação fornecem informações conceituais detalhadas sobre dados de relatório, bem como informações de procedimentos sobre como definir, personalizar e usar partes de um relatório relacionadas aos dados.  
  
 [Conjuntos de dados de relatório &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
 Fornece uma visão geral de como acessar dados de seu relatório.  
  
 [Conexões de dados, fontes de dados e cadeias de caracteres de Conexão no construtor de relatórios](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)  
 Fornece informações sobre conexões de dados e fontes de dados.  
  
 [Relatório inserido conjuntos de dados e conjuntos de dados compartilhados e &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Fornece informações sobre conjuntos de dados inseridos e compartilhados.  
  
 [Coleção de campos de conjunto de dados e &#40; Construtor de relatórios e SSRS & &#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 Fornece informações sobre a coleção de campos de conjuntos de dados gerada pela consulta.  
  
 [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md) na documentação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nos [Manuais Online](http://go.microsoft.com/fwlink/?linkid=121312) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
 Fornece informações detalhadas sobre suporte à plataforma e à versão para cada extensão de dados.  
  
  
## <a name="see-also"></a>Consulte também  
 [Parâmetros de relatório e &#40; Construtor de relatórios, Report Designer e &#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtro, grupo e classificar dados e &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Expressões &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  

