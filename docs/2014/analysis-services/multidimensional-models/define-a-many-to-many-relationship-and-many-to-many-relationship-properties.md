---
title: Definir uma relação muitos-para-muitos e propriedades da relação muitos-para-muitos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- many-to-many relationships [Analysis Services]
ms.assetid: edb5f61a-a581-467a-a367-134b7f9b849f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 93f00a9544512c3c5efb63667d715c57bcf62de9
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53354008"
---
# <a name="define-a-many-to-many-relationship-and-many-to-many-relationship-properties"></a>Definir uma relação muitos-para-muitos e as propriedades da relação muitos-para-muitos
  Este tópico explica as dimensões muitos-para-muitos no Analysis Services, incluindo quando usá-las e como criá-las.  
  
## <a name="introduction"></a>Introdução  
 O Analysis Services dá suporte a dimensões muitos-para-muitos, permitindo uma análise mais complexa do que pode ser descrito em um esquema em estrela clássico. Em um esquema em estrela clássico, todas as dimensões têm uma relação um para muitos com uma tabela de fatos. Cada fato é associado a um membro de dimensão e um simples membro de dimensão é associado a muitos fatos.  
  
 Muitos-para-muitos remove essa restrição de modelagem habilitando um fato (como um saldo de contas) para ser associado a vários membros da mesma dimensão (o saldo de uma conta conjunta pode ser atribuído a dois ou mais titulares de uma conta conjunta).  
  
 Conceitualmente, uma relação dimensional de muitos-para-muitos no Analysis Services é equivalente a relações muitos-para-muitos em um modelo relacional, que dá suporte aos mesmos tipos de cenários. Exemplos comuns de muitos-para-muitos incluem:  
  
-   Alunos inscritos em vários cursos: cada curso tem vários alunos.  
  
-   Médicos têm muitos pacientes; pacientes têm muitos médicos.  
  
-   Clientes têm muitas contas bancárias; contas bancárias podem pertencer a mais de um cliente.  
  
-   No Adventure Works, muitos clientes têm muitos motivos para pedir um produto, e um motivo de vendas pode ser associado a vários pedidos.  
  
 Analiticamente, o problema que uma relação muitos-para-muitos resolve é a representação precisa de uma conta ou soma relativa à relação dimensional (geralmente eliminando contas duplicadas ao realizar cálculos para um membro de dimensão específico). Um exemplo é necessário para esclarecer esse ponto. Considere um produto ou serviço que pertence a mais de uma categoria. Se você estiver contando o número de serviços por categoria, deverá querer que um serviço que pertence a ambas as categorias seja incluído em cada uma. Ao mesmo tempo, você não quer superestimar o número de serviços que fornece. Ao especificar a relação dimensional muitos-para-muitos, você tem mais probabilidade de obter os resultados corretos ao consultar por categoria ou serviço. No entanto, um teste completo é sempre necessário para garantir que esse é o caso.  
  
 Estruturalmente, criar uma relação dimensional de muitos-para-muitos é semelhante a como você pode criar uma relação muitos-para-muitos em um modelo de dados relacional. Enquanto um modelo relacional usa uma *tabela de junção* para armazenar associações de linha, um modelo multidimensional usa um *grupo de medidas intermediário*. Um grupo de medidas intermediário é o termo que usamos para nos referir a uma tabela que mapeia membros de diferentes dimensões.  
  
 Visualmente, uma relação dimensional muitos-para-muitos não é indicada em um diagrama de cubo. Em vez disso, use a guia Uso da Dimensão para identificar rapidamente qualquer relação muitos-para-muitos em um modelo. Uma relação muitos-para-muitos é indicada pelo seguinte ícone.  
  
 ![Ícone de muitos-para-muitos no uso da dimensão](../media/ssas-m2m-icondimusage.png "muitos-para-muitos ícone no uso da dimensão")  
  
 Clique no botão para abrir a caixa de diálogo Definir Relação para verificar se o tipo de relação é muitos-para-muitos, e para visualizar qual grupo de medidas intermediário é usado na relação.  
  
 ![Botão de relação de definir no uso da dimensão](../media/ssas-m2m-btndimusage.png "botão Definir relação no uso da dimensão")  
  
 Em seções subsequentes, você aprenderá a configurar uma dimensão muitos-para-muitos e testar comportamentos modelo. Se você preferir analisar informações adicionais ou tentar tutoriais primeiro, consulte **Saiba mais** no final deste artigo.  
  
