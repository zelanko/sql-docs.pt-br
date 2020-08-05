---
title: Utilitário Profiler
description: O utilitário profiler inicia a ferramenta SQL Server Profiler. Os argumentos opcionais permitem controlar como o aplicativo é iniciado.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- command prompt utilities [SQL Server], profiler90 utility
- profiler90 utility
- Profiler [SQL Server Profiler], starting
- SQL Server Profiler, starting
- starting SQL Server Profiler
ms.assetid: e91c30a9-0d29-4f84-bcb8-e8fb62afadda
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a6a51b6949d3b387c1284bdd5cbaa9a64b3cfa37
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917057"
---
# <a name="profiler-utility"></a>Utilitário Profiler
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]
  O utilitário **profiler** inicia a ferramenta [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] . Os argumentos opcionais listados posteriormente neste tópico permitem controlar como o aplicativo é iniciado.  
  
> [!NOTE]  
>  O utilitário **profiler** não foi criado para ser usado para rastreamentos de script. Para saber mais, confira [SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
profiler  
    [ /? ] |  
[  
{  
{ /U login_id [ /P password ] }  
| /E  
}  
{[ /S sql_server_name ] | [ /A analysis_services_server_name ] }  
[ /D database ]  
[ /T "template_name" ]  
[ /B { "trace_table_name" } ]  
{ [/F "filename" ] | [ /O "filename" ] }  
[ /L locale_ID ]  
[ /M "MM-DD-YY hh:mm:ss" ]  
[ /R ]  
[ /Z file_size ]  
]  
```  
  
## <a name="arguments"></a>Argumentos  
 **/?**  
 Exibe o resumo da sintaxe dos argumentos de **profiler** .  
  
 **/U** *id_de_login*  
 ID de logon do usuário para autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . IDs de logon diferenciam maiúsculas de minúsculas.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)].  
  
 **/P** *senha*  
 Especifica uma senha especificada pelo usuário para a autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 **/E**  
 Especifica a conexão com a autenticação do Windows com as credenciais do usuário atual.  
  
 **/S**  *nome_servidor_sql*  
 Especifica uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. O Profiler vai se conectar automaticamente ao servidor especificado usando as informações de autenticação especificadas nas opções **/U** e **/P** ou na opção **/E** . Para se conectar a uma instância nomeada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], use **/S** *nome_servidor_sql*\\*nome_da_instância*.  
  
 **/A**  *nome_do_servidor_de_analysis_services*  
 Especifica uma instância do Analysis Services. O Profiler vai se conectar automaticamente ao servidor especificado usando as informações de autenticação especificadas nas opções **/U** e **/P** ou na opção **/E** . Para se conectar a uma instância nomeada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], use **/A** *nome_do_servidor_de_analysis_services\nome_da_instância*.  
  
 **/D** *banco_de_dados*  
 Especifica o nome do banco de dados a ser usado com a conexão. Essa opção selecionará o banco de dados padrão para o usuário especificado se nenhum banco de dados for especificado.  
  
 **/B "** *nome_da_tabela_de_rastreamento* **"**  
 Especifica uma tabela de rastreamento a ser carregada quando o profiler for iniciado. Você deve especificar o banco de dados, o usuário ou esquema e a tabela.  
  
 **/T "** *nome_do_modelo* **"**  
 Especifica o modelo que será carregado para configurar o rastreamento. O nome do modelo deve estar entre aspas. O nome do modelo deve estar no diretório de modelos de sistema ou no diretório de modelos de usuário. Se existirem dois modelos com mesmo nome em ambos os diretórios, o modelo do diretório do sistema será carregado. Se nenhum modelo com o nome especificado existir, o modelo padrão será carregado. Observe que a extensão de arquivo do modelo (.tdf) não deve ser especificada como parte do *template_name*. Por exemplo:  
  
```  
/T "standard"  
```  
  
 **/F"** *nome_do_arquivo* **"**  
 Especifica o caminho e o nome de um arquivo de rastreamento a ser carregado quando o profiler for iniciado. O caminho e o nome de arquivo completos devem estar entre aspas. Essa opção não pode ser usada com **/O**.  
  
 **/O "** *nome_do_arquivo*  **"**  
 Especifica o caminho e o nome de um arquivo no qual devem ser gravados os resultados de rastreamento. O caminho e o nome de arquivo completos devem estar entre aspas. Essa opção não pode ser usada com **/F.**  
  
 **/L** *ID_do_local*  
 Não disponível.  
  
 **/M "** *MM-DD-AA hh:mm:ss* **"**  
 Especifica a data e a hora para o rastreamento parar. A hora de parada deve estar entre aspas. Especifique a hora de parada de acordo com os parâmetros na tabela abaixo:  
  
|Parâmetro|Definição|  
|---------------|----------------|  
|MM|Mês de dois dígitos|  
|DD|Dia de dois dígitos|  
|YY|Ano de dois dígitos|  
|hh|Hora de dois dígitos em um relógio de 24 horas|  
|MM|Minuto de dois dígitos|  
|ss|Segundo de dois dígitos|  
  
> [!NOTE]  
>  O formato “MM-DD-AA hh:mm:ss” só poderá ser usado se a opção **Usar configurações regionais para exibir valores de data e hora** estiver habilitada no [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]. Se essa opção não estiver habilitada, você deverá usar o formato de data e hora "AAAA-MM-DD hh:mm:ss".  
  
 **/R**  
 Habilita a substituição do arquivo de rastreamento.  
  
 **/Z**  *tamanho_do_arquivo*  
 Especifica o tamanho do arquivo de rastreamento em megabytes (MB). O tamanho padrão é 5 MB. Se a substituição estiver habilitada, todos os arquivos de substituição serão limitados ao valor especificado neste argumento.  
  
## <a name="remarks"></a>Comentários  
 Para iniciar um rastreamento com um modelo específico, use as opções **/S** e **/T** juntas. Por exemplo, para iniciar um rastreamento usando o modelo Padrão em MyServer\MyInstance, digite o seguinte no prompt de comando:  
  
```  
profiler /S MyServer\MyInstance /T "Standard"  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de utilitários de prompt de comando &#40;Mecanismo de Banco de Dados&#41;](../tools/command-prompt-utility-reference-database-engine.md)  
  
  
