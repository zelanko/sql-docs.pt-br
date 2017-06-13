---
title: "Interface de usuário do Designer de consulta gráfica | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10012"
- sql13.rtp.rptdesigner.dataview.vdtquerydesigner.f1
helpviewer_keywords:
- graphical query designer [Reporting Services]
- data sources [Reporting Services], creating
- text-based query designer [Reporting Services]
- query designers [Reporting Services]
- Reporting Services, query designers
ms.assetid: 5022ae33-03a3-48de-8ac1-82742f48cebe
caps.latest.revision: 54
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3c3bc432fc4dd02527f617b920cdf045103247a9
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="graphical-query-designer-user-interface"></a>Interface de usuário do Designer de consultas gráficas
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] oferece um designer de consultas gráficas e um designer de consultas baseadas em texto; com eles, é possível criar consultas e recuperar dados de um banco de dados relacional relativos a um conjunto de dados de relatório no Designer de Relatórios. Use o designer de consultas gráficas para criar uma consulta interativamente e ver os resultados de tipos de fonte de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle, OLE DB e ODBC. Use o designer de consultas baseadas em texto para especificar várias instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] , consulta complexa ou sintaxe de comando e consultas baseadas em expressões. Para obter mais informações, consulte [Interface do usuário do Designer de Consultas baseado em texto](http://msdn.microsoft.com/library/44b7c664-03aa-494e-a484-052b318e810c). Para obter mais informações sobre como trabalhar com tipos de fontes de dados específicos, consulte [Conjuntos de dados de relatório &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md).  
  
 .  
  
## <a name="graphical-query-designer"></a>Designer de Consultas Gráficas  
 Este designer de consultas gráficas dá suporte a três tipos de comandos de consulta: **Text**, **StoredProcedure**ou **TableDirect**. Antes de criar uma consulta para seu conjunto de dados, selecione uma opção de tipo de comando na página Consulta da caixa de diálogo [Propriedades do Conjunto de Dados](http://msdn.microsoft.com/library/1fa34a4b-7de0-4e92-99fa-bc28a206773f) .  
  
 As seguintes opções estão disponíveis para o tipo de consulta:  
  
-   **Text** Supports standard [!INCLUDE[tsql](../../includes/tsql-md.md)] query text for relational database data sources, including data processing extensions for [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] and Oracle.  
  
-   **TableDirect** Seleciona todas as colunas da tabela especificada. Por exemplo, para uma tabela chamada Clientes, isso equivale à instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] `SELECT * FROM Customers`.  
  
-   **StoredProcedure** Dá suporte a chamadas para procedimentos armazenados na fonte de dados. Para usar esta opção, é necessário que você tenha recebido do administrador de banco de dados as permissões de execução no procedimento armazenado na fonte de dados.  
  
 O tipo de comando padrão é **Text**.  
  
> [!NOTE]  
>  Nem todas as extensões de processamento de dados dão suporte a todos os tipos. O provedor de dados subjacente deve dar suporte a um tipo de comando para que as opções fiquem disponíveis.  
  
### <a name="command-type-text"></a>Tipo de comando Text  
 No tipo **Text** , o designer de consultas gráficas apresenta quatro áreas, ou painéis. É possível especificar colunas, aliases, valores de classificação e valores de filtro para uma consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] . Você pode exibir o texto da consulta gerado a partir das seleções feitas, executar a consulta e ver o conjunto de resultados. A figura a seguir mostra os quatro painéis.  
  
 ![Designer de consultas gráficas para consulta sql](../../reporting-services/report-data/media/rsqd-dsaw-sql.gif "designer de consultas gráficas para consulta sql")  
  
 A tabela a seguir descreve a função de cada painel.  
  