## <a name="create-a-many-to-many-dimension"></a>Criar uma dimensão muitos-para-muitos  
 Uma relação muitos-para-muitos inclui duas dimensões que têm uma cardinalidade muitos-para-muitos, um grupo de medidas intermediário para armazenar associações de membro, e um grupo de medidas de fato contendo dados mensuráveis, como um total de vendas ou o saldo de uma conta bancária.  
  
 As dimensões em uma relação muitos-para-muitos pode ter tabelas correspondentes na DSV, onde cada dimensão no modelo é baseada em uma tabela existente em uma fonte de dados. Por outro lado, as dimensões em seu modelo podem derivar de menos tabelas físicas ou tabelas físicas diferentes na DSV. Usando Motivos de Vendas e Pedidos de Vendas como um caso no ponto, o cubo de exemplo do Adventure Works demonstra uma relação muitos-para-muitos usando dimensões que existem como estruturas de dados de apenas modelos, sem contrapartes físicas na DSV. A dimensão Pedido de Vendas tem como base uma tabela de fatos, em vez de uma tabela de dimensão, na fonte de dados subjacente.  
  
 O próximo procedimento supõe que você já saiba quais entidades participam na relação muitos-para-muitos. Consulte **Saiba mais** para estudar em mais detalhes.  
  
 Para ilustrar as etapas usadas para criar uma relação muitos par muitos, esse procedimento recria uma das relações muitos-para-muitos no cubo de exemplo Adventure Works. Se você tiver os dados de origem (ou seja, o data warehouse de exemplo Adventure Works) instalado em uma instância do mecanismo de banco de dados relacional, você poderá seguir essas etapas.  
  
#### <a name="step-1-verify-dsv-relationships"></a>Etapa 1: Verificar as relações DSV  
  
1.  No SQL Server Data Tools, em um projeto multidimensional, crie uma fonte de dados para o data warehouse relacional Adventure Works DW 2012, hospedado em uma instância do Mecanismo de Banco de Dados do SQL Server.  
  
2.  Criar uma exibição de fonte de dados usando as tabelas existentes a seguir:  
  
    -   FactInternetSales  
  
    -   FactInternetSalesReason  
  
    -   DimSalesReason  
  
