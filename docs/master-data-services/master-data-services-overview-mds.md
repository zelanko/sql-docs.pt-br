---
title: Visão geral do MDS (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 02/14/2017
ms.prod: sql
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
keywords:
- O que são dados mestres?
helpviewer_keywords:
- Master Data Services, overview
- Master Data Services
ms.assetid: 8a4c28b1-6061-4850-80b6-132438b8c156
caps.latest.revision: 28
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Active
ms.openlocfilehash: d2f03949fa0edab709dcdf14a71daad12d12022b
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="master-data-services-overview-mds"></a>Visão geral do MDS (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

 Este tópico descreve os principais recursos de organização e gerenciamento de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. 
  
 O [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] permite que você gerencie um conjunto mestre de dados da sua organização. Você pode organizar os dados em modelos, criar regras para atualizar os dados e controlar quem atualiza os dados. Com o Excel, você pode compartilhar o conjunto de dados mestre com outras pessoas em sua organização. 
  
 >  Para ver uma descrição da arquitetura do [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] , consulte o artigo [Master Data Services – The Basics](https://www.simple-talk.com/sql/database-delivery/master-data-services-basics) (Master Data Services – Noções básicas) em simple-talk.com. Para obter informações sobre os novos recursos do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], consulte [Novidades do MDS &#40;Master Data Services&#41;](../master-data-services/what-s-new-in-master-data-services-mds.md)  
   **Para obter instruções de como instalar o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], configurar o Site e o banco de dados e implantar os modelos de exemplo, consulte** [Instalação e configuração do Master Data Services](../master-data-services/master-data-services-installation-and-configuration.md).  
  
 No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], o modelo é o contêiner de nível mais alto na estrutura de dados mestres. Você cria um modelo para gerenciar grupos de dados semelhantes, por exemplo, para gerenciar dados de produtos online. Um modelo contém uma ou mais entidades, que por sua vez contêm membros que são os registros de dados. Uma entidade é semelhante a uma tabela.  
  
 Por exemplo, o seu modelo de produto online pode conter entidades como produto, cor e estilo. A entidade de cor pode conter membros para as cores vermelho, prata e preto.  
  
 ![Entidade de cor](../master-data-services/media/mds-productmodel-colorentity-composite.png "Entidade de cor")  
  
 Modelos também contêm atributos que são definidos em entidades. Um atributo contém valores que ajudam a descrever os membros da entidade. Há atributos de forma livre e atributos baseados em domínio.  Um atributo baseado em domínio contém valores que são preenchidos por membros de uma entidade e podem ser usados como valores de atributo para outras entidades.  
  
 Por exemplo, a entidade de produto poderia ter atributos de forma livre para custo e peso. Além disso, há um atributo baseado em domínio para a cor ![Número 1](../master-data-services/media/mds-number1.png "Número 1") que contém valores populados pelos membros da entidade de cor. Essa lista mestra de cores é usada como valores de atributo para a entidade Produto ![Número 2](../master-data-services/media/mds-number2.png "Número 2").  
  
 ![Atributo baseado em domínio para cor](../master-data-services/media/mds-productentity-color-domainattribute.png "Atributo baseado em domínio para cor")  
  
 As hierarquias derivadas são provenientes das relações entre entidades em um modelo. Estas são relações de atributo baseado em domínio. No modelo de produto, por exemplo, você pode ter uma hierarquia derivada de cor ![Número 1](../master-data-services/media/mds-number1.png "Número 1") proveniente da relação entre as entidades de cor ![Número 2](../master-data-services/media/mds-number2.png "Número 2") e produto ![Número 3](../master-data-services/media/mds-number3.png "Número 3").  
  
 ![Hierarquia derivada de cor](../master-data-services/media/mds-derivedhierarchy.png "Hierarquia derivada de cor")  
  
 Depois de definir uma estrutura básica para seus dados, você poderá iniciar a adição de registros de dados (membros) usando o recurso de importação. Você carrega dados em tabelas de preparo, valida os dados usando regras de negócio e carrega os dados nas tabelas MDS.  Você também pode usar as regras de negócio para definir valores de atributo.  
  
 A tabela a seguir descreve as tarefas principais [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Salvo indicação em contrário, todos os procedimentos a seguir exigem que você seja um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
> [!NOTE]  
>  Talvez você queira concluir as tarefas a seguir em um ambiente de teste e usar os dados de exemplo fornecidos quando instalar o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. Para obter mais informações, consulte [Implantando modelos &#40;Master Data Services&#41;](../master-data-services/deploying-models-master-data-services.md).  
  
|Ação|Detalhes|Tópicos relacionados|  
|------------|-------------|--------------------|  
|Criar um modelo|Ao ser criado, um modelo é considerado como VERSION_1.|[Modelos &#40;Master Data Services&#41;](../master-data-services/models-master-data-services.md)<br /><br /> [Criar um modelo &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md)|  
|Criar entidades|Crie quantas entidades forem necessárias para conter seus membros.|[Entidades &#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)<br /><br /> [Criar uma entidade &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md)|  
|Crie entidades para usar como atributos com base em domínio|Para criar um atributo com base em domínio, primeiro crie a entidade para preencher a lista de valores de atributo.|[Atributos baseados em domínio &#40;Master Data Services&#41;](../master-data-services/domain-based-attributes-master-data-services.md)<br /><br /> [Criar um atributo baseado em domínio &#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)|  
|Crie atributos para suas entidades|Crie atributos para descrever membros. Atributos de Nome e Código são incluídos automaticamente em cada entidade e não podem ser removidos. Talvez você queira criar outros atributos de forma livre para conter texto, datas, números ou arquivos.|[Atributos &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)<br /><br /> [Criar um atributo de texto &#40;Master Data Services&#41;](../master-data-services/create-a-text-attribute-master-data-services.md)<br /><br /> [Criar um atributo numérico &#40;Master Data Services&#41;](../master-data-services/create-a-numeric-attribute-master-data-services.md)<br /><br /> [Criar um atributo de data &#40;Master Data Services&#41;](../master-data-services/create-a-date-attribute-master-data-services.md)<br /><br /> [Criar um atributo de vínculo &#40;Master Data Services&#41;](../master-data-services/create-a-link-attribute-master-data-services.md)<br /><br /> [Criar um atributo de arquivo &#40;Master Data Services&#41;](../master-data-services/create-a-file-attribute-master-data-services.md)|  
|Crie grupos de atributos|Se você tiver mais de quatro ou cinco atributos para uma entidade, talvez queira criar grupos de atributos. Esses grupos são as guias exibidas acima da grade no **Gerenciador** , que facilitam a navegação agrupando atributos em guias individuais.|[Grupos de atributos &#40;Master Data Services&#41;](../master-data-services/attribute-groups-master-data-services.md)<br /><br /> [Criar um grupo de atributos &#40;Master Data Services&#41;](../master-data-services/create-an-attribute-group-master-data-services.md)|  
|Importar membros para suas entidades de apoio|Importe os dados para suas entidades de suporte usando o processo de preparo. Para o modelo de Produto, isso poderia significar a importação de cores ou tamanhos. Também é possível criar membros manualmente.<br /><br /> <br /><br /> Observação: os usuários podem criar membros no [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] se tiverem no mínimo uma permissão de **Atualização** no objeto modelo de folha de uma entidade e acesso à área funcional do **Gerenciador** .|[Visão geral: Importando dados de tabelas &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)<br /><br /> [Criar um membro folha &#40;Master Data Services&#41;](../master-data-services/create-a-leaf-member-master-data-services.md)|  
|Criar e aplicar regras de negócio para garantir a qualidade dos dados|Crie e publique regras de negócio para garantir a exatidão de seus dados. Você pode usar regras de negócio para:<br /><br /> Definir valores de atributo padrão.<br /><br /> Alterar valores de atributo.<br /><br /> Enviar notificações de email quando os dados não passam na validação de regras de negócio.|[Regras de negócio &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)<br /><br /> [Criar e publicar uma regra de negócio &#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)<br /><br /> [Validar membros específicos em relação a regras de negócio (Master Data Services)](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)<br /><br /> [Configurar notificações por email &#40;Master Data Services&#41;](../master-data-services/configure-email-notifications-master-data-services.md)<br /><br /> [Configurar regras de negócio para enviar notificações &#40;Master Data Services&#41;](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)|  
|Importar membros para suas entidades primárias e aplicar regras de negócio|Importe membros para suas entidades primárias usando o processo de preparo. Ao concluir, valide a versão, o que aplica regras de negócio a todos os membros na versão do modelo.<br /><br /> Em seguida, você poderá trabalhar na correção de eventuais problemas de validação de regra de negócio.|[Validação &#40;Master Data Services&#41;](../master-data-services/validation-master-data-services.md)<br /><br /> [Validar uma versão em relação a regras de negócio &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)<br /><br /> [Procedimento armazenado de validação &#40;Master Data Services&#41;](../master-data-services/validation-stored-procedure-master-data-services.md)|  
|Criar hierarquias derivadas|Hierarquias derivadas podem ser atualizadas conforme suas necessidades comerciais mudarem, garantindo que todos os membros sejam levados em conta no nível apropriado.|[Hierarquias derivadas &#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-master-data-services.md)<br /><br /> [Criar uma hierarquia derivada &#40;Master Data Services&#41;](../master-data-services/create-a-derived-hierarchy-master-data-services.md)|  
|Se necessário, crie hierarquias explícitas|Se quiser criar hierarquias que não sejam fundamentadas em nível e incluam membros de uma única entidade, você pode criar hierarquias explícitas.|[Hierarquias explícitas &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)<br /><br /> [Criar uma hierarquia explícita &#40;Master Data Services&#41;](../master-data-services/create-an-explicit-hierarchy-master-data-services.md)|  
|Se necessário, crie coleções|Se quiser exibir diferentes agrupamentos de membros para fins de relatório ou análise e não precisar de uma hierarquia completa, crie uma coleção.<br /><br /> <br /><br /> Observação: os usuários podem criar coleções no [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] se tiverem no mínimo uma permissão de **Atualização** no objeto modelo de coleção e acesso à área funcional do **Gerenciador** .|[Coleções &#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md)<br /><br /> [Criar uma coleção &#40;Master Data Services&#41;](../master-data-services/create-a-collection-master-data-services.md)|  
|Criar metadados definidos pelo usuário|Para descrever seus objetos de modelo, adicione metadados definidos pelo usuário ao seu modelo. Os metadados podem incluir o proprietário de um objeto ou a origem dos dados.||  
|Bloquear uma versão do seu modelo e atribuir um sinalizador de versão|Bloqueie uma versão do seu modelo para impedir alterações nos membros, exceto por administradores. Quando os dados da versão tiverem sido validados com êxito de acordo com as regras de negócio, você poderá confirmar a versão, o que impedirá alterações nos membros por qualquer usuário.<br /><br /> Crie e atribua um sinalizador de versão ao modelo. Os sinalizadores ajudam os usuários e sistemas de assinatura a identificar qual versão de um modelo usar.|[Versões &#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)<br /><br /> [Bloquear uma versão &#40;Master Data Services&#41;](../master-data-services/lock-a-version-master-data-services.md)<br /><br /> [Criar um sinalizador de versão &#40;Master Data Services&#41;](../master-data-services/create-a-version-flag-master-data-services.md)|  
|Criar exibições de assinatura|Para que seus sistemas de assinatura utilizem seus dados mestre, crie exibições de assinatura, que geram exibições padrão no banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|[Visão geral: Exportando dados &#40;Master Data Services&#41;](../master-data-services/overview-exporting-data-master-data-services.md)<br /><br /> [Criar uma exibição de assinatura para exportar dados &#40;Master Data Services&#41;](../master-data-services/create-a-subscription-view-to-export-data-master-data-services.md)|  
|Configurar permissões de usuário e de grupo|Não é possível copiar permissões de usuário e de grupo de um ambiente de teste para um ambiente de produção. Entretanto, o ambiente de teste pode ser usado para determinar a segurança a ser usada subsequentemente na produção.|[Segurança &#40;Master Data Services&#41;](../master-data-services/security-master-data-services.md)<br /><br /> [Adicionar um grupo &#40;Master Data Services&#41;](../master-data-services/add-a-group-master-data-services.md)<br /><br /> [Adicionar um usuário &#40;Master Data Services&#41;](../master-data-services/add-a-user-master-data-services.md)|  
  
 Quando estiver pronto, você poderá implantar o seu modelo, com ou sem os respectivos dados, no ambiente de produção. Para obter mais informações, consulte [Implantando modelos &#40;Master Data Services&#41;](../master-data-services/deploying-models-master-data-services.md).  
  
  

