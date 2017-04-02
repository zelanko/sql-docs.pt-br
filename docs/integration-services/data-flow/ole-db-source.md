---
title: "Origem de OLE DB | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.oledbsource.f1"
helpviewer_keywords: 
  - "origens [Serviços de Integração], OLE DB"
  - "origem OLE DB [Integration Services]"
ms.assetid: f87cc5f6-b078-40f3-9d87-7a65e13e4c86
caps.latest.revision: 69
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 69
---
# Origem de OLE DB
  A origem de OLE DB extrai dados de uma variedade de bancos de dados relacionais compatíveis com OLE DB usando uma tabela de banco de dados, uma exibição ou um comando SQL. Por exemplo, a origem de OLE DB pode extrair dados de tabelas em [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access ou bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Se a fonte de dados for [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007, ela exigirá um gerenciador de conexões diferente de versões anteriores do Excel. Para obter mais informações, consulte [Conectar-se a uma pasta de trabalho do Excel](../../integration-services/connection-manager/connect-to-an-excel-workbook.md).  
  
 A origem de OLE DB fornece quatro modos de acesso a dados diferentes para extrair dados:  
  
-   Uma tabela ou exibição.  
  
-   Uma tabela ou exibição especificada em uma variável.  
  
-   Os resultados de uma instrução SQL. A consulta pode ser uma consulta parametrizada.  
  
-   Os resultados de uma instrução SQL armazenados em uma variável.  
  
> [!NOTE]  
>  Quando você usa uma instrução SQL para invocar um procedimento armazenado que retorna resultados de uma tabela temporária, use a opção de WITH RESULT SETS para definir metadados para o conjunto de resultados.  
  
 Se você usar uma consulta parametrizada, poderá mapear variáveis para parâmetros para especificar os valores de parâmetros individuais nas instruções SQL.  
  
 Essa origem usa um gerenciador de conexões OLE DB para se conectar a uma fonte de dados e o gerenciador de conexões especifica o provedor OLE DB a ser usado. Para obter mais informações, consulte [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
 Um projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] também fornece o objeto de fonte de dados do qual você pode criar um gerenciador de conexões OLE DB, disponibilizando as fontes de dados para a origem de OLE DB.  
  
 Dependendo do provedor OLE DB, algumas limitações se aplicam à origem de OLE DB:  
  
-   O provedor [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB para Oracle não dá suporte aos tipos de dados BLOB, CLOB, NCLOB, BFILE ou UROWID e a origem de OLE DB não pode extrair dados de tabelas que contenham colunas com esses tipos de dados.  
  
-   Os provedores IBM OLE DB DB2 e [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB DB2 não dão suporte ao uso de um comando SQL que chame um procedimento armazenado. Quando esse tipo de comando é usado, a origem de OLE DB não pode criar os metadados de coluna e, como resultado, os componentes do fluxo de dados que seguem a origem de OLE DB no fluxo de dados não possuem dados de coluna disponíveis e a execução do fluxo de dados falha.  
  
 A origem de OLE DB tem uma saída regular e uma saída de erro.  
  
## Usando instruções SQL parametrizadas  
 A origem de OLE DB pode usar uma instrução SQL para extrair dados. A instrução pode ser uma instrução SELECT ou EXEC.  
  
 A origem de OLE DB usa um gerenciador de conexões OLE DB para se conectar à fonte de dados da qual ela extrai dados. Dependendo do provedor que o gerenciador de conexões OLE DB usa e do RDBMS ao qual o gerenciador de conexões se conecta, diferentes regras se aplicam à nomenclatura e listagem de parâmetros. Se os nomes de parâmetros forem retornados do RDBMS, você poderá usá-los para mapear parâmetros em uma lista de parâmetros em uma instrução SQL; caso contrário, os parâmetros serão mapeados para o parâmetro na instrução SQL por suas posições na lista. Os tipos de nomes de parâmetros que têm suporte variam de acordo com o provedor. Por exemplo, alguns provedores exigem que você use os nomes de variáveis ou colunas, enquanto que outros exigem o uso de nomes simbólicos como 0 ou Param0. Você deve consultar a documentação específica do provedor para obter informações sobre os nomes dos parâmetros a serem usados nas instruções SQL.  
  
 Quando você usa um gerenciador de conexões OLE DB, não pode usar subconsultas parametrizadas, pois a origem de OLE DB não pode derivar informações de parâmetros através do provedor OLE DB. No entanto, você pode usar uma expressão para concatenar os valores de parâmetros na cadeia de consulta e definir a propriedade SqlCommand da origem. No Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)], você configura uma origem de OLE DB usando a caixa de diálogo **Editor de Origem de OLE DB** e mapeia os parâmetros para variáveis na caixa de diálogo **Definir Parâmetro de Consulta**.  
  
### Especificando parâmetros usando posições ordinais  
 Se nenhum nome de parâmetro for retornado, a ordem na qual os parâmetros serão listados na lista **Parâmetros** na caixa de diálogo **Definir Parâmetro de Consulta** controlará à qual marcador de parâmetro eles estarão mapeados em tempo de execução. O primeiro parâmetro na lista é mapeado para o primeiro ? da instrução SQL, o segundo para o segundo ? e assim por diante.  
  
 A seguinte instrução SQL seleciona linhas da tabela **Produto** no banco de dados do [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)]. O primeiro parâmetro na lista **Mapeamentos** é mapeado para o primeiro parâmetro na coluna **Cor**, o segundo parâmetro para a coluna **Tamanho**.  
  
 `SELECT * FROM Production.Product WHERE Color = ? AND Size = ?`  
  
 Os nomes de parâmetros não têm nenhum efeito. Por exemplo, se um parâmetro tiver o mesmo nome da coluna na qual ele se aplica, mas não estiver na posição ordinal correta na lista **Parâmetros**, o mapeamento de parâmetro que ocorre em tempo de execução usará a posição ordinal do parâmetro, não seu nome.  
  
 O comando EXEC geralmente exige que você use os nomes das variáveis que fornecem valores de parâmetros no procedimento como nomes de parâmetros.  
  
### Especificando parâmetros usando nomes  
 Se os nomes de parâmetros reais forem retornados do RDBMS, os parâmetros usados por uma instrução SELECT e EXEC serão mapeados por nome. Os nomes de parâmetros devem corresponder aos nomes que o procedimento armazenado, executado pela instrução SELEC ou EXEC, espera.  
  
 A seguinte instrução SQL executa o procedimento armazenado **uspGetWhereUsedProductID**, disponível no banco de dados do [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)].  
  
 `EXEC uspGetWhereUsedProductID ?, ?`  
  
 O procedimento armazenado espera as variáveis, `@StartProductID` e `@CheckDate`, para fornecer os valores de parâmetros. A ordem na qual os parâmetros aparecem na lista **Mapeamentos** é irrelevante. O único requisito é que os nomes de parâmetros correspondam aos nomes de variáveis no procedimento armazenado, incluindo o sinal @.  
  
