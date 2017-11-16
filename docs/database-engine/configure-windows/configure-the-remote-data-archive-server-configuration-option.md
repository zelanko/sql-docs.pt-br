---
title: "Configurar a opção de configuração de servidor remote data archive | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b5817b5a-f39a-4faf-b11e-a47b54fd9f32
caps.latest.revision: "8"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3f86893797913daca2eb43826ce7597b7eee298d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="configure-the-remote-data-archive-server-configuration-option"></a>Configure a Opção de Configuração do Servidor de arquivo de dados remotos
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Use a opção **remote data archive** para especificar se os bancos de dados e as tabelas no servidor podem ser habilitados para Stretch. Para obter mais informações, consulte [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md).  
  
 A opção **remote data archive** pode ter os valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|0|Bancos de dados e tabelas no servidor não podem ser habilitados para Ampliação.|  
|1|Bancos de dados e tabelas no servidor podem ser habilitados para Ampliação.|  
  
 Executar **sp_configure** para definir o valor da opção **remote data archive** exige permissões sysadmin ou serveradmin.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir exibe primeiro a definição atual da opção **remote data archive** . O exemplo a seguir habilita a opção **remote data archive** definindo seu valor para 1.  
  
```  
EXEC sp_configure 'remote data archive';  
GO  
EXEC sp_configure 'remote data archive' , '1';  
GO  
RECONFIGURE;  
GO  
```  
  
 Para desabilitar a opção, defina o valor para 0.  
  
## <a name="see-also"></a>Consulte também  
 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
