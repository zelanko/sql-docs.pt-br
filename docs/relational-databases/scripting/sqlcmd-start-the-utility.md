---
title: "Iniciar o Utilitário sqlcmd | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 00d57437-7a29-4da1-b639-ee990db055fb
caps.latest.revision: 
author: mightypen
ms.author: genemi
manager: craigg
ms.workload: Active
ms.openlocfilehash: f7e35bb04d5ff169800d837b05a63320640adeff
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2018
---
# <a name="sqlcmd---start-the-utility"></a>sqlcmd – Iniciar o utilitário
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] O utilitário [SQLCMD](../../tools/sqlcmd-utility.md) permite inserir instruções [!INCLUDE[tsql](../../includes/tsql-md.md)], procedimentos do sistema e arquivos de script no prompt de comando, no Editor de Consultas em modo SQLCMD, em um arquivo de script do Windows ou em uma etapa de trabalho do sistema operacional (Cmd.exe) de um trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.
> [!NOTE]  
>  A Autenticação do Windows é o modo de autenticação padrão do **sqlcmd**. Para usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , você deve especificar um nome de usuário e uma senha usando as opções **-U** e **-P** .  
  
> [!NOTE]  
>  Por padrão, o [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] é instalado como a instância nomeada **sqlexpress**.  
  
### <a name="start-the-sqlcmd-utility-and-connect-to-a-default-instance-of-sql-server"></a>Inicie o utilitário sqlcmd e conecte-se a uma instância padrão do SQL Server  
  
1.  No menu **Iniciar** , clique em **Executar**. Na caixa **Abrir** digite **cmd**e, então, clique em **OK** para abrir uma janela do prompt de comando. (Caso não tenha se conectado a essa instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] anteriormente, você poderá precisar configurar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para aceitar conexões.)  
  
2.  No prompt de comando, digite **sqlcmd**.  
  
3.  Pressione ENTER.  
  
     Agora você tem uma conexão confiável com a instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo executada em seu computador.  
  
     **1>** é o prompt do **sqlcmd** que especifica o número de linha. A cada vez que você pressiona ENTER, aparece um número seguinte ao anterior.  
  
4.  Para encerrar a sessão **sqlcmd** , digite **EXIT** no prompt **sqlcmd** .  
  
### <a name="start-the-sqlcmd-utility-and-connect-to-a-named-instance-of-sql-server"></a>Inicie o utilitário sqlcmd e se conectar a uma instância nomeada do SQL Server  
  
1.  Abra uma janela do prompt de comando e digite **sqlcmd -S***myServer\instanceName*. Substitua *myServer\instanceName* pelo nome do computador e a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com a qual você deseja se conectar.  
  
2.  Pressione ENTER.  
  
     O prompt do **sqlcmd** (1>) indica que você está conectado à instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    > [!NOTE]  
    >  As instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] digitadas são armazenadas em um buffer. Elas são executadas como um lote quando o comando GO é encontrado.  
  
## <a name="see-also"></a>Consulte Também  
 [Executar arquivos de script Transact-SQL usando sqlcmd](../../relational-databases/scripting/sqlcmd-run-transact-sql-script-files.md)  
  
  
