---
title: Solucionar problemas do Utilitário do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: f5f47c2a-38ea-40f8-9767-9bc138d14453
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d5203a0a613bcd8af4b247058f3cb594be5d4c3f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72797783"
---
# <a name="troubleshoot-the-sql-server-utility"></a>Solucionar problemas do Utilitário do SQL Server
  A solução de problemas do Utilitário do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode incluir a resolução de uma operação malsucedida de inscrição de uma instância do SQL Server com um UCP, a solução de problemas de falha na coleta de dados que resultam em ícones cinzas na exibição da lista de instâncias gerenciadas em um UCP, a redução de gargalos de desempenho ou a resolução de problemas de integridade de recursos. Para obter mais informações sobre como atenuar os problemas de integridade [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de recursos identificados por um UCP, consulte [solucionar problemas SQL Server Resource Health &#40;utilitário do SQL Server&#41;](../relational-databases/manage/troubleshoot-sql-server-resource-health-sql-server-utility.md).  
  
## <a name="failed-operation-to-enroll-an-instance-of-sql-server-into-a-sql-server-utility"></a>Falha na operação de inscrição de uma instância do SQL Server em um Utilitário do SQL Server  
 Se você se conectar à instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para inscrição usando a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e especificar uma conta proxy pertencente a um domínio do Active Directory diferente do domínio onde o UCP está localizado, a validação de instância terá êxito, mas a operação de inscrição falhará apresentando a seguinte mensagem de erro:  
  
 Ocorreu uma exceção ao executar uma instrução ou um lote Transact-SQL. (Microsoft.SqlServer.ConnectionInfo)  
  
 Informações adicionais: não foi possível obter informações sobre o grupo/usuário '\<DomainName\AccountName>' do Windows NT, código de erro 0x5. (Microsoft SQL Server, Erro: 15404)  
  
 Esse problema pode ocorrer no seguinte exemplo de cenário:  
  
1.  O UCP é um membro de "Domain_1".  
  
2.  Uma relação de confiança de domínio unidirecional está em vigor: ou seja, "Domain_2" não tem a confiança do "Domain_1", mas o "Domain_1" tem a confiança do "Domain_2".  
  
3.  A instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para inscrição no Utilitário do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] também é membro de "Domain_1".  
  
4.  Durante a operação de registro, conecte-se à [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instância do para se registrar usando "SA". Especifique uma conta proxy de "Domain_2".  
  
5.  A validação é bem-sucedida, mas a inscrição falha.  
  
 A solução alternativa para esse problema, usando o exemplo acima, é conectar-se à instância [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] do para se registrar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no utilitário usando "SA" e fornecer uma conta proxy de "Domain_1".  
  
## <a name="failed-wmi-validation"></a>Falha na validação de WMI  
 Se o WMI não for configurado corretamente em uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], as operações Criar UCP e Inscrever Instância Gerenciada exibirão um aviso, mas a operação não será bloqueada. Além disso, se você alterar a configuração da conta do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent de forma que o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent não tenha permissão para as classes WMI necessárias, a coleta de dados na instância gerenciada afetada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não carregará os dados no UCP. Isso resulta em ícones cinzas no UCP.  
  
 A falha na coleta de dados resulta em ícones de status cinzas na exibição de lista do UCP para instâncias gerenciadas afetadas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. O histórico do trabalho na instância gerenciada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] indica que sysutility_mi_collect_and_upload falhou na etapa 2 (Dados de Fase Coletados de Script do PowerShell).  
  
 As mensagens de erro simplificadas são:  
  
 A execução do comando parou porque a variável de shell "ErrorActionPreference" está definida para Parar: acesso negado.  
  
 ERRO: \<data e hora (mm/dd/aaaa hh: mm: SS) >: exceção detectada ao coletar Propriedades de CPU.  Uma consulta de WMI pode ter falhado.  AVISO.  
  
 Para resolver esse problema, verifique os seguintes parâmetros de configuração:  
  
