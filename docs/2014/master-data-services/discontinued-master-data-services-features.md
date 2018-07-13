---
title: Recursos do Master Data Services no SQL Server 2014 descontinuados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3236cce0-cfd9-43f8-8be3-e8c8dff8f162
caps.latest.revision: 12
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: f2e9a15b4a0f1441d63ab39a4b65861fcfef099e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37167045"
---
# <a name="discontinued-master-data-services-features-in-sql-server-2014"></a>Recursos do Master Data Services descontinuados no SQL Server 2014
  Este tópico descreve os recursos do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] que não estão mais disponíveis no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="includesssql14includessssql14-mdmd-discontinued-features"></a>Recursos descontinuados do [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 Não há recursos descontinuados nesta versão.  
  
## <a name="includesssql11includessssql11-mdmd-discontinued-features"></a>Recursos descontinuados do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
  
### <a name="security"></a>Segurança  
 Para tornar a atribuição de segurança mais fácil, você não pode mais atribuir permissões de objeto de modelo a objetos da Hierarquia Derivada, da Hierarquia Explícita e do Grupo de Atributos.  
  
-   Agora, as permissões de hierarquia derivadas são baseadas no modelo. Por exemplo, se você quiser que um usuário tenha permissão para uma hierarquia derivada, você deve atribuir **atualização** para o objeto de modelo. Em seguida, você pode atribuir **Deny** acesso a qualquer entidade que você não deseja que o usuário tenha acesso.  
  
-   Agora, as permissões de hierarquia explícitas são baseadas na entidade. Por exemplo, se o usuário tiver **atualização** permissões a uma entidade de conta, em seguida, todas as hierarquias explícitas para a entidade será atualizáveis.  
  
-   Permissões de grupo de atributo não podem ser atribuídas a **permissões de usuário e grupo** área funcional. Em vez disso, nos **administração do sistema** área funcional em que os grupos de atributos são criados, os usuários e grupos podem receber **atualização** permissão a grupos de atributos. **Somente leitura** permissão a grupos de atributos não está mais disponível.  
  
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
 Regras de negócio que geram valores automaticamente para o atributo Code agora são administradas de maneira diferente. Anteriormente, para gerar valores para o atributo de código, você usou o **atributo padrão para um valor gerado** ação na **administração do sistema** área funcional em **regras de negócio** . Agora, na **administração do sistema**, você deve editar a entidade para habilitar os valores de códigos gerados automaticamente. Para obter mais informações, consulte [Criação automática de código &#40;Master Data Services&#41;](automatic-code-creation-master-data-services.md).  
  
 Se você tiver um pacote de implantação de modelo do [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] que contém uma regra deste tipo, quando atualizar o banco de dados para [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], a regra de negócios será excluída.  
  
### <a name="bulk-updates-and-exporting"></a>Atualizações e exportações em massa  
 No aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], você não pode mais atualizar valores de atributos em massa para vários membros. Para fazer atualizações em massa, use o processo de preparo ou o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)].  
  
 No aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], você não pode mais exportar membros para o Excel. Para trabalhar com membros no Excel, use o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)].  
  
### <a name="transactions"></a>Transactions  
 No **Explorer** área funcional, os usuários não podem mais reverter suas próprias transações. Anteriormente, os usuários podiam reverter alterações feitas nos dados no **Explorer**. Os administradores ainda podem reverter as transações para todos os usuários a **gerenciamento de versões** área funcional.  
  
 Agora, as anotações são permanentes e não podem ser excluídas. Anteriormente, as anotações eram consideradas transações e podiam ser excluídas com a reversão da transação.  
  
### <a name="web-service"></a>Serviço Web  
 Agora, serviço Web do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] é habilitado automaticamente, conforme exigido pelo Silverlight. Anteriormente, o serviço Web tinha de ser habilitado manualmente.  
  
### <a name="powershell-cmdlets"></a>Cmdlets do PowerShell  
 O MDS não contém mais cmdlets do PowerShell.  
  
## <a name="see-also"></a>Consulte também  
 [Recursos do Master Data Services preteridos no SQL Server 2014](deprecated-master-data-services-features.md)  
  
  
