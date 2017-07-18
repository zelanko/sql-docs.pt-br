---
title: "Versões anteriores do SQL Server Management Studio | Microsoft Docs"
ms.custom: 
ms.date: 07/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 87f593c3-8b76-4c12-963a-31d35f2fb294
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: dd279b20fdf0f42d4b44843244aeaf6f19f04718
ms.openlocfilehash: f55f56b31aec2e094a35200e6fe08b28c93affb0
ms.contentlocale: pt-br
ms.lasthandoff: 07/14/2017

---
# <a name="previous-sql-server-management-studio-releases"></a>Versões anteriores do SQL Server Management Studio
  
As seguintes versões anteriores do SQL Server Management Studio estão disponíveis.

## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-170-releasehttpgomicrosoftcomfwlinklinkid847722"></a>![baixar](../ssdt/media/download.png) [SQL Server Management Studio versão 17.0](http://go.microsoft.com/fwlink/?LinkID=847722)

**Informações sobre versão**  
  
*Esta versão do SSMS usa o shell isolado do Visual Studio 2015.*  
O número da versão: 17.0  
O número de build desta versão: 14.0.17099.0

## <a name="changelog"></a>Log de alteração  

Confira [17.0](sql-server-management-studio-changelog-ssms.md#ssms-170-release).

   
## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-1653-releasehttpgomicrosoftcomfwlinklinkid840946"></a>![baixar](../ssdt/media/download.png) [versão do SQL Server Management Studio 16.5.3](http://go.microsoft.com/fwlink/?LinkID=840946)

**Informações sobre versão**  
  
*Esta versão do SSMS usa o shell isolado do Visual Studio 2015.*  
O número de versão: 16.5.3  
O número de build para esta versão: 13.0.16106.4

## <a name="changelog"></a>Log de alteração  

16.5.3

Os seguintes problemas foram corrigidos nesta versão:

* Corrigido um problema introduzido no SSMS 16.5.2 que estava causando a expansão do nó 'Table' quando a tabela tinha mais de uma coluna esparsa.

* Os usuários podem implantar pacotes do SSIS contendo o Gerenciador de Conexões do OData, que se conectam a um recurso do Microsoft Dynamics AX/CRM Online para o catálogo do SSIS. Para obter mais informações, consulte [Gerenciador de Conexões do OData](https://msdn.microsoft.com/library/dn584133.aspx).

* Configurar Always Encrypted para uma tabela existente falha com erros em objetos não relacionados. [ID de Conexão 3103181](https://connect.microsoft.com/SQLServer/feedback/details/3103181/setting-up-always-encrypted-on-an-existing-table-fails-with-errors-on-unrelated-objects)

* Configurar Always Encrypted para um banco de dados com vários esquemas não funciona. [ID de Conexão 3109591](https://connect.microsoft.com/SQLServer/feedback/details/3109591/sql-server-2016-always-encrypted-against-existing-database-with-multiple-schemas-doesnt-work)

* O assistente de coluna Always Encrypted, Encrypted falha devido a banco de dados contendo exibições que referenciam exibições de sistema. [ID de Conexão 3111925](https://connect.microsoft.com/SQLServer/feedback/details/3111925/sql-server-2016-always-encrypted-encrypted-column-wizard-failed-task-failed-due-to-following-error-cannot-save-package-to-file-the-model-has-build-blocking-errors)

* Ao criptografar usando Always Encrypted, erros de atualização de módulos após a criptografia são manipulados incorretamente.

* O menu *Abrir recente* não mostra arquivos salvos recentemente. [ID de Conexão 3113288](https://connect.microsoft.com/SQLServer/feedback/details/3113288/ssms-2016-open-recent-menu-doesnt-show-recently-saved-files)

* O SSMS está lento ao clicar com o botão direito do mouse em um índice para uma tabela (mais de uma conexão remota (Internet)). [ID de Conexão 3114074](https://connect.microsoft.com/SQLServer/feedback/details/3114074/ssms-slow-when-right-clicking-an-index-for-a-table-over-a-remote-internet-connection)
 
* Corrigido um problema com a barra de rolagem do Designer do SQL. [ID de Conexão 3114856](http://connect.microsoft.com/SQLServer/feedback/details/3114856/bug-in-scrollbar-on-sql-desginer-in-ssms-2016)

* O menu de contexto para tabelas trava momentaneamente 
 
* Ocasionalmente, o SSMS lança exceções no Monitor de Atividade e falha. [ID de Conexão 697527](https://connect.microsoft.com/SQLServer/feedback/details/697527/)

* O SSMS 2016 falha com o erro "O processo foi terminado devido a um erro interno no Tempo de Execução do .NET no IP 71AF8579 (71AE0000) com código de saída 80131506"



## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-165-releasehttpgomicrosoftcomfwlinklinkid832812"></a>![Baixar](../ssdt/media/download.png) [o SQL Server Management Studio versão 16.5](http://go.microsoft.com/fwlink/?LinkID=832812)

**Informações da versão**  
  
*Esta versão do SSMS usa o shell isolado do Visual Studio 2015.*  
O número de versão: 16.5  
O número de build para esta versão: 13.0.16000.28

**Problemas conhecidos com este build**  

1. Invoke-Sqlcmd erroneamente insere várias linhas quando a verificação de restrição ocorre. [Item do Microsoft Connect: 811560](https://connect.microsoft.com/SQLServer/feedback/details/811560)

2. Versões de idioma de não ENU não funcionam completamente durante a criação de grupos de disponibilidade.

3. Clicar no plano de consulta XML não abre a interface do usuário de SSMS adequada.

**Log de alteração**

* Corrigido um problema em que uma falha pode ocorrer quando um banco de dados com o nome da tabela que contém ";:" foi clicado.
* Corrigido um problema em que as alterações feitas na página de modelo na janela Propriedades do Banco de Dados Tabulares AS utilizariam scripts da definição original. 
[Item nº 3080744 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/3080744) 
* Corrigido o problema em que os arquivos temporários são adicionados à lista de "Arquivos recentes".  
[Item nº 2558789 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2558789)
* Corrigido o problema em que o item de menu "Gerenciar compactação" é desabilitado para os nós de tabela de usuário na árvore do Gerenciador de objetos.  
[Item nº 3104616 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/3104616)

* Corrigido o problema que usuário não é capaz de definir o tamanho da fonte para o Pesquisador de objetos, Gerenciador de servidores registrados, Gerenciador de modelos, bem como detalhes do Pesquisador de objetos. Fonte para os pesquisadores estarão usando a fonte de Ambiente.  
[Item nº 691432 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/691432)

* Corrigido o problema em que o SSMS sempre se reconecta ao banco de dados padrão quando a conexão é perdida.  
[Item nº 3102337 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/3102337)

* Corrigido muitos dos problemas de DPI alta na janela do Gerenciador de Política e Editor de Consulta, incluindo os ícones de plano de execução.

* Corrigido o problema em que a opção de configuração de fonte e cor para Eventos Estendidos está ausente.

* Corrigido o problema de falhas do SSMS que ocorrem no fechamento do aplicativo ou quando está tentando mostrar a caixa de diálogo de erro.


   
## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-1641-september-2016-releasehttpgomicrosoftcomfwlinklinkid828615"></a>![baixar](../ssdt/media/download.png) [SQL Server Management Studio 16.4.1 (Setembro de 2016)](http://go.microsoft.com/fwlink/?LinkID=828615)

**Informações sobre versão**  
  
*Esta versão do SSMS usa o shell isolado do Visual Studio 2015.*  
O número de versão: 16.4.1  
O número de build desta versão: 13.0.15900.1
  
**Problemas conhecidos com este build**  

1. **Apenas uma única conta do Azure Active Directory pode fazer logon em uma instância do SSMS usando a Autenticação Universal do Active Directory.**  
    Essa restrição está limitada à autenticação do Active Directory Universal. Você pode fazer logon em servidores diferentes usando a Autenticação de Senha do Active Directory, a Autenticação Integrada do Active Directory ou a Autenticação do SQL Server.
    
    Como solução alternativa, você pode usar outra instância do SSMS para fazer logon como outra conta do Azure Active Directory. 
    
2. **Os comandos de DacFx (Estrutura de Aplicativo de Camada de Dados) e o Designer de Esquema no SSMS não dão suporte à Autenticação Universal do Active Directory.**  
    Comandos que usam DacFx (por exemplo, importação e exportação) e o designer de esquema no SSMS atualmente não dão suporte à Autenticação Universal do Active Directory.
    
    Como solução alternativa, você pode usar as outras formas de autenticação fornecidas no SSMS: Autenticação de Senha do Active Directory, Autenticação Integrada do Active Directory ou Autenticação do SQL Server.

3. **O SSMS só pode se conectar a instâncias do SSIS 2016 (SQL Server 2016 Integrated Services).**  
    Há uma limitação conhecida de compatibilidade com o SQL Server Integration Services que impede a conexão com versões anteriores.
    
    Como solução alternativa para esse problema, você pode se conectar à instância do SQL Server Integration Service usando a [versão do SSMS alinhada à sua instância do SSIS.](../ssms/previous-sql-server-management-studio-releases.md) 
  
4. **O SSMS não salvará planos de manutenção para o SQL Server 2008 R2 e versões anteriores do SQL Server.**  
    Essa é uma limitação conhecida que esperamos resolver no futuro. Enquanto isso, você pode usar a [versão 2014 do SSMS](../ssms/previous-sql-server-management-studio-releases.md) para salvar os planos de manutenção.  
    
5. **As instalações do SSMS que não estejam em inglês podem exigir a instalação de um pacote de segurança adicional.**  
Versões do SSMS não localizadas para o inglês exigem o [pacote de atualização de segurança da base de dados 2862966](https://support.microsoft.com/en-us/kb/2862966) se a instalação for realizada em: Windows 8, Windows 7, Windows Server 2012 e Windows Server 2008 R2.
  
6. **O SQL Server Configuration Manager não será iniciado se não houver um SQL Server instalado no computador cliente**  
    Se não tiver o SQL Server instalado no computador cliente e iniciar o SQL Server Configuration Manager, você verá o seguinte erro:   
     `Cannot connect to WMI provider. You do not have permission or the server is unreachable. Note that you can only manage SQL Server 2005 and later servers with SQL Server Configuration Manager. Invalid namespace \[0x8004100e]`,   
   
     * Se você tiver adicionado as instâncias do SQL Server à lista 'Servidores Registrados' no SSMS:  
        1. Navegue até o modo de exibição 'Servidores Registrados' no SSMS.  
        2. Clique na instância do SQL Server que você deseja configurar.  
        3. Selecione 'SQL Server Configuration Manager...' no menu de atalho.    
          
      * Se você não tiver adicionado uma instância do SQL Server à lista 'Servidores Registrados' no SSMS:  
        1. Abra um prompt de comando como Administrador.  
        2. Execute a ferramenta Mofcomp usando o seguinte comando:  
    `mofcomp "%programfiles(x86)%\Microsoft SQL Server\130\Shared\sqlmgmproviderxpsp2up.mof"`  
        3. Após executar a ferramenta Mofcomp, execute os seguintes comandos para reiniciar o serviço WMI para que as alterações entrem em vigor:  
        `net stop "Windows Management Instrumentation"`  
        `net start “Windows Management Instrumentation”`  

 
**Log de alteração** 

*  Foi corrigido um problema no qual ocorria falha durante a tentativa de ALTERAR/Modificar um procedimento armazenado:  
[Item nº 3103831 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/3103831)

* Novos 'Read-SqlTableData', 'Read-SqlViewData' e ‘Write-SqlTableData' para exibir e gravar dados usando o PowerShell.  
[Cartão Read-SqlTableData do Trello](https://trello.com/c/FXVUNJ8x/131-read-sqltabledata)  
[Item nº 2685363 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2685363)
    
* Novo cmdlet 'Add-SqlLogin' para habilitar novos cenários de gerenciamento de logon usando o PowerShell.  
[Item nº 2588952 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2588952)
    
*  Suporte aprimorado e facilidade de uso para os usuários se conectarem a várias nuvens nacionais.
    
*  Corrigido um problema em que uma exceção de memória insuficiente estava sendo lançada.  
[Item nº 3062914 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/3062914)  
[Item nº 3074856 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/3074856)
    
*  Corrigido um problema em que a filtragem por esquema não é uma opção de filtro válida.  
[Item nº 3058105 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/3058105)  
[Item nº 3101136 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/3101136)
    
*  Corrigido um problema em que a janela do Monitor de um banco de dados ampliado não estaria acessível.
    
*  Corrigido um problema em que a Ajuda F1 sempre abria conteúdo online. Os usuários agora podem selecionar se preferem ajuda online ou offline por meio do "Definir Preferência de Ajuda" no menu Ajuda.   
[Item nº 2826366 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2826366)
    
*  Corrigido um problema em que um modelo de tabela do Analysis Services de nível 1200 não remove a senha para script, mesmo que a versão do servidor mostre [objeto de modelo do cliente está agora em sincronização antes de criar scripts].
    
*  Corrigido um problema no qual a opção 'SELECIONAR N LINHAS SUPERIORES' gerava uma sintaxe preterido para o operador TOP.  
[Item nº 3065435 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/3065435)
    
*  Diversos problemas de layout corrigidos em todo o SSMS, incluindo a página Propriedades de Logon e Opções Avançadas de Execução de Consulta.   
[Item nº 3058199 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/3058199)  
[Item nº 3079122 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/3058199)  
[Item nº 3071384 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/3071384)
    
*  Corrigido um problema em que uma solução foi criada automaticamente sempre que um usuário abre uma nova janela de consulta.   
[Item nº 2924667 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2924667)    
[Item nº 2917742 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2917742)   
[Item nº 2612635 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2612635)
    
*  Corrigido um problema em que tabelas de tempo não puderam ser expandidas no Pesquisador de Objetos quando estiverem em banco de dados do sistema.  
[Item nº2551649 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2551649)
    
*  Corrigido um problema em que o SSMS executa uma consulta para SELECT @@trancount depois de executar um lote.    
[Item nº 3042364 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/3042364)
    
*  Corrigido um problema no Analysis Services no qual a criação de um script na página de propriedades de um servidor resultava em uma caixa de diálogo de conexão oculta.
    
*  Corrigido um problema em que Ctrl + Q não seleciona a barra de ferramentas Início Rápido.
    
*  Corrigido um problema em que alterar o MaxSize de um banco de dados usando a caixa de diálogo Propriedades do Servidor foi interrompida para bancos de dados com menos de 2 TB.  
[Item nº 1231091 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/1231091)
    
*  Corrigido um problema em que o Assistente de Restauração do Banco de Dados não aceita nomes de arquivos com espaços em branco à esquerda:   
[Item nº 2395147 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2395147)

*  Corrigido um problema em que o Assistente de Restauração do Banco de Dados não aceita nomes de arquivos com espaços em branco à esquerda:   
[Item nº 2395147 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2395147)



## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-163-august-2016-releasehttpgomicrosoftcomfwlinklinkid824938"></a>![baixar](../ssdt/media/download.png) [versão do SQL Server Management Studio 16.3 (agosto de 2016)](http://go.microsoft.com/fwlink/?LinkID=824938)
 15 de agosto de 2016 | Número de versão:  13.0.15700.28

**Recursos**  
1. Nova opção de autenticação 'Autenticação Universal do Active Directory'
2. Novos cmdlets do módulo SQL Server PowerShell
3. Aprimoramentos para modelos do DTA (Orientador de Otimização do Mecanismo de Banco de Dados) e de Eventos Estendidos
4. Suporte beta para [Monitor de Alta Resolução no SSMS](https://blogs.msdn.microsoft.com/sqlreleaseservices/ssms-highdpi-support/)

[Mais informações sobre recursos estão disponíveis no log de alterações do SSMS.](../ssms/sql-server-management-studio-changelog-ssms.md)

**Problemas conhecidos**

Estes são os problemas e limitações desta versão do SQL Server Management Studio:  

1. **Apenas uma única conta do Azure Active Directory pode fazer logon em uma instância do SSMS usando a Autenticação Universal do Active Directory.**  
    Essa restrição está limitada à autenticação do Active Directory Universal. Você pode fazer logon em servidores diferentes usando a Autenticação de Senha do Active Directory, a Autenticação Integrada do Active Directory ou a Autenticação do SQL Server.
    
    Como solução alternativa, você pode usar outra instância do SSMS para fazer logon como outra conta do Azure Active Directory. 
    
2. **Os comandos de DacFx (Estrutura de Aplicativo de Camada de Dados) e o Designer de Esquema no SSMS não dão suporte à Autenticação Universal do Active Directory.**  
    Comandos que usam DacFx (por exemplo, importação e exportação) e o designer de esquema no SSMS atualmente não dão suporte à Autenticação Universal do Active Directory.
    
    Como solução alternativa, você pode usar as outras formas de autenticação fornecidas no SSMS: Autenticação de Senha do Active Directory, Autenticação Integrada do Active Directory ou Autenticação do SQL Server.

3. **O SSMS só pode se conectar a instâncias do SSIS 2016 (SQL Server 2016 Integrated Services).**  
    Há uma limitação conhecida de compatibilidade com o SQL Server Integration Services que impede a conexão com versões anteriores.
    
    Como solução alternativa para esse problema, você pode se conectar à instância do SQL Server Integration Service usando a [versão do SSMS alinhada à sua instância do SSIS.](../ssms/previous-sql-server-management-studio-releases.md) 
  
4. **O SSMS não salvará planos de manutenção para o SQL Server 2008 R2 e versões anteriores do SQL Server.**  
    Essa é uma limitação conhecida que esperamos resolver no futuro. Enquanto isso, você pode usar a [versão 2014 do SSMS](../ssms/previous-sql-server-management-studio-releases.md) para salvar os planos de manutenção.  
    
5. **As instalações do SSMS que não estejam em inglês podem exigir a instalação de um pacote de segurança adicional.**  
Versões do SSMS não localizadas para o inglês exigem o [pacote de atualização de segurança da base de dados 2862966](https://support.microsoft.com/en-us/kb/2862966) se a instalação for realizada em: Windows 8, Windows 7, Windows Server 2012 e Windows Server 2008 R2.
  
6. **O SQL Server Configuration Manager não será iniciado se não houver um SQL Server instalado no computador cliente**  
    Se não tiver o SQL Server instalado no computador cliente e iniciar o SQL Server Configuration Manager, você verá o seguinte erro:   
     `Cannot connect to WMI provider. You do not have permission or the server is unreachable. Note that you can only manage SQL Server 2005 and later servers with SQL Server Configuration Manager. Invalid namespace \[0x8004100e]`,   
   
     * Se você tiver adicionado as instâncias do SQL Server à lista 'Servidores Registrados' no SSMS:  
        1. Navegue até o modo de exibição 'Servidores Registrados' no SSMS.  
        2. Clique na instância do SQL Server que você deseja configurar.  
        3. Selecione 'SQL Server Configuration Manager...' no menu de atalho.    
          
      * Se você não tiver adicionado uma instância do SQL Server à lista 'Servidores Registrados' no SSMS:  
        1. Abra um prompt de comando como Administrador.  
        2. Execute a ferramenta Mofcomp usando o seguinte comando:  
    `mofcomp "%programfiles(x86)%\Microsoft SQL Server\130\Shared\sqlmgmproviderxpsp2up.mof"`  
        3. Após executar a ferramenta Mofcomp, execute os seguintes comandos para reiniciar o serviço WMI para que as alterações entrem em vigor:  
        `net stop "Windows Management Instrumentation"`  
        `net start “Windows Management Instrumentation”`  


**Correções**
1. Correção de bug para exibir texto não criptografado de colunas de LOB (Objeto Grande) do AlwaysEncrypted descriptografadas no SSMS (Item nº 2413024 do Microsoft Connect).
2. Correção de bug na caixa de diálogo Always Encrypted para corrigir falhas quando estilos visuais do Windows não estão habilitados (por exemplo, habilitando a exibição de alto contraste).
3. Correção de bug para o erro 'Método não encontrado' que impede a conexão com instâncias do SQL Server.
4. Correção de bug para a falha do SSMS ao criar uma função de partição com deslocamento de data e hora.
5. Correção de bug para remover o requisito do Microsoft .NET 3.5 para iniciar a ferramenta de administração do Distributed Replay (DReplay.exe).
6. Correção de bug no assistente de Implantação do Analysis Services para dar suporte a nomes de servidor totalmente qualificados.
7. Correção de bug no SSMS para exibir as partições em modelos tabulares do Analysis Services com um modelo de compatibilidade de 2016 (Item nº 2845053 do Microsoft Connect).

[Mais informações sobre correções estão disponíveis no log de alterações do SSMS.](../ssms/sql-server-management-studio-changelog-ssms.md)
 
---
## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-july-2016-hotfix-update-releasehttpgomicrosoftcomfwlinklinkid822301"></a>![baixar](../ssdt/media/download.png) [versão de atualização de hotfix de julho de 2016 do SQL Server Management Studio](http://go.microsoft.com/fwlink/?LinkID=822301)

13 de julho de 2016 | Número de versão: 13.0.15600.2

**Recursos**  
1. Suporte para SQL Azure Data Warehouse no SSMS.   
2. Atualizações importantes para o módulo PowerShell do SQL Server.   
3. Tempos de conexão significativamente aprimorados para bancos de dados do SQL Azure.  
4. Suporte avançado a bancos de dados tabulares do SQL Server 2016 (nível de compatibilidade 1200) na caixa de diálogo de processo do Analysis Services e muito mais.   

[Mais informações e recursos estão disponíveis no log de alterações do SSMS.](../ssms/sql-server-management-studio-changelog-ssms.md)

**Problemas conhecidos** 
1. **O instalador da versão do hotfix de julho do SSMS é mostrado como a versão de agosto do SSMS.**
A página de instalação do hotfix da atualização de julho indica agosto devido a uma configuração de compilação interna. Esse pacote é, na verdade, um hotfix para a versão de julho do SSMS. 
2. **O SSMS não pode se conectar a instâncias do SQL Server após a instalação da versão do 'hotfix de julho de 2016'.**
Estamos cientes de um problema em relação à atualização mais recente do SSMS em que, ao tentar conectar-se a um servidor, isso resulta na seguinte mensagem de erro: 
   ```
    "Method not found: 'Void Microsoft.SqlServer.Management.Common.SqlConnectionInfo.set_ApplicationIntent(System.String)'"
    ```
  
    A correção para esse problema estará disponível na próxima versão do SSMS. Como solução alternativa para esse problema, você pode desinstalar e reinstalar o SSMS. Para obter mais detalhes, [acesse este thread do Microsoft Connect referente ao problema](https://connect.microsoft.com/SQLServer/feedback/details/2925257/not-able-to-connect-to-sql-server-instances-after-installing-ssms-2016-july-update).
    
3. **O SSMS tem uma falha ao tentar selecionar uma conta de armazenamento do Azure.**
A versão de julho do SSMS e a versão de julho do hotfix têm uma falha se você tenta selecionar uma conta de armazenamento do Azure e não tem uma conta de armazenamento 'clássico'.
A correção para esse problema estará disponível em uma versão futura do SSMS. Como solução alternativa para esse problema, você pode fazer backup/restaurar bancos de dados para uma conta de armazenamento do Azure criando uma conta de armazenamento clássico ou [usando T-SQL para backup ou restauração](https://msdn.microsoft.com/library/jj720552(v=sql.120).aspx).

4. **O SSMS exibirá apenas as contas de armazenamento 'clássico' do Azure nos assistentes de Backup/Restauração.**
A versão de julho do SSMS e a versão do hotfix de julho exibem somente as contas de armazenamento 'clássico' do Azure para a criação de uma nova credencial se você está tentando fazer backup ou restaurar usando o backup ou restaurar os assistentes.
A correção para esse problema estará disponível em uma versão futura do SSMS. Como solução alternativa para esse problema, você pode fazer backup/restaurar seus bancos de dados para a conta de armazenamento 'clássico' do Azure disponível ou fazer backup para as contas de armazenamento do 'tipo ARM' [usando T-SQL para backup ou restauração](https://msdn.microsoft.com/library/jj720552(v=sql.120).aspx). 

5. **As instalações do SSMS que não estejam em inglês podem exigir a instalação de um pacote de segurança adicional.**
Versões do SSMS não localizadas para o inglês exigem o [pacote de atualização de segurança da base de dados 2862966](https://support.microsoft.com/en-us/kb/2862966) se a instalação for realizada em: Windows 8, Windows 7, Windows Server 2012 e Windows Server 2008 R2.
6. **O SSMS só pode se conectar a instâncias do SSIS 2016 (SQL Server 2016 Integrated Services).** Há uma limitação conhecida de compatibilidade com o SQL Server Integration Services que impede a conexão com versões anteriores.
Como solução alternativa para esse problema, você pode se conectar à instância do SQL Server Integration Service usando a versão do SSMS alinhada à sua instância do SSIS.
7. **O SSMS não salvará planos de manutenção para o SQL Server 2008 R2 e versões anteriores do SQL Server.** Estamos trabalhando em uma correção para esse problema. Enquanto isso, você pode usar a versão 2014 do SSMS abaixo para salvar os planos de manutenção.
8. **O SQL Server Configuration Manager não será iniciado se não houver um SQL Server instalado no computador cliente.** Se não tiver o SQL Server instalado no computador cliente e iniciar o SQL Server Configuration Manager, você receberá o erro 'Não é possível conectar-se ao provedor WMI'. Como uma solução alternativa:
    * Abra um novo prompt de comando como Administrador.
    * Execute a ferramenta Mofcomp usando o seguinte comando:  
      mofcomp "%programfiles(x86)%\Microsoft SQL Server\130\Shared\sqlmgmproviderxpsp2up.mof"
    * Após executar a ferramenta Mofcomp, execute os seguintes comandos para reiniciar o serviço WMI para que as alterações entrem em vigor:  
       net stop "Instrumentação de Gerenciamento do Windows"  
       net start "Instrumentação de Gerenciamento do Windows"

**Correções**  
1. Correção de bugs no designer de consulta do SSMS para permitir a adição de tabelas ao designer se um usuário não tiver permissões SELECT.
2. Correção de bugs para adicionar suporte ao IntelliSense para as funções 'TRY_CAST()' e 'TRY_CONVERT()' funções [(Item nº 2453461 do Microsoft Connect)](https://connect.microsoft.com/SQLServer/feedback/details/2453461/sql-server-2012-issue-with-try-cast).
3. Correção de bugs na janela do editor SSMS para permitir a abertura do tipo arrastar e soltar de arquivos SQL [(Item nº 2690658 do Microsoft Connect)](https://connect.microsoft.com/SQLServer/feedback/details/2690658/cannot-drag-sql-files-into-management-studios).
4. Correção de bugs no Analysis Services para mostrar corretamente o provedor de Feed de Dados para modelos multidimensionais do Analysis Services.
5. Correção de bugs no SSMS para evitar falhas ao tentar editar um link de associação no designer de tabela SSMS [(Item nº 2721052 do Microsoft Connect)](https://connect.microsoft.com/SQLServer/feedback/details/2721052/ssms-view-design-mode-right-click-on-join-crashes-ssms).  

[Mais informações e correções estão disponíveis no log de alterações do SSMS.](../ssms/sql-server-management-studio-changelog-ssms.md)

---
## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-june-2016-releasehttpgomicrosoftcomfwlinklinkid799832"></a>![baixar](../ssdt/media/download.png) [versão de junho de 2016 do SQL Server Management Studio](http://go.microsoft.com/fwlink/?LinkID=799832)

1º de junho de 2016 | Número de versão: 13.0.15000.23

**Recursos**  
Novo instalador do SSMS simplificado. Versões autônomas do SSMS. Verificação automática de atualizações. Uma nova caixa de diálogo Localização Rápida. SSMS baseado no shell do Visual Studio 2015 e muito mais.   
[Mais informações estão disponíveis no log de alterações do SSMS.](../ssms/sql-server-management-studio-changelog-ssms.md)

**Problemas conhecidos** 
1. **A geração de scripts do PowerShell por meio do assistente Always Encrypted está desabilitada atualmente.**
Uma correção para esse problema estará disponível em uma atualização mensal do SSMS subsequente.
2. **O item de menu de contexto 'Criptografar Colunas' no Pesquisador de Objetos está desabilitado para tabelas e colunas quando você está conectado ao Banco de Dados SQL do Azure.** Uma correção para esse problema estará disponível em uma atualização mensal do SSMS subsequente. Como alternativa, clique com o botão direito do mouse no Pesquisador de Objetos no banco de dados, selecione 'Tarefas' e 'Criptografar Colunas' para criptografar as tabelas e colunas do Banco de Dados SQL do Azure.
3. **O SSMS só pode se conectar a instâncias do SSIS 2016 (SQL Server 2016 Integrated Services).** Há uma limitação conhecida de compatibilidade com o SQL Server Integration Services que impede a conexão com versões anteriores.
Como solução alternativa para esse problema, você pode se conectar à instância do SQL Server Integration Service usando a versão do SSMS alinhada à sua instância do SSIS.
4. **O SSMS não salvará planos de manutenção para o SQL Server 2008 R2 e versões anteriores do SQL Server.** Estamos trabalhando em uma correção para esse problema. Enquanto isso, você pode usar a versão 2014 do SSMS abaixo para salvar os planos de manutenção.
5. **O SQL Server Configuration Manager não será iniciado se não houver um SQL Server instalado no computador cliente.** Se não tiver o SQL Server instalado no computador cliente e iniciar o SQL Server Configuration Manager, você receberá o erro 'Não é possível conectar-se ao provedor WMI'. Como uma solução alternativa:
    * Abra um novo prompt de comando como Administrador.
    * Execute a ferramenta Mofcomp usando o seguinte comando:  
      mofcomp "%programfiles(x86)%\Microsoft SQL Server\130\Shared\sqlmgmproviderxpsp2up.mof"
    * Após executar a ferramenta Mofcomp, execute os seguintes comandos para reiniciar o serviço WMI para que as alterações entrem em vigor:  
       net stop "Instrumentação de Gerenciamento do Windows"  
       net start "Instrumentação de Gerenciamento do Windows"

**Correções**  
1. Caixa de diálogo de localização rápida no SSMS integrada de forma melhor ao documento atual e que permite pesquisar por meio de expressões regulares ([Item nº 2735513 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2735513/quick-find-replace-in-ssms-2016-rc3/)).
2. Correção de bug na ajuda F1 contextual do SSMS para exibir corretamente artigos e documentos de ajuda.
3. Correção de bug no modo de exibição de 'Consultas Retornadas' do Repositório de Dados de Consulta que causou a falha do SSMS durante a rolagem.
4. Correção de bug no conector OLEDB do Excel Analysis Services para permitir conexões do Excel 2016 ao SQL Server Analysis Services.
5. Correção de bug na caixa de diálogo de conexão do SSMS para mostrar a caixa de diálogo de conexão no mesmo monitor como a janela principal do SSMS em sistemas de vários monitores ([Item nº 724909 do Microsoft Connect)](https://connect.microsoft.com/SQLServer/feedback/details/724909/connection-dialog-appears-off-screen/).
6. Correções de bugs na experiência do Always Encrypted. Foi corrigido um bug em que a opção de menu Always Encrypted não era habilitada corretamente para Stretch Databases. Também foi corrigido um bug no assistente do Always Encrypted em que ele não usava corretamente o provedor HSM da SafeNet (Luna SA).

---
## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-2014-sp1httpdownloadmicrosoftcomdownload156156992e6-f7c7-4e55-833d-249bd2348138enux86sqlmanagementstudiox86enuexe"></a>![baixar](../ssdt/media/download.png) [SQL Server Management Studio 2014 SP1](http://download.microsoft.com/download/1/5/6/156992E6-F7C7-4E55-833D-249BD2348138/ENU/x86/SQLManagementStudio_x86_ENU.exe)

14 de maio de 2015 | Número de versão: 12.0.4100.1

**Recursos**  
Suporte aprimorado de banco de dados SQL com nova abertura no menu do portal de gerenciamento, integração do designer de tabela e muito mais.   
[Mais informações estão disponíveis nas notas de versão](https://support.microsoft.com/en-us/kb/3058865).

**Problemas conhecidos**  
N/A

**Correções**
1. O SSMS falha durante as tarefas de Movimentação de Plano de Manutenção se o nome do Plano de Manutenção e o primeiro nome SUB_PLAN são iguais.
2. Você não pode depurar um procedimento armazenado que chama sp_executesql no SSMS (SQL Server Management Studio). Quando F11 é pressionado, você recebe uma mensagem de erro 'Referência de objeto não definida para uma instância do objeto' ([Item nº 736509 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/736509/sql-server-2012-rtm-management-studio-cannot-debug-sp-executesql)).
3. O SSMS não gerencia totalmente o Texto Completo no SQL Server Express ([Item nº 740181 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/740181/management-studio-does-not-fully-manage-full-text-in-sql-server-express)).
4. O SSMS trata procedimentos Armazenados Numerados de forma inconsistente [(Item nº 764197 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/764197/ssms-2012-inconsistently-handles-numbered-procedures)).
5. O SSMS falha ocasionalmente ao fechar, o que faz com que ele seja reiniciado automaticamente ([Item nº 774317 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/774317/sql-server-management-studio-2012-2014-crashes-when-closing)).
6. A criação de script duplica as instruções ao executar o script de permissões em nível de coluna no SSMS ([Item nº 797967 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/797967/ssms-create-script-duplicates-the-statements-for-grant-or-deny-column-permissions)).
7. O SSMS pode falhar quando você tenta atualizar o ícone da janela do SSMS na barra de tarefas ([Item nº 799430 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/799430/ssms-2012-sp-1-cu-5-installed-crash-when-enforce-refresh-on-connect)).

---
## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-2012-sp3httpdownloadmicrosoftcomdownloadf67f673709c-d371-4a64-8bf9-c1dd73f60990enux86sqlmanagementstudiox86enuexe"></a>![baixar](../ssdt/media/download.png) [SQL Server Management Studio 2012 SP3](http://download.microsoft.com/download/F/6/7/F673709C-D371-4A64-8BF9-C1DD73F60990/ENU/x86/SQLManagementStudio_x86_ENU.exe)  
  
21 de novembro de 2015 | Número de versão: 11.0.6020.0

**Recursos**  
Edições express do SSMS completo. Trechos de códigos. Índices de repositório de colunas e mais.  
[Mais informações estão disponíveis nas notas de versão.](https://support.microsoft.com/en-us/kb/3072779)
 
**Problemas conhecidos**  
N/A

**Correções**
1. Colunas ausentes não podem ser indicadas na mensagem de erro quando você importa dados usando o Assistente de Importação e exportação.
2. Erro "Não é possível criar o plano de restauração devido a quebra na cadeia LSN" quando você restaura um backup diferencial no SSMS

---
## <a name="additional-downloads"></a>Downloads adicionais  
Para obter uma lista de todos os downloads do SQL Server Management Studio, veja o [Centro de Download da Microsoft](https://www.microsoft.com/en-us/download/search.aspx?q=sql%20server%20management%20studio&p=0&r=10&t=&s=Relevancy~Descending).  
  
Para obter a versão mais recente do SQL Server Management Studio, veja [Baixar o SQL Server Management Studio &#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md).  

---  
## <a name="related-resources"></a>Recursos relacionados
[Centro de atualização do Microsoft SQL Server](https://technet.microsoft.com/sqlserver/ff803383.aspx)   
[Início rápido do SQL Server Management Studio](http://msdn.microsoft.com/en-us/d2bade70-07cf-4d94-b5d2-88aecb538ed1)  
[Fórum do SQL Server Management Studio](https://social.msdn.microsoft.com/forums/en-us/home?forum=sqltools)  

  

