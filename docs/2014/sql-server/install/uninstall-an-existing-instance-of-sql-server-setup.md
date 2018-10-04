---
title: Desinstalar uma instância existente do SQL Server (configuração) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- removing instances of SQL Server
- uninstalling instances of SQL Server
- removing SQL Server
- instances of SQL Server, uninstalling
- uninstalling SQL Server
ms.assetid: 3c64b29d-61d7-4b86-961c-0de62261c6a1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9961b074839559bca04d1860084d46fd94ce1b70
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48085906"
---
# <a name="uninstall-an-existing-instance-of-sql-server-setup"></a>Desinstalar uma instância existente do SQL Server (Instalação)
  Este artigo descreve como desinstalar uma instância autônoma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Seguindo as etapas deste tópico, você também prepara o sistema para que seja possível reinstalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Para desinstalar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você deve ser um administrador local com permissão para fazer logon como um serviço.  
  
> [!NOTE]  
>  Para desinstalar um cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use a função Remover Nó fornecida na instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para remover cada nó individualmente. Para obter mais informações, consulte [Adicionar ou remover nós em um cluster de failover do SQL Server &#40;Instalação&#41;](../failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)  
  
 Considere as seguintes informações importantes antes de desinstalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Antes de remover componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um computador que tenha a quantidade mínima necessária de memória física, verifique se o tamanho do arquivo de paginação é suficiente. O tamanho do arquivo de paginação deve ser igual a duas vezes a quantidade de memória física. Memória virtual insuficiente pode provocar uma remoção incompleta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Se você tiver várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será desinstalado automaticamente quando a última instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] for desinstalada.  
  
     Se desejar desinstalar todos os componentes do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], você deverá desinstalar manualmente o componente Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em **Programas e Recursos** no **Painel de Controle**.  
  
### <a name="before-you-uninstall"></a>Antes da desinstalação  
  
1.  **Faça backup dos dados.** Embora essa não seja uma etapa necessária, pode haver bancos de dados que você queira salvar em seu estado atual. Você também pode desejar salvar alterações que foram feitas nos bancos de dados do sistema. Se qualquer situação for verdadeira, certifique-se de fazer backup dos dados antes de desinstalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Como alternativa, salve uma cópia de todos os dados e arquivos de log em uma pasta que não seja a pasta do MSSQL. A pasta do MSSQL é excluída durante a desinstalação.  
  
     Os arquivos que você deve salvar incluem os arquivos de banco de dados a seguir:  
  
    -   Master.mdf  
  
    -   Mastlog.ldf  
  
    -   Model.mdf  
  
    -   Modellog.ldf  
  
    -   Msdbdata.mdf  
  
    -   Msdblog.ldf  
  
    -   Mssqlsystemresource.mdf  
  
    -   Mssqlsystemresource.ldf  
  
    -   Tempdb.mdf  
  
    -   Templog.ldf  
  
    -   `ReportServer[$InstanceName]` (Ar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] banco de dados padrão.)  
  
    -   ReportServer[$InstanceName]TempDB (Este é o banco de dados temporário padrão do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .)  
  
2.  **Exclua os grupos de segurança locais.** Antes de desinstalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], exclua os grupos de segurança locais dos componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
3.  **Interrompa todos os** **serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].** É recomendável interromper todos os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de desinstalar os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Conexões ativas podem impedir a desinstalação com êxito.  
  
4.  **Use uma conta que tenha as permissões apropriadas.** Faça logon no servidor usando a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou usando uma conta que tenha permissões equivalentes. Por exemplo, é possível fazer logon no servidor com uma conta que seja membro do grupo Administradores local.  
  
### <a name="to-uninstall-an-instance-of-includessnoversionincludesssnoversion-mdmd"></a>To Uninstall an Instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
1.  Para começar o processo de desinstalação, vá para o **Painel de Controle** e clique em **Programa e Recursos**.  
  
2.  Clique com botão direito **[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]** e selecione **desinstalação**. Clique em **Remover**. Isso inicia o Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     As Regras de Suporte à Instalação são executadas para verificar a configuração do computador. Para continuar, clique em **Avançar**.  
  
3.  Na página Selecionar Instância, use a caixa suspensa para especificar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a ser removida ou especifique a opção para remover somente os recursos compartilhados e as ferramentas de gerenciamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para continuar, clique em **Avançar**.  
  
4.  Na página Selecionar Recursos, especifique os recursos a serem removidos da instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     As regras de remoção são executadas para verificar se a operação pode ser concluída com êxito.  
  
5.  Na página **Pronto para Desinstalar** , examine a lista de componentes e de recursos que serão desinstalados. Clique em **Remover** para começar a desinstalação  
  
6.  Imediatamente após desinstalar a última instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , os outros programas associados com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ainda estarão visíveis na lista de programas em **Programas e Recursos**. No entanto, se você fechar **Programas e Recursos**, na próxima vez que abrir **Programas e Recursos**, ele atualizará a lista de programas, para mostrar apenas o que realmente ainda está instalado.  
  
### <a name="if-the-uninstallation-fails"></a>Em caso de falha na desinstalação  
  
1.  Se o processo de desinstalação não for concluído com êxito, tente corrigir o problema que causou a falha na desinstalação. Os seguintes artigos podem ajudá-lo a compreender a causa da falha na desinstalação:  
  
    -   [Como identificar problemas de instalação do SQL Server 2008 nos arquivos de log de instalação](http://support.microsoft.com/kb/955396/en-us)  
  
    -   [Exibir e ler arquivos de log da Instalação do SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
2.  Se você não conseguir corrigir a causa da falha na desinstalação, entre em contato com o suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Em alguns casos, como a exclusão não intencional de arquivos importantes, talvez seja necessário reinstalar o sistema operacional antes de reinstalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no computador.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e ler arquivos de log da Instalação do SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
