---
title: "Configure a Op&#231;&#227;o de Configura&#231;&#227;o do Servidor de arquivo de dados remotos | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b5817b5a-f39a-4faf-b11e-a47b54fd9f32
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Configure a Op&#231;&#227;o de Configura&#231;&#227;o do Servidor de arquivo de dados remotos
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Use a opção **remote data archive** para especificar se os bancos de dados e as tabelas no servidor podem ser habilitados para Stretch. Para obter mais informações, consulte [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md).  
  
 A opção **remote data archive** pode ter os valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|0|Bancos de dados e tabelas no servidor não podem ser habilitados para Ampliação.|  
|1|Bancos de dados e tabelas no servidor podem ser habilitados para Ampliação.|  
  
 Executar **sp_configure** para definir o valor da opção **remote data archive** exige permissões sysadmin ou serveradmin.  
  
## Exemplo  
 O exemplo a seguir exibe primeiro a definição atual da opção **remote data archive**. O exemplo a seguir habilita a opção **remote data archive** definindo seu valor para 1.  
  
```  
EXEC sp_configure 'remote data archive';  
GO  
EXEC sp_configure 'remote data archive' , '1';  
GO  
RECONFIGURE;  
GO  
```  
  
 Para desabilitar a opção, defina o valor para 0.  
  
## Consulte também  
 [Habilitar o Stretch Database para um banco de dados](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  