---
title: Inicialização imediata de arquivo do banco de dados
description: Saiba mais sobre a inicialização instantânea de arquivo e como habilitá-la no banco de dados SQL Server.
ms.custom: contperfq4
ms.date: 07/24/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- initializing files [SQL Server]
- instant file initialization [SQL Server]
- fast file initialization [SQL Server]
- file initialization [SQL Server]
- IFI [SQL Server]
- database instant file initialization [SQL Server]
ms.assetid: 1ad468f5-4f75-480b-aac6-0b01b048bd67
author: stevestein
ms.author: sstein
ms.openlocfilehash: 20b182186244221c0f8cea2dda86d8f6a269cd50
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87246566"
---
# <a name="database-instant-file-initialization"></a>Inicialização imediata de arquivo do banco de dados
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
Neste artigo, você aprende sobre a inicialização instantânea de arquivo e como habilitá-la para acelerar o crescimento de seus arquivos de banco de dados do SQL Server.  

Por padrão, arquivos de dados e de log são inicializados para substituir todos os dados existentes que foram deixados no disco por arquivos excluídos anteriormente. Os arquivos de dados e de log são inicializados pela primeira vez ao anular os arquivos (preenchimento com zeros) quando você executa as seguintes operações:  
  
- Criar um banco de dados.  
- Adicionar dados ou arquivos de log a um banco de dados existente.  
- Aumentar o tamanho de um arquivo existente (inclusive operações de aumento automático).  
- Restaurar um banco de dados ou grupo de arquivos.  

No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a IFI (Inicialização Instantânea de Arquivo) permite uma execução mais rápida das operações de arquivo mencionadas anteriormente, já que ela recupera o espaço em disco usado sem preencher esse espaço com zeros. Em vez disso, o conteúdo do disco é substituído à medida que novos dados são gravados nos arquivos. Arquivos de log não podem ser inicializados de imediato.


## <a name="enable-instant-file-initialization"></a>Habilitar a inicialização instantânea de arquivo

A inicialização instantânea de arquivo estará disponível somente se a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta de inicialização do serviço tiver recebido *SE_MANAGE_VOLUME_NAME*. Os membros do grupo administrador do Windows têm esse direito e podem atribuí-lo a outros usuários adicionando-os à política de segurança **Executar tarefas de manutenção de volume** .  
> [!IMPORTANT]
> O uso de alguns recursos, como o [TDE (Transparent Data Encryption)](../../relational-databases/security/encryption/transparent-data-encryption.md), pode impedir a Inicialização Instantânea de Arquivo.  

> [!NOTE]
> A partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], essa permissão pode ser concedida à conta de serviço no momento da instalação. <br><br>Se estiver usando a [instalação do prompt de comando](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md), adicione o argumento /SQLSVCINSTANTFILEINIT ou marque a caixa *Conceder privilégio Realizar Tarefa de Manutenção de Volume para o Serviço de Mecanismo de Banco de Dados do SQL Server* no [assistente de instalação](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md).
  
Para conceder a permissão `Perform volume maintenance tasks` a uma conta:  
  
1.  No computador em que o arquivo de dados será criado, abra o aplicativo **Política de Segurança Local** (`secpol.msc`).  
  
1.  No painel esquerdo, expanda **Políticas Locais**e, em seguida, clique em **Atribuição de Direitos de Usuário**.  
  
1.  No painel direito, clique duas vezes em **Executar tarefas de manutenção de volume**.  
  
1.  Clique em **Adicionar usuário ou grupo** e adicione a conta que executa o serviço SQL Server.  
  
1.  Clique em **Aplicar**e feche todas as caixas de diálogo **Política de Segurança Local** .  

1. Reinicie o serviço SQL Server.

