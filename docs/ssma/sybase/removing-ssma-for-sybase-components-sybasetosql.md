---
title: Remover o SSMA para componentes do Sybase (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: aec09593-17d9-4ec2-ac56-3cd8851406fd
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: b3cebc9bb82778390716212fd3b5ae1bf800d3d3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47744804"
---
# <a name="removing-ssma-for-sybase-components-sybasetosql"></a>Remover componentes SSMA para Sybase (SybaseToSQL)
Quando você terminar de migrar bancos de dados do Sybase Adaptive Server Enterprise (ASE) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], talvez você queira desinstalar os componentes do SSMA. Você pode desinstalar os componentes do cliente a qualquer momento, mas você não deve desinstalar o pacote de extensão de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] menos que tenha certeza de que seus bancos de dados migrados não for mais usam funções na **ssma_syb** esquema dos **sysdb** banco de dados.  
  
## <a name="uninstalling-the-ssma-for-sybase-client"></a>Desinstalando o SSMA para Sybase cliente  
Você pode desinstalar o SSMA usando **adicionar ou remover programas**.  
  
**Para desinstalar o SSMA**  
  
1.  No painel de controle, abra **adicionar ou remover programas**.  
  
2.  Selecione **Microsoft SQL Server Migration Assistant for Sybase**e, em seguida, clique em **remover**.  
  
3.  Para confirmar que você deseja desinstalar o SSMA, clique em **Sim**.  
  
## <a name="uninstalling-the-extension-pack"></a>Desinstalando o pacote de extensão  
Se você tiver certeza seus bancos de dados migrados não usam objetos na **sysdb.ssma_syb** esquema, você pode remover o pacote de extensão usando **adicionar ou remover programas**.  
  
Para desinstalar o pacote de extensão  
  
1.  No painel de controle, abra **adicionar ou remover programas**.  
  
2.  Selecione **Microsoft SQL Server Migration Assistant para o pacote de extensão do Sybase**e, em seguida, clique em **remover**.  
  
3.  Para confirmar que você deseja desinstalar o pacote de extensão, clique em **Sim**.  
  
4.  Nas instâncias com página de Scripts de banco de dados de utilitários, clique em **próxima**.  
  
5.  Na página de parâmetros de Conexão, selecione o método de autenticação e, em seguida, clique em **próxima**.  
  
    Autenticação do Windows usarão suas credenciais do Windows para tentar fazer logon com a instância do SQL Server. Se você selecionar a autenticação do SQL Server, você deve inserir um nome de logon do SQL Server e uma senha.  
  
6.  Na página de operação concluída, clique em **Okey**.  
  
7.  Na página concluir, clique em **Exit**.  
  
Após a desinstalação, você pode confirmar que o **sysdb.ssma_syb** esquema e, possivelmente, todo **sysdb** banco de dados, foi removido usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. No entanto, se você usar outros produtos do SSMA, eles também usam o **sysdb** banco de dados. Se o banco de dados existe e tem certeza de que nenhum outro banco de dados fazem referência a objetos neste banco de dados, é possível desanexar o banco de dados.  
  
## <a name="see-also"></a>Consulte também  
[Instalar o SSMA para Sybase cliente &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[Instalar os componentes do SSMA no SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
  
