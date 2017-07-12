---
title: "SQL Server Management Studio – Notas de Versão | Microsoft Docs"
ms.custom: 
ms.date: 06/22/2017
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
ms.translationtype: Human Translation
ms.sourcegitcommit: fe6de2b16b9792a5399b1c014af72a2a5ee52377
ms.openlocfilehash: f593303a681e2f52161777fc48f0fb1b479d20d9
ms.contentlocale: pt-br
ms.lasthandoff: 06/23/2017

---
<a id="sql-server-management-studio----release-notes" class="xliff"></a>

# SQL Server Management Studio - Notas de Versão
Bem-vindo à nossa versão com disponibilidade geral do SQL Server Management Studio!  Esta versão do SQL Server Management Studio (SSMS) é uma instalação autônoma fora da versão do SQL Server. Nosso objetivo é atualizar isso frequentemente com novsa funcionalidade, correções e suporte para os recursos mais recentes no SQL Server e banco de dados SQL do Azure.  
  
Para instalar o SQL Server Management Studio mais recente, veja [Download SQL Server Management Studio &#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md).  
  
Estes são os problemas e limitações desta versão do SQL Server Management Studio:  

1. **Assistente de banco de dados de restauração gera um padrão de caminho incorreto para o local do arquivo de banco de dados de destino** 
    este é um problema conhecido quando SSMS estiver conectado a um servidor Linux. Mesmo que o caminho é incorreto/ímpar, ela será manipulada corretamente no lado do servidor, ou seja, não há nenhum problema funcional.

2. **Problemas de navegador de arquivo**
    - Ao trabalhar com uma instância com base em Windows do SQL Server de 2017 CTP 2.0, o navegador de arquivos da interface do usuário no SSMS pode falhar ao abrir se o servidor tiver uma unidade de disquete vazia ou um disco fixo protegida pelo Bitlocker instalado. 
    - O interface do usuário do navegador de arquivos não oferece suporte a versões do SQL Server 2017 antes do CTP 2.0.
    


3. **Apenas uma única conta do Azure Active Directory pode fazer logon em uma instância do SSMS usando a Autenticação Universal do Active Directory.**  
    Essa restrição está limitada à autenticação do Active Directory Universal. Você pode fazer logon em servidores diferentes usando a Autenticação de Senha do Active Directory, a Autenticação Integrada do Active Directory ou a Autenticação do SQL Server.
    
    Como solução alternativa, você pode usar outra instância do SSMS para fazer logon como outra conta do Azure Active Directory. 
    
4. **Os comandos de DacFx (Estrutura de Aplicativo de Camada de Dados) e o Designer de Esquema no SSMS não dão suporte à Autenticação Universal do Active Directory.**  
    Comandos que usam DacFx (por exemplo, importação e exportação) e o designer de esquema no SSMS atualmente não dão suporte à Autenticação Universal do Active Directory.
    
    Como solução alternativa, você pode usar as outras formas de autenticação fornecidas no SSMS: Autenticação de Senha do Active Directory, Autenticação Integrada do Active Directory ou Autenticação do SQL Server.

5. **O SSMS só pode se conectar a instâncias do SSIS 2016 (SQL Server 2016 Integrated Services).**  
    Há uma limitação conhecida de compatibilidade com o SQL Server Integration Services que impede a conexão com versões anteriores.
    
    Como solução alternativa para esse problema, você pode se conectar à instância do SQL Server Integration Service usando a [versão do SSMS alinhada à sua instância do SSIS.](../ssms/previous-sql-server-management-studio-releases.md) 
  
5. **O SSMS não salvará planos de manutenção para o SQL Server 2008 R2 e versões anteriores do SQL Server.**  
    Essa é uma limitação conhecida que esperamos resolver no futuro. Enquanto isso, você pode usar a [versão 2014 do SSMS](../ssms/previous-sql-server-management-studio-releases.md) para salvar os planos de manutenção.  
    
5. **As instalações do SSMS que não estejam em inglês podem exigir a instalação de um pacote de segurança adicional.**  
Versões do SSMS não localizadas para o inglês exigem o [pacote de atualização de segurança da base de dados 2862966](https://support.microsoft.com/en-us/kb/2862966) se a instalação for realizada em: Windows 8, Windows 7, Windows Server 2012 e Windows Server 2008 R2.

5. **Clicar em Ajuda ou pressionar F1 não abre a ajuda**  
Alguns ambientes exibem o seguinte ao clicar em Ajuda ou pressionar F1: **você precisará de um novo aplicativo para abrir o ms-xhelp**. Esse erro é um problema conhecido e será corrigido em uma versão futura.
  
<a id="feedback" class="xliff"></a>

## Comentários  
  
![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [Fórum das Ferramentas de Cliente SQL](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [Registre um problema ou uma sugestão no Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback).  
  
<a id="see-also" class="xliff"></a>

## Consulte também  
[Tutorial do SQL Server Management Studio](../ssms/use-sql-server-management-studio.md)  
[Baixar o SQL Server Management Studio &amp;#40;SSMS&amp;#41;](../ssms/download-sql-server-management-studio-ssms.md)  
[Versões anteriores do SQL Server Management Studio](../ssms/previous-sql-server-management-studio-releases.md)  

  

