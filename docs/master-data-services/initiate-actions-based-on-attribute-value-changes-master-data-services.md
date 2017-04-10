---
title: "Iniciar a&#231;&#245;es com base em altera&#231;&#245;es no valor do atributo (Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "regras de negócio [Master Data Services], controle de alterações de atributo"
  - "alterar grupos de controle [Master Data Services], Iniciando ações"
ms.assetid: 5e4402ce-31db-4774-a2a1-552335f87693
caps.latest.revision: 8
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 8
---
# Iniciar a&#231;&#245;es com base em altera&#231;&#245;es no valor do atributo (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], crie uma regra de negócio para iniciar ações com base em alterações para atribuir valores. Por exemplo, quando uma valor de atributo específico for alterado, você pode querer alterar um valor, enviar uma notificação ou iniciar um fluxo de trabalho externo.  
  
## Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do Sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Seus atributos devem estar em um grupo de controle de alterações. Consulte [Adicionar atributos a um grupo de controle de alterações &#40;Master Data Services&#41;](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md) para obter mais informações.  
  
### Criar uma regra de negócios para iniciar ações com base em alterações de valores  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na barra de menus, aponte para **Gerenciar** e clique em **Regras de Negócios**.  
  
3.  Na página **Manutenção de Regra de Negócio**, na lista **Modelo**, selecione um modelo.  
  
4.  Na lista **Entidade**, selecione uma entidade.  
  
5.  Na lista **Tipo de Membro**, selecione um tipo de membro ao qual a regra de negócio será aplicada.  
  
6.  Na lista **Atributo**, selecione um atributo ou deixe o valor padrão **Todos**.  
  
7.  Clique em **Adicionar regra de negócio**.  
  
8.  Clique em **Editar regra de negócio selecionada**.  
  
9. No painel **Componentes**, expanda o nó **Condições**.  
  
10. No nó **Comparação de valores**, arraste **foi alterado** para o rótulo **Condições** do painel **IF**.  
  
11. No painel **Editar Condição**, na caixa **Grupo de controle de alterações**, digite o número do grupo de controle de alterações que você atribuiu como parte dos pré-requisitos.  
  
12. No painel **Editar Condição**, clique em **Salvar item**.  
  
13. No painel **Componentes**, expanda o nó **Ações**.  
  
14. Clique em uma ação e arraste-a até o rótulo **Ação** do painel **THEN**.  
  
15. No painel **Atributos**, clique em um atributo e arraste-o até o rótulo **Selecionar atributo** do painel **Editar Ação**.  
  
16. No painel **Editar Ação**, preencha os campos necessários.  
  
17. No painel **Editar Ação**, clique em **Salvar item**.  
  
18. Clique em **Voltar**.  
  
19. Opcionalmente, na página **Manutenção de Regra de Negócio**, na linha que contém sua regra de negócio, clique duas vezes em uma célula da coluna **Nome**, **Descrição** ou **Notificação** para atualizar o valor.  
  
    > [!NOTE]  
    >  Notificações são enviadas somente para regras que incluem uma ação de validação.  
  
20. Clique em **Publicar regras de negócio**.  
  
21. Na caixa de diálogo de confirmação, clique em **OK**. O status da regra mudará para **Ativo**.  
  
## Próximas etapas  
  
-   Aplique regras de negócio a dados seguindo um destes procedimentos:  
  
    -   [Validar membros específicos em relação a regras de negócio &#40;Master Data Services&#41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [Validar uma versão em relação a regras de negócio &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## Consulte também  
 [Adicionar atributos a um grupo de controle de alterações &#40;Master Data Services&#41;](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)   
 [Regras de negócio &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
  