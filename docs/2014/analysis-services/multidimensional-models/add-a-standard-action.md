---
title: Adicionar uma ação padrão | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: ccb2928a-f75d-4acb-8ff8-fa80bb0935b2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 408f92b86cdfdd148ea11ca49b6ba540b0f4cf86
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48161086"
---
# <a name="add-a-standard-action"></a>Adicionar uma ação padrão
  Você adiciona uma ação a um banco de dados usando a exibição Ações no Designer de Cubo. Essa exibição pode ser acessada pelo [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Depois de você criar uma ação, ela ficará disponível a usuários depois que você reprocessar o cubo pertinente. Para obter mais informações, consulte [Processing Analysis Services Objects](processing-analysis-services-objects.md).  
  
### <a name="to-create-an-action"></a>Criar uma ação  
  
1.  Abra o cubo para o qual deseja criar uma ação, e clique na guia **Ações** .  
  
2.  Na barra de ferramentas, clique no ícone **Nova Ação** e, no painel de expressão, faça o seguinte:  
  
    -   Em **Nome**, digite um nome para a ação.  
  
    -   Na lista suspensa **Tipo de destino** , selecione o tipo de objeto ao qual você quer anexar a ação. O objeto que você selecionar em **Tipo de Destino** determina os objetos que estão disponíveis e o tipo de seleção que você pode fazer em **Objeto de Destino**. A tabela a seguir lista as seleções de **Objeto de Destino** válidas para cada tipo de destino.  
  
        |Se você selecionar o tipo de destino a seguir|Faça a seleção a seguir em Objeto de Destino|  
        |---------------------------------------------|---------------------------------------------------|  
        |Membros de atributo|A única seleção válida é uma única hierarquia de atributo. O tipo de destino da ação será todos os membros do atributo onde quer que eles apareçam (quer dizer, a ação também se aplicará a hierarquias definidas pelo usuário).|  
        |Células|Todas as células são a única seleção disponível. Se você escolher **Células** como um tipo de destino, poderá digitar uma expressão em **Condição** para restringir as células com as quais a ação está associada.|  
        |Cube|CURRENTCUBE é a única seleção disponível. A ação está associada ao cubo atual.|  
        |Membros de dimensão|Selecione uma única dimensão. A ação será associada a todos os membros da dimensão.|  
        |Hierarquia|Selecione uma única hierarquia. A ação será associada somente ao objeto de hierarquia. As hierarquias de atributo só aparecerão na lista se as propriedades **AttributeHierarchyEnabled** e **AttributeHierarchyVisible** forem definidas como **True**.|  
        |Membros de hierarquia|Selecione uma única hierarquia. A ação será associada a todos os membros da hierarquia selecionada. As hierarquias de atributo só aparecerão na lista se as propriedades **AttributeHierarchyEnabled** e **AttributeHierarchyVisible** forem definidas como **True**.|  
        |Nível|Selecione um único nível. A ação será associada somente ao objeto de nível.|  
        |Membros de nível|Selecione um único nível. A ação será associada a todos os membros do nível selecionado.|  
  
    -   Em **Objeto de destino**, clique na seta à direita da caixa de texto e, no modo de exibição de árvore que abre, clique no objeto ao qual você deseja anexar a ação e clique em **OK**.  
  
    -   (Opcional.) Em **Condição**, crie uma expressão MDX para limitar o destino da ação. Você pode digitar a expressão manualmente ou pode arrastar itens das guias **Metadados** e **Funções** .  
  
    -   Na lista suspensa **Tipo** , selecione o tipo de ação que você quer criar. A tabela a seguir lista os tipos de ações disponíveis.  
  
        |Tipo|Description|  
        |----------|-----------------|  
        |Dataset|Recupera um conjunto de dados.|  
        |Proprietário|Executa uma operação usando uma interface diferente das listadas nesta tabela.|  
        |Conjunto de linhas|Recupera um conjunto de linhas.|  
        |Instrução|Executa um comando OLE DB.|  
        |URL|Exibe uma página da Web em um navegador de Internet.|  
  
    -   Em **Expressão de ação**, crie uma expressão que define a ação. A expressão deve ser avaliada como uma cadeia de caracteres. Você pode digitar a expressão manualmente ou pode arrastar itens das guias **Metadados** e **Funções** .  
  
3.  (Opcional.) Expanda **Propriedades Adicionais**e execute uma das etapas a seguir:  
  
    -   Na lista suspensa **Invocação**, especifique como a ação é invocada. A tabela seguinte descreve as opções disponíveis para invocar uma ação.  
  
        |Opção|Description|  
        |------------|-----------------|  
        |Interativo|A ação é disparada pela interação do usuário.|  
        |Lote|A ação é executada como uma operação de lote.|  
        |Em aberto|A ação é executada quando um usuário abre o cubo.|  
  
    -   Em **Aplicativo**, digite o nome do aplicativo que está associado à ação. Por exemplo, se você criar uma ação que leva um usuário a um site específico, o aplicativo associado à ação deve ser Microsoft Internet Explorer ou outro navegador da Web.  
  
        > [!NOTE]  
        >  As ações proprietárias não são retornadas para o servidor a menos que o aplicativo cliente restrinja explicitamente o conjunto de linhas de esquema para retornar somente ações que correspondam ao nome especificadas em **Aplicativo**.  
  
    -   Na **conteúdo da ação**, se você estiver usando o tipo de URL, coloque o endereço de Internet entre aspas, por exemplo, "http://www.adventure-works.com".  
  
    -   Em **Descrição**, digite uma descrição para a ação.  
  
    -   Em **Legenda**, digite uma legenda ou uma expressão MDX avaliada como uma legenda. Esta legenda é exibida para usuários finais quando a ação é iniciada. Se você não especificar uma legenda, o nome da ação será usado.  
  
    -   Na lista suspensa **A legenda é MDX** , especifique se a legenda é MDX. Este campo indica para o servidor se deve avaliar o conteúdo de **Legenda** como uma expressão MDX.  
  
  
