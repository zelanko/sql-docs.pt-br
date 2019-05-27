---
title: Utilitário RS.exe (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- automatic report server tasks
- rs utility
- command prompt utilities [Reporting Services]
- report servers [Reporting Services], automating tasks
- command prompt utilities [SQL Server], rs
- scripts [Reporting Services], command prompt
- deploying reports [Reporting Services]
ms.assetid: bd6f958f-cce6-4e79-8a0f-9475da2919ce
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a6c4bf8f67f787214d38148db40ea8122a064a42
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66099833"
---
# <a name="rsexe-utility-ssrs"></a>RS.exe Utility (SSRS)
  O utilitário rs.exe processa o script que você fornece em um arquivo de entrada. Use esse utilitário para automatizar a implantação de servidor de relatório e tarefas de administração.  
  
> [!NOTE]  
>  A partir do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], o utilitário **rs** tem suporte nos servidores de relatório configurados para o modo integrado do SharePoint e em servidores configurados no modo nativo. As versões anteriores suportavam apenas configurações em modo nativo.  
  
 **Neste tópico:**  
  
-   [Local do arquivo](#bkmk_filelocation)  
  
-   [Argumentos](#bkmk_arguments)  
  
-   [Permissões](#bkmk_permissions)  
  
-   [Exemplos](#bkmk_examples)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
      rs {-?}  
{-i input_file=}  
{-s serverURL}  
{-u username}  
{-p password}  
{-e endpoint}  
{-l time_out}  
{-b batchmode}  
{-v globalvars=}  
{-t trace}  
```  
  
##  <a name="bkmk_filelocation"></a> Local do arquivo  
 **RS.exe** está localizado em **\Arquivos de Programas\Microsoft SQL Server\110\Tools\Binn**. Você pode executar o utilitário de qualquer pasta em seu sistema de arquivos.  
  
##  <a name="bkmk_arguments"></a> Argumentos  
 **-?**  
 (Opcional) Exibe a sintaxe de argumentos **rs** .  
  
 `-i` *input_file*  
 (Obrigatório) Especifica o arquivo .rss a ser executado. Esse valor pode ser um parente ou caminho totalmente qualificado para o arquivo .rss.  
  
 `-s` *serverURL*  
 (Obrigatório) Especifica o nome do servidor Web e nome do diretório virtual do servidor de relatório no qual executar o arquivo. Um exemplo de uma URL de servidor de relatório é `http://examplewebserver/reportserver`. O prefixo http:// ou https:// no início do nome do servidor é opcional. Se você omitir o prefixo, o host de script do servidor de relatório tentará usar https primeiro e depois usará http se https não funcionar.  
  
 `-u` [*domain*\\]*username*  
 (Opcional) Especifica uma conta do usuário usada para conexão com o servidor de relatório. Se `-u` e `-p` forem omitidos, a conta do usuário do Windows atual será usada.  
  
 `-p` *senha*  
 (Obrigatório se `-u` for especificado). Especifica a senha para usar com o argumento `-u`. Esse valor diferencia maiúsculas de minúsculas.  
  
 `-e`  
 (Opcional) Especifica o ponto de extremidade SOAP no qual o script deve ser executado. Os valores válidos são os seguintes:  
  
-   Mgmt2010  
  
-   Mgmt2006  
  
-   Mgmt2005  
  
-   Exec2005  
  
 Se não for especificado um valor, o ponto de extremidade Mgmt2005 será usado. Para obter mais informações sobre pontos de extremidade de SOAP, consulte [Report Server Web Service Endpoints](../report-server-web-service/methods/report-server-web-service-endpoints.md).  
  
 `-l` *time_out*  
 (Opcional) Especifica o número de segundos antes que a conexão com o servidor expire. O padrão é 60 segundos. Se você não especificar um valor de tempo limite, o padrão será usado. Um valor de `0` especifica que a conexão nunca expira.  
  
 **-b**  
 (Opcional) Especifica que os comandos no arquivo de script são executados em um lote. Se algum comando falhar, o lote será revertido. Alguns comandos não podem ser processados em lote e são executados como de costume. Somente exceções emitidas e não controladas no resultado de script resultam em reversão. Se o script controlar uma exceção e retornar normalmente de `Main`, o lote será confirmado. Se você omitir esse parâmetro, os comandos serão executados sem criar um lote. Para obter mais informações, consulte [Batching Methods](../report-server-web-service-net-framework-soap-headers/batching-methods.md).  
  
 `-v` *globalvar*  
 (Opcional) Especifica variáveis globais usadas no script. Se o script usa variáveis globais, você deve especificar esse argumento. O valor que você especifica deve ser válido para a variável global definida no arquivo .rss. É necessário especificar uma variável global para cada argumento **–v**.  
  
 O argumento `-v` é especificado na linha de comando e é usado para definir o valor de uma variável global definida no seu script em tempo de execução. Por exemplo, se seu script contiver uma variável nomeada *parentFolder*, você poderá especificar um nome para aquela pasta na linha de comando:  
  
 `rs.exe -i myScriptFile.rss -s http://myServer/reportserver -v parentFolder="Financial Reports"`  
  
 Variáveis globais são criadas com os nomes dados e definidos para os valores fornecidos. Por exemplo, **- v um =**"`1`" **- v b =**"`2`" resulta em uma variável chamada `a` com um valor de "`1`" e uma variável **b**com um valor de "`2`".  
  
 Variáveis globais estão disponíveis para qualquer função no script. Uma barra invertida e aspas (**\\"**) são interpretadas como aspas duplas. As aspas só serão necessárias se a cadeia de caracteres contiver um espaço. Nomes de variáveis devem ser válidas para o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]; eles devem iniciar com um caractere alfabético ou sublinhado e conter caracteres alfabéticos, dígitos ou sublinhados. Palavras reservadas não podem ser usadas como nomes de variável. Para obter mais informações sobre como usar variáveis globais, consulte [Coleções internas em expressões &#40;Construtor de Relatórios e SSRS&#41;](../report-design/built-in-collections-in-expressions-report-builder.md).  
  
 **-t**  
 (Opcional) Produz mensagens de erro para o log de rastreamento. Esse argumento não exige um valor. Para obter mais informações, consulte [Report Server Service Trace Log](../report-server/report-server-service-trace-log.md).  
  
##  <a name="bkmk_permissions"></a> Permissões  
 Para executar essa ferramenta, você deve ter permissão para se conectar à instância do servidor de relatório no qual o script está sendo executado. Você pode executar scripts para fazer alterações no computador local ou em um computador remoto. Para fazer alterações em um servidor de relatório instalado em um computador remoto, especifique o computador remoto no argumento `-s`.  
  
##  <a name="bkmk_examples"></a> Exemplos  
 O exemplo a seguir ilustra como especificar o arquivo de script que contém o script [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET e os métodos do serviço Web que você quer executar.  
  
```  
rs -i c:\scriptfiles\script_copycontent.rss -s http://localhost/reportserver  
```  
  
 Para obter um exemplo detalhado, consulte [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md).  
  
 Para ver exemplos adicionais, consulte [Executar um arquivo de script do Reporting Services](run-a-reporting-services-script-file.md)  
  
## <a name="remarks"></a>Comentários  
 Você pode definir scripts para definir propriedades do sistema, publicar relatórios, e assim sucessivamente. Os scripts que você cria podem incluir qualquer método de API do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações sobre os métodos e propriedades disponíveis, consulte [Report Server Web Service](../report-server-web-service/report-server-web-service.md).  
  
 O script deve ser gravado no código [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET e armazenado em Unicode ou arquivo de texto UTF-8 com uma extensão de nome de arquivo .rss. Você não pode depurar scripts com o utilitário **rs** . Para depurar um script, execute o código no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
> [!TIP]  
>  Para obter um exemplo detalhado, consulte [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md).  
  
## <a name="see-also"></a>Consulte também  
 [Executar um arquivo de script do Reporting Services](run-a-reporting-services-script-file.md)   
 [Implantação de script e tarefas administrativas](script-deployment-and-administrative-tasks.md)   
 [Gerar scripts com o utilitário rs.exe e o serviço Web](script-with-the-rs-exe-utility-and-the-web-service.md)   
 [Utilitários de prompt de comando do servidor de relatório &#40;SSRS&#41;](report-server-command-prompt-utilities-ssrs.md)  
  
  
