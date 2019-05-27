---
title: Conjuntos de resultados na tarefa Executar SQL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- result sets [Integration Services]
- Execute SQL task [Integration Services]
ms.assetid: 62605b63-d43b-49e8-a863-e154011e6109
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8efb049292caecf21f38ef5bc5a7392138bdcf5a
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66056424"
---
# <a name="result-sets-in-the-execute-sql-task"></a>Conjuntos de resultados na tarefa Executar SQL
  Em um pacote do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , se um conjunto de resultados será retornado à tarefa Executar SQL dependerá do tipo de comando SQL usado pela tarefa. Por exemplo, uma instrução SELECT normalmente retorna um conjunto de resultados, mas uma instrução INSERT não.  
  
 O que o conjunto de resultados contém também varia com o comando SQL. Por exemplo, o conjunto de resultados de uma instrução SELECT pode conter nenhuma linha, uma linha ou muitas linhas. No entanto, o conjunto de resultados de uma instrução SELECT que retorna uma contagem ou soma tem apenas uma única linha.  
  
 Trabalhar com conjuntos de resultados em uma tarefa Executar SQL é mais do que apenas saber se o comando SQL retorna um conjunto de resultados e o que ele contém. Há requisitos de uso e diretrizes adicionais para a utilização bem-sucedida dos conjuntos de resultados na tarefa Executar SQL. Esses requisitos de uso e diretrizes são abordados no restante deste tópico:  
  
