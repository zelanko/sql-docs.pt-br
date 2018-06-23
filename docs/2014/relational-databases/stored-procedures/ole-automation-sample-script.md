---
title: Script de exemplo de automação | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-ole
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- OLE Automation [SQL Server], examples
ms.assetid: e59f75a9-ed41-4f12-888e-ffc57f9b3882
caps.latest.revision: 15
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 147df3898c87abb02b2fedcb14caad3db07fc55b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36005850"
---
# <a name="ole-automation-sample-script"></a>Script de exemplo de automação OLE
  Esse tópico contém um exemplo de lote de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] que usa os procedimentos armazenados da Automação OLE para criar e usar um objeto SQL-DMO SQLServer na instância local do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Partes do código são usadas como exemplos nos tópicos de referência para os procedimentos armazenados do sistema de Automação OLE.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @Object int;  
DECLARE @HR int;  
DECLARE @Property nvarchar(255);  
DECLARE @Return nvarchar(255);  
DECLARE @Source nvarchar(255), @Desc nvarchar(255);  
  
-- Create a SQLServer object.  
SET NOCOUNT ON;  
  
-- First, create the object.  
EXEC @HR = sp_OACreate N'SQLDMO.SQLServer',  
    @Object OUT;  
IF @HR <> 0  
BEGIN  
    -- Report the error.  
    EXEC sp_OAGetErrorInfo @Object,  
        @Source OUT,  
        @Desc OUT;  
    SELECT HR = convert(varbinary(4),@HR),  
        Source=@Source,  
        Description=@Desc;  
    GOTO END_ROUTINE  
END  
ELSE  
-- A DMO.SQLServer object has been successfully created.  
BEGIN  
    -- Specify Windows Authentication for connections.  
    EXEC @HR = sp_OASetProperty @Object,  
        N'LoginSecure',  
        N'TRUE';  
    IF @HR <> 0 GOTO CLEANUP  
  
    -- Set a property.  
    EXEC @HR = sp_OASetProperty @Object,  
        N'HostName',  
        N'SampleScript';  
    IF @HR <> 0 GOTO CLEANUP  
  
    -- Get a property using an output parameter.  
    EXEC @HR = sp_OAGetProperty @Object, N'HostName', @Property OUT;  
    IF @HR <> 0   
        GOTO CLEANUP  
    ELSE  
        PRINT @Property;  
  
    -- Get a property using a result set.  
    EXEC @HR = sp_OAGetProperty @Object,  
        N'HostName';  
    IF @HR <> 0 GOTO CLEANUP  
  
    -- Get a property by calling the method.  
    EXEC @HR = sp_OAMethod @Object,  
        N'HostName',  
        @Property OUT;  
    IF @HR <> 0   
        GOTO CLEANUP  
    ELSE  
        PRINT @Property;  
  
    -- Call the connect method.  
    -- SECURITY NOTE - When possible, use Windows Authentication.  
    EXEC @HR = sp_OAMethod @Object,  
        N'Connect',  
        NULL,  
        N'localhost',  
        NULL,  
        NULL;  
    IF @HR <> 0 GOTO CLEANUP  
  
    -- Call a method that returns a value.  
    EXEC @HR = sp_OAMethod @Object,  
        N'VerifyConnection',  
        @Return OUT;  
    IF @HR <> 0  
        GOTO CLEANUP  
    ELSE  
        PRINT @Return;  
END  
  
CLEANUP:  
-- Check whether an error occurred.  
IF @HR <> 0  
BEGIN  
    -- Report the error.  
    EXEC sp_OAGetErrorInfo @Object,  
        @Source OUT,  
        @Desc OUT;  
    SELECT HR = convert(varbinary(4),@HR),  
        Source=@Source,  
        Description=@Desc;  
END  
  
-- Destroy the object.  
BEGIN  
    EXEC @HR = sp_OADestroy @Object;  
    -- Check if an error occurred.  
    IF @HR <> 0   
    BEGIN  
        -- Report the error.  
        EXEC sp_OAGetErrorInfo @Object,  
        @Source OUT,  
        @Desc OUT;  
        SELECT HR = convert(varbinary(4),@HR),  
        Source=@Source,  
        Description=@Desc;  
    END  
END  
  
END_ROUTINE:  
RETURN;  
GO  
```  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Objetos Automation no Transact-SQL](ole-automation-objects-in-transact-sql.md)  
  
 [sp_OACreate &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-oacreate-transact-sql)  
  
 [sp_OAGetProperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-oagetproperty-transact-sql)  
  
 [sp_OASetProperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-oasetproperty-transact-sql)  
  
 [sp_OAMethod &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-oamethod-transact-sql)  
  
 [sp_OADestroy &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-oadestroy-transact-sql)  
  
  
