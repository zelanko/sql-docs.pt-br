---
title: Recursos de Master Data Services descontinuados no SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 3236cce0-cfd9-43f8-8be3-e8c8dff8f162
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 3f1eb85cb05c8284990d46241ed752515ef5504b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65479434"
---
# <a name="discontinued-master-data-services-features-in-sql-server-2014"></a>Recursos do Master Data Services descontinuados no SQL Server 2014
  Este tópico descreve os recursos do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] que não estão mais disponíveis no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="sssql14-discontinued-features"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Recursos descontinuados  
 Não há recursos descontinuados nesta versão.  
  
## <a name="sssql11-discontinued-features"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Recursos descontinuados  
  
### <a name="security"></a>Segurança  
 Para tornar a atribuição de segurança mais fácil, você não pode mais atribuir permissões de objeto de modelo a objetos da Hierarquia Derivada, da Hierarquia Explícita e do Grupo de Atributos.  
  
-   Agora, as permissões de hierarquia derivadas são baseadas no modelo. Por exemplo, se você quiser que um usuário tenha permissão para uma hierarquia derivada, deverá atribuir **Atualizar** ao objeto de modelo. Em seguida, você pode atribuir acesso **negado** a todas as entidades às quais você não deseja que o usuário tenha acesso.  
  
-   Agora, as permissões de hierarquia explícitas são baseadas na entidade. Por exemplo, se o usuário tiver permissões de **atualização** para uma entidade de conta, todas as hierarquias explícitas para a entidade serão atualizáveis.  
  
-   As permissões de grupo de atributos não podem mais ser atribuídas na área funcional **permissões de usuário e grupo** . Em vez disso, na área funcional **Administração do sistema** em que os grupos de atributos são criados, os usuários e grupos podem receber permissão de **atualização** para grupos de atributos. A permissão **somente leitura** para grupos de atributos não está mais disponível.  
  
### <a name="staging-process"></a>Processo de preparo  
 Você não pode usar o novo processo de preparo para:  
  
-   Criar ou excluir coleções.  
  
-   Adicionar ou remover membros das coleções.  
  
-   Reativar membros e coleções.  
  
 Você pode usar o processo de preparo do [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] para trabalhar com coleções.  
  
### <a name="model-deployment-wizard"></a>Assistente de implantação de modelo  
 Os pacotes que contêm dados não podem mais ser criados e implantados com o assistente no aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]. Um novo utilitário de linha de comando pode ser usado. Para obter mais informações, consulte [Implantando modelos &#40;Master Data Services&#41;](deploying-models-master-data-services.md).  
  
 O assistente ainda pode ser usado para criar e implantar pacotes que não contêm dados.  
  
 Além disso, os pacotes podem ser implantados somente na edição do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] na qual eles foram criados. Isso significa que os pacotes criados no [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] não podem ser implantados no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]. Você deve implantar o pacote em um ambiente do [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] e, em seguida, atualizar o banco de dados para o [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].  
  
### <a name="code-generation-business-rules"></a>Regras de negócio de geração de código  
 Regras de negócio que geram valores automaticamente para o atributo Code agora são administradas de maneira diferente. Anteriormente, para gerar valores para o atributo de código, você usou o **atributo padrão para uma ação de valor gerado** na área funcional **Administração do sistema** em **regras de negócio**. Agora, na **Administração do sistema**, você deve editar a entidade para habilitar valores de código gerados automaticamente. Para obter mais informações, consulte [criação automática de código &#40;Master Data Services&#41;](automatic-code-creation-master-data-services.md).  
  
 Se você tiver um pacote de implantação de modelo do [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] que contém uma regra deste tipo, quando atualizar o banco de dados para [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], a regra de negócios será excluída.  
  
### <a name="bulk-updates-and-exporting"></a>Atualizações e exportações em massa  
 No aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], você não pode mais atualizar valores de atributos em massa para vários membros. Para fazer atualizações em massa, use o processo de preparo ou [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]o.  
  
 No aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], você não pode mais exportar membros para o Excel. Para trabalhar com membros no Excel, use o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)].  
  
### <a name="transactions"></a>Transações  
 Na área funcional **Gerenciador** , os usuários não podem mais reverter suas próprias transações. Anteriormente, os usuários podiam reverter as alterações feitas nos dados no **Explorer**. Os administradores ainda podem reverter transações para todos os usuários na área funcional **Gerenciamento de versões** .  
  
 Agora, as anotações são permanentes e não podem ser excluídas. Anteriormente, as anotações eram consideradas transações e podiam ser excluídas com a reversão da transação.  
  
### <a name="web-service"></a>Serviço Web  
 Agora, serviço Web do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] é habilitado automaticamente, conforme exigido pelo Silverlight. Anteriormente, o serviço Web tinha de ser habilitado manualmente.  
  
### <a name="powershell-cmdlets"></a>Cmdlets do PowerShell  
 O MDS não contém mais cmdlets do PowerShell.  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos do Master Data Services substituídos no SQL Server 2014](deprecated-master-data-services-features.md)  
  
  
