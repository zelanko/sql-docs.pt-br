---
title: Registrar um banco de dados espelhado | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.dbmmonitor.registermirroreddb.f1
ms.assetid: 6acd02b9-2311-49b0-a5f8-3852beecb4b0
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b5be7eb52d0aa8c0a94b1a4ff63493e7f641bdbd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62754463"
---
# <a name="register-mirrored-database"></a>Registrar banco de dados espelho
  Use esta caixa de diálogo para registrar um ou mais bancos de dado espelhados em uma determinada instância do servidor, adicionando o banco de dados, ou bancos de dados, ao Monitor de Espelhamento de Banco de Dados. Quando um banco de dados é adicionado, o Monitor de Espelhamento de Banco de Dados armazena localmente em cache as informações do banco de dados, seus parceiros e como se conectar aos parceiros.  
  
> [!IMPORTANT]  
>  Se você for um membro da função de servidor fixa **sysadmin** na instância do servidor principal, mas não na instância do servidor espelho, você só poderá ver o status na instância do servidor principal.  
  
 **Para usar o SQL Server Management Studio para monitorar o espelhamento de banco de dados**  
  
-   [Iniciar o Monitor de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
## <a name="options"></a>Opções  
 **Instância de servidor**  
 Selecione uma instância de servidor na lista, que contém instâncias de servidor às quais o Monitor de Espelhamento de Banco de Dados já tem uma conexão armazenada, ou clique em **Conectar**. Para especificar novas credenciais para uma instância de servidor listada, clique em **Conectar** e se conecte usando as novas credenciais.  
  
> [!NOTE]  
>  Para registrar bancos de data em várias instâncias de servidor, depois de concluir a verificação dos bancos de dados desejados para uma instância de servidor, clique em **Aplicar**e selecione outra instância de servidor.  
  
 **Connect**  
 Para especificar novas credenciais para a instância de servidor, clique em **Conectar** e conecte-se usando as novas credenciais. Ao se conectar a uma instância de servidor, o Monitor de Espelhamento de Banco de Dados exibe **Aguardando dados**.  
  
 **Bancos de dados espelhados**  
 A grade **Bancos de Dados espelhados** lista os bancos de dados espelhados na instância do servidor.  
  
 A grade contém as seguintes colunas:  
  
|Nome da coluna|DESCRIÇÃO|  
|-----------------|-----------------|  
|**Registrar**|Verifique cada um dos bancos de dados que deseja registrar. Se um banco de dados já estiver monitorado, a sua caixa de seleção será marcada e será desabilitada.<br /><br /> Observação: para cancelar o registro do banco de dados, desmarque a caixa de diálogo **Banco de Dados Espelho Registrado** , selecione o banco de dados na árvore de navegação e selecione **Cancelar registro** no menu **Ação** .|  
|**Backup de banco de dados**|O nome de um banco de dados espelho na instância de servidor selecionada.|  
|**Função Atual**|A função de espelhamento atual do banco de dados, Principal ou Espelho na instância de servidor selecionada.|  
|**Parceiro (Conectar como)**|O nome do parceiro de failover do banco de dados. A **Autenticação do Windows do usuário do console** ou a **Autenticação do SQL Server do logon "***\<nome de logon>***"** é exibida entre parênteses. Essas são as informações de autenticação atualmente usadas, se a instância foi adicionada antes, ou que serão usadas, se esta instância não foi acrescentada ao monitor.|  
  
 **Mostrar a caixa de diálogo Gerenciar Conexões do Servidor quando clicar em OK.**  
 Por padrão, o Monitor de Espelhamento de Banco de Dados usa as credenciais do Windows Authentication para as instâncias do servidor parceiro para as quais credenciais não foram atribuídas anteriormente. Habilite esta opção para alterar as credenciais de uma ou mais instâncias de servidor quando concluir o registro de bancos de dados.  
  
 Se esta opção estiver habilitada, ao clicar em **OK**, a caixa de diálogo **Gerenciar Conexões do Servidor** é exibida. Lá, você pode escolher uma instância de servidor para a qual deseja especificar as credencias a serem usadas pelo monitor ao conectar a um determinado parceiro de failover.  
  
 Para editar as credenciais para o parceiro, localize sua entrada na grade **Instância de servidor** , e clique em **Editar** naquela linha. Isto exibe a caixa de diálogo **Conectar ao Servidor** para aquele nome de instância de servidor, com os controles de credenciais inicializados com o valor cache atual. Altere as credenciais conforme necessário e clique em **Conectar**. Se as credenciais tiverem privilégios suficientes, a coluna **Conectar Usando** é atualizada com as novas credenciais.  
  
 **Aplicar**  
 Clique neste botão para registrar o banco de dados selecionado (e salve os credenciais das instâncias de servidor do parceiro), mantendo ao mesmo tempo a caixa de diálogo aberta.  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar o Monitor de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [Monitorando o espelhamento de banco de dados &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [Iniciar o Assistente para Configurar Segurança de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](start-the-configuring-database-mirroring-security-wizard.md)  
  
  
