---
title: Iniciar o Utilitário sqlcmd | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 00d57437-7a29-4da1-b639-ee990db055fb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ec1ec91705dfb9194f42c079cb7b3d5100c9d396
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66090105"
---
# <a name="start-the-sqlcmd-utility"></a>Iniciar o utilitário sqlcmd
  Para começar a usar o `sqlcmd`, você deve primeiro iniciar o utilitário e se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode se conectar a uma instância padrão ou nomeada. A primeira etapa é iniciar o utilitário `sqlcmd`.  
  
> [!NOTE]  
>  A Autenticação do Windows é o modo de autenticação padrão do `sqlcmd`. Para usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , você deve especificar um nome de usuário e uma senha usando as opções **-U** e **-P** .  
  
> [!NOTE]  
>  Por padrão, o [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] é instalado como a instância nomeada **sqlexpress**.  
  
 Caso você não tenha se conectado a essa instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] anteriormente, você pode ter de configurar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para aceitar conexões.  
  
### <a name="to-start-the-sqlcmd-utility-and-connect-to-a-default-instance-of-sql-server"></a>Para iniciar o utilitário sqlcmd e conectar-se a uma instância padrão do SQL Server  
  
1.  No menu **Iniciar** , clique em **Executar**. Na caixa **Abrir** digite **cmd**e, então, clique em **OK** para abrir uma janela do prompt de comando.  
  
2.  No prompt de comando, digite `sqlcmd`.  
  
3.  Pressione ENTER.  
  
     Agora você tem uma conexão confiável com a instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo executada em seu computador.  
  
     **1 >** é o `sqlcmd` prompt que especifica o número de linha. A cada vez que você pressiona ENTER, aparece um número seguinte ao anterior.  
  
4.  Para encerrar a `sqlcmd` sessão, digite `EXIT` no `sqlcmd` prompt.  
  
### <a name="to-start-the-sqlcmd-utility-and-connect-to-a-named-instance-of-sql-server"></a>Para iniciar o utilitário sqlcmd e se conectar a uma instância nomeada do SQL Server  
  
1.  Abra um Prompt de comando janela e digite `sqlcmd -S` *myServer\instanceName*. Substitua *myServer\instanceName* pelo nome do computador e a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com a qual você deseja se conectar.  
  
2.  Pressione ENTER.  
  
     O `sqlcmd` prompt (1 >) indica que você está conectado à instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    > [!NOTE]  
    >  As instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] digitadas são armazenadas em um buffer. Elas são executadas como um lote quando o comando GO é encontrado.  
  
## <a name="see-also"></a>Consulte também  
 [Executar arquivos de script Transact-SQL usando sqlcmd](sqlcmd-run-transact-sql-script-files.md)  
  
  
