---
title: Conceder permissões em uma dimensão (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.roledesignerdialog.dimensions.f1
helpviewer_keywords:
- dimensions [Analysis Services], security
- read/write permissions
- user access rights [Analysis Services], dimensions
- permissions [Analysis Services], dimensions
ms.assetid: be5b2746-0336-4b12-827e-131462bdf605
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3efce85f27db9d0695ea56e9940ab563ed40537a
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66074955"
---
# <a name="grant-permissions-on-a-dimension-analysis-services"></a>Conceder permissões em uma dimensão (Analysis Services)
  A segurança de dimensão é usada para definir permissões em um objeto de dimensão, e não em seus dados. Normalmente, permitir ou negar acesso a operações de processamento é o principal objetivo ao definir as permissões em uma dimensão.  
  
 No entanto, seu objetivo, talvez, não seja controlar as operações de processamento, mas sim o acesso a dados de uma dimensão ou aos atributos e hierarquias nela contidos. Por exemplo, uma empresa com divisões regionais de vendas pode querer disponibilizar as informações de desempenho de vendas para os que estão fora da divisão. Para permitir ou negar acesso a partes de dados de dimensão para diferentes constituintes, você pode definir as permissões em atributos de dimensão e membros de dimensão. Observe que você não pode negar acesso a um objeto de dimensão individual em si, apenas a seus dados. Se o seu objetivo imediato é permitir ou negar acesso a membros de uma dimensão, incluindo os direitos de acesso a hierarquias de atributo individuais, consulte [Grant custom access to dimension data &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md) para obter mais informações.  
  
 O restante deste tópico abrange as permissões que podem ser definidas no próprio objeto de dimensão, incluindo:  
  
-   Permissões de leitura ou leitura/gravação (você só pode escolher entre leitura ou leitura/gravação; especificar "nenhum" não é uma opção). Como mencionado, se seu objetivo for restringir o acesso a dados de dimensão, consulte [Grant custom access to dimension data &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md) para obter detalhes.  
  
-   Permissões de processamento (faça isso quando cenários solicitarem uma estratégia de processamento que exija permissões personalizadas em objetos individuais)  
  
-   Permissões para ler definição (normalmente, você a usaria para dar suporte ao processamento interativo em uma ferramenta ou para dar visibilidade a um modelo. A permissão para ler definição permite que você veja a estrutura de uma dimensão, sem permissão quanto a seus dados ou à capacidade de modificar sua definição).  
  
 Ao definir as funções para uma dimensão, as permissões disponíveis variam, dependendo se o objeto é uma dimensão de banco de dados autônomo ─ interna em relação ao banco de dados, mas externa para um cubo ─ ou uma dimensão de cubo.  
  
> [!NOTE]  
>  Por padrão, as permissões em uma dimensão de banco de dados são herdadas por uma dimensão de cubo. Por exemplo, se você habilitar **Leitura/Gravação** em uma dimensão de banco de dados de clientes, a dimensão do cubo do cliente herdará **Leitura/Gravação** no contexto da função atual. Você pode apagar as permissões herdadas se quiser substituir uma configuração de permissão.  
  
## <a name="set-permissions-on-a-database-dimension"></a>Definir permissões em uma dimensão de banco de dados  
 As dimensões de banco de dados são objetos autônomos em um banco de dados, permitindo a reutilização da dimensão dentro do mesmo modelo. Considere uma dimensão de banco de dados DATE usada várias vezes em um modelo, como as dimensões de cubo Data do Pedido, Data de Remessa e Data de Vencimento. Como os cubos e as dimensões do banco de dados são objetos pares em um banco de dados, você pode configurar as permissões de processamento de forma independente em cada objeto.  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], expanda **Funções** para o banco de dados adequado no Pesquisador de Objetos e clique em uma função de banco de dados (ou crie uma nova função de banco de dados).  
  
2.  No painel **Dimensões** , a definição de dimensão deve ser definida como **Todas as definições do banco de dados**.  
  
     Por padrão, as permissões são definidas como **Leitura**.  
  
     Embora **Leitura/Gravação** esteja disponível, recomendamos não usar essa permissão. **Leitura/Gravação** é usada para cenários de write-back de dimensão, os quais foram preteridos. Ver [do Analysis Services preteridos Features in SQL Server 2014](../deprecated-analysis-services-features-in-sql-server-2014.md).  
  
     Como opção, você pode definir as permissões **Ler Definição** e **Processo** em objetos de dimensão individuais, desde que essas permissões não estejam definidas no nível de banco de dados. Consulte [Conceder permissões de processo &#40;Analysis Services&#41;](grant-process-permissions-analysis-services.md) e [Conceder permissões de leitura de definição em metadados de objeto &#40;Analysis Services&#41;](grant-read-definition-permissions-on-object-metadata-analysis-services.md) para obter detalhes.  
  
## <a name="set-permissions-on-a-cube-dimension"></a>Definir permissões em uma dimensão de cubo  
 As dimensões do cubo são dimensões de banco de dados que foram adicionadas a um cubo. Como tal, elas são estruturalmente dependentes de grupos de medidas associados. Embora você possa processar esses objetos atomicamente, em termos de autorização, faz sentido tratar os cubo e as dimensões de cubo como uma única entidade.  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], expanda **Funções** para o banco de dados adequado no Pesquisador de Objetos e clique em uma função de banco de dados (ou crie uma nova função de banco de dados).  
  
2.  No **dimensões** painel, altere a dimensão é definida como \<nome do cubo > **dimensões do cubo**.  
  
     Por padrão, as permissões são herdadas a partir de uma dimensão de banco de dados correspondente. Desmarque a caixa de seleção **Herdar** para alterar as permissões de **Leitura** para **Leitura/Gravação**. Antes de usar **Leitura/Gravação**, leia a observação na seção anterior.  
  
> [!IMPORTANT]  
>  Se você configurar permissões de função de banco de dados usando Objetos de Gerenciamento de Análise (AMO), qualquer referência a uma dimensão de cubo no atributo DimensionPermission de um cubo cortará a herança de permissão do atributo DimensionPermission do banco de dados. Para obter mais informações sobre AMO, consulte [Desenvolvendo com Objetos de Gerenciamento de Análise &#40;AMO&#41;](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo).  
  
## <a name="see-also"></a>Consulte também  
 [Funções e permissões &#40;Analysis Services&#41;](roles-and-permissions-analysis-services.md)   
 [Conceder permissões de cubo ou modelo &#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md)   
 [Conceder permissões em estruturas e modelos de mineração de dados &#40;Analysis Services&#41;](grant-permissions-on-data-mining-structures-and-models-analysis-services.md)   
 [Conceder acesso personalizado a dados da dimensão &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md)   
 [Conceder acesso personalizado a dados de célula &#40;Analysis Services&#41;](grant-custom-access-to-cell-data-analysis-services.md)  
  
  
