---
title: Coleção de campos de conjuntos de dados (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: b3884576-1f7e-4d40-bb7d-168312333bb3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 234ebb8b4490d496731e4fb33db8e73a978f7f15
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66107386"
---
# <a name="dataset-fields-collection-report-builder-and-ssrs"></a>Coleção de campos de conjuntos de dados (Construtor de Relatórios e SSRS)
  Os campos de um conjunto de dados representam os dados de uma conexão de dados. Um campo pode representar dados numéricos ou não numéricos. Os exemplos incluem valores de vendas, vendas totais, nomes de clientes, identificadores de banco de dados, URLs, imagens, dados espaciais e endereços de email. Na superfície de design, os campos aparecem como expressões em itens de relatório, como caixas de texto, tabelas e gráficos.  
  
 Um relatório tem três tipos de campos, que são exibidos no painel de Dados do Relatório: campos de conjunto de dados, campos calculados de conjunto de dados e campos internos.  
  
-   **Campos de conjunto de dados.** Os metadados que representam a coleção de campos que serão retornados quando a consulta de conjunto de dados for executada na fonte de dados.  
  
-   **Campos calculados de conjunto de dados.** Campos adicionais que você cria para o conjunto de dados. Cada campo calculado é criado por meio da avaliação de uma expressão que você define.  
  
-   **Campos internos.** Os metadados que representam uma coleção de campos fornecidos pelo Construtor de Relatórios, que oferecem informações do relatório, como o nome ou a hora em que ele foi processado. Para obter mais informações, consulte [Referências de globais internas e referências de usuários &#40;Construtor de Relatórios e SSRS&#41;](../report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md).  
  
 Os nomes de campos de conjunto de dados são salvos como parte da definição do conjunto de dados do relatório. Para obter mais informações, consulte [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Fields"></a> Campos e consultas de conjunto de dados  
 Os campos de conjunto de dados são especificados pelo comando de consulta de conjunto de dados e por quaisquer campos calculados que você definir. A coleção de campos que você vê no relatório depende do tipo do seu conjunto de dados:  
  
-   **Conjunto de dados compartilhado.** A coleção de campos é a lista de campos para a consulta na definição de conjunto de dados compartilhado, no momento em que você adicionou o conjunto de dados compartilhado diretamente ao relatório ou quando adicionou uma parte de relatório que incluía o conjunto de dados compartilhado. A coleção de campos local não se altera quando a definição de conjunto de dados compartilhado é alterada no servidor de relatório. Para atualizar a coleção de campos local, é necessário atualizar a lista para o conjunto de dados compartilhado local.  
  
-   **Conjunto de dados incorporado.** A coleção de campos é a lista de campos retornados pela execução da consulta atual na fonte de dados.  
  
 Para saber mais, confira [Adicionar, editar e atualizar campos no painel de dados do relatório &#40;Construtor de Relatórios e SSRS&#41;](add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)  
  

  
### <a name="calculated-fields"></a>Campos calculados  
 Você especifica manualmente um campo calculado criando uma expressão. Os campos calculados podem ser usados para criar novos valores que não existem na fonte de dados. Por exemplo, um campo calculado pode representar um novo valor, uma ordem de classificação personalizada para um conjunto de valores de campo ou um campo existente que é convertido em um tipo de dados diferente.  
  
 Os campos calculados são locais para um relatório e não podem ser salvos como parte de um conjunto de dados compartilhado.  
  
 Para saber mais, confira [Adicionar, editar e atualizar campos no painel de dados do relatório &#40;Construtor de Relatórios e SSRS&#41;](add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md).  
  

  
### <a name="entities-and-entity-fields"></a>Entidades e campos de entidade  
 Se estiver trabalhando com uma fonte de dados de modelo de relatório, você especificará as entidades e os campos de entidade como dados do relatório. No designer de consulta de um modelo de relatório, você pode explorar e selecionar interativamente as entidades relacionadas, além de escolher os campos que deseja incluir no conjunto de dados do relatório. Depois de concluir o design da consulta, você poderá ver a coleção de identificadores e campos de entidade no painel de Dados do Relatório. Os identificadores de entidade são gerados automaticamente pelo modelo de relatório e geralmente não são exibidos para o usuário final.  
  
### <a name="using-extended-field-properties"></a>Usando propriedades de campo estendidas  
 As fontes de dados que dão suporte às consultas multidimensionais, como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], dão suporte às propriedades nos campos. As propriedades de campo aparecem no conjunto de resultados de uma consulta, mas não são visíveis no painel **Dados do Relatório** . Elas ainda estão disponíveis para serem usadas no relatório. Para fazer referência a uma propriedade de um campo, arraste o campo para o relatório e altere a propriedade padrão `Value` para o nome do campo da propriedade desejada. Por exemplo, em um cubo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , você pode definir formatos para valores nas células do cubo. O valor formatado está disponível pelo uso da propriedade de campo `FormattedValue`. Para usar o valor diretamente em vez de usar um valor e definir a propriedade de formato da caixa de texto, arraste o campo para a caixa de texto e altere a expressão `=Fields!FieldName.Value` para `=Fields!FieldName.FormattedValue`.  
  
> [!NOTE]  
>  Nem todas as propriedades `Field` podem ser usadas com todas as fontes de dados. As propriedades `Value` e `IsMissing` são definidas para todas as fontes de dados. Outras propriedades predefinidas (como `Key`, `UniqueName` e `ParentUniqueName` para fontes de dados multidimensionais) são suportadas apenas se a fonte de dados fornecer essas propriedades. Propriedades personalizadas são suportadas por alguns provedores de dados. Para obter mais informações, consulte os tópicos específicos sobre propriedades de campo estendidas para o tipo de fonte de dados em [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md). Por exemplo, para uma fonte de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], consulte [Propriedades de campos estendidos para um banco de dados do Analysis Services &#40;SSRS&#41;](extended-field-properties-for-an-analysis-services-database-ssrs.md).  
  

  
##  <a name="Defaults"></a> Compreendendo as expressões padrão dos campos  
 Uma caixa de texto pode ser um item de relatório de caixa de texto no corpo do relatório, ou uma caixa de texto em uma célula em uma região de dados tablix. Quando você vincula um campo a uma caixa de texto, a localização da caixa de texto determina a expressão padrão da referência do campo. No corpo do relatório, uma expressão de valor da caixa de texto deve especificar uma agregação e um conjunto de dados. Se houver apenas um conjunto de dados no relatório, essa expressão padrão será criada para você. Para um campo que representa um valor numérico, a função de agregação padrão será Sum. Para um campo que representa um valor não numérico, a função de agregação padrão será First.  
  
 Em uma região de dados tablix, a expressão de campo padrão depende das associações de linha e grupo da caixa de texto que você adiciona ao campo. A expressão de campo para o campo Sales, quando adicionada a uma caixa de texto na linha de detalhes de uma tabela é `[Sales]`. Se você adicionar o mesmo campo a uma caixa de texto de um cabeçalho de grupo, a expressão padrão é `(Sum[Sales])`, pois o cabeçalho do grupo exibe valores resumidos para o grupo, não valores detalhados. Quando o relatório for executado, o processador de relatório avaliará cada expressão e substituirá o resultado no relatório.  
  
 Para obter mais informações sobre expressões, consulte [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md).  
  

  
##  <a name="DataTypes"></a> Tipos de dados de campo  
 Quando você cria um conjunto de dados, os tipos de dados dos campos na fonte de dados podem não ser exatamente os tipos de dados usados em um relatório. Os tipos de dados podem passar por uma ou mais camadas de mapeamento. A extensão de processamento de dados ou o provedor de dados pode mapear tipos de dados da fonte de dados para tipos de dados da linguagem CLR. Os tipos de dados retornados pelas extensões de processamento de dados são mapeados para um subconjunto de tipos de dados CLR (common language runtime) do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
 Na fonte de dados, os dados são armazenados em tipos de dados que têm o suporte da fonte de dados. Por exemplo, os dados em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devem ser tipos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para os quais há suporte como, por exemplo, `nvarchar` ou `datetime`. Quando você recupera dados de uma fonte de dados, os dados passam por uma extensão de processamento ou um provedor de dados associado ao tipo da fonte de dados. Dependendo da extensão de processamento de dados, os dados podem ser convertidos de tipos de dados usados pela fonte de dados em tipos de dados suportados pela extensão de processamento de dados. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa tipos de dados com suporte pelo CLR (Common Language Runtime) instalado com o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. O provedor de dados mapeia todas as colunas do conjunto de resultados do tipo de dados nativo para um tipo de dados CLR do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] .  
  
 A cada estágio, os dados são representados pelos tipos de dados descritos na lista a seguir:  
  
-   **Fonte de dados** Os tipos de dados para os quais a versão do tipo da fonte de dados oferece suporte e ao qual você está se conectando.  
  
     Por exemplo, entre os tipos de dados típicos de uma fonte de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estão `int`, `datetime` e `varchar`. Os tipos de dados introduzidos pelo [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] adicionaram suporte a `date`, `time`, `datetimetz` e `datetime2`. Para obter mais informações, consulte [Tipos de dados (Transact-SQL)](https://go.microsoft.com/fwlink/?linkid=98362).  
  
-   **Provedor de dados ou extensão de processamento de dados** Os tipos de dados para os quais há suporte na versão do provedor de dados da extensão de processamento de dados que você seleciona ao se conectar com a fonte de dados. Os provedores de dados baseados no [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] usam tipos de dados para os quais o CLR oferece suporte. Para obter mais informações sobre tipos de dados do provedor de dados do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] , consulte [Mapeamentos de tipos de dados (ADO.NET)](https://go.microsoft.com/fwlink/?LinkId=112178) e [Trabalhando com tipos base](https://go.microsoft.com/fwlink/?LinkId=112177) no MSDN.  
  
     Por exemplo, entre os tipos de dados típicos suportados pelo [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] estão `Int32` e `String`. Datas e horas do calendário são suportados pela estrutura `DateTime`. O [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 2.0 Service Pack 1 introduziu suporte à estrutura `DateTimeOffset` para datas com deslocamento de fuso horário.  
  
    > [!NOTE]  
    >  O servidor de relatório usa os provedores de dados instalados e configurados no servidor de relatório. Clientes de criação de relatório em modo de Visualização usam as extensões de processamento de dados instaladas e configuradas na máquina cliente. Você deve testar o relatório no ambiente do cliente de relatório e do servidor de relatório.  
  
-   **Processador de relatório** Os tipos de dados se baseiam na versão do CLR instalado quando você instalou o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
     Por exemplo, os tipos de dados que o processador de relatório usa para os tipos de data e hora novos introduzidos no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] são mostrados na tabela a seguir:  
  
    |Tipo de dados SQL|Tipo de dados CLR|Descrição|  
    |-------------------|-------------------|-----------------|  
    |`Date`|`DateTime`|Somente data|  
    |`Time`|`TimeSpan`|Somente hora|  
    |`DateTimeTZ`|`DateTimeOffset`|Data e hora com deslocamento de fuso horário|  
    |`DateTime2`|`DateTime`|Data e hora com milissegundos fracionários|  
  
 Para obter mais informações sobre os tipos de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte [Tipos de dados (Mecanismo de Banco de Dados)](https://go.microsoft.com/fwlink/?linkid=98362) e [Tipos de dados e funções de data e hora (Transact-SQL)](https://go.microsoft.com/fwlink/?linkid=98360).  
  
 Para obter mais informações sobre como incluir referências a um campo de conjunto de dados de uma expressão, consulte [Tipos de dados em expressões &#40;Construtor de Relatórios e SSRS&#41;](../report-design/data-types-in-expressions-report-builder-and-ssrs.md).  
  

  
##  <a name="MissingFields"></a> Detectando campos ausentes em tempo de execução  
 Quando o relatório é processado, o conjunto de resultados de um conjunto de dados pode não conter valores para todas as colunas especificadas, porque elas não existem mais na fonte de dados. É possível usar a propriedade de campo IsMissing para detectar se os valores de um campo foram retornados em tempo de execução. Para obter mais informações, consulte [Referências de coleções de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](../report-design/built-in-collections-dataset-fields-collection-references-report-builder.md).  
  

  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo Propriedades do Conjunto de Dados, Campos &#40;Construtor de Relatórios&#41;](../dataset-properties-dialog-box-fields-report-builder.md)   
 [Partes de relatório e conjuntos de dados no Construtor de Relatórios](report-parts-and-datasets-in-report-builder.md)   
 [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
