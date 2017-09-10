---
title: "Opções de configuração para serviços de aprendizado de máquina avançada | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 11/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8d73fd98-0c61-4a62-94bb-75658195f2a6
caps.latest.revision: 21
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 872acf107d72989b4623a9d5f4ccb85c44d1f2f9
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="advanced-configuration-options-for-machine-learning-services"></a>Opções de configuração para serviços de aprendizado de máquina avançada

Este artigo descreve as alterações feitas após a instalação, para modificar a configuração de execução R e outros serviços associados ao aprendizado de máquina no SQL Server.

Aplica-se a: SQL Server 2016 R Services, SQL Server 2017 serviços de aprendizado de máquina

##  <a name="bkmk_Provisioning"></a>Provisionar contas de usuário máquina aprendizado

Script externo processa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executado no contexto de contas de usuário local de baixo privilégio. Esses processos em execução em contas individuais de baixo privilégio tem os seguintes benefícios:

+ Reduz os privilégios dos processos de tempo de execução do script externo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] computador
+ Fornece isolamento entre as sessões de um tempo de execução externo, como R ou Python.

Como parte da instalação, uma nova janela de *pool de conta de usuário* é criado que contém as contas de usuário local necessárias para executar o processo de tempo de execução de R. Você pode modificar o número de usuários, se necessário, para dar suporte a R. O administrador de banco de dados também deve fornecer a esse grupo permissão para se conectar a qualquer instância em que os serviços de R foram habilitados. Para saber mais, confira [Modify the User Account Pool for SQL Server R Services](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md).

No entanto, uma ACL (lista de controle de acesso) pode ser definida em recursos confidenciais no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para negar acesso a esse grupo para evitar que o processo de tempo de execução de R obtenha acesso aos recursos.

+ O pool de conta de usuário está vinculado a uma instância específica.  Para cada instância em que o script R foi habilitado, um pool separado de contas de trabalho é criado. Contas não podem ser compartilhadas entre instâncias.

+ Nomes de conta de usuário no pool estão no formato SQLInstanceName*nn*. Por exemplo, se você estiver usando a instância padrão de seu servidor R, o pool de contas de usuário oferece suporte a nomes de conta como MSSQLSERVER01, MSSQLSERVER02 e assim por diante.

+ O tamanho do pool de conta de usuário é estático e o valor padrão é 20. O número de sessões de tempo de execução de R que podem ser iniciadas simultaneamente é limitado pelo tamanho desse pool de conta de usuário. No entanto, esse limite pode ser alterado por um administrador usando o SQL Server Configuration Manager.

Para saber mais sobre como fazer alterações para o pool de contas de usuário, veja [Modify the User Account Pool for SQL Server R Services](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md).

##  <a name="bkmk_ManagingMemory"></a>Gerenciar a memória usada pelos processos de Script externo

Por padrão, os processos de tempo de execução de R associados a [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] está limitado a usar não mais do que 20% da memória total do computador. No entanto, esse limite pode ser aumentado pelo administrador, se isso for necessário.

Geralmente, esse valor será inadequado para tarefas de R graves como modelo de treinamento ou para prever em várias linhas de dados. Talvez você precise reduzir a quantidade de memória reservada para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (ou para outros serviços) e usar o Resource Governor para definir um pool de recursos externos ou pools e alocar. Para obter mais informações, consulte [governança de recursos para R](../../advanced-analytics/r/resource-governance-for-r-services.md).

##  <a name="bkmk_ChangingConfig"></a>Alterar opções de serviço avançadas usando o arquivo de configuração

Você pode controlar algumas propriedades avançadas de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] editando o arquivo de configuração do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Esse arquivo é criado durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e por padrão é salvo como um arquivo de texto sem formatação no seguinte local:

`<instance path>\binn\rlauncher.config`

Você deve ser um administrador no computador que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para fazer alterações nesse arquivo. Se você editar o arquivo, é recomendável que você faça uma cópia de backup antes de salvar as alterações.

Por exemplo, para usar o bloco de notas para abrir o arquivo de configuração para a instância padrão, você abrir um prompt de comando como administrador e digite o seguinte comando:

```
C:\>Notepad.exe "%programfiles%\Microsoft SQL Server\MSSQL13.MSSQLSERVER\mssql\binn\rlauncher.config"  
```

##  <a name="bkmk_properties"></a>Editar propriedades de configuração

A tabela a seguir lista cada uma das configurações com suporte para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], com os valores permitidos.

Todas as configurações assumem a forma de um par chave-valor, com cada configuração em uma linha separada. Por exemplo, essa propriedade especifica o nível de rastreamento para RLauncher:

Padrão: TRACE_LEVEL = 4


|**Nome da configuração**|**Tipo de valor**|**Default**|**Descrição**|
|------------------|----------------|-------------|-----------------|
|JOB_CLEANUP_ON_EXIT|Integer<br /><br /> 0 = Desabilitado<br /><br /> 1 = Habilitado|1<br /><br /> Arquivos de log são removidos ao sair|Especifica se a pasta de trabalho temporária criada para cada sessão R deve ser limpa após a sessão de R. Essa configuração é útil para depuração.<br /><br /> Observação: Esta é uma configuração interna apenas, não altere esse valor.|
|TRACE_LEVEL|Integer<br /><br /> 1 = Erro<br /><br /> 2 = Desempenho<br /><br /> 3 = Aviso<br /><br /> 4 = Informações|1<br /><br /> Somente os avisos de saída|Configura o nível de detalhamento do rastreamento do iniciador do R (MSSQLLAUNCHPAD) para fins de depuração. Esta configuração afeta o detalhamento dos rastreamentos armazenados nos seguintes arquivos de rastreamento, que estão localizados no caminho especificado pela configuração LOG_DIRECTORY:<br /><br /> **rlauncher.log**: o arquivo de rastreamento gerado para sessões de R iniciadas por consultas do T-SQL.<br /><br /> |

## <a name="bkmk_Launchpad"></a>Modificar a conta de serviço do Launchpad

Um separado [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] serviço é criado para cada instância em que você configurou a serviços de aprendizado de máquina.

Por padrão, o Launchpad é configurado para ser executado usando a conta, NT Service\MSSQLLaunchpad, que é configurada com todas as permissões necessárias para executar scripts R. No entanto, se você alterar essa conta, a barra inicial não poderá iniciar ou acessar a instância do SQL Server em que os scripts externos devem ser executados.

Se você modificar a conta de serviço, certifique-se de usar o aplicativo **Política de segurança local** e atualizar as permissões em cada conta de serviço para incluir essas permissões:

+ Ajustar cotas de memória para um processo (SeIncreaseQuotaPrivilege)
+ Ignorar verificação completa (SeChangeNotifyPrivilege)
+ Fazer logon como um serviço (SeServiceLogonRight)
+ Substituir um token de nível de processo (SeAssignPrimaryTokenPrivilege)

Para obter mais informações sobre as permissões necessárias para executar serviços SQL Server, consulte [Configurar contas de serviço e permissões do Windows](https://msdn.microsoft.com/library/ms143504.aspx#Windows).

## <a name="see-also"></a>Consulte também

[Considerações sobre segurança](security-considerations-for-the-r-runtime-in-sql-server.md)
