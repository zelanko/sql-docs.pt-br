---
title: Conceder permissões Ler definição em metadados de objeto (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e6cc110a773981a7592f8cdd06b3fd10b2d83144
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50146371"
---
# <a name="grant-read-definition-permissions-on-object-metadata-analysis-services"></a>Conceder permissões para ler definição em metadados de objetos (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  A permissão para ler uma definição de objeto, ou metadados, em objetos selecionados permite que o administrador conceda permissão para exibir informações de objeto, sem conceder permissão para modificar a definição ou a estrutura do objeto ou para exibir os dados reais do objeto. As permissões**Ler Definição** podem ser concedidas no banco de dados, na fonte de dados, na dimensão, na estrutura de mineração e nos níveis de modelo de mineração. Se precisar de permissões **Ler Definição** para um cubo, você deverá habilitar **Ler Definição** para o banco de dados. Não se esqueça de que as permissões são aditivas. Por exemplo, uma função concede permissão para ler os metadados de um cubo, enquanto uma segunda função fornece ao mesmo usuário permissão para ler os metadados de uma dimensão. As permissões das duas funções diferentes são combinadas para fornecer ao usuário permissão para ler os metadados do cubo e os metadados da dimensão dentro desse banco de dados.  
  
> [!NOTE]  
>  A permissão para ler os metadados de um banco de dados é a permissão mínima necessária para conectar-se a um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ou o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Um usuário que tem permissão para ler os metadados também pode usar o conjunto de linhas de esquema DISCOVER_XML_METADATA para consultar o objeto e exibir os metadados. Para obter mais informações, consulte [Conjunto de linhas DISCOVER_XML_METADATA](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-xml-metadata-rowset).  
  
## <a name="set-read-definition-permissions-on-a-database"></a>Definir permissões Ler Definição em um banco de dados  
 Conceder permissão para ler os metadados de banco de dados também concede permissão para ler os metadados de todos os objetos do banco de dados.  
  
 Sugerimos que você inclua a permissão **Ler Definição** no nível de banco de dados sempre que estiver configurando funções para processamento dedicado. A **Ler Definição** permite que não administradores exibam a hierarquia de objetos de um modelo em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e naveguem até objetos individuais para processamento posterior.  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], expanda **Funções** para o banco de dados adequado no Pesquisador de Objetos e clique em uma função de banco de dados (ou crie uma nova função de banco de dados).  
  
2.  Na guia **Geral** , selecione a opção **Ler Definição** .  
  
3.  No painel **Associação** , insira as contas de usuário e de grupo do Windows que se conectam ao Analysis Services usando essa função.  
  
4.  Clique em **OK** para concluir a criação da função.  
  
## <a name="set-read-definition-permissions-on-individual-objects"></a>Definir permissões Ler Definição em objetos individuais  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], abra a pasta **Banco de Dados** , selecione um banco de dados, expanda **Funções** para o banco de dados apropriado no Pesquisador de Objetos e clique em uma função de banco de dados (ou crie uma nova função de banco de dados).  
  
2.  No painel **Geral** , desmarque a permissão de banco de dados para **Ler Definição**. Essa etapa remove a herança de permissão para que você possa definir permissões em objetos individuais.  
  
3.  Selecione o objeto para o qual você está especificando as propriedades **Ler Definição** :  
  
    -   No painel **Fontes de Dados** , clique na caixa de seleção **Ler Definição** para essa fonte de dados. Os membros da função podem ver a cadeia de conexão até a fonte de dados, incluindo o nome do servidor e, possivelmente, o nome de usuário. A permissão está disponível caso você queria fornecer informações da cadeia de conexão, sem conceder também a permissão para modificar a sequência de conexão ou exibir as definições de algum outro objeto.  
  
    -   No painel **Dimensões** , clique na caixa de seleção **Ler Definição** para essa dimensão. Analistas e desenvolvedores experientes talvez precisem exibir a definição sem permissão para modificar ou exibir as definições de outros objetos (como outras dimensões, objetos de cubo ou estruturas e modelos de mineração).  
  
    -   No painel Estruturas de Mineração, clique na caixa de seleção **Ler Definição** das estruturas ou modelos de mineração de dados. **Ler Definição** é necessário para navegar no modelo de dados. Consulte [Conceder permissões em estruturas e modelos de mineração de dados &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md) para obter mais detalhes.  
  
4.  No painel **Associação**, insira as contas de usuário e de grupo do Windows que se conectam ao Analysis Services usando essa função.  
  
5.  Clique em **OK** para concluir a criação da função.  
  
## <a name="see-also"></a>Consulte também  
 [Conceder permissões de banco de dados &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md)   
 [Conceder permissões de processo &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md)  
  
  
