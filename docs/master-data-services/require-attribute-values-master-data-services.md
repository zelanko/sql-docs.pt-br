---
title: "Exigir valores de atributos (Master Data Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "regras de negócio [Master Data Services], exigindo valores de atributo"
  - "atributos [Master Data Services], exigindo valores"
ms.assetid: a360ef13-0c34-43b8-a87e-2f5d8732d30e
caps.latest.revision: 9
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 9
---
# Exigir valores de atributos (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], solicite valores de atributos quando desejar se certificar de que os dados mestres estejam completos.  
  
> [!NOTE]  
>  Os membros que não possuírem valores de atributos baseados em domínio não serão exibidos em hierarquias derivadas baseadas nessas relações.  
  
## Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do Sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, consulte [Administradores e 40; Master Data Services & 41;](../master-data-services/administrators-master-data-services.md).  
  
### Para solicitar valores de atributos  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na barra de menus, aponte para **Gerenciar** e clique em **Regras de Negócios**.  
  
3.  No **regras de negócio** página, do **modelo** lista suspensa, selecione um modelo.  
  
4.  Do **entidade** lista suspensa, selecione uma entidade.  
  
5.  Da **tipos de membro** lista suspensa, selecione um tipo de membro para a regra de negócio para aplicar.  
  
6.  Clique em **Adicionar**.  
  
7.  Na caixa **Nome** , digite um nome para a regra de negócio.  
  
8.  Opcionalmente, no campo **Descrição** , digite a descrição da regra de negócio.  
  
9. Sob o **em seguida,** Bloquear, clique em **Add**. Um painel será exibido.  
  
10. Do **operador** lista suspensa, selecione **necessário ação**.  
  
11. Do **atributo** lista suspensa, selecione um atributo.  
  
12. Clique em **Salvar**. Uma nova linha será adicionada à grade **Então** .  
  
13. Clique em **Salvar**.  
  
14. Clique em **Publicar Tudo**.  
  
15. Na caixa de diálogo de confirmação, clique em **OK**. O valor da coluna **Estado da Regra de Negócio** é **Ativa**.  
  
## Próximas etapas  
  
-   Aplique regras de negócio a dados seguindo um destes procedimentos:  
  
    -   [Validar membros específicos em relação a regras de negócio e 40; Master Data Services & 41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [Validar uma versão em relação a regras de negócio e 40; Master Data Services & 41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## Consulte também  
 [Regras de negócio e 40; Master Data Services & 41;](../master-data-services/business-rules-master-data-services.md)   
 [Hierarquias derivadas & #40. Master Data Services & 41;](../master-data-services/derived-hierarchies-master-data-services.md)  
  
  