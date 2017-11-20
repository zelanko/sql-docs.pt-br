---
title: "Gerando arquivos de despejo para execução do pacote | Microsoft Docs"
ms.custom: 
ms.date: 08/24/2016
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: troubleshooting
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 61ef1731-cb3a-4afb-b4a4-059b04aeade0
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 50f9efe65f14dbd73ccbc3c6e81307c3893c469f
ms.openlocfilehash: c2a77869c6735d5ff67e552abd6c2fc44209166f
ms.contentlocale: pt-br
ms.lasthandoff: 11/07/2017

---
# <a name="generating-dump-files-for-package-execution"></a>Gerando arquivos de despejo para execução de pacote
  No [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], você pode criar arquivos de despejo de depuração que fornecem informações sobre a execução de um pacote. As informações contidas nestes arquivos podem ajudá-lo a solucionar problemas de execução de pacote.  
  
> **OBSERVAÇÃO:** Os arquivos de despejo de depuração podem conter informações confidenciais. Para ajudar a proteger essas informações, você pode usar uma lista de controle de acesso (ACL) para restringir o acesso aos arquivos ou copiar os arquivos para uma pasta que tenha acesso restrito. Por exemplo, antes de enviar os arquivos de depuração para o serviço de suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] , recomendamos que você remova todas as informações confidenciais.  
  
 Ao implantar um projeto no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , você pode criar arquivos de despejo que especifiquem informações sobre a execução dos pacotes contidos no projeto. Quando o processo ISServerExec.exe termina, os arquivos de despejo são criados. Você pode especificar que um arquivo de despejo será criado quando erros ocorrerem durante a execução do pacote, selecionando a opção **Despejar quando ocorrerem erros** na caixa de diálogo **Executar Pacote** . Você também pode usar os seguintes procedimentos armazenados:  
  
-   [catalog.set_execution_parameter_value &#40;Banco de Dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
  
     Chame esse procedimento armazenado para configurar um arquivo de despejo a ser criado quando qualquer erro ou evento ocorrer, e quando eventos específicos ocorrerem, durante uma execução de pacote.  
  
-   [catalog.create_execution_dump](../../integration-services/system-stored-procedures/catalog-create-execution-dump.md)  
  
     Chame esse procedimento armazenado para pausar a execução de um pacote e criar um arquivo de despejo.  
  
 Se estiver usando o modelo de implantação de pacote, você criará os arquivos de despejo de depuração usando o utilitário **dtexec** ou **dtutil** para especificar uma opção de despejo de depuração na linha de comando. Para saber mais, veja [Utilitário dtexec](../../integration-services/packages/dtexec-utility.md) e [Utilitário dtutil](../../integration-services/dtutil-utility.md). Para obter mais informações sobre o modelo de implantação de pacote, consulte [Implantar projetos e pacotes do SSIS (Integration Services)](https://msdn.microsoft.com/library/hh213290.aspx) e [Implantação de pacote herdado &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md).   
  
## <a name="debug-dump-file-format"></a>Formato do arquivo de despejo de depuração  
 Ao especificar uma opção de despejo de depuração, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria os seguintes arquivos de despejo de depuração:  
  
-   Um arquivo de despejo de depuração .mdmp. Esse é um arquivo binário.  
  
-   O arquivo de despejo de depuração .tmp. Esse é um arquivo de texto formatado.  
  
 Por padrão, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] armazena esses arquivos na pasta,  *\<unidade >:*\Program Files\Microsoft Server\110\Shared\ErrorDumps de SQL.  
  
 A tabela a seguir descreve apenas algumas seções no arquivo .tmp. O arquivo .tmp inclui dados adicionais que não estão listados na tabela.  
  
|Tipo de informações|Description|Exemplo|  
|-------------------------|-----------------|-------------|  
|Ambiente|A versão do sistema operacional, os dados de uso da memória, a ID do processo e o nome da imagem do processo. As informações sobre o ambiente estão no começo do arquivo .tmp.|# Despejo Textual do SSIS realizado em 9/13/2007 1:50:34 PM<br /><br /> #PID 4120<br /><br /> #Nome da Imagem [C:\Arquivos de Programas\Microsoft SQL Server\110\DTS\Binn\DTExec.exe]<br /><br /> # OS major=6 minor=0 build=6000<br /><br /> # Em execução em 2 processadores amd64 em WOW64<br /><br /> # Memória: 58% em uso. Física: 845M/2044M  Paginação: 2404M/4095M (disp./total)|  
|Caminho e versão da DLL (Dynamic-link library)|Caminho e versão de cada DLL que o sistema carrega durante o processamento de um pacote.|# Módulo carregado: c:\bb\Sql\DTS\src\bin\debug\i386\DTExec.exe (10.0.1069.5)<br /><br /> # Módulo carregado: C:\Windows\SysWOW64\ntdll.dll (6.0.6000.16386)<br /><br /> # Módulo carregado: C:\Windows\syswow64\kernel32.dll (6.0.6000.16386)|  
|Mensagens recentes|Mensagens recentes emitidas pelo sistema. Inclui hora, tipo, descrição e ID de thread de cada mensagem.|[M:1]   Entrada de buffer de anel:              (*pRecord)<br /><br /> [D:2] <<\<CRingBufferLogging::RingBufferLoggingRecord >>> (@ 0282F1A8)<br /><br /> [E:3]         Carimbo de data/hora: 2007-09-13 13:50:32.786      (szTimeStamp)<br /><br /> [E:3]         ID de Thread: 2368           (ThreadID)<br /><br /> [E:3]         Nome do evento: OnError                        (EventName)<br /><br /> [E:3]         Nome da fonte:                (SourceName)<br /><br /> [E:3]         ID da fonte:                        (SourceID)<br /><br /> [E:3]         ID de execução:                 (ExecutionGUID)<br /><br /> [E:3]         Código de dados: -1073446879              (DataCode)<br /><br /> [E:3]         Descrição: o componente está ausente, não está registrado, não pode ser atualizado ou não tem as interfaces necessárias. As informações de contato desse componente são "".|  
  
## <a name="related-information"></a>Informações relacionadas  
 [Caixa de diálogo Executar Pacote](../../integration-services/packages/run-integration-services-ssis-packages.md#execute_package_dialog)  
  
  