### Mapeando parâmetros para variáveis  
 Os parâmetros são mapeados para variáveis que fornecem os valores de parâmetros em tempo de execução. As variáveis geralmente são definidas pelo usuário, embora você também possa usar as variáveis de sistema que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece. Se você usar variáveis definidas pelo usuário, defina o tipo de dados que seja compatível com o tipo de dados da coluna à qual o parâmetro mapeado faz referência. Para obter mais informações, consulte [Variáveis do SSIS &#40;Integration Services&#41;](../../integration-services/integration-services-ssis-variables.md).  
  
## Solucionando problemas da origem de OLE.DB  
 Você pode registrar as chamadas que a origem de OLE DB faz para provedores de dados externos. Você pode usar essa capacidade de registro para solucionar problemas de carregamento de dados de fontes de dados externas que a origem de OLE DB executa. Para registrar as chamadas que a origem de OLE DB faz aos provedores de dados externos, habilite o registro de pacotes e selecione o evento **Diagnóstico** no nível de pacotes. Para obter mais informações, consulte [Solucionando problemas de ferramentas para execução de pacotes](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## Configurando a origem de OLE DB  
 Você pode definir propriedades programaticamente ou por meio do Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Origem de OLE DB**, clique em um dos seguintes tópicos:  
  
-   [Editor de origem de OLE DB &#40;Página Gerenciador de Conexões&#41;](../../integration-services/data-flow/ole-db-source-editor-connection-manager-page.md)  
  
-   [Editor de Origem de OLE DB &#40;Página Colunas&#41;](../../integration-services/data-flow/ole-db-source-editor-columns-page.md)  
  
-   [Editor de Origem OLE DB &#40;Página Saída de Erro&#41;](../../integration-services/data-flow/ole-db-source-editor-error-output-page.md)  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../Topic/Common%20Properties.md)  
  
-   [Propriedades personalizadas OLE DB](../../integration-services/data-flow/ole-db-custom-properties.md)  
  
## Tarefas relacionadas  
  
-   [Extrair dados por meio da origem OLE DB](../../integration-services/data-flow/extract-data-by-using-the-ole-db-source.md)  
  
-   [Mapear parâmetros de consulta para variáveis em um componente de fluxo de dados](../../integration-services/data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
-   [Definir as propriedades de um componente de fluxo de dados](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [Classificar dados para as transformações Mesclagem e Junção de Mesclagem](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## Conteúdo relacionado  
 Artigo do Wiki, [SSIS with Oracle Connectors (SSIS com Conectores Oracle)](http://go.microsoft.com/fwlink/?LinkId=220670) em social.technet.microsoft.com.  
  
## Consulte também  
 [Destino OLE DB](../../integration-services/data-flow/ole-db-destination.md)   
 [Variáveis do SSIS &#40;Integration Services&#41;](../../integration-services/integration-services-ssis-variables.md)   
 [Fluxo de Dados](../../integration-services/data-flow/data-flow.md)  
  
  