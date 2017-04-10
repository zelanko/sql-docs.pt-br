---
title: "Regras de neg&#243;cio (Master Data Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/18/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "regras de negócio [Master Data Services], sobre regras de negócio"
  - "regras de negócio [Master Data Services]"
ms.assetid: a9f9e41a-2461-4845-b947-58b3a205543f
caps.latest.revision: 16
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 16
---
# Regras de neg&#243;cio (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], uma regra de negócio é uma regra usada para garantir a qualidade e a exatidão de seus dados mestres. Você pode usar uma regra de negócio para atualizar dados automaticamente, enviar email ou iniciar um processo empresarial ou fluxo de trabalho.  
  
 Para ver exemplos de regras de negócio, consulte [exemplos de regras de negócios e 40; Master Data Services & 41;](../master-data-services/business-rule-examples-master-data-services.md).  
  
## Criar e publicar uma regra de negócio  
 Regras de negócio são **If/Then/Else** instruções criadas no [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]. Se um valor de atributo corresponder a uma condição especificada, uma ação será executada, caso contrário a ação Else é executada. As possíveis ações incluem a definição de um valor padrão ou a alteração de um valor. Estas ações podem ser combinadas com enviar uma notificação de email.  
  
 Regras de negócios podem ser baseadas em valores de atributo específicos (por exemplo, realizar ação se Cor=Azul), ou quando os valores de atributo são alterados (por exemplo, realizar ação se o valor do atributo de cor for alterado). Para obter mais informações sobre o controle de alterações não específicas, consulte [Change Tracking & #40. Master Data Services & 41;](../master-data-services/change-tracking-master-data-services.md).  
  
 Para usar regras de negócio, você deve primeiramente criar e publicar suas regras e depois aplicar as regras publicadas aos dados. As regras podem ser aplicadas a subconjuntos de dados ou a todos os dados de uma versão por meio da validação da versão. Uma versão não pode ser confirmada até que todos os atributos sejam submetidos com êxito à validação de regras de negócio.  
  
 Se um usuário tentar adicionar um valor de atributo que não é aprovado na validação das regras de negócio, esse valor ainda poderá ser salvo. Você pode revisar e corrigir problemas de validação, que são exibidos no [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
 Ao criar um pacote de implantação de modelo, se quiser incluir regras de negócio, você deverá incluir dados da versão no pacote.  
  
 Se você criar uma regra de negócio que usa o **ou** operador, você deve criar uma regra separada para cada instrução condicional que possa ser avaliada independentemente. É possível excluir regras conforme necessário, para garantir mais flexibilidade e uma solução de problemas mais fácil.  
  
## Como são aplicadas regras de negócio  
 Você pode definir a ordem de prioridade para executar as regras movendo as regras de negócio para cima e para baixo. No entanto, antes de a prioridade ser levada em conta, são aplicadas regras de negócio com base no tipo de ação que a regra adota. A ordem é a seguinte:  
  
1.  **Valor padrão**  
  
2.  **Alterar valor**  
  
3.  **Validação**  
  
4.  **Ação externa**  
  
5.  **Ação de Script Definido pelo Usuário**  
  
 Nesses grupos, as ações são aplicadas na ordem de prioridade, da mais baixa para a mais alta. Por exemplo, podem ter quatro regras separadas **valor padrão** ações. O **valor padrão** ação que ocorre primeiro depende da ordem de prioridade especificada na interface da web.  
  
 Outras observações importantes sobre como aplicar regras:  
  
-   Se uma regra de negócio for excluída ou não for publicada com um status de **ativos**, a regra ainda está disponível, mas não está incluída quando as regras de negócio são aplicadas.  
  
-   As regras de negócio se aplicam aos valores de atributos para todos os membros da folha ou todos os membros consolidados, não ambos.  
  
-   Regras de negócio podem ser aplicadas a qualquer versão de um modelo que é **Abrir** ou **bloqueado**.  
  
-   Alterações feitas a dados quando regras de negócio são aplicadas não são registradas em log como transações.  
  
-   Uma regra de negócio não pode conter mais de um **Iniciar fluxo de trabalho** ação.  
  
## Configurações do sistema  
 Há duas configurações no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] que afetam as regras de negócio. Você pode ajustar essas configurações no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] ou diretamente na tabela Configurações do Sistema. Para obter mais informações, consulte [configurações do sistema e 40; Master Data Services & 41;](../master-data-services/system-settings-master-data-services.md).  
  
## Tarefas relacionadas  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Criar e publicar uma nova regra de negócio.|[Criar e publicar uma regra de negócio e 40; Master Data Services & 41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)|  
|Adicionar várias condições a uma regra de negócio.|[Adicionar várias condições a uma regra de negócio e 40; Master Data Services & 41;](../master-data-services/add-multiple-conditions-to-a-business-rule-master-data-services.md)|  
|Criar uma regra de negócio para exigir que os atributos tenham valores.|[Exigir valores de atributo & #40. Master Data Services & 41;](../master-data-services/require-attribute-values-master-data-services.md)|  
|Criar uma regra de negócio para tomar uma ação com base nas alterações para atribuir valores.|[Iniciar ações com base em alterações de valor de atributo & #40. Master Data Services & 41;](../master-data-services/initiate-actions-based-on-attribute-value-changes-master-data-services.md)|  
|Criar uma regra de negócio para tirar o script definido pelo usuário como uma condição|[Extensão de regras comerciais e 40; Master Data Services & 41;](../master-data-services/business-rules-extension-master-data-services.md)|  
|Criar uma regra de negócio para tirar o script definido pelo usuário como uma ação|[Extensão de regras comerciais e 40; Master Data Services & 41;](../master-data-services/business-rules-extension-master-data-services.md)|  
|Alterar o nome de uma regra de negócio existente.|[Alterar o nome de uma regra de negócios & #40. Master Data Services & 41;](../master-data-services/change-a-business-rule-name-master-data-services.md)|  
|Configure o [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] para enviar notificações quando as regras de negócio forem aplicadas.|[Configurar regras de negócios para enviar notificações e 40; Master Data Services & 41;](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)|  
|Aplicar regras de negócio a membros específicos.|[Validar membros específicos em relação a regras de negócio e 40; Master Data Services & 41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)|  
|Excluir uma regra de negócio para que ela não seja usada.|[Excluir uma regra de negócio e 40; Master Data Services & 41;](../master-data-services/exclude-a-business-rule-master-data-services.md)|  
|Excluir uma regra de negócio existente.|[Excluir uma regra de negócio & #40. Master Data Services & 41;](../master-data-services/delete-a-business-rule-master-data-services.md)|  
  
## Conteúdo relacionado  
  
-   [Visão geral do Master Data Services & #40. MDS & 41;](../master-data-services/master-data-services-overview-mds.md)  
  
-   [Versões e 40; Master Data Services & 41;](../master-data-services/versions-master-data-services.md)  
  
-   [Validação de & #40. Master Data Services & 41;](../master-data-services/validation-master-data-services.md)  
  
-   [Controle de alterações e 40; Master Data Services & 41;](../master-data-services/change-tracking-master-data-services.md)  
  
  