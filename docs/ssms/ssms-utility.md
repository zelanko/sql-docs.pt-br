---
title: Utilitário de SSMS | Microsoft Docs
ms.custom: ''
ms.date: 12/08/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], opening
- command prompt utilities [SQL Server], sqlwb
- sqlwb utility
- Management Studio command line
- opening SQL Server Management Studio
ms.assetid: aafda520-9e2a-4e1e-b936-1b165f1684e8
caps.latest.revision: 50
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 707777f3b568aa38d06416ca1ab3f1292051e068
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33052853"
---
# <a name="ssms-utility"></a>Utilitário de Ssms
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  O utilitário **Ssms**abre o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Se especificado, o **Ssms** também estabelece uma conexão com um servidor e abre consultas, scripts, arquivos, projetos e soluções.  
  
 Você pode especificar arquivos que contenham consultas, projetos ou soluções. Arquivos que contêm consultas serão conectados automaticamente a um servidor se a informação de conexão for fornecida e o tipo de arquivo for associado com aquele tipo de servidor. Por exemplo, arquivos .sql abrirão uma janela Editor de Consultas SQL em [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]e arquivos .mdx abrirão uma janela Editor de Consultas MDX em [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. **Soluções e Projetos do SQL Server** serão abertos no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
> [!NOTE]  
>  O utilitário **Ssms** não executa consultas. Para executar consultas da linha de comando, use o utilitário **sqlcmd** .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Ssms  
    [scriptfile] [projectfile] [solutionfile]  
    [-S servername] [-d databasename] [-G] [-U username] [-P password]   
    [-E] [-nosplash] [-log [filename]?] [-?]  
```  
  
## <a name="arguments"></a>Argumentos  
 *scriptfile*  
 Especifica um ou mais arquivos de script para serem abertos. O parâmetro deve conter o caminho completo para os arquivos.  
  
 *projectfile*  
 Especifica um projeto de script para ser aberto. O parâmetro deve conter o caminho completo para o arquivo de projeto de script.  
  
 *solutionfile*  
 Especifica uma solução para ser aberta. O parâmetro deve conter o caminho completo para o arquivo de solução.  
  
 [**-S** *servername*]  
  Nome do servidor  
  
 [**-d** *databasename*]  
  Nome do banco de dados  

 [**-G**] Conecte-se usando a Autenticação do Active Directory. O tipo de conexão é determinado se **-P** e/ou **-U** está incluído.
 - Se **-U** e **-P** *não* estiverem incluídos, então, o **Active Directory – Integrado** será usado e nenhuma caixa de diálogo será exibida.
 - Se ambos os **-U** e **-P** estiverem incluídos, então, o **Active Directory – Senha** será usado. O uso dessa opção **não é recomendado** porque você precisa especificar uma senha de texto não criptografado na linha de comando, o que não é recomendado.
 - Se **-U** estiver incluído, mas **-P** estiver ausente, então, a caixa de diálogo de autenticação será exibida, mas todas as tentativas de logon falharão. 

  Observe que o **Active Directory – Universal com suporte do MFA** não tem suporte atualmente. 
  
[**-U** *username*]  
 Nome de usuário ao se conectar com a “Autenticação do SQL” ou “Active Directory – Senha”  
  
[**-P** *password*]  
 Senha ao se conectar com a “Autenticação do SQL” ou “Active Directory – Senha”
  
[**-E**]  
 Conectar usando a Autenticação do Windows  
  
[**-nosplash**]  
 Impede o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] de exibir o gráfico da tela inicial ao abrir. Use essa opção ao conectar-se a um computador que executa o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] por meio de Serviços de Terminal em uma conexão com uma largura da banda limitada. Este argumento não diferencia maiúsculas e minúsculas e pode ser exibido antes ou depois de outros argumentos  
  
[**-log***[nome do arquivo]?*]  
 Registra a atividade do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] no arquivo especificado para solucionar problemas  
  
[**-?**]  
 Exibe a ajuda de linha de comando  
  
## <a name="remarks"></a>Remarks  
 Todas as alternâncias são opcionais e separadas por um espaço, exceto os arquivos que são separados por vírgulas. Se você não especificar nenhuma alternância, o **Ssms** abrirá o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] como especificado nas configurações de **Opções** no menu **Ferramentas** . Por exemplo, se a página **Ambiente/Geral** na opção **Na inicialização** especificar **Abrir nova janela de consulta**, o **SSMS** será aberto com um Editor de Consultas em branco.  
  
 A opção **-log** deve aparecer ao final da linha de comando, após todas as outras opções. O argumento de nome de arquivo é opcional. Se um nome de arquivo for especificado, e o arquivo não existir, o arquivo será criado. Se o arquivo não puder ser criado – por exemplo, devido à falta de acesso de gravação, o log será gravado na localidade de APPDATA não localizada (veja abaixo). Se o argumento de nome de arquivo não for especificado, dois arquivos serão gravados na pasta de dados de aplicativo não localizada do usuário atual. A pasta de dados de aplicativo não localizada para o SQL Server pode ser encontrada na variável de ambiente de APPDATA. Por exemplo, para o SQL Server 2012, a pasta é \<unidade do sistema>:\Users\\<nome de usuário\>\AppData\Roaming\Microsoft\AppEnv\10.0\\. Os dois arquivos são, por padrão, chamados de ActivityLog.xml e ActivityLog.xsl. O primeiro contém os dados de log de atividade e o segundo é uma folha de estilo XML que fornece uma maneira mais conveniente de exibir o arquivo XML. Use as seguintes etapas para exibir o arquivo de log no visualizador padrão de XML, como o Internet Explorer: clique em Iniciar, em seguida clique em Executar…" e, então, digite \<unidade do sistema>:\Users\\<nome de usuário\>\AppData\Roaming\Microsoft\AppEnv\10.0\ActivityLog.xml” no campo fornecido e, em seguida, pressione Enter.  
  
 Arquivos que contenham consultas solicitarão para serem conectados a um servidor se a informação de conexão for fornecida e o tipo de arquivo for associado com o tipo de servidor. Por exemplo, arquivos .sql abrirão uma janela Editor de Consultas SQL em [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]e arquivos .mdx abrirão uma janela Editor de Consultas MDX em [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. **Soluções e Projetos do SQL Server** serão abertos no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
 A tabela a seguir mapeia os tipos de servidor para extensões de arquivo.  
  
|Tipo de servidor|Extensão|  
|-----------------|---------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|.sql|  
|SQL Server Analysis Services|.mdx<br /><br /> .xmla|  
  
## <a name="examples"></a>Exemplos  
 O script seguinte abre o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] em um prompt de comando com as configurações padrão:  
  
```  
Ssms  
  
```  
  
 O script a seguir abre o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] de um prompt de comando usando o *Active Directory – Integrado*:  
  
```  
Ssms.exe -S servername.database.windows.net -G
  
``` 


 O script seguinte abre o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] em um prompt de comando, com Autenticação do Windows, com o Editor de Código definido para o servidor `ACCTG and the database AdventureWorks2012,` sem mostrar a tela inicial:  
  
```  
Ssms -E -S ACCTG -d AdventureWorks2012 -nosplash  
  
```  

 O script seguinte abre o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] em um prompt de comando, e abre o script MonthEndQuery.  
  
```  
Ssms "C:\Documents and Settings\username\My Documents\SQL Server Management Studio Projects\FinanceScripts\FinanceScripts\MonthEndQuery.sql"  
  
```  
  
 O script seguinte abre o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] em um prompt de comando e abre o projeto NewReportsProject no computador nomeado de `developer`:  
  
```  
Ssms "\\developer\fin\ReportProj\ReportProj\NewReportProj.ssmssqlproj"  
  
```  
  
 O script seguinte abre o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] em um prompt de comando e abre a solução MonthlyReports:  
  
```  
Ssms "C:\solutionsfolder\ReportProj\MonthlyReports.ssmssln"  
  
```  
 



## <a name="see-also"></a>Consulte Também  
 [Usar o SQL Server Management Studio](http://msdn.microsoft.com/library/f289e978-14ca-46ef-9e61-e1fe5fd593be)  
  
  
