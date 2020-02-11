---
title: Classe de evento Hash Warning | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Hash Warning event class
ms.assetid: cb93c620-4be9-4362-8bf0-af3f2048bdaf
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cc2b6d2ba25ee487053a7f9f711c499356a5ec59
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62662340"
---
# <a name="hash-warning-event-class"></a>Classe de evento Hash Warning
  A classe de evento Hash Warning pode ser usada para monitorar quando uma recursão de hash ou cessação de hashing (esgotamento de hash) ocorreu durante a operação de hashing.  
  
 A recursão de hash ocorre quando a entrada de criação não cabe na memória disponível, ocasionando a divisão da entrada em várias partições que são processadas separadamente. Se qualquer uma dessas partições ainda não couber na memória disponível, será dividida em subpartições, que serão processadas separadamente. Esse processo de divisão continuará até que cada partição caiba na memória disponível ou até que o nível máximo de recursão seja atingido (exibido na coluna de dados IntegerData).  
  
 O esgotamento hash ocorre quando uma operação de hashing atinge o nível máximo de recursão e é deslocada para um plano alternativo, de forma a processar os dados particionados restantes. O esgotamento de hash geralmente ocorre devido a dados distorcidos.  
  
 A recursão de hash e o esgotamento de hash diminuem o desempenho do servidor. Para eliminar ou reduzir a frequência de recursão de hash e de esgotamento de hash, execute um dos seguintes procedimentos:  
  
-   Certifique-se de que as estatísticas estão presentes nas colunas que estão sendo unidas ou agrupadas.  
  
-   Caso existam, atualize-as.  
  
-   Use um tipo diferente de junção. Por exemplo, use a junção MERGE ou LOOP, se apropriado.  
  
-   Aumente a memória disponível no computador. A recursão de hash ou o esgotamento de hash ocorrem quando não há memória suficiente para processar as consultas existentes e é necessário gravar no disco.  
  
 A criação ou atualização das estatísticas na coluna envolvida na junção é a forma mais eficiente de reduzir o número de recursões de hash ou de esgotamento de hash.  
  
> [!NOTE]  
>  Os termos *grace hash join* e *recursive hash join* também são usados para descrever o esgotamento de hash.  
  
> [!IMPORTANT]  
>  Para determinar onde o evento Hash Warning está ocorrendo quando o otimizador de consultas gera um plano de execução, é também necessário coletar a classe de evento Showplan no rastreamento. É possível escolher qualquer uma das classes de evento Showplan, exceto as classes de evento Showplan Text e Showplan Text (Unencoded), que não retornam a ID do nó. As ID do nó nos Showplans identificam cada operação que o otimizador de consultas executa ao gerar um plano de execução de consulta. Essas operações são chamadas de *operadores*, e cada operador no Showplan tem uma ID do Nó. A coluna ObjectID dos eventos Hash Warning corresponde à ID do nó no Showplans. Assim, é possível determinar o operador ou a operação que gerou o erro.  
  
## <a name="hash-warning-event-class-data-columns"></a>Colunas de dados da classe de evento Hash Warning  
  
|Nome da coluna de dados|Tipo de dados|DESCRIÇÃO|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores transmitidos pelo aplicativo em vez do nome exibido do programa.|10|Sim|  
|ClientProcessID|`int`|ID atribuída pelo computador host ao processo em que o aplicativo cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer a ID de processo do cliente.|9|Sim|  
|DatabaseID|`int`|ID do banco de dados especificado pela instrução USE de *database* ou o banco de dados padrão se nenhuma instrução USE de *database* tiver sido emitida para uma determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados ServerName for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|DatabaseName|`nvarchar`|Nome do banco de dados no qual a instrução do usuário está sendo executada.|35|Sim|  
|EventClass|`int`|Tipo de evento = 55.|27|Não|  
|EventSequence|`int`|Sequência de um determinado evento na solicitação.|51|Não|  
|EventSubClass|`int`|Tipo de subclasse de evento.<br /><br /> 0=Recursion<br /><br /> 1=Bailout|21|Sim|  
|GroupID|`int`|ID do grupo de carga de trabalho no qual o evento de Rastreamento do SQL dispara.|66|Sim|  
|HostName|`nvarchar`|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer o nome do host. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|IntegerData|`int`|Nível de recursão (somente recursão de hash).|25|Sim|  
|IsSystem|`int`|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|LoginName|`nvarchar`|Nome de logon do usuário (logon de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou as credenciais de logon do Windows no formato *\<DOMAIN>\\<username\>* ).|11|Sim|  
|LoginSid|`image`|Número SID (identificação de segurança) do usuário que fez logon. Você pode encontrar essas informações na exibição de catálogo sys.server_principals. Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|NTDomainName|`nvarchar`|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|NTUserName|`nvarchar`|Nome do usuário do Windows.|6|Sim|  
|ObjectID|`int`|ID do nó da raiz da equipe hash envolvida na repartição. Corresponde à ID do nó nos Showplans.|22|Sim|  
|RequestID|`int`|ID da solicitação que contém a instrução.|49|Sim|  
|ServerName|`nvarchar`|Nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26||  
|SessionLoginName|`nvarchar`|Nome de logon do usuário que originou a sessão. Por exemplo, ao se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, SessionLoginName mostrará o Logon1 e LoginName mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|SPID|`int`|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|StartTime|`datetime`|Hora de início do evento, se disponível.|14|Sim|  
|TransactionID|`bigint`|ID da transação atribuída pelo sistema.|4|Sim|  
|XactSequence|`bigint`|Token que descreve a transação atual.|50|Sim|  
  
## <a name="see-also"></a>Consulte Também  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
