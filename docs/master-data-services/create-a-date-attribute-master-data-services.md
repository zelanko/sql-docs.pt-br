---
title: Criar um atributo de data
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- creating date attributes [Master Data Services]
- attributes [Master Data Services], creating date attributes
ms.assetid: 22a8f1a3-b4f2-4cfa-8495-7daad5ce9d12
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 8ffc7c1e901e3c93701c4e94ed62b8e70dbb7c0a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73728510"
---
# <a name="create-a-date-attribute-master-data-services"></a>Criar um atributo de data (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], crie um atributo de data quando desejar que os usuários insiram uma data como um valor de atributo.  
  
> [!NOTE]  
>  O atributo é chamado DateTime, mas valores de tempo não têm suporte.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, consulte [administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Você deve ter uma entidade para a qual possa criar o atributo. Para obter mais informações, consulte [criar uma entidade &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md).  
  
### <a name="to-create-a-date-attribute"></a>Para criar um atributo de data  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na página **gerenciar modelo** , selecione um modelo na grade e clique em **entidades**.  
  
3.  Na página **Gerenciar Entidade** , selecione a linha da entidade para a qual deseja criar um atributo.  
  
4.  Clique em **Atributos**.  
  
5.  Na página **Gerenciar Atributos** , execute um dos procedimentos a seguir e clique em **Adicionar**.  
  
    -   Se o atributo for para membros folha, selecione **Folha** na caixa de listagem **Tipos de Membro** .  
  
    -   Se o atributo for para membros consolidados, selecione **Consolidado** na caixa de listagem **Tipos de Membro** .  
  
    -   Se o atributo for para coleções, selecione **Coleção** na caixa de listagem **Tipos de Membro** .  
  
6.  Na caixa **Nome** , digite um nome para o atributo. Para obter uma lista de palavras que não devem ser usadas como nomes de atributos, consulte [palavras reservadas &#40;Master Data Services&#41;](../master-data-services/reserved-words-master-data-services.md).  
  
7.  Opcionalmente, digite um nome de exibição e digite uma descrição para o atributo na caixa **Descrição** .  
  
8.  Na caixa **Exibir largura em pixels** , digite a largura da coluna de atributo a ser exibida na grade do **Gerenciador** .  
  
9. Na lista **Tipo de atributo** , selecione **Forma livre**.  
  
10. Na lista **Tipo de dados** , selecione **DateTime**.  
  
11. Na lista **Máscara de entrada** , selecione um formato para datas.  
  
12. Opcionalmente, selecione **Habilitar controle de alterações** para controlar alterações de grupos de atributos. Para obter mais informações, consulte [Adicionar atributos a um grupo de controle de alterações &#40;Master Data Services&#41;](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md).  
  
13. Clique em **Salvar**.  
  
## <a name="to-display-the-time-portion-of-a-datetime-value"></a>Para exibir a porção de tempo de um valor datetime  
 Para que a interface de usuário exiba a porção de hora de um valor datetime, você deve selecionar uma máscara de entrada apropriada para o atributo. Nenhuma das máscaras internas para os atributos Datetime faz isso, mas você pode adicionar uma nova máscara que permitirá que você exiba a hora. Para fazer isso, adicione uma linha na tabela mdm.tblList do banco de dados MDS, onde as máscaras internas estão armazenadas. A linha deve ter os seguintes valores:  
  
|||  
|-|-|  
|ListCode|lstInputMask|  
|ListName|Máscara de entrada|  
|Seq|19|  
|Opção de Lista|dd/MM/aaaa hh:mm:ss tt|  
|ID de opção|19|  
|IsVisible|1|  
|ID do grupo|3|  
  
 Depois de inserir uma linha com os valores acima na tabela mdm.tblList, a máscara "dd/MM/aaaa hh:mm:ss tt" estará disponível na caixa de listagem de máscaras de entrada. Você pode então selecionar essa máscara para exibir a data e a hora em uma coluna de atributo de datetime de uma entidade no MDS Explorer.  
  
 A máscara de entrada é uma cadeia de caracteres de formato DateTime .NET personalizada. Para obter mais informações, consulte [Cadeias de caracteres personalizadas de formato data e hora](https://msdn.microsoft.com/library/8kb3ddd4\(v=vs.110\).aspx)  
  
## <a name="see-also"></a>Consulte Também  
 [Atributos &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)   
 [Alterar um nome de atributo e um tipo de dados &#40;Master Data Services&#41;](../master-data-services/change-an-attribute-name-and-data-type-master-data-services.md)   
 [Criar um atributo baseado em domínio &#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)   
 [Criar um atributo de arquivo &#40;Master Data Services&#41;](../master-data-services/create-a-file-attribute-master-data-services.md)  
  
  
