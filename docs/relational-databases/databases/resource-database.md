---
title: Banco de dados de recursos| Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- system objects [SQL Server]
- read-only databases
- mssqlsystemresource.mdf file
- Resource database [SQL Server]
ms.assetid: d592b2b4-bc36-4eb9-9385-8fe4dff0dced
caps.latest.revision: 71
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: efcb8d4f781f634d24c00e0698da746dd3b4efa8
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="resource-database"></a>Banco de dados de recursos
  O banco de dados Recurso é um banco de dados somente leitura que contém todos os objetos de sistema inclusos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos do sistema como sys.objects, são fisicamente persistentes no banco de dados Resource, mas aparecem logicamente no esquema sys de cada banco de dados. O banco de dados Recurso não contém dados de usuário ou metadados de usuário.  
  
 O banco de dados Recurso torna a atualização para uma nova versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] um procedimento mais fácil e mais rápido. Em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a atualização exigia remover e criar objetos do sistema. Como o arquivo de banco de dados Recurso contém todos os objetos de sistema, agora, uma atualização é obtida simplesmente pela cópia do único arquivo de banco de dados Recurso no servidor local.  
  
## <a name="physical-properties-of-resource"></a>Propriedades físicas de Resource  
 Os nomes dos arquivos físicos do banco de dados do Recurso são mssqlsystemresource.mdf e mssqlsystemresource.ldf. Esses arquivos estão localizados em \<*drive*>:\Program Files\Microsoft SQL Server\MSSQL\<version>.\<*instance_name*>\MSSQL\Binn\ e não devem ser movidos. Cada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tem um e apenas um arquivo mssqlsystemresource.mdf associado, e as instâncias não compartilham esse arquivo.  
  
> [!WARNING]  
>  Atualizações e service packs às vezes fornecem um novo banco de dados recurso que é instalado na pasta BINN. Alterar o local do banco de dados do recurso não é suportado nem recomendado.  
  
## <a name="backing-up-and-restoring-the-resource-database"></a>Fazendo backup e restaurando o banco de dados de recursos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode fazer backup do banco de dados Resource. Você pode executar seu próprio backup baseado em arquivo ou baseado em disco ao tratar o arquivo mssqlsystemresource.mdf como se ele fosse um arquivo binário (.EXE), em vez de um arquivo de banco de dados, mas você não pode usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para restaurar seus backups. Só é possível restaurar uma cópia de backup do mssqlsystemresource.mdf manualmente, e você deve ter cuidado para não sobrescrever o atual banco de dados  Recurso com uma versão desatualizada ou potencialmente insegura.  
  
> [!IMPORTANT]  
>  Depois de restaurar um backup do mssqlsystemresource.mdf, você deve reaplicar qualquer atualização subsequente.  
  
## <a name="accessing-the-resource-database"></a>Acessando o banco de dados Resource  
 O banco de dados Recurso só deve ser modificado por ou sob a orientação de um especialista do Serviço de Suporte Técnico da Microsoft (CSS). A ID do banco de dados de  Recursos será sempre 32767. Outros valores importantes associados ao banco de dados de Recursos são o número da versão e a última vez em que o banco de dados foi atualizado.  
  
 **Para determinar o número de versão do banco de dados** Resource **, use**:  
  
```  
SELECT SERVERPROPERTY('ResourceVersion');  
GO  
```  
  
 **Para determinar quando o banco de dados** Resource **foi atualizado pela última vez, use**:  
  
```  
SELECT SERVERPROPERTY('ResourceLastUpdateDateTime');  
GO  
```  
  
 **Para acessar definições SQL dos objetos de sistema, utilize a função OBJECT_DEFINITION:**  
  
```  
SELECT OBJECT_DEFINITION(OBJECT_ID('sys.objects'));  
GO  
```  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Bancos de dados do sistema](../../relational-databases/databases/system-databases.md)  
  
 [Conexão de diagnóstico para administradores de banco de dados](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)  
  
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)  
  
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)  
  
 [Iniciar o SQL Server no modo de usuário único](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md)  
  
  
