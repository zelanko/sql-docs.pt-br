---
title: Interface de usuário do Designer de consulta baseado em texto | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10010"
- sql12.rtp.rptdesigner.dataview.genericquerydesigner.f1
helpviewer_keywords:
- text-based query designer [Reporting Services]
- query designers [Reporting Services], text-based
ms.assetid: 44b7c664-03aa-494e-a484-052b318e810c
author: maggiesmsft
ms.author: maghan
manager: kfile
ms.openlocfilehash: 61c57d661a9865c9ced6912af921dd45b9e1db74
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56012387"
---
# <a name="text-based-query-designer-user-interface"></a>Interface de usuário do Designer de Consulta baseado em texto
  Use o designer de consulta baseado em texto para especificar uma consulta usando o idioma de consulta suportado pela fonte de dados, execute a consulta e exiba os resultados no tempo de design. Você pode especificar várias instruções do [!INCLUDE[tsql](../includes/tsql-md.md)] , consulta ou sintaxe de comando para as extensões de processamento de dados e consultas que são especificadas como expressões. Como o designer de consulta baseado em texto não processa previamente a consulta e pode acomodar qualquer tipo de sintaxe de consulta, esta é a ferramenta de designer de consulta padrão para muitos tipos de fontes de dados.  
  
 O designer de consulta baseado em texto exibe uma barra de ferramentas e os dois painéis a seguir:  
  
-   **Consulta** mostra o texto da consulta, o nome da tabela ou o nome do procedimento armazenado.  
  
-   **Resultado** Mostra os resultados da execução da consulta em tempo de design.  
  
## <a name="text-based-query-designer-toolbar"></a>Barra de ferramentas do Designer de Consulta baseado em texto  
 O designer de consulta baseado em texto fornece uma única barra de ferramentas para todos os tipos de comando. A tabela a seguir lista cada botão da barra de ferramentas e suas respectivas funções.  
  
|Botão|Descrição|  
|------------|-----------------|  
|**Editar como Texto**|Alterna entre o designer de consulta baseado em texto e o designer de consultas gráficas. Nem todos os tipos de fonte de dados dão suporte aos designers de consultas gráficas.|  
|**Importar**|Importa uma consulta existente de um arquivo ou relatório. Apenas os tipos de arquivo .sql e .rdl têm suporte. Para obter mais informações, consulte [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).|  
|![Executar a consulta](../analysis-services/media/rsqdicon-run.gif "Executar a consulta")|Executa a consulta e exibe o conjunto de resultados no painel Resultado.|  
|**Tipo de Comando**|Selecione **Text**, **StoredProcedure**ou **TableDirect**. Se um procedimento armazenado tiver parâmetros, a caixa de diálogo **Definir Parâmetros de Consulta** será aberta quando você clicar em **Executar** na barra de ferramentas e os valores poderão ser preenchidos conforme necessário. Observe que, se um procedimento armazenado retornar mais de um conjunto de resultados, somente o primeiro conjunto de resultados é usado para preencher o conjunto de dados.<br /><br /> O suporte para o tipo de comando varia de acordo com o tipo da fonte de dados. Por exemplo, somente OLE DB e ODBC dão suporte a **TableDirect**.|  
  
### <a name="command-type-text"></a>Tipo de comando Text  
 Ao criar uma consulta do conjunto de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], por padrão, o Designer de Relatórios exibirá o designer de consultas gráficas. Para mudar para o designer de consulta baseado em texto, clique no botão de alternância **Editar como Texto** na barra de ferramentas. O designer de consulta baseado em texto apresenta dois painéis: Consulta e Resultado. A imagem a seguir define cada painel.  
  
 ![Designer de consultas genérico para consulta de dados relacionais](../analysis-services/media/rsqd-dsaw-sql-generic.gif "Designer de consultas genérico para consulta de dados relacionais")  
  
 A tabela a seguir descreve a função de cada painel.  
  
|Painel|Função|  
|----------|--------------|  
|Consulta|Exibe o texto da consulta do [!INCLUDE[tsql](../includes/tsql-md.md)] . Use esse painel para gravar ou editar uma consulta do [!INCLUDE[tsql](../includes/tsql-md.md)] .|  
|Resultado|Exibe os resultados da consulta. Para executar a consulta, clique com o botão direito do mouse em qualquer painel e clique em **Executar**ou clique no botão **Executar** na barra de ferramentas.|  
  
#### <a name="example"></a>Exemplo  
 A consulta a seguir retorna a lista de sobrenomes da tabela `Contact` do banco de dados [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)].  
  
```  
SELECT LastName FROM Person.Person;  
```  
  
 Você pode usar qualquer instrução do [!INCLUDE[tsql](../includes/tsql-md.md)] para o Tipo de Comando Text, incluindo as instruções `EXEC`. A consulta a seguir chama o [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] procedimento armazenado `uspGetEmployeeManagers` e retorna a cadeia de comando para o funcionário com o número de identificação 1.  
  
```  
EXEC uspGetEmployeeManagers 1;  
```  
  
 Ao clicar em **Executar** , na barra de ferramentas, o comando no painel **Consulta** será executado e os resultados serão exibidos no painel **Resultado** .  
  
### <a name="command-type-storedprocedure"></a>Tipo de comando StoredProcedure  
 Quando você seleciona o **Comando typeStoredProcedure**, o designer de consulta baseado em texto apresenta dois painéis: Consulta e Resultado. Insira o nome do procedimento armazenado no painel Consulta e clique em **Executar** na barra de ferramentas. A caixa de diálogo Definir Parâmetros de Consulta é exibida. Insira os valores dos parâmetros do procedimento armazenado. Um parâmetro de relatório é criado para cada parâmetro de procedimento armazenado.  
  
#### <a name="example"></a>Exemplo  
 A consulta a seguir chama o procedimento armazenado `uspGetEmployeeManagers` do [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]. Você deve inserir um valor para o parâmetro do número de identificação do funcionário quando executar a consulta.  
  
```  
uspGetEmployeeManagers;  
```  
  
### <a name="command-type-tabledirect"></a>Tipo de comando TableDirect  
 Quando você seleciona o **Comando typeTableDirect**, o designer de consulta baseado em texto apresenta dois painéis: Consulta e Resultado. Se você inserir uma tabela e clicar no botão **Executar** , todas as colunas dessa tabela serão retornadas.  
  
#### <a name="example"></a>Exemplo  
 A consulta a seguir retorna um conjunto de resultados para todos os clientes no banco de dados [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)].  
  
 `Sales.Customer`  
  
 Quando você insere o nome da tabela Sales. Customer, é o equivalente a criar o [!INCLUDE[tsql](../includes/tsql-md.md)] instrução `SELECT * FROM Sales.Customer;`.  
  
## <a name="see-also"></a>Consulte também  
 [Ferramentas de Design no Designer do SQL Server Data Tools de relatório de consulta &#40;SSRS&#41;](report-data/query-design-tools-ssrs.md)   
 [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [O tipo de conexão do SQL Server &#40;SSRS&#41;](report-data/sql-server-connection-type-ssrs.md)   
 [Tipo de conexão OLE DB &#40;SSRS&#41;](report-data/ole-db-connection-type-ssrs.md)   
 [Tipo de Conexão do ODBC &#40;SSRS&#41;](report-data/odbc-connection-type-ssrs.md)   
 [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Arquivo de configuração RSReportDesigner](report-server/rsreportdesigner-configuration-file.md)  
  
  
