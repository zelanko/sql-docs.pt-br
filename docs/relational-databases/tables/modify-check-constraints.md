---
description: Modificar restrições de verificação
title: Modificar restrições de verificação | Microsoft Docs
ms.custom: ''
ms.date: 06/28/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- CHECK constraints, modifying
- modifying constraints
- constraints [SQL Server], check
- constraints [SQL Server], modifying
ms.assetid: f22daef8-e350-40ef-8ff0-b5f87d1d9e56
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: af223b73ec73a4cd52bcf86e389284ad6b383ec4
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97403813"
---
# <a name="modify-check-constraints"></a>Modificar restrições de verificação
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Você pode modificar uma restrição de verificação no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)] quando você quiser alterar a expressão de restrição ou as opções que habilitam ou desabilitam a restrição de condições específicas.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para modificar uma restrição de verificação usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Exige a permissão ALTER na tabela.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-modify-a-check-constraint"></a>Para modificar uma restrição de verificação  
  
1.  No **Pesquisador de Objetos**, clique com o botão direito do mouse na tabela que contém restrição de verificação e selecione **Design**.  
  
2.  No menu **Designer de Tabela**, clique em **Verificar Restrições...** .  
  
3.  Na caixa de diálogo **Verificar Restrições** , em **Restrição de Verificação Selecionada**, selecione a restrição que deseja editar.  
  
4.  Complete uma ação da seguinte tabela:  
  
    |Para|Siga estas etapas|  
    |--------|------------------------|  
    |Editar a expressão de restrição|Digite uma nova expressão no campo **Expressão** .|  
    |Renomear a restrição|Digite um nome novo no campo **Nome** .|  
    |Aplicar a restrição a dados existentes|Selecione a opção **Verificar Dados Existentes ao Criar ou Habilitar** .|  
    |Desabilitar a restrição quando são adicionados dados novos à tabela ou quando dados existentes são atualizados na tabela.|Desmarque a opção **Aplicar restrições para INSERTs e UPDATEs** .|  
    |Desabilitar a restrição quando um agente de replicação inserir ou atualizar dados em sua tabela.|Desmarque a opção **Impor para Replicação** .|  
  
    > [!NOTE]  
    >  Alguns bancos de dados têm funcionalidade diferente para restrições de verificação.  
  
5.  Clique em **fechar**  
  
6.  No menu **Arquivo**, clique em **Salvar**_nome da tabela_.  

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para modificar uma restrição de verificação**  
  
 Para modificar a restrição `CHECK` usando o [!INCLUDE[tsql](../../includes/tsql-md.md)], exclua primeiramente a restrição `CHECK` e, em seguida, recrie-a com a nova definição. Para obter mais informações, veja [Excluir restrições de verificação](../../relational-databases/tables/delete-check-constraints.md) e [Criar restrições de verificação](../../relational-databases/tables/create-check-constraints.md).  
  
###  <a name="TsqlExample"></a>  
