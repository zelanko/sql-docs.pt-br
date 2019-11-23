---
title: Criar um atributo de arquivo
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- creating file attributes [Master Data Services]
- attributes [Master Data Services], creating file attributes
ms.assetid: d224886b-2ef1-4658-8b01-2213cc4b8df6
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 03892413f5aad3bb33cad4bf3d2dfaa8c468e7e9
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728549"
---
# <a name="create-a-file-attribute-master-data-services"></a>Criar um atributo de arquivo (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], crie um atributo de arquivo para popular os valores de atributo com arquivos.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do Sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Uma entidade deve existir para que se possa criar o atributo para ela. Para obter mais informações, consulte [Criar uma entidade &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md).  
  
## <a name="attribute-information"></a>Informações de Atributo  
 Para cada atributo criado, uma linha com sete colunas é adicionada à grade. A tabela a seguir descreve as colunas.  
  
|Column|Descrição|  
|------------|-----------------|  
|Status|O status do atributo.<br /><br /> Quando você clica em salvar, o ![ícone para atualizar a imagem de status](../master-data-services/media/mds-statusicon-updating.png "Icon para atualizar o status ") é exibido, indicando que o atributo está sendo atualizado.<br /><br /> Se houver erros ao criar ou editar um atributo, a imagem ![ícone para o status de erro](../master-data-services/media/mds-statusicon-error.png "Icon para status de erro ") será exibida.<br /><br /> Caso contrário, o status é OK e o ![ícone para a imagem de status OK](../master-data-services/media/mds-statusicon-ok.png "Icon status OK ") é exibido.|  
|NAME|O nome do atributo.|  
|Nome de Exibição|O nome de exibição do atributo.|  
|Descrição|A descrição do atributo.|  
|Exibir Largura em Pixels|A largura do atributo.|  
|Tipo e Propriedades|As informações de tipo e de tipo de dados do atributo.|  
|Habilitar Controle de Alterações|Especifica se o atributo está habilitado para o controle de alterações e mostra o número do grupo entre parênteses.|  
  
 Quando você clica em um atributo, as seguintes informações são exibidas.  
  
-   **Criado Por**: o nome do usuário que criou o atributo.  
  
-   **Em**: a data e hora em que o atributo foi criado.  
  
-   **Atualizado Por**: o nome do usuário que atualizou o atributo pela última vez.  
  
-   **Em**: a data e a hora em que o atributo foi atualizado pela última vez.  
  
### <a name="to-create-a-file-attribute"></a>Para criar um atributo de arquivo  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na página **Gerenciar Modelo** , escolha um modelo na grade e clique em **Entidades**.  
  
3.  Na página **Gerenciar Entidade** , selecione a linha da entidade para a qual deseja criar um atributo.  
  
4.  Clique em **Atributos**.  
  
5.  Na página **Gerenciar Atributos** , execute um dos procedimentos a seguir e clique em **Adicionar**.  
  
    -   Se o atributo for para membros folha, selecione **Folha** na caixa de listagem **Tipos de Membro** .  
  
    -   Se o atributo for para membros consolidados, selecione **Consolidado** na caixa de listagem **Tipos de Membro** .  
  
    -   Se o atributo for para coleções, selecione **Coleção** na caixa de listagem **Tipos de Membro** .  
  
6.  Na caixa **Nome** , digite um nome para o atributo. Para obter uma lista de palavras que não devem ser usadas como nomes de atributo, consulte [Palavras reservadas &#40;Master Data Services&#41;](../master-data-services/reserved-words-master-data-services.md).  
  
7.  Opcionalmente, digite um nome de exibição e digite uma descrição para o atributo na caixa **Descrição** .  
  
8.  Na caixa **Exibir largura em pixels** , digite a largura da coluna de atributo a ser exibida na grade do **Gerenciador** .  
  
9. Na lista **Tipo de atributo** , selecione **Arquivo**.  
  
10. Na lista **Extensão do arquivo** , selecione o tipo de arquivo que os usuários podem carregar ou aceite o valor padrão (*.\*) para permitir todos os tipos de arquivos.  
  
11. Opcionalmente, selecione **Habilitar controle de alterações** para controlar alterações de grupos de atributos. Para obter mais informações, consulte [Adicionar atributos a um grupo de controle de alterações &#40;Master Data Services&#41;](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md).  
  
12. Clique em **Salvar**.  
  
## <a name="see-also"></a>Consulte também  
 [Atributos &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)   
 [Alterar um nome de atributo e um tipo de dados &#40;Master Data Services&#41;](../master-data-services/change-an-attribute-name-and-data-type-master-data-services.md)   
 [Criar um atributo baseado em domínio &#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)   
 [Criar um atributo de texto &#40;Master Data Services&#41;](../master-data-services/create-a-text-attribute-master-data-services.md)  
  
  
