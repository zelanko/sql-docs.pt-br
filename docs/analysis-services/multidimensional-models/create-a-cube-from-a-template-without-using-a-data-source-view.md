---
title: "Criar um cubo a partir de um modelo sem usar uma exibição da fonte de dados | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5c8c09b1-140c-48db-9b9f-d18a051d7dbd
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 80680ae03ee8ac059cfe3c9b47c3abe6b67db511
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-cube-from-a-template-without-using-a-data-source-view"></a>Criar um Cubo de um modelo sem usar uma Exibição da Fonte de Dados
  Selecione **Criar o cubo sem usar uma fonte de dados** na primeira página do Assistente para Cubos para criar um cubo sem usar uma exibição da fonte de dados. Posteriormente, o Assistente de Geração de Esquema pode ser usado para gerar o esquema relacional para a exibição da fonte de dados com base na estrutura do cubo e possivelmente outros objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obter mais informações sobre como gerar um esquema, consulte [Assistente de Geração de Esquema &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/schema-generation-wizard-analysis-services.md).  
  
## <a name="selecting-the-build-method"></a>Selecionando o Método de Criação  
 No Assistente para Cubos, na página **Selecionar Método de Criação** , clique em **Criar o cubo sem usar uma fonte de dados**. Para criar o cubo usando um modelo de cubo existente, marque a caixa de seleção **Usar modelo de cubo** . . Se você não selecionar para usar um modelo, deverá definir as opções manualmente.  
  
 Os modelos de cubo contêm medidas predefinidas, grupos de medidas, dimensões, hierarquias e atributos. Se você selecionar um modelo, o assistente usará as definições de objeto nos modelos como a base para definir opções nas páginas seguintes. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é instalado com vários modelos para cubos padrão. O administrador do servidor também pode adicionar modelos de cubo ou de dimensão que são criados especificamente para obter os dados de sua organização.  
  
## <a name="selecting-dimensions"></a>Selecionando dimensões  
 Use a página **Selecionar Dimensões** do assistente para adicionar dimensões ao cubo. Esta página será exibida somente se já houver dimensões compartilhadas sem uma fonte de dados no projeto ou banco de dados. Ela não lista dimensões que têm uma fonte de dados.  
  
 Para adicionar dimensões existentes, selecione uma ou mais dimensões na lista **Dimensões compartilhadas** e clique no botão de seta para a direita (**>**) para movê-las para a lista **Dimensões do cubo** . Clique no botão da seta dupla (**>>**) para mover todas as dimensões na lista.  
  
## <a name="defining-new-measures"></a>Definindo novas medidas  
 Use a página **Definir Novas Medidas** do assistente para especificar as medidas e os grupos de medidas no novo cubo. Os grupos de medidas que você especifica aqui corresponderão a tabelas de fato no esquema gerado. As medidas que você especifica aqui corresponderão a colunas não chave numéricas nas tabelas.  
  
 Se você usar um modelo para criar o cubo, as medidas no modelo serão listadas em formato de grade em **Selecionar medidas de modelo**. A caixa de seleção ao lado de cada medida na lista é marcada inicialmente. Você pode desmarcar a caixa de seleção ao lado das medidas que não deseja incluir no cubo. Para adicionar ou remover todas as medidas na lista, marque ou desmarque na barra de título da grade.  
  
 Você pode adicionar medidas ao cubo na lista em **Adicionar novas medidas**. Para adicionar uma nova medida, clique na primeira célula vazia na coluna **Nome da Medida** (que exibe **Adicionar nova medida**). Especifique nome de medida, grupo de medidas, tipo de dados e agregação para cada nova medida. Para excluir uma medida da lista **Adicionar novas medidas** , clique no ícone de excluir (**X**). Se você não usar um modelo, **Adicionar novas medidas** será a única lista nesta página do assistente.  
  
 As grades **Selecionar medidas do modelo** e **Adicionar novas medidas** exibem valores nas colunas descritas na tabela a seguir. Você pode clicar em um valor em qualquer lista para alterá-lo.  
  