-   No Windows Server 2003, o serviço SQL Server Agent deve fazer parte do grupo Monitoramento de Desempenho do Windows na instância gerenciada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   O serviço WMI deve ser habilitado e configurado na instância gerenciada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   O repositório WMI pode estar corrompido na instância gerenciada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   A biblioteca de desempenho pode estar faltando ou corrompida na instância gerenciada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 Para verificar se a instância especificada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está configurada corretamente para relatar dados ao UCP, verifique se as classes a seguir estão disponíveis na instância especificada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]e se elas são acessíveis à conta de serviço do SQL Server Agent:  
  
-   Win32_MountPoint  
  
-   Win32_PerfRawData_PerfProc_Process  
  
-   Win32_PerfRawData_PerfOS_Processor  
  
-   Win32_Processor  
  
-   Win32_Volume  
  
-   Win32_LogicalDisk  
  
 É possível usar o cmdlet Get-WmiObject PowerShell em cada uma das classes para verificar se cada classe é acessível. Execute os seguintes cmdlets na instância gerenciada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
```  
Get-WmiObject Win32_MountPoint -ErrorAction Stop | Out-Null  
Get-WmiObject Win32_PerfRawData_PerfProc_Process -ErrorAction Stop| Out-Null  
Get-WmiObject Win32_PerfRawData_PerfOS_Processor -ErrorAction Stop | Out-Null  
Get-WmiObject Win32_Processor -ErrorAction Stop | Out-Null  
Get-WmiObject Win32_Volume -ErrorAction Stop | Out-Null  
Get-WmiObject Win32_LogicalDisk -ErrorAction Stop | Out-Null  
```  
  
 Para obter mais informações sobre como solucionar problemas do WMI, consulte [Troubleshooting WMI (Solução de problemas da WMI)](https://go.microsoft.com/fwlink/?LinkId=178250). Observe que as consultas nessas operações do Utilitário do SQL Server são executadas localmente e, portanto, o conteúdo sobre DCOM e solução remota de problemas não se aplica.  
  
## <a name="failed-data-collection"></a>Falha na coleta de dados  
 Se eventos de coleta de dados do Utilitário do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] falharem, considere as seguintes possibilidades:  
  
-   Não altere nenhuma propriedade do conjunto de coleta “Informações sobre o Utilitário” em uma instância gerenciada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e não habilite/desabilite a coleta de dados manualmente, pois ela é controlada por um trabalho do agente do utilitário.  
  
-   Validação de WMI com falha ou sem suporte. Para obter mais informações, consulte a seção Falha na verificação de WMI anteriormente neste tópico.  
  
-   Atualize os dados na exibição de lista de instância gerenciada, já que os dados em pontos de visualização do Utilitário do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não são atualizados automaticamente. Para atualizar os dados, clique com o botão direito do mouse no nó **Instâncias Gerenciadas** , no painel de navegação do **Gerenciador do Utilitário** , e selecione **Atualizar**, ou clique com o botão direito do mouse no nome de instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] na exibição de lista e selecione **Atualizar**. Observe que, depois que uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] estiver inscrita em um UCP, poderá demorar até 30 minutos para os dados aparecerem pela primeira vez no painel e nos pontos de vista do painel de conteúdo do Gerenciador do Utilitário.  
  
-   Use o SQL Server Configuration Manager para verificar se a instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está em execução.  
  
-   Se houver falha na coleta ou no carregamento de dados devido a problemas de tempo limite, atualize a função dbo.fn_sysutility_mi_get_collect_script() no banco de dados MSDB. Mais especificamente, na função "Invoca-BulkCopyCommand () " adicione linha:  
  
    ```
    $bulkCopy.BulkCopyTimeout=180  
    ```  
  
     O valor do tempo limite padrão é de 30 segundos.  
  
