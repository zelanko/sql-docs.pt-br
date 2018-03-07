---
title: "Extensão das regras de negócio (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4c18be5f-a3fa-45a8-9be6-0f45f58bbc9e
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7a6de9fcabc39738fc2be3a76389ef16398f8c1f
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2018
---
# <a name="business-rules-extension-master-data-services"></a>Extensão das Regras de Negócio (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], você pode aplicar scripts SQL definidos pelo usuário como uma extensão das ações e condições pré-definidas.  
  
> [!NOTE]  
>  Todos os scripts devem ser definidos sob o esquema [usr].  
  
 As funções SQL que atendem os critérios a seguir podem ser usadas como uma condição de Regra de Negócio.  
  
-   O tipo de valor retornado deve ser BIT.  
  
-   Somente os tipos a seguir têm suporte para tipos de parâmetros.  
  
    -   NVARCHAR  
  
    -   DATETIME2  
  
    -   DECIMAL (precisão, escala)  
  
         a precisão deve ser 38  
  
         a escala deve ser um valor de 0 a 7  
  
 Procedimentos armazenados SQL que usam que a sintaxe a seguir podem ser usados como uma ação de Regra de Negócio  
  
```  
CREATE PROCEDURE [usr].[YourAction]  
       (         
            @MemberIdList mdm.[MemberId] READONLY,  
            @ModelName NVARCHAR(MAX),  
            @VersionName NVARCHAR(MAX),  
            @EntityName NVARCHAR(MAX),  
            @BusinessRuleName NVARCHAR(MAX)  
        )    
      AS BEGIN    
       ...     
       END  
  
```  
  
 Scripts definidos pelo usuário não serão adicionados aos pacotes de implantação. Verifique se que o destino do banco de dados do Master Data Services contém todos os scripts usados nas regras de negócio antes de implantar um pacote.  
  
 Ações de script serão executadas conforme mds_br_user, que tem as permissões a seguir  
  
|||  
|-|-|  
|**Esquema**|**Permissões**|  
|mdm|SELECT|  
|stg|SELECT, UPDATE, DELETE, EXECUTE, INSERT|  
|usr|FULL|  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional Administração do Sistema.  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, consulte [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Scripts definidos pelo usuário foram adicionados ao banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
## <a name="create-a-business-rule-to-take-a-user-defined-script-as-a-condition-or-as-an-action"></a>Criar uma regra de negócio para tirar o script definido pelo usuário ou como uma ação  
  
1.  No Master Data Manager, clique em **Administração do Sistema**.  
  
2.  Na barra de menus, aponte para **Gerenciar** e clique em **Regras de Negócio**.  
  
3.  Na página **Regras de Negócio** , selecione um modelo na lista suspensa **Modelo** .  
  
4.  Na lista suspensa **Entidade** , escolha uma entidade.  
  
5.  Na lista suspensa **Tipo de Membro** , selecione um tipo de membro para aplicar a regra de negócio.  
  
6.  Clique em **Adicionar**.  
  
7.  Faça o seguinte para criar um script definido pelo usuário como uma condição.  
  
    1.  Sob o bloco **If** , clique no botão **Adicionar** . Um painel será exibido.  
  
    2.  Na lista suspensa **Operador** , selecione a função definida pelo usuário em **Script definido pelo usuário** .  
  
    3.  Todos os parâmetros da função definida pelo usuário são exibidos.  
  
    4.  Atribuir um valor a cada parâmetro  
  
    5.  Clique em **Salvar**.  
  
8.  Faça o seguinte para utilizar um script definido pelo usuário como uma ação.  
  
    1.  Sob o bloco **Then** , clique no botão **Adicionar** . Um painel será exibido.  
  
    2.  Na lista suspensa **Operador** , selecione a função definida pelo usuário em **Script definido pelo usuário** .  
  
    3.  Clique em **Salvar**.  
  
## <a name="see-also"></a>Consulte Também  
 [Regras de negócio &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)   
 [Condições de regras de negócio &#40;Master Data Services&#41;](../master-data-services/business-rule-conditions-master-data-services.md)   
 [Ações de regras de negócio &#40;Master Data Services&#41;](../master-data-services/business-rule-actions-master-data-services.md)  
  
  
