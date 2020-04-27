---
title: Exibir informações de etapa de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- displaying job step information
- jobs [SQL Server Agent], viewing
- SQL Server Agent jobs, viewing
- viewing job step information
ms.assetid: e3f06492-dc86-4e06-b186-ea58aff6d591
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8123a523a0fa5212b4c0ffc8d98c6a90aef3396c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63245928"
---
# <a name="view-job-step-information"></a>View Job Step Information
  Este tópico descreve como exibir detalhes de etapa de trabalho na caixa de diálogo Propriedades da Etapa de Trabalho. Ela também inclui informações sobre a exibição da saída da etapa de trabalho.  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para exibir informações de etapas de trabalho usando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
 Se a etapa de trabalho tiver sido configurada de modo a gravar sua saída em uma tabela ou arquivo e o trabalho tiver sido executado pelo menos uma vez, a saída poderá ser vista na página **Avançado** da caixa de diálogo **Propriedades da Etapa de Trabalho** . Quando um trabalho ou etapa de trabalho é excluído, o log de saída é excluído automaticamente.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Você só pode exibir trabalhos de sua propriedade, a não ser que você seja membro da função de servidor fixa **sysadmin** . Membros dessa função podem exibir todos os trabalhos e detalhes de etapa de trabalho.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-view-job-step-information"></a>Para exibir informações de etapas de trabalho  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e a expanda.  
  
2.  Expanda **SQL Server Agent**, expanda **Trabalhos**, clique com o botão direito do mouse no trabalho que contém a etapa que deseja exibir e clique em **Propriedades**.  
  
3.  Na caixa de diálogo **Propriedades do Trabalho** , clique na página **Etapas** .  
  
4.  Clique na etapa de trabalho a ser exibida e clique em **Editar**.  
  
5.  Na página **Geral** da caixa de diálogo **Propriedades da Etapa de Trabalho** , é possível visualizar o tipo de etapa de trabalho e o que ela faz.  
  
6.  Clique na página **Avançado** para visualizar as ações que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent toma em caso de êxito ou falha da etapa, quantas vezes a etapa deve ser tentada, onde deve ser gravada sua saída e o usuário com o qual ela é executada.  
  
#### <a name="to-view-job-step-output"></a>Para exibir a saída da etapa de trabalho  
  
1.  Na caixa de diálogo **Propriedades da Etapa de Trabalho** , clique na página **Avançado** .  
  
2.  Dependendo da versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a que está conectado, você poderá visualizar o arquivo ou a tabela de saída da etapa de trabalho, da seguinte maneira:  
  
    -   Se estiver conectado ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou versão posterior, você só poderá clicar em **Exibir** se a opção **Registrar em tabela** estiver selecionada. Nesse caso, a saída da etapa de trabalho será gravada na tabela **sysjobstepslogs** do banco de dados **msdb** .  
  
    -   O botão **Exibir** encontra-se desabilitado quando a saída da etapa de trabalho é gravada em um arquivo. Para visualizar o arquivo de saída da etapa de trabalho, use o Bloco de Notas.  
  
  
