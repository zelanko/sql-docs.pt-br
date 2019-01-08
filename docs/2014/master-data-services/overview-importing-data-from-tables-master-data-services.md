---
title: Importação de dados (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- staging process [Master Data Services], about staging process
- importing data [Master Data Services]
- staging process [Master Data Services]
ms.assetid: 181d1e22-379c-45d1-b03c-e1e22ff14164
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: a3f9d1589c9e7434b16ce3f500b44eb1d9374cd8
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52756808"
---
# <a name="data-import-master-data-services"></a>Importação de dados (Master Data Services)
  Depois de criar um modelo para seus dados no [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], você pode começar a adicionar dados e fazer alterações nos dados, no banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .   Você usa as tabelas de preparo do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] , procedimentos armazenados e o Master Data Manager.  
  
 Você também pode usar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]para adicionar dados ao repositório do MDS ([!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] banco de dados). Para obter mais informações, consulte [dados de publicação &#40;suplemento MDS para Excel&#41;](microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md).  
  
 Ao adicionar e atualizar dados, você pode realizar os procedimentos a seguir.  
  
-   Carregar e atualizar membros e atualizar valores de atributo  
  
-   Desativar e excluir membros  
  
-   Mover membros de hierarquia explícita  
  
 A adição e atualização de dados incluem as principais tarefas a seguir.  
  
1.  Carregar dados nas tabelas de preparo no banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
2.  Carregar dados das tabelas de preparo para as tabelas apropriadas do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
     Use os procedimentos armazenados de preparo ou o [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] para carregar os dados.  
  
> [!NOTE]  
>  No [!INCLUDE[ssSQL14](../includes/sssql14-md.md)], o suporte para os processos de preparo do [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] foi preterido.  
  
## <a name="deactivating-and-deleting-members"></a>Desativando e excluindo membros  
 Desativar significa que o membro pode ser reativado. Se você reativar um membro, seus atributos e sua associação em hierarquias e coleções serão restaurados. Todas as transações anteriores estão intactas. Transações de desativação são visíveis para administradores na área funcional **Gerenciamento de versões** do Master Data Manager.  
  
 Excluir significa limpar o membro permanentemente do sistema. Todas as transações do membro, todas as relações e todos os atributos são excluídos permanentemente.  
  
> [!NOTE]  
>  Você não pode usar preparo para reativar membros. Você deve fazer isto manualmente no Master Data Manager. Para obter mais informações, consulte [Reativar um membro ou uma coleção &#40;Master Data Services&#41;](reactivate-a-member-or-collection-master-data-services.md).  
>   
>  Você não pode usar preparação para excluir ou desativar coleções. Para obter mais informações sobre como desativar coleções manualmente, consulte [Excluir um membro ou uma coleção &#40;Master Data Services&#41;](../../2014/master-data-services/delete-a-member-or-collection-master-data-services.md).  
  
## <a name="moving-explicit-hierarchy-members"></a>Movendo membros de hierarquia explícita  
 Quando você move o local dos membros em hierarquias explícitas em massa, você pode designar o seguinte.  
  
-   Um membro consolidado como um pai de um membro consolidado.  
  
-   Um membro consolidado como um pai de um membro folha.  
  
-   Um membro folha como irmão de um membro folha ou consolidado.  
  
-   Um membro consolidado como irmão de um membro folha ou consolidado.  
  
## <a name="staging-tables-and-stored-procedures"></a>Tabelas de preparo e procedimentos armazenados  
 O banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] inclui os seguintes tipos de tabelas de preparo que você pode preencher com seus dados.  
  
-   [Tabela de preparo de membros folha &#40;Master Data Services&#41;](../../2014/master-data-services/leaf-member-staging-table-master-data-services.md)  
  
-   [Tabela de preparo de membros consolidados &#40;Master Data Services&#41;](../../2014/master-data-services/consolidated-member-staging-table-master-data-services.md)  
  
-   [Tabela de preparo de relações &#40;Master Data Services&#41;](../../2014/master-data-services/relationship-staging-table-master-data-services.md)  
  
 Para cada entidade no modelo, existe uma tabela de preparo. O nome da tabela indica a entidade correspondente e o tipo de entidade como membro folha. A imagem a seguir mostra as tabelas de preparo para as entidades de moeda, cliente e produto.  
  
 ![Tabelas de preparo no banco de dados do MDS](../../2014/master-data-services/media/mds-stagingtables.png "Tabelas de preparo no banco de dados do MDS")  
  
 O nome de cada tabela é especificado quando uma entidade é criada e não pode ser alterado. Se o nome da tabela de preparo contiver um _1 ou outro número, isso significa que outra tabela daquele nome já existia quando a entidade foi criada.  
  
 O [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] inclui os seguintes tipos de procedimentos de preparo armazenados.  
  
-   stg.udp_\<name>_Leaf  
  
-   stg.udp_\<name>_Consolidated  
  
-   stg.udp_\<name>_Relationship  
  
 Para cada entidade no modelo, há três procedimentos armazenados que correspondem ao membro folha, membros consolidados e tabelas de preparo de relação.  A imagem a seguir mostra as tabelas de procedimentos de preparo armazenado para as entidades de moeda, cliente e produto.  
  
 ![Procedimentos armazenados de preparo no banco de dados do MDS](../../2014/master-data-services/media/mds-stagingstoredprocedures.png "procedimentos armazenados de preparo no banco de dados do MDS")  
  
 Para obter mais informações sobre os procedimentos armazenados, consulte [Preparando um procedimento armazenado &#40;Master Data Services&#41;](../../2014/master-data-services/staging-stored-procedure-master-data-services.md).  
  
## <a name="logging-transactions"></a>Registrando transações em log  
 Todas as transações que ocorrem quando dados ou relações são importados ou atualizados podem ser registradas em log. Uma opção do procedimento armazenado permite esse registro em log. Se você iniciar o processo de preparo usando [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], não ocorrerá registro em log.  
  
 No [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], a configuração **Registrar em log as transações de preparo** não se aplica a esse método de dados de preparo.  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Validação &#40;Master Data Services&#41;](../../2014/master-data-services/validation-master-data-services.md)  
  
-   [Regras de negócio &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)  
  
  
