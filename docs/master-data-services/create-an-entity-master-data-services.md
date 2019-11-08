---
title: Criar uma entidade
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- entities [Master Data Services], creating
- creating entities [Master Data Services]
ms.assetid: d9a6a51e-7b53-4785-a118-3baeb7ca2d48
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 6b06d77f562864a1b18e492d1db70563b62d4647
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728467"
---
# <a name="create-an-entity-master-data-services"></a>Criar uma entidade (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], crie uma entidade para conter os membros e seus atributos.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do Sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Deve existir um modelo. Para obter mais informações, consulte [Criar um modelo &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md).  
  
### <a name="to-create-an-entity"></a>Para criar uma entidade  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na página **Gerenciar modelo** , selecione na grade o modelo que você deseja criar e clique em **Entidades**.  
  
3.  Na página **Gerenciar entidade** , clique em **Adicionar**.  
  
4.  Na caixa **Nome** , digite o nome da entidade.  
  
5.  Opcionalmente, no campo **Descrição** , digite a descrição da entidade.  
  
6.  Opcionalmente, na caixa **Nome para tabelas de preparo** , digite um nome para a tabela de preparo.  
  
     Se você não preencher este campo, será usado o nome da entidade.  
  
    > [!TIP]  
    >  Use o nome do modelo como parte do nome da tabela de preparo, por exemplo, *Modelname_Entityname*. Isto facilita a localização das tabelas no banco de dados. Para obter mais informações sobre as tabelas de preparo, consulte [Visão geral: Importando dados de tabelas &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md).
    > [!TIP]
    > Se a nomenclatura padrão para tabelas de preparo for usada, o MDS acrescentará automaticamente identificadores (por exemplo, " 1", " 2") aos nomes de tabelas de preparo se existir uma entidade com o mesmo nome em outro modelo.
  
7.  No campo **Tipo de Log de Transações**, escolha o tipo de log de transações na lista suspensa.  
  
     Para obter mais informações, consulte [Alterar o tipo de log de transações da entidade &#40;Master Data Services&#41;](../master-data-services/change-the-entity-transaction-log-type-master-data-services.md)  
  
8.  Opcional. Marque a caixa de seleção **Criar valores de códigos automaticamente** . Para obter mais informações, consulte [Criação automática de código &#40;Master Data Services&#41;](../master-data-services/automatic-code-creation-master-data-services.md).  
  
9. Opcional. Marque a caixa de seleção **Habilitar a Compactação de Dados** . A compactação de linha é ativada por padrão. Para obter mais informações, consulte [Data Compression](../relational-databases/data-compression/data-compression.md).  
  
10. Clique em **Salvar**.  
  
## <a name="grid-columns"></a>Colunas da grade  
 Para cada entidade criada, uma linha com treze colunas é adicionada à grade. A seguir estão as colunas.  
  
|Nome|Descrição|  
|----------|-----------------|  
|Status|O status da entidade. Quando você clica em **Salvar** , a imagem a seguir é exibida, indicando que a entidade está atualizando.<br /><br /> ![Ícone para atualizar o status](../master-data-services/media/mds-statusicon-updating.png "Icon para atualizar o status ")<br /><br /> Se houver erros ao criar ou editar uma entidade, a imagem a seguir será exibida.<br /><br /> ![Ícone para status de erro](../master-data-services/media/mds-statusicon-error.png "Icon para status de erro ")<br /><br /> Se o status for OK, a imagem a seguir será exibida.<br /><br /> ![Ícone para status OK](../master-data-services/media/mds-statusicon-ok.png "Icon status OK ")|  
|Nome|O nome da entidade.|  
|Descrição|A descrição da entidade.|  
|Tabela de preparo|Nome do prefixo da tabela usado para armazenar dados.|  
|Tipo de Log de transações|O tipo de log de transações da entidade.|  
|Criação automática de código|Especifica se a criação automática de código está habilitada.|  
|Compactação de dados|Especifica se a compactação de dados está habilitada para a entidade.|  
|É o Destino da Sincronização|Especifica se a entidade é o destino de uma relação de sincronização.|  
|Hierarquia está Habilitada|Especifica se a entidade está habilitada para hierarquias explícitas. Essa coluna mostra Sim se existir pelo menos uma hierarquia explícita criada para a entidade.|  
|Criado por|O nome do usuário que criou a entidade.|  
|Criado em|A data e a hora em que a entidade foi criada.|  
|Atualizado por|O nome do usuário que atualizou a entidade pela última vez.|  
|Atualizado em|A data e a hora em que a entidade foi atualizada pela última vez.|  
  
## <a name="next-steps"></a>Próximas etapas  
  
-   [Criar um atributo de texto &#40;Master Data Services&#41;](../master-data-services/create-a-text-attribute-master-data-services.md)  
  
-   [Criar um atributo baseado em domínio &#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)  
  
-   [Criar um atributo de arquivo &#40;Master Data Services&#41;](../master-data-services/create-a-file-attribute-master-data-services.md)  
  
## <a name="see-also"></a>Consulte também  
 [Entidades &#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)   
 [Hierarquias explícitas &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)   
 [Editar uma entidade &#40;Master Data Services&#41;](../master-data-services/edit-an-entity-master-data-services.md)   
 [Excluir uma entidade &#40;Master Data Services&#41;](../master-data-services/delete-an-entity-master-data-services.md)  
  
  
