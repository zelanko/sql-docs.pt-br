---
title: "SQL Server Management Studio – Notas de Versão | Microsoft Docs"
ms.custom: 
ms.date: 01/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0b95337b-80bf-4624-8f5d-cdaf6181d3b8
caps.latest.revision: 51
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 51e336a22d0c1052c48b8e569330aef26f2af094
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-management-studio----release-notes"></a>SQL Server Management Studio - Notas de Versão
Bem-vindo à nossa versão com disponibilidade geral do SQL Server Management Studio!  Esta versão do SQL Server Management Studio (SSMS) é uma instalação autônoma fora da versão do SQL Server. Nosso objetivo é atualizar isso frequentemente com novsa funcionalidade, correções e suporte para os recursos mais recentes no SQL Server e banco de dados SQL do Azure.  
  
Para instalar o SQL Server Management Studio mais recente, veja [Download SQL Server Management Studio &#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md).  
  
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

## <a name="feedback"></a>Comentários  
  
![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [Fórum das Ferramentas de Cliente SQL](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [Registre um problema ou uma sugestão no Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback).  
  
## <a name="see-also"></a>Consulte também  
[Tutorial do SQL Server Management Studio](../ssms/use-sql-server-management-studio.md)  
[Baixar o SQL Server Management Studio &amp;#40;SSMS&amp;#41;](../ssms/download-sql-server-management-studio-ssms.md)  
[Versões anteriores do SQL Server Management Studio](../ssms/previous-sql-server-management-studio-releases.md)  

  

