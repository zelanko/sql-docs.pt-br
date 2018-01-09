---
title: Vincular grupos de medidas | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- linked measure groups [Analysis Services]
- referencing measure groups
- Linked Measure Group Wizard
- measure groups [Analysis Services], linked
- linked dimensions [Analysis Services]
ms.assetid: 7f838452-8669-4194-8e15-7afdc7f15251
caps.latest.revision: "41"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a5139e2e9e9d5bb06d594f9463f6632b6ee9fb78
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="linked-measure-groups"></a>Grupos de medidas vinculados
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Um grupo de medidas vinculado baseia-se em outro grupo de medidas em um cubo diferente no mesmo banco de dados ou outro banco de dados do Analysis Services. Você poderá usar um grupo de medidas vinculado se quiser reutilizar um conjunto de medidas, e os valores de dados correspondentes, em vários cubos.  
  
 A Microsoft recomenda que os grupos de medidas vinculados e originais residam em soluções executadas no mesmo servidor. Vincular a um grupo de medidas em um servidor remoto está agendada para substituição em uma versão futura (consulte [Recursos do Analysis Services preteridos no SQL Server 2016](../../analysis-services/deprecated-analysis-services-features-in-sql-server-2016.md)).  
  
> [!IMPORTANT]  
>  Os grupos de medidas vinculados são somente leitura. Para obter as alterações mais recentes, você deve excluir e recriar todos os grupos de medidas vinculados com base no objeto de origem modificado. Por esse motivo, copiar e colar os grupos de medidas entre projetos é uma abordagem alternativa que você deve considerar no caso da necessidade de alterações futuras ao grupo de medidas.  
  
## <a name="usage-limitations"></a>Limitações de uso  
 Como observado anteriormente, uma restrição importante ao uso de medidas vinculadas é uma incapacidade de personalizar uma medida vinculada diretamente. As modificações no tipo de dados, no formato, na associação de dados e na visibilidade, bem como a associação dos itens no próprio grupo de medidas, são alterações que devem ser feitas no grupo de medidas original.  
  
 Operacionalmente, os grupos de medidas vinculados são idênticos a outros grupos de medidas, quando acessados por aplicativos cliente e são consultados da mesma maneira que outros grupos de medidas.  
  
 Quando você consulta um cubo que contenha um grupo de medidas vinculado, o vínculo é estabelecido e resolvido durante a primeira fase de cálculo do cubo de destino. Devido a esse comportamento, qualquer cálculo armazenado no grupo de medidas vinculado não pode ser resolvido antes que a consulta seja avaliada. Em outras palavras, as medidas e células calculadas devem ser recriadas no cubo de destino em vez de herdadas do cubo de origem.  
  
 A lista a seguir resume as limitações de uso.  
  
-   Você não pode criar um grupo de medidas vinculado a partir de outro grupo de medidas vinculado.  
  
-   Você não pode adicionar ou remover medidas em um grupo de medidas vinculado. A associação é definida somente no grupo de medidas original.  
  
-   Não há suporte a write-back nos grupos de medidas vinculados.  
  
-   Os grupos de medidas vinculados não podem ser usados em vários relacionamentos muitos para muitos, especialmente quando esses relacionamentos estiverem em cubos diferentes. Fazer isso poderá resultar em agregações ambíguas. Para obter mais informações, consulte [Incorrect Amounts for Linked Measures in Cubes containing Many-to-Many Relationships](http://social.technet.microsoft.com/wiki/contents/articles/22911.incorrect-amounts-for-linked-measures-in-cubes-containing-many-to-many-relationships-ssas-troubleshooting.aspx)(Quantidades incorretas de medidas vinculadas em cubos com relacionamentos muitos para muitos).  
  
 As medidas contidas em um grupo de medidas vinculado podem ser diretamente organizadas apenas junto com dimensões vinculados recuperadas do mesmo banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . No entanto, você pode usar membros calculados para relacionar informações de grupos de medidas vinculados a outras dimensões não vinculadas no cubo. Você também pode usar uma relação indireta, como um referência ou relação muitos para muitos, para relacionar dimensões não vinculadas a um grupo de medidas vinculado.  
  
## <a name="create-or-modify-a-linked-measure"></a>Criar ou modificar uma medida vinculada  
 Use o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] para criar um grupo de medidas vinculado.  
  
1.  Finalize qualquer modificação feita no grupo de medidas original agora, no cubo de origem, de forma que você não precise recriar os grupos de medidas vinculados posteriormente em cubos subsequentes. Você pode renomear um objeto vinculado, mas não pode alterar qualquer outra propriedade.  
  
2.  No Gerenciador de Soluções, clique duas vezes no cubo ao qual você está adicionando o grupo de medidas vinculado. Esta etapa abre o cubo no Designer de Cubo.  
  
3.  No Designer de Cubo, no painel Medidas ou no painel Dimensões, clique com o botão direito do mouse em um dos painéis e selecione **Novo Objeto Vinculado**. Isso iniciará o Assistente para Objetos Vinculados.  
  
4.  Na primeira página, especifique a fonte de dados. Esta etapa confirma o local do grupo de medidas original. O padrão é o cubo atual no banco de dados atual, mas você também pode escolher um banco de dados do Analysis Services diferente.  
  
5.  Na página seguinte, escolha o grupo de medidas ou a dimensão que você deseja vincular. Os objetos de Dimensões e do Cubo, como grupos de medidas, são listados separadamente. Somente os objetos que ainda não estejam presentes no cubo atual estarão disponíveis.  
  
6.  Clique em **Concluir** para criar o objeto vinculado. Os objetos vinculados aparecem no painel Medidas e Dimensões, indicados pelo ícone de link.  
  
## <a name="secure-a-linked-measure"></a>Proteger uma medida vinculada  
 Depois que o vínculo tiver sido definido, o acesso às medidas em um grupo de medidas vinculado será gerenciado da mesma maneira que o acesso aos outros grupos de medidas. Um objeto vinculado aparece ao lado de suas contrapartes não vinculadas no Designer de Função. Para obter mais informações sobre como gerenciar a segurança de um grupo de medidas, consulte [Conceder permissões de cubo ou modelo &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md).  
  
 Para definir ou usar um grupo de medidas vinculado, a conta do serviço Windows para a instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] deve pertencer a uma função de banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que tenha direitos de acesso de **ReadDefinition** e **Read** para a instância de origem do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para o cubo de origem e grupo de medidas ou deve pertencer à função de Administradores do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] da instância [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de origem.  
  
## <a name="see-also"></a>Consulte Também  
 [Definir dimensões vinculadas](../../analysis-services/multidimensional-models/define-linked-dimensions.md)  
  
  