-   [Especificando um tipo de conjunto de resultados](#Result_set_type)  
  
-   [Popular uma variável com um conjunto de resultados](#Populate_variable_with_result_set)  
  
-   [Configurando resultados conjuntos no Execute SQL Editor da tarefa](#Configure_result_sets)  
  
##  <a name="Result_set_type"></a> Especificando um conjunto de resultados tipo  
 O a tarefa Executar SQL dá suporte aos seguintes tipos de conjuntos de resultados:  
  
-   O conjunto de resultados **Nenhum** é usado quando a consulta não retorna nenhum resultado. Por exemplo, esse conjunto de resultados é usado para consultas que adicionam, alteram e excluem registros em uma tabela.  
  
-   O conjunto de resultados **Linha simples** é usado quando a consulta retorna apenas uma linha. Por exemplo, esse conjunto de resultados é usado para uma instrução SELECT que retorna uma contagem ou soma.  
  
-   O **Conjunto de resultados completo** é usado quando a consulta retorna várias linhas. Por exemplo, este conjunto de resultados é usado para uma instrução SELECT que recupera todas as linhas em uma tabela.  
  
-   O conjunto de resultados **XML** é usado quando a consulta retorna um conjunto de resultados em um formato XML. Por exemplo, esse conjunto de resultados é usado para uma instrução SELECT que inclui uma cláusula FOR XML.  
  
 Se a tarefa Executar SQL usar o **Conjunto de resultados completo** e a consulta retornar vários conjuntos de linhas, a tarefa retornará apenas o primeiro. Se este conjunto de linhas gerar um erro, a tarefa informará o erro. Se outros conjuntos de linhas gerarem erros, a tarefa não os informará.  
  
##  <a name="Populate_variable_with_result_set"></a> Populando uma variável com um conjunto de resultados  
 Você poderá associar o conjunto de resultados retornado por uma consulta a uma variável definida pelo usuário se o tipo de conjunto de resultados for uma única linha, um conjunto de linhas ou XML.  
  
 Se o tipo de conjunto resultante for **Linha simples**, você poderá associar uma coluna no resultado de retorno a uma variável usando o nome da coluna como o nome do conjunto de resultados ou pode usar a posição ordinal da coluna na lista de colunas como o nome do conjunto de resultados. Por exemplo, o nome do conjunto de resultados da consulta `SELECT Color FROM Production.Product WHERE ProductID = ?` pode ser **Color** ou **0**. Se a consulta retornar várias colunas e você quiser acessar os valores em todas elas, associe cada coluna a uma variável diferente. Se você mapear as colunas para variáveis usando números como nomes do conjunto de resultados, os números refletirão a ordem em que as colunas aparecerão na lista de colunas da consulta. Por exemplo, na consulta `SELECT Color, ListPrice, FROM Production.Product WHERE ProductID = ?`, você usa 0 para a coluna **Color** e 1 para a coluna **ListPrice** . A capacidade de usar um nome de coluna como o nome do conjunto de resultados depende do provedor que a tarefa está configurada para usar. Nem todos os provedores tornam os nomes das colunas disponíveis.  
  
 Algumas consultas que retornam um único valor podem não incluir nomes de colunas. Por exemplo, a instrução `SELECT COUNT (*) FROM Production.Product` não retorna nenhum nome de coluna. Você pode acessar o resultado de retorno usando a posição ordinal, 0, como o nome do resultado. Para acessar o resultado de retorno por nome de coluna, a consulta deve incluir uma cláusula AS \<nome do alias> para fornecer um nome de coluna. A instrução `SELECT COUNT (*)AS CountOfProduct FROM Production.Product`fornece a coluna **CountOfProduct** . Você pode acessar a coluna de resultado de retorno que usa o nome de coluna **CountOfProduct** ou a posição ordinal 0.  
  
 Se o tipo de conjunto de resultados for **Conjunto de resultados completo** ou **XML**, será necessário usar 0 como o nome de conjunto de resultados.  
  
 Quando você mapeia uma variável para um conjunto de resultados com o tipo de conjunto de resultados **Linha simples** , a variável deve ter um tipo de dados compatível com o tipo de dados da coluna que o conjunto de resultados contém. Por exemplo, um conjunto de resultados que contém uma coluna com um tipo de dados `String` não pode ser mapeado para uma variável com um tipo de dados numérico. Quando você define o **TypeConversionMode** propriedade `Allowed`, a tarefa Executar SQL tentará converter o parâmetro de saída e resultados para os dados de tipo da variável os resultados da consulta são atribuídos.  
  
 Um conjunto de resultados XML somente pode ser mapeado para uma variável com o tipo de dados `String` ou `Object`. Se a variável tiver o tipo de dados `String`, a tarefa Executar SQL retorna uma cadeia de caracteres e a fonte XML pode consumir os dados XML. Se a variável tiver o tipo de dados `Object`, a tarefa Executar SQL retornará um objeto do Modelo de Objeto de Documento (DOM).  
  
 Um **conjunto de resultados completo** deve ser mapeado para uma variável do `Object` tipo de dados. O resultado de retorno é um objeto de conjunto de linhas. Você pode usar um contêiner do Loop Foreach para extrair os valores de linha da tabela que são armazenados na variável Object em variáveis ​​de pacote e usar uma Tarefa Script para gravar os dados armazenados em variáveis ​​de pacotes em um arquivo. Para uma demonstração de como fazer isso usando um contêiner de Loop Foreach e uma Tarefa Script, confira a amostra CodePlex, [Executar conjuntos de resultados e parâmetros SQL](https://go.microsoft.com/fwlink/?LinkId=157863), no msftisprodsamples.codeplex.com.  
  
 A tabela a seguir resume os tipos de dados de variáveis que podem ser mapeadas para conjuntos de resultados.  
  
|Tipo de conjunto de resultados|Tipo de dados da variável|Tipo de objeto|  
|---------------------|---------------------------|--------------------|  
|Linha simples|Qualquer tipo compatível com a coluna de tipo no conjunto de resultados.|Não aplicável|  
|Conjunto de resultados completo|`Object`|Se a tarefa usar um gerenciador de conexões nativo, incluindo os gerenciadores de conexões ADO, OLE DB, Excel e ODBC, o objeto retornado será `Recordset` ADO.<br /><br /> Se a tarefa usar um gerenciador de conexões gerenciado, como o gerenciador de conexões [!INCLUDE[vstecado](../includes/vstecado-md.md)], o objeto retornado será um `System.Data.DataSet`.<br /><br /> Você pode usar uma tarefa Script para acessar o objeto `System.Data.DataSet` , conforme mostrado no exemplo a seguir.<br /><br /> `Dim dt As Data.DataTable` <br /> `Dim ds As Data.DataSet = CType(Dts.Variables("Recordset").Value, DataSet)` <br /> `dt = ds.Tables(0)`|  
|XML|`String`|`String`|  
|XML|`Object`|Se a tarefa usar um gerenciador de conexões nativo, inclusive os gerenciadores de conexões ADO, OLE DB, Excel e ODBC, o objeto retornado será `MSXML6.IXMLDOMDocument`.<br /><br /> Se a tarefa usa um Gerenciador de conexão gerenciado, como o [!INCLUDE[vstecado](../includes/vstecado-md.md)] Gerenciador de conexão, o objeto retornado será um `System.Xml.XmlDocument`.|  
  
 A variável pode ser definida no escopo da tarefa Executar SQL ou do pacote. Se a variável tiver escopo de pacote, o conjunto de resultados estará disponível para outras tarefas e contêineres no pacote e para qualquer pacote executado pelas tarefas Executar pacote ou Executar Pacotes do DTS 2000.  
  
 Quando você mapeia uma variável para um conjunto de resultados de **Linha simples** , os valores que não são de cadeia de caracteres retornados pela instrução SQL são convertidos em cadeias de caracteres quando as seguintes condições são atendidas:  
  
-   A propriedade **TypeConversionMode** é definida como verdadeira. Você define o valor da propriedade na janela Propriedades ou por meio do **Editor da Tarefa Executar SQL**.  
  
-   A conversão não resultará em truncamento de dados.  
  
 Para obter informações sobre como carregar um conjunto de resultados em uma variável, consulte [Mapear conjuntos de resultados para variáveis em uma tarefa Executar SQL](control-flow/execute-sql-task.md).  
  
##  <a name="Configure_result_sets"></a> Configurando conjuntos de resultados tarefa Executar SQL  
 Para obter mais informações sobre as propriedades dos conjuntos de resultados que podem ser definidas no Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] , clique no seguinte tópico:  
  
-   [SQL Editor da tarefa executar &#40;página conjunto de resultados&#41;](../../2014/integration-services/execute-sql-task-editor-result-set-page.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](../../2014/integration-services/set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 [Mapear conjuntos de resultados para variáveis em uma tarefa Executar SQL](control-flow/execute-sql-task.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   Exemplo do CodePlex, [Execute SQL Parameters and Result Sets (em inglês)](https://go.microsoft.com/fwlink/?LinkId=157863), em msftisprodsamples.codeplex.com  
  
  
