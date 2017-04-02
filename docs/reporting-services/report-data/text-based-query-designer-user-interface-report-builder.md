---
title: "Interface de usu&#225;rio do Designer de Consulta baseado em texto (Construtor de Relat&#243;rios) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "10010"
helpviewer_keywords: 
  - "designers de consulta, baseados em texto"
ms.assetid: 89fddca5-bd96-4128-9072-5348d1b6e02c
caps.latest.revision: 15
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 15
---
# Interface de usu&#225;rio do Designer de Consulta baseado em texto (Construtor de Relat&#243;rios)
  Use o designer de consulta baseado em texto para especificar uma consulta usando o idioma de consulta suportado pela fonte de dados, execute a consulta e exiba os resultados no tempo de design. Você pode especificar várias instruções do [!INCLUDE[tsql](../../includes/tsql-md.md)], consulta ou sintaxe de comando para as extensões de processamento de dados e consultas que são especificadas como expressões. Como o designer de consulta baseado em texto não processa previamente a consulta e pode acomodar qualquer tipo de sintaxe de consulta, esta é a ferramenta de designer de consulta padrão para muitos tipos de fontes de dados.  
  
> [!IMPORTANT]  
>  Os usuários acessam fontes de dados quando criam e executam consultas. Você deve conceder permissões mínimas nas fontes de dados, como permissões somente leitura.  
  
 O designer de consulta baseado em texto exibe uma barra de ferramentas e os dois painéis a seguir:  
  
-   **Consulta** Mostra o texto da consulta, o nome da tabela ou o nome do procedimento armazenado, dependendo do tipo de consulta. Nem todos os tipos de consulta estão disponíveis para todos os tipos de fontes de dados. Por exemplo, nome da tabela tem suporte apenas para o tipo de fonte de dados OLE DB.  
  
-   **Resultado** Mostra os resultados da execução da consulta em tempo de design.  
  
## Barra de ferramentas do Designer de Consulta baseado em texto  
 O designer de consulta baseado em texto fornece uma única barra de ferramentas para todos os tipos de comando. A tabela a seguir lista cada botão da barra de ferramentas e suas respectivas funções.  
  
|Botão|Description|  
|------------|-----------------|  
|**Editar como Texto**|Alterna entre o designer de consulta baseado em texto e o designer de consultas gráficas. Nem todos os tipos de fonte de dados dão suporte aos designers de consultas gráficas.|  
|**Importar**|Importa uma consulta existente de um arquivo ou relatório. Apenas os tipos de arquivo .sql e .rdl têm suporte|  
|![Executar a consulta](../../reporting-services/report-data/media/rsqdicon-run.png "Executar a consulta")|Executa a consulta e exibe o conjunto de resultados no painel Resultado.|  
|**Tipo de Comando**|Selecione **Text**, **StoredProcedure** ou **TableDirect**. Se um procedimento armazenado tiver parâmetros, a caixa de diálogo **Definir Parâmetros de Consulta** será aberta quando você clicar em **Executar** na barra de ferramentas e os valores poderão ser preenchidos conforme necessário. O suporte para o tipo de comando varia de acordo com o tipo da fonte de dados. Por exemplo, somente OLE DB e ODBC dão suporte a **TableDirect**.<br /><br /> Observação: se um procedimento armazenado retornar mais de um conjunto de resultados, somente o primeiro deles será usado para popular o conjunto de dados.|  
  
### Tipo de comando Text  
 Quando você cria um conjunto de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o designer de consulta relacional é aberto por padrão. Para mudar para o designer de consulta baseado em texto, clique no botão de alternância **Editar como Texto** na barra de ferramentas. O designer de consulta baseado em texto apresenta dois painéis: Consulta e Resultado. A imagem a seguir define cada painel.  
  
 ![Designer de consulta genérico, para consulta de dados relacional](../../reporting-services/report-data/media/rsqd-dsaw-sql-generic.gif "Designer de consulta genérico, para consulta de dados relacional")  
  
 A tabela a seguir descreve a função de cada painel.  
  
