---
title: Renomear um computador que hospeda uma instância autônoma do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- remote login errors [SQL Server]
- standalone computer names [SQL Server]
- names [SQL Server], standalone instances of SQL Server
- renaming standalone instances of SQL Server
- sysservers system table
- removing remote logins
- deleting remote logins
- dropping remote logins
ms.assetid: bbaf1445-b8a2-4ebf-babe-17d8cf20b037
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1bd9e18d1dfe7226d043a7c8c968999da680da08
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62775001"
---
# <a name="rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server"></a>Renomear um computador que hospeda uma instância autônoma do SQL Server
  Quando você altera o nome do computador que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o novo nome será reconhecido durante a inicialização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Não é necessário executar novamente a Instalação para redefinir o nome do computador. Em vez disso, use as etapas a seguir para atualizar os metadados do sistema armazenados em sys.servers e relatados pela função de sistema @@SERVERNAME . Atualize os metadados do sistema para que reflitam as alterações de nome do computador de conexões remotas e aplicativos que usam @@SERVERNAME ou que consultam o nome do servidor em sys.servers.  
  
 As etapas a seguir não podem ser usadas para renomear uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Elas só podem ser usadas para renomear a parte do nome de instância que corresponde ao nome do computador. Por exemplo, você pode alterar um computador denominado MB1 que hospede uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] denominada Instance1 para outro nome, como MB2. Entretanto, a parte de instância do nome, Instance1, permanecerá inalterada. Neste exemplo, \\\\*ComputerName*\\*InstanceName* seria alterado de \\\MB1\Instance1 para \\\MB2\Instance1.  
  
 **Antes de começar**  
  
 Antes de começar o processo de renomeação, revise as seguintes informações:  
  
-   Quando uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fizer parte de um cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o processo de renomeação do computador difere de um computador que hospeda uma instância autônoma.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não dá suporte à renomeação de computadores que estejam envolvidos em replicação, exceto quando você usar o envio de logs com a replicação. O computador secundário no envio de logs poderá ser renomeado se o computador primário for permanentemente perdido. Para obter mais informações, veja [Replicação e envio de logs &#40;SQL Server&#41;](../log-shipping/log-shipping-and-replication-sql-server.md).  
  
-   Quando você renomear um computador que está configurado para usar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] poderá não ficar disponível após a alteração do nome do computador. Para obter mais informações, veja [Renomear um computador de servidor de relatório](../../reporting-services/report-server/rename-a-report-server-computer.md).  
  
-   Quando você renomear um computador que está configurado para usar espelhamento de banco de dados, deverá desativar o espelhamento de banco de dados antes da operação de renomeação. Em seguida, restabeleça o espelhamento de banco de dados com o novo nome do computador. Os metadados para o espelhamento de banco de dados não serão atualizados automaticamente para refletir o novo nome do computador. Use as etapas a seguir para atualizar os metadados de sistema.  
  
-   Os usuários que se conectem ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio de um grupo do Windows que use uma referência embutida em código ao nome do computador talvez não consigam se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Isso pode acontecer após a renomeação se o grupo do Windows especificar o nome antigo do computador. Para assegurar que tais grupos do Windows tenham conectividade com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] após a operação de renomeação, atualize o grupo do Windows para especificar o novo nome do computador.  
  
 Você poderá se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o novo nome do computador depois de reiniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para garantir que @@SERVERNAME retorne o nome atualizado da instância do servidor local, execute manualmente o procedimento a seguir aplicável ao seu cenário. O procedimento usado depende de a atualização ser feita em um computador que hospeda uma instância padrão ou nomeada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="to-rename-a-computer-that-hosts-a-stand-alone-instance-of-includessnoversionincludesssnoversion-mdmd"></a>Para renomear um computador que hospeda uma instância autônoma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Para um computador renomeado que hospeda uma instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], execute os seguintes procedimentos:  
  
    ```  
    sp_dropserver <old_name>;  
    GO  
    sp_addserver <new_name>, local;  
    GO  
    ```  
  
     Reinicie a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Para um computador renomeado que hospeda uma instância nomeada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], execute os seguintes procedimentos:  
  
    ```  
    sp_dropserver <old_name\instancename>;  
    GO  
    sp_addserver <new_name\instancename>, local;  
    GO  
    ```  
  
     Reinicie a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="after-the-renaming-operation"></a>Após a operação de renomeação  
 Depois que um computador for renomeado, quaisquer conexões que usavam o nome antigo do computador deverão ser conectadas usando o novo nome.  
  
#### <a name="to-verify-that-the-renaming-operation-has-completed-successfully"></a>Para verificar se a operação renomeação foi concluída com êxito  
  
-   Selecione informações de @@SERVERNAME ou sys.servers. A função @@SERVERNAME retornará o novo nome e a tabela sys.servers mostrará o novo nome. O exemplo a seguir mostra o uso de @@SERVERNAME .  
  
    ```  
    SELECT @@SERVERNAME AS 'Server Name';  
    ```  
  
## <a name="additional-considerations"></a>Considerações adicionais  
 **Logons remotos** – Se o computador tiver logons remotos, a execução de **sp_dropserver** poderá gerar um erro semelhante ao seguinte:  
  
 `Server: Msg 15190, Level 16, State 1, Procedure sp_dropserver, Line 44 There are still remote logins for the server 'SERVER1'.`  
  
 Para resolver o erro, você deve descartar logons remotos para esse servidor.  
  
#### <a name="to-drop-remote-logins"></a>Para descartar logons remotos  
  
-   Para uma instância padrão, execute o seguinte procedimento:  
  
    ```  
    sp_dropremotelogin old_name;  
    GO  
    ```  
  
-   Para uma instância nomeada, execute o seguinte procedimento:  
  
    ```  
    sp_dropremotelogin old_name\instancename;  
    GO  
    ```  
  
 **Configurações de servidor vinculado** – As configurações de servidor vinculado serão afetadas pela operação de renomeação de computador. Use `sp_addlinkedserver` ou `sp_setnetname` para atualizar referências de nome de computador. Para obter mais informações, veja [sp_addlinkedserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql) ou [sp_setnetname &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-setnetname-transact-sql).  
  
 **Nomes de alias de cliente** – Os aliases de cliente que usam pipes nomeados serão afetados pela operação de renomeação do computador. Por exemplo, se foi criado um alias "PROD_SRVR" para apontar para SRVR1 que usa o protocolo de pipes nomeados, o nome do pipe será `\\SRVR1\pipe\sql\query`. Depois que o computador for renomeado, o caminho do pipe nomeado deixará de ser válido. Para obter mais informações sobre pipes nomeados, veja o tópico [Criando uma cadeia de conexão válida usando pipes nomeados](https://go.microsoft.com/fwlink/?LinkId=111063).  
  
## <a name="see-also"></a>Consulte Também  
 [Instalar o SQL Server 2014](../../database-engine/install-windows/install-sql-server.md)  
  
  
