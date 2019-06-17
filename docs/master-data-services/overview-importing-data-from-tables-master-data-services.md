---
title: 'Visão geral: Importando dados de tabelas (Master Data Services) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- staging process [Master Data Services], about staging process
- importing data [Master Data Services]
- staging process [Master Data Services]
ms.assetid: 181d1e22-379c-45d1-b03c-e1e22ff14164
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: e32932bff030fd187349c4b2c7adcaf65aed304f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65489597"
---
# <a name="overview-importing-data-from-tables-master-data-services"></a>Visão geral: Importando dados de tabelas (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Depois de criar um modelo para seus dados no [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], você pode começar a adicionar dados e fazer alterações nos dados.   Você usa as tabelas de preparo do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] , procedimentos armazenados e o Master Data Manager.  
  
 Para obter instruções sobre como adicionar e modificar dados, consulte [Importar dados de tabelas &#40;Master Data Services&#41;](../master-data-services/import-data-from-tables-master-data-services.md).  
  
> [!NOTE]
>  Você também pode usar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] para adicionar dados ao repositório do MDS (banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]) do Excel. Para obter mais informações, confira [Visão geral: importando dados do Excel &#40;Suplemento MDS para Excel&#41;](../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md).  
  
 Ao adicionar e modificar dados, você pode fazer o seguinte.  
  
-   Carregar e atualizar membros e atualizar valores de atributo  
  
-   Desativar e excluir membros  
  
-   Mover membros de hierarquia explícita  
  
 A adição e atualização de dados incluem as principais tarefas a seguir.  
  
1.  Carregar dados nas tabelas de preparo no banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
2.  Carregar dados das tabelas de preparo para as tabelas apropriadas do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
     Use os procedimentos armazenados de preparo ou o [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] para carregar os dados.  
  
> [!NOTE]  
>  No [!INCLUDE[ssSQL15](../includes/sssql15-md.md)], o suporte para os processos de preparo do [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] foi preterido.  
  
## <a name="deactivating-and-deleting-members-mds"></a>Desativando e excluindo membros (MDS)  
 Desativar significa que o membro pode ser reativado. Se você reativar um membro, seus atributos e sua associação em hierarquias e coleções serão restaurados. Todas as transações anteriores estão intactas. Transações de desativação são visíveis para administradores na área funcional **Gerenciamento de versões** do Master Data Manager.  
  
 Excluir significa limpar o membro permanentemente do sistema. Todas as transações do membro, todas as relações e todos os atributos são excluídos permanentemente.  
  
> [!NOTE]  
>  Você não pode usar preparo para reativar membros. Você deve fazer isto manualmente no Master Data Manager. Para obter mais informações, consulte [Reativar um membro ou uma coleção &#40;Master Data Services&#41;](../master-data-services/reactivate-a-member-or-collection-master-data-services.md).  
>   
>  Você não pode usar preparação para excluir ou desativar coleções. Para obter mais informações sobre como desativar coleções manualmente, consulte [Excluir um membro ou uma coleção &#40;Master Data Services&#41;](../master-data-services/delete-a-member-or-collection-master-data-services.md).  
  
## <a name="moving-explicit-hierarchy-members-mds"></a>Movendo membros de hierarquia explícita (MDS)  
 Quando você move o local dos membros em hierarquias explícitas em massa, você pode designar o seguinte.  
  
-   Um membro consolidado como um pai de um membro consolidado.  
  
-   Um membro consolidado como um pai de um membro folha.  
  
-   Um membro folha como irmão de um membro folha ou consolidado.  
  
-   Um membro consolidado como irmão de um membro folha ou consolidado.  
  
## <a name="staging-tables-and-stored-procedures-mds"></a>Tabelas de preparo e procedimentos armazenados (MDS)  
 O banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] inclui os seguintes tipos de tabelas de preparo que você pode preencher com seus dados.  
  
-   [Tabela de preparo de membros folha &#40;Master Data Services&#41;](../master-data-services/leaf-member-staging-table-master-data-services.md)  
  
-   [Tabela de preparo de membros consolidados &#40;Master Data Services&#41;](../master-data-services/consolidated-member-staging-table-master-data-services.md)  
  
-   [Tabela de preparo de relações &#40;Master Data Services&#41;](../master-data-services/relationship-staging-table-master-data-services.md)  
  
 Para cada entidade no modelo, existe uma tabela de preparo. O nome da tabela indica a entidade correspondente e o tipo de entidade como membro folha. A imagem a seguir mostra as tabelas de preparo para as entidades de moeda, cliente e produto.  
  
 ![Tabelas de preparo no banco de dados do MDS](../master-data-services/media/mds-staging-tables.png "Tabelas de preparo no banco de dados do MDS")  
  
 O nome de cada tabela é especificado quando uma entidade é criada e não pode ser alterado. Se o nome da tabela de preparo contiver um _1 ou outro número, isso significa que outra tabela daquele nome já existia quando a entidade foi criada.  
  
 O [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] inclui os seguintes tipos de procedimentos de preparo armazenados.  
  
-   stg.udp_\<name>_Leaf  
  
-   stg.udp_\<name>_Consolidated  
  
-   stg.udp_\<name>_Relationship  
  
 Para cada entidade no modelo, há três procedimentos armazenados que correspondem ao membro folha, membros consolidados e tabelas de preparo de relação.  A imagem a seguir mostra as tabelas de procedimentos de preparo armazenado para as entidades de moeda, cliente e produto.  
  
 ![Preparando procedimentos armazenados no banco de dados do MDS](../master-data-services/media/mds-staging-storedprocedures.png "Preparando procedimentos armazenados no banco de dados do MDS")  
  
 Para obter mais informações sobre os procedimentos armazenados, consulte [Preparando um procedimento armazenado &#40;Master Data Services&#41;](../master-data-services/staging-stored-procedure-master-data-services.md).  
  
## <a name="logging-transactions-mds"></a>Registrando transações em log (MDS)  
 Todas as transações que ocorrem quando dados ou relações são importados ou atualizados podem ser registradas em log. Uma opção do procedimento armazenado permite esse registro em log. Se você iniciar o processo de preparo usando [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], não ocorrerá registro em log.  
  
 No [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], a configuração **Registrar em log as transações de preparo** não se aplica a esse método de dados de preparo.  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Validação &#40;Master Data Services&#41;](../master-data-services/validation-master-data-services.md)  
  
-   [Regras de negócio &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
  