-   Se a instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não for clusterizada, verifique se o serviço [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent está em execução e definido para ser iniciado automaticamente no UCP e na instância gerenciada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   Verifique se uma conta válida está sendo usada para executar a coleta de dados na instância gerenciada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Por exemplo, a senha pode ter expirado. Se a senha do proxy tiver expirado, atualize as credenciais de senha no SSMS, como se segue:  
  
    1.  No **Pesquisador de Objetos**do SSMS, expanda o nó **Segurança** e, em seguida, expanda o nó **Credenciais** .  
  
    2.  Clique com o botão direito do mouse em **UtilityAgentProxyCredential_\<GUID>** e selecione **Propriedades**.  
  
    3.  Na caixa de diálogo Propriedades da credencial, atualize as credenciais conforme necessário para o **GUID de UtilityAgentProxyCredential_\<>** credencial.  
  
    4.  Clique em **OK** para confirmar a alteração.  
  
-   O protocolo TCP/IP deve estar habilitado no UCP e na instância gerenciada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Habilite o TCP/IP usando o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager.  
  
-   O serviço Navegador do SQL Server no UCP deve ser iniciado e configurado para iniciar automaticamente. Se sua organização impedir o uso do serviço Navegador do SQL Server, use as seguintes etapas para permitir que uma instância gerenciada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se conecte ao UCP:  
  
    1.  Na barra de tarefas do Windows na instância gerenciada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], clique em **Iniciar**e em **executar...**.  
  
    2.  Digite "cliconfg.exe" no espaço fornecido e clique em **OK**.  
  
    3.  Se for solicitado a permitir que o utilitário de configuração do cliente SQL ("SQL Client Configuration Utility EXE") seja iniciado, clique em "**Continuar**".  
  
    4.  Na caixa de diálogo **SQL Server utilitário de rede do cliente** , selecione a guia **alias** e clique em **Adicionar...**.  
  
    5.  Na caixa de diálogo **Adicionar Configuração da Biblioteca de Rede** :  
  
    6.  Especifique TCP/IP na lista de bibliotecas de rede.  
  
    7.  Especifique o ComputerName\InstanceName do UCP na caixa de texto **Alias do Servidor** .  
  
    8.  Especifique o ComputerName do UCP na caixa de texto **Nome do Servidor** .  
  
    9. Desmarque a caixa de seleção **Determinar porta dinamicamente** .  
  
    10. Especifique o número da porta em que o UCP está escutando na caixa de texto **Número da porta** .  
  
    11. Clique em **OK** para salvar suas alterações.  
  
    12. Repita essas etapas para cada instância gerenciada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que se conectar a um UCP em que o serviço Navegador do SQL Server não está habilitado.  
  
-   Assegure-se de que as instâncias gerenciadas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] estejam conectadas à rede.  
  
-   Se houver bancos de dados com o mesmo nome, mas configurações distintas para diferenciação de maiúsculas e minúsculas em uma instância gerenciada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], a identificação entre o banco de dados e seus pontos de vista poderá estar incorreta, o que resulta em falha na coleta de dados. Por exemplo, um banco de dados denominado "MYDATABASE" poderia mostrar estados de integridade para um banco de dados denominado "MyDatabase". Nenhum erro é gerado nesse cenário. A falha na coleta de dados também pode ser o resultado de discrepâncias entre maiúsculas e minúsculas em outros objetos exibidos no UCP, como nomes de arquivos de banco de dados e de grupos de arquivos.  
  
-   Se uma instância gerenciada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] estiver hospedada em um computador com Windows Server 2003, a conta de serviço do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent deverá pertencer ao grupo de segurança Usuários de Monitor de Desempenho ou ao grupo Administradores local. Caso contrário, a coleta de dados falhará com um erro de acesso negado. Para adicionar uma conta do serviço [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent ao grupo de segurança Usuários de Monitor de Desempenho, use as seguintes etapas:  
  
    1.  Abra **Gerenciamento do Computador**, **Usuários e Grupos Locais**e, em seguida, **Grupos**.  
  
    2.  Clique com o botão direito do mouse em **Usuários de Monitor de Desempenho** e selecione **Adicionar ao grupo**.  
  
    3.  Clique em **Adicionar**.  
  
    4.  Insira a conta na qual o serviço SQL Server Agent está sendo executado e clique em **OK**.  
  
    5.  Se a instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] já estiver inscrita no UCP antes de o usuário ser adicionado a esse grupo, reinicie o serviço [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent.  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos e tarefas do Utilitário do SQL Server](../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Solucionar problemas de integridade de recursos do SQL Server &#40;Utilitário do SQL Server&#41;](../relational-databases/manage/troubleshoot-sql-server-resource-health-sql-server-utility.md)