1. Verifique o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na inicialização.
   
  
    **Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4, [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 e [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posteriores).
    1. Se a conta de inicialização de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiver a concessão de *SE_MANAGE_VOLUME_NAME*, uma mensagem informativa semelhante à seguinte será registrada no log:

        `Database Instant File Initialization: enabled. For security and performance considerations see the topic 'Database Instant File Initialization' in SQL Server Books Online. This is an informational message only. No user action is required.`

    1. Se a conta de inicialização de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **não** tiver a concessão de *SE_MANAGE_VOLUME_NAME*, uma mensagem informativa semelhante à seguinte será registrada no log:

        `Database Instant File Initialization: disabled. For security and performance considerations see the topic 'Database Instant File Initialization' in SQL Server Books Online. This is an informational message only. No user action is required.`
    > [!NOTE]
    > Use também a coluna *instant_file_initialization_enabled* na DMV [sys.dm_server_services](../../relational-databases/system-dynamic-management-views/sys-dm-server-services-transact-sql.md) para identificar se a inicialização instantânea de arquivo está habilitada.

## <a name="security-considerations"></a>Considerações de segurança

É recomendável habilitar a inicialização instantânea de arquivo, pois os benefícios podem superar o risco à segurança.

Ao usar a inicialização instantânea de arquivo, o conteúdo de disco excluído será substituído apenas à medida que novos dados forem gravados nos arquivos. Por esse motivo, o conteúdo excluído poderá ser acessado por uma entidade de segurança não autorizada, até que outros dados sejam gravados naquela área específica do arquivo de dados.

Embora o arquivo de banco de dados esteja associado à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esse risco de divulgação de informações é reduzido pela DACL (lista de controle de acesso discricionário) no arquivo. Essa DACL permite acesso de arquivo somente à conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ao administrador local. Porém, quando o arquivo é desassociado, ele pode ser acessado por um usuário ou serviço que não tenha *SE_MANAGE_VOLUME_NAME*.

Há considerações semelhantes quando:

* *É feito backup do banco de dados.* Se o arquivo de backup não estiver protegido com uma DACL adequada, o conteúdo excluído poderá ficar disponível para um usuário ou um serviço não autorizado.  

* *Um arquivo é expandido usando a IFI*. Um administrador do SQL Server pode, potencialmente, acessar o conteúdo da página bruta e ver o conteúdo excluído anteriormente.

* *Os arquivos do banco de dados são hospedados em uma rede de área de armazenamento*. Também é possível que a rede de área de armazenamento apresente sempre novas páginas como pré-inicializadas e fazer com que o sistema operacional reinicialize as páginas poderá gerar uma sobrecarga desnecessária.

Se houver preocupação com a possível divulgação do conteúdo excluído, você deverá executar uma das seguintes ações ou ambas:  
  
- Sempre se certifique de que todos os arquivos de dados desassociados e arquivos de backup tenham DACL restritivas.  
- Desabilite a inicialização instantânea de arquivo para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].    Para fazer isso, revogue a *SE_MANAGE_VOLUME_NAME* da conta de inicialização do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
    
    > [!NOTE]
    > Desabilitar aumentará os tempos de alocação para arquivos de dados e afetará apenas os arquivos que forem criados ou aumentados em tamanho após o direito do usuário ser revogado.
  
### <a name="se_manage_volume_name-user-right"></a>Direito do usuário SE_MANAGE_VOLUME_NAME

O privilégio do usuário *SE_MANAGE_VOLUME_NAME* pode ser atribuído nas **Ferramentas Administrativas do Windows**, miniaplicativo de **Política de Segurança Local**. Em **Políticas Locais**, selecione **Atribuição de Direito do Usuário** e modifique a propriedade **Executar tarefas de manutenção de volume**.

## <a name="performance-considerations"></a>Considerações sobre o desempenho

O processo de inicialização do arquivo de banco de dados grava zeros nas novas regiões do arquivo em inicialização. A duração desse processo depende do tamanho da parte do arquivo que é inicializada e do tempo de resposta e da capacidade do sistema de armazenamento. Se a inicialização demorar muito tempo, as mensagens a seguir poderão ser registradas no log de erros do SQL Server e no Log do Aplicativo.

```
Msg 5144
Autogrow of file '%.*ls' in database '%.*ls' was cancelled by user or timed out after %d milliseconds.  Use ALTER DATABASE to set a smaller FILEGROWTH value for this file or to explicitly set a new file size.
```

```
Msg 5145
Autogrow of file '%.*ls' in database '%.*ls' took %d milliseconds.  Consider using ALTER DATABASE to set a smaller FILEGROWTH for this file.
```

O longo aumento automático de um banco de dados e/ou de um arquivo de log de transações poderá causar problemas de desempenho de consulta. Isso ocorre porque uma operação que requer o aumento automático de um arquivo será mantida com recursos do tipo bloqueio ou trava durante a operação de aumento do arquivo. Podem ocorrer longas esperas nas travas para as páginas de alocação. A operação que exige o longo aumento automático mostrará um tipo de espera igual a PREEMPTIVE_OS_WRITEFILEGATHER.





## <a name="see-also"></a>Consulte Também  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)
