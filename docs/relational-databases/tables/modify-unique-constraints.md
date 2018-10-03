---
title: Modificar restrições exclusivas | Microsoft Docs
ms.custom: ''
ms.date: 10/12/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- modifying constraints
- UNIQUE constraints [SQL Server], modifying
- constraints [SQL Server], modifying
- constraints [SQL Server], unique
ms.assetid: fddbdc9e-958b-4614-8e88-6ca205d64a4e
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 241596df017e06519c2a2cc1993a7fb025addc97
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47734614"
---
# <a name="modify-unique-constraints"></a>Modificar restrições exclusivas
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Você pode modificar uma restrição exclusiva no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para modificar uma restrição exclusiva usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige a permissão ALTER na tabela.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-modify-a-unique-constraint"></a>Para modificar uma restrição exclusiva  
  
1.  No **Pesquisador de Objetos**, clique com o botão direito do mouse na tabela que contém restrição exclusiva e selecione **Design**.  
  
2.  No menu **Designer de Tabela** , clique em **Índices/Chaves…**.  
  
3.  Na caixa de diálogo **Índices/Chaves** , selecione **Índice ou Chave Exclusiva/Primária Selecionada**e selecione a restrição que deseja editar.  
  
4.  Complete uma ação da seguinte tabela:  
  
    |Para|Siga estas etapas|  
    |--------|------------------------|  
    |Alterar as colunas às quais a restrição está associada|1) Na grade, em **(Geral)**, clique em **Colunas** e nas reticências **(…)** à direita da propriedade.<br /><br /> 2) Na caixa de diálogo **Colunas de Índice** , especifique a nova coluna, a ordem de classificação ou ambas para o índice.|  
    |Renomear a restrição|Na grade, em **Identidade**, digite um novo nome na caixa **Nome** . Verifique se seu novo nome não duplica um nome na lista **Índice ou Chave Exclusiva/Primária Selecionada** .|  
    |Definir a opção clustered|Na grade, em selecione **Designer de Tabela**, selecione **Criar como Clusterizado** e, na lista suspensa, escolha Sim para criar um índice clusterizado e Não para criar um não clusterizado. Só pode existir um índice clusterizado por tabela. Se já houver um índice clusterizado nessa tabela, você deverá desmarcar essa configuração no índice original.|  
    |Definir um fator de preenchimento|Na grade, em **Designer de Tabela**, expanda a categoria **Especificação de Preenchimento** e digite um inteiro de 0 a 100 na caixa **Fator de Preenchimento** .|  
  
5.  No menu **Arquivo** , clique em **Salvar**_table name_.  
  
##  <a name="TsqlProcedure"></a> **Para modificar uma restrição exclusiva**  
  
 Para modificar a restrição UNIQUE usando o Transact-SQL, exclua primeiramente a restrição UNIQUE existente e, em seguida, recrie-a com a nova definição. Para obter mais informações, consulte [Delete Unique Constraints](../../relational-databases/tables/delete-unique-constraints.md) e [Create Unique Constraints](../../relational-databases/tables/create-unique-constraints.md).  
  
###  <a name="TsqlExample"></a>  
