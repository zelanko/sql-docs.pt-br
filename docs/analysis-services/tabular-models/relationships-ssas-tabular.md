---
title: Relações | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b704b7e2fdc299006d77e08314d2b16ffd750a0a
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34045300"
---
# <a name="relationships"></a>Relações 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Em modelos tabulares, uma relação é uma conexão entre duas tabelas de dados. A relação estabelece como os dados nas duas tabelas devem ser correlacionados. Por exemplo, podem ser relacionadas às tabelas Customers e Orders para mostrar o nome do cliente associado a cada ordem.  
  
 Ao usar o Assistente de Importação de Tabela para importar da mesma fonte de dados, as relações que já existem nas tabelas (na fonte de dados) que você escolhe importar serão recriadas no modelo. Você pode exibir relações que foram detectadas e recriadas automaticamente usando o designer de modelos na Exibição de Diagrama ou usando a caixa de diálogo Gerenciar Relações. Você também pode criar manualmente novas relações entre tabelas usando o designer de modelos na Exibição de Diagrama ou usando a caixa de diálogo Criar Relação ou Gerenciar Relações.  
  
 Após a definição de relações entre tabelas, automaticamente durante a importação ou manualmente, você poderá filtrar dados usando colunas relacionadas e pesquisar valores em tabelas relacionadas.  
  
> [!TIP]  
>  Se seu modelo contiver muitas relações, a Exibição de Diagrama poderá ajudá-lo a visualizar melhor e criar novas relações entre tabelas.  
  
  
##  <a name="what"></a> Benefícios  
 Relação é uma conexão entre duas tabelas de dados, baseada em uma ou mais colunas em cada tabela. Para saber por que as relações são úteis, imagine que você acompanhe dados para pedidos de clientes na empresa. Você poderia acompanhar todos os dados em uma única tabela com uma estrutura semelhante à seguinte:  
  
|CustomerID|Nome|EMail|DiscountRate|OrderID|OrderDate|Product|Quantidade|  
|----------------|----------|-----------|------------------|-------------|---------------|-------------|--------------|  
|1|Ashton|chris.ashton@contoso.com|0,05|256|2010-01-07|Compact Digital|11|  
|1|Ashton|chris.ashton@contoso.com|0,05|255|2010-01-03|SLR Camera|15|  
|2|Jaworski|michal.jaworski@contoso.com|0,10|254|2010-01-03|Budget Movie-Maker|27|  
  
 Esta abordagem pode funcionar, mas envolve o armazenamento de muitos dados redundantes, como o endereço de email do cliente para todos os pedidos. Embora o armazenamento seja barato, você deverá ter certeza de que atualizou todas as linhas desse cliente se o endereço de email for alterado. Uma solução para esse problema é dividir os dados em várias tabelas e definir relações entre essas tabelas. Essa é a abordagem usada em *bancos de dados relacionais* como o SQL Server. Por exemplo, um banco de dados importado para um modelo pode representar dados de pedidos usando três tabelas relacionadas:  
  
### <a name="customers"></a>Customers  
  
|[CustomerID]|Nome|EMail|  
|--------------------|----------|-----------|  
|1|Ashton|chris.ashton@contoso.com|  
|2|Jaworski|michal.jaworski@contoso.com|  
  
### <a name="customerdiscounts"></a>CustomerDiscounts  
  
|[CustomerID]|DiscountRate|  
|--------------------|------------------|  
|1|0,05|  
|2|0,10|  
  
### <a name="orders"></a>Orders  
  
