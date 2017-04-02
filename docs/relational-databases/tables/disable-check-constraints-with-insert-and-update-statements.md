---
title: "Desabilitar restri&#231;&#245;es de verifica&#231;&#227;o com instru&#231;&#245;es INSERT e UPDATE | Microsoft Docs"
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
  - "Restrições CHECK, desabilitando"
  - "restrições [SQL Server], desabilitando"
  - "desabilitando restrições"
  - "restrições [SQL Server], verificar"
ms.assetid: c7287ad1-50d2-4e80-bc0c-b5570f7e5f69
caps.latest.revision: 17
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 17
---
# Desabilitar restri&#231;&#245;es de verifica&#231;&#227;o com instru&#231;&#245;es INSERT e UPDATE
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Você pode desabilitar uma restrição de verificação para transações INSERT e UPDATE no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Depois de desabilitar as restrições de verificação, as inserções ou atualizações futuras na coluna não serão validadas em relação às condições de restrição. Use esta opção se você souber que novos dados violarão a restrição existente ou se a restrição se aplicar somente aos dados que já estão no banco de dados.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para desabilitar uma restrição de verificação para instruções INSERT e UPDATE usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige a permissão ALTER na tabela.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### Para desabilitar uma restrição de verificação para instruções INSERT e UPDATE  
  
1.  No **Pesquisador de Objetos**, expanda a tabela com a restrição e expanda a pasta **Restrições** .  
  
2.  Clique com o botão direito do mouse na restrição e selecione **Modificar**.  
  
3.  Na grade, em **Designer de Tabela**, clique em **Impor para INSERTs e UPDATEs** e selecione **Não** no menu suspenso.  
  
4.  Clique em **Fechar**.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### Para desabilitar uma restrição de verificação para instruções INSERT e UPDATE  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole os exemplos a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    ALTER TABLE Purchasing.PurchaseOrderHeader  
    NOCHECK CONSTRAINT CK_PurchaseOrderHeader_Freight;   
    GO  
    ```  
  
 Para obter mais informações, veja [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).  
  
###  <a name="TsqlExample"></a>  