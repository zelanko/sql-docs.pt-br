---
title: Baixar o SQL Server Management Studio (SSMS) | Microsoft Docs
ms.custom: 
ms.date: 08/07/2017
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
ms.translationtype: HT
ms.sourcegitcommit: 3f12671ace99d5fefc199c7b1c2db31e5b3cfade
ms.openlocfilehash: a689293fadb1a442f94d88cc06a9e7a4ef06650f
ms.contentlocale: pt-br
ms.lasthandoff: 08/08/2017

---
# <a name="download-sql-server-management-studio-ssms"></a>Baixar o SQL Server Management Studio (SSMS)

O SSMS é um ambiente integrado para gerenciar qualquer infraestrutura de SQL, do SQL Server para o Banco de Dados SQL do Microsoft Azure. O SSMS fornece ferramentas para configurar, monitorar e administrar instâncias do SQL. Use o SSMS para implantar, monitorar e atualizar os componentes da camada de dados usados pelos seus aplicativos, além de construir consultas e scripts.

Use o SQL Server Management Studio (SSMS) para consultar, criar e gerenciar seus bancos de dados e data warehouses, independentemente de onde estiverem – no computador local ou na nuvem.

**O SSMS é gratuito!**

O SSMS 17.X é a última geração do *SQL Server Management Studio* e é compatível com o SQL Server 2017.

