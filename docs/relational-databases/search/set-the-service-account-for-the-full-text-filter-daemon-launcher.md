---
description: Definir a conta de serviço do Iniciador do Daemon de Filtro de Texto Completo
title: Definir a conta de serviço do Iniciador do Daemon de Filtro de Texto Completo
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], FDHOST Launcher (MSSQLFDLauncher) service account
- FDHOST Launcher (MSSQLFDLauncher) [SQL Server]
ms.assetid: 3ab1d101-7ae0-488f-9b57-468e2517b737
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.custom: seo-lt-2019
ms.openlocfilehash: db5d05ce1b3712eebbd77d34e8ae0b380e18dcbf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420370"
---
# <a name="set-the-service-account-for-the-full-text-filter-daemon-launcher"></a>Definir a conta de serviço do Iniciador do Daemon de Filtro de Texto Completo
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
 Este tópico descreve como definir ou alterar a conta de serviço Iniciador do Daemon de Filtro de Texto Completo do SQL (MSSQLFDLauncher) usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager. A conta de serviço padrão usada pelo programa de instalação do SQL Server é `NT Service\MSSQLFDLauncher`.
  
  
## <a name="about-the-sql-full-text-filter-daemon-launcher-service"></a>Sobre o serviço do Iniciador do Daemon de Filtro de Texto Completo do SQL
O serviço Iniciador do Daemon do Filtro de Texto Completo do SQL é usado pela Pesquisa de texto completo do SQL Server para iniciar o processo do host do daemon de filtro, que manipula a filtragem da pesquisa de texto completo e a quebra de palavras. Esse Iniciador deve estar em execução para usar a pesquisa de texto completo.  
  
O Iniciador do Daemon de Filtro de Texto Completo do SQL é um serviço de reconhecimento de instâncias associado a uma instância específica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O serviço Iniciador do Daemon de Filtro de Texto Completo do SQL propaga as informações da conta de serviço para cada processo do host do daemon de filtro que ele inicia.  

##  <a name="set-the-service-account"></a><a name="setting"></a> Definir a conta de serviço  
  
1.  No menu **Iniciar**, aponte para **Todos os Programas**, expanda [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)] e clique em **SQL Server 2016 Configuration Manager**.  
  
2.  No **SQL Server Configuration Manager**, clique em **Serviços do SQL Server**, clique com o botão direito do mouse em **Iniciador do Daemon de Filtro de Texto Completo do SQL (**_nome da instância_**)** e clique em **Propriedades**.  
  
3.  Clique na guia **Fazer Logon** da caixa de diálogo e selecione ou digite a conta em que será executado os processos iniciados pelo serviço Iniciador do Daemon de Filtro de Texto Completo do SQL.  
  
4.  Depois que você fechar a caixa de diálogo, clique em **Reiniciar** para reiniciar o serviço Iniciador do Daemon de Filtro de Texto Completo do SQL.  
  
![Propriedades do processo do Iniciador do Daemon de Filtro de Texto Completo do SQL](../../relational-databases/search/media/sql-full-text-filter-daemon-launch-process-properties.png)
  
##  <a name="troubleshoot-the-sql-full-text-filter-daemon-launcher-service-if-it-doesnt-start"></a><a name="error"></a> Solucionar os problemas do serviço Iniciador do Daemon de Filtro de Texto Completo do SQL se ele não iniciar  
 Se o serviço Iniciador do Daemon de Filtro de Texto Completo do SQL não for iniciado, examine as seguintes causas possíveis:  
  
### <a name="permissions-issues"></a>Problemas de permissões
-   O grupo de serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não tem permissão para iniciar o serviço Iniciador do Daemon de Filtro de Texto Completo do SQL.  

     Verifique se o grupo de serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tem permissões na conta de serviço Iniciador do Daemon de Filtro de Texto Completo do SQL. Durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é concedido ao grupo de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permissão padrão para gerenciar, consultar e iniciar o serviço Iniciador do Daemon de Filtro de Texto Completo do SQL. Se as permissões do grupo de serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a conta de serviço Iniciador do Daemon de Filtro de Texto Completo do SQL tiverem sido removidas após a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o serviço Iniciador do Daemon de Filtro de Texto Completo do SQL não será iniciado e a pesquisa de texto completo será desabilitada.     

-   A conta usada para fazer logon no serviço não possui privilégios.  
  
     Talvez você esteja usando uma conta que não tem privilégios de logon no computador em que está instalada a instância do servidor. Verifique se está fazendo o logon com uma conta que possua direitos e permissões de Usuário no computador local.  

### <a name="service-account-and-password-issues"></a>Problemas de conta de serviço e senha
-   A conta de usuário ou a senha da conta de serviço está incorreta.  
  
     No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 Configuration Manager, verifique se o serviço está usando a conta de serviço e senha corretas.  
  
-   A senha associada à conta do serviço Iniciador do Daemon de Filtro de Texto Completo do SQL expirou.  
  
     Se você utiliza uma conta de usuário local para o serviço Iniciador do Daemon de Filtro de Texto Completo do SQL e a senha expirar, será necessário:  
  
    1.  Definir uma nova senha do Windows para a conta.  
  
    2.  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 Configuration Manager, atualize o serviço Iniciador do Daemon de Filtro de Texto Completo do SQL para usar a nova senha.  
  
### <a name="named-pipes-configuration-issues"></a>Problemas de configuração de pipes nomeados
-   O serviço Iniciador do Daemon de Filtro de Texto Completo do SQL não está configurado corretamente.  
  
     Se a funcionalidade de pipes nomeados foi desabilitada no computador local ou se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi configurado para usar um pipe nomeado diferente do padrão, é possível que o serviço Iniciador do Daemon de Filtro de Texto Completo do SQL não seja iniciado.  
  
-   Outra instância do mesmo pipe nomeado já está sendo executada.  
  
     Os serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atua como um servidor de pipe nomeado para o cliente do serviço Iniciador do Daemon de Filtro de Texto Completo do SQL. Se o pipe nomeado já foi criado por outro processo antes de o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ser iniciado, um erro será registrado no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e no Log de Eventos do Windows, e a pesquisa de texto completo não estará disponível.  Determine qual processo ou aplicativo está tentando usar o mesmo pipe nomeado e interrompa o aplicativo.  
  
## <a name="see-also"></a>Consulte Também  
 [Tópicos de instruções sobre gerenciamento de serviços &#40;SQL Server Configuration Manager&#41;](https://msdn.microsoft.com/library/78dee169-df0c-4c95-9af7-bf033bc9fdc6)   
 [Atualizar pesquisa de texto completo](../../relational-databases/search/upgrade-full-text-search.md)  
  
  
