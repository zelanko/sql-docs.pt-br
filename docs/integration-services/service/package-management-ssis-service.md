---
title: "Gerenciamento de pacotes (servi&#231;o SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "11/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "pacotes do SQL Server Integration Services, gerenciando"
  - "pacotes [Integration Services], gerenciando"
  - "pacotes do Integration Services, gerenciando"
  - "armazenando pacotes"
  - "pasta Pacotes Armazenados"
  - "pacotes atuais"
  - "pasta Pacotes em Execução"
  - "informações de status [Integration Services]"
  - "Pacotes SSIS, gerenciando"
  - "armazenamento [Integration Services]"
  - "monitoramento [Integration Services], pacotes"
  - "Serviço do Integration Services, gerenciamento de pacotes"
  - "serviços [Integration Services], gerenciamento de pacotes"
ms.assetid: 0261ed9e-3b01-4e37-a9d4-d039c41029b6
caps.latest.revision: 59
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 57
---
# Gerenciamento de pacotes (servi&#231;o SSIS)
  O gerenciamento de pacotes envolve tarefas, inclusive as seguintes:  
  
-   Monitorando pacotes em execução  
  
-   Gerenciamento do armazenamento de pacotes  
  
-   Importação e exportação de pacotes  
  
> [!IMPORTANT]  
>  Esse tópico discute o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , um serviço do Windows para o gerenciamento de pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] dá suporte ao serviço para compatibilidade de versões anteriores com versões anteriores do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. A partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], você pode gerenciar objetos como pacotes no servidor do Integration Services.  
  
