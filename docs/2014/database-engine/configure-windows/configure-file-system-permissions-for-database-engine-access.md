---
title: Configurar permissões do sistema de arquivos para acesso ao Mecanismo de Banco de Dados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- file system permissions
- service account [SQL Server], file system permissions
- permissions [SQL Server], file system
ms.assetid: 78bba43c-4edb-4216-84ac-d6246ae5546d
caps.latest.revision: 6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d16d2580775cde3c1b87c934c1bd69133501d3ab
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37260942"
---
# <a name="configure-file-system-permissions-for-database-engine-access"></a>Configurar permissões do sistema de arquivos para acesso ao mecanismo de banco de dados
  Este tópico descreve como conceder ao [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]acesso ao sistema de arquivos ao local onde os arquivos de banco de dados são armazenados. O serviço do [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve ter a permissão do sistema de arquivos do Windows para acessar a pasta onde os arquivos de banco de dados são armazenados. A permissão para o local padrão é configurada durante a instalação. Se você colocar seus arquivos de banco de dados em um local diferente, poderá precisar seguir estas etapas para conceder ao [!INCLUDE[ssDE](../../includes/ssde-md.md)] a permissão de controle total para esse local.  
  
 A partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , as permissões são atribuídas ao SID por serviço para cada um de seus serviços. Este sistema ajuda a fornecer o isolamento de serviço e defesa mais eficiente. O SID por serviço é derivado do nome do serviço e é exclusivo a cada serviço. O tópico [Configurar contas de serviço e permissões do Windows](configure-windows-service-accounts-and-permissions.md) descreve o SID por serviço e fornece os nomes na seção **Privilégios e direitos do Windows**. É o SID por serviço que deve receber a permissão de acesso no local do arquivo.  
  
## <a name="to-grant-file-system-permission-to-the-per-service-sid"></a>Para conceder permissão do sistema de arquivos ao SID por serviço  
  
1.  Usando o Windows Explorer, navegue até o local do sistema de arquivos onde os arquivos de banco de dados são armazenados. Clique com o botão direito do mouse na pasta do sistema de arquivos e clique em **Propriedades**.  
  
2.  Na guia **Segurança** , clique em **Editar**e em **Adicionar**.  
  
3.  Na caixa de diálogo **Selecionar Usuários, Computadores, Conta de Serviço ou Grupos** , clique em **Localizações**na parte superior da lista de localizações, selecione o nome de seu computador e clique em **OK**.  
  
4.  No **digite os nomes de objeto para selecionar** caixa, digite o nome do SID por serviço listado no tópico nos Manuais Online **configurar contas de serviço do Windows e permissões**. (Para o [!INCLUDE[ssDE](../../includes/ssde-md.md)] SID por serviço, use **NT SERVICE\MSSQLSERVER** para uma instância padrão, ou **NT SERVICE\MSSQL$ NomeInstância** para uma instância nomeada.)  
  
5.  Clique em **Verificar Nomes** para validar a entrada. A validação geralmente falha e pode alertá-lo de que o nome não foi localizado. Quando você clica em **OK**, uma caixa de diálogo **Vários nomes encontrados** é exibida.  
  
6.  Agora, selecione o SID por serviço, ou **MSSQLSERVER** ou **NT SERVICE\MSSQL$ NomeInstância**e, em seguida, clique em **Okey**.  
  
7.  Clique em **Okey** novamente para retornar para o **permissões** caixa de diálogo.  
  
8.  No **grupo ou usuário** nomes, marque o SID por serviço e, em seguida, no **permissões para** \<nome > caixa, selecione o **permitir** caixadeseleção **Controle total**.  
  
9. Clique em **Aplicar**e em **OK** duas vezes para sair.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar os serviços do Mecanismo de Banco de Dados](manage-the-database-engine-services.md)   
 [Mover bancos de dados do sistema](../../relational-databases/databases/system-databases.md)   
 [Mover bancos de dados de usuário](../../relational-databases/databases/move-user-databases.md)  
  
  