|Painel|Função|  
|----------|--------------|  
|Diagrama|Exibe representações gráficas das tabelas da consulta. Use este painel para selecionar campos e definir relações entre tabelas.|  
|Grade|Exibe uma lista dos campos retornados pela consulta. Use este painel para definir aliases, ordem de classificação, filtros, grupos e parâmetros.|  
|SQL|Exibe a consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] representada pelos painéis Diagrama e Grade. Use este painel para gravar ou atualizar uma consulta usando [!INCLUDE[tsql](../../includes/tsql-md.md)].|  
|Resultado|Exibe os resultados da consulta. Para executar a consulta, clique com o botão direito do mouse em qualquer painel e clique em **Executar**ou no botão **Executar** da barra de ferramentas.|  
  
 Quando você altera as informações contidas em qualquer um dos três primeiros painéis, as alterações serão exibidas nos demais painéis. Por exemplo, se você adicionar uma tabela ao painel Diagrama, ela será adicionada automaticamente à consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] do painel SQL. A inclusão de um campo em uma consulta do painel SQL adiciona o campo à lista do painel Grade e atualiza a tabela do painel Diagrama automaticamente.  
  
 Para obter mais informações, consulte [Ferramentas de Designer de Consultas e Exibição&#40;Visual Database Tools&#41;](http://msdn.microsoft.com/library/12e4b5a5-b793-4b6c-a0e5-c450c49bf26f).  
  
#### <a name="toolbar-for-the-graphical-query-designer"></a>Barra de ferramentas do Designer de Consultas Gráficas  
 A barra de ferramentas do designer de consultas gráficas contém botões que ajudam você a criar consultas [!INCLUDE[tsql](../../includes/tsql-md.md)] usando a interface gráfica.  
  
|Botão|Description|  
|------------|-----------------|  
|**Editar como Texto**|Alterna entre o designer de consulta baseado em texto e o designer de consultas gráficas.|  
|**Importar**|Importa uma consulta existente de um arquivo ou relatório. Há suporte apenas para tipos de arquivo .sql e .rdl. Para obter mais informações, consulte [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).|  
|![Botão de alternância do painel de diagrama de Mostrar/ocultar](../../reporting-services/report-data/media/rsqdicon-showhidediagram.gif "Mostrar/Ocultar botão de alternância de painel de diagrama")|Mostre ou oculte o painel Diagrama.|  
|![Mostrar ou Ocultar grade alternância de painel](../../reporting-services/report-data/media/rsqdicon-showhidegrid.gif "Mostrar ou Ocultar grade alternância de painel")|Mostre ou oculte o painel Grade.|  
|![Mostrar ou ocultar o botão de alternância de painel sql](../../reporting-services/report-data/media/rsqdicon-showhidesql.gif "Mostrar ou ocultar o botão de alternância de painel sql")|Mostre ou oculte o painel SQL.|  
|![Mostrar ou ocultar resultados alternância de painel](../../reporting-services/report-data/media/rsqdicon-showhideresult.gif "Mostrar ou ocultar resultados alternância de painel")|Mostre ou oculte o painel Resultado.|  
|![Execute a consulta](../../reporting-services/report-data/media/rsqdicon-run.gif "executar a consulta")|Executa a consulta.|  
|![Verificar SQL no botão do painel SQL](../../reporting-services/report-data/media/rsqdicon-verifysql.gif "verificar SQL no botão do painel SQL")|Verifique se a sintaxe do texto da consulta está correta.|  
|![Definir classificação crescente no campo selecionado](../../reporting-services/report-data/media/rsqdicon-sortascending.gif "definir classificação crescente no campo selecionado")|Defina a ordem de classificação como **Classificação Crescente** para a coluna selecionada no painel Diagrama.|  
|![Definir classificação decrescente no campo selecionado](../../reporting-services/report-data/media/rsqdicon-sortdescending.gif "definir classificação decrescente no campo selecionado")|Defina a ordem de classificação como **Classificação Decrescente** para a coluna selecionada no painel Diagrama.|  
|![Remover filtro no campo selecionado](../../reporting-services/report-data/media/rsqdicon-removefilter.gif "Remover filtro no campo selecionado")|Remova o filtro para a coluna selecionada no painel de diagrama está marcado como tendo um filtro (![gráfico de filtro ao lado da coluna de filtro selecionada](../../reporting-services/report-data/media/rsqdicon-filter.gif "gráfico de filtro ao lado da coluna de filtro selecionada")).|  
|![Usar Agrupar por para o campo selecionado](../../reporting-services/report-data/media/rsqdicon-usegroupby.gif "usar Group By para o campo selecionado")|Mostre ou oculte a coluna **Agrupar por** do painel Grade. Quando o botão de alternância **Agrupar por** está ativo, uma coluna extra, chamada **Agrupar por** , é exibida no painel Grade e cada valor das colunas selecionadas na consulta usa como padrão **Agrupar por**, que faz com que a coluna selecionada seja incluída em uma cláusula Group By no texto SQL. Use o botão Agrupar por para adicionar automaticamente uma cláusula GROUP BY que inclua todas as colunas da cláusula SELECT. Quando a cláusula SELECT inclui chamadas de função de agregação (por exemplo, SUM(ColumnName)), inclua cada coluna que não seja de agregação na cláusula GROUP BY se desejar que ela apareça no conjunto de resultados.<br /><br /> Para aparecer no painel Resultado, cada coluna da consulta deve ter uma função de agregação definida para uso no cálculo do valor a ser exibido no painel Resultado, ou a coluna da consulta deve ser especificada na cláusula GROUP BY da consulta SQL.|  
|![Adicionar uma nova tabela ao painel diagrama](../../reporting-services/report-data/media/rsqdicon-addtable.gif "adicionar uma nova tabela ao painel do diagrama")|Adicione uma nova tabela da fonte de dados ao painel Diagrama.<br /><br /> **Observação** Quando você adiciona uma nova tabela, o designer de consultas tenta combinar as relações de chave estrangeira da fonte de dados. Depois de adicionar uma tabela, verifique se as relações de chave estrangeira representadas por vínculos entre as tabelas estão corretas.|  
  
#### <a name="example"></a>Exemplo  
 A consulta a seguir retorna a lista de sobrenomes da tabela [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] Pessoa **do banco de dados** :  
  
```  
SELECT LastName FROM Person.Person;  
```  
  
 Também é possível executar procedimentos usando o painel SQL. A seguinte consulta executa o procedimento armazenado **uspGetEmployeeManagers** no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] :  
  
