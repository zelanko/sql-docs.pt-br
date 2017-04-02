---
title: "Modificar restri&#231;&#245;es de verifica&#231;&#227;o | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-tables"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "restrições CHECK, modificando"
  - "modificando restrições"
  - "restrições [SQL Server], verificar"
  - "restrições [SQL Server], modificando"
ms.assetid: f22daef8-e350-40ef-8ff0-b5f87d1d9e56
caps.latest.revision: 18
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 18
---
# Modificar restri&#231;&#245;es de verifica&#231;&#227;o
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Você pode modificar uma restrição de verificação no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)] quando você quiser alterar a expressão de restrição ou as opções que habilitam ou desabilitam a restrição de condições específicas.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para modificar uma restrição de verificação usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige a permissão ALTER na tabela.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### Para modificar uma restrição de verificação  
  
1.  No **Pesquisador de Objetos**, clique com o botão direito do mouse na tabela que contém restrição de verificação e selecione **Design**.  
  
2.  No menu **Designer de Tabela** , clique em **Verificar Restrições...**.  
  
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
  
5.  Clique em **Fechar**.  
  
6.  No menu **Arquivo** , clique em **Salvar***table name*.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 **Para modificar uma restrição de verificação**  
  
 Para modificar a restrição `CHECK` usando o [!INCLUDE[tsql](../../includes/tsql-md.md)], exclua primeiramente a restrição `CHECK` e, em seguida, recrie-a com a nova definição. Para obter mais informações, veja [Excluir restrições de verificação](../../relational-databases/tables/delete-check-constraints.md) e [Criar restrições de verificação](../../relational-databases/tables/create-check-constraints.md).  
  
###  <a name="TsqlExample"></a>  