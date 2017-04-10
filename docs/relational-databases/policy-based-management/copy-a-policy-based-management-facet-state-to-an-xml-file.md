---
title: "Copiar um estado de faceta do Gerenciamento Baseado em Pol&#237;ticas para um arquivo XML | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Gerenciamento baseado em políticas, estado de faceta de cópia de arquivo XML"
ms.assetid: 7d604ab1-6dd6-4f8e-a79c-eba99ab106fd
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# Copiar um estado de faceta do Gerenciamento Baseado em Pol&#237;ticas para um arquivo XML
  Este tópico descreve como copiar o estado de uma faceta de Gerenciamento Baseado em Política para um arquivo XML no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para copiar um estado de faceta para um arquivo XML, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Os procedimentos deste tópico exigem a associação à função PolicyAdministratorRole no banco de dados msdb.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### Para copiar um estado de faceta para um arquivo XML  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um objeto de instância, banco de dados ou objeto de banco de dados e clique em **Facetas**.  
  
2.  Na caixa de diálogo **Exibir Facetas –***object_name*, clique em **Exportar Estado Atual como Política**.  
  
3.  Na caixa de diálogo **Exportar como Política**, digite o caminho e o nome do arquivo ou use o botão Procurar (**...**) para localizar o arquivo e digite o nome do arquivo XML. Para obter mais informações sobre as opções disponíveis nesta caixa de diálogo, consulte [Export As Policy Dialog Box](../../relational-databases/policy-based-management/export-as-policy-dialog-box.md).  
  
4.  Quando terminar, clique em **OK**.  
  
  