```  
EXEC uspGetEmployeeManagers '1';  
```  
  
### <a name="command-type-tabledirect"></a>Tipo de comando TableDirect  
 No tipo **TableDirect** , o designer de consultas gráficas exibe uma lista suspensa das tabelas disponíveis na fonte de dados e um painel Resultado. Se você selecionar uma tabela e clicar no botão **Executar** , serão retornadas todas as colunas dessa tabela.  
  
> [!NOTE]  
>  O recurso TableDirect só tem suporte pelos tipos de fonte de dados **OLE DB** e **ODBC** .  
  
 A tabela a seguir descreve a função de cada painel.  
  
|Painel|Função|  
|----------|--------------|  
|Lista suspensa Tabela|Lista todas as tabelas disponíveis na fonte de dados. Selecione um na lista para torná-lo ativo.|  
|Resultado|Exibe todas as colunas da tabela selecionada. Para executar a consulta de tabela, clique no botão **Executar** da barra de ferramentas.|  
  
#### <a name="toolbar-buttons-for-the-command-type-tabledirect"></a>Botões da barra de ferramentas relacionados ao tipo de comando TableDirect  
 A barra de ferramentas do designer de consultas gráficas fornece uma lista suspensa das tabelas existentes na fonte de dados. A tabela a seguir lista cada botão e a função correspondente.  
  
