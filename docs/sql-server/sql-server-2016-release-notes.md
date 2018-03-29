---
title: Notas de versão do SQL Server 2016 | Microsoft Docs
ms.date: 03/14/2018
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: ''
ms.component: sql-non-specified
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology:
- server-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- build notes
- release issues
ms.assetid: c64077a2-bec8-4c87-9def-3dbfb1ea1fb6
caps.latest.revision: ''
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 1a6d422098fdacb3a7bc6392b99fe63bb25c2c36
ms.sourcegitcommit: 6e16d1616985d65484c72f5e0f34fb2973f828f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/16/2018
---
# <a name="sql-server-2016-release-notes"></a>Notas de Versão do SQL Server 2016.
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
  Este artigo descreve as limitações e os problemas com as versões do SQL Server 2016, incluindo service packs. Para obter informações sobre as novidades, veja [Novidades no SQL Server 2016](https://docs.microsoft.com/en-us/sql/sql-server/what-s-new-in-sql-server-2016).

> [![Baixar no Centro de Avaliação](../includes/media/download2.png)](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)  Baixar o SQL Server 2016 no **[Centro de Avaliação](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)**
>
> [![Máquina Virtual pequena do Azure](../includes/media/azure-vm.png)](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016sp1standardwindowsserver2016/) Tem uma conta do Azure?  Em seguida, acesse **[aqui](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016sp1standardwindowsserver2016/)** para criar uma Máquina Virtual com o SQL Server 2016 SP1 já está instalado.
>
> [![Baixar o SSMS](../includes/media/download2.png)](../ssms/download-sql-server-management-studio-ssms.md) Para obter a versão mais recente do SQL Server Management Studio, veja **[Baixar o SSMS (SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md)**.

## <a name="bkmk_2016sp1"></a>SQL Server 2016 Service Pack 1 (SP1)
![info_tip](../sql-server/media/info-tip.png) O SQL Server 2016 SP1 inclui todas as correções até o SQL Server 2016 RTM Atualização Cumulativa 3, incluindo a Atualização de Segurança MS16-136. Ele contém um rollup de soluções fornecidas nas atualizações cumulativas do SQL Server 2016 até, e incluindo, a atualização cumulativa mais recente, CU3, e a Atualização de Segurança MS16-136 lançada em 8 de novembro de 2016. 

Os seguintes recursos estão disponíveis nas edições Standard, Web, Express e Local DB do SQL Server SP1 (salvo indicação em contrário):
- Always encrypted
- Captura de dados alterados (não disponível no Express)
- columnstore
- Compactação
- Mascaramento de dados dinâmicos
- Auditoria refinada
- OLTP in-memory (não disponível no Local DB)
- Vários contêineres de fluxo de arquivos (não disponíveis no banco de dados Local)
- Particionamento
- Polybase
- Segurança em nível de linha

A tabela a seguir resume as principais melhorias fornecidas no SQL Server 2016 SP1.

|Recurso|Description|Para obter mais informações|
|---|---|---|
|Inserção em massa em heaps com TABLOCK automático em TF 715| O Sinalizador de Rastreamento 715 habilita o bloqueio de tabela para operações de carregamento em massa em um heap sem índices não clusterizados.|[Migrar cargas de trabalho do SAP para o SQL Server ficou 2,5 x mais rápido](https://blogs.msdn.microsoft.com/sql_server_team/migrating-sap-workloads-to-sql-server-just-got-2-5x-faster/)|
|CREATE OR ALTER|Implante objetos, como procedimentos armazenados, disparadores, funções definidas pelo usuário e modos de exibição.|[Blog do Mecanismo de Banco de Dados do SQL Server](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/11/17/create-or-alter-another-great-language-enhancement-in-sql-server-2016-sp1/)|
|Suporte a DROP TABLE para replicação|Suporte a DROP TABLE DDL para replicação a fim de permitir que os artigos de replicação sejam removidos.|[KB 3170123](https://support.microsoft.com/help/3170123/supports-drop-table-ddl-for-articles-that-are-included-in-transactiona)|
|Assinatura do driver Filestream RsFx|O driver Filestream RsFx é assinado e certificado usando o portal do Painel da Central do Desenvolvedor para Hardware do Windows (Portal de desenvolvimento) permitindo que o driver do Filestream RsFx para SQL Server 2016 SP1 seja instalado no Windows Server 2016/Windows 10 sem nenhum problema.|[Migrar cargas de trabalho do SAP para o SQL Server ficou 2,5 x mais rápido](https://blogs.msdn.microsoft.com/sql_server_team/migrating-sap-workloads-to-sql-server-just-got-2-5x-faster/)|
|LPIM para conta de serviço do SQL – identificação programática|Permite que os DBAs identifiquem programaticamente se o privilégio de LPIM (Bloquear páginas na memória) está em vigor no momento da inicialização do serviço.|[Escolha dos desenvolvedores: identificar programaticamente privilégios LPIM e IFI no SQL Server](https://blogs.msdn.microsoft.com/sql_server_team/developers-choice-programmatically-identify-lpim-and-ifi-privileges-in-sql-server)|
|Limpeza do controle de alterações manual|O novo procedimento armazenado limpa a tabela interna de controle de alterações sob demanda.| [KB 3173157](https://support.microsoft.com/help/3173157/adds-a-stored-procedure-for-the-manual-cleanup-of-the-change-tracking)|
|Alterações do INSERT..SELECT paralelo para tabelas temporárias locais|Novo INSERT paralelo em operações INSERT..SELECT.|[Equipe de consultoria do cliente do SQL Server](https://blogs.msdn.microsoft.com/sqlcat/2016/07/21/real-world-parallel-insert-what-else-you-need-to-know/)|
|Showplan XML|Diagnóstico estendido, incluindo o aviso de concessão e memória máxima habilitada para uma consulta, sinalizadores de rastreamento habilitados e também resulta em outras informações de diagnóstico. | [KB 3190761](https://support.microsoft.com/help/3190761/update-to-improve-diagnostics-by-expose-data-type-of-the-parameters-fo)|
|Memória de classe de armazenamento|Aumente o processamento de transações usando a memória de classe de armazenamento no Windows Server 2016, resultando na capacidade de acelerar as horas de confirmação de transação por ordem de grandeza.|[Blog do Mecanismo de Banco de Dados do SQL Server](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/12/02/transaction-commit-latency-acceleration-using-storage-class-memory-in-windows-server-2016sql-server-2016-sp1/)|
|USE HINT|Use a opção de consulta `OPTION(USE HINT('<option>'))` para alterar o comportamento do otimizador de consultas usando dicas de nível de consulta compatíveis. Diferentemente do QUERYTRACEON, a opção USE HINT não requer privilégios de administrador do sistema.|[Escolha dos desenvolvedores: dicas de consulta USE HINT](https://blogs.msdn.microsoft.com/sql_server_team/developers-choice-use-hint-query-hints/)|
|Adições de XEvent|Novos recursos de diagnóstico de XEvents e Perfmon melhoram a solução de problemas de latência.|[Eventos estendidos](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)|

Além disso, observe as seguintes correções:
- Com base nos comentários da comunidade do SQL e de DBAs, a partir do SQL 2016 SP1, as mensagens de registro em log do Hekaton são reduzidas ao mínimo.
- Veja os novos [sinalizadores de rastreamento](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql).
- As versões completas dos bancos de dados de exemplo WideWorldImporters agora funcionam com a Standard Edition e a Express Edition, a partir do SQL Server 2016 SP1, e estão disponíveis no [Github]( https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0). Nenhuma alteração é necessária no exemplo. Os backups de banco de dados criados no RTM para o trabalho do Enterprise edition com Standard e Express no SP1. 

A instalação do SQL Server 2016 SP1 pode exigir a reinicialização após a instalação. Como prática recomendada, é melhor planejar e executar uma reinicialização após a instalação do SQL Server 2016 SP1.

### <a name="download-pages-and-more-information"></a>Páginas de download e mais informações

- [Baixar o Service Pack 1 para Microsoft SQL Server 2016](https://www.microsoft.com/download/details.aspx?id=54276)
- [SQL Server 2016 Service Pack 1 (SP1) lançado](https://blogs.msdn.microsoft.com/sqlreleaseservices/sql-server-2016-service-pack-1-sp1-released/)
- [Informações de versão do SQL Server 2016 Service Pack 1](https://support.microsoft.com/kb/3182545)
- ![info_tip](../sql-server/media/info-tip.png) Visite o [Centro de Atualização do SQL Server](https://msdn.microsoft.com/library/ff803383.aspx) para obter links e informações para todas as versões compatíveis, incluindo service packs do [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 

##  <a name="bkmk_2016_ga"></a> SQL Server 2016 Release - General Availability (GA)
-   [Mecanismo de Banco de Dados (GA)](#bkmk_ga_instalpatch) 
-   [Stretch Database (GA)](#bkmk_ga_stretch)
-   [Repositório de Consultas (GA)](#bkmk_ga_query_store)
-   [Documentação do produto (GA)](#bkmk_ga_docs)
 
### ![repl_icon_warn](../database-engine/availability-groups/windows/media/repl-icon-warn.gif) <a name="bkmk_ga_instalpatch"></a> Install Patch Requirement (GA) 
**Problema e impacto sobre o cliente:** a Microsoft identificou um problema que afeta os binários do Tempo de Execução Microsoft VC++ 2013 que são instalados como um pré-requisito pelo SQL Server 2016. Uma atualização está disponível para correção deste problema. Se essa atualização para os binários do Tempo de Execução de VC não for instalada, o SQL Server 2016 poderá apresentar problemas de estabilidade em determinados cenários. Antes de instalar o SQL Server 2016, verifique se o computador precisa do patch descrito em [KB 3164398](http://support.microsoft.com/kb/3164398). O patch também é incluído no [CU1 (Pacote de Atualização Cumulativa 1) para o SQL Server 2016 RTM](https://www.microsoft.com/download/details.aspx?id=53338). 

**Resolução:** use uma das seguintes soluções:

- Instale a [KB 3138367 – Atualização para o Visual C++ 2013 e o Pacote Redistribuível do Visual C++](http://support.microsoft.com/kb/3138367). A KB é a resolução preferencial. Você pode instalá-la antes ou depois de instalar o SQL Server 2016. 

    Se o SQL Server 2016 já estiver instalado, siga as seguintes etapas na ordem:

    1.  Baixe o *vcredist_\*exe* apropriado.
    1.  Interrompa todas as instâncias do mecanismo de banco de dados no serviço do SQL Server.
    1.  Instale a **KB 3138367**.
    1.  Reinicialize o computador.
 

 - Instalar a  [KB 3164398 – Atualização crítica para os pré-requisitos MSVCRT do SQL Server 2016](http://support.microsoft.com/kb/3164398).  
 
    Se você usar a **KB 3164398**, é possível instalá-la durante a instalação do SQL Server, por meio do Microsoft Update ou no Centro de Download da Microsoft. 

    - **Durante a instalação do SQL Server 2016:** se o computador que está executando a instalação do SQL Server tiver acesso à Internet, a instalação do SQL Server verificará a atualização como parte da instalação geral do SQL Server. Se você aceitar a atualização, a instalação baixará e atualizará os binários durante a instalação.

    - **Microsoft Update:** a atualização está disponível no Microsoft Update como uma atualização crítica não relacionada à segurança do SQL Server 2016. A instalação por meio do Microsoft Update, após o SQL Server 2016, exige a reinicialização do servidor após a atualização. 

    - **Centro de Download:** finalmente, a atualização está disponível no Centro de Download da Microsoft. Você pode baixar o software da atualização e instalá-lo nos servidores depois que tiverem o SQL Server 2016. 


### <a name="bkmk_ga_stretch"></a>Stretch Database

#### <a name="problem-with-a-specific-character-in-a-database-or-table-name"></a>Problema com um caractere específico em um nome de banco de dados ou de tabela

**Problema e impacto sobre o cliente:** a tentativa de habilitar o Stretch Database em um banco de dados ou uma tabela falha com um erro. O problema ocorre quando o nome do objeto inclui um caractere que é tratado como um caractere diferente quando convertido de letras minúsculas em maiúsculas. Um exemplo de um caractere que causa esse problema é o caractere “ƒ” (criado ao digitar ALT+159).

**Solução alternativa:** se você deseja habilitar o Stretch Database no banco de dados ou na tabela, a única opção é renomear o objeto e remover o caractere problemático.

#### <a name="problem-with-an-index-that-uses-the-include-keyword"></a>Problema com um índice que usa a palavra-chave INCLUDE

**Problema e impacto sobre o cliente:** a tentativa de habilitar o Stretch Database em uma tabela que contém um índice que usa a palavra-chave INCLUDE para incluir colunas adicionais no índice falha com um erro.

**Solução alternativa:** remova o índice que usa a palavra-chave INCLUDE, habilite o Stretch Database na tabela e recrie o índice. Se você fizer isso, lembre-se de seguir as práticas e políticas de manutenção de sua organização para garantir um impacto mínimo ou nenhum impacto sobre os usuários da tabela afetada.

### <a name="bkmk_ga_query_store"></a>Query Store

#### <a name="problem-with-automatic-data-cleanup-on-editions-other-than-enterprise-and-developer"></a>Problema com a limpeza automática de dados em edições que não sejam Enterprise e Developer

 **Problema e impacto sobre o cliente:** a limpeza automática de dados falha em edições que não sejam o Enterprise e o Developer. Consequentemente, se os dados não forem limpos manualmente o espaço usado pelo Repositório de Consultas aumentará ao longo do tempo até que seja atingido o limite configurado. Se não for atenuado, esse problema também preencherá o espaço em disco alocado para os logs de erros, pois cada tentativa de executar a limpeza produzirá um arquivo de despejo. O período de ativação da limpeza depende da frequência da carga de trabalho, não sendo mais longo do que 15 minutos.

 **Solução alternativa:** se você planeja usar o Repositório de Consultas em edições que não sejam o Enterprise e o Developer, será necessário desativar explicitamente as políticas de limpeza. Faça isto no SQL Server Management Studio (página Propriedades do banco de dados) ou por meio do script Transact-SQL:

```ALTER DATABASE <database name> SET QUERY_STORE (OPERATION_MODE = READ_WRITE, CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 0), SIZE_BASED_CLEANUP_MODE = OFF)```

Além disso, considere as opções de limpeza manual para impedir que o Repositório de Consultas faça a transição para o modo somente leitura. Por exemplo, execute a seguinte consulta para limpar periodicamente o espaço inteiro de dados:

```ALTER DATABASE <database name> SET QUERY_STORE CLEAR```

Além disso, execute os seguintes procedimentos armazenados do Repositório de Consultas periodicamente para limpar estatísticas de tempo de execução, consultas ou planos específicos:

- `sp_query_store_reset_exec_stats`

- `sp_query_store_remove_plan`

- `sp_query_store_remove_query`


###  <a name="bkmk_ga_docs"></a> Documentação do produto (GA) 
 **Problema e impacto sobre o cliente:** ainda não há uma versão da documentação do SQL Server 2016 disponível para download. Quando você usa o Gerenciador da Biblioteca da Ajuda para tentar **Instalar o conteúdo online**, a documentação do SQL Server 2012 e do SQL Server 2014 é exibida, mas não existem opções para a documentação do SQL Server 2016.    
    
 **Solução alternativa:** use uma das seguintes soluções alternativas:    
    
 ![Gerenciar configurações da ajuda do SQL Server](../sql-server/media/docs-sql2016-managehelpsettings.png "Gerenciar configurações da ajuda do SQL Server")    
    
-   Use a opção **Escolher ajuda online ou local** e configure a Ajuda para "Eu quero usar a ajuda online".    
    
-   Use a opção **Instalar conteúdo online** e baixe o conteúdo do SQL Server 2014.    
    
 **Ajuda F1:** por design, quando você pressiona F1 no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], a versão online do artigo da Ajuda F1 é exibida no navegador. O problema está na ajuda baseada em navegador, mesmo quando você configurou e instalou a Ajuda local. 
     
**Atualização do conteúdo:**    
No SQL Server Management Studio e no Visual Studio, o aplicativo Help Viewer poderá congelar (parar de responder) durante o processo de adição da documentação. Para resolver esse problema, conclua as etapas a seguir. Para obter mais informações sobre esse problema, confira [O Visual Studio Help Viewer congela](https://msdn.microsoft.com/library/mt654096.aspx).    
    
* Abra o arquivo %LOCALAPPDATA%\Microsoft\HelpViewer2.2\HlpViewer_SSMS16_en-US.settings | HlpViewer_VisualStudio14_en-US.settings no Bloco de Notas e altere a data no código a seguir para alguma data no futuro.    
    
     
```    
     Cache LastRefreshed="12/31/2017 00:00:00"    
``` 

## <a name="additional-information"></a>Informações adicionais
+ [Instalação do SQL Server 2016](../database-engine/install-windows/installation-for-sql-server-2016.md)
+ [Centro de atualização do SQL Server – links e informações para todas as versões com suporte](https://msdn.microsoft.com/library/ff803383.aspx)


[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]    

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png "MS_Logo_X-Small")    