## Repositório de pacotes  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece duas pastas de nível superior para acessar pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]: **Pacotes em Execução** e **Pacotes Armazenados**. A pasta **Pacotes em Execução** lista os pacotes que estão sendo executados atualmente no servidor. A pasta **Pacotes Armazenados** lista os pacotes que são salvos no armazenamento de pacotes. Esses são os únicos pacotes que o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] gerencia. O repositório de pacotes pode consistir em um ou em ambos, o banco de dados msdb e as pastas do sistema de arquivos, listados no arquivo de configuração de serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. O arquivo de configuração especifica o msdb e as pastas do sistema de arquivos a serem gerenciados. Você também pode ter pacotes armazenados em outros lugares no sistema de arquivos que não são gerenciados pelo serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Os pacotes salvos no msdb são armazenados em uma tabela chamada sysssispackages. Quando você salva pacotes no msdb, também pode agrupá-los em pastas lógicas. O uso de pastas lógicas pode ajudar a organizar os pacotes por finalidade ou filtrar os pacotes na tabela sysssispackages. Você pode criar pastas lógicas por meio do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Por padrão, qualquer pasta lógica que você adicionar ao msdb será automaticamente incluída no repositório de pacotes.  
  
 As pastas lógicas criadas para o agrupamento de pacotes no msdb são representadas como linhas na tabela sysssispackagefolders do msdb. As colunas folderid e parentfolderid no sysssispackagefolders definem a hierarquia de pastas. As pastas raiz lógicas no msdb são as linhas do sysssispackagefolders que têm valores nulos na coluna parentfolderid. Para obter mais informações, consulte [sysssispackages &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysssispackages-transact-sql.md) e [sysssispackagefolders &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysssispackagefolders-transact-sql.md).  
  
 Ao abrir o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e se conectar ao [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], você verá as pastas do msdb gerenciadas pelo serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] listadas na pasta Pacotes Armazenados. Se o arquivo de configuração especificar pastas do sistema do arquivo raiz, a pasta Pacotes Armazenados também listará pacotes salvos no sistema de arquivos nessas pastas e em todas as subpastas.  
  
 Você pode armazenar pacotes em qualquer pasta do sistema de arquivos, mas eles não serão listados nas subpastas da pasta **Pacotes Armazenados** , a menos que você adicione a pasta à lista de pastas no arquivo de configuração para armazenamento de arquivos. Para obter mais informações sobre esse arquivo de configuração, veja [Configurando o Serviço Integration Services &#40;Serviço SSIS&#41;](../../integration-services/service/configuring-the-integration-services-service-ssis-service.md).  
  
 A pasta **Pacotes em Execução** não contém nenhuma subpasta e não é extensível.  
  
 Por padrão, a pasta **Pacotes Armazenados** contém duas pastas: **Sistema de Arquivos** e **MSDB**. A pasta **Sistema de Arquivos** lista os pacotes salvos no sistema de arquivos. O local desses arquivos é especificado no arquivo de configuração do serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . A pasta padrão é a pasta Pacotes, localizada em %Arquivos de Programas%\Microsoft SQL Server\100\DTS. A pasta **MSDB** lista os pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que foram salvos no banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do msdb no servidor. A tabela sysssispackages contém os pacotes salvos no msdb.  
  
 Para exibir a lista de pacotes no repositório de pacotes, você precisa abrir o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e conectar-se ao [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Para obter mais informações, consulte [Exibir pacotes do Integration Services no SQL Server Management Studio &#40;Serviço SSIS&#41;](../../integration-services/service/view-integration-services-packages-in-sql-server-management-studio-ssis-service.md).  
  
## Monitorando pacotes em execução  
 A pasta **Pacotes em Execução** lista os pacotes que estão sendo executados atualmente. Para visualizar as informações sobre pacotes existentes na página **Resumo** do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], clique na pasta **Pacotes em Execução** . Informações como a duração da execução dos pacotes em execução são listadas na página **Resumo** . Opcionalmente, atualize a pasta para exibir as informações mais recentes.  
  
 Para visualizar as informações sobre um único pacote em execução na página **Resumo** , clique no pacote. A página **Resumo** exibe informações como a versão e a descrição do pacote.  
  
 Você pode interromper um pacote em execução na pasta **Pacotes em Execução** clicando com o botão direito do mouse no pacote e clicando em **Parar**.  
  
## Gerenciamento do armazenamento de pacotes  
 Para organizar pacotes, você pode adicionar pastas personalizadas às pastas de repositório de pacotes de raiz que o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] lista em seu arquivo de configuração. Por padrão, as pastas raiz são as pastas **Sistema de Arquivos** e **MSDB** . Por exemplo, talvez você queira adicionar à pasta **Sistema de Arquivos** uma pasta **Limpeza de dados** que contém todos os pacotes usados para limpar dados. Você pode adicionar pastas personalizadas às pastas personalizadas, criando uma hierarquia de pastas aninhadas adequadas às suas necessidades. As pastas personalizadas podem ser excluídas e renomeadas; porém, você não pode renomear ou excluir as pastas raiz especificadas pelo arquivo de configuração. Para atualizar as pastas raiz que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] lista, você deve atualizar o arquivo de configuração.  
  
 Para obter mais informações, consulte [Configurando o serviço Integration Services &#40; Serviço SSIS&#41;](../../integration-services/service/configuring-the-integration-services-service-ssis-service.md).  
  
## Importação e exportação de pacotes  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Os pacotes podem ser salvos no banco de dados msdb ou no sistema de arquivos. Você pode copiar um pacote de um tipo de armazenamento para o outro com o recurso de importação ou exportação fornecido pelo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Você também pode importar um pacote para o mesmo tipo de armazenamento e dar ao pacote um nome diferente para criar uma cópia do pacote. O utilitário de prompt de comando **dtutil** (dtutil.exe) também pode ser usado para importar e exportar pacotes.  
  
 Para obter mais informações, consulte [dtutil Utility](../../integration-services/dtutil-utility.md).  
  
## Tarefas relacionadas  
  
-   [Importar e exportar pacotes &#40;Serviço SSIS&#41;](../../integration-services/service/import-and-export-packages-ssis-service.md)  
  
-   [Exibir pacotes do Integration Services no SQL Server Management Studio &#40;Serviço SSIS&#41;](../../integration-services/service/view-integration-services-packages-in-sql-server-management-studio-ssis-service.md)  
  
## Consulte também  
 [Serviço Integration Services &#40;Serviço SSIS&#41;](../../integration-services/service/integration-services-service-ssis-service.md)  
  
  