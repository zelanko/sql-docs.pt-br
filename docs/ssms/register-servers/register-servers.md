---
title: Registrar servidores | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.sqlserverregisteredserver.dhelp
helpviewer_keywords:
- connections [SQL Server], registered servers
- registering servers
- servers [SQL Server], registering
- server management [SQL Server], registering servers
- server registration [SQL Server]
ms.assetid: c2a2513e-fa09-419c-99e7-a12d57c5a0db
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 880692611ff827b77ec5f24565f7ce3626df17a5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65104267"
---
# <a name="register-servers"></a>Registrar servidores
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  O registro de um servidor no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] lhe permite armazenar as informações de conexão de servidor para conexões futuras. Há três modos de registrar um servidor no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
1.  As instâncias locais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são registradas automaticamente durante a primeira inicialização do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] após sua instalação.  
  
2.  Você também pode iniciar a qualquer hora o processo de registro automático, para restaurar o registro de instâncias do servidor local.  
  
3.  E ainda, você pode registrar um servidor usando a ferramenta Servidores Registrados no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="benefits-of-registered-servers"></a>Benefícios dos Servidores Registrados  
 Com os Servidores Registrados, você pode:  
  
-   Registrar servidores para preservar as informações de conexão.  
  
-   Determinar se um servidor registrado está sendo executado.  
  
-   Conectar facilmente o Pesquisador de Objetos e o Editor de Consultas a um servidor registrado.  
  
-   Editar ou excluir as informações de registro de um servidor registrado.  
  
-   Criar grupos de servidores.  
  
-   Fornecer nomes amigáveis para servidores registrados fornecendo um valor na caixa **Nome do servidor registrado** , que é diferente da lista **Nome do servidor** .  
  
-   Fornecer descrições detalhadas dos servidores registrados.  
  
-   Fornecer descrições detalhadas dos grupos de servidores registrados.  
  
-   Exportar grupos de servidores registrados.  
  
-   Importar grupos de servidores registrados.  
  
-   Exibir os arquivos de log do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para instâncias online ou offline do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="related-tasks"></a>Related Tasks  
 Use os seguintes tópicos como introdução rápida a servidores registrados:  
  
|**Descrição**|**Tópico**|  
|---------------------|---------------|  
|Registrar instâncias do servidor local|[Registrar um servidor conectado &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/register-a-connected-server-sql-server-management-studio.md)|  
|Registrar um servidor|[Criar um novo servidor registrado &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/create-a-new-registered-server-sql-server-management-studio.md)|  
|Exibir servidores registrados|[Exibir Servidores Registrados no SQL Server Management Studio](../../tools/sql-server-management-studio/view-registered-servers-in-sql-server-management-studio.md)|  
|Remover um servidor registrado|[Remover um servidor registrado &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/remove-a-registered-server-sql-server-management-studio.md)|  
|Alterar um registro de servidor|[Alterar um registro do servidor &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/change-a-server-s-registration-sql-server-management-studio.md)|  
|Conectar-se com um servidor registrado|[Conectar-se a um servidor registrado &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/connect-to-a-registered-server-sql-server-management-studio.md)|  
|Desconectar de um servidor registrado|[Desconectar-se de um Servidor Registrado &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/disconnect-from-a-registered-server-sql-server-management-studio.md)|  
|Mover um servidor registrado ou grupo de servidores|[Mover um servidor registrado ou um grupo de Servidores Registrados &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/move-a-registered-server-or-registered-server-group.md)|  
|Altere o nome de um servidor registrado ou grupo de servidores|[Alterar o nome de um Servidor Registrado ou de um grupo de Servidores Registrados &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/change-the-name-of-registered-server-or-registered-server-group.md)|  
|Criar ou editar um grupo de servidor|[Criar ou editar um grupo de servidores &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/create-or-edit-a-server-group-sql-server-management-studio.md)|  
|Remover um grupo de servidor|[Remover um grupo de servidores &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/remove-a-server-group-sql-server-management-studio.md)|  
|Exportar informações de servidor registrado|[Exportar informações de servidor registrado &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/export-registered-server-information-sql-server-management-studio.md)|  
|Importar informações de servidor registrado|[Importar informações de servidor registrado &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/import-registered-server-information-sql-server-management-studio.md)|  
|Criar um servidor de gerenciamento central e grupo de servidor|[Criar um servidor de gerenciamento central e um grupo de servidores &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/create-a-central-management-server-and-server-group.md)|  
|Executar instruções em vários servidores simultaneamente|[Executar instruções em vários servidores simultaneamente &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/execute-statements-against-multiple-servers-simultaneously.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Servidores remotos](../../database-engine/configure-windows/remote-servers.md)  
  
  
