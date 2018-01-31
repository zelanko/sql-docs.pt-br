---
title: Origem OLE DB | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.oledbsource.f1
- sql13.dts.designer.oledbsourceadapter.connection.f1
- sql13.dts.designer.oledbsourceadapter.columns.f1
- sql13.dts.designer.oledbsourceadapter.errorhandling.f1
helpviewer_keywords:
- sources [Integration Services], OLE DB
- OLE DB source [Integration Services]
ms.assetid: f87cc5f6-b078-40f3-9d87-7a65e13e4c86
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e659322d66c01081c664850366a6cc4abf190d16
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="ole-db-source"></a>Origem de OLE DB
  A origem de OLE DB extrai dados de uma variedade de bancos de dados relacionais compatíveis com OLE DB usando uma tabela de banco de dados, uma exibição ou um comando SQL. Por exemplo, a origem de OLE DB pode extrair dados de tabelas em [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access ou bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
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
  
 Essa origem usa um gerenciador de conexões OLE DB para se conectar a uma fonte de dados e o gerenciador de conexões especifica o provedor OLE DB a ser usado. Para saber mais, veja [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
 Um projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] também fornece o objeto de fonte de dados do qual você pode criar um gerenciador de conexões OLE DB, disponibilizando as fontes de dados para a origem de OLE DB.  
  
 Dependendo do provedor OLE DB, algumas limitações se aplicam à origem de OLE DB:  
  
-   O provedor [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB para Oracle não dá suporte aos tipos de dados BLOB, CLOB, NCLOB, BFILE ou UROWID e a origem de OLE DB não pode extrair dados de tabelas que contenham colunas com esses tipos de dados.  
  
-   Os provedores IBM OLE DB DB2 e [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB DB2 não dão suporte ao uso de um comando SQL que chame um procedimento armazenado. Quando esse tipo de comando é usado, a origem de OLE DB não pode criar os metadados de coluna e, como resultado, os componentes do fluxo de dados que seguem a origem de OLE DB no fluxo de dados não possuem dados de coluna disponíveis e a execução do fluxo de dados falha.  
  
 A origem de OLE DB tem uma saída regular e uma saída de erro.  
  
## <a name="using-parameterized-sql-statements"></a>Usando instruções SQL parametrizadas  
 A origem de OLE DB pode usar uma instrução SQL para extrair dados. A instrução pode ser uma instrução SELECT ou EXEC.  
  
 A origem de OLE DB usa um gerenciador de conexões OLE DB para se conectar à fonte de dados da qual ela extrai dados. Dependendo do provedor que o gerenciador de conexões OLE DB usa e do RDBMS ao qual o gerenciador de conexões se conecta, diferentes regras se aplicam à nomenclatura e listagem de parâmetros. Se os nomes de parâmetros forem retornados do RDBMS, você poderá usá-los para mapear parâmetros em uma lista de parâmetros em uma instrução SQL; caso contrário, os parâmetros serão mapeados para o parâmetro na instrução SQL por suas posições na lista. Os tipos de nomes de parâmetros que têm suporte variam de acordo com o provedor. Por exemplo, alguns provedores exigem que você use os nomes de variáveis ou colunas, enquanto que outros exigem o uso de nomes simbólicos como 0 ou Param0. Você deve consultar a documentação específica do provedor para obter informações sobre os nomes dos parâmetros a serem usados nas instruções SQL.  
  
 Quando você usa um gerenciador de conexões OLE DB, não pode usar subconsultas parametrizadas, pois a origem de OLE DB não pode derivar informações de parâmetros através do provedor OLE DB. No entanto, você pode usar uma expressão para concatenar os valores de parâmetros na cadeia de consulta e definir a propriedade SqlCommand da origem. No Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] , você configura uma origem de OLE DB usando a caixa de diálogo **Editor de Origem de OLE DB** e mapeia os parâmetros para variáveis na caixa de diálogo **Definir Parâmetro de Consulta** .  
  
### <a name="specifying-parameters-by-using-ordinal-positions"></a>Especificando parâmetros usando posições ordinais  
 Se nenhum nome de parâmetro for retornado, a ordem na qual os parâmetros serão listados na lista **Parâmetros** na caixa de diálogo **Definir Parâmetro de Consulta** controlará à qual marcador de parâmetro eles estarão mapeados em tempo de execução. O primeiro parâmetro na lista é mapeado para o primeiro ? da instrução SQL, o segundo para o segundo ? e assim por diante.  
  
 A seguinte instrução SQL seleciona linhas da tabela **Produto** no banco de dados do [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] . O primeiro parâmetro na lista **Mapeamentos** é mapeado para o primeiro parâmetro na coluna **Cor** , o segundo parâmetro para a coluna **Tamanho** .  
  
 `SELECT * FROM Production.Product WHERE Color = ? AND Size = ?`  
  
 Os nomes de parâmetros não têm nenhum efeito. Por exemplo, se um parâmetro tiver o mesmo nome da coluna na qual ele se aplica, mas não estiver na posição ordinal correta na lista **Parâmetros** , o mapeamento de parâmetro que ocorre em tempo de execução usará a posição ordinal do parâmetro, não seu nome.  
  
 O comando EXEC geralmente exige que você use os nomes das variáveis que fornecem valores de parâmetros no procedimento como nomes de parâmetros.  
  
### <a name="specifying-parameters-by-using-names"></a>Especificando parâmetros usando nomes  
 Se os nomes de parâmetros reais forem retornados do RDBMS, os parâmetros usados por uma instrução SELECT e EXEC serão mapeados por nome. Os nomes de parâmetros devem corresponder aos nomes que o procedimento armazenado, executado pela instrução SELEC ou EXEC, espera.  
  
 A seguinte instrução SQL executa o procedimento armazenado **uspGetWhereUsedProductID** , disponível no banco de dados do [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] .  
  
 `EXEC uspGetWhereUsedProductID ?, ?`  
  
 O procedimento armazenado espera as variáveis, `@StartProductID` e `@CheckDate`, para fornecer os valores de parâmetros. A ordem na qual os parâmetros aparecem na lista **Mapeamentos** é irrelevante. O único requisito é que os nomes de parâmetros correspondam aos nomes de variáveis no procedimento armazenado, incluindo o sinal @.  
  
### <a name="mapping-parameters-to-variables"></a>Mapeando parâmetros para variáveis  
 Os parâmetros são mapeados para variáveis que fornecem os valores de parâmetros em tempo de execução. As variáveis geralmente são definidas pelo usuário, embora você também possa usar as variáveis de sistema que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece. Se você usar variáveis definidas pelo usuário, defina o tipo de dados que seja compatível com o tipo de dados da coluna à qual o parâmetro mapeado faz referência. Para obter mais informações, consulte [Variáveis do SSIS &#40;Integration Services&#41;](../../integration-services/integration-services-ssis-variables.md).  
  
## <a name="troubleshooting-the-ole-db-source"></a>Solucionando problemas da origem de OLE.DB  
 Você pode registrar as chamadas que a origem de OLE DB faz para provedores de dados externos. Você pode usar essa capacidade de registro para solucionar problemas de carregamento de dados de fontes de dados externas que a origem de OLE DB executa. Para registrar as chamadas que a origem de OLE DB faz aos provedores de dados externos, habilite o registro de pacotes e selecione o evento **Diagnóstico** no nível de pacotes. Para obter mais informações, consulte [Solucionando problemas de ferramentas para execução de pacotes](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="configuring-the-ole-db-source"></a>Configurando a origem de OLE DB  
 Você pode definir propriedades programaticamente ou por meio do Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas OLE DB](../../integration-services/data-flow/ole-db-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Extrair dados por meio da origem OLE DB](../../integration-services/data-flow/extract-data-by-using-the-ole-db-source.md)  
  
-   [Mapear parâmetros de consulta para variáveis em um componente de fluxo de dados](../../integration-services/data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
-   [Definir as propriedades de um componente de fluxo de dados](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [Classificar dados para as transformações Mesclagem e Junção de Mesclagem](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Artigo do Wiki, [SSIS with Oracle Connectors (SSIS com Conectores Oracle)](http://go.microsoft.com/fwlink/?LinkId=220670)em social.technet.microsoft.com.  
  
## <a name="ole-db-source-editor-connection-manager-page"></a>Editor de Origem OLE DB (página Gerenciador de Conexões)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Origem OLE DB** para selecionar o gerenciador de conexões OLE DB para a origem. Essa página também permite que você selecione uma tabela ou exibição a partir do banco de dados.  
  
> [!NOTE]  
>  Para carregar dados de uma fonte de dados que usa o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007, use uma origem OLE DB. Você não pode usar uma origem do Excel para carregar dados de uma fonte de dados do Excel 2007. Para obter mais informações, consulte [Configurar Gerenciador de Conexões OLE DB](../../integration-services/connection-manager/configure-ole-db-connection-manager.md).  
>   
>  Para carregar dados de uma fonte de dados que usa o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2003 ou uma versão anterior, use uma origem do Excel. Para obter mais informações, consulte [Editor de Fonte Excel &#40;Página Gerenciador de Conexões&#41;](../../integration-services/data-flow/excel-source-editor-connection-manager-page.md).  
  
> [!NOTE]  
>  A propriedade **CommandTimeout** da origem OLE DB não está disponível no **Editor de Origem OLE DB**, mas pode ser definida usando o **Editor Avançado**. Para obter mais informações sobre esta propriedade, consulte a seção Origem do Excel em [Propriedades personalizadas do OLE DB](../../integration-services/data-flow/ole-db-custom-properties.md).  
  
### <a name="open-the-ole-db-source-editor-connection-manager-page"></a>Abrir o Editor de Origem OLE DB (Página do Gerenciador de Conexões)  
  
1.  Adicione a origem OLE DB ao pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Clique com o botão direito do mouse no componente de origem e clique em **Editar**.  
  
3.  Clique em **Gerenciador de Conexões**.  
  
### <a name="static-options"></a>Opções estáticas  
 **Gerenciador de conexões OLE DB**  
 Selecione um gerenciador de conexões existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 **Nova**  
 Crie um novo gerenciador de conexões usando a caixa de diálogo **Configurar Gerenciador de Conexões OLE DB** .  
  
 **Modo de acesso aos dados**  
 Especifique o método para selecionar os dados da origem.  
  
|Opção|Description|  
|------------|-----------------|  
|Tabela ou exibição|Recupere os dados de uma tabela ou exibição na fonte de dados OLE DB.|  
|Nome da tabela ou variável do nome de exibição|Especifique a tabela ou nome de exibição em uma variável.<br /><br /> **Informações relacionadas:** [Usar variáveis em pacotes](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|Comando SQL|Recupere os dados da fonte de dados OLE DB usando uma consulta SQL.|  
|Comando SQL a partir da variável|Especifique o texto da consulta SQL em uma variável.|  
  
 **Visualização**  
 Visualize os resultados usando a caixa de diálogo **Exibição de Dados** . A**visualização** pode exibir até 200 linhas.  
  
> [!NOTE]  
>  Quando você visualiza os dados, as colunas com um tipo de dado CLR definido pelo usuário não contêm dados. Em vez disso, o valor \<valor muito grande para ser exibido> ou System.Byte[] é exibido. O primeiro é exibido quando a fonte de dados é acessada usando o provedor SQL OLE DB e o segundo, usando o provedor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
### <a name="data-access-mode-dynamic-options"></a>Opções dinâmicas de modo de acesso aos dados  
  
#### <a name="data-access-mode--table-or-view"></a>Modo de acesso aos dados = Tabela ou exibição  
 **Nome da tabela ou da exibição**  
 Selecione o nome da tabela ou da exibição na lista de tabelas ou exibições disponíveis na fonte de dados.  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>Modo de acesso aos dados = Variável do nome da tabela ou do nome de exibição  
 **Nome da variável**  
 Selecione a variável que contém o nome da tabela ou da exibição.  
  
#### <a name="data-access-mode--sql-command"></a>Modo de acesso aos dados = Comando SQL  
 **Texto do comando SQL**  
 Digite o texto de uma consulta SQL, crie a consulta clicando em **Construir Consulta**ou localize o arquivo que contém o texto da consulta clicando em **Procurar**.  
  
 **Parâmetros**  
 Se você inseriu uma consulta parametrizada usando ? como um espaço reservado para o parâmetro no texto da consulta, use a caixa de diálogo **Definir Parâmetros da Consulta** para mapear os parâmetros de entrada da consulta para as variáveis do pacote.  
  
 **Build query**  
 Use a caixa de diálogo **Construtor de Consultas** para construir a consulta SQL visualmente.  
  
 **Procurar**  
 Use a caixa de diálogo **Abrir** para localizar o arquivo com contém o texto da consulta SQL.  
  
 **Analisar consulta**  
 Verifique a sintaxe do texto da consulta.  
  
#### <a name="data-access-mode--sql-command-from-variable"></a>Modo de acesso aos dados = Comando SQL a partir da variável  
 **Nome da variável**  
 Selecione a variável que contém o texto da consulta SQL.  
  
## <a name="ole-db-source-editor-columns-page"></a>Editor de Origem de OLE DB (página Colunas)
  Use a página **Colunas** da caixa de diálogo do **Editor de Origem de OLE DB** para mapear uma coluna de saída para cada coluna externa (origem).  
  
### <a name="options"></a>Opções  
 **Colunas Externas Disponíveis**  
 Exiba a lista de colunas externas disponíveis na fonte de dados. Você não pode usar esta tabela para adicionar ou excluir colunas.  
  
 **Coluna Externa**  
 Exiba as colunas externas (origem) na ordem em que serão exibidas ao configurar os componentes que consomem os dados dessa origem. É possível alterar esta ordem desmarcando as colunas selecionadas na tabela e selecionando as colunas externas da lista em uma ordem diferente.  
  
 **Coluna de Saída**  
 Forneça um nome exclusivo para cada coluna de saída. O padrão é o nome da coluna externa (origem) selecionada; porém, é possível escolher qualquer nome descritivo exclusivo. O nome fornecido será exibido no Designer SSIS.  
  
## <a name="ole-db-source-editor-error-output-page"></a>Editor de Origem de OLE DB (página Saída de Erro)
  Use a página **Saída de Erro** da caixa de diálogo do **Editor de Origem OLE DB** para selecionar opções de tratamento de erro e definir propriedades em colunas de saída de erros.  
  
### <a name="options"></a>Opções  
 **Entrada/Saída**  
 Exibe o nome da fonte de dados.  
  
 **Coluna**  
 Exiba as colunas externas (origem) que você selecionou na página **Gerenciador de Conexões** da caixa de diálogo do **Editor de Origem OLE DB**.  
  
 **Erro**  
 Especifique o que deve acontecer quando ocorre um erro: ignorar a falha, redirecionar a linha ou causar falha no componente.  
  
 **Tópicos Relacionados:** [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **Truncation**  
 Especifique o que deve acontecer quando ocorre um truncamento: ignorar a falha, redirecionar a linha ou causar falha do componente.  
  
 **Descrição**  
 Exiba a descrição do erro.  
  
 **Definir este valor para células selecionadas**  
 Especifique o que deve acontecer a todas as células selecionadas quando ocorre um erro ou um truncamento: ignorar a falha, redirecionar a linha ou causar a falha no componente.  
  
 **Aplicar**  
 Aplique a opção de tratamento de erros às células selecionadas.  
  
## <a name="see-also"></a>Consulte Também  
 [Destino OLE DB](../../integration-services/data-flow/ole-db-destination.md)   
 [Variáveis do SSIS &#40;Integration Services&#41;](../../integration-services/integration-services-ssis-variables.md)   
 [Fluxo de Dados](../../integration-services/data-flow/data-flow.md)  
  
  
