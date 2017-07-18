---
title: Baixar o SQL Server Management Studio (SSMS) | Microsoft Docs
ms.custom: 
ms.date: 06/27/2017
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
ms.sourcegitcommit: 47182ebd082dfae0963d761e54c4045be927d627
ms.openlocfilehash: 8c43f57c6d40d3f2c29f220581dddcf74bf96287
ms.contentlocale: pt-br
ms.lasthandoff: 07/11/2017

---
# <a name="download-sql-server-management-studio-ssms"></a>Baixar o SQL Server Management Studio (SSMS)
O SSMS (SQL Server Management Studio) é um ambiente integrado para gerenciar qualquer infraestrutura de SQL, do SQL Server para o banco de dados SQL. O SSMS fornece ferramentas para configurar, monitorar e administrar instâncias do SQL independentemente de onde você implantá-lo. Com o SSMS, você pode implantar, monitorar e atualizar os componentes da camada de dados usados pelos seus aplicativos, além de construir consultas e scripts. 

Esta versão conta com compatibilidade aprimorada com versões anteriores do SQL Server, um instalador da Web independente e notificações do sistema no SSMS quando novas versões estiverem disponíveis.  
  
![baixar](../ssdt/media/download.png) o SSMS é gratuito! **[Baixar o SQL Server Management Studio 17.1](https://go.microsoft.com/fwlink/?linkid=849819)** O SSMS 17.X é a geração mais recente do SQL Server Management Studio e fornece suporte para o SQL Server 2017. 

![download](../ssdt/media/download.png) **[Baixar o Pacote de Atualização do SQL Server Management Studio 17.1 (atualiza o 17.0 para o 17.1)](https://go.microsoft.com/fwlink/?linkid=849821)**

> [!NOTE]
> O módulo do SQL Server PowerShell agora é uma instalação separada por meio da Galeria do PowerShell.  Para obter mais informações, consulte [Instruções de download](download-sql-server-ps-module.md).

## <a name="sql-server-management-studio"></a>SQL Server Management Studio   
**Informações sobre versão**  
  
O número da versão: 17.1  
O número de build desta versão: 14.0.17119.0

## <a name="new-in-this-release"></a>Novo nesta versão  

O SSMS 17.1 é a primeira atualização para a geração 17.X do SQL Server Management Studio.  A geração 17.X compatível com quase todas as áreas de recursos do SQL Server 2008 por meio do SQL Server 2017.  A versão 17.X também é a geração do SSMS compatível com SQL Analysis Service PaaS.

A versão 17.1 inclui:

* Correções para diversos problemas relatados pelos usuários 
* Uma nova ferramenta de gerenciamento de expansão do Integration Services

Para ver a lista completa de recursos, consulte   
                [SQL Server Management Studio – Changelog (SSMS)](../ssms/sql-server-management-studio-changelog-ssms.md)  
   
Para obter informações sobre a coleta de dados de usuário, consulte   
                [Política de Privacidade do SQL Server](http://www.microsoft.com/privacystatement/en-us/SQLServer/Default.aspx) 
  
## <a name="supported-sql-offerings"></a>Ofertas de SQL com suporte
  
* Esta versão do SSMS funciona com todas as [versões com suporte do SQL Server 2008 – SQL Server 2017](https://support.microsoft.com/lifecycle?C2=1044) e fornece o maior nível de suporte para trabalhar com os recursos de nuvem mais recentes no Banco de Dados SQL do Azure e SQL Data Warehouse do Azure.  
* Não há um bloqueio explícito para SQL Server 2000 ou SQL Server 2005, mas alguns recursos podem não funcionar corretamente.  
* Além disso, o SSMS 17.X pode ser instalado lado a lado com o SSMS 16.X ou o SSMS do SQL Server 2014 e anteriores. 
  
## <a name="supported-operating-systems"></a>Sistemas Operacionais com suporte
  
Esta versão do SSMS dá suporte às seguintes plataformas quando usada com o service pack mais recente disponível:   
- Windows 10
- Windows 8.1
- Windows 8
- Windows 7 (SP1)
- Windows Server 2016
- Windows Server 2012 (64 bits) 
- Windows Server 2012 R2 (64 bits) 
- Windows Server 2008 R2 (64 bits)  

>[!NOTE]
>O SSMS 17.X é baseado no shell do Visual Studio 2015 isolado, que foi lançado antes do Windows Server 2016. A Microsoft leva muito a sério a compatibilidade de aplicativo e garante que os aplicativos já fornecidos continuarão sendo executados nas versões mais recentes do Windows. Para minimizar problemas ao executar o SSMS no Windows Server 2016, verifique se o SSMS tem todas as atualizações mais recentes aplicadas. Se você tiver problemas com o SSMS no Windows Server 2016, contate o suporte. A equipe de suporte determina se o problema é com o SSMS, o Visual Studio ou com a compatibilidade do Windows. Em seguida, a equipe de suporte encaminha o problema à equipe apropriada para obter mais informações.

## <a name="ssms-installation-tips-and-issues"></a>Problemas e dicas de instalação do SSMS

>[!NOTE]
> A instalação do SSMS 17.x não atualiza ou substitui versões anteriores do SSMS.  O SSMS 17.x é instalado lado a lado com versões anteriores para que ambas versões estejam disponíveis para uso.
> Se um computador contiver instalações lado a lado do SSMS, verifique se você iniciou a versão correta para suas necessidades específicas.
>  ![SSMS 17.x](media/ssms-start-menu.png)

**Minimizar as reinicializações de instalação**
- Execute as seguintes ações para reduzir as chances de que a instalação do SSMS exija uma reinicialização no final da instalação:
  - Verifique se você está executando uma versão atualizada do pacote redistribuível do Visual C++ 2013. A versão 12.00.40649.5 (ou superior) é necessária. Apenas a versão x64 é necessária.
  - Verifique se a versão do .NET Framework no computador é a 4.6.1 (ou superior).
  - Feche todas as outras instâncias do Visual Studio que estão abertas no computador.
  - Verifique se todas as atualizações mais recentes do sistema operacional estão instaladas no computador.
  - As ações indicadas geralmente são necessárias uma única vez. Há alguns casos em que uma reinicialização é necessária durante as atualizações adicionais para a mesma versão principal do SSMS. Para obter atualizações secundárias, todos os pré-requisitos do SSMS já estarão instalados no computador.

- Para ver a lista de problemas conhecidos e soluções alternativas, consulte [SQL Server Management Studio – notas de versão](../ssms/sql-server-management-studio-release-notes.md)

## <a name="available-languages"></a>Idiomas disponíveis  
> Versões do SSMS não localizadas para o inglês exigem o [pacote de atualização de segurança da base de dados 2862966](https://support.microsoft.com/en-us/kb/2862966) se a instalação for realizada em: Windows 8, Windows 7, Windows Server 2012 e Windows Server 2008 R2. 
  
Esta versão do SSMS pode ser instalada nos seguintes idiomas:

SQL Server Management Studio 17.1:<br>
[Chinês (República Popular da China)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x804) | [Chinês (Taiwan)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x40a)

Baixar o Pacote de Atualização do SQL Server Management Studio 17.1 (atualiza o 17.0 para o 17.1):<br>
[Chinês (República Popular da China)](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x804) | [Chinês (Taiwan)](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x40a)

## <a name="previous-releases"></a>Versões anteriores  
[Versões anteriores do SQL Server Management Studio](../ssms/previous-sql-server-management-studio-releases.md)  
  
## <a name="feedback"></a>Comentários  
  
![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [Fórum das Ferramentas de Cliente SQL](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [Registre um problema ou uma sugestão no Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback)  
  
## <a name="see-also"></a>Veja também  
[Tutorial: SQL Server Management Studio](http://msdn.microsoft.com/en-us/d2bade70-07cf-4d94-b5d2-88aecb538ed1)  
[Documentação do SQL Server Management Studio](https://msdn.microsoft.com/library/hh213248(v=sql.130).aspx)  
[Microsoft SQL Server](https://msdn.microsoft.com/library/bb545450.aspx)  
[Pacotes de serviço e atualizações adicionais](https://technet.microsoft.com/sqlserver/ff803383.aspx)  
[Baixar o SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)  



