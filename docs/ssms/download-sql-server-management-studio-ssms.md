---
title: Baixar o SQL Server Management Studio (SSMS) | Microsoft Docs
ms.custom: 
ms.date: 10/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- instalar ssms, baixar ssms, ssms mais recentes
- SQL Server Management Studio
- ssms.exe
- sql man studio
- sql management studio
- "instalação do SQL management studio"
- baixar o sql management studio
- ms sql management studio
- instalar o sql management studio
- ssms download
- sql server ssms
- ssms express
ms.assetid: adafeeef-4255-4924-8042-02f503d599ca
caps.latest.revision: 145
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.translationtype: HT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: be3d22491e1cf5e6446f9ac597d613e1d203a28e
ms.contentlocale: pt-br
ms.lasthandoff: 10/10/2017

---
# <a name="download-sql-server-management-studio-ssms"></a>Baixar o SQL Server Management Studio (SSMS)

O SSMS é um ambiente integrado para gerenciar qualquer infraestrutura de SQL, do SQL Server para o Banco de Dados SQL do Microsoft Azure. O SSMS fornece ferramentas para configurar, monitorar e administrar instâncias do SQL. Use o SSMS para implantar, monitorar e atualizar os componentes da camada de dados usados pelos seus aplicativos, além de construir consultas e scripts.

Use o SQL Server Management Studio (SSMS) para consultar, criar e gerenciar seus bancos de dados e data warehouses, independentemente de onde estiverem – no computador local ou na nuvem.

**O SSMS é gratuito!**

O SSMS 17.X é a última geração do *SQL Server Management Studio* e é compatível com o SQL Server 2017.

