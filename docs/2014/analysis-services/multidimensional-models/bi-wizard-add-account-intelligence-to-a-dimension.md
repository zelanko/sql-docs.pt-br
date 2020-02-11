---
title: Adicionar inteligência de conta a uma dimensão | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- dimensions [Analysis Services], Business Intelligence enhancements
- Business Intelligence enhancements [Analysis Services], account intelligence
- account intelligence [Analysis Services]
ms.assetid: 36f454ae-a9f2-4a59-b19d-40310af9f901
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 111948911c0fe7bdc0e7ce260a15b8efee50e9db
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66076897"
---
# <a name="add-account-intelligence-to-a-dimension"></a>Adicionar inteligência de conta a uma dimensão
  Adicione o aprimoramento da inteligência de conta a um cubo ou a uma dimensão para atribuir classificações de conta padrão, como receita e despesa, a membros de um atributo de conta. Esse aprimoramento também identifica os tipos de conta (como Ativo e Passivo) e atribui a agregação apropriada a cada tipo de conta. [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode usar as classificações para agregar contas ao longo do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tempo.  
  
> [!NOTE]  
>  A inteligência de conta está disponível somente para dimensões baseadas nas fontes de dados existentes. Para dimensões que foram criadas sem usar uma fonte de dados, execute o Assistente de Geração de Esquema para criar uma exibição da fonte de dados antes de adicionar a inteligência de conta.  
  
 Aplique a inteligência de conta a uma dimensão que especifica as informações da conta (por exemplo, nome, número e tipo da conta). Para adicionar inteligência de conta, use o Assistente de Business Intelligence e selecione a opção **Definir inteligência de conta** na página **Escolher Melhoria** . Esse assistente orienta você pelas etapas de seleção da dimensão à qual você deseja aplicar a inteligência de conta, de identificação dos atributos da dimensão de conta selecionada e de mapeamento de tipos de conta da tabela de dimensões para os tipos de conta reconhecidos pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
## <a name="selecting-a-dimension"></a>Selecionando uma dimensão  
 Na primeira página **Definir Inteligência de Conta** do assistente, especifique a dimensão à qual você quer aplicar a inteligência de conta. O aprimoramento de inteligência de conta adicionado à dimensão selecionada provocará alterações na dimensão. Essas alterações serão herdadas por todos os cubos que tiverem a dimensão selecionada.  
  
## <a name="specifying-account-attributes"></a>Especificando atributos de conta  
 Na página **Configurar Atributos de Dimensão** do assistente, especifique os atributos de conta da dimensão de conta selecionada. Primeiro, na coluna **Incluir** , marque a caixa de seleção ao lado de cada tipo de atributo de conta que você quer mapear para o atributo dessa dimensão. Em seguida, na coluna **Atributo de Dimensão** , expanda a lista suspensa e selecione o atributo da dimensão correspondente ao tipo de atributo selecionado. A seleção do atributo da lista configura a propriedade `Type` do atributo com os atributos de conta.  
  
## <a name="mapping-account-types"></a>Mapeando tipos de conta  
 A segunda página **Definir Inteligência de Conta** mapeia os valores de tipo de conta da tabela da dimensão para os tipos reconhecidos pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Essa página aparecerá somente se você incluiu na dimensão o atributo de dimensão **Tipo de Conta** . Para incluir a dimensão **Tipo de Conta** , na página **Definir Inteligência de Conta** do assistente, marque a caixa de seleção ao lado de **Tipo de Conta**e selecione o atributo apropriado.  
  
 Na segunda página **Definir Inteligência de Conta** , há duas colunas:  
  
-   A coluna **Tipos de Conta de Tabela de Origem** lista os tipos de conta que o assistente obtém da tabela de dimensões.  
  
-   A coluna **Tipos de Conta de Servidor** identifica o tipo de conta correspondente que o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] reconhece. A tabela a seguir lista os tipos de conta que o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] reconhece e a agregação padrão para cada um deles. As seleções serão feitas automaticamente se a tabela de dimensões usar o mesmo nome de tipo de conta que o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
    |Tipo de conta de servidor|Agregação|DESCRIÇÃO|  
    |-------------------------|-----------------|-----------------|  
    |**Estatística**|`None`|Uma taxa calculada de algo ou a contagem de algo que não é agregada no decorrer do tempo. Esse tipo de conta não é convertido em outras moedas pelas regras de conversão.|  
    |**Obrigação**|`LastNonEmpty`|O dinheiro ou valor de coisas devidos em um momento específico. Esse tipo de conta não é acumulado com o passar do tempo e, portanto, não é agregado naturalmente no decorrer do tempo. Por exemplo, a quantia de Ano é o valor do último mês com dados. Esse tipo de conta é convertido em outras moedas com a taxa Fim do Período.|  
    |**Ativo**|`LastNonEmpty`|O dinheiro ou valor de coisas de propriedade em um momento específico. Esse tipo de conta não é acumulado com o passar do tempo e, portanto, não é agregado naturalmente com o decorrer do tempo. Por exemplo, a quantia de Ano é o valor do último mês com dados. Esse tipo de conta é convertido em outras moedas com a taxa Fim do Período.|  
    |**Saldo**|`LastNonEmpty`|A contagem de algo em um momento especificado. Esse tipo de conta é acumulado, mas não agregado naturalmente com o passar do tempo. Por exemplo, a quantia de Ano é o valor do último mês com dados.|  
    |**Fluxo**|`Sum`|Uma conta com incremento de algo. Esse tipo de conta é agregado com o passar do tempo como uma `Sum` mas não é convertido pelas regras de conversão de moeda.|  
    |**Custos**|`Sum`|O dinheiro ou valor de coisas gasto. Esse tipo de conta é agregado com o passar do tempo como uma `Sum` e é convertido em outras moedas pela taxa média.|  
    |**Líqui**|`Sum`|O dinheiro ou valor de coisas recebido. Esse tipo de conta é agregado com o passar do tempo como uma `Sum` e é convertido em outras moedas pela taxa média.|  
  
    > [!NOTE]  
    >  Se apropriado, é possível mapear mais de um tipo de conta da dimensão para um determinado tipo de conta de servidor.  
  
 Para alterar as agregações padrão mapeadas para cada tipo de conta de um banco de dados, use o Designer de Banco de Dados.  
  
1.  No Gerenciador de Soluções, clique com o botão direito do mouse no projeto do Analysis Services e clique em **Editar Banco de Dados**.  
  
2.  Na caixa **Mapeamento de Tipo de Conta** , selecione um tipo de conta no **Nome**.  
  
3.  Na caixa de texto **Alias** , digite um alias para esse tipo de conta.  
  
4.  Na caixa de listagem suspensa **Função de Agregação** , altere a Função de Agregação padrão para esse tipo de conta.  
  
  