|Coluna|Description|  
|------------|-----------------|  
|**Nome da Medida**|Um valor nessa coluna define o nome de uma medida no cubo. Clique em um valor nessa coluna para digitar um nome. Clique em **Adicionar nova medida** nesta coluna para criar uma nova medida. Essa coluna define a propriedade **Name** no objeto de medida.|  
|**Grupo de Medidas**|O nome do grupo de medidas que contém a medida. Clique nesse valor para escolher ou digitar um nome. Se você excluir todas as medidas que pertencem a um grupo de medidas específico, o grupo de medidas também será removido. Essa coluna define a propriedade **Name** no objeto de grupo de medidas.|  
|**Tipo de Dados**|O tipo de dados para a medida. Clique nesse valor para alterar o tipo de dados. O padrão quando você cria uma medida é **Single**. Essa coluna define a propriedade **DataType** no objeto de medida.|  
|**Agregação**|A agregação padrão para a medida. Clique nesta célula para especificar uma das agregações padrão para a medida (ou **Nenhum**). O padrão quando você cria uma medida é **Soma**. Essa coluna define a propriedade **AggregationFunction** no objeto de medida.|  
  
## <a name="defining-new-dimensions"></a>Definindo novas dimensões  
 Use a página **Definir Novas Dimensões** do assistente para especificar as dimensões no novo cubo.  
  
 Se você usar um modelo para criar o cubo, as grades em **Selecionar dimensões de modelo** exibirão as dimensões no modelo. Você pode desmarcar a caixa de seleção ao lado de qualquer dimensão para removê-la do cubo. Desmarque a caixa de seleção na barra de título da grade para remover todas as dimensões listadas. Se você não usar um modelo, esta grade listará somente a dimensão de Tempo.  
  
 Você pode adicionar dimensões ao cubo na grade em **Adicionar novas dimensões**. Para adicionar uma dimensão, clique na célula na coluna **Nome** que contém o texto **Adicionar nova dimensão**e digite um nome para a dimensão. Para remover uma linha da lista, clique no ícone de excluir (**X**).  
  
 As grades **Selecionar dimensões do modelo** e **Adicionar novas dimensões** exibem valores nas colunas descritas na tabela a seguir. Você pode clicar em um valor em qualquer lista para alterá-lo.  
  
|Coluna|Description|  
|------------|-----------------|  
|**Tipo**|Exibe o tipo de dimensão para uma dimensão de modelo. Clique nesta célula para alterar o tipo de dimensão para uma dimensão. Essa coluna define a propriedade **Type** para o objeto de dimensão.|  
|**Name**|Exibe o nome da dimensão. Clique nessa célula para digitar um nome diferente. Esse valor define a propriedade **Name** para o objeto de dimensão.|  
|**SCD**|Especifica que esta é uma SCD (dimensão de alteração lenta). Marcar esta caixa de seleção adiciona os atributos Data de Início da SCD, ID Original da Data de Término e Status à dimensão. **SCD** será selecionado por padrão se você usar um modelo para criar o cubo e o assistente detectar estes quatro tipos de atributo em uma dimensão de modelo.|  
|**Atributos**|Exibe os atributos que devem ser criados para a dimensão. Cada nome de atributo na lista é precedido pelo nome de dimensão. Esta lista é somente leitura. Você pode editar os atributos usando o Designer de Dimensão depois de concluir o assistente.|  
  
## <a name="defining-time-periods"></a>Definindo períodos de tempo  
 Use a página **Definir Períodos de Tempo** do assistente para especificar o intervalo de datas que deseja incluir na dimensão. Por exemplo, você pode escolher um intervalo iniciando no dia 1 de janeiro do ano mais cedo em seus dados e estendendo anos além da sua transação mais atual. As transações que estão fora do intervalo não aparecem ou aparecem como membros desconhecidos na dimensão, dependendo da configuração da propriedade **UnknownMemberVisible** da dimensão. A propriedade **UnknownMemberName** especifica a legenda do membro desconhecido. Também é possível alterar o primeiro dia da semana usado por seus dados (o padrão é domingo).  
  
