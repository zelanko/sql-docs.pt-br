---
title: "Definir ou alterar o agrupamento do servidor | Microsoft Docs"
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
  - "agrupamentos de servidor [SQL Server]"
  - "agrupamentos [SQL Server], servidor"
ms.assetid: 3242deef-6f5f-4051-a121-36b3b4da851d
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# Definir ou alterar o agrupamento do servidor
  O agrupamento do servidor atua como o agrupamento padrão de todos os bancos de dados do sistema instalados com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], e também com quaisquer bancos de dados de usuário recém-criados. O agrupamento do servidor é especificado durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md).  
  
## Alterando o agrupamento do servidor  
 A alteração do agrupamento padrão para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser uma operação complexa e engloba as seguintes etapas:  
  
-   Verifique se você tem todas as informações ou scripts necessários para recriar seus bancos de dados de usuário e todos os objetos neles.  
  
-   Exporte todos os seus dados usando uma ferramenta como [bcp Utility](../../tools/bcp-utility.md). Para obter mais informações, consulte [Importação e exportação em massa de dados &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md).  
  
-   Descarte todos os bancos de dados de usuário.  
  
-   Reconstrua o banco de dados mestre especificando o novo agrupamento na propriedade SQLCOLLATION do comando **setup**. Por exemplo:  
  
    ```  
    Setup /QUIET /ACTION=REBUILDDATABASE /INSTANCENAME=InstanceName   
    /SQLSYSADMINACCOUNTS=accounts /[ SAPWD= StrongPassword ]   
    /SQLCOLLATION=CollationName  
    ```  
  
     Para obter mais informações, consulte [Recriar bancos de dados do sistema](../../relational-databases/databases/rebuild-system-databases.md).  
  
-   Crie todos os bancos de dados e todos os objetos neles.  
  
-   Importe todos os dados.  
  
> [!NOTE]  
>  Em vez de alterar o agrupamento padrão de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode especificar um agrupamento para cada novo banco de dados que criar.  
  
## Consulte também  
 [Suporte a agrupamentos e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md)   
 [Definir ou alterar o agrupamento de banco de dados](../../relational-databases/collations/set-or-change-the-database-collation.md)   
 [Definir ou alterar o agrupamento de coluna](../../relational-databases/collations/set-or-change-the-column-collation.md)   
 [Recriar bancos de dados do sistema](../../relational-databases/databases/rebuild-system-databases.md)  
  
  