|[CustomerID]|OrderID|OrderDate|Product|Quantidade|  
|--------------------|-------------|---------------|-------------|--------------|  
|1|256|2010-01-07|Compact Digital|11|  
|1|255|2010-01-03|SLR Camera|15|  
|2|254|2010-01-03|Budget Movie-Maker|27|  
  
 Se você importar essas tabelas do mesmo banco de dados, o Assistente de Importação de Tabela poderá detectar as relações entre as tabelas com base nas colunas que estão entre [colchetes] e poderá reproduzir essas relações na janela do designer de modelo. Para obter mais informações, consulte [Detecção automática e inferência de relações](#detection) neste tópico. Se você importar tabelas de várias fontes, você pode criar relações manualmente conforme descrito em [criar uma relação entre duas tabelas](../../analysis-services/tabular-models/create-a-relationship-between-two-tables-ssas-tabular.md).  
  
### <a name="columns-and-keys"></a>Colunas e chaves  
 As relações se baseiam em colunas de cada tabela que contenham os mesmos dados. Por exemplo, as tabelas Customers e Orders podem estar relacionadas porque ambas contêm uma coluna que armazena uma ID do cliente. No exemplo, os nomes de coluna são os mesmos, mas isso não é um requisito. Uma pessoa poderia ser CustomerID e outra, CustomerNumber, desde que todas as linhas na tabela Orders contivessem uma ID que também é armazenada na tabela Customers.  
  
 Em um banco de dados relacional, há vários tipos de *chaves*que normalmente são apenas colunas com propriedades especiais. Os seguintes quatro tipos de chaves podem ser usados em bancos de dados relacionais:  
  
-   *Chave primária*: identifica exclusivamente uma linha de uma tabela, como CustomerID na tabela Customers.  
  
-   *Chave alternativa* (ou *chave candidata*): uma coluna diferente da chave primária que é exclusiva. Por exemplo, uma tabela Employees pode armazenar uma ID de funcionário e um cadastro de pessoas físicas, ambos sendo exclusivos.  
  
-   *Chave estrangeira*: uma coluna que se refere a uma coluna exclusiva de outra tabela, como CustomerID na tabela Orders, que se refere a CustomerID na tabela Customers.  
  
-   *Chave composta*: uma chave composta de mais de uma coluna. Não há suporte para chaves compostas em modelos de tabela. Para obter mais informações, consulte "Chaves compostas e colunas de pesquisa" neste tópico.  
  
 Em modelos de tabela, a chave primária ou a chave alternativa é referenciada como a *coluna de pesquisa relacionada*ou apenas *coluna de pesquisa*. Se uma tabela tiver uma chave primária e uma chave alternativa, será possível usar qualquer uma delas como a coluna de pesquisa. A chave estrangeira é chamada de *coluna de origem* ou apenas *coluna*. Em nosso exemplo, uma relação seria definida entre CustomerID na tabela Orders (a coluna) e CustomerID (a coluna de pesquisa) na tabela Customers. Se você importar dados de um banco de dados relacional, o designer de modelos escolhe por padrão a chave estrangeira em uma tabela e a chave primária correspondente em outra. No entanto, é possível usar qualquer coluna com valores exclusivos para a coluna de pesquisa.  
  
### <a name="types-of-relationships"></a>Tipos de relações  
 A relação entre Customers e Orders é uma *relação um-para-muitos*. Todo cliente pode ter várias ordens, mas uma ordem não pode ter vários clientes. Os outros tipos de relação são *um-para-um* e *muitos-para-muitos*. A tabela CustomerDiscounts, que define uma única taxa de desconto para cada cliente, está em uma relação um-para-um com a tabela Customers. Um exemplo de uma relação muitos-para-muitos é uma relação direta entre Products e Customers, na qual um cliente pode comprar muitos produtos e o mesmo produto pode ser comprado por vários clientes. O designer de modelo não oferece suporte a relações muitos para muitos na interface do usuário. Para obter mais informações, consulte "[Relações muitos para muitos](#bkmk_many_to_many)" neste tópico.  
  
 A tabela a seguir mostra as relações entre as três tabelas:  
  
|Relação|Tipo|coluna de pesquisa|coluna|  
|------------------|----------|-------------------|------------|  
|Customers-CustomerDiscounts|um-para-um|Customers.CustomerID|CustomerDiscounts.CustomerID|  
|Customers-Orders|um-para-muitos|Customers.CustomerID|Orders.CustomerID|  
  
### <a name="relationships-and-performance"></a>Relações e desempenho  
 Após a criação de uma relação, o designer de modelo normalmente deve recalcular todas as fórmulas que usam colunas de tabelas na relação recém-criada. O processamento pode ser demorado, dependendo do volume de dados e da complexidade das relações.  
  
##  <a name="requirements"></a> Requirements for relationships  
 O designer de modelo tem vários requisitos que devem ser seguidos durante a criação de relações:  
  
### <a name="single-active-relationship-between-tables"></a>Relação ativa única entre tabelas  
 Várias relações podem resultar em dependências ambíguas entre as tabelas. Para criar cálculos exatos, você precisa de um único caminho de uma tabela para a próxima. Por isso, pode haver apenas uma relação ativa entre cada par de tabelas. Por exemplo, no AdventureWorks DW 2012, a tabela, DimDate, contém uma coluna, DateKey, que está relacionada a três colunas diferentes da tabela FactInternetSales: OrderDate, DueDate e ShipDate. Se você tentar importar essas tabelas, a primeira relação será criada com êxito, mas você receberá o seguinte erro em relações sucessivas que envolvam a mesma coluna:  
  
 \* Relação: tabela [column 1] -> tabela [column 2] - Status: error - motivo: não é possível criar uma relação entre tabelas \<tabela 1 > e \<tabela 2 >. Só pode existir uma relação direta ou indireta entre duas tabelas.  
  
 Se tiver duas tabelas e várias relações entre elas, você precisará importar várias cópias da tabela que contém a coluna de pesquisa e criar uma relação entre cada par de tabelas.  
  
 Pode haver muitas relações inativas entre tabelas. O caminho para usar entre tabelas é especificado pelo cliente de relatório na hora da consulta.  
  
### <a name="one-relationship-for-each-source-column"></a>Uma relação para cada coluna de origem  
 Uma coluna de origem não pode participar de várias relações. Se você já usou uma coluna como coluna de origem em uma relação, mas deseja usar essa coluna para conectar a outra coluna de pesquisa relacionada em uma tabela diferente, você poderá criar uma cópia da coluna e usá-la para a nova relação.  
  
 É fácil criar uma cópia de uma coluna que tenha exatamente os mesmos valores usando uma fórmula DAX em uma coluna calculada. Para obter mais informações, consulte [criar uma coluna calculada](../../analysis-services/tabular-models/ssas-calculated-columns-create-a-calculated-column.md).  
  
### <a name="unique-identifier-for-each-table"></a>Identificador exclusivo para cada tabela  
 Cada tabela deve ter uma única coluna que identifica exclusivamente cada linha nessa tabela. Essa coluna geralmente é chamada de chave primária.  
  
### <a name="unique-lookup-columns"></a>Colunas de pesquisa exclusivas  
 Os valores de dados na coluna de pesquisa devem ser exclusivos. Em outras palavras, a coluna não pode conter duplicatas. Em modelos tabulares, as cadeias de caracteres nulas e vazias equivalem a um espaço em branco, que é um valor de dados distinto. Isso significa que não pode haver vários nulos na coluna de pesquisa.  
  
### <a name="compatible-data-types"></a>Tipos de dados compatíveis  
 Os tipos de dados da coluna de origem e da coluna de pesquisa devem ser compatíveis. Para obter mais informações sobre tipos de dados, consulte [tipos de dados com suporte](../../analysis-services/tabular-models/data-types-supported-ssas-tabular.md).  
  
### <a name="composite-keys-and-lookup-columns"></a>Chaves compostas e colunas de pesquisa  
 Não é possível usar chaves compostas em um modelo de tabela; você deve sempre ter uma coluna que identifique exclusivamente cada linha da tabela. Se você tentar importar tabelas que tenham uma relação existente com base em uma chave composta, o Assistente de Importação de Tabela ignorará essa relação porque ela não pode ser criada no modelo de tabela.  
  
 Se quiser criar uma relação entre duas tabelas no designer de modelo e houver várias colunas que definam as chaves primária e estrangeira, você deverá combinar os valores para criar uma coluna de chave única antes de criar a relação. Isso pode ser feito antes de você importar os dados, ou no designer de modelo com a criação de uma coluna calculada.  
  
###  <a name="bkmk_many_to_many"></a> Many-to-Many relationships  
 Os modelos de tabela não dão suporte a relações muitos-para-muitos, e não é possível simplesmente adicionar *tabelas de junção* no designer de modelo. No entanto, você pode usar funções DAX para modelar relações muitos para muitos.  
  
 Você também pode tentar configurar um filtro cruzado bidirecional para ver se ele atinge a mesma finalidade. Às vezes, o requisito de relação muitos-para-muitos pode ser atendido por meio de filtros cruzados que mantêm um contexto de filtro entre várias relações de tabela. Consulte [Filtros cruzados bidirecionais para modelos de tabela no SQL Server 2016 Analysis Services](../../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md) para obter detalhes.  
  
### <a name="self-joins-and-loops"></a>Autojunções e loops  
 Não são permitidas autojunções em tabelas do modelo de tabela. Uma autojunção é uma relação recursiva entre uma tabela e ela mesma. Autojunções costumam ser usadas para definir hierarquias pai-filho. Por exemplo, você poderá unir uma tabela Employees a ela própria para produzir uma hierarquia que mostra a cadeia de gerenciamento em uma empresa.  
  
 O designer de modelo não permite criar loops entre relações em um modelo. Em outras palavras, o conjunto de relações a seguir é proibido.  
  
 Tabela 1, coluna a   a   Tabela 2, coluna f  
  
 Tabela 2, coluna f   a   Tabela 3, coluna n  
  
 Tabela 3, coluna n   a   Tabela 1, coluna a  
  
 Se você tentar criar uma relação que resulte na criação de um loop, será gerado um erro.  
  
##  <a name="detection"></a> Inference of relationships  
 Em alguns casos, as relações entre as tabelas são encadeadas automaticamente. Por exemplo, se você criar uma relação entre os dois primeiros conjuntos de tabelas abaixo, uma relação será inferida como existente entre as outras duas tabelas, e uma relação será estabelecida automaticamente.  
  
 Products e Category -- criada manualmente  
  
 Category e SubCategory -- criada manualmente  
  
 Products e SubCategory -- a relação é inferida  
  
 Para que sejam encadeadas automaticamente, as relações devem seguir em uma direção, conforme mostrado acima. Se as relações iniciais fossem entre, por exemplo, Sales e Products e Sales e Customers, uma relação não seria inferida. Isso ocorre porque a relação entre Products e Customers é uma relação muitos para muitos.  
  
##  <a name="bkmk_detection"></a> Detection of relationships when importing data  
 Quando você importa de uma tabela de fonte de dados relacional, o Assistente de Importação de Tabela detecta relações existentes nessas tabelas de origem com base nos dados do esquema de origem. Se as tabelas relacionadas forem importadas, essas relações serão duplicadas no modelo.  
  
##  <a name="bkmk_manually_create"></a> Manually create relationships  
 Apesar de a maioria das relações entre tabelas em uma única fonte de dados relacional serem detectadas automaticamente, e criadas no modelo de tabela, também há muitas instâncias onde você deve criar relações manualmente entre tabelas modelo.  
  
 Se seu modelo contiver dados de várias origens, provavelmente você precisará criar relações manualmente. Por exemplo, você pode importar as tabelas Customers, CustomerDiscounts e Orders de uma fonte de dados relacional. As relações existentes entre essas tabelas na origem são criadas automaticamente no modelo. Você pode adicionar outra tabela de uma origem diferente; por exemplo, você importa dados de região de uma tabela Geography em uma pasta de trabalho do Microsoft Excel. Você pode criar manualmente uma relação entre uma coluna na tabela Customers e uma coluna na tabela Geography.  
  
 Para criar manualmente relações em um modelo de tabela, você pode usar o designer de modelos na Exibição de Diagrama ou usar a caixa de diálogo Gerenciar Relações. A exibição de diagrama exibe tabelas, com relações entre elas, em um formato gráfico. Você pode clicar em uma coluna em uma tabela e arrastar o cursor até outra tabela para criar facilmente uma relação, na ordem correta, entre as tabelas. A caixa de diálogo Gerenciar Relações exibe relações entre tabelas em um formato de tabela simples. Para aprender a criar relações manualmente, consulte [criar uma relação entre duas tabelas](../../analysis-services/tabular-models/create-a-relationship-between-two-tables-ssas-tabular.md).  
  
##  <a name="bkmk_dupl_errors"></a> Duplicate values and other errors  
 Se você escolher uma coluna que não possa ser usada na relação, um X vermelho aparecerá ao lado da coluna. Você pode pausar o cursor sobre o ícone de erro para visualizar uma mensagem que fornece mais informações sobre o problema. Os problemas que podem tornar impossível a criação de uma relação entre as colunas selecionadas incluem os seguintes:  
  
|Problema ou mensagem|Resolução|  
|------------------------|----------------|  
|Não é possível criar a relação porque as duas colunas selecionadas contêm valores duplicados.|Para criar uma relação válida, pelo menos uma coluna do par selecionado deve conter somente valores exclusivos.<br /><br /> É possível editar as colunas para remover as duplicatas ou inverter a ordem das colunas de modo que a coluna que contenha os valores exclusivos seja usada como a **Tabela de Pesquisa Relacionada**.|  
|A coluna contém um valor nulo ou vazio.|Colunas de dados não podem ser unidas em um valor nulo. Para todas as linhas, deve haver um valor em ambas as colunas usadas em uma relação.|  
  
##  <a name="bkmk_related_tasks"></a> Related tasks  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Criar uma relação entre duas tabelas](../../analysis-services/tabular-models/create-a-relationship-between-two-tables-ssas-tabular.md)|Descreve como criar uma relação manualmente entre duas tabelas.|  
|[Excluir relações](../../analysis-services/tabular-models/delete-relationships-ssas-tabular.md)|Descreve como excluir uma relação e as ramificações de excluir relações.|  
|[Filtros cruzados bidirecionais para modelos de tabela no SQL Server 2016 Analysis Services](../../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md)|Descreve a filtragem cruzada bidirecional para tabelas relacionadas. Um contexto de filtro de uma relação de tabela pode ser usado ao realizar a consulta em uma segunda relação de tabela se as tabelas forem relacionadas e filtros cruzados bidirecionais estiverem definidos.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas e colunas](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)   
 [Importar dados](http://msdn.microsoft.com/library/6617b2a2-9f69-433e-89e0-4c5dc92982cf)  
  
  
