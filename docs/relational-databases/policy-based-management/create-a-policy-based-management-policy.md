---
title: "Criar uma política de gerenciamento baseado em políticas | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Policy-Based Management, creating policies
ms.assetid: b28bf963-89f9-4941-b6c1-6004fec347f1
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 28d614d27647f0466abd5a6715244b6334ec56be
ms.lasthandoff: 04/11/2017

---
# <a name="create-a-policy-based-management-policy"></a>Criar uma política do Gerenciamento Baseado em Políticas
  Este tópico descreve como criar uma Política de Gerenciamento Baseado em Políticas no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para criar uma política, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a associação à função PolicyAdministratorRole no banco de dados msdb.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-create-a-policy"></a>Para criar uma política  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor no qual você deseja criar uma nova política de Gerenciamento Baseado em Políticas.  
  
2.  Clique no sinal de adição para expandir a pasta **Gerenciamento** .  
  
3.  Clique no sinal de adição para expandir a pasta **Gerenciamento de Política**.  
  
4.  Clique com o botão direito do mouse na pasta **Políticas** e selecione **Nova Política**.  
  
5.  Na caixa de diálogo **Criar Nova Política** , na caixa **Nome** , digite o nome da nova política.  
  
6.  Se você quiser habilitar a política assim que seja criado, marque a caixa de seleção **Habilitado** . Se o modo de avaliação for **Sob Demanda**, a caixa de seleção **Habilitado** não estará disponível.  
  
7.  Na lista **Verificar condição** , selecione um das condições existentes ou selecione **Nova Condição**. Para editar uma condição, selecione a condição e clique nas reticências (**...**). Para obter mais informações, veja [Criar uma nova condição de Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/create-a-new-policy-based-management-condition.md) ou [Exibir ou modificar as propriedades de uma condição de Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/view-or-modify-the-properties-of-a-policy-based-management-condition.md).  
  
8.  Na caixa **Em relação aos destinos** , selecione um ou mais tipos de destino para essa política. Só podem ser se aplicadas algumas condições e facetas a certos tipos de destinos. Os conjuntos de destino disponíveis aparecem na caixa associada. Expanda **Todo** para selecionar uma condição de filtragem para alguns tipos de destinos. Se nenhum destino for exibido nesta caixa, o escopo da condição de verificação será no nível de servidor.  
  
9. Na caixa **Modo de Avaliação** , selecione como essa política se comportará. Condições diferentes podem ter modos de avaliação válidos diferentes. Para obter mais informações sobre quais modos de avaliação são válidos, veja [Administrar servidores usando o Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md).  
  
10. Se a política for avaliada em um agendamento, clique em **Ao Agendar**e em **Escolher** para selecionar um agendamento ou clique em **Novo** para criar um novo agendamento.  
  
11. Para limitar a política a um subconjunto dos tipos de destino, na caixa **Restrição de servidor** , selecione a partir das condições de limitação ou crie uma nova condição.  
  
     Para obter mais informações sobre as opções disponíveis contidas na caixa de diálogo **Criar Nova Política** , consulte [Create New Policy or Open Policy Dialog Box, General Page](../../relational-databases/policy-based-management/create-new-policy-or-open-policy-dialog-box-general-page.md) ou [Create New Policy or Open Policy Dialog Box, Description Page](../../relational-databases/policy-based-management/create-new-policy-or-open-policy-dialog-box-description-page.md).  
  
12. Quando terminar, clique em **OK**.  
  
  
