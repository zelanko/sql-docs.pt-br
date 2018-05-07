---
title: Criando procedimentos armazenados estendidos | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: extended-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- warnings [SQL Server]
- extended stored procedures [SQL Server], debugging
- extended stored procedures [SQL Server], creating
- messages [SQL Server], extended stored procedures
ms.assetid: 9f7c0cdb-6d88-44c0-b049-29953ae75717
caps.latest.revision: 38
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 21d29aa0ceb7ba16216db3f52e18379f55b775dd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="creating-extended-stored-procedures"></a>Criando procedimentos armazenados estendidos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a integração CLR.  
  
 Um procedimento armazenado estendido é uma função com um protótipo:  
  
 SRVRETCODE *xp_extendedProcName* **(** SRVPROC **\*);**  
  
 O uso do prefixo xp_ é opcional. Os nomes de procedimento armazenado estendido fazem distinção de maiúsculas e minúsculas quando mencionados em instruções [!INCLUDE[tsql](../../includes/tsql-md.md)], independentemente da página de código/ordem de classificação instalada no servidor. Quando você compila uma DLL:  
  
-   Se um ponto de entrada for necessário, grave uma função DllMain.  
  
     Essa função será opcional; se você não a fornecer em código-fonte, o compilador vinculará sua própria versão, o que não resultará em nada, mas retornará TRUE. Se você fornecer uma função DllMain, o sistema operacional chamará essa função quando um thread ou processo for anexado ou desanexado da DLL.  
  
-   Todas as funções chamadas de fora da DLL (todas as Efunctions do procedimento armazenado estendido) devem ser exportadas.  
  
     Você pode exportar uma função listando seu nome na seção EXPORTS de um arquivo. def, ou você poderá colocar o nome da função no código-fonte com dllexport, uma extensão de compilador da Microsoft (Observe que \__declspec() começa com dois sublinhados).  
  
 Estes arquivos são necessários para criar uma DLL de procedimento armazenado estendido.  
  
|Arquivo|Description|  
|----------|-----------------|  
|Srv.h|Arquivo de cabeçalho da API do Procedimento Armazenado Estendido|  
|Opends60.lib|Biblioteca de importação para Opends60.dll|  
  
 Para criar uma DLL de procedimento armazenado estendido, crie um projeto do tipo Biblioteca de Vínculo Dinâmico. Para obter mais informações sobre a criação de uma DLL, consulte a documentação do ambiente de desenvolvimento.  
  
 É altamente recomendado que todas as DLLs de procedimento armazenado estendido implementem e exportem a seguinte função:  
  
```  
__declspec(dllexport) ULONG __GetXpVersion()  
{  
   return ODS_VERSION;  
}  
```  
  
> [!NOTE]  
>  __declspec(dllexport) é uma extensão de compilador específica da Microsoft. Se seu compilador não aceitar esta diretiva, você deverá exportar esta função no arquivo DEF, na seção EXPORTS.  
  
 Quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciado com o rastreamento de sinalizador - T260 ou se um usuário com privilégios de administrador do sistema executa DBCC TRACEON (260), e se o armazenado estendido DLL de procedimento não dá suporte a __GetXpVersion(), uma mensagem de aviso (erro 8131: o procedimento armazenado estendido A DLL '% s' não exporta \__GetXpVersion().) é impressa no log de erros. (Observe que \__GetXpVersion() começa com dois sublinhados.)  
  
 Se a DLL de procedimento armazenado estendido exportar __GetXpVersion(), mas a versão retornada pela função for menor que aquela exigida pelo servidor, uma mensagem de aviso informando a versão retornada pela função e a versão esperada pelo servidor será impressa no log de erros. Se você receber essa mensagem, você estiver retornando um valor incorreto de \__GetXpVersion(), ou você está compilando com uma versão mais antiga de SRV.  
  
> [!NOTE]  
>  SetErrorMode, uma função do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Win32, não deve ser chamada em procedimentos armazenados estendidos.  
  
 Será recomendável que um procedimento armazenado estendido de execução demorada chame srv_got_attention periodicamente, de forma que o procedimento possa ser encerrado por si mesmo se a conexão for interrompida ou o lote for anulado.  
  
 Para depurar uma DLL de procedimento armazenado estendido, copie-a no diretório [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\Binn. Para especificar o executável para a sessão de depuração, insira o nome de arquivo e caminho do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] arquivo executável (por exemplo, C:\Program Files\Microsoft SQL mssql13. MSSQLSERVER\MSSQL\Binn\Sqlservr.exe). Para obter informações sobre argumentos sqlservr, consulte [aplicativo sqlservr](../../tools/sqlservr-application.md).  
  
## <a name="see-also"></a>Consulte também  
 [srv_got_attention &#40;API de procedimento armazenado estendido&#41;](../../relational-databases/extended-stored-procedures-reference/srv-got-attention-extended-stored-procedure-api.md)  
  
  