**[![download](../ssdt/media/download.png) Baixar o SQL Server Management Studio 17.3](https://go.microsoft.com/fwlink/?linkid=858904)**

**download[ ![](../ssdt/media/download.png) Baixar o Pacote de atualização do SQL Server Management Studio 17.3 (atualiza o 17.x para o 17.3)](https://go.microsoft.com/fwlink/?linkid=858906)**

A instalação do SSMS 17.x não atualiza nem substitui versões do SSMS 16.x ou anteriores. O SSMS 17.x é instalado lado a lado com versões anteriores para que ambas versões estejam disponíveis para uso.
Se um computador contiver instalações lado a lado do SSMS, verifique se você iniciou a versão correta para suas necessidades específicas. A versão mais recente é rotulada *Microsoft SQL Server Management Studio 17* e tem um novo ícone: 
 
   ![SSMS 17.x](media/download-sql-server-management-studio-ssms/version-icons.png)


> [!NOTE]
> O módulo do SQL Server PowerShell agora é uma instalação separada por meio da Galeria do PowerShell.  Para obter mais informações, consulte [Instruções de download](download-sql-server-ps-module.md).

## <a name="sql-server-management-studio"></a>SQL Server Management Studio

**Informações sobre versão**

O número da versão: 17.3

O número de build desta versão: 14.0.17199.0

## <a name="new-in-this-release"></a>Novo nesta versão

O SMS 17.3 é a versão mais recente do SQL Server Management Studio. A geração 17.X do SSMS oferece suporte a quase todas as áreas de recursos do SQL Server 2008 por meio do SQL Server 2017. A Versão 17.x também oferece suporte ao PaaS do SQL Analysis Service.

A versão 17.3 inclui:

- Adição do novo assistente "Importar arquivo simples" para simplificar a experiência de importação de arquivos CSV com uma estrutura inteligente, exigindo a mínima intervenção do usuário ou o mínimo conhecimento especializado do domínio. Para obter detalhes, consulte [Import Flat File to SQL Wizard](../relational-databases/import-export/import-flat-file-wizard.md) (Assistente para Importar arquivo simples no SQL).
- Adição do nó "XEvent Profiler" ao Pesquisador de Objetos. Para obter detalhes, consulte [Use the SSMS XEvent Profiler](../relational-databases/extended-events/use-the-ssms-xe-profiler.md) (Usar o SSMS XEvent Profiler).
- Atualização da filtragem e da categorização de esperas no relatório histórico de esperas do Painel de desempenho.
- Adição da verificação de sintaxe da função “Prever”.
- Adição da verificação de sintaxe das consultas de Gerenciamento de biblioteca externa.
- Adição do suporte SMO para Gerenciamento de biblioteca externa.
- Adição do suporte "Iniciar PowerShell" à janela "Servidores registrados" (requer um novo módulo do SQL PowerShell).
- Sempre ativo: adição do [suporte a roteamento de somente leitura](../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md) para grupos de disponibilidade.
- Adição de uma opção de enviar detalhes do rastreamento para a Janela de Saída para os logons do “Active Directory – suporte universal com MFA” (desativado por padrão, precisa ser ativado nas configurações do usuário em “Ferramentas > Opções > Serviços do Azure > Azure Cloud > Nível de rastreamento da Janela de Saída do ADAL”). 
- Repositório de Consultas: 
  - A interface do usuário do Repositório de Consultas poderá ser acessada mesmo quando o QDS estiver DESATIVADO contanto que o QDS tenha registrado algum dado.
  - Agora a interface do usuário do Repositório de Consultas expõe a categorização de esperas em todos os relatórios existentes. Isso permitirá que os clientes desbloqueiem os cenários das Principais consultas de espera e muitos outros.
- Realização da inclusão dos cabeçalhos dos parâmetros de script opcionais (desativada por padrão; pode ser habilitada nas configurações do usuário em “Ferramentas > Opções > Pesquisador de Objetos do SQL Server > Script > Incluir cabeçalho dos parâmetros de script”) – [Item do Connect 3139199](https://connect.microsoft.com/SQLServer/feedback/details/3139199).
- Marca "RC" removida.

Para obter uma lista completa de alterações, consulte [SQL Server Management Studio – log de alterações (SSMS)](../ssms/sql-server-management-studio-changelog-ssms.md).

Para obter informações sobre a coleta de dados de usuário, consulte [Política de privacidade do SQL Server](http://www.microsoft.com/privacystatement/en-us/SQLServer/Default.aspx).

## <a name="supported-sql-offerings"></a>Ofertas de SQL com suporte

* Esta versão do SSMS funciona com todas as [versões com suporte do SQL Server 2008 – SQL Server 2017](https://support.microsoft.com/lifecycle?C2=1044) e fornece o maior nível de suporte para trabalhar com os recursos de nuvem mais recentes no Banco de Dados SQL do Azure e SQL Data Warehouse do Azure.
* Não há um bloqueio explícito para SQL Server 2000 ou SQL Server 2005, mas alguns recursos podem não funcionar corretamente.
* Além disso, o SSMS 17.X pode ser instalado lado a lado com o SSMS 16.X ou o SSMS do SQL Server 2014 e anteriores.

## <a name="supported-operating-systems"></a>Sistemas Operacionais com suporte
  
Esta versão do SSMS é compatível com as seguintes plataformas de 64 bits quando usada com o service pack mais recente disponível:
- Windows 10 (64 bits)
- Windows 8.1 (64 bits)
- Windows 8 (64 bits)
- Windows 7 (SP1) (64 bits)
- Windows Server 2016 *
- Windows Server 2012 R2 (64 bits)
- Windows Server 2012 (64 bits)
- Windows Server 2008 R2 (64 bits)

\* O SSMS 17.X é baseado no shell do Visual Studio 2015 isolado, que foi lançado antes do Windows Server 2016. A Microsoft leva muito a sério a compatibilidade de aplicativo e garante que os aplicativos já fornecidos continuarão sendo executados nas versões mais recentes do Windows. Para minimizar problemas ao executar o SSMS no Windows Server 2016, verifique se o SSMS tem todas as atualizações mais recentes aplicadas. Se você tiver problemas com o SSMS no Windows Server 2016, contate o suporte. A equipe de suporte determina se o problema é com o SSMS, o Visual Studio ou com a compatibilidade do Windows. Em seguida, a equipe de suporte encaminha o problema à equipe apropriada para obter mais informações.

## <a name="ssms-installation-tips-and-issues"></a>Problemas e dicas de instalação do SSMS

### <a name="minimize-installation-reboots"></a>Minimizar as reinicializações de instalação

* Execute as seguintes ações para reduzir as chances de que a instalação do SSMS exija uma reinicialização no final da instalação:
  * Verifique se você está executando uma versão atualizada do pacote redistribuível do Visual C++ 2013. A versão 12.00.40649.5 (ou superior) é necessária. Apenas a versão x64 é necessária.
  * Verifique se a versão do .NET Framework no computador é a 4.6.1 (ou superior).
  * Feche todas as outras instâncias do Visual Studio que estão abertas no computador.
  * Verifique se todas as atualizações mais recentes do sistema operacional estão instaladas no computador.
  * As ações indicadas geralmente são necessárias uma única vez. Há alguns casos em que uma reinicialização é necessária durante as atualizações adicionais para a mesma versão principal do SSMS. Para obter atualizações secundárias, todos os pré-requisitos do SSMS já estarão instalados no computador.

* Para ver a lista de problemas conhecidos e soluções alternativas, consulte [SQL Server Management Studio – notas de versão](../ssms/sql-server-management-studio-release-notes.md)

## <a name="available-languages"></a>Idiomas disponíveis

> [!NOTE]
> Versões do SSMS não localizadas para o inglês exigem o [pacote de atualização de segurança da base de dados 2862966](https://support.microsoft.com/en-us/kb/2862966) se a instalação for realizada em: Windows 8, Windows 7, Windows Server 2012 e Windows Server 2008 R2.

Esta versão do SSMS pode ser instalada nos seguintes idiomas:

SQL Server Management Studio 17.3:<br>
[Chinês (República Popular da China)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x804) | [Chinês (Taiwan)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x40a)

Pacote de atualização do SQL Server Management Studio 17.3 (atualiza a 17.x para a 17.3):<br>
[Chinês (República Popular da China)](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x804) | [Chinês (Taiwan)](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x40a)

## <a name="release-notes"></a>Notas de Versão

Estes são os problemas e limitações com a versão 17.3:

**SSMS geral**

- A funcionalidade SSMS a seguir não é compatível com a autenticação do Azure AD usando o agente do usuário com MFA:
   - O Orientador de Otimização do Mecanismo de Banco de Dados não é compatível com a autenticação do Azure AD; há um problema conhecido em que a mensagem de erro apresentada ao usuário está um pouco criptografada “Não foi possível carregar o arquivo ou assembly 'Microsoft.IdentityModel.Clients.ActiveDirectory,…" em vez da mensagem esperada “O Orientador de Otimização do Mecanismo de Banco de Dados não é compatível com o Banco de Dados SQL do Microsoft Azure. (DTAClient)”.
- A tentativa de analisar uma consulta nos resultados do DTA resulta em erro: "o objeto deve implementar IConvertible. (mscorlib)".
- *Consultas retornadas* está ausente na lista de relatórios do Repositório de Consultas no Pesquisador de Objetos.
   - Solução alternativa: clique com o botão direito do mouse no nó **Repositório de Consultas** e selecione **Exibir consultas retornadas**.

**IS (Integration Services)**

- O [execution_path] em [catalog]. [event_messagea] não está correto para execuções de pacote no Scale Out. O [Execution_path] começa com "\Package" em vez do nome do objeto do executável do pacote. Ao exibir o relatório de visão geral de execuções de pacote no SSMS, o link do "Caminho de execução" na Visão geral de execução não funciona. A solução alternativa é clicar em "Exibir mensagens” no relatório de visão geral para verificar todas as mensagens do evento.



## <a name="previous-releases"></a>Versões anteriores

[Versões anteriores do SQL Server Management Studio](../ssms/sql-server-management-studio-changelog-ssms.md#previous-ssms-releases)

## <a name="feedback"></a>Comentários

![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [Fórum das Ferramentas de Cliente SQL](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [Registre um problema ou uma sugestão no Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback)

## <a name="see-also"></a>Veja também

- [Tutorial: SQL Server Management Studio](tutorials/tutorial-sql-server-management-studio.md)
- [Documentação do SQL Server Management Studio](sql-server-management-studio-ssms.md)
- [Pacotes de serviço e atualizações adicionais](https://technet.microsoft.com/sqlserver/ff803383.aspx)
- [Baixar o SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)

