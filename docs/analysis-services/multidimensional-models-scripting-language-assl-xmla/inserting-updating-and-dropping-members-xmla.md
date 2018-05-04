---
title: Inserindo, atualizando e descartando membros (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f80756cb147b33b7caede48093fb69e17eb4a263
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="inserting-updating-and-dropping-members-xmla"></a>Inserindo, atualizando e descartando membros (XMLA)
  Você pode usar o [inserir](../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md), [atualizar](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md), e [Drop](../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md) comandos em XML for Analysis (XMLA) respectivamente inserir, atualizar ou excluir membros de uma dimensão habilitada para gravação. Para obter mais informações sobre dimensões habilitadas para gravação, consulte [Write-Enabled dimensões](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md).  
  
## <a name="inserting-new-members"></a>Inserindo membros novos  
 O **inserir** comando insere novos membros em atributos especificados em uma dimensão habilitada para gravação.  
  
 Antes de criar o **inserir** de comando, você deve ter as seguintes informações disponíveis para os novos membros a serem inseridos:  
  
-   A dimensão na qual os membros novos serão inseridos.  
  
-   O atributo da dimensão no qual os membros novos serão inseridos.  
  
-   Os nomes dos membros novos, incluindo qualquer tradução aplicável para o nome.  
  
-   As chaves dos membros novos. Se um atributo usar uma chave composta, ela poderá exigir diversos valores.  
  
-   Os valores para qualquer propriedade de atributo aplicável que não são implementados como outros atributos dentro da dimensão. Tais propriedades de atributo incluem operações unárias, traduções, rollups personalizados, propriedades de rollup personalizadas e níveis ignorados.  
  
 O **inserir** comando só contém duas propriedades:  
  
-   O [objeto](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md) propriedade, que contém uma referência de objeto para a dimensão na qual os membros serão inseridos. A referência de objeto contém o identificador de banco de dados, o identificador de cubo e o identificador de dimensão para a dimensão.  
  
-   O [atributos](../../analysis-services/xmla/xml-elements-properties/attributes-element-xmla.md) propriedade, que contém um ou mais [atributo](../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md) elementos para identificar os atributos em que os membros serão inseridos. Cada **atributo** elemento identifica um atributo e fornece o nome, valor, traduções, operador unário, rollup personalizado, propriedades de rollup personalizadas e níveis ignorados para um único membro a ser adicionado ao atributo identificado.  
  
    > [!NOTE]  
    >  Todas as propriedades para o **atributo** elemento deve ser incluído. Caso contrário, poderá ocorrer um erro.  
  
## <a name="updating-existing-members"></a>Atualizando membros existentes  
 O **atualização** comando atualiza membros existentes em atributos especificados, com base nas relações com outros membros em outros atributos, em uma dimensão habilitada para gravação. O **atualização** comando pode mover membros em outros níveis em hierarquias contidas pela dimensão e podem ser usados para reestruturar hierarquias pai-filho definidas por atributos pai.  
  
 Antes de criar o **atualização** de comando, você deve ter as seguintes informações disponíveis para os membros a serem atualizados:  
  
-   A dimensão na qual os membros existentes serão atualizados.  
  
-   Os atributos de dimensão nos quais os membros existentes serão atualizados.  
  
-   As chaves dos membros existentes. Se um atributo usar uma chave composta, ela poderá exigir diversos valores.  
  
-   Os valores para qualquer propriedade de atributo aplicável que não são implementados como outros atributos dentro da dimensão. Tais propriedades de atributo incluem operações unárias, traduções, rollups personalizados, propriedades de rollup personalizadas e níveis ignorados.  
  
 O **atualização** comando leva apenas três propriedades obrigatórias:  
  
-   O **objeto** propriedade, que contém uma referência de objeto para a dimensão na qual os membros serão atualizados. A referência de objeto contém o identificador de banco de dados, o identificador de cubo e o identificador de dimensão para a dimensão.  
  
-   O **atributos** propriedade, que contém um ou mais **atributo** elementos para identificar os atributos em que os membros serão atualizados. O **atributo** elemento identifica um atributo e fornece o nome, valor, traduções, operador unário, rollup personalizado, propriedades de rollup personalizadas e níveis ignorados para um único membro atualizado para o atributo identificado.  
  
    > [!NOTE]  
    >  Todas as propriedades para o **atributo** elemento deve ser incluído. Caso contrário, poderá ocorrer um erro.  
  
-   O [onde](../../analysis-services/xmla/xml-elements-properties/where-element-xmla.md) propriedade, que contém um ou mais **atributo** elementos que restringem os atributos em que os membros serão atualizados. O **onde** propriedade é fundamental para limitar uma **atualização** comando para instâncias específicas de um membro. Se o **onde** propriedade não for especificada, todas as instâncias de um determinado membro serão atualizadas. Por exemplo, existem três clientes para quem você deseja alterar o nome da cidade de Redmond para Bellevue. Para alterar o nome da cidade, você deve fornecer um **onde** atributo de propriedade que identifica os três membros de cliente para que os membros do atributo City devem ser alterados. Se você não fornecer essa **onde** propriedade, todos os clientes cujo nome de cidade é Redmond teria o nome da cidade Bellevue após o **atualização** comando seja executado.  
  
    > [!NOTE]  
    >  Com exceção dos membros novos, o **atualizar** comando só pode atualizar valores de chave de atributo para atributos não incluídos no **onde** cláusula. Por exemplo, o nome da cidade não pode ser atualizado quando um cliente é atualizado; caso contrário, o nome da cidade seria alterado para todos os clientes.  
  
### <a name="updating-members-in-parent-attributes"></a>Atualizando membros em atributos pai  
 Para dar suporte a atributos pai, o **atualização** comando opcional [MoveWithDescendants](../../analysis-services/xmla/xml-elements-properties/movewithdescendants-element-xmla.md)possui propriedades. Definindo o **MoveWithDescendants** propriedade como true indica que os descendentes do membro pai também devem ser movidos com o membro pai quando o identificador desse membro pai é alterado. Se esse valor for definido como falso, mover um membro pai fará com que os descendentes imediatos desse membro pai sejam promovidos ao nível no qual o membro pai residia anteriormente.  
  
 Ao atualizar os membros em um atributo pai, o **atualizar** comando não pode atualizar membros em outros atributos.  
  
## <a name="dropping-existing-members"></a>Descartando membros existentes  
 Antes de criar o **Drop** de comando, você deve ter as seguintes informações disponíveis para os membros a serem removidos:  
  
-   A dimensão na qual os membros existentes serão descartados.  
  
-   Os atributos de dimensão nos quais os membros existentes serão descartados.  
  
-   As chaves dos membros existentes serem descartados. Se um atributo usar uma chave composta, ela poderá exigir diversos valores.  
  
 O **Drop** comando tem apenas duas propriedades obrigatórias:  
  
-   O **objeto** propriedade, que contém uma referência de objeto para a dimensão na qual os membros devem ser descartados. A referência de objeto contém o identificador de banco de dados, o identificador de cubo e o identificador de dimensão para a dimensão.  
  
-   O **onde** propriedade, que contém um ou mais **atributo** elementos para restringir os atributos em que os membros serão excluídos. O **onde** propriedade é fundamental para limitar uma **Drop** comando para instâncias específicas de um membro. Se o **onde** comando não for especificado, todas as instâncias de um determinado membro serão descartadas. Por exemplo, existem três clientes que você deseja descartar de Redmond. Para descartar esses clientes, você deve fornecer um **onde** propriedade que identifica os três membros do atributo Customer a ser removido e o membro Redmond do atributo cidade do qual os três clientes serão removidas. Se o **onde** propriedade especifica apenas o membro Redmond do atributo City, todos os clientes associados a Redmond serão descartados pelo **Drop** comando. Se o **onde** propriedade especifica apenas os três membros do atributo Customer, os três clientes serão excluídos completamente pelo **Drop** comando.  
  
    > [!NOTE]  
    >  O **atributo** elementos incluídos em um **Drop** comando deve conter apenas o **AttributeName** e **chaves** propriedades. Caso contrário, poderá ocorrer um erro.  
  
### <a name="dropping-members-in-parent-attributes"></a>Descartando membros em atributos pai  
 Definindo o [DeleteWithDescendants](../../analysis-services/xmla/xml-elements-properties/deletewithdescendants-element-xmla.md) propriedade indica que os descendentes de um membro pai também devem ser excluídos com o membro pai. Se esse valor for definido como falso, os descendentes imediatos do membro pai serão promovidos ao nível no qual o membro pai residia anteriormente.  
  
> [!IMPORTANT]  
>  Um usuário só precisa ter permissões de exclusão para o membro pai para poder excluir o membro pai e seus descendentes. Um usuário não precisa excluir permissões nos descendentes.  
  
## <a name="see-also"></a>Consulte também  
 [Remover elemento & #40; XMLA & #41;](../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)   
 [Inserir o elemento & #40; XMLA & #41;](../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [Atualizar o elemento & #40; XMLA & #41;](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [Definindo e identificando objetos &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/defining-and-identifying-objects-xmla.md)   
 [Desenvolvendo com XMLA no Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