> [!NOTE]  
>  A página **Definir Períodos de Tempo** somente será exibida se você incluir uma dimensão de tempo em seu cubo na página **Definir Novas Dimensões** do assistente.  
  
 Selecione os períodos de tempo (**Ano**, **Semestre**, **Trimestre**, **Quadrimestre**, **Mês**, **Dez Dias**, **Semana**e **Data**) que você deseja incluir em seu esquema. Você deve selecionar o período de tempo Data; o atributo Data é o atributo de chave para a dimensão, que não pode funcionar sem ele. Você também pode alterar o idioma usado para rotular os membros da dimensão.  
  
 Os períodos de tempo que você seleciona criam atributos de tempo correspondentes na nova dimensão de tempo. O assistente também adiciona atributos relacionados que não aparecem na lista. Por exemplo, quando você seleciona intervalos de tempo **Ano** e **Semestre** , o assistente cria os atributos Dia do Ano, Dia do Semestre e Semestres de Ano, além dos atributos Ano e Semestre.  
  
 Depois de terminar de criar o cubo, você poderá usar o Designer de Dimensão para adicionar ou remover atributos de tempo. Como o atributo Data é o atributo de chave para a dimensão, você não pode removê-lo. Para ocultar o atributo Data dos usuários, você pode alterar a propriedade **AttributeHierarchyVisible** como **False**.  
  
 Todos os períodos de tempo disponíveis são exibidos no painel de Períodos de Tempo do Designer de Dimensão. (Este painel substitui o painel **Exibição da Fonte de Dados** para dimensões que são baseadas em tabelas de dimensão.) Você pode alterar o intervalo de datas para uma dimensão alterando a configuração de propriedade **Origem** (associação de tempo) para a dimensão. Como esta é uma alteração estrutural, você deve reprocessar a dimensão e os cubos que a usam antes de procurar os dados.  
  
## <a name="specifying-additional-calendars"></a>Especificando calendários adicionais  
 Na página **Especificar Calendários Adicionais** do assistente, selecione os calendários nos quais as hierarquias na dimensão se baseiam. Você pode escolher um dos seguintes calendários.  
  
|Calendário|Description|  
|--------------|-----------------|  
|Calendário fiscal|Um calendário fiscal de doze meses. Se você selecionar esse calendário, especifique o dia e o mês iniciais para o ano fiscal usado pela empresa.|  
|Calendário de relatório (ou marketing)|Um calendário de relatório de doze meses que inclui dois meses de quatro semanas e um mês de cinco semanas em um padrão recorrente de três meses (trimestral). Se você selecionar esse calendário, especifique o dia e o mês iniciais e o padrão trimestral de 4–4–5, 4–5–4 ou 5–4–4 semanas, sendo que cada dígito representa o número de semanas do mês.|  
|Calendário de produção|Um calendário que usa 13 períodos de quatro semanas, dividido em três trimestres de quatro períodos e um trimestre de cinco períodos. Se você selecionar esse calendário, especifique a semana (entre 1 e 4) e o mês iniciais para o ano de produção e o trimestre com períodos extras.|  
|Calendário ISO 8601|O calendário padrão de representação de datas e hora da Organização Internacional de Padronização (ISO) (8601). Esse calendário possui um número integrante de semanas de 7 dias. Para evitar dividir uma semana, este calendário inicia um ano novo até vários dias antes ou depois de 1 de janeiro.|  
  
 O calendário e as configurações que você seleciona determinam os atributos que são criados na dimensão. Por exemplo, se você selecionar os períodos de tempo **Ano** e **Trimestre** na página **Definir Períodos de Tempo** do assistente e o **Calendário fiscal** nessa página, os atributos FiscalYear, FiscalQuarter e FiscalQuarterOfYear serão criados para o calendário fiscal.  
  
 O assistente também cria hierarquias específicas do calendário, compostas pelos atributos criados para o calendário. Para todo calendário, cada nível de cada hierarquia se acumula no nível acima dele. Por exemplo, no calendário padrão de 12 meses, o assistente cria uma hierarquia de Anos e Semanas ou Anos e Meses. Porém, as semanas de um calendário padrão não estão contidas uniformemente dentro dos meses, então não há hierarquia de Anos, Meses e Semanas. Por outro lado, as semanas de um calendário de relatório ou fabricação estão divididas uniformemente dentro dos meses, então nesses calendários as semanas se acumulam em meses.  
  
## <a name="defining-dimension-usage"></a>Definindo uso de dimensão  
 Use a página **Definir Uso de Dimensão** do assistente para especificar quais medidas de cubo são agregadas por cada dimensão no assistente. A grade **Uso de dimensão** nesta página lista as dimensões como linhas e grupos de medidas como colunas. Marque a caixa de seleção para qualquer combinação de dimensão e grupo de medidas na qual a dimensão agrega as medidas desse grupo de medidas.  
  
## <a name="completing-the-cube-wizard"></a>Concluindo o Assistente para Cubos  
 Na página **Concluindo o Assistente** , examine a estrutura do novo cubo e, na caixa **Nome do cubo** , digite um nome para ele. Como opção, marque a caixa de seleção **Gerar esquema agora** para iniciar o assistente de geração de esquema. Na maioria dos casos, você não deve marcar esta caixa de seleção se planejar criar outros objetos. Você também pode usar o Designer de Cubo para gerar o esquema posteriormente.  
  
  