**[![download](../ssdt/media/download.png) Baixar o SQL Server Management Studio 17.2](https://go.microsoft.com/fwlink/?linkid=854085)**

**download[ ![](../ssdt/media/download.png) Baixar o Pacote de atualização do SQL Server Management Studio 17.2 (atualiza do 17.x para o 17.2)](https://go.microsoft.com/fwlink/?linkid=854087)**

A instalação do SSMS 17.x não atualiza nem substitui versões do SSMS 16.x ou anteriores. O SSMS 17.x é instalado lado a lado com versões anteriores para que ambas versões estejam disponíveis para uso.
Se um computador contiver instalações lado a lado do SSMS, verifique se você iniciou a versão correta para suas necessidades específicas. A versão mais recente é rotulada *Microsoft SQL Server Management Studio 17* e tem um novo ícone: 
 
   ![SSMS 17.x](media/download-sql-server-management-studio-ssms/version-icons.png)


> [!NOTE]
> O módulo do SQL Server PowerShell agora é uma instalação separada por meio da Galeria do PowerShell.  Para obter mais informações, consulte [Instruções de download](download-sql-server-ps-module.md).

## <a name="sql-server-management-studio"></a>SQL Server Management Studio

**Informações sobre versão**

O número de versão 17.2 O número de build para essa versão: 14.0.17177.0

## <a name="new-in-this-release"></a>Novo nesta versão

O SMS 17.2 é a versão mais recente do SQL Server Management Studio. A geração 17.X do SSMS oferece suporte a quase todas as áreas de recursos do SQL Server 2008 por meio do SQL Server 2017. A Versão 17.x também oferece suporte ao PaaS do SQL Analysis Service.

A versão 17.2 inclui:

- MFA (Autenticação Multifator do Microsoft Azure)
  - Autenticação de vários usuários do Azure AD para Autenticação universal com Autenticação Multifator do Microsoft Azure (UA com MFA)
  - Foi adicionado um novo campo de entrada de credenciais do usuário para autenticação Universal com MFA para oferecer suporte à autenticação de vários usuários.
- A caixa de diálogo de conexão agora oferece suporte aos 5 seguintes métodos de autenticação:
  - Autenticação do Windows
  - Autenticação do SQL Server
  - Active Directory – Universal com suporte à MFA
  - Active Directory – Senha
  - Active Directory – Integrado

- A exportação/importação do banco de dados para o assistente de DacFx agora pode usar a Autenticação universal com MFA.
- Para suporte de API, consulte a [Interface IUniversalAuthProvider](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx).
- Biblioteca ADAL gerenciada usada pela Autenticação universal do Azure AD com MFA foi atualizada para a versão 3.13.9.
- Uma nova interface de CLI com suporte para a configuração de administrador do Azure AD para o banco de dados SQL e SQL Data Warehouse.

 Para obter mais informações sobre os métodos de autenticação do Active Directory, consulte [Autenticação universal com o banco de dados SQL e SQL Data Warehouse (suporte de SSMS para MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication) e [configure a autenticação multifator do Banco de Dados SQL do Azure para SQL Server Management Studio](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication-configure).

- A janela de saída tem entradas para consultas executadas durante a expansão de nós do Pesquisador de Objetos do SQL Server
- Designer de exibição para os Bancos de dados SQL do Azure habilitado
- As opções de script padrão para gerar scripts de objetos no Pesquisador de Objetos do SQL Server no SSMS foram alteradas:
  - Anteriormente, o padrão em uma nova instalação era que o script gerado utilizava a versão mais recente do SQL Server (atualmente SQL Server 2017).
  - No SSMS 17.2, uma nova opção foi adicionada: *Corresponder configurações de script com a origem*. Quando definido como *True*, o script gerado utiliza a mesma versão, o tipo de mecanismo e edição do mecanismo que o servidor de onde o objeto que está sendo inserido no script veio.
  - O valor de *Corresponder configurações de script com a origem* é definido como *True* por padrão, portanto, novas instalações do SSMS serão automaticamente padronizadas para sempre gerar scripts de objetos com o mesmo destino do servidor original.
  - Quando o valor de *Corresponder configurações de Script com a origem* estiver definido como *False*, as opções de destino do script normal serão habilitadas e funcionarão como antes.
  - Além disso, todas as opções de script foram movidas para sua própria seção – *Opções de versão*. Elas não estão mais em *Opções Gerais de Script*.

- Suporte adicionado para as Nuvens nacionais em "Restaurar de URL"
- Os relatórios do QueryStoreUI agora dão suporte a métricas adicionais (RowCount, DOP, CLR Time etc.) do sys.query_store_runtime_stats.
- Agora há suporte para o IntelliSense para o banco de dados SQL do Azure
    - https://connect.microsoft.com/SQLServer/feedback/details/3100677/ssms-2016-would-be-nice-to-have-intellisense-on-azure-sql-databases
- Segurança: a caixa de diálogo de conexão será padronizada para não confiar em certificados de servidor e solicitar criptografia para conexões de banco de dados SQL do Azure
- Aperfeiçoamentos gerais sobre o suporte do SQL Server no Linux:
 - Nó de Correio do banco de dados está de volta
 - Alguns problemas relacionados aos caminhos corrigidos
 - Melhorias na estabilidade do Monitor de atividade
 - A caixa de diálogo Propriedades da Conexão exibe a plataforma correta
- Relatório de servidor de Painel desempenho agora está disponível como um relatório padrão:
  - Pode se conectar ao SQL Server 2008 e versões mais recentes.
  - O sub-relatório de índices ausentes usa a pontuação para ajudar a identificar os índices mais úteis.
  - O sub-relatório de histórico de estatísticas de espera agora agrega esperas por categoria. Esperas ociosas e suspensas filtradas por padrão.
  - Novo sub-relatório de histórico de travas.
- Pesquisa de nó do plano de execução permite pesquisar nas propriedades do plano. Pesquise facilmente por qualquer propriedade de operador como nome da tabela. Para usar essa opção ao exibir um plano:
  - Clique com o botão direito do mouse no plano e, no menu de contexto, clique na opção Localizar Nó
  - Use CTRL+F

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

SQL Server Management Studio 17.2:<br>
[Chinês (República Popular da China)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x804) | [Chinês (Taiwan)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x40a)

Pacote de atualização do SQL Server Management Studio 17.2 (atualiza do 17.x para o 17.2):<br>
[Chinês (República Popular da China)](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x804) | [Chinês (Taiwan)](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x40a)

## <a name="release-notes"></a>Notas de Versão

Estes são os problemas e limitações com a versão 17.2:

- Janelas de consulta usando a autenticação "Active Directory – Universal com suporte a MFA" podem ter um erro semelhante ao seguinte, ao tentar executar uma consulta depois de estarem abertas por uma hora ou mais:

   `Msg 0, Level 11, State 0, Line 0
The connection is broken and recovery is not possible. The client driver attempted to recover the connection one or more times and all attempts failed. Increase the value of *ConnectRetryCount* to increase the number of recovery attempts.`

   Executar novamente a consulta deve corrigir o erro e ser bem-sucedida.

- Não há suporte para a seguinte funcionalidade do SSMS para o Azure AD usando a Autenticação universal com MFA:
  - O designer **Nova tabela/exibição** mostra o prompt de logon de estilo antigo e não funciona para a autenticação do Azure AD.
  - O recurso **Editar 200 linhas superiores** não dá suporte à autenticação do Azure AD.
  - O componente **Servidor Registrado** não dá suporte à autenticação do Azure AD.
  - Não há suporte para o **Orientador de Otimização do Mecanismo de Banco de Dados** para autenticação do Azure AD. Há um problema conhecido em que a mensagem de erro apresentada ao usuário não é útil: *Não foi possível carregar o arquivo ou assembly 'Microsoft.IdentityModel.Clients.ActiveDirectory,…* em vez da esperada *O Orientador de Otimização do Mecanismo de Banco de Dados não dá suporte ao Banco de Dados SQL do Microsoft Azure. (DTAClient)*.

**AS**

- Pesquisador de Objetos do SQL Server no SSAS não mostrará o nome de usuário de autenticação do Windows nas propriedades de conexão do AS Azure.
Para obter mais informações, consulte o [log de alterações do SSMS](sql-server-management-studio-changelog-ssms.md).

## <a name="previous-releases"></a>Versões anteriores

[Versões anteriores do SQL Server Management Studio](../ssms/sql-server-management-studio-changelog-ssms.md#previous-ssms-releases)

## <a name="feedback"></a>Comentários

![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [Fórum das Ferramentas de Cliente SQL](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [Registre um problema ou uma sugestão no Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback)

## <a name="see-also"></a>Veja também

- [Tutorial: SQL Server Management Studio](tutorials/tutorial-sql-server-management-studio.md)
- [Documentação do SQL Server Management Studio](sql-server-management-studio-ssms.md)
- [Pacotes de serviço e atualizações adicionais](https://technet.microsoft.com/sqlserver/ff803383.aspx)
- [Baixar o SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)