3.  Verifique se todas as tabelas que você planeja usar nas relações muitos-para-muitos estão relacionadas na DSV por meio de relações de chave primária. Esse é um requisito para estabelecer um link para o grupo de medidas intermediário em uma etapa subsequente.  
  
    > [!NOTE]  
    >  Se a fonte de dados subjacente não fornecer relações de chave primária e estrangeira, você poderá criar as relações manualmente na DSV. Para obter mais informações, consulte [Definir relações lógicas em uma exibição da fonte de dados &#40;Analysis Services&#41;](define-logical-relationships-in-a-data-source-view-analysis-services.md).  
  
     O exemplo a seguir confirma que as tabelas usadas nesse procedimento estão vinculadas usando as chaves primárias.  
  
     ![DSV que mostra tabelas relacionadas](../media/ssas-m2m-dsvpkeys.PNG "DSV que mostra tabelas relacionadas")  
  
#### <a name="step-2-create-dimensions-and-measure-groups"></a>Etapa 2: Criar dimensões e grupos de medidas  
  
1.  No SQL Server Data Tools, em um projeto multidimensional, clique com o botão direito do mouse em **Dimensões** e selecione **Nova Dimensão**.  
  
2.  Crie uma nova dimensão com base em uma tabela existente, **DimSalesReason**. Aceite todos os valores padrão ao especificar a origem.  
  
     Para atributos, selecione tudo.  
  
     ![Lista de atributos na nova dimensão](../media/ssas-m2m-dimsalesreason.PNG "lista de atributos na nova dimensão")  
  
3.  Crie uma segunda dimensão com base em uma tabela existente, Fact Internet Sales. Embora essa seja uma tabela de fatos, ela contém informações de Pedido de Vendas. Usaremos isso para criar uma dimensão de Pedido de Vendas.  
  
4.  Em Especificar Informações sobre a Origem, você verá um aviso que indica que uma coluna Nome deve ser especificada. Escolha **SalesOrderNumber** como o Nome.  
  
     ![Dimensão de pedidos de vendas mostrando a coluna de nome](../media/ssas-m2m-dimsalesordersource.PNG "mostrando a coluna de nome de dimensão de pedido de vendas")  
  
5.  Na próxima página do assistente, escolha os atributos. Nesse exemplo, você pode selecionar apenas **SalesOrderNumber**.  
  
     ![Lista de atributos do pedido de vendas dimensão mostrando](../media/ssas-m2m-dimsalesorderattrib.PNG "Sales order dimensão mostrando atributo a lista")  
  
6.  Renomeie a dimensão como **Dim Sales Orders**para que você tenha uma convenção de nomenclatura consistente para as dimensões.  
  
     ![Página do assistente que mostra a renomeação da dimensão](../media/ssas-m2m-dimsalesorders.PNG "mostrando a renomeação da dimensão de página do Assistente")  
  
7.  Clique com o botão direito do mouse em **Cubos** e selecione **Novo Cubo**.  
  
8.  Nas tabelas do grupo de medidas, escolha **FactInternetSales** e **FactInternetSalesReason**.  
  
     Você está escolhendo **FactInternetSales** porque contém as medidas que deseja usar no cubo. Você está escolhendo **FactInternetSalesReason** porque é o grupo de medidas intermediário, fornecendo dados da associação de membros que relaciona os pedidos de vendas aos motivos da venda.  
  
9. Escolha as medidas para cada tabela de fatos.  
  
     Para simplificar seu modelo, limpe todas as medidas, em seguida, selecione apenas **Sales Amount** e **Fact Internet Sales Count** na parte inferior da lista. **FactInternetSalesReason** tem apenas uma medida, portanto, é selecionada automaticamente.  
  
10. Na lista de dimensões, você deverá ver **Dim Sales Reason** e **Dim Sales Orders**.  
  
     Na página Selecionar Novas Dimensões, o assistente solicita que você crie uma nova dimensão para **Fact Internet Sales Dimension**. Você não precisa dessa dimensão; portanto, pode limpá-la da lista.  
  
11. Nomeie o cubo e clique em **Concluir**.  
  
#### <a name="step-3-define-many-to-many-relationship"></a>Etapa 3: Definir muitos-para-muitos relação  
  
1.  No designer de cubo, clique na guia Uso da Dimensão. Observe que já há uma relação de muitos para muitos entre **Dim Sales Reason** e **Fact Internet Sales**. Lembre-se de que o ícone a seguir indica uma relação muitos-para-muitos.  
  
     ![Ícone de muitos-para-muitos no uso da dimensão](../media/ssas-m2m-icondimusage.png "muitos-para-muitos ícone no uso da dimensão")  
  
2.  Clique na célula de interseção entre **Dim Sales Reason** e **Fact Internet Sales**, em seguida, clique no botão para abrir a caixa de diálogo Definir Relação.  
  
     Você pode ver que essa caixa de diálogo é usada para especificar uma relação muitos-para-muitos. Se você estivesse adicionando dimensões que têm uma relação regular, deveria usar essa caixa de diálogo para alterá-la para muitos-para-muitos.  
  
     ![Botão de relação de definir no uso da dimensão](../media/ssas-m2m-btndimusage.png "botão Definir relação no uso da dimensão")  
  
3.  Implante o projeto a uma instância multidimensional do Analysis Services. Na próxima etapa, você procurará o cubo no Excel para verificar seus comportamentos.  
  
## <a name="testing-many-to-many"></a>Teste de muitos-para-muitos  
 Quando você define uma relação muitos-para-muitos em um cubo, o teste é fundamental para garantir que as consultas retornem os resultados esperados. Você deve testar o cubo usando a ferramenta de aplicativo cliente que será usada pelos usuários finais. Nesse próximo procedimento, você usará o Excel para se conectar ao cubo e verificar os resultados da consulta.  
  
#### <a name="browse-the-cube-in-excel"></a>Procurar o cubo no Excel  
  
1.  Implante o projeto e procure o cubo para confirmar se as agregações são válidas.  
  
2.  No Excel, clique em **Dados** | **De Outras Fontes** | **Do Analysis Services**. Insira o nome do servidor, escolha o banco de dados e o cubo.  
  
3.  Crie uma Tabela Dinâmica que use o seguinte:  
  
    -   **Sales Amount** como o Valor  
  
    -   **Sales Reason Name** nas Colunas  
  
    -   **Sales Order Number** nas Linhas  
  
4.  Analise os resultados. Como estamos usando dados de exemplo, a impressão inicial é que todos os pedidos de vendas têm valores idênticos. No entanto, se você rolar para baixo, começará a ver variação de dados.  
  
     Do meio para baixo, você localizará os valores das vendas e os motivos das vendas para o número de pedido **SO5382**. O total geral desse pedido específico é **539,99**e os motivos da compra atribuídos a ele incluem a Promoção, Outros e Preço.  
  
     ![Planilha do Excel que mostra agregações muitos-para-muitos](../media/ssas-m2m-excel.png "planilha do Excel que mostra agregações muitos-para-muitos")  
  
     Observe que Sales Amount está calculado corretamente para o pedido; é **539,99** para o pedido inteiro. Embora **539,99** esteja indicado para cada motivo, esse valor não é somado para todos os três motivos, inflacionando erroneamente nosso total geral.  
  
     Por que motivo se deve colocar um valor de vendas sob cada motivo de vendas? A resposta é que isso permite que nós identifiquemos o valor de vendas que podemos atribuir a cada motivo.  
  
5.  Role até a parte inferior da planilha. Agora é fácil ver que o Preço é o motivo mais importante para as compras dos clientes, em comparação com outros motivos assim como o total geral.  
  
     ![Pasta de trabalho do Excel que mostra totais em muitos-para-muitos](../media/ssas-m2m-excelgrandtotal.png "pasta de trabalho do Excel que mostra totais em muitos-para-muitos")  
  
#### <a name="tips-for-handling-unexpected-query-results"></a>Dicas para lidar com resultados de consulta inesperados  
  
1.  Oculte as medidas no grupo de medidas intermediário, como a contagem, que não retornam resultados significativos em uma consulta. Isso impede que as pessoas tentem usar agregações que produzem dados insignificantes. Para ocultar uma medida, defina **Visibilidade** como **Falso** no atributo no designer de dimensão.  
  
2.  Crie perspectivas para usar um subconjunto de medidas e dimensões que dão suporte à experiência analítica que você quer fornecer. Possivelmente, um cubo que contém muitos grupos de medidas e dimensões não funciona bem junto em todos os casos. Ao isolar a dimensão e os grupos de medidas que você pretende que sejam usados juntos, você garante um resultado mais previsível.  
  
3.  Sempre lembre-se de implantar e reconectar depois de alterar um modelo. No Excel, use o botão Atualizar na faixa de opções Analisar da Tabela Dinâmica.  
  
4.  Evite usar grupos de medidas vinculados em vários relacionamentos muitos para muitos, especialmente quando esses relacionamentos estiverem em cubos diferentes. Fazer isso poderá resultar em agregações ambíguas. Para obter mais informações, consulte [Incorrect Amounts for Linked Measures in Cubes containing Many-to-Many Relationships](https://social.technet.microsoft.com/wiki/contents/articles/22911.incorrect-amounts-for-linked-measures-in-cubes-containing-many-to-many-relationships-ssas-troubleshooting.aspx)(Quantidades incorretas de medidas vinculadas em cubos com relacionamentos muitos para muitos).  
  
##  <a name="bkmk_Learn"></a> Learn more  
 Use os links a seguir para obter informações adicionais que ajudam a dominar os conceitos.  
  
 [Como posso definir uma dimensão muitos-para-muitos no Analysis Services](https://go.microsoft.com/fwlink/?LinkId=324759)  
  
 [A revolução muitos-para-muitos 2.0](https://go.microsoft.com/fwlink/?LinkId=324760)  
  
 [Tutorial: Exemplo de dimensão muitos-para-muitos para SQL Server Analysis Services](https://go.microsoft.com/fwlink/?LinkId=324761)  
  
## <a name="see-also"></a>Consulte também  
 [Relações de dimensão](../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [Instalar dados de exemplo e projetos para o tutorial de modelagem multidimensional do Analysis Services](../install-sample-data-and-projects.md)   
 [Implantar projetos do Analysis Services &#40;SSDT&#41;](deploy-analysis-services-projects-ssdt.md)   
 [Perspectivas em modelos multidimensionais](perspectives-in-multidimensional-models.md)  
  
  
