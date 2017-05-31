---
title: Baixar o SQL Server Management Studio (SSMS) | Microsoft Docs
ms.custom: 
ms.date: 04/03/2017
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
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cc827737cec19c11d2102f968dc2b8bc638bda86
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="download-sql-server-management-studio-ssms"></a>Baixar o SQL Server Management Studio (SSMS)
O SSMS (SQL Server Management Studio) é um ambiente integrado para acessar, configurar, gerenciar, administrar e desenvolver todos os componentes do SQL Server. O SSMS combina um amplo grupo de ferramentas gráficas com vários editores de script avançados para fornecer acesso ao SQL Server para desenvolvedores e administradores de todos os níveis de conhecimento. Esta versão conta com compatibilidade aprimorada com versões anteriores do SQL Server, um instalador da Web independente e notificações do sistema no SSMS quando novas versões estiverem disponíveis.  

    
| ![download](../ssdt/media/download.png) Baixar o SQL Server Management Studio (SSMS)  |  |
|:---|:---|
|**[Baixar o SQL Server Management Studio (16.5.3)](https://go.microsoft.com/fwlink/?LinkID=840946)**|Versão atual para uso em produção.|
|**[Baixar o SQL Server Management Studio – versão Release Candidate (17.0 RC3)](../ssms/sql-server-management-studio-ssms-release-candidate.md)**|Inclui suporte para o SQL Server vNext CTP1.3 e funciona lado a lado com o 16.x, mas não é recomendado para uso em produção.| 


> [!NOTE]
> As versões do SSMS agora são sinalizadas numericamente, não em meses. O SSMS é gratuito! Ele não requer uma licença para instalar e usar.  


## <a name="sql-server-management-studio"></a>SQL Server Management Studio   
**Informações da versão**  
  
O número de versão: 16.5.3  
O número de build para esta versão: 13.0.16106.4
  
**Versões do SQL Server com suporte**  
  
* Esta versão do SSMS funciona com todas as [versões com suporte do SQL Server (SQL Server 2008 – SQL Server 2016)](https://support.microsoft.com/en-us/lifecycle?C2=1044) e fornece o maior nível de suporte para trabalhar com os recursos de nuvem mais recentes no Banco de Dados SQL do Azure e Azure SQL Data Warehouse.  
* Não há um bloqueio explícito para SQL Server 2000 ou SQL Server 2005, mas alguns recursos podem não funcionar corretamente.  
* Além disso, uma versão do SSMS 16.x ou do SSMS 2016 pode ser instalada lado a lado com versões anteriores do SSMS 2014. 
  
**Sistemas Operacionais com suporte**  
  
Esta versão do SSMS dá suporte às seguintes plataformas quando usada com o service pack mais recente disponível:   
 Windows 10, Windows 8, Windows 8.1, Windows 7 (SP1), Windows Server 2012 (64 bits), Windows Server 2012 R2 (64 bits), Windows Server 2008 R2 (64 bits)  
   
 **Idiomas disponíveis**  
> [!NOTE]  
> Versões do SSMS não localizadas para o inglês exigem o [pacote de atualização de segurança da base de dados 2862966](https://support.microsoft.com/en-us/kb/2862966) se a instalação for realizada em: Windows 8, Windows 7, Windows Server 2012 e Windows Server 2008 R2. 
  
 Esta versão do SSMS pode ser instalada nos seguintes idiomas:  
[Chinês (República Popular da China)](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x804) | [Chinês (Taiwan)](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x404) | [Inglês (Estados Unidos)](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x409) | [Francês](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x40c)  
[Alemão](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x407) | [Italiano](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x410) | [Japonês](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x411) | [Coreano](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x412) | [Português (Brasil)](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x416) | [Russo](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x419) | [Espanhol](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x40a)  

 
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





Para obter a lista completa de recursos, consulte   
                [SQL Server Management Studio – Changelog (SSMS)](../ssms/sql-server-management-studio-changelog-ssms.md)  
  
Para ver a lista de problemas conhecidos e soluções alternativas, consulte   
                [SQL Server Management Studio – Notas de Versão](../ssms/sql-server-management-studio-release-notes.md)  
  
Para obter informações sobre a coleta de dados de usuário, consulte   
                [Política de Privacidade do SQL Server](http://www.microsoft.com/privacystatement/en-us/SQLServer/Default.aspx).  
  
## <a name="previous-releases"></a>Versões anteriores  
[Versões anteriores do SQL Server Management Studio](../ssms/previous-sql-server-management-studio-releases.md)  
  
## <a name="feedback"></a>Comentários  
  
![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [Fórum das Ferramentas de Cliente SQL](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [Registre um problema ou uma sugestão no Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback).  
  
## <a name="see-also"></a>Veja também  
[Tutorial: SQL Server Management Studio](http://msdn.microsoft.com/en-us/d2bade70-07cf-4d94-b5d2-88aecb538ed1)  
[Documentação do SQL Server Management Studio](https://msdn.microsoft.com/library/hh213248(v=sql.130).aspx)  
[Microsoft SQL Server](https://msdn.microsoft.com/library/bb545450.aspx)  
[Pacotes de serviço e atualizações adicionais](https://technet.microsoft.com/sqlserver/ff803383.aspx)  
[Baixar o SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)  



