---
title: Exibir ou alterar os locais padrão de arquivos de dados e de log (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- log files [SQL Server], changing default location
- data files [SQL Server], changing default location
ms.assetid: 70a57fda-fcfe-490f-9cf6-5df620e32b2a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 06d17a4feaec0db614f61fb7761b37ea415efc24
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62808704"
---
# <a name="view-or-change-the-default-locations-for-data-and-log-files-sql-server-management-studio"></a>Exibir ou alterar os locais padrão de arquivos de log e de dados (SQL Server Management Studio)
  Este tópico descreve como exibir e alterar os locais padrão de novos arquivos de log e de dados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. O caminho padrão é obtido do Registro. Depois que você alterar o local, todos os novos bancos de dados criados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usarão esse local se um local diferente não for especificado.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Recomendações](#Recommendations)  
  
-   **Para exibir ou alterar os locais padrão dos dados e do arquivos de log usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
-   **Acompanhamento:**  [alterando os locais padrão](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Recommendations"></a> Recomendações  
 A prática recomendada para proteger seus arquivos de dados e arquivos de log é garantir que eles sejam protegidos por ACLs (listas de controle de acesso). As ACLs devem ser definidas no diretório raiz em que os arquivos são criados.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-view-or-change-the-default-locations-for-database-files"></a>Para exibir ou alterar os locais padrão dos arquivos de banco de dados  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em um servidor e clique em **Propriedades**.  
  
2.  No painel esquerdo, clique na página **Configurações do Banco de Dados** .  
  
3.  Em **Locais padrão de banco de dados**, exiba os locais atuais padrão dos novos arquivos de dados e novos arquivos de log. Para alterar um local padrão, digite um novo nome de caminho padrão no campo **Dados** ou **Log** ou clique no botão Procurar para localizar e selecionar um nome de caminho.  
  
##  <a name="FollowUp"></a>Acompanhamento: depois de alterar os locais padrão  
 Você deve parar e iniciar o serviço do SQL Server para concluir a alteração.  
  
## <a name="see-also"></a>Consulte Também  
 [CRIAR &#40;de banco de dados SQL Server&#41;Transact-SQL](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [Criar um banco de dados](../../relational-databases/databases/create-a-database.md)  
  
  
