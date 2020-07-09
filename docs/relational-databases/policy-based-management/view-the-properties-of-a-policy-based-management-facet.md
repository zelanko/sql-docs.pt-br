---
title: Exibir as propriedades de uma faceta do gerenciamento baseado em políticas
description: Saiba como exibir as propriedades de uma faceta do gerenciamento baseado em políticas no SQL Server usando o SSMS (SQL Server Management Studio).
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, view facet properties
ms.assetid: 022a244c-c2e7-4467-b9a2-c7a27859be22
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: d2aa58294e23f32ebfc1a43d300ab54cd6622aa4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85774073"
---
# <a name="view-the-properties-of-a-policy-based-management-facet"></a>Exibir as propriedades de uma faceta de gerenciamento baseado em políticas
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Este tópico descreve como exibir as propriedades de uma faceta do Gerenciamento Baseado em Políticas no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para exibir as propriedades de uma faceta, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a associação à função PolicyAdministratorRole no banco de dados msdb.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-view-the-properties-of-a-facet"></a>Para visualizar as propriedades de uma faceta  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor que contém a faceta cujas propriedades você deseja exibir.  
  
2.  Clique no sinal de adição para expandir a pasta **Gerenciamento** .  
  
3.  Clique no sinal de adição para expandir a pasta **Gerenciamento de Política**.  
  
4.  Clique no sinal de adição para expandir a pasta **Facetas** .  
  
5.  Clique com o botão direito do mouse na faceta cujas propriedades você deseja exibir e selecione **Propriedades**. Para obter mais informações sobre as opções disponíveis na caixa de diálogo **Propriedades da faceta -** _nome_da_faceta_, confira [Caixa de diálogo Propriedades de Faceta, página Geral](../../relational-databases/policy-based-management/facet-properties-dialog-box-general-page.md), [Caixa de diálogo Propriedades da Faceta, página Políticas Dependentes](../../relational-databases/policy-based-management/facet-properties-dialog-box-dependent-policies-page.md) e [Caixa de diálogo Propriedades da Faceta, página Condições Dependentes](../../relational-databases/policy-based-management/facet-properties-dialog-box-dependent-conditions-page.md).  
  
6.  Quando terminar, clique em **Fechar**.  