|Painel|Função|  
|----------|--------------|  
|Consulta|Exibe o texto da consulta do [!INCLUDE[tsql](../../includes/tsql-md.md)]. Use esse painel para gravar ou editar uma consulta do [!INCLUDE[tsql](../../includes/tsql-md.md)].|  
|Resultado|Exibe os resultados da consulta. Para executar a consulta, clique com o botão direito do mouse em qualquer painel e clique em **Executar** ou clique no botão **Executar** na barra de ferramentas.|  
  
#### Exemplo  
 A consulta a seguir retorna a lista de sobrenomes da tabela **ContactType** do banco de dados AdventureWorks2014 para o esquema **Person**.  
  
```  
SELECT Name FROM Person.ContactType  
```  
  
 Ao clicar em **Executar**, na barra de ferramentas, o comando no painel **Consulta** será executado e os resultados serão exibidos no painel **Resultado**. O conjunto de resultados exibe uma lista de 20 tipos de contatos, por exemplo, Proprietário ou Agente de Vendas.  
  
### Tipo de comando StoredProcedure  
 Quando você seleciona o **Comando typeStoredProcedure**, o designer de consulta baseado em texto apresenta dois painéis: Consulta e Resultado. Insira o nome do procedimento armazenado no painel Consulta e clique em **Executar** na barra de ferramentas. Se o procedimento armazenado usar parâmetros, a caixa de diálogo **Definir Parâmetros de Consulta** será aberta. Insira os valores dos parâmetros do procedimento armazenado. Um parâmetro de relatório é criado para cada parâmetro de entrada de procedimento armazenado.  
  
 A figura a seguir mostra os painéis Consulta e Resultados quando você executa um procedimento armazenado. Neste caso, os parâmetros de entrada são constantes.  
  
 ![Procedimento armazenado no designer de consultas baseado em texto](../../reporting-services/report-data/media/rs-relational-text-sp.gif "Procedimento armazenado no designer de consultas baseado em texto")  
  
 A tabela a seguir descreve a função de cada painel.  
  
|Painel|Função|  
|----------|--------------|  
|Consulta|Exibe o nome do procedimento armazenado e os parâmetros de entrada.|  
|Resultado|Exibe os resultados da consulta. Para executar a consulta, clique com o botão direito do mouse em qualquer painel e clique em **Executar** ou clique no botão **Executar** na barra de ferramentas.|  
  
#### Exemplo  
 A consulta a seguir chama o procedimento armazenado **uspGetWhereUsedProductID** do AdventureWorks2014. Você deve inserir um valor para o parâmetro do número de identificação do produto quando executar a consulta.  
  
```  
uspGetWhereUsedProductID  
```  
  
 Clique no botão **Executar** (**!**). Quando os parâmetros de consulta forem solicitados, use a seguinte tabela para digitar valores.  
  
|||  
|-|-|  
|*@StartProductID*|820|  
|*@CheckDate*|20010115|  
  
 Para a data especificada, o conjunto de resultados exibe uma lista de 13 identificadores de produtos que usaram o número de componente especificado.  
  
### Tipo de comando TableDirect  
 Quando você seleciona o **Comando typeTableDirect**, o designer de consulta baseado em texto apresenta dois painéis: Consulta e Resultado. Se você inserir uma tabela e clicar no botão **Executar**, todas as colunas dessa tabela serão retornadas.  
  
#### Exemplo  
 Para um tipo de fonte de dados OLE DB, a seguinte consulta de banco de dados retorna um conjunto de resultados para todos os tipos de contatos no banco de dados AdventureWorks2014.  
  
 `Person.ContactType`  
  
 Quando você insere o nome da tabela Person.ContactType, esse procedimento equivale à criação da instrução `SELECT * FROM Person.ContactType` do [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## Consulte também  
 [Interface do usuário do Designer de Consultas Relacional &#40;Construtor de Relatórios&#41;](../../reporting-services/report-data/relational-query-designer-user-interface-report-builder.md)   
 [Designers de Consultas &#40;Construtor de Relatórios&#41;](../Topic/Query%20Designers%20\(Report%20Builder\).md)  
  
  