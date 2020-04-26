---
title: Gerar arquivos de despejo para execução de pacote | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 61ef1731-cb3a-4afb-b4a4-059b04aeade0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8022532dcb038b7c9a5839acb0541337ac3d5001
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/25/2020
ms.locfileid: "62766140"
---
# <a name="generating-dump-files-for-package-execution"></a>Gerando arquivos de despejo para execução de pacote
  No [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], você pode criar arquivos de despejo de depuração que fornecem informações sobre a execução de um pacote. As informações contidas nestes arquivos podem ajudá-lo a solucionar os problemas sobre a execução do pacote.  
  
> [!NOTE]  
>  Os arquivos de despejo de depuração podem conter informações confidenciais. Para ajudar a proteger essas informações, você pode usar uma lista de controle de acesso (ACL) para restringir o acesso aos arquivos ou copiar os arquivos para uma pasta que tenha acesso restrito. Por exemplo, antes de enviar os arquivos de depuração para o serviço de suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] , recomendamos que você remova todas as informações confidenciais.  
  
 Ao implantar um projeto no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , você pode criar arquivos de despejo que especifiquem informações sobre a execução dos pacotes contidos no projeto. Quando o processo ISServerExec.exe termina, os arquivos de despejo são criados. Você pode especificar que um arquivo de despejo será criado quando erros ocorrerem durante a execução do pacote, selecionando a opção **Despejar quando ocorrerem erros** na caixa de diálogo **Executar Pacote** . Você também pode usar os seguintes procedimentos armazenados:  
  
-   [catalog.set_execution_parameter_value &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database)  
  
     Chame esse procedimento armazenado para configurar um arquivo de despejo a ser criado quando qualquer erro ou evento ocorrer, e quando eventos específicos ocorrerem, durante uma execução de pacote.  
  
-   [catalog.create_execution_dump](/sql/integration-services/system-stored-procedures/catalog-create-execution-dump)  
  
     Chame esse procedimento armazenado para pausar a execução de um pacote e criar um arquivo de despejo.  
  
 Se for implantar pacotes que usam o modelo de implantação de pacote, você criará os arquivos de despejo de depuração usando o utilitário **dtexec** ou **dtutil** para especificar uma opção de despejo de depuração na linha de comando. Para saber mais, veja [Utilitário dtexec](../packages/dtexec-utility.md) e [Utilitário dtutil](../dtutil-utility.md). Para obter mais informações sobre o modelo de implantação de pacote, consulte [implantação de projetos e pacotes](../packages/deploy-integration-services-ssis-projects-and-packages.md) e [implantação de pacote &#40;SSIS&#41;](../packages/legacy-package-deployment-ssis.md).  
  
## <a name="debug-dump-file-format"></a>Formato do arquivo de despejo de depuração  
 Ao especificar uma opção de despejo de depuração, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria os seguintes arquivos de despejo de depuração:  
  
-   Um arquivo de despejo de depuração .mdmp. Esse é um arquivo binário.  
  
-   O arquivo de despejo de depuração .tmp. Esse é um arquivo de texto formatado.  
  
 Por padrão, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] o armazena esses arquivos na pasta, * \<unidade>:* \Program Files\Microsoft SQL Server\110\Shared\ErrorDumps.  
  
 A tabela a seguir descreve apenas algumas seções no arquivo .tmp. O arquivo .tmp inclui dados adicionais que não estão listados na tabela.  
  
|Tipo de informações|Descrição|Exemplo|  
|-------------------------|-----------------|-------------|  
|Ambiente|A versão do sistema operacional, os dados de uso da memória, a ID do processo e o nome da imagem do processo. As informações sobre o ambiente estão no começo do arquivo .tmp.|# Despejo Textual do SSIS realizado em 9/13/2007 1:50:34 PM<br /><br /> #PID 4120<br /><br /> #Nome da Imagem [C:\Arquivos de Programas\Microsoft SQL Server\110\DTS\Binn\DTExec.exe]<br /><br /> # OS major=6 minor=0 build=6000<br /><br /> # Em execução em 2 processadores amd64 em WOW64<br /><br /> # Memória: 58% em uso. Física: 845M/2044M  Paginação: 2404M/4095M (disp./total)|  
|Caminho e versão da DLL (Dynamic-link library)|Caminho e versão de cada DLL que o sistema carrega durante o processamento de um pacote.|# Módulo carregado: c:\bb\Sql\DTS\src\bin\debug\i386\DTExec.exe (10.0.1069.5)<br /><br /> # Módulo carregado: C:\Windows\SysWOW64\ntdll.dll (6.0.6000.16386)<br /><br /> # Módulo carregado: C:\Windows\syswow64\kernel32.dll (6.0.6000.16386)|  
|Mensagens recentes|Mensagens recentes emitidas pelo sistema. Inclui hora, tipo, descrição e ID de thread de cada mensagem.|[M:1]   Entrada de buffer de anel:              (*pRecord)<br /><br /> [D:2]      <<\<CRingBufferLogging::RingBufferLoggingRecord>>> ( \@ 0282F1A8 )<br /><br /> [E:3]         Carimbo de data/hora: 2007-09-13 13:50:32.786      (szTimeStamp)<br /><br /> [E:3]         ID de Thread: 2368           (ThreadID)<br /><br /> [E:3]         Nome do evento: OnError                        (EventName)<br /><br /> [E:3]         Nome da fonte:                (SourceName)<br /><br /> [E:3]         ID da fonte:                        (SourceID)<br /><br /> [E:3]         ID de execução:                 (ExecutionGUID)<br /><br /> [E:3]         Código de dados: -1073446879              (DataCode)<br /><br /> [E:3]         Descrição: o componente está ausente, não está registrado, não pode ser atualizado ou não tem as interfaces necessárias. As informações de contato desse componente são "".|  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Execute Package Dialog Box](../execute-package-dialog-box.md)  
  
  
