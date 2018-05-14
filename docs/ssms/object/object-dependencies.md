---
title: Dependências de objeto | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-objects
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.common.objectdependencies.f1
ms.assetid: c63d1160-3f3d-45df-99be-6fe081125fb5
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a7fae20ced8820f16353c8e8cc4633dda078b3a0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="object-dependencies"></a>Dependências de objeto
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Alguns objetos de banco de dados têm dependências de outros objetos de banco de dados. Por exemplo, exibições e procedimentos armazenados dependem da existência de tabelas que contenham dados retornados pela exibição ou pelo procedimento. As **Dependências entre objetos (página Geral)** para o objeto atual lista ambos os objetos de banco de dados que devem estar presentes para o objeto funcionar corretamente e os objetos que dependem do objeto selecionado. Um objeto que faz referência a outro objeto em sua definição, e essa definição é armazenada no catálogo do sistema, é denominado *entidade de referência*. Um objeto que é referenciado por outro objeto é denominado *entidade referenciada*.  
  
As **Dependências entre objetos (página Avançado)** do objeto atual lista os objetos de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e os objetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)] que dependem do objeto. Os objetos podem ser armazenados em servidores diferentes.  
  
Use esta caixa de diálogo para entender as dependências antes de alterar ou excluir o objeto selecionado.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
**Objetos que dependem de** *<selected object>*  
Clicando neste botão, você exibe uma lista dos objetos que são rastreados por dependência e que dependem do objeto selecionado.  
  
**Objetos dos quais** *<selected object>* **depende**  
Clicando neste botão, você exibe uma lista dos objetos que são rastreados por dependência e dos quais depende o objeto selecionado.  
  
**Dependências**  
Se você clicar em **Objetos que dependem de** *<selected object>* , será exibida uma exibição hierárquica dos objetos que dependem do objeto selecionado. Se você clicar em **Objetos dos quais** *<selected object>* **depende**, será exibida uma exibição hierárquica dos objetos dos quais depende o objeto selecionado.  
  
**Nome**  
Exibe o nome do objeto selecionado no modo de exibição de árvore **Dependências** acima.  
  
**Tipo**  
Exibe o tipo do objeto selecionado no modo de exibição de árvore **Dependências** acima.  
  
**Horário da Última Sincronização**  
> [!NOTE]  
> Esta opção só está disponível na página **Avançado** .  
  
Especifica a data e a hora em que as informações de dependência foram atualizadas pela última vez.  
  
**Tipo de dependência**  
> [!NOTE]  
> Esta opção só está disponível na página **Geral** .  
  
Exibe o tipo de dependência entre dois objetos. Pode ser uma destas opções:  
  
-   Dependência associada a esquema  
  
    É uma relação entre dois objetos que impedem o objeto mencionado de ser descartado ou modificado desde que exista o objeto referenciado. Uma dependência associada a esquema é criada quando uma exibição ou função definida pelo usuário é criada usando a cláusula WITH SCHEMABINDING, ou quando uma tabela faz referência a outro objeto por uma restrição CHECK ou DEFAULT ou na definição de uma coluna computada.  
  
-   Dependência não associada a esquema  
  
    É uma relação entre dois objetos que não impedem o descarte ou a modificação do objeto referenciado.  
  
-   Entidade não disponível ou não resolvida  
  
    Indica que o tipo de dependência não pode ser determinado. Isso só acontece quando o objeto selecionado estiver em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] que é anterior a [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)].  
  