|Botão|Description|  
|------------|-----------------|  
|**Editar como Texto**|Alterna entre o designer de consulta baseado em texto e o designer de consultas gráficas.|  
|**Importar**|Importa uma consulta existente de um arquivo ou relatório. Há suporte apenas para tipos de arquivo .sql e .rdl. Para obter mais informações, consulte [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).|  
|![Ícone do botão Designer de consultas genérico](../../reporting-services/report-data/media/icongenericquerydesigner.gif "ícone do botão Designer de consultas genérico")|Alterne entre o designer de consultas genéricas e o designer de consultas gráficas, preservando a exibição do texto da consulta ou do procedimento armazenado.|  
|![Execute a consulta](../../reporting-services/report-data/media/rsqdicon-run.gif "executar a consulta")|Selecione todas as colunas da tabela selecionada.|  
  
### <a name="command-type-storedprocedure"></a>Tipo de comando StoredProcedure  
 No tipo **StoredProcedure** , o designer de consultas gráficas exibe uma lista suspensa dos procedimentos armazenados disponíveis na fonte de dados e um painel Resultado. A tabela a seguir descreve a função de cada painel.  
  
|Painel|Função|  
|----------|--------------|  
|Lista suspensa Procedimento armazenado|Lista todos os procedimentos armazenados disponíveis na fonte de dados. Selecione um na lista para torná-lo ativo.|  
|Resultado|Exibe o resultado da execução do procedimento armazenado. Para executar o procedimento armazenado selecionado, clique no botão **Executar** na barra de ferramentas.|  
  
#### <a name="toolbar-buttons-for-command-type-storedprocedure"></a>Botões da barra de ferramentas relacionados ao tipo de comando StoredProcedure  
 A barra de ferramentas do designer de consultas gráficas fornece uma lista suspensa dos procedimentos armazenados existentes na fonte de dados. A tabela a seguir lista cada botão e a função correspondente.  
  
|Botão|Description|  
|------------|-----------------|  
|**Editar como Texto**|Alterna entre o designer de consulta baseado em texto e o designer de consultas gráficas.|  
|**Importar**|Importa uma consulta existente de um arquivo ou relatório. Há suporte apenas para tipos de arquivo .sql e .rdl. Para obter mais informações, consulte [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).|  
|![Execute a consulta](../../reporting-services/report-data/media/rsqdicon-run.gif "executar a consulta")|Execute o procedimento armazenado selecionado.|  
|Lista suspensa Procedimento armazenado|Clique na seta para baixo para exibir uma lista dos procedimentos armazenados disponíveis na fonte de dados. Clique em qualquer procedimento armazenado da lista para selecioná-lo.|  
  
#### <a name="example"></a>Exemplo  
 O procedimento armazenado a seguir chama uma lista de cadeia de comandos dos gerentes contidos na tabela [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Esse procedimento armazenado aceita *BusinessEntityID* como parâmetro. Você pode inserir qualquer inteiro pequeno.  
  
 `uspGetEmployeeManagers '1';`  
  
## <a name="see-also"></a>Consulte também  
 [Ferramentas de Design da Consulta &#40;SSRS&#41;](../../reporting-services/report-data/query-design-tools-ssrs.md)   
 [Conjuntos de dados de relatório &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [O tipo de conexão do SQL Server &#40;SSRS&#41;](../../reporting-services/report-data/sql-server-connection-type-ssrs.md)   
 [Tipo de conexão OLE DB &#40;SSRS&#41;](../../reporting-services/report-data/ole-db-connection-type-ssrs.md)   
 [Conjuntos de dados de relatório &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [Tipo de conexão Oracle &#40;SSRS&#41;](../../reporting-services/report-data/oracle-connection-type-ssrs.md)   
 [Arquivo de configuração RSReportDesigner](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)   
 [Tópicos de instruções de como criar consultas e exibições &#40;Visual Database Tools&#41;](http://msdn.microsoft.com/library/200903f4-1208-4563-9dca-26aabaacfa20)  
  
  
